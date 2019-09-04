---
title: 'Python 자습서: 모델 배포 (선형 회귀)'
description: 이 자습서에서는 SQL Server Machine Learning Services에서 Python 및 선형 회귀를 사용 하 여 ski 대 여의 수를 예측 합니다. Machine Learning Services를 사용 하 여 Python에서 개발한 선형 회귀 모델을 SQL Server 데이터베이스에 배포할 수 있습니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/03/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 08f5d19af93ab180c660a264d5aaabc538d527a5
ms.sourcegitcommit: ecb19d0be87c38a283014dbc330adc2f1819a697
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70242521"
---
# <a name="python-tutorial-deploy-a-linear-regression-model-to-sql-server-machine-learning-services"></a>Python 자습서: 선형 회귀 모델을 배포 하 여 SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

네 부분으로 구성 된 자습서 시리즈의 4 부에서는 Machine Learning Services를 사용 하 여 Python에서 개발한 선형 회귀 모델을 SQL Server 데이터베이스로 배포 합니다.

이 문서에서는 다음 방법을 설명합니다.

> [!div class="checklist"]
> * Machine learning 모델을 생성 하는 저장 프로시저 만들기
> * 모델을 데이터베이스 테이블에 저장 합니다.
> * 모델을 사용 하 여 예측을 수행 하는 저장 프로시저 만들기
> * 새 데이터를 사용 하 여 모델 실행

[1 부](python-ski-rental-linear-regression.md)에서는 샘플 데이터베이스를 복원 하는 방법을 배웠습니다.

[2 부](python-ski-rental-linear-regression-prepare-data.md)에서는 SQL Server에서 python 데이터 프레임으로 데이터를 로드 하 고 python에서 데이터를 준비 하는 방법을 배웠습니다.

[3 부](python-ski-rental-linear-regression-train-model.md)에서는 Python에서 선형 회귀 기계 학습 모델을 학습 하는 방법을 배웠습니다.

## <a name="prerequisites"></a>사전 요구 사항

* 이 자습서의 4 부에서는 [1 부](python-ski-rental-linear-regression.md) 및 해당 필수 구성 요소를 완료 했다고 가정 합니다.

## <a name="create-a-stored-procedure-that-generates-the-model"></a>모델을 생성 하는 저장 프로시저 만들기

이제 개발한 Python 스크립트를 사용 하 여 scikit에서 LinearRegression를 사용 하 여 선형 회귀 모델을 학습 하 고 생성 하는 저장 프로시저 **generate_rental_rx_model** 를 만듭니다.

Azure Data Studio에서 다음 T-sql 문을 실행 하 여 모델을 학습 하는 저장 프로시저를 만듭니다.

```sql
-- Stored procedure that trains and generates a Python model using the rental_data and a decision tree algorithm
DROP PROCEDURE IF EXISTS generate_rental_py_model;
go
CREATE PROCEDURE generate_rental_py_model (@trained_model varbinary(max) OUTPUT)
AS
BEGIN
    EXECUTE sp_execute_external_script
      @language = N'Python'
    , @script = N'
from sklearn.linear_model import LinearRegression
import pickle

df = rental_train_data

# Get all the columns from the dataframe.
columns = df.columns.tolist()

# Store the variable well be predicting on.
target = "RentalCount"

# Initialize the model class.
lin_model = LinearRegression()

# Fit the model to the training data.
lin_model.fit(df[columns], df[target])

# Before saving the model to the DB table, convert it to a binary object
trained_model = pickle.dumps(lin_model)'

, @input_data_1 = N'select "RentalCount", "Year", "Month", "Day", "WeekDay", "Snow", "Holiday" from dbo.rental_data where Year < 2015'
, @input_data_1_name = N'rental_train_data'
, @params = N'@trained_model varbinary(max) OUTPUT'
, @trained_model = @trained_model OUTPUT;
END;
GO
```

## <a name="store-the-model-in-a-database-table"></a>모델을 데이터베이스 테이블에 저장 합니다.

TutorialDB 데이터베이스에 테이블을 만든 다음 모델을 테이블에 저장 합니다.

1. Azure Data Studio에서 다음 T-sql 문을 실행 하 여 모델을 저장 하는 데 사용 되는 **rental_py_models** 라는 테이블을 만듭니다.

    ```sql
    USE TutorialDB;
    DROP TABLE IF EXISTS dbo.rental_py_models;
    GO
    CREATE TABLE dbo.rental_py_models (
        model_name VARCHAR(30) NOT NULL DEFAULT('default model') PRIMARY KEY,
        model VARBINARY(MAX) NOT NULL
    );
    GO
    ```

1. 모델 이름이 **linear_model**인 이진 개체로 모델을 테이블에 저장 합니다.

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC generate_rental_py_model @model OUTPUT;
    
    INSERT INTO rental_py_models (model_name, model) VALUES('linear_model', @model);
    ```

## <a name="create-a-stored-procedure-that-makes-predictions"></a>예측을 수행 하는 저장 프로시저 만들기

1. 학습 된 모델과 새 데이터 집합을 사용 하 여 예측을 수행 하는 저장 프로시저 **py_predict_rentalcount** 를 만듭니다. Azure Data Studio 아래에서 T-sql을 실행 합니다.

    ```sql
    DROP PROCEDURE IF EXISTS py_predict_rentalcount;
    GO
    CREATE PROCEDURE py_predict_rentalcount (@model varchar(100))
    AS
    BEGIN
        DECLARE @py_model varbinary(max) = (select model from rental_py_models where model_name = @model);
    
        EXEC sp_execute_external_script
                    @language = N'Python',
                    @script = N'
    
    # Import the scikit-learn function to compute error.
    from sklearn.metrics import mean_squared_error
    import pickle
    import pandas as pd
    
    rental_model = pickle.loads(py_model)
    
    df = rental_score_data
    
    # Get all the columns from the dataframe.
    columns = df.columns.tolist()
    
    # Variable you will be predicting on.
    target = "RentalCount"
    
    # Generate the predictions for the test set.
    lin_predictions = rental_model.predict(df[columns])
    print(lin_predictions)
    
    # Compute error between the test predictions and the actual values.
    lin_mse = mean_squared_error(lin_predictions, df[target])
    #print(lin_mse)
    
    predictions_df = pd.DataFrame(lin_predictions)
    
    OutputDataSet = pd.concat([predictions_df, df["RentalCount"], df["Month"], df["Day"], df["WeekDay"], df["Snow"], df["Holiday"], df["Year"]], axis=1)
    '
    , @input_data_1 = N'Select "RentalCount", "Year" ,"Month", "Day", "WeekDay", "Snow", "Holiday"  from rental_data where Year = 2015'
    , @input_data_1_name = N'rental_score_data'
    , @params = N'@py_model varbinary(max)'
    , @py_model = @py_model
    with result sets (("RentalCount_Predicted" float, "RentalCount" float, "Month" float,"Day" float,"WeekDay" float,"Snow" float,"Holiday" float, "Year" float));
    
    END;
    GO
    ```

1. 예측을 저장 하는 테이블을 만듭니다.

    ```sql
    DROP TABLE IF EXISTS [dbo].[py_rental_predictions];
    GO

    CREATE TABLE [dbo].[py_rental_predictions](
     [RentalCount_Predicted] [int] NULL,
     [RentalCount_Actual] [int] NULL,
     [Month] [int] NULL,
     [Day] [int] NULL,
     [WeekDay] [int] NULL,
     [Snow] [int] NULL,
     [Holiday] [int] NULL,
     [Year] [int] NULL
    ) ON [PRIMARY]
    GO
    ```

1. 저장 프로시저를 실행 하 여 임대 횟수 예측

    ```sql
    --Insert the results of the predictions for test set into a table
    INSERT INTO py_rental_predictions
    EXEC py_predict_rentalcount 'linear_model';

    -- Select contents of the table
    SELECT * FROM py_rental_predictions;
    ```

SQL Server Machine Learning Services에서 모델을 만들고 학습 하 고 배포 했습니다. 그런 다음 저장 프로시저에서 해당 모델을 사용 하 여 새 데이터를 기반으로 값을 예측 합니다.

## <a name="next-steps"></a>다음 단계

이 자습서 시리즈의 4 부에서는 다음 단계를 완료 했습니다.

* Machine learning 모델을 생성 하는 저장 프로시저 만들기
* 모델을 데이터베이스 테이블에 저장 합니다.
* 모델을 사용 하 여 예측을 수행 하는 저장 프로시저 만들기
* 새 데이터를 사용 하 여 모델 실행

SQL Server Machine Learning Services에서 Python을 사용 하는 방법에 대 한 자세한 내용은 다음을 참조 하세요.

+ [SQL Server Machine Learning Services에 대 한 Python 자습서](sql-server-python-tutorials.md)