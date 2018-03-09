---
title: "저장된 프로시저에서 Python 코드를 줄 바꿈 | Microsoft Docs"
titleSuffix: SQL Server
ms.custom: 
ms.date: 02/28/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2017
dev_langs:
- Python
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 11b5b649a942b1d1804b799426530a1b82ee9458
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2018
---
# <a name="wrap-python-code-in-a-stored-procedure"></a>저장된 프로시저에서 Python 코드를 래핑하십시오.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

에 [이전 단원](run-python-using-t-sql.md), SQL Server에 설명 하는 Python을 확인 하는 방법을 배웠습니다. 이 단원에서는 Python 샘플 데이터 집합에서 데이터를 가져오고 SQL Server 테이블에 해당 데이터를 기록 하려면 저장된 프로시저에서 Python 코드를 포함 하는 방법에 설명 합니다.

시스템 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) Python으로 SQL 변수 및 SQL 데이터 집합을 전달 하는 래퍼를 제공 합니다. 또한 Python 하 여 결과 출력을 처리 하 고 전달 SQL Server 형식으로 SQL 데이터 형식과 호환 합니다.

이 수식이 어떻게 살펴보겠습니다.

## <a name="prepare-the-database-and-tables"></a>준비 데이터베이스 및 테이블

원격 클라이언트를 설정 하는 시나리오를 단순화 하기 위해 Visual Studio Code, Visual Studio, PyCharm, 또는 다른 도구를 사용 하 여 Python 코드를 실행할 수 있지만이 단원에서는 모든 코드는 저장된 프로시저의 일부로 실행 해야 합니다.

1. SQL Server Management Studio를 시작 하 고 새 **쿼리** 창.  

2. 이 프로젝트에 대 한 새 데이터베이스를 만들고의 컨텍스트를 변경 하면 **쿼리** 창에서 새 데이터베이스를 사용 합니다.

    ```sql
    CREATE DATABASE sqlpy;
    GO;
    USE sqlpy;
    GO;
    ```

    > [!TIP] 
    > 로그인에 있는 검색 하지 않고 작업을 시작 하는 일반적인 실수는 SQL Server를 처음 사용 하는 소유 하는 서버에서 작업 하는 경우는 **마스터** 데이터베이스입니다. 올바른 데이터베이스를 사용 하 고 있는지를 항상 지정을 사용 하 여 컨텍스트는 `USE <database name>` 문.

3. 일부 빈 테이블 추가: 데이터를 저장할 한 학습을 수행 하는 모델을 저장할 수 있습니다. 나중에 Python을 사용 하는 테이블을 채웁니다.

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

    T-SQL을 처음 접하는 경우 지불 하는 것 외우는 `DROP...IF` 문. SQL Server는 오류를 반환 하 고 있는 테이블을 만들려고 시도 하는 경우: "이미입니다. 데이터베이스에 ' iris_data' 라는 개체." 이러한 오류를 방지 하기 위해 가지 방법은 코드의 일환으로 기존 테이블 또는 다른 개체를 삭제 하는 것입니다.

4. 학습된 된 모델을 저장 하는 데 사용 되는 테이블을 만들려면 다음 코드를 실행 합니다. SQL Server에서 Python (또는 R) 모델을 저장 하려면 수 직렬화 하 고 되어야 형식의 열에 저장 된 **varbinary (max)**합니다. 

    ```sql
    DROP TABLE IF EXISTS iris_models;
    GO
    
    CREATE TABLE iris_models (
      model_name VARCHAR(50) NOT NULL DEFAULT('default model') PRIMARY KEY,
      model VARBINARY(MAX) NOT NULL
    );
    GO
    ```

    모델 콘텐츠 외에도 일반적으로 모델의 이름과 같이 학습 하는 날짜 소스 알고리즘 및 매개 변수를 원본 데이터를 다른 유용한 메타 데이터에 대 한 열을 추가 하는 식으로 계속 합니다. 지금은 단순하게 유지 알아보고 모델 이름만 사용 하겠습니다.

## <a name="populate-the-table"></a>테이블을 채웁니다

SQL Server에 Python에서 학습 데이터를 이동 하려면 작업 테이블은 다단계 프로세스:

+ 원하는 데이터를 가져오는 저장된 프로시저를 디자인 합니다.
+ 실제로 데이터를 가져오는 데 저장된 프로시저를 실행 합니다.
+ INSERT 문을 사용 하 여 검색된 된 데이터를 저장할 위치를 지정 합니다.

1. Python 코드를 포함 하는 다음 저장된 프로시저를 만듭니다. 

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

    이 코드를 실행 하면 해야 하면 메시지가 "명령이 완료 되었습니다." 이 따라서 모든 사용자가 지정한 대로 저장된 프로시저가 만들어진 것입니다.

2. 실제로 테이블을 구성을 하려면 저장된 프로시저를 실행 하 고는 데이터를 쓸 테이블을 지정 합니다. 실행 되는 경우 저장된 프로시저는 기본 제공 된 Python 샘플 데이터에서 Iris 데이터 집합을 로드 하는 Python 코드를 실행 합니다.

    ```sql
    INSERT INTO iris_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species", "SpeciesId")
    EXEC dbo.get_iris_dataset;
    ```

    T-SQL을 처음 접하는 경우 INSERT 문은 새 데이터를 추가 하는 주의 해야 않습니다 기존 데이터에 대 한 확인 또는 삭제 하 고 테이블을 다시 작성 합니다. 테이블의 동일한 데이터의 여러 복사본을 가져오는 것을 방지 하려면이 문을 실행할 수 있습니다이 먼저: `TRUNCATE TABLE iris_data`합니다. T-SQL [TRUNCATE TABLE](https://docs.microsoft.com/sql/t-sql/statements/truncate-table-transact-sql) 문은 기존 데이터를 삭제 하지만 테이블의 구조를 그대로 유지 합니다.

    > [!TIP]
    > 저장된 프로시저를 수정 하려면 나중 필요가 없습니다 삭제 하 고 다시 만듭니다. 사용 하 여 [ALTER PROCEDURE](https://docs.microsoft.com/sql/t-sql/statements/alter-procedure-transact-sql) 문. 

3. 데이터가 올바르게 로드 되었음을 확인 하려면 몇 가지 간단한 쿼리를 실행할 수 있습니다.

    ```sql
    SELECT TOP(10) * FROM iris_data;
    SELECT COUNT(*) FROM iris_data;
    ```

에 [다음 단원](../tutorials/train-score-using-python-in-tsql.md), 기계 학습 모델을 만들고 테이블에 저장 합니다.

### <a name="further-reading-about-stored-procedures"></a>저장된 프로시저에 대 한 추가 정보

SQL Server을 처음 접하는 경우 처음에 복잡 한 저장된 프로시저를 확인할 수 있습니다. 하지만 저장된 프로시저는 응용 프로그램 및 서버 간에 데이터를 전달 하기 위한 강력 하 고 유연한 인터페이스. 저장된 프로시저를 사용 하 여 동적으로 정의한 입력을 손쉽게 전달할 새 모델 이름, 새 매개 변수 및 새 데이터에서 Python 코드를 변경 하지 않고.

어떻게 저장된 프로시저 작업의 개요를 참조 하십시오. [저장 프로시저 (데이터베이스 엔진)](https://docs.microsoft.com/sql/relational-databases/stored-procedures/stored-procedures-database-engine), 또는이 자습서: [쓰기 TRANSACT-SQL 문을](https://docs.microsoft.com/sql/t-sql/tutorial-writing-transact-sql-statements)합니다.

또한 몇 가지 좋은 자습서에 있는 커뮤니티 사이트와 같은 [SQL Server Central](http://www.sqlservercentral.com/) 또는 [SQL 팀](http://www.sqlteam.com/)합니다.

T-SQL에서 Python 코드 가장 캡슐화 수는 방법을 생각해도 고려해 야 이러한 기능을 사용 하 여:

+ 저장된 프로시저에 대 한 기본값을 정의합니다.
+ OUTPUT 키워드를 사용 하 여 입력된 변수를 통과할 수
+ 적절 한 데이터 형식 및 열 이름을 포함 된 결과 사용 하 여 응용 프로그램에서 사용할 데이터를 보냈음을 확인 하는 스키마 정의 만들기
+ 일괄 처리를 개선 하는 힌트를 제공 합니다.
+ EXECUTE AS를 사용 하 여 코드를 테스트 하려면 다른 사용자를 가장 절

## <a name="next-lesson"></a>다음 단원

[Python 모델을 학습 하 고 SQL Server의 점수를 생성 합니다.](../tutorials/train-score-using-python-in-tsql.md)