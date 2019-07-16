---
title: R 함수-SQL Server Machine Learning을 보여주는 빠른 시작
description: 이 빠른 시작에서는 고급 통계 계산을 위해 R 함수를 작성 하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: fa2d47729641e8efd13e9e30be7a61186a892b5c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962017"
---
# <a name="quickstart-using-r-functions"></a>빠른 시작: R 함수 사용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이전 빠른 시작을 완료 하는 경우 기본 작업을 사용 하 여 친숙 하 고 통계 함수와 같은 더 복잡 한 항목에 대 한 준비 하는 것이 여러분이 합니다. T-SQL에서 구현 하는 복잡 한 고급 통계 함수 코드 한 줄만을 사용 하 여 R에서 수행할 수 있습니다.

이 빠른 시작에서는 R 수학를 포함할 수 있습니다 및 저장 프로시저를 SQL Server 유틸리티 함수입니다.

## <a name="prerequisites"></a>사전 요구 사항

이전 빠른 시작에서는 [SQL Server에 있는지 확인 하는 R](quickstart-r-verify.md), 정보를 제공 하 고이 빠른 시작에 필요한 R 환경 설정에 대 한 링크입니다.

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>난수를 생성하는 저장 프로시저 만들기

간단히 하기 위해 R을 사용 하겠습니다 `stats` 패키지를 설치 하 고 SQL Server에서 R 기능 지원을 설치 하면 기본적으로 로드 됩니다. 이 패키지에는 일반 통계 작업용으로 수백 개의 함수가 포함되어 있으며, 그 중 `rnorm` 함수는 주어진 표준 편차와 평균으로 정규 분포를 사용한 지정된 수의 난수를 생성합니다.

예를 들어 이 R 코드는 평균 50, 표준 편차 3에 기반을 둔 100개의 숫자를 반환합니다.

```R
as.data.frame(rnorm(100, mean = 50, sd = 3));
```

이 R 라인을 T-SQL에서 호출하려면 sp_execute_external_script를 실행하고 다음과 같이 R 스크립트 매개 변수에 R 함수를 추가합니다.

```sql
EXEC sp_execute_external_script
      @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(100, mean = 50, sd =3));'
    , @input_data_1 = N'   ;'
      WITH RESULT SETS (([Density] float NOT NULL));
```

다른 난수 집합을 더 쉽게 생성하려면 어떻게 하면 될까요?

SQL Server와 결합하면 쉬워집니다. 사용자로부터 인수를 가져오는 저장 프로시저를 정의합니다. 그런 다음 그 인수를 R 스크립트에 변수로 전달합니다.

```sql
CREATE PROCEDURE MyRNorm (@param1 int, @param2 int, @param3 int)
AS
    EXEC sp_execute_external_script
      @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(mynumbers, mymean, mysd));'
    , @input_data_1 = N'   ;'
    , @params = N' @mynumbers int, @mymean int, @mysd int'
    , @mynumbers = @param1
    , @mymean = @param2
    , @mysd = @param3
    WITH RESULT SETS (([Density] float NOT NULL));
```

+ 첫 번째 줄은 저장 프로시저가 실행될 때 필요한 각 SQL 입력 매개 변수를 정의합니다.

+ `@params`로 시작하는 줄은 R 코드에서 사용되는 변수들과 해당하는 SQL 데이터 형식을 정의합니다.

+ 바로 뒤에 오는 줄은 SQL 매개 변수 이름을 해당 R 변수 이름에 매핑합니다.

이제 저장 프로시저에서 R 함수를 래핑했으므로 다음과 같이 쉽게 함수를 호출하고 다른 값을 전달할 수 있습니다.

```sql
EXEC MyRNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="use-r-utility-functions-for-troubleshooting"></a>문제 해결에 R 유틸리티 함수 사용

기본적으로 R 설치에는 `utils` 패키지가 포함되며 현재 R 환경을 조사하기 위한 다양한 유틸리티 함수를 제공합니다. 이 패키지는 R 코드가 SQL Server 내부와 외부 환경에서 실행되는 방식이므로 불일치를 찾는 경우 유용할 수 있습니다.

예를 들어 R의 `memory.limit()` 함수를 사용하여 현재 R 환경에 사용할 메모리를 가져올 수 있습니다. `utils` 패키지는 기본적으로 로드되지 않으므로 먼저 `library()` 함수를 사용하여 로드해야 합니다.

```sql
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N'
        library(utils);
        mymemory <- memory.limit();
        OutputDataSet <- as.data.frame(mymemory);'
    , @input_data_1 = N' ;'
WITH RESULT SETS (([Col1] int not null));
```

많은 사용자가 성능 문제 분석을 위해 R 프로세스가 사용하는 시간을 캡처해주는 `sy`system.time` `proc.time` 같은 시스템 타이밍 함수를 사용합니다.

예를 들어이 자습서를 참조 하세요. [데이터 기능 만들기](../tutorials/walkthrough-create-data-features.md)합니다. 이 연습에서는 R 시간 함수는 데이터에서 기능을 만들기 위한 두 가지 방법의 성능을 비교 하는 솔루션에 포함 됩니다. R 함수 및 T-SQL 함수의 성능을 비교합니다.

## <a name="next-steps"></a>다음 단계

다음으로 SQL Server에서 R을 사용하여 예측 모델을 빌드합니다.

> [!div class="nextstepaction"]
> [빠른 시작: 예측 모델 만들기](quickstart-r-create-predictive-model.md)
