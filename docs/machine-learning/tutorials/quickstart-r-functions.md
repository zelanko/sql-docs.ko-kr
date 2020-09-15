---
title: '빠른 시작: R 함수'
titleSuffix: SQL machine learning
description: 이 빠른 시작에서는 SQL 기계 학습에서 R 수학 및 유틸리티 함수를 사용하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/21/2020
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: e5700e5b0bab7df8506725c2522c28479155fdab
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88178476"
---
# <a name="quickstart-r-functions-with-sql-machine-learning"></a>빠른 시작: SQL 기계 학습에서 R 함수 사용
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
이 빠른 시작에서는 [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) 또는 [빅 데이터 클러스터](../../big-data-cluster/machine-learning-services.md)에서 R 수학 및 유틸리티 함수를 사용하는 방법을 알아봅니다. 통계 함수는 T-SQL에서 구현하기에 복잡한 경우가 많으며 다만 몇 줄의 코드만으로 R에서 수행할 수 있습니다.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
이 빠른 시작에서는 [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md)에서 R 수학 및 유틸리티 함수를 사용하는 방법을 알아봅니다. 통계 함수는 T-SQL에서 구현하기에 복잡한 경우가 많으며 다만 몇 줄의 코드만으로 R에서 수행할 수 있습니다.
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
이 빠른 시작에서는 [SQL Server R Services](../r/sql-server-r-services.md)에서 R 수학 및 유틸리티 함수를 사용하는 방법을 알아봅니다. 통계 함수는 T-SQL에서 구현하기에 복잡한 경우가 많으며 다만 몇 줄의 코드만으로 R에서 수행할 수 있습니다.
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
이 빠른 시작에서는 [Azure SQL Managed Instance Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview)에서 R을 사용할 때 데이터 구조와 데이터 형식을 사용하는 방법을 알아봅니다. R과 SQL Managed Instance 사이의 데이터 이동과 일반적으로 발생할 수 있는 문제에 대해 알아봅니다.
::: moniker-end

## <a name="prerequisites"></a>사전 요구 사항

이 빠른 시작을 실행하려면 다음과 같은 필수 구성 요소가 필요합니다.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
- SQL Server Machine Learning Services. Machine Learning Services를 설치하는 방법은 [Windows 설치 가이드](../install/sql-machine-learning-services-windows-install.md) 또는 [Linux 설치 가이드](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fmachine-learning%2Ftoc.json)를 참조하세요. [SQL Server 빅 데이터 클러스터에서 Machine Learning Services를 사용하도록 설정](../../big-data-cluster/machine-learning-services.md)할 수도 있습니다.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
- SQL Server Machine Learning Services. Machine Learning Services를 설치하는 방법은 [Windows 설치 가이드](../install/sql-machine-learning-services-windows-install.md)를 참조하세요. 
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
- SQL Server 2016 R Services. R Services를 설치하는 방법은 [Windows 설치 가이드](../install/sql-r-services-windows-install.md)를 참조하세요.
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
- Azure SQL Managed Instance Machine Learning Services. 등록 방법은 [Azure SQL Managed Instance Machine Learning Services 개요](/azure/azure-sql/managed-instance/machine-learning-services-overview)를 참조하세요.
::: moniker-end

- R 스크립트가 포함된 SQL 쿼리를 실행하기 위한 도구. 이 빠른 시작에서는 [Azure Data Studio](../../azure-data-studio/what-is.md)를 사용합니다.

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>난수를 생성하는 저장 프로시저 만들기

간단히 하기 위해 기본적으로 설치 및 로드되는 R `stats` 패키지를 사용하겠습니다. 패키지에는 일반 통계 태스크에 대한 수백 개의 함수가 포함되고, 이들 중 `rnorm` 함수는 표준 편차 및 평균을 고려하고 정규 분포를 사용하여 지정된 개수의 난수를 생성합니다.

예를 들어 다음 R 코드는 표준 편차 3을 고려하여 평균 50에 대한 100개의 숫자를 반환합니다.

```R
as.data.frame(rnorm(100, mean = 50, sd = 3));
```

T-SQL에서 R의 이 줄을 호출하려면 다음과 같이 `sp_execute_external_script`의 R 스크립트 매개 변수에 R 함수를 추가합니다.

```sql
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(100, mean = 50, sd =3));'
    , @input_data_1 = N'   ;'
      WITH RESULT SETS (([Density] float NOT NULL));
```

다른 난수 집합을 더 쉽게 생성할 수 있다면 어떻게 될까요?

T-SQL과 결합하면 쉽습니다. 사용자로부터 인수를 가져오는 저장 프로시저를 정의한 다음, 해당 인수를 R 스크립트에 변수로 전달합니다.

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

- `@params`로 시작하는 줄은 R 코드에서 사용되는 모든 변수 및 해당하는 SQL 데이터 형식을 정의합니다.

- 바로 뒤에 오는 줄은 SQL 매개 변수 이름을 해당 R 변수 이름에 매핑합니다.

이제 저장 프로시저에서 R 함수를 래핑했으므로 다음과 같이 쉽게 함수를 호출하고 다른 값을 전달할 수 있습니다.

```sql
EXECUTE MyRNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="use-r-utility-functions-for-troubleshooting"></a>문제 해결에 R 유틸리티 함수 사용

기본적으로 설치되는 **utils** 패키지는 R 환경을 조사하기 위한 다양한 유틸리티 함수를 제공합니다. 이러한 함수는 SQL Server 및 외부 환경에서 R 코드가 실행되는 방식으로 불일치를 찾는 경우에 유용할 수 있습니다.

예를 들어 R에서 `system.time` 및 `proc.time`과 같은 시스템 시간 함수를 사용하여 R 프로세스에 사용된 시간을 파악하고 성능 문제를 분석할 수 있습니다. 예를 들어 솔루션에 R 타이밍 함수가 포함된 [데이터 기능 만들기](../tutorials/walkthrough-create-data-features.md) 자습서를 참조하세요.

```sql
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N'
        library(utils);
        start.time <- proc.time();
        
        # Run R processes
        
        elapsed_time <- proc.time() - start.time;'
```

## <a name="next-steps"></a>다음 단계

SQL 기계 학습에서 R을 사용하여 기계 학습 모델을 만들려면 다음 빠른 시작을 수행합니다.

> [!div class="nextstepaction"]
> [R에서 SQL 기계 학습을 사용하여 예측 모델 만들기 및 채점](quickstart-r-train-score-model.md)
