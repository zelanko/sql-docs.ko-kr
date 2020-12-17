---
description: SQL 기계 학습을 사용하는 Python 및 R 자습서용 아이리스 데모 데이터
title: 자습서용 아이리스 데모 데이터 세트
titleSuffix: SQL machine learning
Description: 아이리스 데이터 세트 및 예상 모델을 포함하는 데이터베이스를 만듭니다. 이 데이터 세트는 SQL 기계 학습을 사용하는 R 및 Python 자습서에 사용됩니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 05/26/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current'
ms.openlocfilehash: 76e746701aa331cf1720ea56befd5956fd65cfd4
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470464"
---
# <a name="iris-demo-data-for-python-and-r-tutorials-with-sql-machine-learning"></a>SQL 기계 학습을 사용하는 Python 및 R 자습서용 아이리스 데모 데이터
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

이 연습에서는 [아이리스 꽃 데이터 세트](https://en.wikipedia.org/wiki/Iris_flower_data_set)의 데이터를 저장할 데이터베이스를 만들고 동일한 데이터를 기반으로 모델을 만듭니다. 아이리스 데이터는 R 및 Python 배포판 모두에 포함되며, SQL 기계 학습용 기계 학습 자습서에서 사용됩니다.

이 연습을 완료하려면 [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) 또는 T-SQL 쿼리를 실행할 수 있는 다른 도구가 있어야 합니다.

이 데이터 세트를 사용하는 자습서 및 빠른 시작에는 다음이 포함됩니다.

+ [빠른 시작: Python에서 예측 모델 만들기 및 점수 매기기](quickstart-python-train-score-model.md)

## <a name="create-the-database"></a>데이터베이스 만들기

1. SQL Server Management Studio를 시작하고 새 **쿼리** 창을 엽니다.  

2. 이 프로젝트에 대한 새 데이터베이스를 만들고 새 데이터베이스를 사용하도록 **쿼리** 창의 컨텍스트를 변경합니다.

    ```sql
    CREATE DATABASE irissql
    GO
    USE irissql
    GO
    ```

3. 데이터를 저장할 테이블 하나와 학습된 모델을 저장할 테이블을 포함한 몇 가지 빈 테이블을 추가합니다. **iris_models** 테이블은 다른 연습에서 생성된 직렬화된 모델을 저장하는 데 사용됩니다.

    다음 코드는 학습 데이터에 대한 테이블을 만듭니다.

    ```sql
    DROP TABLE IF EXISTS iris_data;
    GO
    CREATE TABLE iris_data (
      id INT NOT NULL IDENTITY PRIMARY KEY
      , "Sepal.Length" FLOAT NOT NULL, "Sepal.Width" FLOAT NOT NULL
      , "Petal.Length" FLOAT NOT NULL, "Petal.Width" FLOAT NOT NULL
      , "Species" VARCHAR(100) NOT NULL, "SpeciesId" INT NOT NULL
    );
    ```

4. 다음 코드를 실행하여 학습된 모델을 저장하는 데 사용되는 테이블을 만듭니다. SQL Server에 Python(또는 R) 모델을 저장하려면 직렬화하고 **varbinary(max)** 형식의 열에 저장해야 합니다.

    ```sql
    DROP TABLE IF EXISTS iris_models;
    GO

    CREATE TABLE iris_models (
      model_name VARCHAR(50) NOT NULL DEFAULT('default model') PRIMARY KEY,
      model VARBINARY(MAX) NOT NULL
    );
    GO
    ```

    모델 내용 외에도 일반적으로 모델 이름, 학습된 날짜, 원본 알고리즘 및 매개 변수, 원본 데이터 등의 기타 유용한 메타데이터에 대한 열도 추가합니다. 지금은 간단하게 유지하고 모델 이름만 사용합니다.

## <a name="populate-the-table"></a>테이블 채우기

R 또는 Python에서 기본 제공되는 아이리스 데이터를 가져올 수 있습니다. Python 또는 R을 사용하여 데이터를 데이터 프레임에 로드한 다음, 데이터베이스의 테이블에 삽입할 수 있습니다. 외부 세션의 학습 데이터를 테이블로 이동하는 것은 다단계 프로세스입니다.

+ 원하는 데이터를 가져오는 저장 프로시저를 설계합니다.
+ 저장 프로시저를 실행하여 실제로 데이터를 가져옵니다.
+ 검색된 데이터를 저장해야 하는 위치를 지정하는 INSERT 문을 작성합니다.

1. Python이 통합된 시스템에서 Python 코드를 사용하여 데이터를 로드하는 다음 저장 프로시저를 만듭니다.

    ```sql
    CREATE PROCEDURE get_iris_dataset
    AS
    BEGIN
    EXEC sp_execute_external_script @language = N'Python', 
    @script = N'
    from sklearn import datasets
    iris = datasets.load_iris()
    iris_data = pandas.DataFrame(iris.data)
    iris_data["Species"] = pandas.Categorical.from_codes(iris.target, iris.target_names)
    iris_data["SpeciesId"] = iris.target
    ', 
    @input_data_1 = N'', 
    @output_data_1_name = N'iris_data'
    WITH RESULT SETS (("Sepal.Length" float not null, "Sepal.Width" float not null, "Petal.Length" float not null, "Petal.Width" float not null, "Species" varchar(100) not null, "SpeciesId" int not null));
    END;
    GO
    ```

    이 코드를 실행하면 "명령이 완료되었습니다."라는 메시지가 표시됩니다. 이는 저장 프로시저가 사양에 따라 생성되었다는 의미입니다.

2. 또는 R이 통합된 시스템에서 R을 대신 사용하는 프로시저를 만듭니다.

    ```sql
    CREATE PROCEDURE get_iris_dataset
    AS
    BEGIN
    EXEC sp_execute_external_script @language = N'R', 
    @script = N'
    library(RevoScaleR)
    data(iris)
    iris$SpeciesID <- c(unclass(iris$Species))
    iris_data <- iris
    ', 
    @input_data_1 = N'', 
    @output_data_1_name = N'iris_data'
    WITH RESULT SETS (("Sepal.Length" float not null, "Sepal.Width" float not null, "Petal.Length" float not null, "Petal.Width" float not null, "Species" varchar(100) not null, "SpeciesId" int not null));
    END;
    GO
    ```

3. 실제로 테이블을 채우려면 저장 프로시저를 실행하고 데이터를 써야 하는 테이블을 지정합니다. 저장 프로시저는 실행될 때 Python 또는 R 코드를 실행하여 기본 제공되는 아이리스 데이터 세트를 로드한 다음, **iris_data** 테이블에 데이터를 삽입합니다.

    ```sql
    INSERT INTO iris_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species", "SpeciesId")
    EXEC dbo.get_iris_dataset;
    ```

    T-SQL을 처음 사용하는 경우 INSERT 문이 새 데이터만 추가한다는 점에 유의해야 합니다. 기존 데이터를 확인하거나 테이블을 삭제하고 다시 빌드하지는 않습니다. 동일한 데이터의 여러 복사본이 테이블에 표시되지 않도록 하려면 먼저 `TRUNCATE TABLE iris_data` 문을 실행하면 됩니다. T-SQL [TRUNCATE TABLE](../../t-sql/statements/truncate-table-transact-sql.md) 문은 기존 데이터를 삭제하지만 테이블 구조는 그대로 유지합니다.

## <a name="query-the-data"></a>데이터 쿼리

유효성 검사 단계로, 쿼리를 실행하여 데이터가 업로드되었는지 확인합니다.

1. 개체 탐색기의 데이터베이스에서 **irissql** 데이터베이스를 마우스 오른쪽 단추로 클릭하고 새 쿼리를 시작합니다.

2. 몇 가지 간단한 쿼리를 실행합니다.

    ```sql
    SELECT TOP(10) * FROM iris_data;
    SELECT COUNT(*) FROM iris_data;
    ```

## <a name="next-steps"></a>다음 단계

다음 빠른 시작에서 기계 학습 모델을 만들어 테이블에 저장한 다음, 모델을 사용하여 예측된 결과를 생성합니다.

+ [빠른 시작: Python에서 예측 모델 만들기 및 점수 매기기](quickstart-python-train-score-model.md)