---
title: RevoScaleR rxDataStep을 사용 하 여 데이터 변환
description: SQL Server에서 R 언어를 사용 하 여 데이터를 변환 하는 방법에 대 한 자습서 연습입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c76bdf56febd06ecba6f2d9d11f1710eefdc23e6
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715510"
---
# <a name="transform-data-using-r-sql-server-and-revoscaler-tutorial"></a>R을 사용 하 여 데이터 변환 (SQL Server 및 RevoScaleR 자습서)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 단원에서는 SQL Server [RevoScaleR 함수](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) 를 사용 하는 방법에 대 한 [RevoScaleR 자습서](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 의 일부입니다.

이 단원에서는 다양 한 분석 단계에서 데이터를 변환 하는 **RevoScaleR** 함수에 대해 알아봅니다.

> [!div class="checklist"]
> * **Rxdatastep** 을 사용 하 여 데이터 하위 집합 만들기 및 변환
> * **Rximport** 를 사용 하 여 가져오기 중에 xdf 파일 또는 메모리 내 데이터 프레임 간에 전송 중인 데이터를 변환 합니다.

특별히 데이터 이동에 사용되지는 않지만 **rxSummary**, **rxCube**, **rxLinMod**및 **rxLogit** 함수도 모두 데이터 변환을 지원합니다.

## <a name="use-rxdatastep-to-transform-variables"></a>RxDataStep을 사용 하 여 변수 변환

[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) 함수는 하나의 데이터 원본에서 읽어 다른 데이터 원본에 쓰면서 한 번에 하나씩 데이터 청크를 처리합니다. 변환할 열, 로드할 변환 등을 지정할 수 있습니다.

이 예제를 흥미 있게 하려면 다른 R 패키지의 함수를 사용 하 여 데이터를 변환 해 보겠습니다. **boot** 패키지는 "권장" 패키지 중 하나이므로, **boot** 는 R의 모든 배포에 포함되지만 시작할 때 자동으로 로드되지 않습니다. 따라서 R 통합을 위해 구성 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 패키지를 이미 사용할 수 있어야 합니다.

**부팅** 패키지에서 **inv**함수를 사용 하 여 logit의 역함수를 계산 합니다. 즉, **inv.logit** 함수는 로짓을 다시 [0,1] 눈금의 확률로 변환합니다.

> [!TIP] 
> 이 눈금의 예측을 구하는 또 다른 방법은 원래의 *rxPredict* 호출에서 **type** 매개 변수를 **response**로 설정하는 것입니다.

1. 먼저 테이블 `ccScoreOutput`의 대상 데이터를 보관할 데이터 원본을 만듭니다.
  
    ```R
    sqlOutScoreDS <- RxSqlServerData( table =  "ccScoreOutput",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
2. 테이블 `ccScoreOutput2`의 데이터를 보관할 다른 데이터 원본을 추가 합니다.
  
    ```R
    sqlOutScoreDS2 <- RxSqlServerData( table =  "ccScoreOutput2",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
    새 테이블에서 이전 `ccScoreOutput` 테이블의 모든 변수와 새로 만든 변수를 저장 합니다.
  
3. 컴퓨팅 컨텍스트를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스로 설정합니다.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. **RxSqlServerTableExists** 함수를 사용 하 여 출력 테이블이 `ccScoreOutput2` 이미 있는지 여부를 확인 하 고, 그렇다면 **rxSqlServerDropTable** 함수를 사용 하 여 테이블을 삭제 합니다.
  
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

    각 열에 적용되는 변환을 정의할 때 변환에 필요한 추가 R 패키지를 지정할 수도 있습니다.  수행할 수 있는 변환 유형에 대 한 자세한 내용은 [RevoScaleR를 사용 하 여 데이터를 변환 하 고 하위 집합 하는 방법](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-transform)을 참조 하세요.
  
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

요소 변수는 테이블 `ccScoreOutput2` 에 문자 데이터로 기록 됩니다. 이후 분석에서 요소로 사용하려면 *colInfo* 매개 변수를 사용하여 수준을 지정합니다.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [rxImport를 사용하여 메모리에 데이터 로드](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)