---
title: RevoScaleR 자습서-SQL Server Machine Learning 요약 통계를 계산 합니다.
description: SQL Server에서 R 언어를 사용 하 여 통계 요약 통계를 계산 하는 방법에 대 한 연습 자습서입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: dea877323911b3965f7fef5d52ffc121b3990f7d
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645252"
---
# <a name="compute-summary-statistics-in-r-sql-server-and-revoscaler-tutorial"></a>R (RevoScaleR 및 SQL Server 자습서)에 대 한 요약 통계를 계산 합니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 단원에서는의 일부인를 [RevoScaleR 자습서](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 사용 하는 방법에 [RevoScaleR 함수](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) SQL Server를 사용 하 여 합니다.

이 구성 파일에서 고성능 R 스크립트를 실행 하려면 설정 된 데이터 원본과 이전 단원에서 만든 계산 컨텍스트를 사용 합니다. 이 단원에서는 다음 작업에 대 한 로컬 및 원격 서버 계산 컨텍스트를 사용 합니다.

> [!div class="checklist"]
> * SQL server 계산 컨텍스트를 전환 합니다.
> * 원격 데이터 개체에 대 한 요약 통계 가져오기
> * 로컬 요약 계산

이전 단원을 완료 하는 경우 이러한 원격 계산 컨텍스트 있어야: sqlCompute 및 sqlComputeTrace 합니다. 사용할 앞으로 이동 됩니다 sqlCompute 및 로컬 계산 컨텍스트에서 이후 단원에서.

R IDE를 사용 하 여 또는 **Rgui** 이 단원에서는 R 스크립트를 실행 합니다.

## <a name="compute-summary-statistics-on-remote-data"></a>원격 데이터에 대 한 요약 통계를 계산 합니다.

R 코드를 원격으로 실행 하기 전에 원격 계산 컨텍스트를 지정 해야 합니다. 모든 후속 계산 수행 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 지정 된 컴퓨터를 *sqlCompute* 매개 변수입니다.

계산 컨텍스트를 변경할 때까지 활성 상태로 유지 됩니다. 그러나 모든 R 스크립트는 *없습니다* 원격 서버 컨텍스트에서 실행은 자동으로 로컬로 실행 합니다.

계산 컨텍스트에서 작동 원리를 확인 하려면 원격 SQL Server에서 sqlFraudDS 데이터 원본에 대 한 요약 통계를 생성 합니다. 이 데이터 원본 개체에서 만든 [두 단원](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md) ccFraudSmall 표의 RevoDeepDive 데이터베이스를 나타냅니다. 

1. 이전 단원에서 만든 sqlCompute 계산 컨텍스트를 전환 합니다.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```

2. [rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary)를 수식이나 데이터 원본 등의 필수 인수와 함께 호출하고 그 결과를 `sumOut` 변수에 할당합니다.
  
    ```R
    sumOut <- rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS)
    ```
  
    R 언어는 많은 요약 함수를 제공 하지만 **rxSummary** 에 **RevoScaleR** 다양 한 원격 계산 컨텍스트를 포함 하 여 실행을 지원 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 이와 유사한 함수에 대한 정보는 [RevoScaleR을 사용하여 데이터 요약하기](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries)를 참고하십시오.
  
3. 콘솔로 sumOut의 콘텐츠를 인쇄 합니다.
  
    ```R
    sumOut
    ```
    > [!NOTE]
    > 오류가 발생 하는 경우에 실행을 마칠 명령을 다시 시도 하기 전에 몇 분 동안 기다립니다.

**결과**

```R
Summary Statistics Results for: ~gender + balance + numTrans + numIntlTrans + creditLine
Data: sqlFraudDS (RxSqlServerData Data Source)
Number of valid observations: 10000

 Name  Mean    StdDev  Min Max ValidObs    MissingObs
 balance       4075.0318 3926.558714            0   25626 100000
 numTrans        29.1061   26.619923 0     100 10000    0           100000
 numIntlTrans     4.0868    8.726757 0      60 10000    0           100000
 creditLine       9.1856    9.870364 1      75 10000    0          100000
 
 Category Counts for gender
 Number of categories: 2
 Number of valid observations: 10000
 Number of missing observations: 0

 gender Counts
  Male   6154
  Female 3846
```

## <a name="create-a-local-summary"></a>로컬 요약 만들기

1. 모든 작업을 로컬에서 수행하도록 계산 컨텍스트를 변경합니다.
  
    ```R
    rxSetComputeContext ("local")
    ```
  
2. SQL Server에서 데이터를 추출할 때 얻을 수 있습니다 종종 더 나은 성능을 각 읽기에 대해 추출 된 행의 수를 늘려 가정 하 고 메모리에서 향상 된 블록 크기를 수용할 수 있습니다. 에 대 한 값을 늘리려면 다음 명령을 실행 합니다 *rowsPerRead* 데이터 원본에 대 한 매개 변수입니다. 이전에는 *rowsPerRead* 값이 5000으로 설정되었습니다.
  
    ```R
    sqlServerDS1 <- RxSqlServerData(
       connectionString = sqlConnString,
       table = sqlFraudTable,
       colInfo = ccColInfo,
       rowsPerRead = 10000)
    ```

3. 호출 **rxSummary** 새 데이터 원본에 있습니다.
  
    ```R
    rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlServerDS1)
    ```
  
   실제 결과는 **컴퓨터의 컨텍스트에서** rxSummary [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 실행할 때와 같아야 합니다. 그러나 작업은 더 빠르거나 느릴 수 있습니다. 데이터가 분석을 위해 로컬 컴퓨터로 전송되므로 이러한 작업 속도는 데이터베이스에 대한 연결에 크게 좌우됩니다.

4. 다음 몇 가지 단원에 대 한 계산 컨텍스트를 원격으로 다시 전환 합니다.

    ```R
    rxSetComputeContext(sqlCompute)
    ```

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [R을 사용하여 SQL Server 데이터 시각화](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)