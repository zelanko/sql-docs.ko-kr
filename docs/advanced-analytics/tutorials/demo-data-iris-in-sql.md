---
title: Python 및 R 자습서-SQL Server Machine Learning에 대 한 Iris 데모 데이터 집합
Description: Iris 데이터 집합 및 모델을 저장 하는 것에 대 한 테이블을 포함 하는 데이터베이스를 만듭니다. 이 데이터 집합은 SQL Server 저장 프로시저에서 R 언어 또는 Python 코드를 래핑하는 방법을 보여 주는 연습에 사용 됩니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/19/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 26358fea3b7d08d986a5078cf6484e7c4e0d3dd1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962110"
---
#  <a name="iris-demo-data-for-python-and-r-tutorials-in-sql-server"></a>SQL Server에서 Python 및 R 자습서 아이리스 데이터 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 연습에서는 데이터를 저장 하는 SQL Server 데이터베이스를 만들 합니다 [아이리스 꽃 데이터 집합](https://en.wikipedia.org/wiki/Iris_flower_data_set) 모델과 동일한 데이터를 기반으로 합니다. 아이리스 데이터는 SQL Server로 설치 하는 R 및 Python 배포판에 포함 되 고 SQL Server machine learning 자습서에 사용 됩니다. 

이 연습을 완료 하려면 있어야 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) 또는 T-SQL 쿼리를 실행할 수 있는 다른 도구입니다.

이 데이터 집합을 사용 하 여 퀵 스타트 및 자습서에는 다음과 같습니다.

+  [빠른 시작: 만들기, 학습 및 Python 모델을 사용 하 여 SQL Server에서 저장된 프로시저를 사용 하 여](quickstart-python-train-score-in-tsql.md)

## <a name="create-the-database"></a>데이터베이스 만들기

1. SQL Server Management Studio를 시작 하 고 새 **쿼리** 창입니다.  

2. 이 프로젝트에 새 데이터베이스를 만들고의 컨텍스트를 변경 하 **쿼리** 창에서 새 데이터베이스를 사용 합니다.

    ```sql
    CREATE DATABASE irissql
    GO
    USE irissql
    GO
    ```

    > [!TIP] 
    > SQL Server를 처음 사용 하거나 소유 하는 서버에서 작업 하는 경우 일반적인 실수를 로그인 하 고 있는 알아채지 않으면 서 작업을 시작 합니다 **마스터** 데이터베이스입니다. 올바른 데이터베이스를 사용 하 고 있는지를 항상 지정을 사용 하 여 컨텍스트를 `USE <database name>` 문 (예를 들어 `use irissql`).

3. 일부 빈 테이블을 추가 합니다: 데이터를 저장 하 고 학습 된 모델을 저장할 하나입니다. 합니다 **iris_models** 테이블을 다른 연습에서 생성 된 직렬화 된 모델을 저장 하는 데 사용 됩니다.

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
    > 기억해 야 비로소 T-SQL을 처음 접하는 경우는 `DROP...IF` 문입니다. 테이블을 만들려고 할 때 이미 SQL Server 오류를 반환 합니다. "이미 있기 'iris_data' 데이터베이스의 명명 된 개체입니다." 이러한 오류를 방지 하는 한 가지 방법은 코드의 일부로 모든 기존 테이블 또는 다른 개체를 삭제 하는 것입니다.

4. 학습된 된 모델을 저장 하는 데 사용 하는 테이블을 만들려면 다음 코드를 실행 합니다. SQL Server의 Python (또는 R) 모델을 저장 하려면 수 직렬화 하 고 되어야 형식의 열에 저장 **varbinary (max)** 합니다. 

    ```sql
    DROP TABLE IF EXISTS iris_models;
    GO
    
    CREATE TABLE iris_models (
      model_name VARCHAR(50) NOT NULL DEFAULT('default model') PRIMARY KEY,
      model VARBINARY(MAX) NOT NULL
    );
    GO
    ```

    모델 콘텐츠 외에도 일반적으로 모델의 이름과 같은 학습 된 날짜 원본 알고리즘 및 매개 변수를 원본 데이터를 기타 유용한 메타 데이터 열을 추가 하는 등입니다. 지금은에서는 간단 하 게 유지 하 고 모델 이름만 사용 합니다.

## <a name="populate-the-table"></a>테이블을 채웁니다

R 또는 Python에서 기본 제공 아이리스 데이터를 가져올 수 있습니다. Python 또는 R 데이터 프레임에 데이터 로드를 사용 하 여 수 있으며 그런 다음 데이터베이스의 테이블에 삽입할 수 있습니다. 외부 세션에서 학습 데이터를 이동 하는 SQL Server 테이블에는 다단계 프로세스입니다.

+ 원하는 데이터를 가져오는 저장된 프로시저를 디자인 합니다.
+ 실제로 데이터를 가져오는 저장된 프로시저를 실행 합니다.
+ 검색된 된 데이터를 저장할 위치를 지정 하는 INSERT 문을 생성 합니다.

1. Python 통합을 사용 하 여 시스템에서 Python 코드를 사용 하 여 데이터를 로드 하는 다음 저장된 프로시저를 만듭니다.

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

    이 코드를 실행 하는 경우는 메시지가 표시 "명령을 완료 했습니다." 모든이 즉 사양에 따라 저장된 프로시저가 만들어진 것입니다.

2. 또는 R 통합 시스템을에서 R을 대신 사용 하는 프로시저를 만듭니다.

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

3. 테이블에 실제로 채우기 위해 저장된 프로시저를 실행 하 고 테이블 데이터를 쓸 위치를 지정 합니다. 저장된 프로시저가 실행은 기본 제공 Iris 데이터 집합을 로드 하 고 다음에 데이터를 삽입 하는 Python 또는 R 코드를 실행 합니다 **iris_data** 테이블입니다.

    ```sql
    INSERT INTO iris_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species", "SpeciesId")
    EXEC dbo.get_iris_dataset;
    ```

    T-SQL을 처음 접하는 경우 주의 INSERT 문의만 새 데이터 추가 않습니다 기존 데이터를 확인 또는 삭제 하 고 테이블을 다시 작성 합니다. 테이블의 동일한 데이터의 여러 복사본을 가져오는 것을 방지 하려면이 문을 실행할 수 있습니다이 먼저: `TRUNCATE TABLE iris_data`합니다. T-SQL [TRUNCATE TABLE](https://docs.microsoft.com/sql/t-sql/statements/truncate-table-transact-sql) 문은 기존 데이터를 삭제 하지만 테이블의 구조를 그대로 유지 합니다.

    > [!TIP]
    > 저장된 프로시저를 수정 하려면 나중에 필요가 없습니다를 삭제 하 고 다시 만듭니다. 사용 된 [ALTER PROCEDURE](https://docs.microsoft.com/sql/t-sql/statements/alter-procedure-transact-sql) 문입니다. 


## <a name="query-the-data"></a>데이터를 쿼리 합니다.

유효성 검사 단계로, 데이터가 업로드 되었는지 확인 하는 쿼리를 실행 합니다.

1. 개체 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭 합니다 **irissql** 데이터베이스 및 새 쿼리를 시작 합니다.

2. 몇 가지 간단한 쿼리를 실행 합니다.

    ```sql
    SELECT TOP(10) * FROM iris_data;
    SELECT COUNT(*) FROM iris_data;
    ```

## <a name="next-steps"></a>다음 단계

다음 빠른 시작에서 기계 학습 모델 및 테이블에 저장 만들고 모델을 사용 하 여 예측된 결과 생성 합니다.

+ [빠른 시작: 만들기, 학습 및 Python 모델을 사용 하 여 SQL Server에서 저장된 프로시저를 사용 하 여](quickstart-python-train-score-in-tsql.md)
