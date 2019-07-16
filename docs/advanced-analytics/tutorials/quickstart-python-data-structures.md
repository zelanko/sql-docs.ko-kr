---
title: Python – SQL Server Machine Learning에서에서 데이터 구조를 사용 하 여 작업에 대 한 빠른 시작
description: 이 빠른 시작에서는 SQL Server에서 Python 스크립트에 알아봅니다에 대 한는 데이터 구조를 어떻게 sp_execute_external_script 시스템 저장 프로시저를 사용 하 여 사용 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: ffbbd39c08221db4afa6427626ca618e04617166
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962084"
---
# <a name="quickstart-python-data-structures-in-sql-server"></a>빠른 시작: SQL Server의 Python 데이터 구조
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 빠른 시작이에서는 Python을 사용 하 여 SQL Server Machine Learning Services의 경우 데이터 구조를 사용 하는 방법을 보여 줍니다.

SQL Server Python 의존 **pandas** 패키지는 테이블 형식 데이터로 작업 하는 데 매우 유용 합니다. 그러나 Python에서 SQL Server 스칼라 전달할 수 없으며 "작업만" 예상. 이 빠른 시작에서는 Python과 SQL Server 간 테이블 형식 데이터를 전달 하는 경우에서 실행 될 수 있는 추가 문제에 대 한 작업을 준비 하려면 일부 기본 데이터 형식 정의 살펴보겠습니다.

+ 데이터 프레임을 사용 하 여 테이블인 _여러_ 열입니다.
+ 데이터 프레임의 단일 열에는 일련의 호출 목록 같은 개체입니다.
+ 단일 값이 데이터 프레임의 셀을 인덱스로 호출 되어야 합니다.

어떻게는 노출 하 여 계산을 데이터 프레임으로 단일 결과 data.frame 테이블 형식 구조를 요구 하는 경우? 하나의 대답이 데이터 프레임으로 쉽게 변환 되는 계열으로 단일 스칼라 값을 나타낼 수 합니다. 

## <a name="prerequisites"></a>사전 요구 사항

이전 빠른 시작에서는 [SQL Server에 있는지 확인 하는 Python](quickstart-python-verify.md), 정보를 제공 하 고이 빠른 시작에 필요한 Python 환경을 설정 하는 것에 대 한 링크입니다.

## <a name="scalar-value-as-a-series"></a>일련의 스칼라 값

이 예제에서는 몇 가지 간단한 수학 않으며 계열로 스칼라를 변환 합니다.

1. 계열 여기에 표시 된 대로 수동으로 또는 프로그래밍 방식으로 할당할 수 있는 인덱스에 필요 합니다.

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

## <a name="convert-series-to-data-frame"></a>시계열 데이터 프레임으로 변환

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

2. 결과 다음과 같습니다. Data.frame에서 특정 값을 가져오려면 인덱스를 사용 하는 경우에 인덱스 값에는 출력의 일부가 아닙니다.

    **결과**

    |ResultValue|
    |------|
    |0.5|
    |2|

## <a name="output-values-into-dataframe"></a>Data.frame에 출력 값

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

## <a name="next-steps"></a>다음 단계

다음으로, SQL Server에서 Python을 사용 하 여 예측 모델을 빌드합니다.

> [!div class="nextstepaction"]
> [만들기, 학습 및 Python 모델을 사용 하 여 SQL Server에서 저장된 프로시저를 사용 하 여](quickstart-python-train-score-in-tsql.md)