---
title: RevoScaleR rxImport를 사용 하 여 메모리에 데이터 로드
description: SQL Server에서 R 언어를 사용 하 여 데이터를 로드 하는 방법에 대 한 자습서 연습입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 6e7e986b3d0ebd21527d730cb5b4bd5fa60d1c4f
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469740"
---
# <a name="load-data-into-memory-using-rximport-sql-server-and-revoscaler-tutorial"></a>RxImport를 사용 하 여 메모리에 데이터 로드 (SQL Server 및 RevoScaleR 자습서)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 단원에서는 SQL Server [RevoScaleR 함수](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) 를 사용 하는 방법에 대 한 [RevoScaleR 자습서](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 의 일부입니다.

[Rximport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) 함수를 사용 하 여 데이터 원본에서 세션 메모리의 데이터 프레임으로 데이터를 이동 하거나 디스크의 xdf 파일로 데이터를 이동할 수 있습니다. 파일을 대상으로 지정하지 않으면 데이터는 메모리에 데이터 프레임으로 저장됩니다.

이 단계에서는에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]데이터를 가져온 다음 **rximport** 함수를 사용 하 여 대상 데이터를 로컬 파일에 저장 하는 방법에 대해 알아봅니다. 이렇게 하면 데이터베이스를 다시 쿼리하지 않고도 로컬 컴퓨팅 컨텍스트에서 반복하여 데이터를 분석할 수 있습니다.

## <a name="extract-a-subset-of-data-from-sql-server-to-local-memory"></a>SQL Server에서 로컬 메모리로 데이터의 하위 집합 추출

위험도가 높은 개인만 자세히 검토 하기로 결정 했습니다. 의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 원본 테이블은 크므로 높은 위험 수준 고객에 대 한 정보를 가져올 수 있습니다. 그런 다음 해당 데이터를 로컬 워크스테이션의 메모리에 있는 데이터 프레임에 로드 합니다.

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

3. [Rximport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) 함수를 호출 하 여 로컬 R 세션의 데이터 프레임으로 데이터를 읽습니다.

    ```R
    highRisk <- rxImport(sqlServerProbDS)
    ```

    작업에 성공 하면 다음과 같은 상태 메시지가 표시 됩니다. "읽은 행: 35, 총 처리 된 행: 35, 총 청크 시간: 0.036 초 "

4. 이제 높은 위험 수준의 관찰이 메모리 내 데이터 프레임에 있으므로 다양 한 R 함수를 사용 하 여 데이터 프레임을 조작할 수 있습니다. 예를 들어 고객의 위험 점수를 기준으로 고객의 순서를 지정할 수 있으며 가장 높은 위험을 야기 하는 고객의 목록을 인쇄할 수 있습니다.

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

**Rximport** 함수는 가져오기 프로세스 동안 열에 변수 이름을 할당 하지만, *colInfo* 매개 변수를 사용 하 여 새 변수 이름을 지정 하거나 colclasses 매개 변수를 사용 하 여  데이터 형식을 변경할 수 있습니다.

*transforms* 매개 변수에서 추가 작업을 지정하여 읽은 각 데이터 청크에 대한 기본 처리를 수행할 수 있습니다.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [rxDataStep을 사용하여 새 SQL Server 테이블 만들기](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)