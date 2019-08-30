---
title: R을 사용하여 SSIS 및 SSRS 워크플로 만들기
description: SQL Server Machine Learning Services 및 R Services, Reporting Services (SSRS) 및 SQL Server Integration Services (SSIS)를 결합 하는 통합 시나리오.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/17/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2b8d55e95991437e4d76911fd26afb5b1bc9c550
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715168"
---
# <a name="create-ssis-and-ssrs-workflows-with-r-on-sql-server"></a>SQL Server에서 R을 사용 하 여 SSIS 및 SSRS 워크플로 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 SQL Server SQL Server Machine Learning Services의 언어 및 데이터 과학 기능을 사용 하 여 포함 된 R 및 Python 스크립트를 사용 하는 방법을 설명 합니다. SQL Server Integration Services (SSIS) 및 SQL Server Reporting Services SSRS. SQL Server의 R 및 Python 라이브러리는 통계 및 예측 함수를 제공 합니다. SSIS 및 SSRS는 각각 조정 ETL 변환과 시각화를 제공 합니다. 이 문서에서는 이러한 모든 기능을이 워크플로 패턴에 함께 포함 하는 방법을 설명 합니다.

> [!div class="checklist"]
> * R 또는 Python 실행 파일을 포함 하는 저장 프로시저 만들기
> * SSIS 또는 SSRS에서 저장 프로시저 실행

이 문서의 예제는 대부분 R 및 SSIS에 대 한 것 이지만, 개념과 단계는 Python에 동일 하 게 적용 됩니다. 두 번째 섹션에서는 SSRS 시각화에 대 한 지침과 링크를 제공 합니다.

<a name="bkmk_ssis"></a> 

## <a name="use-ssis-for-automation"></a>Automation에 SSIS 사용

데이터 과학 워크플로는 반복이 매우 빈번하며, 크기 조정, 집계, 확률 계산, 특성 병합 및 이름 변경을 비롯한 데이터 변환이 많이 이루어집니다. 데이터 과학자는 R, Python 또는 기타 언어로 이러한 작업을 대부분 수행하지만 엔터프라이즈 데이터로 이러한 워크플로를 실행하려면 ETL 도구 및 프로세스와의 원활한 통합이 필요합니다.

에서는 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] transact-sql 및 저장 프로시저를 통해 R에서 복잡 한 작업을 실행할 수 있으므로 데이터 과학 작업을 기존 ETL 프로세스와 통합할 수 있습니다. 메모리를 많이 사용 하는 작업의 체인을 수행 하는 대신 및 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)]를 비롯 하 여 가장 효율적인 도구를 사용 하 여 데이터 준비를 최적화할 수 있습니다. 

다음은를 사용 하 여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]데이터 처리 및 모델링 파이프라인을 자동화할 수 있는 방법에 대 한 몇 가지 아이디어입니다.

+ 온-프레미스 또는 클라우드 소스에서 데이터를 추출 하 여 학습 데이터 빌드 
+ 데이터 통합 워크플로의 일부로 R 또는 Python 모델 빌드 및 실행
+ 정기적으로 (예약 된) 모델 다시 학습
+ R 또는 Python 스크립트에서 Excel, Power BI, Oracle, Teradata 등의 다른 대상으로 결과를 로드 하 여
+ SSIS 작업을 사용 하 여 SQL database에 데이터 기능 만들기
+ 조건부 분기를 사용 하 여 R 및 Python 작업에 대 한 계산 컨텍스트 전환

## <a name="ssis-example"></a>SSIS 예제

다음 예제는이 URL에서 Jimmy Wong에 의해 작성 된 현재 사용 중지 된 MSDN 블로그 게시물에서 시작 됩니다.`https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/`

이 예에서는 SSIS를 사용 하 여 작업을 자동화 하는 방법을 보여 줍니다. SQL Server Management Studio를 사용 하 여 포함 된 R을 사용 하 여 저장 프로시저를 만든 후 SSIS 패키지의 [T-sql 실행 태스크](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) 에서 해당 저장 프로시저를 실행 합니다.

이 예를 단계별로 실행 하려면 Management Studio, SSIS, SSIS 디자이너, 패키지 디자인 및 T-sql에 대해 잘 알고 있어야 합니다. SSIS 패키지는 학습 데이터를 테이블에 삽입 하 고, 데이터를 모델링 하 고, 데이터 점수를 매기는 세 개의 [T-sql 실행 태스크](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) 를 사용 하 여 예측 출력을 가져옵니다.

### <a name="load-training-data"></a>학습 데이터 로드

SQL Server Management Studio에서 다음 스크립트를 실행 하 여 데이터를 저장 하는 테이블을 만듭니다. 이 연습에서는 테스트 데이터베이스를 만들어 사용 해야 합니다. 

```T-SQL
Use test-db
GO

Create table ssis_iris (
    id int not null identity primary key
    , "Sepal.Length" float not null, "Sepal.Width" float not null
    , "Petal.Length" float not null, "Petal.Width" float not null
    , "Species" varchar(100) null
);
GO
```

데이터 프레임에 학습 데이터를 로드 하는 저장 프로시저를 만듭니다. 이 예에서는 기본 제공 되는 Iri 데이터 집합을 사용 합니다. 

```T-SQL
Create procedure load_iris
as
begin
    execute sp_execute_external_script
        @language = N'R'
        , @script = N'iris_df <- iris;'
        , @input_data_1 = N''
        , @output_data_1_name = N'iris_df'
    with result sets (("Sepal.Length" float not null, "Sepal.Width" float not null, "Petal.Length" float not null, "Petal.Width" float not null, "Species" varchar(100)));
end;
```

SSIS 디자이너에서 방금 정의한 저장 프로시저를 실행 하는 [SQL 실행 태스크](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task) 를 만듭니다. **SQLStatement** 에 대 한 스크립트는 기존 데이터를 제거 하 고 삽입할 데이터를 지정한 다음 저장 프로시저를 호출 하 여 데이터를 제공 합니다.

```T-SQL
truncate table ssis_iris;
insert into ssis_iris("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species")
exec dbo.load_iris;
```

![데이터 삽입] (../media/create-workflows-using-r-in-sql-server/ssis-exec-sql-insert-data.png "데이터 삽입")

### <a name="generate-a-model"></a>모델 생성

SQL Server Management Studio에서 다음 스크립트를 실행 하 여 모델을 저장 하는 테이블을 만듭니다. 

```T-SQL
Use test-db
GO

Create table ssis_iris_models (
    model_name varchar(30) not null default('default model') primary key,
    model varbinary(max) not null
);
GO
```

[RxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)를 사용 하 여 선형 모델을 생성 하는 저장 프로시저를 만듭니다. RevoScaleR 및 revoscalepy 라이브러리는 SQL Server의 R 및 Python 세션에서 자동으로 사용할 수 있으므로 라이브러리를 가져올 필요가 없습니다.

```T-SQL
Create procedure generate_iris_rx_model
as
begin
    execute sp_execute_external_script
        @language = N'R'
        , @script = N'
          irisLinMod <- rxLinMod(Sepal.Length ~ Sepal.Width + Petal.Length + Petal.Width + Species, data = ssis_iris);
          trained_model <- data.frame(payload = as.raw(serialize(irisLinMod, connection=NULL)));'
        , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" from ssis_iris'
        , @input_data_1_name = N'ssis_iris'
        , @output_data_1_name = N'trained_model'
    with result sets ((model varbinary(max)));
end;
GO
```

SSIS 디자이너에서 **generate_iris_rx_model** 저장 프로시저를 실행 하는 [SQL 실행 태스크](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task) 를 만듭니다. 모델이 직렬화 되 고 ssis_iris_models 테이블에 저장 됩니다. **SQLStatement** 에 대 한 스크립트는 다음과 같습니다.

```T-SQL
insert into ssis_iris_models (model)
exec generate_iris_rx_model;
update ssis_iris_models set model_name = 'rxLinMod' where model_name = 'default model';
```

![선형 모델을 생성 합니다](../media/create-workflows-using-r-in-sql-server/ssis-exec-rxlinmod.png "선형 모델을 생성 합니다") .

검사점으로이 작업이 완료 되 면 ssis_iris_models를 쿼리하여 이진 모델이 하나 포함 되어 있는지 확인할 수 있습니다.

### <a name="predict-score-outcomes-using-the-trained-model"></a>"학습 된" 모델을 사용 하 여 결과 예측 (점수)

이제 학습 데이터를 로드 하 고 모델을 생성 하는 코드가 있으므로 남은 단계는 예측을 생성 하는 모델을 사용 하는 것입니다. 

이렇게 하려면 SQL 쿼리에 R 스크립트를 배치 하 여 ssis_iris_model에서 [Rxpredict](https://docs.microsoft.com//machine-learning-server/r-reference/revoscaler/rxpredict) 기본 제공 r 함수를 트리거합니다. **Predict_species_length** 라는 저장 프로시저는이 작업을 수행 합니다.

```T-SQL
Create procedure predict_species_length (@model varchar(100))
as
begin
    declare @rx_model varbinary(max) = (select model from ssis_iris_models where model_name = @model);
    -- Predict based on the specified model:
    exec sp_execute_external_script
        @language = N'R'
        , @script = N'
irismodel <-unserialize(rx_model);
irispred <- rxPredict(irismodel, ssis_iris[,2:6]);
OutputDataSet <- cbind(ssis_iris[1], irispred$Sepal.Length_Pred, ssis_iris[2]);
colnames(OutputDataSet) <- c("id", "Sepal.Length.Actual", "Sepal.Length.Expected");
#OutputDataSet <- subset(OutputDataSet, Species.Length.Actual != Species.Expected);
'
    , @input_data_1 = N'
    select id, "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" from ssis_iris
    '
    , @input_data_1_name = N'ssis_iris'
    , @params = N'@rx_model varbinary(max)'
    , @rx_model = @rx_model
    with result sets ( ("id" int, "Species.Length.Actual" float, "Species.Length.Expected" float)
        );
end;
```

SSIS 디자이너에서 **predict_species_length** 저장 프로시저를 실행 하 여 예측 꽃잎 길이를 생성 하는 [SQL 실행 태스크](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task) 를 만듭니다.

```T-SQL
exec predict_species_length 'rxLinMod';
```

![예측 생성] (../media/create-workflows-using-r-in-sql-server/ssis-exec-predictions.png "예측 생성")

### <a name="run-the-solution"></a>솔루션 실행

SSIS 디자이너에서 F5 키를 눌러 패키지를 실행 합니다. 다음 스크린샷에서 유사한 결과가 표시 됩니다.

![디버그 모드에서 실행 하는 F5 키](../media/create-workflows-using-r-in-sql-server/ssis-exec-F5-run.png "디버그 모드에서 실행 하는 F5 키")

<a name="bkmk_ssrs"></a> 

## <a name="use-ssrs-for-visualizations"></a>시각화에 SSRS 사용

R은 차트와 흥미로운 시각화를 만들 수 있지만 외부 데이터 원본과 잘 통합 되지 않으므로 각 차트 또는 그래프를 개별적으로 생성 해야 합니다. 공유도 어려울 수 있습니다.

를 사용 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]하면 저장 프로시저를 통해 [!INCLUDE[tsql](../../includes/tsql-md.md)] R에서 복잡 한 작업을 실행할 수 있습니다 .이는 및 Power BI을 비롯 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 한 다양 한 엔터프라이즈 보고 도구에서 쉽게 사용할 수 있습니다.

### <a name="ssrs-example"></a>SSRS 예

[Microsoft Reporting Services(SSRS)용 R 그래픽 장치](https://rgraphicsdevice.codeplex.com/)

이 CodePlex 프로젝트는 R의 그래픽 출력을 보고서에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 사용할 수 있는 이미지로 렌더링 하는 사용자 지정 보고서 항목을 만드는 데 도움이 되는 코드를 제공 합니다.  사용자 지정 보고서 항목을 사용하여 다음을 수행할 수 있습니다.

+ R 그래픽 디바이스를 사용하여 만든 차트 및 그림을 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 대시보드에 게시

+ [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 매개 변수를 R 그림에 전달

> [!NOTE]
> 이 샘플에서는 Reporting Services에 대 한 R 그래픽 장치를 지 원하는 코드를 Visual Studio 뿐만 아니라 Reporting Services 서버에 설치 해야 합니다. 수동 컴파일 및 구성도 필요합니다.

## <a name="next-steps"></a>다음 단계

이 문서의 SSIS 및 SSRS 예제에서는 포함 된 R 또는 Python 스크립트를 포함 하는 저장 프로시저를 실행 하는 두 가지 사례를 보여 줍니다. 키 요점은 저장 프로시저에 실행 요청을 보낼 수 있는 모든 응용 프로그램이 나 도구에서 R 또는 Python 스크립트를 사용할 수 있도록 할 수 있습니다. SSIS에 대 한 추가 요점은은 작업 체인에 포함 된 R 또는 Python 데이터 과학 기능을 사용 하 여 데이터 취득, 정리, 조작 등의 광범위 한 작업을 자동화 하 고 예약 하는 패키지를 만들 수 있다는 것입니다. 자세한 내용 및 아이디어는 [SQL Server Machine Learning Services에서 저장 프로시저를 사용 하 여 운영 R 코드](operationalizing-your-r-code.md)를 참조 하세요.