---
title: "Azure SQL 데이터베이스에서 R을 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 12/08/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0a90c438-d78b-47be-ac05-479de64378b2
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 8960f8a8c5dadaa0c53cd4fcb1ab786ce6e720a7
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/02/2018
---
# <a name="using-r-in-azure-sql-database"></a>Azure SQL 데이터베이스에서 R을 사용 하 여

2017 년 1 월에서에서 SQL Server 개발 팀은 R 코드에서-데이터베이스의 SQL Server 2016에서 R 서비스와 비슷한 저장된 프로시저를 사용 하 여 실행을 지원 하려면 계획을 발표 했습니다. 

최신 공개 릴리스 일정 및 예정 된 이벤트를 유지 하려면 참조는 [SQL Server 블로그](https://blogs.technet.microsoft.com/dataplatforminsider/) 또는 [Microsoft R Server 블로그](https://blogs.msdn.microsoft.com/rserver/)합니다.

> [!IMPORTANT]
> 현재, R 지원의 미리 보기는 중앙 미국 서 부의에서 Azure SQL 데이터베이스에서 사용할 수 있는 전용 및 R에 대 한 기능에 비해 제한 된 기능을와 Python 코드에서 SQL Server 2016 또는 2017 실행 합니다.

## <a name="whats-included"></a>포함 된 내용

다음 데이터베이스 서비스 계층 및 성능 수준에서 데이터베이스에 R 기능을 사용할 수 있습니다.
 
- Premium 서비스 계층 – P1, P2, P4, P6, P11, P15
- 프리미엄 RS 서비스 계층 – PRS1, PRS2, PRS4, PRS6
- 프리미엄 탄력적 풀 – 125 Edtu 이상
- 프리미엄 RS 탄력적인 풀 – 125 Edtu 이상

미리 보기 버전에 이러한 패키지에 포함 됩니다.

+   Microsoft R Open r 3.3.3 버전
+   이미 설치 되어 R 기본 패키지 및 함수
+   Microsoft R Server 9.2, RevoScaleR 패키지를 포함 하 여

현재 미리 보기 릴리스에서 다음과 같은 작업을 수행할 수 있습니다.

+ 메모리 내에 포함 된 모든 데이터를 사용 하 여 모델의 학습
+   메모리 내에 포함 된 모든 데이터를 사용 하 여 모델의 점수 매기기
+   R 스크립트 실행에 대 한 간단한 병렬 처리 (사용 하 여 @parallel sp_execute_external_script에서 매개 변수)
+   R 스크립트 실행에 대 한 실행 스트리밍 (사용 하 여 @r_RowsPerRead sp_execute_external_script에서 매개 변수)
+   한 번에 하나의 R 스크립트 실행


Azure SQL 데이터베이스에는 R의 미리 보기 릴리스에서 다음 작업 지원 되지 않습니다.

+ 특정 데이터베이스에서 R 스크립트 실행을 사용할 수 없습니다.
+ CPU 모니터에 제공 되는 Dmv 및 R 스크립트의 메모리 사용량 사용할 수 없습니다.
+ 타사 패키지를 설치할 수 있습니다. 외부 라이브러리 만들기 문이 지원 되지 않습니다.

## <a name="example"></a>예제

Azure SQL DB 모든 R 명령이 실행 되어 T-SQL에서 저장된 프로시저를 사용 하 여 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)합니다. 

다음 예제에서는 기본 오른쪽에 포함 된 iris 데이터 집합을 사용 하 여 미리 보기 기능을 미리 사용해 방법을 보여 줍니다.

### <a name="step-1-create-the-data-tables"></a>1단계. 데이터 테이블 만들기

두 테이블을 만들어 시작: R에서 추출 된 원본 데이터를 저장 하 고 학습된 된 모델을 저장 하기 위한 하나 있습니다.

```sql
DROP TABLE IF EXISTS iris_data, iris_models;
GO
CREATE TABLE iris_data (
        id INT NOT NULL IDENTITY PRIMARY KEY
        , "Sepal.Length" FLOAT NOT NULL, "Sepal.Width" FLOAT NOT NULL
        , "Petal.Length" FLOAT NOT NULL, "Petal.Width" FLOAT NOT NULL
        , "Species" VARCHAR(100) NULL
);
CREATE TABLE iris_models (
    model_name VARCHAR(30) NOT NULL PRIMARY KEY,
    model VARBINARY(max) NOT NULL,
    native_model VARBINARY(MAX) NOT NULL
);
GO
```

### <a name="step-2-populate-table-with-data-from-the-iris-dataset"></a>2단계. Iris 데이터 집합의 데이터로 테이블 채우기

테이블을 만든 후 테이블에 학습 데이터를 삽입 하려면 다음 코드를 실행 합니다. 저장된 프로시저 sp_execute_external_script R을 호출 하 고 INSERT INTO 문을에 지정 된 스키마를 사용 하 여 데이터 프레임으로 iris 데이터 집합을 반환 합니다.

```sql
INSERT INTO iris_data
("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species")
EXEC sp_execute_external_script @language = N'R'
  , @script = N'iris_data <- iris;'
  , @input_data_1 = N''
  , @output_data_1_name = N'iris_data';
GO
```

### <a name="step-3-create-the-stored-procedure-that-generates-the-model"></a>3단계. 모델을 생성 하는 저장된 프로시저 만들기

다음 저장된 프로시저는 실제로 만들고 이진 두 형식 중 하나로 저장 될 수 있는 모델을 학습 작업을 수행 합니다.

```sql
CREATE PROCEDURE generate_iris_model
    @trained_model VARBINARY(MAX) OUTPUT, 
    @native_trained_model VARBINARY(MAX) OUTPUT
AS
BEGIN
  EXEC sp_execute_external_script @language = N'R'
  , @script = N'
    iris_model <- rxDTree(Species ~ Sepal.Length + Sepal.Width + Petal.Length + Petal.Width, data = iris_rx_data);
    trained_model <- as.raw(serialize(iris_model, connection=NULL));
    native_trained_model <- rxSerializeModel(iris_model, realtimeScoringOnly = TRUE)
    '
  , @input_data_1 = N'SELECT "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" FROM iris_data'
  , @input_data_1_name = N'iris_rx_data'
  , @params = N'@trained_model VARBINARY(MAX) OUTPUT, @native_trained_model VARBINARY(MAX) OUTPUT
    , @trained_model = @trained_model OUTPUT
    , @native_trained_model = @native_trained_model OUTPUT;
End
```

+ **출력** 값을 통과 하 고도 출력에 사용 되는 키워드의 입력된 매개 변수를 나타냅니다.
+ 로 시작 하는 줄 `iris_model` 종 꽃 특성을 기반으로 예측에 의사 결정 트리 모델을 정의 합니다.
+ 에 대 한 호출 `serialize` 저장소 SQL Server에 대 한 적합 한 모델을 이진 형식에서으로 저장 합니다. 
+ 또한, RevoScaleR 알고리즘을 기반으로 모델을 사용할 수 있습니다는 [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) 새로운 네이티브 이진 형식으로 모델을 저장 하는 함수입니다. SQL Server에서 PREDICT 함수 점수 매기기에 대 한이 형식으로 저장 하는 모델을 로드할 수 있습니다.

### <a name="step-4-train-and-save-the-model"></a>4단계. 학습 및 모델 저장

저장된 프로시저를 만든 호출 하면 입력된 데이터를 처리 하 고 모델을 만듭니다. 다음 코드는 테이블에는 모델 저장 **iris_models**꽃 종 예측할 나중에 사용할 수 있도록 합니다.

```sql
DECLARE @model VARBINARY(MAX), @native_modelVARBINARY(MAX);
EXEC generate_iris_model @model OUTPUT, @native_model OUTPUT;
DELETE FROM iris_models WHERE model_name = 'iris.dtree';
INSERT INTO iris_models (model_name, model, native_model) VALUES('iris.dtree', @model, @native_model);
SELECT model_name, datalength(model)/1024. AS model_size_kb, datalength(native_model)/1024. AS native_model_size_kb FROM iris_models;
GO
```

### <a name="step-5-create-a-stored-procedure-for-scoring"></a>5단계. 점수 매기기에 대 한 저장된 프로시저 만들기

다음으로 점수를 매기기 위해는 저장된 프로시저를 만듭니다. 이 저장된 프로시저는 테이블에서 지정된 된 모델을 로드 하 고 입력된 데이터를 기반으로 하는 점수를 작성 합니다.

```sql
CREATE PROCEDURE predict_iris_species (@model varchar(100))
AS
BEGIN
  DECLARE @rx_model VARBINARY(MAX) = (SELECT model FROM iris_models WHERE model_name = @model);
  EXEC sp_execute_external_script @language = N'R'
  , @script = N'
    irismodel<-unserialize(rx_model);
    OutputDataSet <-rxPredict(irismodel, iris_rx_data, extraVarsToWrite = c("Species", "id"));
      '
  , @input_data_1 = N'SELECT "id", "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" FROM iris_data'
  , @input_data_1_name = N'iris_rx_data'
  , @params = N'@rx_model varbinary(max)'
  , @rx_model = @rx_model
  WITH RESULT SETS ( ("setosa_Pred" FLOAT, "versicolor_Pred" FLOAT, "virginica_Pred" FLOAT, "Species.Actual" VARCHAR(100), "id" INT));
END;
GO
```

이 저장 프로시저는 [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) 함수가 있지만 있습니다 사용할 수도 네이티브 PREDICT 함수 T-SQL에서 표시 된 것 처럼 [여기](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/09/25/announcing-general-availability-of-native-scoring-using-predict-function-in-azure-sql-database/)합니다. 예측 함수의 사용을 사용 해야 하는 [ **rx** 모델](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-revoscaler) 사용 하 여 모델을 저장 하 고 [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)합니다.

### <a name="step-6-use-the-stored-procedure-to-generate-predictions"></a>6단계. 저장된 프로시저를 사용 하 여 예측을 생성 하려면

모델에서 점수를 생성 하려면 저장된 프로시저를 실행 합니다. 테이블에 값을 삽입 하거나 호출 응용 프로그램으로는 예측을 반환 합니다.

```sql
EXEC predict_iris_species 'iris.dtree';
GO
```

## <a name="related-resources"></a>관련 리소스

Azure 마켓플레이스는 또한 SQL Server 2017을 포함 하는 여러 가상 컴퓨터를 제공 합니다.

+ [Azure 기계 학습에 대 한 가상 컴퓨터를 프로 비전](provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)

또한 다양 한 도구를 학습 하는 인기 있는 컴퓨터와 미리 구성 된 상태로 이러한 Vm을 확인해 보세요.

+ [데이터 과학 가상 컴퓨터](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/overview)
+ [심층 학습 가상 컴퓨터](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/deep-learning-dsvm-overview)

