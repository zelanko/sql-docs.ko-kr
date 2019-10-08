---
title: Python 및 SQL 데이터 형식 및 개체 작업
titleSuffix: SQL Server Machine Learning Services
description: 이 빠른 시작에서는 Python에서 데이터 형식 및 데이터 개체를 사용 하 고 SQL Server Machine Learning Services SQL Server 하는 방법에 대해 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c09c9ad4625520054f2d3f103ec055c37764aed2
ms.sourcegitcommit: 84e6922a57845a629391067ca4803e8d03e0ab90
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72008433"
---
# <a name="quickstart-handle-data-types-and-objects-using-python-in-sql-server-machine-learning-services"></a>빠른 시작: SQL Server Machine Learning Services에서 Python을 사용 하 여 데이터 형식 및 개체를 처리 합니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 빠른 시작에서는 SQL Server Machine Learning Services에서 Python을 사용 하는 경우 데이터 구조를 사용 하는 방법을 보여 줍니다.

SQL Server는 Python **pandas** 패키지를 사용 하 여 테이블 형식 데이터로 작업 하는 데 유용 합니다. 그러나 Python에서 SQL Server로 스칼라를 전달 하 고 "단지 작동" 하는 것으로 예측할 수는 없습니다. 이 빠른 시작에서는 몇 가지 기본 데이터 형식 정의를 검토 하 여 Python과 SQL Server 사이에 표 형식 데이터를 전달할 때 실행할 수 있는 추가 문제를 준비 합니다.

앞에서 소개 하는 개념은 다음과 같습니다.

- 데이터 프레임은 _여러_ 열이 있는 테이블입니다.
- 데이터 프레임의 단일 열은 계열 이라는 목록 형식의 개체입니다.
- 데이터 프레임의 단일 값을 셀 이라고 하며 인덱스를 통해 액세스 합니다.

데이터 프레임에 테이블 형식 구조가 필요한 경우 계산의 단일 결과를 데이터 프레임으로 노출 하는 방법 한 가지 대답은 단일 스칼라 값을 데이터 프레임으로 쉽게 변환 되는 계열로 나타내는 것입니다. 

> [!NOTE]
> 날짜를 반환할 때 SQL의 Python은 날짜 범위가 1753-01-01 (-53690)에서 9999-12-31 (2958463)까지 제한 된 DATETIME을 사용 합니다. 

## <a name="prerequisites"></a>사전 요구 사항

- 이 빠른 시작에서는 Python 언어가 설치 된 [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) 를 사용 하 여 SQL Server 인스턴스에 액세스할 수 있어야 합니다.

- 또한 Python 스크립트를 포함 하는 SQL 쿼리를 실행 하기 위한 도구도 필요 합니다. 모든 데이터베이스 관리 또는 쿼리 도구를 사용 하 여 이러한 스크립트를 실행 하 고 SQL Server 인스턴스에 연결 하 고 T-sql 쿼리 또는 저장 프로시저를 실행할 수 있습니다. 이 빠른 시작에서는 [SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)를 사용 합니다.

## <a name="scalar-value-as-a-series"></a>스칼라 값 (계열)

이 예에서는 몇 가지 간단한 수학 연산을 수행 하 고 스칼라를 계열로 변환 합니다.

1. 계열에는 여기에 나와 있는 것 처럼 수동으로 할당 하거나 프로그래밍 방식으로 할당할 수 있는 인덱스가 필요 합니다.

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

   계열은 데이터 프레임으로 변환 되지 않았기 때문에 메시지 창에 값이 반환 되지만 결과의 테이블 형식이 더 많을 수 있습니다.

   **결과**

   ```text
   STDOUT message(s) from external script: 
   0.5
   simple math example 1    0.5
   dtype: float64
   ```

1. 계열의 길이를 늘리려면 배열을 사용 하 여 새 값을 추가할 수 있습니다. 

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

   인덱스를 지정 하지 않으면 0으로 시작 하 여 배열의 길이로 끝나는 값을 포함 하는 인덱스가 생성 됩니다.

   **결과**

   ```text
   STDOUT message(s) from external script: 
   0    0.5
   1    2.0
   dtype: float64
   ```

1. **인덱스** 값의 수를 늘리고 새 **데이터** 값을 추가 하지 않으면 데이터 값이 반복 되어 계열을 채웁니다.

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

스칼라 수학 결과를 테이블 형식 구조체로 변환한 후에는 SQL Server 처리할 수 있는 형식으로 변환 해야 합니다.

1. 계열을 데이터 프레임으로 변환 하려면 pandas [데이터 프레임](https://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe) 메서드를 호출 합니다.

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

   결과는 다음과 같습니다. 인덱스를 사용 하 여 데이터 프레임에서 특정 값을 가져오는 경우에도 인덱스 값은 출력에 포함 되지 않습니다.

   **결과**

   |ResultValue|
   |------|
   |0.5|
   |2|

## <a name="output-values-into-dataframe"></a>데이터를 데이터 프레임에 출력 합니다.

이제 두 가지 일련의 수학 결과에서 데이터 프레임으로 특정 값을 출력 합니다. 첫 번째에는 Python에 의해 생성 된 순차 값의 인덱스가 있습니다. 두 번째는 임의의 문자열 값 인덱스를 사용 합니다.

1. 다음 예에서는 정수 인덱스를 사용 하 여 계열에서 값을 가져옵니다.

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

   자동 생성 된 인덱스는 0에서 시작 합니다. 범위를 벗어난 인덱스 값을 사용 하 여 결과를 확인 하세요.

1. 이제 문자열 인덱스를 사용 하 여 다른 데이터 프레임에서 단일 값을 가져옵니다.

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

   숫자 인덱스를 사용 하 여이 계열에서 값을 가져오는 경우 오류가 발생 합니다.

## <a name="next-steps"></a>다음 단계

SQL Server에서 고급 Python 함수를 작성 하는 방법을 알아보려면 다음 빠른 시작을 따르세요.

> [!div class="nextstepaction"]
> [SQL Server Machine Learning Services를 사용 하 여 고급 Python 함수 작성](quickstart-python-functions.md)

SQL Server Machine Learning Services에서 Python을 사용 하는 방법에 대 한 자세한 내용은 다음 문서를 참조 하세요.

- [Python에서 예측 모델 만들기 및 점수 매기기](quickstart-python-train-score-model.md)
- [SQL Server Machine Learning Services (Python 및 R)는 무엇 인가요?](../what-is-sql-server-machine-learning.md)
