---
title: RevoScaleR을 사용하여 데이터 변환
description: 'RevoScaleR 자습서 9: SQL Server에서 R 언어를 사용하여 데이터를 변환하는 방법입니다.'
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7ed1884b1d4dc6f2b1b32a06d348307171edd592
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85757114"
---
# <a name="transform-data-using-r-sql-server-and-revoscaler-tutorial"></a>R을 사용하여 데이터 변환(SQL Server 및 RevoScaleR 자습서)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

이것은 SQL Server에서 [RevoScaleR 함수](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)를 사용하는 방법에 대한 [RevoScaleR 자습서 시리즈](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 중 자습서 9에 해당됩니다.

이 자습서에서는 다양한 분석 단계에서 데이터를 변환하기 위한 **RevoScaleR** 함수에 대해 알아봅니다.

> [!div class="checklist"]
> * **rxDataStep**을 사용하여 데이터 하위 세트를 만들고 변환합니다.
> * 가져오는 동안 **rxImport**를 사용하여 전송 중인 데이터를 XDF 파일 또는 메모리 내 데이터 프레임으로 변환합니다.

특별히 데이터 이동에 사용되지는 않지만 **rxSummary**, **rxCube**, **rxLinMod**및 **rxLogit** 함수도 모두 데이터 변환을 지원합니다.

## <a name="use-rxdatastep-to-transform-variables"></a>rxDataStep을 사용하여 변수 변환

[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) 함수는 하나의 데이터 원본에서 읽어 다른 데이터 원본에 쓰면서 한 번에 하나씩 데이터 청크를 처리합니다. 변환할 열, 로드할 변환 등을 지정할 수 있습니다.

이 예제를 흥미롭게 만들기 위해 다른 R 패키지의 함수를 사용하여 데이터를 변환해 보겠습니다. **boot** 패키지는 "권장" 패키지 중 하나이므로, **boot** 는 R의 모든 배포에 포함되지만 시작할 때 자동으로 로드되지 않습니다. 따라서 패키지는 R 통합을 위해 구성된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 이미 사용할 수 있어야 합니다.

**boot** 패키지에서 로짓의 역수를 계산하는 **inv.logit** 함수를 사용합니다. 즉, **inv.logit** 함수는 로짓을 다시 [0,1] 눈금의 확률로 변환합니다.

> [!TIP] 
> 이 눈금의 예측을 구하는 또 다른 방법은 원래의 *rxPredict* 호출에서 **type** 매개 변수를 **response**로 설정하는 것입니다.

1. 먼저 `ccScoreOutput` 테이블에 사용되는 데이터를 저장할 데이터 원본을 만듭니다.
  
    ```R
    sqlOutScoreDS <- RxSqlServerData( table =  "ccScoreOutput",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
2. `ccScoreOutput2` 테이블에 사용되는 데이터를 저장할 다른 데이터 원본을 추가합니다.
  
    ```R
    sqlOutScoreDS2 <- RxSqlServerData( table =  "ccScoreOutput2",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
    새 테이블에서 이전 `ccScoreOutput` 테이블의 모든 변수와 새로 만든 변수를 저장합니다.
  
3. 컴퓨팅 컨텍스트를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스로 설정합니다.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. **rxSqlServerTableExists** 함수를 사용하여 출력 테이블 `ccScoreOutput2`가 이미 있는지 확인하고, 이미 있는 경우 **rxSqlServerDropTable** 함수를 사용하여 테이블을 삭제합니다.
  
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

    각 열에 적용되는 변환을 정의할 때 변환에 필요한 추가 R 패키지를 지정할 수도 있습니다.  수행할 수 있는 변환 유형에 대한 자세한 내용은 [RevoScaleR을 사용하여 데이터를 변환하고 하위 집합하는 방법](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-transform)을 참조하세요.
  
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

요소 변수가 테이블 `ccScoreOutput2`에 문자 데이터로 기록되었습니다. 이후 분석에서 요소로 사용하려면 *colInfo* 매개 변수를 사용하여 수준을 지정합니다.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [rxImport를 사용하여 메모리에 데이터 로드](../../machine-learning/tutorials/deepdive-load-data-into-memory-using-rximport.md)