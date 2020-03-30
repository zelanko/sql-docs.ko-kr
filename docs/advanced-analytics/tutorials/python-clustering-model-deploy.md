---
title: 'Python 자습서: 클러스터 모델 배포'
description: 4부로 구성된 이 자습서 시리즈의 4부에서는 Python에서 SQL Server Machine Learning Services를 사용하여 클러스터링 모델을 배포합니다.
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/27/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: df0fd7cb27977679a6ca879d7ae01045ed3fa8c8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "73727141"
---
# <a name="tutorial-deploy-a-model-in-python-to-categorize-customers-with-sql-server-machine-learning-services"></a>자습서: Python에서 SQL Server Machine Learning Services를 사용하여 고객을 분류하기 위한 모델 배포

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 4부로 구성된 자습서 시리즈의 4부에서는 Machine Learning Services를 사용하여 Python에서 개발한 클러스터링 모델을 SQL 데이터베이스에 배포합니다.

새 고객이 계속 등록되므로 정기적으로 클러스터링을 수행하기 위해서는 어떤 앱에서든 Python 스크립트를 호출할 수 있어야 합니다. 이를 위해서는 데이터베이스에서 SQL 저장 프로시저 내에 Python 스크립트를 저장하여 SQL Server에서 Python 스크립트를 배포할 수 있습니다. 모델이 SQL 데이터베이스에서 실행되기 때문에 데이터베이스에 저장된 데이터에 대해 쉽게 학습을 수행할 수 있습니다.

이 섹션에서는 바로 전에 작성한 Python 코드를 SQL Server로 이동하고 SQL Server Machine Learning Services를 사용해서 클러스터링을 배포합니다.

이 문서에서는 다음을 수행하는 방법을 알아봅니다.

> [!div class="checklist"]
> * 모델을 생성하는 저장 프로시저 만들기
> * SQL Server에서 클러스터링 수행
> * 클러스터링 정보 사용

[1부](python-clustering-model.md)에서는 사전 요구 사항을 설치하고 샘플 데이터베이스를 복원했습니다.

[2부](python-clustering-model-prepare-data.md)에서는 클러스터링을 수행하기 위해 SQL 데이터베이스의 데이터를 준비하는 방법을 배웠습니다.

[3부](python-clustering-model-build.md)에서는 Python에서 K-평균 클러스터링 모델을 만들고 학습시키는 방법을 배웠습니다.

## <a name="prerequisites"></a>사전 요구 사항

* 이 자습서 시리즈의 4부에서는 [**1부**](python-clustering-model.md)의 사전 요구 사항을 수행하고 [**2부**](python-clustering-model-prepare-data.md) 및 [**3부**](python-clustering-model-build.md)의 단계를 완료했다고 가정합니다.

## <a name="create-a-stored-procedure-that-generates-the-model"></a>모델을 생성하는 저장 프로시저 만들기

다음 T-SQL 스크립트를 실행하여 저장 프로시저를 만듭니다. 이 절차는 이 자습서 시리즈의 1부 및 2부에서 개발한 단계를 다시 만듭니다.

* 구매 및 반품 기록을 기준으로 고객 분류
* K-평균 알고리즘을 사용하여 4가지 고객 클러스터 생성

```sql
USE [tpcxbb_1gb]
GO

CREATE procedure [dbo].[py_generate_customer_return_clusters]
AS

BEGIN
    DECLARE

-- Input query to generate the purchase history & return metrics
     @input_query NVARCHAR(MAX) = N'
SELECT
  ss_customer_sk AS customer,
  CAST( (ROUND(COALESCE(returns_count / NULLIF(1.0*orders_count, 0), 0), 7) ) AS FLOAT) AS orderRatio,
  CAST( (ROUND(COALESCE(returns_items / NULLIF(1.0*orders_items, 0), 0), 7) ) AS FLOAT) AS itemsRatio,
  CAST( (ROUND(COALESCE(returns_money / NULLIF(1.0*orders_money, 0), 0), 7) ) AS FLOAT) AS monetaryRatio,
  CAST( (COALESCE(returns_count, 0)) AS FLOAT) AS frequency
FROM
  (
    SELECT
      ss_customer_sk,
      -- return order ratio
      COUNT(distinct(ss_ticket_number)) AS orders_count,
      -- return ss_item_sk ratio
      COUNT(ss_item_sk) AS orders_items,
      -- return monetary amount ratio
      SUM( ss_net_paid ) AS orders_money
    FROM store_sales s
    GROUP BY ss_customer_sk
  ) orders
  LEFT OUTER JOIN
  (
    SELECT
      sr_customer_sk,
      -- return order ratio
      count(distinct(sr_ticket_number)) as returns_count,
      -- return ss_item_sk ratio
      COUNT(sr_item_sk) as returns_items,
      -- return monetary amount ratio
      SUM( sr_return_amt ) AS returns_money
    FROM store_returns
    GROUP BY sr_customer_sk
  ) returned ON ss_customer_sk=sr_customer_sk
 '

EXEC sp_execute_external_script
      @language = N'Python'
    , @script = N'

import pandas as pd
from sklearn.cluster import KMeans

#get data from input query
customer_data = my_input_data

#We concluded in step 2 in the tutorial that 4 would be a good number of clusters
n_clusters = 4

#Perform clustering
est = KMeans(n_clusters=n_clusters, random_state=111).fit(customer_data[["orderRatio","itemsRatio","monetaryRatio","frequency"]])
clusters = est.labels_
customer_data["cluster"] = clusters

OutputDataSet = customer_data
'
    , @input_data_1 = @input_query
    , @input_data_1_name = N'my_input_data'
             with result sets (("Customer" int, "orderRatio" float,"itemsRatio" float,"monetaryRatio" float,"frequency" float,"cluster" float));
END;
GO
```

## <a name="perform-clustering-in-sql-database"></a>SQL 데이터베이스에서 클러스터링 수행

이제 저장 프로시저를 만들었으므로, 이 프로시저를 사용해서 다음 스크립트를 실행하여 클러스터링을 수행합니다.

```sql
--Create a table to store the predictions in

DROP TABLE IF EXISTS [dbo].[py_customer_clusters];
GO

CREATE TABLE [dbo].[py_customer_clusters] (
    [Customer] [bigint] NULL
  , [OrderRatio] [float] NULL
  , [itemsRatio] [float] NULL
  , [monetaryRatio] [float] NULL
  , [frequency] [float] NULL
  , [cluster] [int] NULL
  ,
    ) ON [PRIMARY]
GO

--Execute the clustering and insert results into table
INSERT INTO py_customer_clusters
EXEC [dbo].[py_generate_customer_return_clusters];

-- Select contents of the table to verify it works
SELECT * FROM py_customer_clusters;
```

## <a name="use-the-clustering-information"></a>클러스터링 정보 사용

데이터베이스에 클러스터링 프로시저를 저장했으므로 동일한 데이터베이스에 저장된 고객 데이터에 대해 효율적으로 클러스터링을 수행할 수 있습니다. 고객 데이터가 업데이트될 때마다 프로시저를 수행하고, 업데이트된 클러스터링 정보를 사용할 수 있습니다.

비활성 상태의 그룹인 클러스터 0의 고객들에게 판촉 이메일을 보낸다고 가정해보세요(4개 클러스터에 대한 설명은 이 자습서의 [3부](python-clustering-model-build.md#analyze-the-results) 참조). 다음 코드는 클러스터 0에 해당하는 고객들의 이메일 주소를 선택합니다.

```sql
USE [tpcxbb_1gb]
--Get email addresses of customers in cluster 0 for a promotion campaign
SELECT customer.[c_email_address], customer.c_customer_sk
  FROM dbo.customer
  JOIN
  [dbo].[py_customer_clusters] as c
  ON c.Customer = customer.c_customer_sk
  WHERE c.cluster = 0
```

**c.cluster** 값을 바꿔서 다른 클러스터의 고객들에 대한 이메일 주소를 반환할 수 있습니다.

## <a name="clean-up-resources"></a>리소스 정리

이 자습서를 완료했으면, SQL Server에서 tpcxbb_1gb 데이터베이스를 삭제할 수 있습니다.

## <a name="next-steps"></a>다음 단계

이 자습서 시리즈의 4부에서는 다음 단계를 완료했습니다.

* 모델을 생성하는 저장 프로시저 만들기
* SQL Server에서 클러스터링 수행
* 클러스터링 정보 사용

SQL Server Machine Learning Services에서 Python을 사용하는 방법에 대한 자세한 내용은 다음을 참조하세요.

* [빠른 시작: SQL Server Machine Learning Services를 사용하여 간단한 Python 스크립트 만들기 및 실행](quickstart-python-create-script.md)
* [SQL Server Machine Learning Services를 위한 다른 Python 자습서](sql-server-python-tutorials.md)
* [sqlmlutils를 사용하여 Python 패키지 설치](../package-management/install-additional-python-packages-on-sql-server.md)

