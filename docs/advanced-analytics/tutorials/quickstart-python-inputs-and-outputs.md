---
title: Python – SQL Server Machine Learning에서에서 입력 및 출력을 사용 하 여 작업에 대 한 빠른 시작
description: SQL Server의 Python 스크립트에 대 한이 빠른 시작에서는 입력 및 출력 sp_execute_external_script 시스템 저장 프로시저를 구성 하는 방법에 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: a778c4a65b9e3f4cbf4ed77cff46e9061d4b6a8a
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/15/2019
ms.locfileid: "59583226"
---
# <a name="quickstart-handle-inputs-and-outputs-using-python-in-sql-server"></a>빠른 시작: 입력 및 SQL Server에서 Python을 사용 하 여 출력 처리
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 빠른 시작이에서는 입력을 처리 하는 방법을 보여 줍니다 하 고 SQL Server Machine Learning Services에서 Python을 사용 하는 경우를 출력 합니다.

기본적으로 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 형식의 유효한 SQL 쿼리를 제공 하는 일반적으로 단일 입력된 dataset을 수락 합니다.

다른 유형의 입력 SQL 변수로 전달할 수 있습니다: 예를 들어, 전달할 수 있습니다 학습된 된 모델을 변수로 같은 serialization 함수를 사용 하 여 [pickle](https://docs.python.org/3.0/library/pickle.html) 또는 [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) 에서 모델을 작성 하는 이진 형식입니다.

저장된 프로시저가 반환 단일 Python [pandas](https://pandas.pydata.org/pandas-docs/stable/index.html) 데이터 프레임 출력으로 하지만 스칼라 및 변수로 모델을 출력할 수도 있습니다. 예를 들어 이진 변수 학습된 된 모델 출력 하 고 테이블에 해당 모델을 작성 하는 T-SQL INSERT 문을 전달할 수 있습니다. 이진 형식의 그림 또는 스칼라를 생성할 수도 있습니다 (날짜 및 시간을 같은 개별 값을 시간 경과 됨 모델을 학습 등).

## <a name="prerequisites"></a>사전 요구 사항

이전 빠른 시작에서는 [SQL Server에 있는지 확인 하는 Python](quickstart-python-verify.md), 정보를 제공 하 고이 빠른 시작에 필요한 Python 환경을 설정 하는 것에 대 한 링크입니다.

## <a name="create-the-source-data"></a>원본 데이터 만들기

다음 T-SQL 문을 실행 하 여 테스트 데이터의 작은 테이블을 만듭니다.

```sql
CREATE TABLE PythonTestData (col1 INT NOT NULL)
INSERT INTO PythonTestData VALUES (1);
INSERT INTO PythonTestData VALUES (10);
INSERT INTO PythonTestData VALUES (100);
GO
```

테이블을 만들었으면 다음 문을 사용하여 테이블을 쿼리합니다.
  
```sql
SELECT * FROM PythonTestData
```

**결과**

![PythonTestData 테이블의 내용](./media/select-pythontestdata.png)

## <a name="inputs-and-outputs"></a>입/출력

기본값에 살펴보겠습니다 sp_execute_external_script의 입력 및 출력 변수: `InputDataSet` 고 `OutputDataSet`입니다.

1. R 스크립트에 대 한 입력으로 테이블에서 데이터를 가져올 수 있습니다. 다음 문을 실행 합니다. 테이블에서 데이터를 가져오고, R 런타임을 통해 왕복 하며 열 이름의 값을 반환 합니다 *NewColName*합니다.

    쿼리에서 반환 되는 데이터를 데이터 프레임으로 SQL Database로 데이터를 반환 하는 R 런타임에 전달 됩니다. WITH RESULT SETS 절을 SQL Database에 대 한 반환된 된 데이터 테이블의 스키마를 정의 합니다.

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'Python'
        , @script = N'OutputDataSet = InputDataSet;'
        , @input_data_1 = N'SELECT * FROM PythonTestData;'
    WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    **결과**

    ![테이블에서 데이터를 반환 하는 Python 스크립트의 출력](./media/python-output-pythontestdata.png)

2. 입력 또는 출력 변수의 이름을 변경해 보겠습니다. 위의 스크립트 사용 기본 입력 및 출력 변수 이름 _InputDataSet_ 하 고 _OutputDataSet_합니다. 연결 된 입력된 데이터를 정의 하 _InputDatSet_를 사용 합니다 *@input_data_1* 변수.

    이 스크립트를 저장된 프로시저의 출력 및 입력된 변수 이름이 변경 되었습니다 *SQL_out* 하 고 *SQL_in*:

    ```sql
    EXECUTE sp_execute_external_script
      @language = N'Python'
      , @script = N'SQL_out = SQL_in'
      , @input_data_1 = N' SELECT 12 as Col;'
      , @input_data_1_name  = N'SQL_in'
      , @output_data_1_name =  N'SQL_out'
      WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    입력 및 출력 변수를 대/소문자 `@input_data_1_name` 하 고 `@output_data_1_name` 에서 Python 코드에서 소문자가 일치 해야 `@script`Python는 대/소문자 구분.

    하나의 입력 데이터 세트만 매개 변수로 전달할 수 있으며 하나의 데이터 세트만 반환할 수 있습니다. 그러나 Python 코드 내에서 다른 데이터 집합을 호출할 수 있으며 데이터 집합 외에 다른 유형의 출력을 반환할 수 있습니다. 또한 모든 매개 변수에 OUTPUT 키워드를 추가하여 결과와 함께 매개 변수를 반환할 수도 있습니다. 

    `WITH RESULT SETS` 문은 SQL Server에서 사용 되는 데이터에 대 한 스키마를 정의 합니다. Python에서 반환 하는 각 열에 대 한 SQL 호환 데이터 형식을 제공 해야 합니다. 스키마 정의 사용 하 여 새 열 이름을 너무 Python data.frame의 열 이름을 사용할 필요가 없습니다.

3. Python 스크립트를 사용 하 여 값을 생성 하 고 수도의 입력된 쿼리 문자열 _@input_data_1_ 비어 있습니다.

    ```sql
    EXECUTE sp_execute_external_script
    @language = N'Python'
    , @script = N'
    import pandas as pd
    mytextvariable = pandas.Series(["hello", " ", "world"]);
    OutputDataSet = pd.DataFrame(mytextvariable);'
    , @input_data_1 = N''
    WITH RESULT SETS (([Col1] CHAR(20) NOT NULL));
    ```

    **결과**

    ![쿼리 결과 사용 하 여 @script 입력으로](./media/python-data-generated-output.png)

## <a name="next-steps"></a>다음 단계

Python과 SQL Server 간 테이블 형식 데이터를 전달할 때 발생할 수 있는 문제 중 일부를 검사 합니다.

> [!div class="nextstepaction"]
> [빠른 시작: SQL Server의 Python 데이터 구조](quickstart-python-data-structures.md)