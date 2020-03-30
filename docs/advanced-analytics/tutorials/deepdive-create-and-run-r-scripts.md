---
title: RevoScaleR의 요약 통계
description: 'RevoScaleR 자습서 5: SQL Server에서 R 언어를 사용하여 통계적 요약 통계를 계산하는 방법을 안내합니다.'
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 43745602fc099f1b992eb1d76622ff3d7e6d0916
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "74947283"
---
# <a name="compute-summary-statistics-in-r-sql-server-and-revoscaler-tutorial"></a>R의 컴퓨팅 요약 통계(SQL Server 및 RevoScaleR 자습서)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이것은 SQL Server에서 [RevoScaleR 함수](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)를 사용하는 방법에 대한 [RevoScaleR 자습서 시리즈](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 중 자습서 5에 해당됩니다.

이 자습서는 이전 자습서에서 만든 기존 데이터 원본 및 컴퓨팅 컨텍스트를 사용하여 고성능 R 스크립트를 실행합니다. 이 자습서에서는 다음 작업에 로컬 및 원격 서버 컴퓨팅 컨텍스트를 사용합니다.

> [!div class="checklist"]
> * 컴퓨팅 컨텍스트를 SQL Server로 전환
> * 원격 데이터 개체에 대한 요약 통계 가져오기
> * 로컬 요약 컴퓨팅

이전 자습서를 완료한 경우, sqlCompute 및 sqlComputeTrace라는 원격 컴퓨팅 컨텍스트가 있어야 합니다. 이후 자습서에서는 sqlCompute 및 로컬 컴퓨팅 컨텍스트를 사용합니다.

이 자습서에서는 R IDE 또는 **Rgui**를 사용하여 R 스크립트를 실행합니다.

## <a name="compute-summary-statistics-on-remote-data"></a>원격 데이터에 대한 요약 통계 컴퓨팅

R 코드를 원격으로 실행하기 전에 원격 컴퓨팅 컨텍스트를 지정해야 합니다. 이후의 모든 계산은 *sqlCompute* 매개 변수에 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에서 수행됩니다.

컴퓨팅 컨텍스트를 변경할 때까지 활성 상태로 유지됩니다. 그러나 원격 서버 컨텍스트에서 실행할 수 *없는* 모든 R 스크립트는 자동으로 로컬로 실행됩니다.

컴퓨팅 컨텍스트의 작동 방식을 확인하려면 원격 SQL Server의 sqlFraudDS 데이터 원본에 대한 요약 통계를 생성합니다. 이 데이터 원본 개체는 [자습서 2](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)에서 만들어졌으며 RevoDeepDive 데이터베이스의 ccFraudSmall 테이블을 나타냅니다. 

1. 컴퓨팅 컨텍스트를 이전 자습서에서 만든 sqlCompute로 전환합니다.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```

2. [rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary) 함수를 호출하고 수식 및 데이터 원본과 같은 필수 인수를 전달하고 결과를 변수 `sumOut`에 할당합니다.
  
    ```R
    sumOut <- rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS)
    ```
  
    R 언어는 많은 요약 함수를 제공하지만 **RevoScaleR**의 **rxSummary**는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 비롯한 다양한 원격 컴퓨팅 컨텍스트에서의 실행을 지원합니다. 유사한 함수에 대한 자세한 내용은 [RevoScaleR을 사용한 데이터 요약](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries)을 참조하세요.
  
3. sumOut의 내용을 콘솔에 인쇄합니다.
  
    ```R
    sumOut
    ```
    > [!NOTE]
    > 오류가 발생하면 명령을 다시 시도하기 전에 실행이 완료될 때까지 몇 분 정도 기다립니다.

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
  
2. SQL Server에서 데이터를 추출할 때 증가된 블록 크기를 메모리에 수용할 수 있다고 가정하여 각 읽기에 대해 추출되는 행 수를 늘려 성능을 향상시킬 수 있습니다. 다음 명령을 실행하여 데이터 원본에 대한 *rowsPerRead* 매개 변수의 값을 늘립니다. 이전에는 *rowsPerRead* 값이 5000으로 설정되었습니다.
  
    ```R
    sqlServerDS1 <- RxSqlServerData(
       connectionString = sqlConnString,
       table = sqlFraudTable,
       colInfo = ccColInfo,
       rowsPerRead = 10000)
    ```

3. 새 데이터 원본에 대해 **rxSummary**를 호출합니다.
  
    ```R
    rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlServerDS1)
    ```
  
   실제 결과는 **컴퓨터의 컨텍스트에서** rxSummary [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 실행할 때와 같아야 합니다. 그러나 작업은 더 빠르거나 느릴 수 있습니다. 데이터가 분석을 위해 로컬 컴퓨터로 전송되므로 이러한 작업 속도는 데이터베이스에 대한 연결에 크게 좌우됩니다.

4. 다음 몇 가지 자습서를 위한 원격 컴퓨팅 컨텍스트로 다시 전환합니다.

    ```R
    rxSetComputeContext(sqlCompute)
    ```

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [R을 사용하여 SQL Server 데이터 시각화](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)