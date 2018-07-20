---
title: 사용 하 여 Python 모델 학습 및 점수 매기기에 대 한 sql | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 02ffd5a25c076ef5a65a6e3a998aae485e37d982
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39085025"
---
# <a name="use-python-model-in-sql-for-training-and-scoring"></a>SQL에서 Python 모델을 사용 하 여 학습 및 점수 매기기에 대 한
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

에 [이전 단원](wrap-python-in-tsql-stored-procedure.md), SQL과 함께 Python을 사용 하기 위한 일반적인 패턴을 학습 합니다. Python 코드는 명확 하 게 정의 된 하나의 data.frame, 출력 및 필요에 따라 여러 스칼라 또는 이진 변수를 출력 하는 것이 알아보았습니다. SQL 저장 프로시저는 Python에 올바른 형식의 데이터를 전달 하 고 결과 처리 하도록 설계 되어야 하는 것이 배웠습니다.

이 섹션에서는이 동일한 패턴을 사용 하 여 SQL Server를 추가한 다음 데이터에서 모델을 학습 및 모델 SQL Server 테이블을 저장 합니다.

+ Python 기계 학습 함수를 호출 하는 저장된 프로시저를 디자인 합니다.
+ 저장된 프로시저는 모델 학습에 사용 하도록 SQL Server에서 데이터를 해야 합니다.
+ 저장된 프로시저는 이진 변수 학습된 된 모델을 출력합니다. 
+ 변수는 모델 테이블에 삽입 하 여 학습된 된 모델을 저장 합니다. 

## <a name="create-the-stored-procedure-and-train-a-python-model"></a>저장된 프로시저 만들기 및 Python 모델을 학습

1. 모델을 작성 하는 저장된 프로시저를 만들려면 SQL Server Management Studio에서 다음 코드를 실행 합니다.

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

2. 이 명령은 오류 없이 실행 되 면 새 저장된 프로시저를 만들고 데이터베이스에 추가 합니다. Management Studio에서 저장된 프로시저를 찾을 수 있습니다 **개체 탐색기**아래에 있는 **프로그래밍**합니다.

3. 이제 저장된 프로시저를 실행 합니다.

    ```sql
    EXEC generate_iris_model
    ```

    저장된 프로시저 입력 필요를 제공 하지 않은 오류를 가져와야 합니다.

    "프로시저 또는 함수 'generate_iris_model' 예상 매개 변수 '\@trained_model'에 제공 되지 않았습니다."

4. 필요한 입력을 사용 하 여 모델을 생성 하 고 테이블에 저장 하려면 일부 추가 문이 필요 합니다.

    ```sql
    DECLARE @model varbinary(max);
    EXEC generate_iris_model @model OUTPUT;
    INSERT INTO iris_models (model_name, model) values('Naive Bayes', @model);
    ```

5. 이제 모델 생성 코드를 한 번 더 실행 해 보세요. 

    오류를 얻게 됩니다: "PRIMARY KEY 제약 조건 위반 중복 키 'dbo.iris_models' 개체에 삽입할 수 없습니다. 중복 키 값 (Naive Bayes)은 ".

    INSERT 문의 일부로 "Naive Bayes"에 수동으로 입력 하 여 모델 이름을 제공한 때문입니다. 만들려는 모델의 여러 다른 매개 변수 또는 다른 알고리즘을 사용 하 여 각 실행에서 가정 하 고, 있습니다 모델을 자동으로 이름을 지정할 수 있습니다 하 고 더 쉽게 식별할 수 있도록 설정 메타 데이터 구성표를 고려해 야 합니다.

6. 를이 오류를 해결 하기 위해 SQL 래퍼에 약간의 수정을 거치면 할 수 있습니다. 이 예제에는 현재 날짜 및 시간을 추가 하 여 고유한 모델 이름을 생성 합니다.

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
    | Naive Bayes | 0x800363736B6C656172... |
    | Naive Bayes 01 2018 년 1 월 오전 9시 39분 | 0x800363736B6C656172... |
    | Naive Bayes 01 2018 년 2 월 오전 10시 51분 | 0x800363736B6C656172... |

## <a name="generate-scores-from-the-model"></a>모델에서 점수를 생성 합니다.

마지막으로 보겠습니다 변수를 테이블에서이 모델을 로드 하 고 점수를 생성 하는 Python으로 다시 전달할 합니다.

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

    저장된 프로시저 원시 Bayes 모델 테이블에서 가져오고 모델과 관련 된 함수를 사용 하 여 점수를 생성 합니다. 이 예제에서는 저장된 프로시저에서 모델 이름을 사용 하 여 테이블에서 모델을 가져옵니다. 그러나 모델로 저장 하는 메타 데이터의 종류에 따라 가져올 수도 있습니다 최신 모델 또는 모델 정확도 가장 높은 합니다.

2. 모델 이름을 "Naive Bayes" 점수 매기기 코드를 실행 하는 저장된 프로시저에 전달할 다음 줄을 실행 합니다. 

    ```sql
    EXEC predict_species 'Naive Bayes';
    GO
    ```

    저장된 프로시저를 실행 하면 Python data.frame을 반환 합니다. T-SQL이이 줄 반환된 된 결과 대 한 스키마를 지정합니다. `WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));`

    결과 새 테이블을 삽입할 수도 있고 응용 프로그램에 반환 합니다.

    이 예제는 점수를 매기기 위해 Python iris 데이터 집합에서 데이터를 사용 하 여 간단한 변경 되었습니다. (줄이 표시 되는지 `iris_data[[1,2,3,4]])`.) 그러나 일반적으로 새 데이터를 가져오는 SQL 쿼리를 실행 하는 Python으로를 전달 `InputDataSet`합니다. 

### <a name="remarks"></a>Remarks

Python에서 작업에 사용 하는 경우 데이터를 로드, 일부 요약 및 그래프를 만드는 다음 모델 학습 및 코드 250 동일한 줄에 모두 몇 가지 점수를 생성에 익숙한 수 있습니다.

그러나 SQL Server의 프로세스 (예: 모델 만들기, 점수 매기기, 등)를 운영 하는 것이 목표인 경우 것 매개 변수를 사용 하 여 수정할 수 있는 반복 가능한 단계로 프로세스를 분리할 수 있습니다 하는 방법을 고려해 야 합니다. 가능한 만큼 명확 하 게 입력 및 저장된 프로시저 입력 및 출력에 매핑되는 출력을 정의 하는 저장된 프로시저에서 실행 되는 Python 코드를 원하는 합니다.

또한 모델을 학습 또는 점수를 생성 하는 프로세스에서 데이터 탐색 프로세스를 구분 하 여 일반적으로 성능을 개선할 수 있습니다. 

병렬 처리와 같은 SQL Server의 기능을 활용 하 여 또는 알고리즘을 사용 하 여 점수 매기기 및 교육 프로세스 최적화 종종 수 [revoscalepy](../python/what-is-revoscalepy.md) 하거나 [MicrosoftML](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) 해당 지원 스트리밍 및 병렬 실행을 사용 하는 대신 표준 Python 라이브러리입니다. 

## <a name="next-lesson"></a>다음 단원

마지막 단원에서는 SQL Server 계산 컨텍스트로 사용 하 여 원격 클라이언트에서 Python 코드를 실행 합니다. Python 클라이언트를 없는 또는 저장된 프로시저 외부 Python을 실행 하지 않으려는 경우이 단계는 선택 사항입니다.

+ [Python 클라이언트에서 revoscalepy 모델 만들기](use-python-revoscalepy-to-create-model.md)
