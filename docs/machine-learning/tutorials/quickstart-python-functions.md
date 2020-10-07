---
title: '빠른 시작: Python 함수'
titleSuffix: SQL machine learning
description: 이 빠른 시작에서는 SQL 기계 학습에서 Python 수학 및 유틸리티 함수를 사용하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/28/2020
ms.topic: quickstart
author: cawrites
ms.author: chadam
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: a810a5dbc6e5d07f0926d99dd62c71e38dfacdff
ms.sourcegitcommit: b93beb4f03aee2c1971909cb1d15f79cd479a35c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91497947"
---
# <a name="quickstart-python-functions-with-sql-machine-learning"></a>빠른 시작: SQL 기계 학습에서 Python 함수 사용
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

이 빠른 시작에서는 [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md), [Azure SQL Managed Instance Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview) 또는 [SQL Server 빅 데이터 클러스터](../../big-data-cluster/machine-learning-services.md)에서 Python 수학 및 유틸리티 함수를 사용하는 방법을 알아봅니다. 통계 함수는 T-SQL에서 구현하기에 복잡한 경우가 많으며 다만 몇 줄의 코드만으로 Python에서 수행할 수 있습니다.

## <a name="prerequisites"></a>사전 요구 사항

이 빠른 시작을 실행하려면 다음과 같은 필수 구성 요소가 필요합니다.

- 다음 플랫폼 중 하나에 있는 SQL 데이터베이스:
  - [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md). Machine Learning Services를 설치하는 방법은 [Windows 설치 가이드](../install/sql-machine-learning-services-windows-install.md) 또는 [Linux 설치 가이드](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fmachine-learning%2Ftoc.json)를 참조하세요.
  - SQL Server 빅 데이터 클러스터. [SQL Server 빅 데이터 클러스터에서 Machine Learning Services 사용](../../big-data-cluster/machine-learning-services.md)을 참조하세요.
  - Azure SQL Managed Instance Machine Learning Services. 등록 방법은 [Azure SQL Managed Instance Machine Learning Services 개요](/azure/azure-sql/managed-instance/machine-learning-services-overview)를 참조하세요.

- Python 스크립트가 포함된 SQL 쿼리를 실행하기 위한 도구. 이 빠른 시작에서는 [Azure Data Studio](../../azure-data-studio/what-is.md)를 사용합니다.

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>난수를 생성하는 저장 프로시저 만들기

간단히 하기 위해 기본적으로 설치 및 로드되는 Python `numpy` 패키지를 사용하겠습니다. 패키지에는 일반 통계 태스크에 대한 수백 개의 함수가 포함되고, 이들 중 `random.normal` 함수는 표준 편차 및 평균을 고려하고 정규 분포를 사용하여 지정된 개수의 난수를 생성합니다.

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

다른 난수 집합을 더 쉽게 생성할 수 있다면 어떻게 될까요? 사용자로부터 인수를 가져오는 저장 프로시저를 정의한 다음, 해당 인수를 Python 스크립트에 변수로 전달합니다.

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

SQL 기계 학습에서 Python을 사용하여 기계 학습 모델을 만들려면 다음 빠른 시작을 수행합니다.

> [!div class="nextstepaction"]
> [빠른 시작: Python에서 예측 모델 만들기 및 점수 매기기](quickstart-python-train-score-model.md)
