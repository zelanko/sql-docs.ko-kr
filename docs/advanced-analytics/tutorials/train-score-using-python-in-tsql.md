---
title: 학습 및 점수 매기기에 대 한 SQL에서 사용 하 여 Python 모델 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b7f5883356ff6878f869ee10f915bcb93a2dba17
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="use-python-model-in-sql-for-training-and-scoring"></a>SQL에서 Python 모델을 학습 및 점수 매기기에 사용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

에 [이전 단원](wrap-python-in-tsql-stored-procedure.md), Python SQL과 함께 사용 하기 위한 일반적인 패턴을 학습 합니다. 프로그램 Python 코드를 한 명확 하 게 정의 data.frame 출력 하 고 필요에 따라 수 해야 스칼라 또는 이진에 대 한 여러 변수를 출력 하도록 배웠습니다. 지금까지 학습 Python에 올바른 형식의 데이터를 전달 하 고 결과 처리 하는 SQL 저장 프로시저를 디자인 해야 합니다.

이 섹션에서는 이와 같은 패턴을 사용 하 여 SQL Server를 추가 했으므로 데이터에 모델을 학습 하 고 SQL Server 테이블에는 모델 저장:

+ Python 기계 학습 함수를 호출 하는 저장된 프로시저를 디자인 합니다.
+ 저장된 프로시저는 모델 학습에 사용 하도록 SQL Server에서 데이터를 해야 합니다.
+ 저장된 프로시저를 이진 변수로 학습된 된 모델을 출력합니다. 
+ 변수는 모델 테이블에 삽입 하 여 학습 된 모델을 저장 합니다. 

## <a name="create-the-stored-procedure-and-train-a-python-model"></a>저장된 프로시저를 만들고 Python 모델 학습

1. 모델을 작성 하는 저장된 프로시저를 만드는 SQL Server Management Studio에서 다음 코드를 실행 합니다.

    ```sql
    CREATE PROCEDURE generate_iris_model (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script @language = N'Python',
    @script = N'
    import pickle
    from sklearn.naive_bayes import GaussianNB
    GNB = GaussianNB()
    trained_model = pickle.dumps(GNB.fit(iris_data[[0,1,2,3]], iris_data[[4]]))
    '
    , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "SpeciesId" from iris_data'
    , @input_data_1_name = N'iris_data'
    , @params = N'@trained_model varbinary(max) OUTPUT'
    , @trained_model = @trained_model OUTPUT;
    END;
    GO
    ```

2. 이 명령이 오류 없이 실행 되는 경우 새 저장된 프로시저를 만들고 데이터베이스에 추가 합니다. Management Studio에서 저장된 프로시저를 찾을 수 있습니다 **개체 탐색기**아래 **프로그래밍**합니다.

3. 이제 저장된 프로시저를 실행 합니다.

    ```sql
    EXEC generate_iris_model
    ```

    저장된 프로시저의 입력 요구를 제공 하지 않은 오류를 받아야 합니다.

    "프로시저 또는 함수 'generate_iris_model' 매개 변수를 필요 '@trained_model', 제공 되지 않았습니다."

4. 필요한 입력을 지 원하는 모델을 생성 하 고 테이블에 저장 하려면 일부 추가 문이 필요 합니다.

    ```sql
    DECLARE @model varbinary(max);
    EXEC generate_iris_model @model OUTPUT;
    INSERT INTO iris_models (model_name, model) values('Naive Bayes', @model);
    ```

5. 이제 모델 생성 코드를 한 번 더 실행 해 보십시오. 

    이 오류를 받아야 하며: "PRIMARY KEY 제약 조건 위반 중복 키 'dbo.iris_models' 개체에 삽입할 수 없습니다. 중복 키 값 (Naive Bayes)은 ".

    INSERT 문의 일부로 "Naive Bayes"에 수동으로 입력 하 여 모델 이름이 제공 때문입니다. 각 실행에 다른 매개 변수 또는 서로 다른 알고리즘을 사용 하 여를 다양 한 모델을 만들 계획인 경우 고려해 야 메타 데이터 스키마를 설정 모델을 자동으로 이름을 지정할 수 있습니다 및 더에 쉽게 식별할 수 있도록 합니다.

6. 이 오류를 해결 하려면 SQL 래퍼에 몇 가지 약간의 수정 가능 합니다. 이 예제에서는 현재 날짜 및 시간을 추가 하 여 고유한 모델 이름을 생성 됩니다.

    ```sql
    DECLARE @model varbinary(max);
    DECLARE @new_model_name varchar(50)
    SET @new_model_name = 'Naive Bayes ' + CAST(GETDATE()as varchar)
    SELECT @new_model_name 
    EXEC generate_iris_model @model OUTPUT;
    INSERT INTO iris_models (model_name, model) values(@new_model_name, @model);
    ```

7. 모델을 보려면 간단한 SELECT 문을 실행 합니다.

    ```sql
    SELECT * FROM iris_models;
    GO
    ```

    **결과**

    |model_name | model |
    |------|------|
    | Naive Bayes | 0x800363736B6C656172 중... |
    | Naive Bayes 1 월 1 일 2018 오전 9시 39분 | 0x800363736B6C656172 중... |
    | Naive Bayes 2 월 1 일 2018 오전 10시 51분 | 0x800363736B6C656172 중... |

## <a name="generate-scores-from-the-model"></a>모델에서 점수를 생성 합니다.

마지막으로, 보겠습니다을 변수에 테이블에서이 모델을 로드 하 고 점수를 생성 하는 Python에 다시 전달 합니다.

1. 점수 매기기를 수행 하는 저장된 프로시저를 만들려면 다음 코드를 실행 합니다. 

    ```sql
    CREATE PROCEDURE predict_species (@model varchar(100))
    AS
    BEGIN
    DECLARE @nb_model varbinary(max) = (SELECT model FROM iris_models WHERE model_name = @model);
    EXEC sp_execute_external_script @language = N'Python', 
    @script = N'
    import pickle
    irismodel = pickle.loads(nb_model)
    species_pred = irismodel.predict(iris_data[[1,2,3,4]])
    iris_data["PredictedSpecies"] = species_pred
    OutputDataSet = iris_data.query( ''PredictedSpecies != SpeciesId'' )[[0, 5, 6]]
    print(OutputDataSet)
    '
    , @input_data_1 = N'select id, "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "SpeciesId" from iris_data'
    , @input_data_1_name = N'iris_data'
    , @params = N'@nb_model varbinary(max)'
    , @nb_model = @nb_model
    WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));
    END;
    GO
    ```

    저장된 프로시저는 Naïve Bayes 모델 테이블에서 가져오고 모델에 연결 된 함수를 사용 하 여 점수를 생성 합니다. 이 예제에서는 저장된 프로시저는 모델 이름을 사용 하 여 테이블에서 모델을 가져옵니다. 그러나 어떤 유형의 메타 데이터를 저장 하는 모델에 따라 얻을 수 있습니다 수도 가장 최근의 모델 또는 모델의 높은 정확도.

2. 모델 "Naive Bayes 라는 이름이" 점수 매기기 코드를 실행 하는 저장된 프로시저에 전달 하려면 다음 줄을 실행 합니다. 

    ```sql
    EXEC predict_species 'Naive Bayes';
    GO
    ```

    저장된 프로시저를 실행 하는 경우 Python data.frame를 반환 합니다. T-SQL이이 줄은 반환 된 결과 대 한 스키마를 지정합니다. `WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));`

    결과 새 테이블을 삽입할 수도 있고 응용 프로그램에를 반환할 수 있습니다.

    이 예제는 점수 매기기에 대 한 Python iris 데이터 집합에서 데이터를 사용 하 여 간단한 변경 되었습니다. (줄이 표시 되는지 `iris_data[[1,2,3,4]])`.) 그러나 일반적으로 새 데이터를 가져오는 SQL 쿼리를 실행 하는 Python으로 전달 하는 `InputDataSet`합니다. 

### <a name="remarks"></a>주의

Python에서 작업 하는 데 익숙한 데이터를 로드, 일부 요약 및 그래프를 만드는 다음 모델 학습 및 250 똑같은 코드가 모두에서 몇 가지 점수를 생성 수 있습니다.

그러나 SQL Server의 프로세스 (예: 모델 생성, 점수 매기기, 등)을 운용 하는 것이 목표인 경우 되기 수 나누는 프로세스 매개 변수를 사용 하 여 수정할 수 있는 단계를 반복 하는 방법을 고려해 야 하는 것이 중요 합니다. 가능한 한 명확 하 게 입력 및 저장된 프로시저 입력 및 출력에 매핑되는 출력을 정의 하는 저장된 프로시저에서 실행 되는 Python 코드가 필요한 합니다.

또한 모델 학습 또는 점수를 생성 하는 프로세스에서 데이터 탐색 프로세스를 구분 하 여 일반적으로 성능을 높일 수 있습니다. 

병렬 처리와 같은 SQL Server의 기능을 활용 하 여 또는에서 알고리즘을 사용 하 여 점수 매기기 및 학습 프로세스 최적화할 경우가 많습니다 있습니다 [revoscalepy](../python/what-is-revoscalepy.md) 또는 [MicrosoftML](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) 해당 지원 스트리밍 병렬 실행 보다는 표준 Python 라이브러리를 사용 합니다. 

## <a name="next-lesson"></a>다음 단원

최종 단원에서는 SQL Server를 사용 하 여 계산 컨텍스트로 써 원격 클라이언트에서 Python 코드를 실행 합니다. Python 클라이언트 없는 또는 Python 저장된 프로시저 외부에서 실행 하지 않으려는 경우이 단계는 선택 사항입니다.

+ [Python 클라이언트에서 revoscalepy 모델 만들기](use-python-revoscalepy-to-create-model.md)
