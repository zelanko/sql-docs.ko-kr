---
title: R 함수를 SQL Server 데이터와 함께 사용하기(SQL에서 R 빠른 시작) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 52b03b16c55b4ae8a772c2c12861fcc4b184d1f4
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34585745"
---
# <a name="using-r-functions-with-sql-server-data-r-in-sql-quickstart"></a>R 함수를 SQL Server 데이터와 함께 사용하기(SQL에서 R 빠른 시작)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이제 기본 작업에 익숙해졌으므로 R의 재미있는 점을 살펴보겠습니다. 예를 들어 T-SQL을 사용하면 많은 고급 통계 함수를 구현하기가 복잡할 수 있지만 R을 사용하면 한 줄만 있으면 됩니다.  R Services를 통해 R 유틸리티 스크립트를 저장 프로시저에 쉽게 포함할 수 있습니다.

이 예제에서는 R의 수학 및 유틸리티 함수를 SQL Server 저장 프로시저에 포함할 것입니다.

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>난수를 생성하는 저장 프로시저 만들기

단순하게 사용하기 위해, R Services에서 기본적으로 설치 및 로드되는 R `stats` 패키지를 사용합니다. 이 패키지에는 일반 통계 작업용으로 수백 개의 함수가 포함되어 있으며, 그 중 `rnorm` 함수는 주어진 표준 편차와 평균으로 정규 분포를 사용한 지정된 수의 난수를 생성합니다.

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

예제를 보려면 [3단원: 데이터 특성 만들기(R SQL Server용 데이터 과학 전체 과정 연습)](../tutorials/walkthrough-create-data-features.md) 자습서를 참조하세요. 이 연습에서는 데이터로부터 특성을 만들기 위한 두 가지 방법(R 함수 vs. T-SQL 함수)의 성능을 비교하는 해결 방법에서 R 타이밍 함수가 포함됩니다. (역주: proc_time()이 사용됨) T-SQL 함수의 성능을 비교합니다.

## <a name="next-lesson"></a>다음 단원

다음으로 SQL Server에서 R을 사용하여 예측 모델을 빌드합니다.

[예측 모델 만들기](../tutorials/rtsql-create-a-predictive-model-r.md)
