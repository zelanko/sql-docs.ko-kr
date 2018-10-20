---
title: Python 모델을 학습 및 예측에 대 한 SQL Server에서 사용 | Microsoft Docs
description: 만들고 클래식 아이리스 데이터 집합 및 Python을 사용 하 여 모델을 학습 합니다. SQL server에 모델을 저장 하 고를 사용 하 여 예측된 결과 생성 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/18/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 839bcecdeaf7b5e2a7ea1297fe941353bffed20e
ms.sourcegitcommit: 3cd6068f3baf434a4a8074ba67223899e77a690b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49461839"
---
# <a name="use-a-python-model-in-sql-server-for-training-and-scoring"></a>Python 모델을 학습 및 점수 매기기에 대 한 SQL Server에서 사용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 Python 연습 만들기, 교육 및 모델을 사용 하 여 SQL server에서에 대 한 일반적인 패턴에 알아봅니다. 이 연습에서는 두 개의 저장된 프로시저를 만듭니다. 첫 번째 꽃 특징을 기반으로 아이리스 종류를 예측 하는 것은 순진한 Bayes 모델을 생성 합니다. 두 번째 절차는 점수 매기기입니다. 예측 집합을 출력 하는 첫 번째 절차에서 생성 된 모델을 호출 합니다. 이 연습을 단계별로 실행 하 여 기본 SQL Server 데이터베이스 엔진 인스턴스에서 실행 중인 Python 코드에는 기본적인 기술을 배웁니다.

이 연습에서 사용 하는 샘플 데이터를 [Iris 데이터 집합](demo-data-iris-in-sql.md) 에 **irissql** 데이터베이스입니다.

## <a name="create-a-model-using-a-sproc"></a>저장 프로시저를 사용 하 여 모델 만들기

1. 에 열린 Management studio에서 새 쿼리 창이 연결 된 **irissql** 데이터베이스. 

    ```sql
    USE irissql
    GO
    ```

2. 빌드 및 모델을 학습 하는 저장된 프로시저를 만들려면 새 쿼리 창에서 다음 코드를 실행 합니다. SQL Server에서 다시 사용할 수 있도록 저장 된 모델을 바이트 스트림으로 직렬화 되 고 데이터베이스 테이블에 varbinary (max) 열에 저장 합니다. 모델을 만든 후 학습, 직렬화 되 고 데이터베이스에 저장 된 호출 될 수 나 워크 로드를 평가 시 예측 T-SQL 함수에 다른 프로시저에서.

   이 코드는 scikit 원시 Bayes 알고리즘을 제공 하 고 모델을 serialize 할 pickle을 사용 합니다. 모델에서 열의 0부터 4 까지의 데이터를에서 사용 하 여 학습 됩니다 합니다 **iris_data** 테이블입니다. 프로시저의 두 번째 부분에 표시 하는 매개 변수를 데이터 입력을 명확히 하 고 모델 출력 합니다. 

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

3. 저장된 프로시저가 있는지 확인 합니다. 이전 단계에서 T-SQL 스크립트가 오류 없이 실행 하는 경우 새 저장 프로시저 호출 **generate_iris_model** 만들어지고에 추가 합니다 **irissql** 데이터베이스입니다. Management Studio에서 저장된 프로시저를 찾을 수 있습니다 **개체 탐색기**아래에 있는 **프로그래밍**합니다.

## <a name="execute-the-sproc-to-create-and-train-models"></a>모델을 학습 하는 저장 프로시저를 실행 합니다.

1. 저장된 프로시저를 만든 후에 실행 하려면 아래 다음 코드를 실행 합니다. 저장된 프로시저를 실행 하는 것에 대 한 특정 문이 `EXEC` 다섯 번째 줄에 있습니다.

   이 스크립트는 동일한 이름 ("Naive Bayes") 확보 하기 위해 새로 만든 동일한 절차를 다시 실행 하 여 기존 모델을 삭제 합니다. 모델 삭제 하지 않고 오류 개체가 이미 있다는 발생 합니다. 

    ```sql
    DECLARE @model varbinary(max);
    DECLARE @new_model_name varchar(50)
    SET @new_model_name = 'Naive Bayes '
    SELECT @new_model_name 
    EXEC generate_iris_model @model OUTPUT;
    DELETE iris_models WHERE model_name = @new_model_name;
    INSERT INTO iris_models (model_name, model) values(@new_model_name, @model);
    GO
    ```

2. 출력 영역에서 결과 봅니다. 스크립트에 모델 있는지를 보여 주는 SELECT 문을 포함 합니다. 모델의 목록을 반환 하는 또 다른 방법은 것 `SELECT * FROM iris_models` 에 **irissql**합니다.

    **결과**

    |   | (열 이름 없음 |
    |---|-----------------|
    | 1 | Naive Bayes     | 


## <a name="create-and-execute-a-sproc-for-generating-predictions"></a>만들기 및 예측을 생성 하는 것에 대 한 저장 된 프로시저를 실행 합니다.

만들어, 학습 한 모델을 저장, 했으므로 다음 단계로 이동 합니다: 예측을 생성 하는 저장된 프로시저를 만들고 있습니다. Python을 시작 하 고 마지막 연습에서 생성 하 고 그런 다음이 점수를 매길 데이터 입력을 제공 하는 직렬화 된 모델을 로드 하는 Python 스크립트에 전달 하려면 sp_execute_external_script를 호출 하 여이 작업을 합니다.

1. 점수 매기기를 수행 하는 저장된 프로시저를 만들려면 다음 코드를 실행 합니다. 런타임 시이 프로시저는 이진 모델을 로드, 열을 사용 하 여 `[1,2,3,4]` 입력을 열을 지정 `[0,5,6]` 출력으로 합니다.

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

2. 모델 이름을 "Naive Bayes"를 지정 하 여 프로시저를 사용 하는 모델에서 알 수 있도록 저장된 프로시저를 실행 합니다. 

    ```sql
    EXEC predict_species 'Naive Bayes';
    GO
    ```

    저장된 프로시저를 실행 하면 Python data.frame을 반환 합니다. 반환된 된 결과 대 한 스키마를 지정 하는 T-SQL의이 줄: `WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));`합니다. 결과 새 테이블을 삽입할 수도 있고 응용 프로그램에 반환 합니다.

    ![저장된 프로시저 실행에서 결과 집합](media/train-score-using-python-NB-model-results.png)

    결과 꽃 특성을 사용 하 여 입력으로 지정 하는 방법에 대 한 150 예측 합니다. 예측된 종류는 관찰의 대부분에서는 실제 종류와 일치합니다.

    이 예제는 학습 및 점수 매기기에 대 한 Python iris 데이터 집합을 사용 하 여 간단한 변경 되었습니다. 더 일반적인 방법은 새 데이터를 가져오는 SQL 쿼리를 실행 하는 경우도으로 Python를 전달 `InputDataSet`합니다. 

## <a name="conclusion"></a>결론

이 연습에서는 다른 작업을 각 저장된 프로시저는 시스템 저장 프로시저를 사용 하는 위치에 대 한 저장된 프로시저를 만드는 방법을 배웠습니다 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) Python 프로세스를 시작 합니다. Python 프로세스에 대 한 입력 매개 변수로 sp_execute_external 스크립트에 전달 됩니다. Python 스크립트 자체 및 SQL Server 데이터베이스에서 데이터 변수를 모두 입력으로 전달 됩니다.

Python에서 작업에 사용 하는 경우 데이터를 로드, 일부 요약 및 그래프를 만드는 다음 모델 학습 및 코드 250 동일한 줄에 모두 몇 가지 점수를 생성에 익숙한 수 있습니다. 이 문서에서는 작업의 경우 별도 절차가을 구성 하 여 일반적인 접근 방식에서 다릅니다. 이 방법은 여러 수준에서 유용합니다.

이점 중 하나는 매개 변수를 사용 하 여 수정할 수 있는 반복 가능한 단계로 프로세스를 분리할 수 있습니다. 가능한 만큼 명확 하 게 입력 및 출력 저장된 프로시저 입력에 매핑되는 런타임에 전달 될 수 있는 출력을 정의 하는 저장된 프로시저에서 실행 되는 Python 코드를 원하는 합니다. 이 연습에서는 (이 예제의 "Naive Bayes" 명명 된) 모델을 만드는 Python 코드는 점수 매기기 프로세스에서 모델을 호출 하는 두 번째 저장된 프로시저에 대 한 입력으로 전달 됩니다.

두 번째 장점은 하 여 학습 하 고, 리소스 거 버 넌 스, 병렬 처리와 같은 SQL Server의 기능을 활용 하 여 또는 알고리즘을 사용 하 여 프로세스를 점수 매기기을 최적화할 수 있습니다 [revoscalepy](../python/what-is-revoscalepy.md) 또는 [MicrosoftML ](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) 스트리밍을 지원 하 고 병렬 실행 합니다. 학습 및 점수 매기기를 분리 하 여 특정 워크 로드에 대 한 최적화 대상으로 지정할 수 있습니다.

## <a name="next-steps"></a>다음 단계

이전 자습서 로컬 실행에 집중 합니다. 그러나 실행할 수 있습니다도 Python 코드는 클라이언트 워크스테이션에서 SQL Server를 사용 하 여 원격 계산 컨텍스트로. SQL Server에 연결 하는 클라이언트 워크스테이션을 설정 하는 방법에 대 한 자세한 내용은 참조 하세요. [Python 클라이언트 도구 설정](../python/setup-python-client-tools-sql.md)합니다.

+ [Python 클라이언트에서 revoscalepy 모델 만들기](use-python-revoscalepy-to-create-model.md)
