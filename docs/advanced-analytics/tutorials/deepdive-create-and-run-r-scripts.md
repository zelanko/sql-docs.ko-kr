---
title: Compute summary statistics RevoScaleR 자습서
description: SQL Server에서 R 언어를 사용 하 여 통계 요약 통계를 계산 하는 방법에 대 한 자습서 연습입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 5f90cc0e6101e168e15ed7c1145d286f799375ac
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344712"
---
# <a name="compute-summary-statistics-in-r-sql-server-and-revoscaler-tutorial"></a>R의 계산 요약 통계 (SQL Server 및 RevoScaleR 자습서)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 단원에서는 SQL Server [RevoScaleR 함수](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) 를 사용 하는 방법에 대 한 [RevoScaleR 자습서](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 의 일부입니다.

이전 단원에서 만든 설정 된 데이터 원본 및 계산 컨텍스트를 사용 하 여이 스크립트에서 고성능 R 스크립트를 실행 합니다. 이 단원에서는 로컬 및 원격 서버 계산 컨텍스트를 사용 하 여 다음 작업을 수행 합니다.

> [!div class="checklist"]
> * 계산 컨텍스트를 SQL Server로 전환
> * 원격 데이터 개체에 대 한 요약 통계 가져오기
> * 로컬 요약 계산

이전 단원을 완료 한 경우 다음과 같은 원격 계산 컨텍스트가 필요 합니다. sqlCompute 및 Sqlcompute Et레이스. 이후 단원에서 sqlCompute 및 로컬 계산 컨텍스트를 사용 합니다.

R IDE 또는 **Rgui** 를 사용 하 여이 단원에서 r 스크립트를 실행 합니다.

## <a name="compute-summary-statistics-on-remote-data"></a>원격 데이터에 대 한 계산 요약 통계

R 코드를 원격으로 실행 하려면 원격 계산 컨텍스트를 지정 해야 합니다. 모든 후속 계산은 *sqlcompute* 매개 변수에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지정 된 컴퓨터에서 수행 됩니다.

계산 컨텍스트는 변경 될 때까지 활성 상태로 유지 됩니다. 그러나 원격 서버 컨텍스트에서 실행할 *수 없는* R 스크립트는 로컬로 자동으로 실행 됩니다.

계산 컨텍스트가 어떻게 작동 하는지 확인 하려면 원격 SQL Server에서 sqlFraudDS 데이터 원본에 대 한 요약 통계를 생성 합니다. 이 데이터 원본 개체는 [2 단원](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md) 에서 생성 되었으며 RevoDeepDive 데이터베이스의 ccFraudSmall 테이블을 나타냅니다. 

1. 계산 컨텍스트를 이전 단원에서 만든 sqlCompute로 전환 합니다.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```

2. [rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary)를 수식이나 데이터 원본 등의 필수 인수와 함께 호출하고 그 결과를 `sumOut` 변수에 할당합니다.
  
    ```R
    sumOut <- rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS)
    ```
  
    R 언어는 많은 요약 함수를 제공 하지만 **RevoScaleR** 의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **rxsummary** 는를 비롯 한 다양 한 원격 계산 컨텍스트에서 실행을 지원 합니다. 이와 유사한 함수에 대한 정보는 [RevoScaleR을 사용하여 데이터 요약하기](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries)를 참고하십시오.
  
3. SumOut의 내용을 콘솔에 인쇄 합니다.
  
    ```R
    sumOut
    ```
    > [!NOTE]
    > 오류가 발생 하는 경우 명령을 다시 시도 하기 전에 실행이 완료 될 때까지 몇 분 정도 기다립니다.

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

1. 모든 작업을 로컬에서 수행하도록 컴퓨팅 컨텍스트를 변경합니다.
  
    ```R
    rxSetComputeContext ("local")
    ```
  
2. SQL Server에서 데이터를 추출할 때 증가 하는 블록 크기를 메모리에 수용할 수 있다고 가정 하 여 각 읽기에 대해 추출 되는 행 수를 늘려 성능을 향상 시킬 수 있습니다. 다음 명령을 실행 하 여 데이터 원본에 대 한 *Rowsperread* 매개 변수의 값을 늘립니다. 이전에는 *rowsPerRead* 값이 5000으로 설정되었습니다.
  
    ```R
    sqlServerDS1 <- RxSqlServerData(
       connectionString = sqlConnString,
       table = sqlFraudTable,
       colInfo = ccColInfo,
       rowsPerRead = 10000)
    ```

3. 새 데이터 원본에 대 한 **Rxsummary** 를 호출 합니다.
  
    ```R
    rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlServerDS1)
    ```
  
   실제 결과는 **컴퓨터의 컨텍스트에서** rxSummary [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 실행할 때와 같아야 합니다. 그러나 작업은 더 빠르거나 느릴 수 있습니다. 데이터가 분석을 위해 로컬 컴퓨터로 전송되므로 이러한 작업 속도는 데이터베이스에 대한 연결에 크게 좌우됩니다.

4. 다음 몇 개의 단원을 위한 원격 계산 컨텍스트로 다시 전환 합니다.

    ```R
    rxSetComputeContext(sqlCompute)
    ```

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [R을 사용하여 SQL Server 데이터 시각화](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)