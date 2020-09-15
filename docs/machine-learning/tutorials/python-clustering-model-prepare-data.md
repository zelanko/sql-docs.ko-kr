---
title: 'Python 자습서: 클러스터 데이터 준비'
titleSuffix: SQL machine learning
description: 4부로 구성된 이 자습서 시리즈의 2부에서는 Python에서 SQL 기계 학습을 사용하여 클러스터링을 수행하기 위한 SQL 데이터를 준비합니다.
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 05/21/2020
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: e6265a25a4a218e15e39c1f6a7163dbb6a958f32
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88173427"
---
# <a name="python-tutorial-prepare-data-to-categorize-customers-with-sql-machine-learning"></a>Python 자습서: SQL 기계 학습을 사용하여 고객을 분류하는 데이터 준비
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
4부로 구성된 이 자습서 시리즈의 2부에서는 Python을 사용하여 데이터베이스의 데이터를 복원하고 준비합니다. 이 시리즈의 후반부에서는 Python에서 SQL Server Machine Learning Services 또는 빅 데이터 클러스터를 사용하여 이 데이터로 클러스터링 모델을 학습시키고 배포합니다.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
4부로 구성된 이 자습서 시리즈의 2부에서는 Python을 사용하여 데이터베이스의 데이터를 복원하고 준비합니다. 이 시리즈의 후반부에서는 이 데이터를 사용하여 SQL Server Machine Learning Services와 함께 Python에서 클러스터링 모델을 학습시키고 배포합니다.
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
4부로 구성된 이 자습서 시리즈의 2부에서는 Python을 사용하여 데이터베이스의 데이터를 복원하고 준비합니다. 이 시리즈의 후반부에서는 이 데이터를 사용하여 Azure SQL Managed Instance Machine Learning Services와 함께 Python에서 클러스터링 모델을 학습시키고 배포합니다.
::: moniker-end

이 문서에서는 다음을 수행하는 방법을 알아봅니다.

> [!div class="checklist"]
> * Python을 사용하여 다양한 차원에 따라 고객 구분
> * 데이터베이스의 데이터를 Python 데이터 프레임에 로드

[1부](python-clustering-model.md)에서는 사전 요구 사항을 설치하고 샘플 데이터베이스를 복원했습니다.

[3부](python-clustering-model-build.md)에서는 Python에서 K-평균 클러스터링 모델을 만들고 학습시키는 방법을 알아봅니다.

[4부](python-clustering-model-deploy.md)에서는 새 데이터를 기준으로 Python에서 클러스터링을 수행할 수 있는 저장 프로시저를 데이터베이스에서 만드는 방법을 알아봅니다.

## <a name="prerequisites"></a>사전 요구 사항

* 이 자습서의 2부에서는 [**1부**](python-clustering-model.md)의 필수 구성 요소를 충족했다고 가정합니다.

## <a name="separate-customers"></a>개별 고객

클러스터링 고객을 준비하려면 먼저 다음 차원에 따라 고객을 구분합니다.

* **orderRatio** = 반품 주문 비율(전체 주문 수 대비 부분 또는 전체적으로 반품된 주문 합계 수)
* **itemsRatio** = 반품 항목 비율(구입한 항목 수 대비 반품된 총 항목 수)
* **monetaryRatio** = 반품 금액 비율(구입한 금액 대비 반품된 항목의 총 금액)
* **frequency** = 반품 빈도

Azure Data Studio에서 새 Notebook을 열고 다음 스크립트를 입력합니다.

연결 문자열에서 필요에 따라 연결 세부 정보를 바꿉니다.

```python
# Load packages.
import pyodbc
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
from scipy.spatial import distance as sci_distance
from sklearn import cluster as sk_cluster

################################################################################################

## Connect to DB and select data

################################################################################################

# Connection string to connect to SQL Server named instance.
conn_str = pyodbc.connect('DRIVER={ODBC Driver 17 for SQL Server}; SERVER=<server>; DATABASE=tpcxbb_1gb; UID=<username>; PWD=<password>')

input_query = '''SELECT
ss_customer_sk AS customer,
ROUND(COALESCE(returns_count / NULLIF(1.0*orders_count, 0), 0), 7) AS orderRatio,
ROUND(COALESCE(returns_items / NULLIF(1.0*orders_items, 0), 0), 7) AS itemsRatio,
ROUND(COALESCE(returns_money / NULLIF(1.0*orders_money, 0), 0), 7) AS monetaryRatio,
COALESCE(returns_count, 0) AS frequency
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
GROUP BY sr_customer_sk ) returned ON ss_customer_sk=sr_customer_sk'''


# Define the columns we wish to import.
column_info = {
    "customer": {"type": "integer"},
    "orderRatio": {"type": "integer"},
    "itemsRatio": {"type": "integer"},
    "frequency": {"type": "integer"}
}
```

## <a name="load-the-data-into-a-data-frame"></a>데이터 프레임에 데이터 로드

쿼리의 결과는 Pandas **read_sql** 함수를 사용하여 Python으로 반환됩니다. 프로세스의 일부로 이전 스크립트에서 정의한 열 정보를 사용합니다.

```python
customer_data = pandas.read_sql(input_query, conn_str)
```

이제 데이터 프레임의 시작 부분을 표시하여 올바르게 보이는지 확인합니다.

```python
print("Data frame:", customer_data.head(n=5))
```

```results
Rows Read: 37336, Total Rows Processed: 37336, Total Chunk Time: 0.172 seconds
Data frame:     customer  orderRatio  itemsRatio  monetaryRatio  frequency
0    29727.0    0.000000    0.000000       0.000000          0
1    97643.0    0.068182    0.078176       0.037034          3
2    57247.0    0.000000    0.000000       0.000000          0
3    32549.0    0.086957    0.068657       0.031281          4
4     2040.0    0.000000    0.000000       0.000000          0
```

## <a name="clean-up-resources"></a>리소스 정리

이 자습서를 계속 진행할 생각이 없으면 tpcxbb_1gb 데이터베이스를 삭제하세요.

## <a name="next-steps"></a>다음 단계

이 자습서 시리즈의 2부에서 다음 단계를 완료했습니다.

* Python을 사용하여 다양한 차원에 따라 고객 구분
* 데이터베이스의 데이터를 Python 데이터 프레임에 로드

이 고객 데이터를 사용하는 기계 학습 모델을 만들려면 다음 자습서 시리즈의 3부를 따르세요.

> [!div class="nextstepaction"]
> [Python 자습서: 예측 모델 만들기](python-clustering-model-build.md)
