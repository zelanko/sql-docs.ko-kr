---
title: "R (SQL과 R 심층 분석)를 사용 하 여 데이터를 변환 | Microsoft Docs"
ms.date: 12/24/2017
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
ms.assetid: 0327e788-94cc-4a47-933b-7c5c027b9208
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: d3dbda505155cb8da1f192b2dc36a6889938ccde
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2018
---
# <a name="transform-data-using-r-sql-and-r-deep-dive"></a>R (SQL과 R 심층 분석)를 사용 하 여 데이터를 변환 합니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 데이터 과학 심층 분석 자습서를 사용 하는 방법에 대 한 일부 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) SQL Server와 함께 합니다.

**RevoScaleR** 패키지는 다양한 분석 단계에서 데이터를 변환하기 위한 여러 함수를 제공합니다.

- **rxDataStep** 은 데이터 하위 집합을 만들고 변환하는 데 사용할 수 있습니다.

- **rxImport** 는 XDF 파일 또는 메모리 내 데이터 프레임으로 또는 그 반대로 데이터를 가져올 때 데이터 변환을 지원합니다.

- 특별히 데이터 이동에 사용되지는 않지만 **rxSummary**, **rxCube**, **rxLinMod**및 **rxLogit** 함수도 모두 데이터 변환을 지원합니다.

이 섹션에서는 이러한 함수를 사용 하는 방법을 설명 합니다. 부터 시작 하겠습니다 [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep)합니다.

## <a name="use-rxdatastep-to-transform-variables"></a>RxDataStep를 사용 하 여 변수를 변환

**rxDataStep** 함수는 하나의 데이터 원본에서 읽어 다른 데이터 원본에 쓰면서 한 번에 하나씩 데이터 청크를 처리합니다. 변환할 열, 로드할 변환 등을 지정할 수 있습니다.

효과적으로 만들기 위해이 예에서는, 데이터를 변형 다른 R 패키지의 함수를 사용 하겠습니다.  **boot** 패키지는 "권장" 패키지 중 하나이므로, **boot** 는 R의 모든 배포에 포함되지만 시작할 때 자동으로 로드되지 않습니다. 따라서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 함께 사용 중인 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]인스턴스에서 패키지를 이미 사용할 수 있어야 합니다.

**부팅** 함수를 사용 하 여, 패키지 `inv.logit`는 logit의 역 수를 계산 합니다. 즉, `inv.logit` 함수는 로짓을 다시 [0,1] 눈금의 확률로 변환합니다.

> [!TIP] 
> 이 규모에 맞게 예측을 가져오는 다른 방법을 설정 하는 것은 *형식* 매개 변수를 **응답** rxPredict 원래 호출에 합니다.

1. 테이블에 데이터를 저장할 데이터 소스를 만들어 시작 `ccScoreOutput`합니다.
  
    ```R
    sqlOutScoreDS <- RxSqlServerData( table =  "ccScoreOutput",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
2. 다른 데이터 소스 테이블에 대 한 데이터를 저장할 추가 `ccScoreOutput2`합니다.
  
    ```R
    sqlOutScoreDS2 <- RxSqlServerData( table =  "ccScoreOutput2",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
    새 테이블에는 이전 모든 변수를 저장 `ccScoreOutput` 테이블 및 새로 만든된 변수에 합니다.
  
3. 계산 컨텍스트를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스로 설정합니다.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. 함수를 사용 하 여 **rxSqlServerTableExists** 확인 하려면 있는지 여부를 출력 테이블 `ccScoreOutput2` 이미; 있으며이 경우 함수를 사용 **rxSqlServerDropTable** 는 테이블을 삭제 합니다.
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput2"))     rxSqlServerDropTable("ccScoreOutput2")
    ```
  
5. **rxDataStep** 함수를 호출하고 목록에서 원하는 변환을 지정합니다.
  
    ```R
    rxDataStep(inData = sqlOutScoreDS,
        outFile = sqlOutScoreDS2,
        transforms = list(ccFraudProb = inv.logit(ccFraudLogitScore)),
        transformPackages = "boot",
        overwrite = TRUE)
    ```

    각 열에 적용되는 변환을 정의할 때 변환에 필요한 추가 R 패키지를 지정할 수도 있습니다.  변환 수행할 수 있는 형식에 대 한 자세한 내용은 참조 [RevoScaleR을 사용 하 여 데이터를 변환 및 부분 집합 방법](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-transform)합니다.
  
6. **rxGetVarInfo** 를 호출하여 새 데이터 집합의 변수 요약을 확인합니다.
  
    ```R
    rxGetVarInfo(sqlOutScoreDS2)
    ```

    **결과**
    
    *Var 1: ccFraudLogitScore, Type: numeric*
    
    *Var 2: state, Type: character*
    
    *Var 3: gender, Type: character*
    
    *Var 4: cardholder, Type: character*
    
    *Var 5: balance, Type: integer*
    
    *Var 6: numTrans, Type: integer*
    
    *Var 7: numIntlTrans, Type: integer*
    
    *Var 8: creditLine, Type: integer*
    
    *Var 9: ccFraudProb, Type: numeric*

원래 로짓 점수는 유지되지만 새 열 *ccFraudProb*가 추가되어 로짓 점수가 0과 1 사이의 값으로 표시됩니다.

테이블에 기록 된 비율 변수는 `ccScoreOutput2` 문자 데이터로 합니다. 이후 분석에서 요소로 사용하려면 *colInfo* 매개 변수를 사용하여 수준을 지정합니다.

## <a name="next-step"></a>다음 단계

[rxImport를 사용하여 메모리에 데이터 로드](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)

## <a name="previous-step"></a>이전 단계

[R 스크립트 만들기 및 실행](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)
