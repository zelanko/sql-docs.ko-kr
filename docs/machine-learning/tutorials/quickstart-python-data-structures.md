---
title: '빠른 시작: Python 데이터 구조'
titleSuffix: SQL machine learning
description: 이 빠른 시작에서는 SQL 기계 학습을 사용하여 Python에서 데이터 구조 및 데이터 개체로 작업을 수행하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/28/2020
ms.topic: quickstart
author: cawrites
ms.author: chadam
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 18f16b45c6bc5f2069783333be7905af94a41b41
ms.sourcegitcommit: b93beb4f03aee2c1971909cb1d15f79cd479a35c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91497972"
---
# <a name="quickstart-data-structures-and-objects-using-python-with-sql-machine-learning"></a>빠른 시작: SQL 기계 학습에서 Python을 사용하는 데이터 구조 및 개체
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

이 빠른 시작에서는 [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md), [Azure SQL Managed Instance Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview) 또는 [SQL Server 빅 데이터 클러스터](../../big-data-cluster/machine-learning-services.md)에서 Python을 사용하는 경우 데이터 구조와 데이터 형식을 사용하는 방법을 알아봅니다. Python과 SQL Server 사이의 데이터 이동과 일반적으로 발생할 수 있는 문제에 대해 알아봅니다.

SQL 기계 학습은 표 형식 데이터를 사용할 때 유용한 Python **pandas** 패키지를 사용합니다. 하지만 Python에서 데이터베이스로 스칼라를 전달하기만 하면 작동하는 것은 아닙니다. 이 빠른 시작에서는 Python과 데이터베이스 사이에 표 형식 데이터를 전달할 때 발생할 수 있는 추가적인 문제들을 준비하기 위해 몇 가지 기본적인 데이터 구조 정의를 검토합니다.

처음에 알아야 할 개념은 다음과 같습니다.

- 데이터 프레임은 _여러_ 열이 포함된 테이블입니다.
- 데이터 프레임의 단일 열은 계열이라고 부르는 목록과 비슷한 개체입니다.
- 데이터 프레임의 단일 값은 셀이라고 부르고, 인덱스로 액세스됩니다.

data.frame에 표 형식 구조가 필요한 경우 계산의 단일 결과를 데이터 프레임으로 노출하려면 어떻게 할까요? 한 가지 답변은 데이터 프레임으로 쉽게 변환되는 계열로 단일 스칼라 값을 표시하는 것입니다.

> [!NOTE]
> 날짜를 반환할 때 SQL의 Python은 1753-01-01(-53690)에서 9999-12-31(2958463)까지 제한된 날짜 범위를 갖는 DATETIME을 사용합니다.

## <a name="prerequisites"></a>사전 요구 사항

이 빠른 시작을 실행하려면 다음과 같은 필수 구성 요소가 필요합니다.

- 다음 플랫폼 중 하나에 있는 SQL 데이터베이스:
  - [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md). Machine Learning Services를 설치하는 방법은 [Windows 설치 가이드](../install/sql-machine-learning-services-windows-install.md) 또는 [Linux 설치 가이드](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fmachine-learning%2Ftoc.json)를 참조하세요.
  - SQL Server 빅 데이터 클러스터. [SQL Server 빅 데이터 클러스터에서 Machine Learning Services 사용](../../big-data-cluster/machine-learning-services.md)을 참조하세요.
  - Azure SQL Managed Instance Machine Learning Services. 등록 방법은 [Azure SQL Managed Instance Machine Learning Services 개요](/azure/azure-sql/managed-instance/machine-learning-services-overview)를 참조하세요.

- Python 스크립트가 포함된 SQL 쿼리를 실행하기 위한 도구. 이 빠른 시작에서는 [Azure Data Studio](../../azure-data-studio/what-is.md)를 사용합니다.

## <a name="scalar-value-as-a-series"></a>계열로서의 스칼라 값

이 예에서는 몇 가지 수식을 계산하고 스칼라를 계열로 변환합니다.

1. 계열은 여기에 표시된 것처럼 수동으로 또는 프로그래밍 방식으로 할당할 수 있는 인덱스가 필요합니다.

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   a = 1
   b = 2
   c = a/b
   print(c)
   s = pandas.Series(c, index =["simple math example 1"])
   print(s)
   '
   ```

   계열이 data.frame으로 변환되지 않았기 때문에 값이 메시지 창에 반환되지만, 결과가 표 형식이 되어 있음을 알 수 있습니다.

   **결과**

   ```text
   STDOUT message(s) from external script: 
   0.5
   simple math example 1    0.5
   dtype: float64
   ```

1. 계열의 길이를 늘리려면 배열을 사용해서 새 값을 추가할 수 있습니다.

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   a = 1
   b = 2
   c = a/b
   d = a*b
   s = pandas.Series([c,d])
   print(s)
   '
   ```

   인덱스를 지정하지 않으면 0부터 시작하여 배열 길이로 끝나는 값이 포함된 인덱스가 생성됩니다.

   **결과**

   ```text
   STDOUT message(s) from external script:
   0    0.5
   1    2.0
   dtype: float64
   ```

1. **인덱스** 값의 수를 늘리지만 새 **데이터** 값을 추가하지 않으면, 계열을 채우기 위해 데이터 값이 반복됩니다.

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   a = 1
   b = 2
   c = a/b
   s = pandas.Series(c, index =["simple math example 1", "simple math example 2"])
   print(s)
   '
   ```

   **결과**

   ```text
   STDOUT message(s) from external script:
   0.5
   simple math example 1    0.5
   simple math example 2    0.5
   dtype: float64
   ```

## <a name="convert-series-to-data-frame"></a>계열을 데이터 프레임으로 변환

스칼라 쉭 결과를 테이블 형식 구조로 변환한 후에도 여전히 이를 SQL 기계 학습이 처리할 수 있는 형식으로 변환해야 합니다.

1. 계열을 data.frame으로 변환하려면 pandas [DataFrame](https://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe) 메서드를 호출합니다.

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   import pandas as pd
   a = 1
   b = 2
   c = a/b
   d = a*b
   s = pandas.Series([c,d])
   print(s)
   df = pd.DataFrame(s)
   OutputDataSet = df
   '
   WITH RESULT SETS((ResultValue FLOAT))
   ```

   결과는 아래에 표시되어 있습니다. data.frame에서 특정 값을 가져오기 위해 인덱스를 사용하더라도, 인덱스 값은 출력에 포함되지 않습니다.

   **결과**

   |ResultValue|
   |------|
   |0.5|
   |2|

## <a name="output-values-into-dataframe"></a>data.frame으로 값 출력

이제 수식 결과의 두 계열로부터 특정 값을 data.frame으로 출력합니다. 첫 번째 항목에는 Python으로 생성된 순차적 값의 인덱스가 포함됩니다. 두 번째 항목은 문자열 값에 대한 임의 인덱스를 사용합니다.

1. 다음 예제는 정수 인덱스를 사용해서 계열로부터 값을 가져옵니다.

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   import pandas as pd
   a = 1
   b = 2
   c = a/b
   d = a*b
   s = pandas.Series([c,d])
   print(s)
   df = pd.DataFrame(s, index=[1])
   OutputDataSet = df
   '
   WITH RESULT SETS((ResultValue FLOAT))
   ```

   **결과**

   |ResultValue|
   |------|
   |2.0|

   자동 생성된 인덱스는 0부터 시작됩니다. 범위를 벗어난 인덱스 값을 사용해서 어떤 결과가 발생하는지 살펴보세요.

1. 이제 문자열 인덱스를 사용하여 다른 데이터 프레임에서 단일 값을 가져옵니다.

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   import pandas as pd
   a = 1
   b = 2
   c = a/b
   s = pandas.Series(c, index =["simple math example 1", "simple math example 2"])
   print(s)
   df = pd.DataFrame(s, index=["simple math example 1"])
   OutputDataSet = df
   '
   WITH RESULT SETS((ResultValue FLOAT))
   ```

   **결과**

   |ResultValue|
   |------|
   |0.5|

   숫자 인덱스를 사용하여 이 계열로부터 값을 가져오려고 시도하면 오류가 발생합니다.

## <a name="next-steps"></a>다음 단계

SQL 기계 학습에서 고급 Python 함수를 작성하는 방법을 알아보려면 다음 빠른 시작을 참조하세요.

> [!div class="nextstepaction"]
> [고급 Python 함수 작성](quickstart-python-functions.md)
