---
title: 저장 프로시저를 사용한 학습 및 예측 용 Python 모델에 대 한 빠른 시작
description: SQL Server 저장 프로시저에 Python 코드를 포함 하 여 클래식 Iri 데이터 집합으로 Python 모델을 만들고 학습 하 고 사용할 수 있습니다. SQL Server에 학습 된 모델을 저장 한 다음이를 사용 하 여 예측 결과를 생성 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 47ee23d945ded9fac97fe3eddc2137eeead00ae1
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469506"
---
# <a name="quickstart-create-train-and-use-a-python-model-with-stored-procedures-in-sql-server"></a>빠른 시작: SQL Server에서 저장 프로시저를 사용 하 여 Python 모델 만들기, 학습 및 사용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 빠른 시작에서는 Python을 사용 하 여 두 개의 저장 프로시저를 만들고 실행 합니다. 첫 번째는 클래식 Iri 꽃 데이터 집합을 사용 하 고 Naive Bayes 모델을 생성 하 여 꽃 특성을 기반으로 하는 조리개 종류를 예측 합니다. 두 번째 절차는 점수 매기기를 위한 것입니다. 첫 번째 절차에서 생성 된 모델을 호출 하 여 예측 집합을 출력 합니다. 저장 프로시저에 코드를 배치 하면 다른 저장 프로시저와 클라이언트 응용 프로그램에서 작업을 포함 하 고 재사용 가능 하며 호출할 수 있습니다. 

이 빠른 시작을 완료 하 여 다음을 배울 수 있습니다.

> [!div class="checklist"]
> * 저장 프로시저에 Python 코드를 포함 하는 방법
> * 저장 프로시저의 입력을 통해 코드에 입력을 전달 하는 방법
> * 저장 프로시저를 사용 하 여 모델을 운영 하는 방법

## <a name="prerequisites"></a>사전 요구 사항

이전 퀵 스타트 인 [SQL Server에 python이 있는지 확인](quickstart-python-verify.md)하 고,이 빠른 시작에 필요한 python 환경을 설정 하기 위한 정보 및 링크를 제공 합니다.

이 연습에서 사용 되는 샘플 데이터는 [**irissql**](demo-data-iris-in-sql.md) 데이터베이스입니다.

## <a name="create-a-stored-procedure-that-generates-models"></a>모델을 생성 하는 저장 프로시저 만들기

SQL Server 개발의 일반적인 패턴은 프로그래밍 가능 작업을 별개의 저장 프로시저에 구성 하는 것입니다. 이 단계에서는 결과를 예측 하는 모델을 생성 하는 저장 프로시저를 만듭니다. 

1. **Irissql** 데이터베이스에 연결 된 Management Studio에서 새 쿼리 창을 엽니다. 

    ```sql
    USE irissql
    GO
    ```

2. 다음 코드를 복사 하 여 새 저장 프로시저를 만듭니다. 

   이 프로시저는 실행 될 때 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 를 호출 하 여 Python 세션을 시작 합니다. 
   
   Python 코드에 필요한 입력은이 저장 프로시저에 입력 매개 변수로 전달 됩니다. 출력은 기계 학습 알고리즘에 대 한 Python **scikit 학습** 라이브러리를 기반으로 학습 된 모델이 됩니다. 

   이 코드는 [**pickle**](https://docs.python.org/2/library/pickle.html) 를 사용 하 여 모델을 직렬화 합니다. 모델은 **iris_data** 테이블의 0부터 4 열의 데이터를 사용 하 여 학습 됩니다. 
   
   프로시저의 두 번째 부분에 표시 되는 매개 변수는 데이터 입력 및 모델 출력을 표현 합니다. 저장 프로시저에서 실행 되는 Python 코드에서 런타임에 전달 되는 저장 프로시저 입력 및 출력에 매핑되는 명확 하 게 정의 된 입력 및 출력을 갖도록 할 수 있습니다. 

    ```sql
    CREATE PROCEDURE generate_iris_model (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script @language = N'Python',
    @script = N'
    import pickle
    from sklearn.naive_bayes import GaussianNB
    GNB = GaussianNB()
    trained_model = pickle.dumps(GNB.fit(iris_data[[0,1,2,3]], iris_data[[4]].values.ravel()))
    '
    , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "SpeciesId" from iris_data'
    , @input_data_1_name = N'iris_data'
    , @params = N'@trained_model varbinary(max) OUTPUT'
    , @trained_model = @trained_model OUTPUT;
    END;
    GO
    ```

3. 저장 프로시저가 있는지 확인 합니다. 

   이전 단계의 T-sql 스크립트가 오류 없이 실행 된 경우 **generate_iris_model** 라는 새 저장 프로시저가 만들어지고 **irissql** 데이터베이스에 추가 됩니다. Management Studio의 **개체 탐색기**에서 **프로그래밍 기능**을 통해 저장 프로시저를 찾을 수 있습니다.

## <a name="execute-the-procedure-to-create-and-train-models"></a>프로시저를 실행 하 여 모델을 만들고 학습 합니다.

이 단계에서는 포함 된 코드를 실행 하는 프로시저를 실행 하 여 학습 되 고 serialize 된 모델을 출력으로 만듭니다. SQL Server 다시 사용 하기 위해 저장 된 모델은 바이트 스트림으로 직렬화 되 고 데이터베이스 테이블의 VARBINARY (MAX) 열에 저장 됩니다. 모델을 만들고, 학습 하 고, serialize 하 고, 데이터베이스에 저장 한 후에는 다른 프로시저 또는 점수 매기기 작업의 [예측 t-sql](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) 함수에 의해 호출 될 수 있습니다.

1. 프로시저를 실행 하려면 다음 코드를 복사 합니다. 저장 프로시저 `EXEC` 를 실행 하는 특정 문은 다섯 번째 줄에 있습니다.

   이 특정 스크립트는 동일한 이름 ("Naive Bayes")의 기존 모델을 삭제 하 여 동일한 절차를 다시 실행 하 여 새로 만든 공간을 만듭니다. 모델을 삭제 하지 않으면 개체가 이미 존재 하는 것을 나타내는 오류가 발생 합니다. 모델은 **irissql** 데이터베이스를 만들 때 프로 비전 된 **iris_models**라는 테이블에 저장 됩니다.

    ```sql
    DECLARE @model varbinary(max);
    DECLARE @new_model_name varchar(50)
    SET @new_model_name = 'Naive Bayes'
    EXEC generate_iris_model @model OUTPUT;
    DELETE iris_models WHERE model_name = @new_model_name;
    INSERT INTO iris_models (model_name, model) values(@new_model_name, @model);
    GO
    ```

2. 모델이 모델 목록을 반환 하는 다른 방법으로 삽입 되었는지 확인 합니다.

    ```sql
    SELECT * FROM dbo.iris_models
    ```

    **결과**

    | model_name  | model |
    |---|-----------------|
    | Naive Bayes | 0x800363736B6C6561726E2E6E616976655F62617965730A... | 

## <a name="create-and-execute-a-stored-procedure-for-generating-predictions"></a>예측을 생성 하는 저장 프로시저 만들기 및 실행

모델을 만들고, 학습 하 고, 저장 했으므로 다음 단계로 이동 합니다. 예측을 생성 하는 저장 프로시저 만들기 이렇게 하려면 sp_execute_external_script를 호출 하 여 Python을 시작한 후 마지막 연습에서 만든 serialize 된 모델을 로드 하는 Python 스크립트를 전달 하 고 점수에 대 한 데이터 입력을 제공 합니다.

1. 다음 코드를 실행 하 여 점수 매기기를 수행 하는 저장 프로시저를 만듭니다. 런타임에이 프로시저는 이진 모델을 로드 하 고, 열 `[1,2,3,4]` 을 입력으로 사용 하 고, 열 `[0,5,6]` 을 출력으로 지정 합니다.

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
    OutputDataSet = iris_data[[0,5,6]] 
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

2. 모델 이름 "Naive Bayes"를 제공 하 여 프로시저에서 사용할 모델을 알 수 있도록 저장 프로시저를 실행 합니다. 

    ```sql
    EXEC predict_species 'Naive Bayes';
    GO
    ```

    저장 프로시저를 실행 하면 Python 데이터 프레임이 반환 됩니다. T-sql의이 줄은 반환 된 결과 `WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));`에 대 한 스키마를 지정 합니다. 결과를 새 테이블에 삽입 하거나 응용 프로그램에 반환할 수 있습니다.

    ![실행 중인 저장 프로시저의 결과 집합](media/train-score-using-python-NB-model-results.png)

    결과는 흰꽃잎색 특성을 입력으로 사용 하는 방법에 대 한 150의 예측입니다. 대부분의 관찰에서 예측 된 종류는 실제 종류와 일치 합니다.

    이 예제는 학습 및 점수 매기기에 Python iri 데이터 집합을 사용 하 여 간단 하 게 만들었습니다. 보다 일반적인 접근 방법에는 새 데이터를 가져오기 위해 SQL 쿼리를 실행 하 고이를 Python `InputDataSet`으로 전달 하는 작업이 포함 됩니다. 

## <a name="conclusion"></a>결론

이 연습에서는 각 저장 프로시저에서 시스템 저장 프로시저를 사용 하 여 Python 프로세스를 시작 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 다른 태스크 전용 저장 프로시저를 만드는 방법을 알아보았습니다. Python 프로세스에 대 한 입력은 sp_execute_external 스크립트에 매개 변수로 전달 됩니다. SQL Server 데이터베이스의 Python 스크립트 자체와 데이터 변수는 모두 입력으로 전달 됩니다.

일반적으로는 세련 된 Python 코드와 함께 SSMS를 사용 하거나 행 기반 출력을 반환 하는 간단한 Python 코드를 사용 하도록 계획 해야 합니다. 이 도구로 SSMS는 T-sql과 같은 쿼리 언어를 지원 하 고 평면화 된 행 집합을 반환 합니다. 코드에서 산 점도 또는 히스토그램과 같은 시각적 출력을 생성 하는 경우 이미지를 렌더링할 수 있는 도구나 최종 사용자 응용 프로그램이 필요 합니다.

광범위 한 작업을 처리 하는 모든 포괄 스크립트를 작성 하는 데 사용 되는 일부 Python 개발자의 경우에는 별도의 프로시저로 태스크를 구성 하지 못할 수 있습니다. 하지만 학습 및 점수 매기기에는 서로 다른 사용 사례가 있습니다. 이러한 항목을 구분 하 여 각 작업을 서로 다른 일정에 배치 하 고 작업에 범위를 지정할 수 있습니다.

마찬가지로, 높아지면 SQL Server 기능 (예: 병렬 처리, 리소스 관리)을 활용 하거나 스트리밍 및 병렬 실행을 지 원하는 [revoscalepy](../python/ref-py-revoscalepy.md) 또는 [microsoftml](../python/ref-py-microsoftml.md) 의 알고리즘을 사용 하는 스크립트를 작성 하 여 사용할 수도 있습니다. 학습 및 점수 매기기를 분리 하 여 특정 작업에 대 한 최적화를 대상으로 지정할 수 있습니다.

최종 장점으로는 매개 변수를 사용 하 여 프로세스를 수정할 수 있습니다. 이 연습에서는 모델 (이 예에서는 "Naive Bayes" 이라고 명명 됨)을 만든 Python 코드가 점수 매기기 프로세스에서 모델을 호출 하는 두 번째 저장 프로시저에 대 한 입력으로 전달 되었습니다. 이 연습에서는 하나의 모델만 사용 하지만 점수 매기기 작업에서 모델을 매개 변수화 하 여 스크립트를 보다 유용 하 게 만드는 방법을 생각해 볼 수 있습니다.

## <a name="next-steps"></a>다음 단계

Python에 대 한 SQL 개발자 인 경우 로컬 세션에서 원격 SQL Server 인스턴스로 실행을 전환할 수 있는 기능을 사용 하 여 로컬로 Python 코드를 사용 하는 단계 및 도구를 검토 합니다.

> [!div class="nextstepaction"]
> [Python 클라이언트 워크스테이션을 설정](../python/setup-python-client-tools-sql.md)합니다.

