---
title: '빠른 시작: Python에서 모델 학습'
description: 이 빠른 시작에서는 Python을 사용하여 예측 모델을 만들고 학습합니다. SQL Server 인스턴스의 테이블에 모델을 저장한 다음 SQL Server Machine Learning Services로 새로운 데이터의 값을 예측하는 데 해당 모델을 사용합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/27/2020
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c6c74d73a531a40e0f8e57e7104109de71e27ce3
ms.sourcegitcommit: acfdeacc80c112992c1201748e0b5c59a473032d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/04/2020
ms.locfileid: "76977547"
---
# <a name="quickstart-create-and-score-a-predictive-model-in-python-with-sql-server-machine-learning-services"></a>빠른 시작: SQL Server Machine Learning Services를 사용하여 Python에서 예측 모델 만들기 및 채점
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 빠른 시작에서는 Python을 사용하여 예측 모델을 만들고 학습합니다. SQL Server 인스턴스의 테이블에 모델을 저장한 다음 [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md)로 새로운 데이터의 값을 예측하는 데 해당 모델을 사용합니다.

SQL에서 실행되는 두 개의 저장 프로시저를 만들고 실행합니다. 첫 번째 저장 프로시저는 클래식 아이리스 꽃 데이터 세트를 사용하여 꽃 특성을 기반으로 아이리스 종류를 예측하는 Naive Bayes 모델을 생성합니다. 두 번째 저장 프로시저는 첫 번째 프로시저에서 생성된 모델을 호출하여 새 데이터를 기반으로 예측 세트를 출력합니다. SQL 저장 프로시저에 Python 코드를 배치하면 작업이 SQL에 포함되고 다시 사용할 수 있으며, 다른 저장 프로시저와 클라이언트 애플리케이션에서 호출할 수 있습니다.

이 빠른 시작을 완료하면 다음을 배울 수 있습니다.

> [!div class="checklist"]
> - 저장 프로시저에 Python 코드를 포함하는 방법
> - 저장 프로시저의 입력을 통해 코드에 입력을 전달하는 방법
> - 저장 프로시저를 사용하여 모델을 운영하는 방법

## <a name="prerequisites"></a>사전 요구 사항

- 이 빠른 시작을 수행하려면 Python 언어가 설치된 [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)가 포함된 SQL Server 인스턴스에 대한 액세스 권한이 필요합니다.

- 또한 Python 스크립트가 포함된 SQL 쿼리를 실행하기 위한 도구가 필요합니다. SQL Server 인스턴스에 연결할 수 있는 데이터베이스 관리 또는 쿼리 도구를 사용하여 이러한 스크립트를 실행하고 T-SQL 쿼리 또는 저장 프로시저를 실행할 수 있습니다. 이 빠른 시작에서는 [SSMS(SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)를 사용합니다.

- 이 연습에 사용되는 샘플 데이터는 아이리스 샘플 데이터입니다. [아이리스 데모 데이터](demo-data-iris-in-sql.md)의 지침에 따라 샘플 데이터베이스 **irissql**을 만듭니다.

## <a name="create-a-stored-procedure-that-generates-models"></a>모델을 생성하는 저장 프로시저 만들기

이 단계에서는 결과를 예측하는 모델을 생성하는 저장 프로시저를 만듭니다.

1. SSMS를 열고 SQL Server 인스턴스에 연결한 다음, 새 쿼리 창을 엽니다.

1. irissql 데이터베이스에 연결합니다.

    ```sql
    USE irissql
    GO
    ```

1. 새 저장 프로시저를 만드는 다음 코드를 복사합니다.

   이 프로시저를 실행하면 Python 세션을 시작하는 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)가 호출됩니다. 
   
   Python 코드에 필요한 입력은 이 저장 프로시저의 입력 매개 변수로 전달됩니다. 출력은 기계 학습 알고리즘에 대한 Python **scikit-learn** 라이브러리를 기반으로 학습된 모델입니다. 

   이 코드는 [**pickle**](https://docs.python.org/2/library/pickle.html)을 사용하여 모델을 직렬화합니다. 이 모델은 **iris_data** 테이블의 0~4열의 데이터를 사용하여 학습됩니다. 
   
   프로시저의 두 번째 부분에 보이는 매개 변수는 데이터 입력 및 모델 출력을 설명합니다. 되도록이면 저장 프로시저에서 실행되는 Python 코드의 입력 및 출력이 런타임에 전달되는 저장 프로시저 입력 및 출력에 매핑되도록 명확하게 정의하는 것이 좋습니다.

    ```sql
    CREATE PROCEDURE generate_iris_model (@trained_model VARBINARY(max) OUTPUT)
    AS
    BEGIN
        EXECUTE sp_execute_external_script @language = N'Python'
            , @script = N'
    import pickle
    from sklearn.naive_bayes import GaussianNB
    GNB = GaussianNB()
    trained_model = pickle.dumps(GNB.fit(iris_data[["Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width"]], iris_data[["SpeciesId"]].values.ravel()))
    '
            , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "SpeciesId" from iris_data'
            , @input_data_1_name = N'iris_data'
            , @params = N'@trained_model varbinary(max) OUTPUT'
            , @trained_model = @trained_model OUTPUT;
    END;
    GO
    ```

1. 저장 프로시저가 있는지 확인합니다. 

   이전 단계의 T-SQL 스크립트가 오류 없이 실행된 경우 **generate_iris_model**이라는 새 저장 프로시저가 생성되어 **irissql** 데이터베이스에 추가됩니다. SSMS **개체 탐색기**의 **프로그래밍 기능**에서 저장 프로시저를 찾을 수 있습니다.

## <a name="execute-the-procedure-to-create-and-train-models"></a>프로시저를 실행하여 모델을 만들고 학습

이 단계에서는 포함된 코드를 실행하는 프로시저를 실행하고, 그 출력으로 학습 및 직렬화된 모델을 만듭니다. 

SQL Server에서 다시 사용하기 위해 저장된 모델은 바이트 스트림으로 직렬화되어 데이터베이스 테이블의 VARBINARY(MAX) 열에 저장됩니다. 모델이 생성되고, 학습되고, 직렬화되고, 데이터베이스에 저장된 후에는 다른 프로시저 또는 채점 워크로드의 [PREDICT T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) 함수를 사용하여 모델을 호출할 수 있습니다.

1. 다음 스크립트를 실행하여 프로시저를 실행합니다. 저장 프로시저를 실행하는 특정 문은 네 번째 줄의 `EXECUTE`입니다.

   이 특정 스크립트는 동일한 프로시저를 다시 실행하여 생성되는 모델의 공간을 마련하기 위해 이름이 같은("Naive Bayes") 기존 모델을 삭제합니다. 모델을 삭제하지 않으면 개체가 이미 있다는 내용의 오류가 발생합니다. 모델은 **irissql** 데이터베이스를 만들 때 프로비저닝된 **iris_models**라는 테이블에 저장됩니다.

    ```sql
    DECLARE @model varbinary(max);
    DECLARE @new_model_name varchar(50)
    SET @new_model_name = 'Naive Bayes'
    EXECUTE generate_iris_model @model OUTPUT;
    DELETE iris_models WHERE model_name = @new_model_name;
    INSERT INTO iris_models (model_name, model) values(@new_model_name, @model);
    GO
    ```

1. 모델이 삽입되었는지 확인합니다.

    ```sql
    SELECT * FROM dbo.iris_models
    ```

    **결과**

    | model_name  | model |
    |---|-----------------|
    | Naive Bayes | 0x800363736B6C6561726E2E6E616976655F62617965730A... | 

## <a name="create-and-execute-a-stored-procedure-for-generating-predictions"></a>예측을 생성하는 저장 프로시저를 만들고 실행

모델을 만들고, 학습시키고, 저장했으므로 다음 단계인 예측을 생성하는 저장 프로시저 만들기로 넘어가겠습니다. 이를 위해 직렬화된 모델을 로드하고 채점할 새 데이터 입력을 제공하는 `sp_execute_external_script`를 호출할 것입니다.

1. 다음 코드를 실행하여 채점을 수행하는 저장 프로시저를 만듭니다. 런타임에 이 프로시저는 이진 모델을 로드하고, `[1,2,3,4]` 열을 입력으로 사용하고, `[0,5,6]` 열을 출력으로 지정합니다.

   ```sql
   CREATE PROCEDURE predict_species (@model VARCHAR(100))
   AS
   BEGIN
       DECLARE @nb_model VARBINARY(max) = (
               SELECT model
               FROM iris_models
               WHERE model_name = @model
               );
   
       EXECUTE sp_execute_external_script @language = N'Python'
           , @script = N'
   import pickle
   irismodel = pickle.loads(nb_model)
   species_pred = irismodel.predict(iris_data[["Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width"]])
   iris_data["PredictedSpecies"] = species_pred
   OutputDataSet = iris_data[["id","SpeciesId","PredictedSpecies"]] 
   print(OutputDataSet)
   '
           , @input_data_1 = N'select id, "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "SpeciesId" from iris_data'
           , @input_data_1_name = N'iris_data'
           , @params = N'@nb_model varbinary(max)'
           , @nb_model = @nb_model
       WITH RESULT SETS((
                   "id" INT
                 , "SpeciesId" INT
                 , "SpeciesId.Predicted" INT
                   ));
   END;
   GO
   ```

2. 저장 프로시저를 실행하고, 프로시저가 사용할 모델을 알 수 있도록 모델 이름을 "Naive Bayes"로 지정합니다.

   ```sql
   EXECUTE predict_species 'Naive Bayes';
   GO
   ```

   저장 프로시저를 실행하면 저장 프로시저가 Python data.frame을 반환합니다. 이 T-SQL 줄은 반환된 결과에 대한 `WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));` 스키마를 지정합니다. 결과를 새 테이블에 삽입하거나 애플리케이션에 반환할 수 있습니다.

   ![실행 중인 저장 프로시저의 결과 세트](media/train-score-using-python-NB-model-results.png)

   결과는 꽃의 특징을 입력으로 사용하는 꽃 종류에 대한 150개 예측입니다. 대부분의 관찰에서 예측된 종류는 실제 종류와 일치합니다.

   이 예제는 학습 및 채점에 Python 아이리스 데이터 세트를 사용하여 간단하게 만들었습니다. 보다 일반적인 방법은 SQL 쿼리를 실행하여 새 데이터를 가져오고, Python에 `InputDataSet`로 전달하는 것입니다.

## <a name="conclusion"></a>결론

이 연습에서는 다른 작업에 전용될 저장 프로시저를 만드는 방법을 알아보았으며, 해당 작업에서 각 저장 프로시저는 시스템 저장 프로시저 `sp_execute_external_script`를 사용하여 Python 프로세스를 시작합니다. Python 프로세스에 대한 입력은 `sp_execute_external`에 매개 변수로 전달됩니다. Python 스크립트 자체와 SQL Server 데이터베이스의 데이터 변수는 모두 입력으로 전달됩니다.

일반적으로 세련된 Python 코드와 함께 SSMS를 사용하거나 행 기반 출력을 반환하는 간단한 Python 코드만 사용하도록 계획을 세워야 합니다. SSMS 도구는 T-SQL 같은 쿼리 언어를 지원하고 평면화된 행 세트를 반환합니다. 코드에서 산점도 또는 히스토그램과 같은 시각적 출력을 생성하는 경우 저장 프로시저 외부에서 이미지를 렌더링할 수 있는 별도의 도구 또는 최종 사용자 애플리케이션이 필요합니다.

광범위한 작업을 처리하는 모든 것이 포함된 스크립트를 작성하는 데 익숙한 Python 개발자의 경우 작업을 별도의 프로시저로 구성할 필요가 없다고 생각할 수 있습니다. 하지만 학습과 채점의 사용 사례는 서로 다릅니다. 둘을 구분하면 각 작업을 서로 다른 일정에 배치하고 각 작업의 권한 범위를 지정할 수 있습니다.

마찬가지로, 병렬 처리, 리소스 관리 등의 SQL Server 리소싱 기능을 활용할 수도 있고, 또는 스크립트를 작성하여 스트리밍 및 병렬 실행을 지원하는 [microsoftml](../python/ref-py-microsoftml.md)의 알고리즘을 사용할 수도 있습니다. 학습과 채점을 분리하면 특정 워크로드의 최적화를 목표로 삼을 수 있습니다.

마지막 장점으로, 매개 변수를 사용하여 프로세스를 수정할 수 있습니다. 이 연습에서 모델(이 예제에서는 "Naive Bayes")을 만든 Python 코드는 채점 프로세스에서 모델을 호출하는 두 번째 저장 프로시저에 입력으로 전달되었습니다. 이 연습에서는 하나의 모델만 사용하지만, 채점 작업에서 모델을 어떻게 매개 변수화해야 보다 유용한 스크립트를 만들 수 있을지 생각해 볼 수 있습니다.

## <a name="next-steps"></a>다음 단계

SQL Server Machine Learning Services에 대한 자세한 내용은 다음을 참조하세요.

- [SQL Server Machine Learning Services(Python 및 R)란?](../what-is-sql-server-machine-learning.md)
