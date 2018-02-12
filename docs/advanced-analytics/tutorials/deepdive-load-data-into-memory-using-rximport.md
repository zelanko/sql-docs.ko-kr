---
title: "데이터 rxImport (SQL과 R 심층 분석)를 사용 하 여 메모리에 로드 | Microsoft Docs"
ms.custom: 
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs:
- R
ms.assetid: 47a42e9a-05a0-4a50-871d-de73253cf070
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 68e9533509c731b9cddff737a4db120be0dc86b8
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2018
---
# <a name="load-data-into-memory-using-rximport-sql-and-r-deep-dive"></a>RxImport (SQL과 R 심층 분석)를 사용 하 여 메모리에 데이터 로드
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 데이터 과학 심층 분석 자습서를 사용 하는 방법에 대 한 일부 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) SQL Server와 함께 합니다.

[rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) 데이터 프레임에서 세션 메모리 나 디스크에 있는 XDF 파일에 데이터 원본에서 데이터를 이동 하는 함수를 사용할 수 있습니다. 파일을 대상으로 지정하지 않으면 데이터는 메모리에 데이터 프레임으로 저장됩니다.

이 단계에서 데이터를 가져오는 방법을 배웁니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 사용 하 여는 **rxImport** 관심 있는 데이터는 로컬 파일에 추가 하는 함수입니다. 이렇게 하면 데이터베이스를 다시 쿼리하지 않고도 로컬 계산 컨텍스트에서 반복하여 데이터를 분석할 수 있습니다.

## <a name="extract-a-subset-of-data-from-sql-server-to-local-memory"></a>SQL Server에서 로컬 메모리에 데이터의 하위 집합을 추출

자세히 위험 수준이 높은 개인만 검사할 것인지 결정 합니다. 원본 테이블에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 크므로 방금 위험 수준이 높은 고객에 대 한 정보를 가져오려는 합니다. 그런 다음 로컬 워크스테이션의 메모리에 데이터 프레임으로 해당 데이터를 로드 합니다.

1. 계산 컨텍스트를 로컬 워크스테이션으로 다시 설정합니다.

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

3. 함수 호출 [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) 로컬 R 세션에서 데이터 프레임으로 데이터를 읽을 수 있습니다.

    ```R
    highRisk <- rxImport(sqlServerProbDS)
    ```

    작업에 성공 하면 다음과 같은 상태 메시지가 나타납니다: "Rows Read: 35, 총 행 처리 됨: 35, 총 청크 시간: 0.036 시간 (초)"

4. 메모리 내 데이터 프레임에서 위험 수준이 높은 관찰 인 했으므로 데이터 프레임을 조작 하기 위한 다양 한 R 함수를 사용할 수 있습니다. 예를 들어 해당 위험 점수 고객 주문 수 있으며 가장 높은 위험 노출 하는 고객의 목록을 인쇄.

    ```R
    orderedHighRisk <- highRisk[order(-highRisk$ccFraudProb),]
    row.names(orderedHighRisk) <- NULL
    head(orderedHighRisk)
    ```

**결과**

*ccFraudLogitScore   state gender cardholder balance numTrans numIntlTrans creditLine ccFraudProb1*

*9.786345    SD   Male  Principal   23456       25            5 75   0.99994382*

*9.433040    FL Female  Principal   20629       24           28 75   0.99992003*

*8.556785    NY Female  Principal   19064       82           53 43   0.99980784*

*8.188668    AZ Female  Principal   19948       29            0 75   0.99972235*

*7.551699    NY Female  Principal   11051       95            0 75   0.99947516*

*7.335080    NV   Male  Principal   21566        4            6  75   0.9993482*

## <a name="more-about-rximport"></a>rxImport 대한 자세한 정보

**rxImport** 를 사용하여 데이터 이동은 물론 데이터를 읽는 동안 데이터를 변환할 수도 있습니다. 예를 들어 고정 너비 열에 대해 문자 수를 지정하고, 변수에 대한 설명을 제공하고, 요소 열에 대한 수준을 설정하고, 가져온 후 사용할 새로운 수준을 만들 수 있습니다.

**rxImport** 함수 가져오기 프로세스 동안 열에 변수 이름을 할당 하지만 사용 하 여 새 변수 이름을 지정할 수 있습니다는 *colInfo* 매개 변수 또는 를사용하여변경데이터형식*colClasses* 매개 변수입니다.

*transforms* 매개 변수에서 추가 작업을 지정하여 읽은 각 데이터 청크에 대한 기본 처리를 수행할 수 있습니다.

## <a name="next-step"></a>다음 단계

[rxDataStep을 사용하여 새 SQL Server 테이블 만들기](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)

## <a name="previous-step"></a>이전 단계

[R을 사용하여 데이터 변환](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)

