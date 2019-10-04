---
title: 고급 R 함수 작성
titleSuffix: SQL Server Machine Learning Services
description: 이 빠른 시작에서는 SQL Server Machine Learning Services를 사용 하 여 고급 통계 계산을 위해 R 함수를 작성 하는 방법에 대해 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/03/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 55849cec8b3362b3a5f2786e007f08f0c376b8a5
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71951859"
---
# <a name="quickstart-write-advanced-r-functions-with-sql-server-machine-learning-services"></a>빠른 시작: SQL Server Machine Learning Services를 사용 하 여 고급 R 함수 작성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 빠른 시작에서는 SQL Server Machine Learning Services를 사용 하 여 SQL 저장 프로시저에 R 수학 및 유틸리티 함수를 포함 하는 방법을 설명 합니다. T-sql에서 구현 하기에 복잡 한 고급 통계 함수는 단 한 줄의 코드를 사용 하 여 R에서 수행할 수 있습니다.

## <a name="prerequisites"></a>사전 요구 사항

- 이 빠른 시작을 사용 하려면 R 언어가 설치 된 [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) 를 사용 하 여 SQL Server 인스턴스에 액세스 해야 합니다.

  SQL Server 인스턴스는 Azure 가상 머신 또는 온-프레미스에 있을 수 있습니다. 외부 스크립팅 기능은 기본적으로 사용 하지 않도록 설정 되어 있으므로 [외부 스크립팅을 사용 하도록 설정](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) 하 고 시작 하기 전에 **SQL Server 실행 패드 서비스가** 실행 중인지 확인 해야 할 수 있습니다.

- R 스크립트를 포함 하는 SQL 쿼리를 실행 하기 위한 도구도 필요 합니다. 모든 데이터베이스 관리 또는 쿼리 도구를 사용 하 여 이러한 스크립트를 실행 하 고 SQL Server 인스턴스에 연결 하 고 T-sql 쿼리 또는 저장 프로시저를 실행할 수 있습니다. 이 빠른 시작에서는 [SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)를 사용 합니다.

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>난수를 생성하는 저장 프로시저 만들기

간단히 하기 위해 r 설치 된 SQL Server Machine Learning Services `stats` 에서 기본적으로 설치 및 로드 되는 r 패키지를 사용 하겠습니다. 이 패키지에는 일반 통계 작업용으로 수백 개의 함수가 포함되어 있으며, 그 중 `rnorm` 함수는 주어진 표준 편차와 평균으로 정규 분포를 사용한 지정된 수의 난수를 생성합니다.

예를 들어 다음 R 코드는 표준 편차가 3 인 경우 100를 평균 50로 반환 합니다.

```R
as.data.frame(rnorm(100, mean = 50, sd = 3));
```

T-sql에서 r의이 줄을 호출 하려면 다음과 같이의 `sp_execute_external_script`r 스크립트 매개 변수에 r 함수를 추가 합니다.

```sql
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(100, mean = 50, sd =3));'
    , @input_data_1 = N'   ;'
      WITH RESULT SETS (([Density] float NOT NULL));
```

다른 난수 집합을 더 쉽게 생성하려면 어떻게 하면 될까요?

SQL Server와 함께 사용 하는 것이 쉽습니다. 사용자의 인수를 가져온 다음 해당 인수를 R 스크립트에 변수로 전달 하는 저장 프로시저를 정의 합니다.

```sql
CREATE PROCEDURE MyRNorm (
    @param1 INT
    , @param2 INT
    , @param3 INT
    )
AS
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(mynumbers, mymean, mysd));'
    , @input_data_1 = N'   ;'
    , @params = N' @mynumbers int, @mymean int, @mysd int'
    , @mynumbers = @param1
    , @mymean = @param2
    , @mysd = @param3
WITH RESULT SETS(([Density] FLOAT NOT NULL));
```

- 첫 번째 줄은 저장 프로시저가 실행될 때 필요한 각 SQL 입력 매개 변수를 정의합니다.

- `@params`로 시작하는 줄은 R 코드에서 사용되는 변수들과 해당하는 SQL 데이터 형식을 정의합니다.

- 바로 뒤에 오는 줄은 SQL 매개 변수 이름을 해당 R 변수 이름에 매핑합니다.

이제 저장 프로시저에서 R 함수를 래핑했으므로 다음과 같이 쉽게 함수를 호출하고 다른 값을 전달할 수 있습니다.

```sql
EXECUTE MyRNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="use-r-utility-functions-for-troubleshooting"></a>문제 해결에 R 유틸리티 함수 사용

기본적으로 설치 되는 **유틸리티** 패키지는 현재 R 환경을 조사 하기 위한 다양 한 유틸리티 함수를 제공 합니다. 이러한 함수는 R 코드가 SQL Server 및 외부 환경에서 수행 하는 방식에서 불일치를 발견 하는 경우에 유용할 수 있습니다.

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

> [!TIP]
> 대부분의 사용자는 r에서 시스템 타이밍 함수 (예: `system.time` 및 `proc.time`)를 사용 하 여 r 프로세스에 사용 되는 시간을 캡처하고 성능 문제를 분석 하는 것입니다. 예를 들어 솔루션에 R 타이밍 함수가 포함 된 [데이터 기능 만들기](../tutorials/walkthrough-create-data-features.md) 자습서를 참조 하세요.

## <a name="next-steps"></a>다음 단계

Machine Learning Services SQL Server에 대 한 자세한 내용은 다음을 참조 하세요.

- [SQL Server Machine Learning Services (Python 및 R)는 무엇 인가요?](../what-is-sql-server-machine-learning.md)
