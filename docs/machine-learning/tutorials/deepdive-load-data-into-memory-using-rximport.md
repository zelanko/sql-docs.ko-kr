---
title: rxImport를 사용하여 데이터 로드
description: SQL Server에서 데이터를 가져온 다음, rxImport 함수를 사용하여 관심 있는 데이터를 로컬 파일에 저장하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7c31650525934b14bf31135264d9b86c52d85119
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179950"
---
# <a name="load-data-into-memory-using-rximport-sql-server-and-revoscaler-tutorial"></a>rxImport를 사용하여 메모리에 데이터 로드(SQL Server 및 RevoScaleR 자습서)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

이것은 SQL Server에서 [RevoScaleR 함수](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)를 사용하는 방법에 대한 [RevoScaleR 자습서 시리즈](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 중 자습서 10에 해당됩니다.

이 자습서에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터를 가져온 다음, **rxImport** 함수를 사용하여 관심 있는 데이터를 로컬 파일에 저장하는 방법을 알아봅니다. 이렇게 하면 데이터베이스를 다시 쿼리하지 않고도 로컬 컴퓨팅 컨텍스트에서 반복하여 데이터를 분석할 수 있습니다.

[rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) 함수를 사용하여 데이터 원본의 데이터를 세션 메모리의 데이터 프레임 또는 디스크의 XDF 파일로 이동할 수 있습니다. 파일을 대상으로 지정하지 않으면 데이터는 메모리에 데이터 프레임으로 저장됩니다.

## <a name="extract-a-subset-of-data-from-sql-server-to-local-memory"></a>SQL Server에서 로컬 메모리로 데이터 하위 집합 추출

고위험 개인만 자세히 검사하기로 결정했습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 원본 테이블이 크므로 고위험 고객에 대한 정보만 가져올 수 있습니다. 그런 다음, 해당 데이터를 로컬 워크스테이션의 메모리에 있는 데이터 프레임에 로드합니다.

1. 컴퓨팅 컨텍스트를 로컬 워크스테이션으로 다시 설정합니다.

    ```R
    rxSetComputeContext("local")
    ```

2. *sqlQuery* 매개 변수에 유효한 SQL 문을 제공하는 새 SQL Server 데이터 원본 개체를 만듭니다. 이 예제에서는 위험 점수가 가장 높은 관찰의 하위 집합을 가져옵니다. 이렇게 하면 필요한 데이터만 로컬 메모리에 저장됩니다.

    ```R
    sqlServerProbDS \<- RxSqlServerData(
        sqlQuery = paste("SELECT * FROM ccScoreOutput2",
        "WHERE (ccFraudProb > .99)"),
        connectionString = sqlConnString)
    ```

3. [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) 함수를 호출하여 로컬 R 세션의 데이터 프레임으로 데이터를 읽습니다.

    ```R
    highRisk <- rxImport(sqlServerProbDS)
    ```

    작업에 성공하면 다음과 같은 상태 메시지가 표시됩니다. "행 읽기: 35, 총 처리된 행: 35, 총 청크 시간: 0.036초"

4. 이제 고위험 관찰이 메모리 내 데이터 프레임에 있으므로 다양한 R 함수를 사용하여 데이터 프레임을 조작할 수 있습니다. 예를 들어 고객의 위험 점수를 기준으로 고객 순서를 매기고 가장 위험도가 높은 고객 목록을 인쇄할 수 있습니다.

    ```R
    orderedHighRisk <- highRisk[order(-highRisk$ccFraudProb),]
    row.names(orderedHighRisk) <- NULL
    head(orderedHighRisk)
    ```

**결과**

```R
ccFraudLogitScore   state gender cardholder balance numTrans numIntlTrans creditLine ccFraudProb1
9.786345    SD   Male  Principal   23456       25            5 75   0.99994382
9.433040    FL Female  Principal   20629       24           28 75   0.99992003
8.556785    NY Female  Principal   19064       82           53 43   0.99980784
8.188668    AZ Female  Principal   19948       29            0 75   0.99972235
7.551699    NY Female  Principal   11051       95            0 75   0.99947516
7.335080    NV   Male  Principal   21566        4            6  75   0.9993482
```

## <a name="more-about-rximport"></a>rxImport 대한 자세한 정보

**rxImport** 를 사용하여 데이터 이동은 물론 데이터를 읽는 동안 데이터를 변환할 수도 있습니다. 예를 들어 고정 너비 열에 대해 문자 수를 지정하고, 변수에 대한 설명을 제공하고, 요소 열에 대한 수준을 설정하고, 가져온 후 사용할 새로운 수준을 만들 수 있습니다.

**rxImport** 함수는 가져오는 동안 열에 변수 이름을 할당하지만 *colInfo* 매개 변수를 사용하여 새 변수 이름을 지정하거나 *colClasses* 매개 변수를 사용하여 데이터 형식을 변경할 수 있습니다.

*transforms* 매개 변수에서 추가 작업을 지정하여 읽은 각 데이터 청크에 대한 기본 처리를 수행할 수 있습니다.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [rxDataStep을 사용하여 새 SQL Server 테이블 만들기](../../machine-learning/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)