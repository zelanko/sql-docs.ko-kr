---
title: 고급 Python 함수 작성
titleSuffix: SQL Server Machine Learning Services
description: 이 빠른 시작에서는 SQL Server Machine Learning Services를 사용 하 여 고급 통계 계산을 위한 Python 함수를 작성 하는 방법에 대해 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e369e83c99543cc31287932a25949c2ddec98e89
ms.sourcegitcommit: 454270de64347db917ebe41c081128bd17194d73
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007723"
---
# <a name="quickstart-write-advanced-python-functions-with-sql-server-machine-learning-services"></a>빠른 시작: SQL Server Machine Learning Services를 사용 하 여 고급 Python 함수 작성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 빠른 시작에서는 SQL Server Machine Learning Services를 사용 하 여 SQL 저장 프로시저에 Python 수학 및 유틸리티 함수를 포함 하는 방법을 설명 합니다. T-sql에서 구현 하기에 복잡 한 고급 통계 함수는 한 줄의 코드를 사용 하 여 Python에서 수행할 수 있습니다.

## <a name="prerequisites"></a>사전 요구 사항

- 이 빠른 시작에서는 Python 언어가 설치 된 [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) 를 사용 하 여 SQL Server 인스턴스에 액세스할 수 있어야 합니다.

  SQL Server 인스턴스는 Azure 가상 머신 또는 온-프레미스에 있을 수 있습니다. 외부 스크립팅 기능은 기본적으로 사용 하지 않도록 설정 되어 있으므로 [외부 스크립팅을 사용 하도록 설정](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) 하 고 시작 하기 전에 **SQL Server 실행 패드 서비스가** 실행 중인지 확인 해야 할 수 있습니다.

- 또한 Python 스크립트를 포함 하는 SQL 쿼리를 실행 하기 위한 도구도 필요 합니다. 모든 데이터베이스 관리 또는 쿼리 도구를 사용 하 여 이러한 스크립트를 실행 하 고 SQL Server 인스턴스에 연결 하 고 T-sql 쿼리 또는 저장 프로시저를 실행할 수 있습니다. 이 빠른 시작에서는 [SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)를 사용 합니다.

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>난수를 생성하는 저장 프로시저 만들기

편의를 위해 Python이 설치 된 SQL Server Machine Learning Services에 기본적으로 설치 및 로드 되는 Python `numpy` 패키지를 사용 하겠습니다. 이 패키지에는 일반 통계 작업용으로 수백 개의 함수가 포함되어 있으며, 그 중 `random.normal` 함수는 주어진 표준 편차와 평균으로 정규 분포를 사용한 지정된 수의 난수를 생성합니다.

예를 들어 다음 Python 코드는 표준 편차가 3 인 경우 100를 평균 50로 반환 합니다.

```Python
numpy.random.normal(size=100, loc=50, scale=3)
```

T-sql에서이 Python 줄을 호출 하려면 `sp_execute_external_script`의 Python 스크립트 매개 변수에 Python 함수를 추가 합니다. 출력에는 데이터 프레임이 필요 하므로 `pandas`을 사용 하 여 변환 하십시오.

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

다른 난수 집합을 더 쉽게 생성하려면 어떻게 하면 될까요?

SQL Server와 함께 사용 하는 것이 쉽습니다. 사용자가 인수를 가져온 다음 해당 인수를 Python 스크립트에 변수로 전달 하는 저장 프로시저를 정의 합니다.

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

- @No__t-0으로 시작 하는 줄은 Python 코드에서 사용 하는 모든 변수와 해당 하는 SQL 데이터 형식을 정의 합니다.

- 바로 뒤에 오는 줄은 SQL 매개 변수 이름을 해당 Python 변수 이름에 매핑합니다.

이제 Python 함수를 저장 프로시저에 래핑하여 다음과 같이 쉽게 함수를 호출 하 고 다른 값을 전달할 수 있습니다.

```sql
EXECUTE MyPyNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="use-python-utility-functions-for-troubleshooting"></a>문제 해결을 위해 Python 유틸리티 함수 사용

Python 패키지는 현재 Python 환경을 조사 하기 위한 다양 한 유틸리티 함수를 제공 합니다. 이러한 함수는 Python 코드가 SQL Server 및 외부 환경에서 수행 하는 방식에서 불일치를 발견 하는 경우에 유용할 수 있습니다.

예를 들어 `time` 패키지에서 시스템 타이밍 함수를 사용 하 여 Python 프로세스에서 사용 하는 시간을 측정 하 고 성능 문제를 분석할 수 있습니다.

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

SQL Server에서 Python을 사용 하 여 기계 학습 모델을 만들려면이 빠른 시작을 수행 합니다.

> [!div class="nextstepaction"]
> [빠른 시작: SQL Server Machine Learning Services @ no__t를 사용 하 여 Python에서 예측 모델 만들기 및 점수 매기기

Machine Learning Services SQL Server에 대 한 자세한 내용은 다음을 참조 하세요.

- [SQL Server Machine Learning Services (Python 및 R)는 무엇 인가요?](../what-is-sql-server-machine-learning.md)
