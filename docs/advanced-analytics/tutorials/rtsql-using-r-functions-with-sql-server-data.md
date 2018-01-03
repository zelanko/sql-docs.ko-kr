---
title: "R 함수를 사용 하 여 SQL Server 데이터 (SQL 빠른 시작에서 R) | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
dev_langs:
- R
- SQL
ms.assetid: e2fe5d90-eee9-4daf-9eae-21d17b3ef320
caps.latest.revision: "8"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 0a536b0d569fba36c84b550bec0b60896b448e45
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2017
---
# <a name="using-r-functions-with-sql-server-data-r-in-sql-quickstart"></a>R 함수를 사용 하 여 SQL Server 데이터 (SQL 빠른 시작에서 R)

이제 기본 작업에 익숙해졌으므로 R의 재미있는 점을 살펴보겠습니다. 예를 들어 T-SQL을 사용하면 많은 고급 통계 함수를 구현하기가 복잡할 수 있지만 R을 사용하면 한 줄만 있으면 됩니다.  R Services를 통해 R 유틸리티 스크립트를 저장 프로시저에 쉽게 포함할 수 있습니다.

이러한 예제에서는 R 수학 및 유틸리티 함수를 SQL Server 저장 프로시저에 포함합니다.

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>난수를 생성하는 저장 프로시저 만들기

간단히 하기 위해 사용 R `stats` 패키지를 설치 및 R 서비스와 함께 기본적으로 로드 합니다. 패키지에는 일반 통계 태스크에 대한 수백 개의 함수가 포함되고, 이들 중 `rnorm` 함수는 표준 편차 및 평균을 고려하고 정규 분포를 사용하여 지정된 개수의 난수를 생성합니다.

예를 들어 이 R 코드는 표준 편차 3을 고려하여 평균 50에 대한 100개의 숫자를 반환합니다.

```R
as.data.frame(rnorm(100, mean = 50, sd = 3));
```

T-SQL에서 R의 이 줄을 호출하려면 sp_execute_external_script를 실행하고 다음과 같이 R 스크립트 매개 변수에 R 함수를 추가합니다.

```sql
EXEC sp_execute_external_script
      @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(100, mean = 50, sd =3));'
    , @input_data_1 = N'   ;'
      WITH RESULT SETS (([Density] float NOT NULL));
```

다른 난수 집합을 더 쉽게 생성할 수 있다면 어떻게 될까요?

가 SQL Server를 함께 사용 하면 쉽게: 저장된 프로시저는 사용자 로부터 인수를 정의 합니다. 그다음에 해당 인수를 R 스크립트에 변수로 전달합니다.

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

+ `@params`로 시작하는 줄은 R 코드에서 사용되는 모든 변수 및 해당하는 SQL 데이터 형식을 정의합니다.

+ 바로 뒤에 오는 줄은 SQL 매개 변수 이름을 해당 R 변수 이름에 매핑합니다.

이제 저장 프로시저에서 R 함수를 래핑했으므로 다음과 같이 쉽게 함수를 호출하고 다른 값을 전달할 수 있습니다.

```sql
EXEC MyRNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="related-resources"></a>관련 리소스

+ 추가 R 패키지를 설치 하 시겠습니까, 추가 정보 보기를 고급 통계 함수? 참조 [R 패키지를 관리 및 설치](../r/installing-and-managing-r-packages.md)합니다.

+ Microsoft R 팀이 새 R 패키지를 SQL Server 저장 프로시저를 사용 하 여 쉽게 parameterized 수 있는 형식으로 프로그램 독립 실행형 R 코드를 변환할 수 있도록 제공 **sqlrutils**합니다. 자세한 내용은 참조 [sqlrutils를 사용 하 여 저장된 프로시저를 만드는 방법을](../r/how-to-create-a-stored-procedure-using-sqlrutils.md)합니다.

## <a name="use-r-utility-functions-for-troubleshooting"></a>문제 해결에 R 유틸리티 함수 사용

기본적으로 설치 된 R 포함 됩니다는 `utils` 현재 R 환경 조사 하기 위한 다양 한 유틸리티 함수를 제공 하는 패키지입니다. 이 패키지는 SQL Server 및 외부 환경에서 R 코드가 실행되는 방식으로 불일치를 찾는 경우 유용할 수 있습니다.

예를 들어 R `memory.limit()` 함수를 사용하여 현재 R 환경에 사용할 메모리를 가져올 수 있습니다. `utils` 패키지는 설치되지만 기본적으로 로드되지 않으므로 먼저 `library()` 함수를 사용하여 로드해야 합니다.

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

많은 사용자가 R을와 같은 시스템 타이밍 함수를 사용 하 여 하고자 `system.time` 및 `proc.time`R 프로세스에서 사용 되는 시간을 캡처 및 성능 문제를 분석할 수, 합니다.

예제를 보려면 [3단원: 데이터 기능 만들기(데이터 과학 종단 간 연습)](../tutorials/walkthrough-create-data-features.md) 자습서를 참조하세요. 이 연습에서 R 시간 함수는 솔루션에 포함되어 데이터에서 기능을 생성할 수 있는 두 가지 메서드인 R 함수 및 T-SQL 함수의 성능을 비교합니다.

## <a name="next-lesson"></a>다음 단원

다음으로 SQL Server에서 R을 사용하여 예측 모델을 빌드합니다.

[예측 모델 만들기](../tutorials/rtsql-create-a-predictive-model-r.md)
