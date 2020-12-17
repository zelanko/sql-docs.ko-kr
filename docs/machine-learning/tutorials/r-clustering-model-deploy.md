---
title: '자습서: R에서 클러스터링 모델 배포'
titleSuffix: SQL machine learning
description: 4부로 구성된 이 자습서 시리즈의 4부에서는 R에서 SQL 기계 학습을 사용하여 클러스터링 모델을 배포합니다.
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.reviewer: garye, davidph
ms.date: 05/21/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current'
ms.openlocfilehash: 35a2b00b671d70849de0c191aae113ce1635b68c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470204"
---
# <a name="tutorial-deploy-a-clustering-model-in-r-with-sql-machine-learning"></a>자습서: R에서 SQL 기계 학습을 사용하여 클러스터링 모델 배포
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
4부로 구성된 이 자습서 시리즈의 4부에서는 R에서 개발한 클러스터링 모델을 SQL Server Machine Learning Services 또는 빅 데이터 클러스터를 사용하여 데이터베이스에 배포합니다.
::: moniker-end
::: moniker range="=sql-server-2017"
4부로 구성된 이 자습서 시리즈의 4부에서는 R에서 개발한 클러스터링 모델을 SQL Server Machine Learning Services를 사용하여 데이터베이스에 배포합니다.
::: moniker-end
::: moniker range="=sql-server-2016"
4부로 구성된 이 자습서 시리즈의 4부에서는 R에서 개발한 클러스터링 모델을 SQL Server R Services를 사용하여 데이터베이스에 배포합니다.
::: moniker-end
::: moniker range="=azuresqldb-mi-current"
4부로 구성된 이 자습서 시리즈의 4부에서는 R에서 개발한 클러스터링 모델을 Azure SQL Managed Instance Machine Learning Services를 사용하여 데이터베이스에 배포합니다.
::: moniker-end

새 고객이 계속 등록되므로 정기적으로 클러스터링을 수행하려면 어떤 앱에서든 R 스크립트를 호출할 수 있어야 합니다. 그러려면 SQL 저장 프로시저 내부에 Python 스크립트를 배치하여 데이터베이스에 R 스크립트를 배포하면 됩니다. 모델이 데이터베이스에서 실행되기 때문에 데이터베이스에 저장된 데이터에 대해 쉽게 학습시킬 수 있습니다.

이 문서에서는 다음을 수행하는 방법을 알아봅니다.

> [!div class="checklist"]
> * 모델을 생성하는 저장 프로시저 만들기
> * 클러스터링 수행
> * 클러스터링 정보 사용

[1부](r-clustering-model-introduction.md)에서는 사전 요구 사항을 설치하고 샘플 데이터베이스를 복원했습니다.

[2부](r-clustering-model-prepare-data.md)에서는 클러스터링을 수행하기 위해 데이터베이스의 데이터를 준비하는 방법을 배웠습니다.

[3부](r-clustering-model-build.md)에서는 R에서 K-평균 클러스터링 모델을 만들고 학습시키는 방법을 배웠습니다.

## <a name="prerequisites"></a>사전 요구 사항

* 이 자습서 시리즈의 4부에서는 [**1부**](r-clustering-model-introduction.md)의 사전 요구 사항을 수행하고 [**2부**](r-clustering-model-build.md) 및 [**3부**](r-clustering-model-build.md)의 단계를 완료했다고 가정합니다.

## <a name="create-a-stored-procedure-that-generates-the-model"></a>모델을 생성하는 저장 프로시저 만들기

다음 T-SQL 스크립트를 실행하여 저장 프로시저를 만듭니다. 이 프로시저는 이 자습서 시리즈의 2부 및 3부에서 개발한 단계를 다시 만듭니다.

* 구매 및 반품 기록을 기준으로 고객 분류
* K-평균 알고리즘을 사용하여 4가지 고객 클러스터 생성

이 프로시저는 이전 작업의 결과로 얻은 고객 클러스터 매핑을 데이터베이스 테이블 **customer_return_clusters** 에 저장합니다.

```sql
USE [tpcxbb_1gb]
DROP PROC IF EXISTS generate_customer_return_clusters;
GO
CREATE procedure [dbo].[generate_customer_return_clusters]
AS
/*
  This procedure uses R to classify customers into different groups
  based on their purchase & return history.
*/
BEGIN
    DECLARE @duration FLOAT
    , @instance_name NVARCHAR(100) = @@SERVERNAME
    , @database_name NVARCHAR(128) = db_name()
-- Input query to generate the purchase history & return metrics
    , @input_query NVARCHAR(MAX) = N'
SELECT ss_customer_sk AS customer,
    round(CASE 
            WHEN (
                    (orders_count = 0)
                    OR (returns_count IS NULL)
                    OR (orders_count IS NULL)
                    OR ((returns_count / orders_count) IS NULL)
                    )
                THEN 0.0
            ELSE (cast(returns_count AS NCHAR(10)) / orders_count)
            END, 7) AS orderRatio,
    round(CASE 
            WHEN (
                    (orders_items = 0)
                    OR (returns_items IS NULL)
                    OR (orders_items IS NULL)
                    OR ((returns_items / orders_items) IS NULL)
                    )
                THEN 0.0
            ELSE (cast(returns_items AS NCHAR(10)) / orders_items)
            END, 7) AS itemsRatio,
    round(CASE 
            WHEN (
                    (orders_money = 0)
                    OR (returns_money IS NULL)
                    OR (orders_money IS NULL)
                    OR ((returns_money / orders_money) IS NULL)
                    )
                THEN 0.0
            ELSE (cast(returns_money AS NCHAR(10)) / orders_money)
            END, 7) AS monetaryRatio,
    round(CASE 
            WHEN (returns_count IS NULL)
                THEN 0.0
            ELSE returns_count
            END, 0) AS frequency
FROM (
    SELECT ss_customer_sk,
        -- return order ratio
        COUNT(DISTINCT (ss_ticket_number)) AS orders_count,
        -- return ss_item_sk ratio
        COUNT(ss_item_sk) AS orders_items,
        -- return monetary amount ratio
        SUM(ss_net_paid) AS orders_money
    FROM store_sales s
    GROUP BY ss_customer_sk
    ) orders
LEFT OUTER JOIN (
    SELECT sr_customer_sk,
        -- return order ratio
        count(DISTINCT (sr_ticket_number)) AS returns_count,
        -- return ss_item_sk ratio
        COUNT(sr_item_sk) AS returns_items,
        -- return monetary amount ratio
        SUM(sr_return_amt) AS returns_money
    FROM store_returns
    GROUP BY sr_customer_sk
    ) returned ON ss_customer_sk = sr_customer_sk
 '
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N'
# Define the connection string

connStr <- paste("Driver=SQL Server; Server=", instance_name,
                 "; Database=", database_name,
                 "; uid=Username;pwd=Password; ",
                 sep="" )

# Input customer data that needs to be classified.
# This is the result we get from the query.
library(RODBC)

ch <- odbcDriverConnect(connStr);

customer_data <- sqlQuery(ch, input_query)

sqlDrop(ch, "customer_return_clusters")

## create clustering model
clust <- kmeans(customer_data[,2:5],4)

## create clustering output for table
customer_cluster <- data.frame(cluster=clust$cluster,customer=customer_data$customer,orderRatio=customer_data$orderRatio,
            itemsRatio=customer_data$itemsRatio,monetaryRatio=customer_data$monetaryRatio,frequency=customer_data$frequency)

## write cluster output to DB table
sqlSave(ch, customer_cluster, tablename = "customer_return_clusters")

## clean up
odbcClose(ch)
'
    , @input_data_1 = N''
    , @params = N'@instance_name nvarchar(100), @database_name nvarchar(128), @input_query nvarchar(max), @duration float OUTPUT'
    , @instance_name = @instance_name
    , @database_name = @database_name
    , @input_query = @input_query
    , @duration = @duration OUTPUT;
END;

GO
```

## <a name="perform-clustering"></a>클러스터링 수행

저장 프로시저를 만들었으므로, 이제 다음 스크립트를 실행하여 클러스터링을 수행합니다.

```sql
--Empty table of the results before running the stored procedure
TRUNCATE TABLE customer_return_clusters;

--Execute the clustering
--This will load the table customer_return_clusters with cluster mappings
EXECUTE [dbo].[generate_customer_return_clusters];
```

스크립트가 제대로 작동하는지, 실제로 고객 목록과 클러스터 매핑이 생기는지 확인합니다.

```sql
--Select data from table customer_return_clusters
--to verify that the clustering data was loaded
SELECT TOP (5) *
FROM customer_return_clusters;
```

```result
cluster  customer  orderRatio  itemsRatio  monetaryRatio  frequency
1        29727     0           0           0              0
4        26429     0           0           0.041979       1
2        60053     0           0           0.065762       3
2        97643     0           0           0.037034       3
2        32549     0           0           0.031281       4
```

## <a name="use-the-clustering-information"></a>클러스터링 정보 사용

데이터베이스에 클러스터링 프로시저를 저장했으므로 동일한 데이터베이스에 저장된 고객 데이터에 대해 효율적으로 클러스터링을 수행할 수 있습니다. 고객 데이터가 업데이트될 때마다 프로시저를 수행하고, 업데이트된 클러스터링 정보를 사용할 수 있습니다.

비활성 상태의 그룹인 클러스터 0의 고객들에게 판촉 이메일을 보낸다고 가정해보세요(4개 클러스터에 대한 설명은 이 자습서의 [3부](r-clustering-model-build.md#analyze-the-results) 참조). 다음 코드는 클러스터 0에 해당하는 고객들의 이메일 주소를 선택합니다.

```sql
USE [tpcxbb_1gb]
--Get email addresses of customers in cluster 0 for a promotion campaign
SELECT customer.[c_email_address], customer.c_customer_sk
  FROM dbo.customer
  JOIN
  [dbo].[customer_clusters] as c
  ON c.Customer = customer.c_customer_sk
  WHERE c.cluster = 0
```

**c.cluster** 값을 바꿔서 다른 클러스터의 고객들에 대한 이메일 주소를 반환할 수 있습니다.

## <a name="clean-up-resources"></a>리소스 정리

이 자습서를 마쳤으면 tpcxbb_1gb 데이터베이스를 삭제해도 됩니다.

## <a name="next-steps"></a>다음 단계

이 자습서 시리즈의 4부에서는 다음 작업을 수행하는 방법을 알아보았습니다.

* 모델을 생성하는 저장 프로시저 만들기
* SQL 기계 학습을 사용하여 클러스터링 수행
* 클러스터링 정보 사용

Machine Learning Services에서 R을 사용하는 방법에 대한 자세한 내용은 다음을 참조하세요.

* [간단한 R 스크립트 실행](quickstart-r-create-script.md)
* [R 데이터 구조, 형식 및 개체](quickstart-r-data-types-and-objects.md)
* [R 함수](quickstart-r-functions.md)
