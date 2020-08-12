---
title: '자습서: R에서 예측 모델 배포'
titleSuffix: SQL machine learning
description: 4부로 구성된 이 자습서 시리즈의 4부에서는 R에서 SQL 기계 학습을 사용하여 예측 모델을 배포합니다.
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: cawrites
ms.author: chadam
ms.reviewer: garye, davidph
ms.date: 05/21/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: af3826d5153e2be157a74c96037bff51c6039e7c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85728557"
---
# <a name="tutorial-deploy-a-predictive-model-in-r-with-sql-machine-learning"></a>자습서: R에서 SQL 기계 학습을 사용하여 예측 모델 배포
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
4부로 구성된 이 자습서 시리즈의 4부에서는 R에서 개발한 기계 학습 모델을 SQL Server Machine Learning Services 또는 빅 데이터 클러스터에 배포합니다.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
4부로 구성된 이 자습서 시리즈의 4부에서는 Machine Learning Services를 사용하여 R에서 개발한 기계 학습 모델을 SQL Server에 배포합니다.
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
4부로 구성된 이 자습서 시리즈의 4부에서는 SQL Server R Services를 사용하여 R에서 개발한 기계 학습 모델을 SQL Server에 배포합니다.
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
4부로 구성된 이 자습서 시리즈의 4부에서는 R에서 개발한 기계 학습 모델을 Machine Learning Services를 사용하여 Azure SQL Managed Instance에 배포합니다.
::: moniker-end

이 문서에서는 다음을 수행하는 방법을 알아봅니다.

> [!div class="checklist"]
> * 기계 학습 모델을 생성하는 저장 프로시저 만들기
> * 모델을 데이터베이스 테이블에 저장
> * 모델을 사용하여 예측을 수행하는 저장 프로시저 만들기
> * 새 데이터로 모델 실행

[1부](r-predictive-model-introduction.md)에서 샘플 데이터베이스를 복원하는 방법을 배웠습니다.

[2부](r-predictive-model-prepare-data.md)에서는 샘플 데이터베이스를 가져온 다음, R에서 예측 모델을 학습하는 데 사용할 데이터를 준비하는 방법을 살펴보았습니다.

[3부](r-predictive-model-train.md)에서는 R에서 여러 기계 학습 모델을 만들고 학습시킨 후 가장 정확한 모델을 선택하는 방법을 알아보았습니다.

## <a name="prerequisites"></a>사전 요구 사항

이 자습서의 4부에서는 [**1부**](r-predictive-model-introduction.md)의 사전 요구 사항을 수행하고 [**2부**](r-predictive-model-prepare-data.md) 및 [**3부**](r-predictive-model-train.md)의 단계를 완료했다고 가정합니다.

## <a name="create-a-stored-procedure-that-generates-the-model"></a>모델을 생성하는 저장 프로시저 만들기

이 자습서 시리즈의 3부에서는 의사 결정 트리(dtree) 모델이 가장 정확하다고 확인했습니다. 이제 앞에서 개발한 R 스크립트를 사용하여 R 패키지의 rpart를 통해 dtree 모델을 학습시키고 생성하는 저장 프로시저(`generate_rental_model`)를 만듭니다.

Azure Data Studio에서 다음 명령을 실행합니다.

```sql
USE [TutorialDB]
DROP PROCEDURE IF EXISTS generate_rental_model;
GO
CREATE PROCEDURE generate_rental_model (@trained_model VARBINARY(max) OUTPUT)
AS
BEGIN
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'
rental_train_data$Month   <- factor(rental_train_data$Month);
rental_train_data$Day     <- factor(rental_train_data$Day);
rental_train_data$Holiday <- factor(rental_train_data$Holiday);
rental_train_data$Snow    <- factor(rental_train_data$Snow);
rental_train_data$WeekDay <- factor(rental_train_data$WeekDay);

#Create a dtree model and train it using the training data set
library(rpart);
model_dtree <- rpart(RentalCount ~ Month + Day + WeekDay + Snow + Holiday, data = rental_train_data);
#Serialize the model before saving it to the database table
trained_model <- as.raw(serialize(model_dtree, connection=NULL));
'
        , @input_data_1 = N'
            SELECT RentalCount
                 , Year
                 , Month
                 , Day
                 , WeekDay
                 , Snow
                 , Holiday
            FROM dbo.rental_data
            WHERE Year < 2015
            '
        , @input_data_1_name = N'rental_train_data'
        , @params = N'@trained_model varbinary(max) OUTPUT'
        , @trained_model = @trained_model OUTPUT;
END;
GO
```

## <a name="store-the-model-in-a-database-table"></a>모델을 데이터베이스 테이블에 저장

TutorialDB 데이터베이스에 테이블을 만든 다음, 모델을 테이블에 저장합니다.

1. 모델을 저장하기 위한 테이블(`rental_models`)을 만듭니다.

    ```sql
    USE TutorialDB;
    DROP TABLE IF EXISTS rental_models;
    GO
    CREATE TABLE rental_models (
          model_name VARCHAR(30) NOT NULL DEFAULT('default model') PRIMARY KEY
        , model VARBINARY(MAX) NOT NULL
        );
    GO
    ```

1. 모델 이름을 "DTree"로 지정하여 모델을 테이블에 이진 개체로 저장합니다.

    ```sql
    -- Save model to table
    TRUNCATE TABLE rental_models;
    
    DECLARE @model VARBINARY(MAX);
    
    EXECUTE generate_rental_model @model OUTPUT;
    
    INSERT INTO rental_models (
          model_name
        , model
        )
    VALUES (
         'DTree'
        , @model
        );
    
    SELECT *
    FROM rental_models;
    ```

## <a name="create-a-stored-procedure-that-makes-predictions"></a>예측을 수행하는 저장 프로시저 만들기

학습된 모델 및 새 데이터 세트를 사용하여 예측하는 저장 프로시저(`predict_rentalcount_new`)를 만듭니다.

```sql
-- Stored procedure that takes model name and new data as input parameters and predicts the rental count for the new data
USE [TutorialDB]
DROP PROCEDURE IF EXISTS predict_rentalcount_new;
GO
CREATE PROCEDURE predict_rentalcount_new (
      @model_name VARCHAR(100)
    , @input_query NVARCHAR(MAX)
    )
AS
BEGIN
    DECLARE @model VARBINARY(MAX) = (
            SELECT model
            FROM rental_models
            WHERE model_name = @model_name
            );

    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'
#Convert types to factors
rentals$Month   <- factor(rentals$Month);
rentals$Day     <- factor(rentals$Day);
rentals$Holiday <- factor(rentals$Holiday);
rentals$Snow    <- factor(rentals$Snow);
rentals$WeekDay <- factor(rentals$WeekDay);

#Before using the model to predict, we need to unserialize it
rental_model <- unserialize(model);

#Call prediction function
rental_predictions <- predict(rental_model, rentals);
rental_predictions <- data.frame(rental_predictions);
'
        , @input_data_1 = @input_query
        , @input_data_1_name = N'rentals'
        , @output_data_1_name = N'rental_predictions'
        , @params = N'@model varbinary(max)'
        , @model = @model
    WITH RESULT SETS(("RentalCount_Predicted" FLOAT));
END;
GO
```

## <a name="execute-the-model-with-new-data"></a>새 데이터로 모델 실행

이제 저장 프로시저 `predict_rentalcount_new`를 사용하여 새 데이터에서 대여 수를 예측할 수 있습니다.

```sql
-- Use the predict_rentalcount_new stored procedure with the model name and a set of features to predict the rental count
EXECUTE dbo.predict_rentalcount_new @model_name = 'DTree'
    , @input_query = '
        SELECT CONVERT(INT,  3) AS Month
             , CONVERT(INT, 24) AS Day
             , CONVERT(INT,  4) AS WeekDay
             , CONVERT(INT,  1) AS Snow
             , CONVERT(INT,  1) AS Holiday
        ';
GO
```

다음과 유사한 결과가 표시되어야 합니다.

```results
RentalCount_Predicted
332.571428571429
```

데이터베이스에서 모델을 만들고, 학습하고, 배포했습니다. 그런 다음, 저장 프로시저에서 해당 모델을 사용하여 새 데이터를 기반으로 값을 예측합니다.


## <a name="clean-up-resources"></a>리소스 정리

TutorialDB 데이터베이스 사용을 마치면 서버에서 삭제합니다.

## <a name="next-steps"></a>다음 단계

이 자습서 시리즈의 4부에서는 다음 작업을 수행하는 방법을 알아보았습니다.

* 기계 학습 모델을 생성하는 저장 프로시저 만들기
* 모델을 데이터베이스 테이블에 저장
* 모델을 사용하여 예측을 수행하는 저장 프로시저 만들기
* 새 데이터로 모델 실행

Machine Learning Services에서 R을 사용하는 방법에 대한 자세한 내용은 다음을 참조하세요.

* [간단한 R 스크립트 실행](quickstart-r-create-script.md)
* [R 데이터 구조, 형식 및 개체](quickstart-r-data-types-and-objects.md)
* [R 함수](quickstart-r-functions.md)
