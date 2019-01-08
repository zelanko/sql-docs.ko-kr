---
title: 저장 프로시저-SQL Server Machine Learning Python 모델 학습에 사용 하 여 예측에 대 한 빠른 시작
description: 만들기, 학습 및 클래식 붓 꽃 데이터 집합을 사용 하 여 Python 모델을 사용 하려면 SQL Server 저장 프로시저에서 Python 코드를 포함 합니다. SQL server에 학습된 된 모델을 저장 하 고를 사용 하 여 예측된 결과 생성 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: e8bacc383eba1148c1b357c344bc483e824df99b
ms.sourcegitcommit: baca29731a1be4f8fa47567888278394966e2af7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/04/2019
ms.locfileid: "54046913"
---
# <a name="quickstart-create-train-and-use-a-python-model-with-stored-procedures-in-sql-server"></a>빠른 시작: 만들기, 학습 및 Python 모델을 사용 하 여 SQL Server에서 저장된 프로시저를 사용 하 여
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 빠른 시작에서는 Python을 사용 하 여 만들고 두 개의 저장된 프로시저를 실행 합니다. 첫 번째 클래식 아이리스 꽃 데이터 집합을 사용 하 고 꽃 특징을 기반으로 아이리스 종류를 예측 하는 것은 순진한 Bayes 모델을 생성 합니다. 두 번째 절차는 점수 매기기입니다. 예측 집합을 출력 하는 첫 번째 절차에서 생성 된 모델을 호출 합니다. 저장된 프로시저에서 코드를 배치 하 여 작업은 포함 된, 재사용 가능한 및 호출 가능 다른 저장된 프로시저 및 클라이언트 응용 프로그램입니다. 

이 빠른 시작을 완료 하면 배웁니다.

> [!div class="checklist"]
> * 저장된 프로시저에서 Python 코드를 포함 하는 방법
> * 저장된 프로시저에 입력을 통해 코드에 대 한 입력을 전달 하는 방법
> * 모델을 운영할 저장된 프로시저를 사용 하는 방법

## <a name="prerequisites"></a>사전 요구 사항

이전 빠른 시작에서는 [SQL Server에 있는지 확인 하는 Python](quickstart-python-verify.md), 정보를 제공 하 고이 빠른 시작에 필요한 Python 환경을 설정 하는 것에 대 한 링크입니다.

이 연습에 사용 되는 샘플 데이터를 [ **irissql** ](demo-data-iris-in-sql.md) 데이터베이스입니다.

## <a name="create-a-stored-procedure-that-generates-models"></a>모델을 생성 하는 저장된 프로시저 만들기

SQL Server 개발에서 일반적인 패턴으로 고유한 저장된 프로시저 프로그래밍 작업을 구성 하는 것입니다. 이 단계에서는 결과 예측에 대 한 모델을 생성 하는 저장된 프로시저를 만들게 됩니다. 

1. 에 열린 Management studio에서 새 쿼리 창이 연결 된 **irissql** 데이터베이스. 

    ```sql
    USE irissql
    GO
    ```

2. 새 저장된 프로시저를 만드는 다음 코드를 복사 합니다. 

   를 실행 하는 경우이 프로시저 호출 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) Python 세션을 시작 합니다. 
   
   Python 코드에 필요한 입력이 저장된 프로시저에 입력된 매개 변수로 전달 됩니다. 출력은 Python을 기반으로 학습된 된 모델을 됩니다 **scikit-알아봅니다** 기계 학습 알고리즘에 대 한 라이브러리입니다. 

   이 코드를 사용 [ **pickle** ](https://docs.python.org/2/library/pickle.html) 모델을 serialize 합니다. 모델에서 열의 0부터 4 까지의 데이터를에서 사용 하 여 학습 됩니다 합니다 **iris_data** 테이블입니다. 
   
   프로시저의 두 번째 부분에 표시 하는 매개 변수를 데이터 입력을 명확히 하 고 모델 출력 합니다. 가능한 만큼 입력 명확 하 게 정의 하는 저장된 프로시저에서 실행 되는 Python 코드 한 저장된 프로시저 입력 및 출력 런타임에 전달에 매핑되는 출력 합니다. 

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

3. 저장된 프로시저가 있는지 확인 합니다. 

   이전 단계에서 T-SQL 스크립트가 오류 없이 실행 하는 경우 새 저장 프로시저 호출 **generate_iris_model** 만들어지고에 추가 합니다 **irissql** 데이터베이스입니다. Management Studio에서 저장된 프로시저를 찾을 수 있습니다 **개체 탐색기**아래에 있는 **프로그래밍**합니다.

## <a name="execute-the-procedure-to-create-and-train-models"></a>만들고 모델을 학습 하는 절차를 실행 합니다.

이 단계에서 출력으로 학습 하 고 직렬화 된 모델을 만드는 포함된 된 코드를 실행 하는 절차를 실행 합니다. SQL Server에서 다시 사용할 수 있도록 저장 된 모델을 바이트 스트림으로 직렬화 되 고 데이터베이스 테이블에 varbinary (max) 열에 저장 합니다. 모델 생성, 학습, serialize 되어 데이터베이스에 저장, 되 면 호출 될 수 또는 다른 프로시저에서 합니다 [예측 T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) 워크 로드를 평가 시 함수입니다.

1. 프로시저를 실행한 다음 코드를 복사 합니다. 저장된 프로시저를 실행 하는 것에 대 한 특정 문이 `EXEC` 다섯 번째 줄에 있습니다.

   이 스크립트는 동일한 이름 ("Naive Bayes") 확보 하기 위해 새로 만든 동일한 절차를 다시 실행 하 여 기존 모델을 삭제 합니다. 모델 삭제 하지 않고 오류 개체가 이미 있다는 발생 합니다. 모델 이라고 하는 테이블에 저장 됩니다 **iris_models**를 만들 때 프로 비전 합니다 **irissql** 데이터베이스입니다.

    ```sql
    DECLARE @model varbinary(max);
    DECLARE @new_model_name varchar(50)
    SET @new_model_name = 'Naive Bayes'
    EXEC generate_iris_model @model OUTPUT;
    DELETE iris_models WHERE model_name = @new_model_name;
    INSERT INTO iris_models (model_name, model) values(@new_model_name, @model);
    GO
    ```

2. 모델 삽입 되었는지 확인 모델 목록을 반환 하는 또 다른 방법은 것

    ```sql
    SELECT * FROM dbo.iris_models
    ```

    **결과**

    | model_name  | model |
    |---|-----------------|
    | Naive Bayes | 0x800363736B6C6561726E2E6E616976655F62617965730A... | 

## <a name="create-and-execute-a-stored-procedure-for-generating-predictions"></a>만들기 및 예측을 생성 하는 것에 대 한 저장된 프로시저를 실행 합니다.

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

이 연습에서는 다른 작업을 각 저장된 프로시저는 시스템 저장 프로시저를 사용 하는 위치에 저장된 프로시저를 만드는 방법을 배웠습니다 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) Python 프로세스를 시작 합니다. Python 프로세스에 대 한 입력 매개 변수로 sp_execute_external 스크립트에 전달 됩니다. Python 스크립트 자체 및 SQL Server 데이터베이스에서 데이터 변수를 모두 입력으로 전달 됩니다.

일반적으로 SSMS를 사용 하 여 세련 된 Python 코드 또는 행 기반 출력을 반환 하는 간단한 Python 코드를 사용 하 여 계획만 해야 합니다. 도구로 SSMS T-SQL과 같은 쿼리 언어를 지원 하 고 평면화 된 행 집합을 반환 합니다. 산 점도 또는 히스토그램과 같은 visual 출력을 생성 하는 코드, 이미지를 렌더링할 수 있는 도구 또는 최종 사용자 응용 프로그램이 필요 합니다.

다양 한 작업을 처리 하는 일체 스크립트를 작성 하는 데 사용 되는 몇 가지 Python 개발자를 위한 구성 작업의 경우 별도 절차가에 울 수 있지만 불필요 한 합니다. 하지만 학습 및 점수 매기기는 다양 한 사용 사례가 있습니다. 구분 하 여 다른 일정 및 작업에 사용 권한 범위에서 각 작업을 넣을 수 있습니다.

마찬가지로, 리소스 거 버 넌 스, 병렬 처리와 같은 또는 알고리즘을 사용 하 여 스크립트를 작성 하 여 SQL Server의 리소스 기능도 활용할 수 있습니다 [revoscalepy](../python/ref-py-revoscalepy.md) 하거나 [microsoftml](../python/ref-py-microsoftml.md) 는 스트리밍 및 병렬 실행을 지원 합니다. 학습 및 점수 매기기를 분리 하 여 특정 워크 로드에 대 한 최적화 대상으로 지정할 수 있습니다.

최종 혜택은 프로세스 매개 변수를 사용 하 여 수정할 수 있도록 합니다. 이 연습에서는 (이 예제의 "Naive Bayes" 이라는) 모델을 생성 하는 Python 코드는 점수 매기기 프로세스에서 모델을 호출 하는 두 번째 저장된 프로시저에 대 한 입력으로 전달 되었습니다. 이 연습에서는 하나의 모델을 사용 하지만 어떻게 모델 점수 매기기 작업에서 매개 변수화 없게 스크립트 유용한 상상할 수 있습니다.

## <a name="next-steps"></a>다음 단계

Python을 처음 사용 하는 SQL 개발자 인 경우 원격 SQL Server 인스턴스를 로컬 세션에서 실행을 전환 하는 기능을 사용 하 여 단계 및 Python 코드를 로컬로 사용 하기 위한 도구를 검토 합니다.

> [!div class="nextstepaction"]
> [Python 클라이언트 워크스테이션 설정](../python/setup-python-client-tools-sql.md)합니다.

