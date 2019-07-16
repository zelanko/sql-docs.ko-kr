---
title: RevoScaleR rxDataStep-SQL Server Machine Learning을 사용 하 여 데이터 변환
description: SQL Server에서 R 언어를 사용 하 여 데이터를 변환 하는 방법에 대 한 연습 자습서입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 0da478798e87497da7828126b2168bbae5d980f7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962173"
---
# <a name="transform-data-using-r-sql-server-and-revoscaler-tutorial"></a>R (RevoScaleR 및 SQL Server 자습서)를 사용 하 여 데이터 변환
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 단원에서는의 일부인를 [RevoScaleR 자습서](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 사용 하는 방법에 [RevoScaleR 함수](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) SQL Server를 사용 하 여 합니다.

이 단원에 대해 알아봅니다 합니다 **RevoScaleR** 분석의 여러 단계에서 데이터를 변환 하기 위한 함수입니다.

> [!div class="checklist"]
> * 사용 하 여 **rxDataStep** 을 만들고 데이터 하위 집합을 변환 하려면
> * 사용 하 여 **rxImport** XDF 파일 또는 메모리 내 데이터 프레임 간에 전송 중인 데이터를 가져오는 동안 변환할

특별히 데이터 이동에 사용되지는 않지만 **rxSummary**, **rxCube**, **rxLinMod**및 **rxLogit** 함수도 모두 데이터 변환을 지원합니다.

## <a name="use-rxdatastep-to-transform-variables"></a>RxDataStep을 사용 하 여 변수 변환

[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) 함수는 하나의 데이터 원본에서 읽어 다른 데이터 원본에 쓰면서 한 번에 하나씩 데이터 청크를 처리합니다. 변환할 열, 로드할 변환 등을 지정할 수 있습니다.

이 예제에서는 유용 하도록 데이터를 변환할 다른 R 패키지의 함수를 사용해 보겠습니다. **boot** 패키지는 "권장" 패키지 중 하나이므로, **boot** 는 R의 모든 배포에 포함되지만 시작할 때 자동으로 로드되지 않습니다. 따라서 패키지는 이미 사용할 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 R 통합용으로 구성 합니다.

**부팅** 함수를 사용, 패키지 **inv.logit**는 logit의 역을 계산 하는 합니다. 즉, **inv.logit** 함수는 로짓을 다시 [0,1] 눈금의 확률로 변환합니다.

> [!TIP] 
> 이 눈금의 예측을 구하는 또 다른 방법은 원래의 *rxPredict* 호출에서 **type** 매개 변수를 **response**로 설정하는 것입니다.

1. 테이블에 대해 사용 되는 데이터를 저장 하는 데이터 소스를 만들어 시작 `ccScoreOutput`합니다.
  
    ```R
    sqlOutScoreDS <- RxSqlServerData( table =  "ccScoreOutput",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
2. 테이블에 대 한 데이터를 저장할 다른 데이터 원본 추가 `ccScoreOutput2`합니다.
  
    ```R
    sqlOutScoreDS2 <- RxSqlServerData( table =  "ccScoreOutput2",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
    새 테이블을 이전 모든 변수를 저장할 `ccScoreOutput` 테이블과 새로 생성된 된 변수입니다.
  
3. 컴퓨팅 컨텍스트를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스로 설정합니다.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. 함수를 사용 **rxSqlServerTableExists** 검사할 여부를 출력 테이블 `ccScoreOutput2` 이미 있으면 하 고 그렇다면 함수를 사용 **rxSqlServerDropTable** 테이블을 삭제 합니다.
  
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

    각 열에 적용되는 변환을 정의할 때 변환에 필요한 추가 R 패키지를 지정할 수도 있습니다.  수행할 수 있는 변환 유형에 대 한 자세한 내용은 참조 하세요. [RevoScaleR을 사용 하 여 데이터를 변환 및 일부 방법](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-transform)합니다.
  
6. **rxGetVarInfo** 를 호출하여 새 데이터 집합의 변수 요약을 확인합니다.
  
```R
rxGetVarInfo(sqlOutScoreDS2)
```

**결과**

```R
Var 1: ccFraudLogitScore, Type: numeric
Var 2: state, Type: character
Var 3: gender, Type: character
Var 4: cardholder, Type: character
Var 5: balance, Type: integer
Var 6: numTrans, Type: integer
Var 7: numIntlTrans, Type: integer
Var 8: creditLine, Type: integer
Var 9: ccFraudProb, Type: numeric
```

원래 로짓 점수는 유지되지만 새 열 *ccFraudProb*가 추가되어 로짓 점수가 0과 1 사이의 값으로 표시됩니다.

요소 변수 테이블에 기록 된 알림 `ccScoreOutput2` 문자 데이터입니다. 이후 분석에서 요소로 사용하려면 *colInfo* 매개 변수를 사용하여 수준을 지정합니다.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [rxImport를 사용하여 메모리에 데이터 로드](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)