---
title: '자습서: R에서 클러스터링을 수행할 데이터 준비'
titleSuffix: SQL machine learning
description: 4부로 구성된 이 자습서 시리즈의 2부에서는 SQL 기계 학습을 사용하여 R에서 클러스터링을 수행하기 위해 데이터베이스의 데이터를 준비합니다.
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.reviewer: garye, davidph
ms.date: 05/21/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 1c6bf16d51d0180b56007f237001d01cedfecf8d
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870285"
---
# <a name="tutorial-prepare-data-to-perform-clustering-in-r-with-sql-machine-learning"></a>자습서: R에서 SQL 기계 학습을 사용하여 클러스터링을 수행하기 위한 데이터 준비
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
4부로 구성된 이 자습서 시리즈의 2부에서는 SQL Server Machine Learning Services 또는 빅 데이터 클러스터를 사용하여 R에서 클러스터링을 수행하기 위해 데이터베이스의 데이터를 준비합니다.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
4부로 구성된 이 자습서 시리즈의 2부에서는 SQL Server Machine Learning Services를 사용하여 R에서 클러스터링을 수행하기 위해 데이터베이스의 데이터를 준비합니다.
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
4부로 구성된 이 자습서 시리즈의 2부에서는 SQL Server 2016 R Services를 사용하여 R에서 클러스터링을 수행하기 위해 데이터베이스의 데이터를 준비합니다.
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
4부로 구성된 이 자습서 시리즈의 2부에서는 Azure SQL Managed Instance Machine Learning Services를 사용하여 R에서 클러스터링을 수행하기 위해 데이터베이스의 데이터를 준비합니다.
::: moniker-end

이 문서에서는 다음을 수행하는 방법을 알아봅니다.

> [!div class="checklist"]
> * R을 사용하여 다양한 기준에 따라 고객 분류
> * 데이터베이스의 데이터를 R 데이터 프레임에 로드

[1부](r-clustering-model-introduction.md)에서는 사전 요구 사항을 설치하고 샘플 데이터베이스를 복원했습니다.

[3부](r-clustering-model-build.md)에서는 R에서 K-평균 클러스터링 모델을 만들고 학습시키는 방법을 알아봅니다.

[4부](r-clustering-model-deploy.md)에서는 새 데이터를 기준으로 R에서 클러스터링을 수행할 수 있는 저장 프로시저를 데이터베이스에서 만드는 방법을 알아봅니다.

## <a name="prerequisites"></a>사전 요구 사항

* 이 자습서의 2부에서는 [**1부**](r-clustering-model-introduction.md)를 완료했다고 가정합니다.

## <a name="separate-customers"></a>개별 고객

RStudio에서 새 RScript 파일을 만든 후 다음 스크립트를 실행합니다.
SQL 쿼리에서 다음 기준에 따라 고객을 분류합니다.

* **orderRatio** = 반품 주문 비율(전체 주문 수 대비 부분 또는 전체적으로 반품된 주문 합계 수)
* **itemsRatio** = 반품 항목 비율(구입한 항목 수 대비 반품된 총 항목 수)
* **monetaryRatio** = 반품 금액 비율(구입한 금액 대비 반품된 항목의 총 금액)
* **frequency** = 반품 빈도

**connStr** 함수에서 **ServerName** 을 해당하는 연결 정보로 바꿉니다.

```r
# Define the connection string to connect to the tpcxbb_1gb database

connStr <- "Driver=SQL Server;Server=ServerName;Database=tpcxbb_1gb;uid=Username;pwd=Password"

#Define the query to select data
input_query <- "
SELECT ss_customer_sk AS customer
    ,round(CASE 
            WHEN (
                       (orders_count = 0)
                    OR (returns_count IS NULL)
                    OR (orders_count IS NULL)
                    OR ((returns_count / orders_count) IS NULL)
                    )
                THEN 0.0
            ELSE (cast(returns_count AS NCHAR(10)) / orders_count)
            END, 7) AS orderRatio
    ,round(CASE 
            WHEN (
                     (orders_items = 0)
                  OR (returns_items IS NULL)
                  OR (orders_items IS NULL)
                  OR ((returns_items / orders_items) IS NULL)
                 )
            THEN 0.0
            ELSE (cast(returns_items AS NCHAR(10)) / orders_items)
            END, 7) AS itemsRatio
    ,round(CASE 
            WHEN (
                     (orders_money = 0)
                  OR (returns_money IS NULL)
                  OR (orders_money IS NULL)
                  OR ((returns_money / orders_money) IS NULL)
                 )
            THEN 0.0
            ELSE (cast(returns_money AS NCHAR(10)) / orders_money)
            END, 7) AS monetaryRatio
    ,round(CASE 
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
    ) returned ON ss_customer_sk = sr_customer_sk";
```

## <a name="load-the-data-into-a-data-frame"></a>데이터 프레임에 데이터 로드

이제 다음 스크립트를 사용하여 쿼리 결과를 R 데이터 프레임에 반환합니다.

```r
# Query using input_query and get the results back
# to data frame customer_data

library(RODBC)

ch <- odbcDriverConnect(connStr)

customer_data <- sqlQuery(ch, input_query)

# Take a look at the data just loaded
head(customer_data, n = 5);
```

다음과 비슷한 결과가 표시됩니다.

```results
  customer orderRatio itemsRatio monetaryRatio frequency
1    29727          0          0      0.000000         0
2    26429          0          0      0.041979         1
3    60053          0          0      0.065762         3
4    97643          0          0      0.037034         3
5    32549          0          0      0.031281         4
```

## <a name="clean-up-resources"></a>리소스 정리

이 자습서를 계속 진행할 생각이 없으면 tpcxbb_1gb 데이터베이스를 삭제하세요.

## <a name="next-steps"></a>다음 단계

이 자습서 시리즈의 2부에서는 다음 작업을 수행하는 방법을 알아보았습니다.

* R을 사용하여 다양한 기준에 따라 고객 분류
* 데이터베이스의 데이터를 R 데이터 프레임에 로드

이 고객 데이터를 사용하는 기계 학습 모델을 만들려면 다음 자습서 시리즈의 3부를 따르세요.

> [!div class="nextstepaction"]
> [R에서 SQL 기계 학습을 사용하여 예측 모델 만들기](r-clustering-model-build.md)
