---
title: SQL Server에서 T-SQL을 사용 하 여 Python 실행 | Microsoft Docs
description: Python 통합이 사용 되는 SQL Server 데이터베이스 엔진 인스턴스에서 T-SQL 및 저장된 프로시저를 사용 하 여 Python 코드를 실행 하는 것에 대 한 기본 사항을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 59897cbe6abc13b9842dc148ef8c2de4413926d0
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51702961"
---
# <a name="run-python-using-t-sql"></a>T-SQL을 사용하여 Python 실행
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 SQL Server 2017에서 Python 코드를 실행 하는 방법을 설명 합니다. SQL Server 및 Python 간 데이터 이동의 기본 사항을 안내 합니다: 요구 사항, 데이터 구조, 입력 및 출력 합니다. 저장된 프로시저에서 잘 구성 된 Python 코드를 래핑하는 방법도 설명 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 을 빌드, 학습 및 SQL Server에서 기계 학습 모델을 사용 합니다.

## <a name="prerequisites"></a>필수 구성 요소

이 연습에서 예제 코드를 실행 하려면 먼저 SQL Server 2017을 설치 하 고에 설명 된 대로 인스턴스에서 Machine Learning 서비스를 사용 하도록 설정 [설치 SQL Server 2017 Machine Learning Services (In-database)](../install/sql-machine-learning-services-windows-install.md)합니다. 

또한 설치 해야 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)합니다. 또는 서버 및 데이터베이스에 연결 하는 T-SQL 쿼리 또는 저장된 프로시저를 실행 하기만 다른 데이터베이스 관리 또는 쿼리 도구를 사용할 수 있습니다.

환경 준비 되 면 저장된 프로시저의 컨텍스트에서 Python 코드를 실행 하는 방법을 알아보려면이 페이지를 반환 합니다. 

## <a name="verify-python-exists"></a>Python 있는지 확인

다음 단계는 Python 사용 하도록 설정 하는 SQL Server 실행 패드 서비스가 실행 중인지 확인 합니다.

1. Python 통합 데이터베이스 엔진 인스턴스에 설치 되어 있는지 확인 합니다. 찾아야 **python.exe** 라는 폴더에 **PYTHON_SERVICES** C:\Program Files\Microsoft SQL Server\MSSQL14에서. MSSQLSERVER\. SQL Server Python 코드를 실행 하는 데 사용 하는 Python 실행 파일입니다.

2. 외부 스크립트 사용 되는지 여부를 확인 합니다. Management studio에서 다음 문을 실행 합니다.

    ```sql
    sp_configure 'external scripts enabled'
    ```

    하는 경우 **run_value** 는 1, machine learning 기능을 설치 및 사용 준비 합니다.

    오류의 일반적인 원인은 합니다 [SQL Server 실행 패드 서비스](../concepts/extensibility-framework.md#launchpad), 중지 되었습니다. SQL Server 및 Python 간 통신을 관리 하는 합니다. Windows를 사용 하 여 실행 패드 상태를 볼 수 있습니다 **Services** 패널 또는 SQL Server 구성 관리자를 열면 됩니다. 서비스가 중지 된 경우 다시 시작 합니다.

3. Python 런타임에서 작업 하 고 SQL Server와의 통신을 확인 합니다. 이렇게 하려면 새 열 **쿼리** SQL Server Management studio에서 창에 Python 설치 된 인스턴스에 연결 합니다.

    ```sql
    EXEC sp_execute_external_script @language = N'Python', 
    @script = N'print(3+4)'
    ```

    모든 작업이 제대로이 이와 같은 결과 메시지가 표시 됩니다.

    ```text
    STDOUT message(s) from external script: 
    7
    ```

3. 오류가 발생 하는 경우 서버 및 Python 통신할 수 있도록 할 수 있는 작업의 다양 한 사항이 있습니다. 

    Windows 사용자 그룹을 추가 해야 `SQLRUserGroup` 실행 패드에 Python 및 SQL Server 간의 통신을 제공할 수 있는지 확인 하는 인스턴스 로그인으로 합니다. (동일한 그룹에는 모두 R 및 Python 코드 실행 합니다.) 자세한 내용은 [암시적된 인증 사용](../security/add-sqlrusergroup-to-database.md)합니다.
    
    또한 비활성화 된 네트워크 프로토콜을 사용 하도록 설정 하거나 SQL Server는 외부 클라이언트와 통신할 수 있도록 방화벽을 열기 해야 합니다. 자세한 내용은 [설치 문제 해결](../common-issues-external-script-execution.md)합니다.

### <a name="call-revoscalepy-functions"></a>Revoscalepy 함수를 호출 합니다.

확인 하려면 **revoscalepy** 수를 포함 하는 스크립트 실행 [rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) 통계 요약 데이터를 생성 하는 합니다. 이 스크립트 revoscalepy에 포함 된 기본 제공 샘플에서 샘플.xdf 데이터 파일을 검색 하는 방법에 설명 합니다. RxOptions 함수를 제공 합니다 **sampleDataDir** 샘플 파일의 위치를 반환 하는 매개 변수입니다.

Rx_summary 형식의 개체를 반환 하므로 `class revoscalepy.functions.RxSummary.RxSummaryResults`여러 요소를 포함 하는, pandas를 사용 하 여 바로 테이블 형식으로 데이터 프레임을 추출 합니다.

```SQL
EXEC sp_execute_external_script @language = N'Python', 
@script = N'
import os
from pandas import DataFrame
from revoscalepy import rx_summary
from revoscalepy import RxXdfData
from revoscalepy import RxOptions

sample_data_path = RxOptions.get_option("sampleDataDir")
print(sample_data_path)

ds = RxXdfData(os.path.join(sample_data_path, "AirlineDemoSmall.xdf"))
summary = rx_summary("ArrDelay + DayOfWeek", ds)
print(summary)
dfsummary = summary.summary_data_frame
OutputDataSet = dfsummary
'
WITH RESULT SETS  ((ColName nvarchar(25) , ColMean float, ColStdDev  float, ColMin  float,   ColMax  float, Col_ValidObs  float, Col_MissingObs int))
```

## <a name="basic-python-interaction"></a>기본 Python 상호 작용

두 가지 방법으로 SQL Server에서 Python 코드를 실행할 수 있습니다.

+ 시스템 저장 프로시저의 인수로 서 Python 스크립트를 추가 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)합니다.

+ [원격 Python 클라이언트](../python/setup-python-client-tools-sql.md)SQL Server에 연결한 후 SQL Server 계산 컨텍스트로 사용 하 여 코드를 실행 합니다. 그러려면 [revoscalepy](../python/what-is-revoscalepy.md)합니다.

다음 연습에서는 첫 번째 상호 작용 모델에 포커스가: 저장된 프로시저에 Python 코드를 전달 하는 방법입니다.

1. 데이터는 SQL Server와 Python 간에 앞뒤로 전달 하는 방법을 확인 하려면 몇 가지 간단한 코드를 실행 합니다.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    d = a*b
    print(c, d)
    '
    ```

2. 올바르게 설정 완벽 하 게 하 고 서로 Python 및 SQL Server와 통신 하는 경우 올바른 결과 계산 하 고 Python `print` 함수 결과 반환 합니다 **메시지** windows.

    **결과**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```
    
    가져오는 동안 **stdout** 메시지 코드를 테스트할 때 유용 합니다 더 자주 해야 응용 프로그램에서 사용 하거나 테이블에 쓸 수 있도록 테이블 형식으로 결과 반환 합니다. 

이제 이러한 규칙에 유의 하십시오.

+ 내의 모든 항목을 `@script` 인수는 유효한 Python 코드 여야 합니다. 
+ 코드는 들여쓰기, 변수 이름 등 관련 된 모든 Python 규칙을 따라야 합니다. 오류가 발생 하는 경우 공백 및 대/소문자를 확인 합니다.
+ 기본적으로 로드 되지 않은 모든 라이브러리를 사용 하는 경우 로드 하는 데 스크립트의 시작 부분에 import 문을 사용 해야 합니다. SQL Server는 여러 제품 관련 라이브러리를 추가합니다. 자세한 내용은 [Python 라이브러리](../python/python-libraries-and-data-types.md)합니다.
+ 라이브러리에 이미 설치 되어 있지 않으면를 중지 하 고 여기에 설명 된 대로 SQL Server 외부 Python 패키지 설치: [SQL Server에 새로운 Python 패키지 설치](../python/install-additional-python-packages-on-sql-server.md)

## <a name="inputs-and-outputs"></a>입/출력

기본적으로 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 형식의 유효한 SQL 쿼리를 제공 하는 일반적으로 단일 입력된 dataset을 수락 합니다. 

다른 유형의 입력 SQL 변수로 전달할 수 있습니다: 예를 들어, 전달할 수 있습니다 학습된 된 모델을 변수로 같은 serialization 함수를 사용 하 여 [pickle](https://docs.python.org/3.0/library/pickle.html) 또는 [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) 에서 모델을 작성 하는 이진 형식입니다.

저장된 프로시저가 반환 단일 Python [pandas](https://pandas.pydata.org/pandas-docs/stable/index.html) 데이터 프레임 출력으로 하지만 스칼라 및 변수로 모델을 출력할 수도 있습니다. 예를 들어 이진 변수 학습된 된 모델 출력 하 고 테이블에 해당 모델을 작성 하는 T-SQL INSERT 문을 전달할 수 있습니다. 이진 형식의 그림 또는 스칼라를 생성할 수도 있습니다 (날짜 및 시간을 같은 개별 값을 시간 경과 됨 모델을 학습 등).

지금은 살펴보겠습니다 기본값 sp_execute_external_script의 입력 및 출력 변수: `InputDataSet` 고 `OutputDataSet`입니다. 

1. 몇 가지 계산을 수행 하 고 결과 출력에 다음 코드를 실행 합니다.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    print(c)
    OutputDataSet = c
    '
    WITH RESULT SETS ((ResultValue float))
    ```

2. Python 코드는 스칼라를 데이터 프레임을 생성 하기 때문에 오류를 가져와야 합니다.

    **결과**

    ```text
    line 43, in transform
        raise TypeError('OutputDataSet should be of type pandas.DataFrame')
    ```

3. 지금 확인해 전달 하는 경우 테이블 형식 데이터 집합에서 python, 기본 입력된 변수를 사용 하 여 `InputDataSet`입니다. 

    ```sql
    EXECUTE sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    OutputDataSet = InputDataSet
    ',
    @input_data_1 = N'SELECT 1 as Col1'
    ```

    저장된 프로시저 추가 Python 코드에서 아무 작업도 수행 하지 않아도 자동으로 data.frame을 반환 합니다.

    **결과**

    | columnname 없음|
    |------|
    | 1|

    기본적으로 단일 테이블 형식 입력된 데이터 집합 이름이 `InputDataSet`합니다. 그러나 다음과 같은 줄을 추가 하 여 해당 이름을 변경할 수 있습니다: `@input_data_1_name = N'myResultName'`합니다.

    Python에서 사용 하는 열 이름은 출력에 유지 되지 됩니다. 입력된 쿼리 열 이름을 지정 하는 있지만 `Col1`이름이 반환 되지 않으면, 또는 Python 스크립트에서 사용 된 모든 열 머리글을 것입니다. SQL Server로 데이터를 반환 하는 경우 열 이름과 데이터 형식을 지정 하려면 T-SQL을 사용 하 여 `WITH RESULT SETS` 절.

4. 이 예제에서는 입력 및 출력 변수에 대 한 새 이름을 제공 합니다.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    MyOutput = MyInput
    ',
    @input_data_1_name = N'MyInput',
    @input_data_1 = N'SELECT 1 as Col1',
    @output_data_1_name = N'MyOutput'
    WITH RESULT SETS ((ResultValue int))
    ```

    결과 집합 사용 하 여 절을 data.frame를 사용 하 여 Python 열 이름이 반환 되지 되므로 출력에 대 한 스키마를 정의 합니다.

    **결과**

    | ResultValue|
    |------|
    | 1|

5. 이제 일반적인 Python 오류에 살펴보겠습니다. 이전 예제에서 줄을 변경 `@input_data_1_name = N'MyInput'` 에 `@input_data_1_name = N'myinput'`입니다.

    Python 오류는 SQL Server에서 사용 하는 위성 서비스에 의해 메시지로 전달 됩니다. 메시지 긴 수 있고 SQL Server 오류 또는 실행 패드 오류 Python 오류 외에도 포함 하므로 기다려주십시오 키를 눌러 텍스트를 통해 관련 합니다. 주요 메시지는이 줄에서:

    ```text
    MyOutput = MyInput
    NameError: name 'MyInput' is not defined
    ```

    Python, R과 같은 대/소문자 구분 임을 기억 하십시오. 따라서 모든 종류의 오류를 가져올 때 해야 변수 이름, 확인 및 간격, 들여쓰기 및 데이터 형식을 사용 하 여 문제를 확인 합니다.

## <a name="python-data-structures"></a>Python 데이터 구조

SQL Server Python 의존 **pandas** 패키지는 테이블 형식 데이터로 작업 하는 데 매우 유용 합니다. 그러나는 Python에서 SQL Server 스칼라 전달할 수 없으며 "작업만" 것으로 예상 되 이미 살펴봤습니다 보십시오. 이 섹션에서는 Python과 SQL Server 간 테이블 형식 데이터를 전달 하는 경우에서 실행 될 수 있는 추가 문제에 대 한 작업을 준비 하려면 일부 기본 데이터 형식 정의 살펴보겠습니다.

+ 데이터 프레임을 사용 하 여 테이블인 _여러_ 열입니다.
+ 데이터 프레임의 단일 열에는 일련의 호출 목록 같은 개체입니다.
+ 단일 값이 데이터 프레임의 셀을 인덱스로 호출 되어야 합니다.

그렇다면는 노출 하 여 계산을 데이터 프레임으로 단일 결과 data.frame 테이블 형식 구조를 요구 하는 경우? 하나의 대답이 데이터 프레임으로 쉽게 변환 되는 계열으로 단일 스칼라 값을 나타낼 수 합니다. 

1. 이 예제에서는 몇 가지 간단한 수학 않으며 계열로 스칼라를 변환 합니다. 계열 여기에 표시 된 대로 수동으로 또는 프로그래밍 방식으로 할당할 수 있는 인덱스에 필요 합니다.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    print(c)
    s = pandas.Series(c, index =["simple math example 1"])
    print(s)
    '
    ```

2. 계열 data.frame로 변환 되지 않은 메시지 창에 반환 되므로 값 하지만 더 테이블 형식으로 결과 볼 수 있습니다.

    **결과**

    ```text
    STDOUT message(s) from external script: 
    0.5
    simple math example 1    0.5
    dtype: float64
    ```

3. 시리즈의 길이 늘리려면 배열을 사용 하 여 새 값을 추가할 수 있습니다. 

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    d = a*b
    s = pandas.Series([c,d])
    print(s)
    '
    ```

    인덱스를 지정 하지 않으면 인덱스는 0부터 시작 하 고 배열의 길이 사용 하 여 종료 값이 있는 생성 됩니다.

    **결과**

    ```text
    STDOUT message(s) from external script: 
    0    0.5
    1    2.0
    dtype: float64
    ```

4. 수를 늘리면 **인덱스** 값을 새로 추가 하지 않지만 **데이터** 값 시리즈를 채울 데이터 값이 반복 됩니다.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
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

### <a name="convert-series-to-data-frame"></a>시계열 데이터 프레임으로 변환

스칼라 수학 결과 테이블 형식 구조로 변환 하지를 계속 해야 SQL Server에서 처리할 수 있는 형식으로 변환 합니다. 

1. 계열 data.frame로 변환 하려면 호출을 pandas [DataFrame](https://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe) 메서드.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
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
    WITH RESULT SETS (( ResultValue float ))
    ```

2. Data.frame에서 특정 값을 가져오려면 인덱스를 사용 하는 경우에 인덱스 값을 출력 하지는 note 합니다.

    **결과**

    |ResultValue|
    |------|
    |0.5|
    |2|

### <a name="output-values-into-dataframe-using-an-index"></a>인덱스를 사용 하 여 data.frame로 출력 값

간단한 수학 연산의 결과 포함 하는 두 계열이 있는 data.frame로 변환 작동 하는 방법을 살펴보겠습니다. 첫 번째 Python에서 생성 된 순차 값의 인덱스를 갖습니다. 두 번째는 임의의 문자열 값의 인덱스를 사용합니다.

1. 이 예제에서는 정수 인덱스를 사용 하 여 계열에서 값을 가져옵니다.

    ```sql
    EXECUTE sp_execute_external_script 
    @language = N'Python', 
    @script = N'
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
    WITH RESULT SETS (( ResultValue float ))
    ```

    자동으로 생성 된 인덱스는 0부터 시작 하 해야 합니다. 범위 인덱스 값을 사용 하 고 어떻게 되는지 확인 합니다.

2. 이제 문자열 인덱스에 있는 다른 데이터 프레임에서 단일 값을 살펴보겠습니다. 

    ```sql
    EXECUTE sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    import pandas as pd
    a = 1
    b = 2
    c = a/b
    s = pandas.Series(c, index =["simple math example 1", "simple math example 2"])
    print(s)
    df = pd.DataFrame(s, index=["simple math example 1"])
    OutputDataSet = df
    '
    WITH RESULT SETS (( ResultValue float ))
    ```

    **결과**

    |ResultValue|
    |------|
    |0.5|

    이 시리즈에서 값 가져오기 숫자 인덱스를 사용 하려고 하면 오류가 발생 합니다.

이 연습에서는 다른 Python 데이터 구조를 사용 하 고 데이터 프레임으로 올바른 결과 얻을 수 있는지 확인 하는 방법의 아이디어를 제공 하기 위한 것 이었습니다. 해당 출력을 단일 값 데이터 프레임의 분량 보다 더 문제는 결론을 내렸습니다 수 있습니다! 다행 스럽게도 변수로 모든 종류의 저장된 프로시저에서 값을 쉽게 전달할 수 있습니다. 다음 단원에서 다룹니다.

## <a name="tips"></a>팁

+ Python은 가장 유연한 중 프로그래밍 언어 중에서 작은따옴표 및 큰따옴표;와 관련 하 여 해당 정책은 거의 서로 바꿔 사용할 수 있습니다. 

    그러나 T-SQL가 작은따옴표를 사용 하 여 특정 항목에 대 한 및 `@script` 인수 작은따옴표를 사용 하 여 유니코드 문자열로 Python 코드를 묶습니다. 따라서 Python 코드를 검토 하 고 큰따옴표를 작은따옴표로 일부 변경 해야 합니다.

+ 저장된 프로시저를 찾을 수 없습니다 `sp_execute_external_script`? 즉, 아마도 아직 완료 외부 스크립트 실행을 지원 하도록 인스턴스를 구성 합니다. SQL Server 2017 설치 프로그램을 실행 하 고 기계 학습 언어도 Python 선택을 명시적으로 설정 해야 사용 하 여 기능 `sp_configure`, 한 다음 인스턴스를 다시 시작 합니다. 

    자세한 내용은 참조 하세요 [설치 SQL Server 2017 Machine Learning Services (In-database)](../install/sql-machine-learning-services-windows-install.md)합니다.

## <a name="next-steps"></a>다음 단계

[Iris 데모 데이터 집합 설정](demo-data-iris-in-sql.md)