---
title: Python 및 R 자습서에 대 한 조리개 데모 데이터 집합
Description: 모델을 저장 하는 데 사용할 Iri 데이터 집합 및 테이블이 포함 된 데이터베이스를 만듭니다. 이 데이터 집합은 SQL Server 저장 프로시저에서 R 언어 또는 Python 코드를 래핑하는 방법을 보여 주는 연습에 사용 됩니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/19/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 78acdd0ef2eed808d8f974c38899282dc823436d
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715505"
---
#  <a name="iris-demo-data-for-python-and-r-tutorials-in-sql-server"></a>SQL Server에서 Python 및 R 자습서에 대 한 데모 데이터를 조리개 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 연습에서는 동일한 데이터를 기반으로 하는 [조리개 꽃 데이터 집합](https://en.wikipedia.org/wiki/Iris_flower_data_set) 및 모델의 데이터를 저장 하는 SQL Server 데이터베이스를 만듭니다. Iri 데이터는 SQL Server에 의해 설치 되는 R 및 Python 배포 모두에 포함 되며, SQL Server machine learning 자습서에서 사용 됩니다. 

이 연습을 완료 하려면 T-sql 쿼리를 실행할 수 있는 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) 또는 다른 도구가 있어야 합니다.

이 데이터 집합을 사용 하는 자습서 및 빠른 시작에는 다음이 포함 됩니다.

+  [빠른 시작: SQL Server에서 저장 프로시저를 사용 하 여 Python 모델 만들기, 학습 및 사용](quickstart-python-train-score-in-tsql.md)

## <a name="create-the-database"></a>데이터베이스 만들기

1. SQL Server Management Studio를 시작 하 고 새 **쿼리** 창을 엽니다.  

2. 이 프로젝트에 대 한 새 데이터베이스를 만들고 새 데이터베이스를 사용 하도록 **쿼리** 창의 컨텍스트를 변경 합니다.

    ```sql
    CREATE DATABASE irissql
    GO
    USE irissql
    GO
    ```

    > [!TIP] 
    > SQL Server를 처음 사용 하거나 소유 하 고 있는 서버에서 작업 하는 경우 일반적으로 로그인 하 여 **master** 데이터베이스에 있는 것으로 표시 하지 않고 작업을 시작 합니다. 올바른 데이터베이스를 사용 하 고 있는지 확인할 수 있도록 항상 `USE <database name>` 문을 사용 하 여 컨텍스트를 지정 합니다 ( `use irissql`예:).

3. 빈 테이블을 추가 합니다. 하나는 데이터를 저장 하 고 다른 하나는 학습 된 모델을 저장 하는 테이블입니다. **Iris_models** 테이블은 다른 연습에서 생성 된 serialize 된 모델을 저장 하는 데 사용 됩니다.

    다음 코드는 학습 데이터에 대 한 테이블을 만듭니다.

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

    > [!TIP] 
    > T-sql을 처음 접하는 경우에는 `DROP...IF` 문을 기억으로 지불 합니다. 테이블을 만들려고 했지만 하나는 이미 있는 경우 SQL Server에서 오류를 반환 합니다. "데이터베이스에 이름이 ' iris_data ' 인 개체가 이미 있습니다." 이러한 오류를 방지 하는 한 가지 방법은 코드의 일부로 기존 테이블 또는 다른 개체를 삭제 하는 것입니다.

4. 다음 코드를 실행 하 여 학습 된 모델을 저장 하는 데 사용 되는 테이블을 만듭니다. SQL Server에 Python (또는 R) 모델을 저장 하려면 해당 모델을 serialize 하 여 **varbinary (max)** 형식의 열에 저장 해야 합니다. 

    ```sql
    DROP TABLE IF EXISTS iris_models;
    GO
    
    CREATE TABLE iris_models (
      model_name VARCHAR(50) NOT NULL DEFAULT('default model') PRIMARY KEY,
      model VARBINARY(MAX) NOT NULL
    );
    GO
    ```

    모델 내용 외에도 일반적으로 모델 이름, 학습 된 날짜, 원본 알고리즘 및 매개 변수, 원본 데이터 등의 기타 유용한 메타 데이터에 대 한 열도 추가 합니다. 지금은 간단 하 게 유지 하 고 모델 이름만 사용 합니다.

## <a name="populate-the-table"></a>테이블 채우기

R 또는 Python에서 기본 제공 되는 Iri 데이터를 가져올 수 있습니다. Python 또는 R을 사용 하 여 데이터를 데이터 프레임에 로드 한 다음 데이터베이스의 테이블에 삽입할 수 있습니다. 외부 세션의 학습 데이터를 SQL Server 테이블로 이동 하는 것은 다단계 프로세스입니다.

+ 원하는 데이터를 가져오는 저장 프로시저를 디자인 합니다.
+ 저장 프로시저를 실행 하 여 실제로 데이터를 가져옵니다.
+ 검색 된 데이터를 저장 해야 하는 위치를 지정 하는 INSERT 문을 생성 합니다.

1. Python이 통합 된 시스템에서 Python 코드를 사용 하 여 데이터를 로드 하는 다음 저장 프로시저를 만듭니다.

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

    이 코드를 실행 하면 "명령이 성공적으로 완료 되었습니다." 라는 메시지가 표시 됩니다. 이는 저장 프로시저가 사양에 따라 생성 되었다는 것을 의미 합니다.

2. 또는 R 통합을 수행 하는 시스템에서 R을 대신 사용 하는 프로시저를 만듭니다.

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

3. 실제로 테이블을 채우려면 저장 프로시저를 실행 하 고 데이터를 써야 하는 테이블을 지정 합니다. 이 저장 프로시저는 실행 될 때 기본 제공 된 Iri 데이터 집합을 로드 하는 Python 또는 R 코드를 실행 한 다음 **iris_data** 테이블에 데이터를 삽입 합니다.

    ```sql
    INSERT INTO iris_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species", "SpeciesId")
    EXEC dbo.get_iris_dataset;
    ```

    T-sql을 처음 접하는 경우 INSERT 문은 새 데이터만 추가 합니다. 기존 데이터를 확인 하거나 테이블을 삭제 하 고 다시 작성 하지 않습니다. 동일한 데이터의 여러 복사본이 테이블에 표시 되지 않도록 하려면 먼저 다음 `TRUNCATE TABLE iris_data`문을 실행 하면 됩니다. T-sql [TRUNCATE TABLE](https://docs.microsoft.com/sql/t-sql/statements/truncate-table-transact-sql) 문은 기존 데이터를 삭제 하지만 테이블 구조는 그대로 유지 합니다.

    > [!TIP]
    > 저장 프로시저를 나중에 수정 하려면 삭제 한 후 다시 만들 필요가 없습니다. [ALTER PROCEDURE](https://docs.microsoft.com/sql/t-sql/statements/alter-procedure-transact-sql) 문을 사용 합니다. 


## <a name="query-the-data"></a>데이터 쿼리

유효성 검사 단계로, 쿼리를 실행 하 여 데이터가 업로드 되었는지 확인 합니다.

1. 개체 탐색기의 데이터베이스에서 **irissql** 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 새 쿼리를 시작 합니다.

2. 몇 가지 간단한 쿼리를 실행 합니다.

    ```sql
    SELECT TOP(10) * FROM iris_data;
    SELECT COUNT(*) FROM iris_data;
    ```

## <a name="next-steps"></a>다음 단계

다음 빠른 시작에서 기계 학습 모델을 만들어 테이블에 저장 한 다음 모델을 사용 하 여 예측 된 결과를 생성 합니다.

+ [빠른 시작: SQL Server에서 저장 프로시저를 사용 하 여 Python 모델 만들기, 학습 및 사용](quickstart-python-train-score-in-tsql.md)
