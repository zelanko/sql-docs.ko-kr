---
title: "R을 사용 하 여 데이터를 변환 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 0327e788-94cc-4a47-933b-7c5c027b9208
caps.latest.revision: 19
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 10670f1a5ac3e002d67eab076c41b822b2e757fd
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="transform-data-using-r"></a>R을 사용 하 여 데이터를 변환 합니다.

**RevoScaleR** 패키지는 다양한 분석 단계에서 데이터를 변환하기 위한 여러 함수를 제공합니다.

- **rxDataStep** 은 데이터 하위 집합을 만들고 변환하는 데 사용할 수 있습니다.

- **rxImport** 는 XDF 파일 또는 메모리 내 데이터 프레임으로 또는 그 반대로 데이터를 가져올 때 데이터 변환을 지원합니다.

- 특별히 데이터 이동에 사용되지는 않지만 **rxSummary**, **rxCube**, **rxLinMod**및 **rxLogit** 함수도 모두 데이터 변환을 지원합니다.

이 섹션에서는 이러한 함수를 사용하는 방법을 알아봅니다. RxDataStep부터 살펴보겠습니다.

## <a name="use-rxdatastep-to-transform-variables"></a>RxDataStep을 사용하여 변수 변환

RxDataStep 함수는 하나의 데이터 원본에서 읽고 쓰는 다른 한 번에 하나의 데이터 청크를 처리 합니다. 변환할 열, 로드할 변환 등을 지정할 수 있습니다.

이 예제를 흥미롭게 만들기 위해 다른 R 패키지의 함수를 사용하여 데이터를 변환하겠습니다.  **boot** 패키지는 "권장" 패키지 중 하나이므로, **boot** 는 R의 모든 배포에 포함되지만 시작할 때 자동으로 로드되지 않습니다. 따라서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 함께 사용 중인 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]인스턴스에서 패키지를 이미 사용할 수 있어야 합니다.

**부팅** 패키지 함수를 사용 합니다 `inv.logit`는 logit의 역 수를 계산 합니다. 즉, `inv.logit` 함수는 로짓을 다시 [0,1] 눈금의 확률로 변환합니다.

> [!TIP] 
> 이 규모에 맞게 예측을 가져오는 다른 방법을 설정 하는 것은 *형식* 매개 변수를 **응답** rxPredict 원래 호출에 합니다.

1. 먼저 *ccScoreOutput*테이블에 사용되는 데이터를 저장할 데이터 원본을 만듭니다.
  
    ```R
    sqlOutScoreDS <- RxSqlServerData( table =  "ccScoreOutput",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
2. ccScoreOutput2 테이블에 사용되는 데이터를 저장할 다른 데이터 원본을 추가합니다.
  
    ```R
    sqlOutScoreDS2 <- RxSqlServerData( table =  "ccScoreOutput2",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
    새 테이블에서 이전 *ccScoreOutput* 테이블의 모든 변수와 새로 만든 변수를 가져옵니다.
  
3. 계산 컨텍스트를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스로 설정합니다.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. 함수 rxSqlServerTableExists를 사용 하 여 확인 여부 출력 테이블 *ccScoreOutput2* 이미; 있으며이 경우 함수 rxSqlServerDropTable을 사용 하 여 테이블을 삭제 하 합니다.
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput2"))     rxSqlServerDropTable("ccScoreOutput2")
    ```
  
5. RxDataStep 함수를 호출 하 고 목록에서 원하는 변환을 지정 합니다.
  
    ```R
    rxDataStep(inData = sqlOutScoreDS,
        outFile = sqlOutScoreDS2,
        transforms = list(ccFraudProb = inv.logit(ccFraudLogitScore)),
        transformPackages = "boot",
        overwrite = TRUE)
    ```

    각 열에 적용되는 변환을 정의할 때 변환에 필요한 추가 R 패키지를 지정할 수도 있습니다.  수행할 수 있는 변환 유형에 대한 자세한 내용은  [Transforming and Subsetting Data](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-data-transform)(데이터 변환 및 하위 집합 사용)를 참조하세요.
  
6. 새 데이터 집합의 변수 중 한 요약을 볼 수는 rxGetVarInfo를 호출 합니다.
  
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

요소 변수는 *ccScoreOutput2* 테이블에 문자 데이터로 기록되었습니다.  이후 분석에서 요소로 사용하려면 *colInfo* 매개 변수를 사용하여 수준을 지정합니다.

## <a name="next-step"></a>다음 단계

[데이터 rxImport를 사용 하 여 메모리에 로드](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)

## <a name="previous-step"></a>이전 단계

[만들기 및 R 스크립트 실행](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)

