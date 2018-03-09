---
title: "T-SQL을 사용 하 여 Python 실행 | Microsoft Docs"
ms.custom: 
ms.date: 02/28/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2017
dev_langs:
- Python
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 5c6145d3af6918a5f3daa954aae5522ffffebb89
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2018
---
# <a name="run-python-using-t-sql"></a>T-SQL을 사용 하 여 Python 실행
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 자습서에서는 SQL Server 2017에서 Python 코드를 실행 하는 방법을 설명 합니다. SQL Server 및 Python 간에 데이터를 이동 하는 과정을 안내 하 고 저장된 프로시저에서 잘 구성 된 Python 코드를 래핑하는 방법에 설명 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 작성, 학습 및 기계 학습 모델을 사용 하 여 SQL에서 서버입니다.

## <a name="prerequisites"></a>필수 구성 요소

이 자습서를 완료 하려면 먼저 SQL Server 2017 설치 하며에서 설명한 대로 컴퓨터 학습 서비스 인스턴스의 활성화 [이 여기서](../python/setup-python-machine-learning-services.md)합니다. 

또한 설치 해야 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)합니다. 또는 서버 및 데이터베이스를 연결할 수 있고 T-SQL 쿼리 또는 저장된 프로시저를 실행 한다면 다른 데이터베이스 관리 또는 쿼리 도구를 사용할 수 있습니다.

설치를 완료 한 후 저장된 프로시저의 컨텍스트 내에서 Python 코드를 실행 하는 방법에 알아보려면이 자습서로 반환 합니다. 

## <a name="overview"></a>개요

이 자습서는 다음 네 단원에 포함 됩니다.

+ SQL Server 및 Python 간에 데이터를 이동 하는 기본적인: 기본 요구 사항, 데이터 구조, 입력 및 출력에 알아봅니다.
+ 샘플 데이터를 로드 하는 등의 간단한 Python 작업에 대 한 저장된 프로시저를 사용 하는 것이 좋습니다.
+ Python 기계 학습 모델을 만들려면 저장된 프로시저를 사용 하 고 모델에서 점수를 생성 합니다.
+ Python으로 SQL Server를 사용 하 여 원격 클라이언트에서 실행 하려고 하는 경우 사용자에 대 한 선택적는 단원에서 _계산 컨텍스트_합니다. 즉, 모델을 작성 하기 위한 코드를 포함 합니다. 그러나, 익숙한 이미 다소 Python 환경 및 Python 도구를 사용 해야 합니다.

SQL Server 2017 관련 추가 Python 예제는 다음과 같습니다: [SQL Server Python 자습서](../tutorials/sql-server-python-tutorials.md)

## <a name="verify-that-python-is-enabled-and-the-launchpad-is-running"></a>Python 설정 되어 있고 실행 패드에서 실행 되 고 있음을 확인 합니다.

1. Management Studio에서이 문을 실행 하는 서비스를 사용할 수 있는지 확인 합니다.

    ```sql
    sp_configure 'external scripts enabled'
    ```

    경우 **run_value** 1 이면 컴퓨터 학습 기능이 설치 되어 사용할 준비가 되어 있습니다.

    오류의 일반적인 원인은 SQL Server 및 Python 간의 통신을 관리 하는 실행 패드 중지 되었습니다. Windows를 사용 하 여 실행 패드 상태를 볼 수 있습니다 **서비스** 패널, 또는 SQL Server 구성 관리자를 여십시오. 서비스가 중지 된 경우 다시 시작 합니다.

2. 다음으로 Python 런타임의 SQL Server와 통신 한 작동 하는지를 확인 합니다. 이 위해 열고 새 **쿼리** SQL Server Management Studio에서 창 고 Python 설치 된 인스턴스에 연결 합니다.

    ```sql
    EXEC sp_execute_external_script @language = N'Python', 
    @script = N'print(3+4)'
    ```

    작업이 제대로 하는 경우 다음과 같은 결과 메시지가 나타납니다.

    ```text
    STDOUT message(s) from external script: 
    7
    ```

3. 오류가 발생할 경우 서버 및 Python 통신할 수 있는지 확인을 수행할 수 있는 작업의 여러 가지가 있습니다. 

    Windows 사용자 그룹에 추가 해야 `SQLRUserGroup` 실행 패드 Python 및 SQL Server 간의 통신을 제공할 수 있는지 확인 하는 인스턴스 로그인으로 합니다. (동일한 그룹을 모두 R에 대 한 사용 및 Python 코드 실행 합니다.) 자세한 내용은 참조 [Enabled 암시 된 인증이](../r/add-sqlrusergroup-to-database.md)합니다.
    
    또한, 비활성화 된 네트워크 프로토콜 설정 또는 SQL Server 외부 클라이언트와 통신할 수 있도록 방화벽을 열고 할 수 있습니다. 자세한 내용은 참조 [설치 문제 해결](../common-issues-external-script-execution.md)합니다.

## <a name="basic-python-interaction"></a>기본 Python 상호 작용

SQL Server에서 Python 코드를 실행 하는 방법은 두 가지가 있습니다.

+ 시스템 저장 프로시저의 인수로 서 Python 스크립트 추가 **sp_execute_external_script**
+ 원격 Python 클라이언트에서 SQL Server에 연결 하 고 SQL Server를 사용 하 여 계산 컨텍스트로 써 코드를 실행 합니다. 이 위해서는 [revoscalepy](../python/what-is-revoscalepy.md)합니다.

이 자습서의 기본 목표는 저장된 프로시저에서 Python을 사용할 수 있는지 확인 하는 것입니다.

1. 데이터는 SQL Server 및 Python 간에 간에 전달 방식을 확인 하려면 몇 가지 간단한 코드를 실행 합니다.

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

2. 모든 요소 및 Python 및 SQL Server 통신의 대상이 서로 라고 가정할 경우 정확한 결과 계산 필드 및 Python `print` 함수 결과를 반환 된 **메시지** windows 합니다.

    **결과**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```
    
    가져오는 동안 **stdout** 메시지 코드를 테스트할 때 유용를 더 자주 해야 응용 프로그램에서 사용 하거나 테이블에 쓸 수 있도록 테이블 형식으로 결과 반환 합니다. 

이제 이러한 규칙을 고려 하세요.

+ 내의 모든 항목은 `@script` 인수에 유효한 Python 코드 여야 합니다. 
+ 코드는 들여쓰기, 변수 이름 등에 관한 모든 Pythonic 규칙을 따라야 합니다. 오류가 발생 하는 경우 공백 및 대/소문자를 확인 합니다.
+ 기본적으로 로드 되지 않은 모든 라이브러리를 사용 하는 경우 로드 하는 데 스크립트의 시작 부분에 import 문을 사용 해야 합니다. 
+ 라이브러리에 이미 설치 되어 있지 않으면, 중지 및 여기에 설명 된 대로 SQL Server 외부에서 Python 패키지 설치: [SQL Server에 새 Python 패키지 설치](../python/install-additional-python-packages-on-sql-server.md)

## <a name="inputs-and-outputs"></a>입/출력

기본적으로 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 유효한 SQL 쿼리의 형식에 제공 하는 일반적으로 단일 입력된 dataset을 수락 합니다. 다른 유형의 입력 SQL 변수 변수로 전달할 수 있습니다: 예를 들어 전달할 수 있습니다는 학습 된 모델을 변수로 등 serialization 함수를 사용 하 여 [곡](https://docs.python.org/3.0/library/pickle.html) 또는 [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) 에서 모델을 작성 하는 이진 형식입니다.

저장된 프로시저가 반환 단일 Python [팬더](http://pandas.pydata.org/pandas-docs/stable/index.html) 데이터 프레임을 출력 합니다. 그러나 변수로 스칼라 및 모델을 출력할 수 있습니다. 예를 들어 이진 변수로 학습된 된 모델을 출력 한 테이블에 해당 모델을 작성 하는 T-SQL INSERT 문을 전달할 수 있습니다. 스칼라 또는 이진 형식으로 플롯을 생성할 수도 있습니다 (날짜 및 시간 등의 개별 값을 시간 경과 됨 모델을 학습 등).

지금은 살펴보겠습니다 방금 기본 입력 및 출력 변수 `InputDataSet` 및 `OutputDataSet`합니다. 

1. 특정 계산을 수행 하 고 결과 출력 하는 다음 코드를 실행 합니다.

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

2. Python 코드에서는 발생 하는 스칼라 데이터 프레임이 아닌 때문에 오류를 받아야 합니다.

        **Results**

        ```text
        line 43, in transform
            raise TypeError('OutputDataSet should be of type pandas.DataFrame')
        ```

3. 이제 전달 되는 테이블 형식 데이터 집합 Python, 기본 입력된 변수를 사용 하 여 수행 되는 작업을 볼 `InputDataSet`합니다. 

    ```sql
    EXECUTE sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    OutputDataSet = InputDataSet
    ',
    @input_data_1 = N'SELECT 1 as Col1'
    ```

    저장된 프로시저는 data.frame를 모든 Python 코드의 추가 작업을 수행할 필요 없이 자동으로 반환 합니다.

    **결과**

    | 열 이름 없음|
    |------|
    | 1.|

    기본적으로 단일 테이블 형식 입력된 데이터 집합에는 이름이 `InputDataSet`합니다. 다음과 같은 줄을 추가 하 여 해당 이름을 변경할 수 있습니다: `@input_data_1_name = N'myResultName'`합니다.

    Python에서 사용 하는 열 이름은 출력에 보존 되지 않습니다. 입력된 쿼리 열 이름 지정 있지만 `Col1`이름이 반환 되지 않으면, 또는 Python 스크립트에서 사용 하는 모든 열 머리글을 것입니다. SQL Server로 데이터를 반환할 때 열 이름과 데이터 형식을 지정 하는 T-SQL을 사용 하 여 `WITH RESULT SETS` 절.

4. 이 예에서는 입력 및 출력 변수에 대 한 새 이름을 제공합니다.

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

    결과 집합으로 절은 data.frame와 Python 열 이름은 반환 되지 이후 출력에 대 한 스키마를 정의 합니다.

    **결과**

    | ResultValue|
    |------|
    | 1.|

5. 이제 일반적인 Python 오류에 살펴보겠습니다. 이전 예제에서 줄을 변경 `@input_data_1_name = N'MyInput'` 를 `@input_data_1_name = N'myinput'`합니다.

    Python 오류는 SQL Server에서 사용 하는 위성 서비스에 의해 메시지로 있습니다에 전달 됩니다. 메시지 긴 수 있고 SQL Server 오류 또는 Python 오류 뿐 아니라 실행 패드 오류가 포함 관련 정보를 텍스트를 가로질러 환자를 기울여야 합니다. 키 메시지를이 줄에서 되었습니다.

    ```text
    MyOutput = MyInput
    NameError: name 'MyInput' is not defined
    ```

    같은 R, Python, 대/소문자 구분 임을 기억 하십시오. 따라서 모든 종류의 오류를 얻으면 수 변수 이름, 확인 하 고 문제 간격, 들여쓰기 및 데이터 형식에 대 한 확인 해야 합니다.

## <a name="python-data-structures"></a>Python 데이터 구조

SQL Server에서 Python 사용 **팬더** 테이블 형식 데이터로 작업 하기 위한 훌륭한입니다. 그러나 이미 본 Python에서 SQL Server에는 스칼라를 전달할 수 없습니다 및 "작동"입니다. 이 섹션에서는 몇 가지 기본 데이터 형식 정의 Python 및 SQL Server 간에 표 형식 데이터를 전달할 때 간에 실행 될 수 있는 추가 문제에 대비를 검토 합니다.

+ 데이터 프레임에 있는 테이블은 _여러_ 열입니다.
+ 데이터 프레임으로 이루어진 단일 열에는 일련의 호출 목록 형식 개체입니다.
+ 단일 값을 데이터 프레임의 셀 이며 인덱스에서 호출할 수 있습니다.

어떻게가 노출 하 여 계산을 데이터 프레임으로 단일 결과 data.frame 테이블 형식 구조를 요구 하는 경우? 다음 중 하나 데이터 프레임으로 쉽게 변환 되는 계열로 단일 스칼라 값을 나타내는 것입니다. 

1. 이 예제는 간단한 몇 가지 계산 하 고 계열로 스칼라를 변환 합니다. 계열에는 여기에 표시 된 대로 수동으로 또는 프로그래밍 방식으로 할당할 수 있는 인덱스를 필요 합니다.

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

2. 되풀이 되지 않은 한 data.frame로 변환 되 때문에 메시지 창에 값이 반환 됩니다 하지만 결과가 더 표 형식으로 볼 수 있습니다.

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

    인덱스를 지정 하지 않으면 인덱스는 0부터 배열 길이 값을 가진 생성 됩니다.

    **결과**

    ```text
    STDOUT message(s) from external script: 
    0    0.5
    1    2.0
    dtype: float64
    ```

4. 값을 늘리면 **인덱스** 값, 새 추가 하지 않지만 **데이터** 값을 데이터 값 계열을 채우려면 반복 되는 합니다.

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

### <a name="convert-series-to-data-frame"></a>계열 데이터 프레임으로 변환 합니다.

하지 수학 스칼라 결과 테이블 형식 구조로 변환, 여전히 해야 SQL Server에서 처리할 수 있는 형식으로 변환 합니다. 

1. 호출 하면 팬더 일련은 data.frame 변환할 [데이터 프레임](http://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe) 메서드.

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

2. Note는 data.frame에서 특정 값을 가져올 인덱스를 사용 하는 경우에 인덱스 값이 출력 되지 해당 합니다.

    **결과**

    |ResultValue|
    |------|
    |0.5|
    |2|

### <a name="output-values-into-dataframe-using-an-index"></a>인덱스를 사용 하 여 data.frame에 출력 값

간단한 수치 연산의 결과 포함 하는 두 개의 계열과 data.frame 변환이 작동 하는 방법을 살펴보겠습니다. 첫 번째는 Python에 의해 생성 된 순차 값의 인덱스입니다. 두 번째는 임의의 문자열 값의 인덱스를 사용합니다.

1. 이 예제에서는 정수 인덱스를 사용 하는 계열에서 값을 가져옵니다.

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

    자동 생성 된 인덱스는 0에서 시작을 기억 합니다. 인덱스 값 범위를 벗어난을 사용 하 여 시도 하 고 섹션을 참조 합니다.

2. 이제 단일 값 문자열 인덱스를 가진 다른 데이터 프레임에서 살펴보겠습니다. 

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

    이 시리즈의 값을 가져오는 숫자 인덱스를 사용 하려고 하면 오류가 발생 합니다.

이 연습 시킬 알 수 있습니다 다른 Python 데이터 구조를 사용 하 고 데이터 프레임으로 올바른 결과 얻을 수 있는지 확인 하는 방법의 수입니다. 해당 출력 하는 중 하나의 값을 데이터 프레임은 해당 값 보다 더 문제 완료 될 수 있습니다! 다행히 변수로 모든 종류의 저장된 프로시저 내부 및 외부 값을 쉽게 전달할 수 있습니다. 다음 단원에서 다룹니다.

## <a name="tips"></a>팁

+ Python은 가장 유연한 중 프로그래밍 언어 중 작은따옴표 및 큰따옴표; 관련 하 여 하기가 거의 동일 합니다. 

    그러나 T-SQL가 작은따옴표를 사용 하 여 특정 작업을 위해 및 `@script` 인수를 유니코드 문자열로 Python 코드를 포함 하려면 작은따옴표를 사용 합니다. 따라서 Python 코드를 검토 하 고 큰따옴표를 작은따옴표로 일부 변경 해야 합니다.

+ 저장된 프로시저를 찾을 수 없습니다 `sp_execute_external_script`? 아마도 완료 하지 않았습니다 외부 스크립트 실행을 지원 하도록 인스턴스를 구성 하는 것이 것입니다. SQL Server 2017 설치 프로그램을 실행 하 기계 학습 언어도 Python을 선택한 후 명시적으로 설정 해야 사용 하 여 기능 `sp_configure`, 한 다음 인스턴스를 다시 시작 합니다. 

    자세한 내용은 참조 [python 설치 컴퓨터 학습 서비스](../python/setup-python-machine-learning-services.md)합니다.

## <a name="next-steps"></a>다음 단계

[SQL 저장 프로시저에서 Python 코드를 래핑하십시오.](wrap-python-in-tsql-stored-procedure.md)