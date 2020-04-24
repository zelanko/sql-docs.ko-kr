---
title: '빠른 시작: Python 함수'
description: 이 빠른 시작에서는 SQL Server Machine Learning Services와 함께 Python 수학 및 유틸리티 함수를 사용하는 방법에 대해 알아보겠습니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/27/2020
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 577bb4e6d956c53182a20f0e363642946c33c92c
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487333"
---
# <a name="quickstart-python-functions-with-sql-server-machine-learning-services"></a>빠른 시작: SQL Server Machine Learning Services를 사용한 Python 함수
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 빠른 시작에서는 SQL Server Machine Learning Services와 함께 Python 수학 및 유틸리티 함수를 사용하는 방법에 대해 알아보겠습니다. 통계 함수는 T-SQL에서 구현하기에 복잡한 경우가 많으며 다만 몇 줄의 코드만으로 Python에서 수행할 수 있습니다.

## <a name="prerequisites"></a>사전 요구 사항

- 이 빠른 시작을 수행하려면 Python 언어가 설치된 [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)가 포함된 SQL Server 인스턴스에 대한 액세스 권한이 필요합니다.

  SQL Server 인스턴스는 Azure 가상 머신 또는 온-프레미스에 있을 수 있습니다. 외부 스크립팅 기능은 기본적으로 사용하지 않도록 설정되어 있으므로 시작하기 전에 [외부 스크립팅을 활성화](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature)하고 **SQL Server 실행 패드 서비스**가 실행 중인지 확인해야 합니다.

- 또한 Python 스크립트가 포함된 SQL 쿼리를 실행하기 위한 도구가 필요합니다. SQL Server 인스턴스에 연결할 수 있는 데이터베이스 관리 또는 쿼리 도구를 사용하여 이러한 스크립트를 실행하고 T-SQL 쿼리 또는 저장 프로시저를 실행할 수 있습니다. 이 빠른 시작에서는 [SSMS(SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)를 사용합니다.

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>난수를 생성하는 저장 프로시저 만들기

편의상 Python `numpy` 패키지를 사용합니다. 이 패키지는 Python이 설치된 SQL Server Machine Learning Services에 기본적으로 설치되고 로드됩니다. 패키지에는 일반 통계 태스크에 대한 수백 개의 함수가 포함되고, 이들 중 `random.normal` 함수는 표준 편차 및 평균을 고려하고 정규 분포를 사용하여 지정된 개수의 난수를 생성합니다.

예를 들어 다음 Python 코드는 표준 편차 3을 고려하여 평균 50에 대한 100개의 숫자를 반환합니다.

```Python
numpy.random.normal(size=100, loc=50, scale=3)
```

T-SQL에서 이 Python 줄을 호출하려면 `sp_execute_external_script`의 Python 스크립트 매개 변수에 Python 함수를 추가합니다. 출력에는 데이터 프레임이 필요하므로 `pandas`를 사용하여 변환합니다.

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import numpy
import pandas
OutputDataSet = pandas.DataFrame(numpy.random.normal(size=100, loc=50, scale=3));
'
    , @input_data_1 = N'   ;'
WITH RESULT SETS(([Density] FLOAT NOT NULL));
```

다른 난수 집합을 더 쉽게 생성할 수 있다면 어떻게 될까요?

SQL Server와 결합하면 쉽습니다. 사용자로부터 인수를 가져오는 저장 프로시저를 정의한 다음, 해당 인수를 Python 스크립트에 변수로 전달합니다.

```sql
CREATE PROCEDURE MyPyNorm (
      @param1 INT
    , @param2 INT
    , @param3 INT
    )
AS
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import numpy
import pandas
OutputDataSet = pandas.DataFrame(numpy.random.normal(size=mynumbers, loc=mymean, scale=mysd));
'
    , @input_data_1 = N'   ;'
    , @params = N' @mynumbers int, @mymean int, @mysd int'
    , @mynumbers = @param1
    , @mymean = @param2
    , @mysd = @param3
WITH RESULT SETS(([Density] FLOAT NOT NULL));
```

- 첫 번째 줄은 저장 프로시저가 실행될 때 필요한 각 SQL 입력 매개 변수를 정의합니다.

- `@params`로 시작하는 줄은 Python 코드에서 사용되는 모든 변수와 해당 SQL 데이터 형식을 정의합니다.

- 바로 뒤에 오는 줄은 SQL 매개 변수 이름을 해당 Python 변수 이름에 매핑합니다.

이제 저장 프로시저에서 Python 함수를 래핑했으므로 다음과 같이 쉽게 함수를 호출하고 다른 값을 전달할 수 있습니다.

```sql
EXECUTE MyPyNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="use-python-utility-functions-for-troubleshooting"></a>문제 해결을 위해 Python 유틸리티 함수 사용

Python 패키지는 현재 Python 환경을 조사하기 위한 다양한 유틸리티 함수를 제공합니다. 이러한 함수는 SQL Server 및 외부 환경에서 Python 코드가 실행되는 방식으로 불일치를 찾는 경우에 유용할 수 있습니다.

예를 들어 `time` 패키지의 시스템 타이밍 함수를 사용하여 Python 프로세스에 사용되는 시간을 측정하고 성능 문제를 분석할 수 있습니다.

```sql
EXECUTE sp_execute_external_script
      @language = N'Python'
    , @script = N'
import time
start_time = time.time()

# Run Python processes

elapsed_time = time.time() - start_time
'
    , @input_data_1 = N' ;';
```

## <a name="next-steps"></a>다음 단계

SQL Server에서 Python을 사용하여 기계 학습 모델을 만들려면 다음 빠른 시작을 수행합니다.

> [!div class="nextstepaction"]
> [빠른 시작: SQL Server Machine Learning Services를 사용하여 Python에서 예측 모델 만들기 및 점수 매기기](quickstart-python-train-score-model.md)

SQL Server Machine Learning Services에 대한 자세한 내용은 다음을 참조하세요.

- [SQL Server Machine Learning Services(Python 및 R)란?](../sql-server-machine-learning-services.md)
