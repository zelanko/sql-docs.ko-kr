---
title: R-SQL Server Machine Learning Services를 사용 하 여 SSIS 및 SSRS 워크플로 만들기
description: 통합 시나리오를 SQL Server Machine Learning Services 및 R Services, Reporting Services (SSRS) 및 SQL Server Integration Services (SSIS)를 결합 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/15/2019
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 76ddf3e3fdb43fea6bb8fd224f8199cda4134b64
ms.sourcegitcommit: e9fcd10c7eb87a4f09ac2d8f7647018e83a5f5c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/14/2019
ms.locfileid: "57976303"
---
# <a name="create-ssis-and-ssrs-workflows-with-r-on-sql-server"></a>SQL Server에서 R을 사용 하 여 SSIS 및 SSRS 워크플로 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 Microsoft R 라이브러리에서 데이터 과학 기능은 관계형 데이터를 결합 하는 방식으로 두 가지 중요 한 SQL Server 기능, SQL Server Integration Services (SSIS), 및 SQL Server Reporting Services SSRS에서 저장된 프로시저를 사용 하는 방법 설명 및 조정 된 데이터 변환 및 시각화에 대 한 BI 기능을 추가 합니다. 기능에 알아봅니다 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 자체적으로 데이터 과학 솔루션을 합니다. 이 문서에서는 또한 알려 시각화에 제공 된 코드와 저장된 프로시저에 포함된 된 R 코드와 같은 SQL server에서 데이터 쉽게 사용 되는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]합니다.

## <a name="bring-compute-power-to-the-data"></a>데이터에 계산 능력을 가져오기

SQL Server에서 R 및 Python 통합의 주요 디자인 목표를 분석 데이터에 근접 했습니다. 다음과 같은 여러 이점을 제공 합니다.

+ 데이터 보안. 데이터 원본에 더 가까운 곳에 R을 가져오는 불필요 하거나 안전 하지 않은 데이터 이동을 방지할 수 있습니다.
+ 속도. 데이터베이스는 집합 기반 작업에 최적화됩니다. 메모리 내 테이블에 같은 데이터베이스의 최신 혁신 요약 및 번개, 집계 및 데이터 과학을 완벽 하 게 보완 됩니다.
+ 배포 및 통합 편의성입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다른 많은 데이터 관리 작업 및 응용 프로그램에 대 한 작업의 중앙 지점이입니다. 보고 웨어하우스 데이터베이스에 있는 데이터를 사용 하 여 기계 학습 솔루션에서 사용 하는 데이터가 일관성 있고 최신 인지 확인 합니다. 
+ 클라우드 및 온-프레미스에서 효율성입니다. R에서 데이터를 처리하는 대신 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 및 Azure Data Factory를 비롯한 엔터프라이즈 데이터 파이프라인을 사용할 수 있습니다. Power BI 또는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 통해 결과 또는 분석을 쉽게 보고할 수 있습니다.

다양한 데이터 처리 및 분석 작업에 SQL과 R을 적절하게 조합하여 사용하면 데이터 과학자와 개발자가 모두 생산성을 높일 수 있습니다.

<a name="bkmk_ssis"></a> 

## <a name="use-ssis-for-data-transformation-and-automation"></a>SSIS를 사용 하 여 데이터 변환 및 자동화

데이터 과학 워크플로는 반복이 매우 빈번하며, 크기 조정, 집계, 확률 계산, 특성 병합 및 이름 변경을 비롯한 데이터 변환이 많이 이루어집니다. 데이터 과학자는 R, Python 또는 기타 언어로 이러한 작업을 대부분 수행하지만 엔터프라이즈 데이터로 이러한 워크플로를 실행하려면 ETL 도구 및 프로세스와의 원활한 통합이 필요합니다.

Transact-SQL 및 저장 프로시저를 통해 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]을 사용하여 R로 복잡한 작업을 실행할 수 있기 때문에 다시 개발하는 작업을 최소화하여 R 작업과 기존 ETL 프로세스를 통합할 수 있습니다. 대신 R에서 메모리 집중형 작업의 체인을 수행 하는 보다 데이터 준비를 최적화할 수 있습니다를 비롯 한 가장 효율적인 도구를 사용 하 여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 고 [!INCLUDE[tsql](../../includes/tsql-md.md)]입니다. 

다음은 데이터 처리를 자동화할 수 있습니다 하는 방법에 대 한 몇 가지 아이디어 및 모델링에 사용 하 여 파이프라인 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:

+ 사용 하 여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] SQL database에 필요한 데이터 기능 만들기 작업
+ 조건부 분기를 사용하여 R 작업에 대한 컴퓨팅 컨텍스트 전환
+ 데이터베이스에서 자신의 데이터를 생성 하는 R 작업을 실행 하 고 응용 프로그램을 사용 하 여 해당 데이터를 공유 합니다.
+ 사용 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 텍스트 변수로 저장 된 R 스크립트를 로드 및 SQL Server에서 실행

## <a name="ssis-example"></a>SSIS 예제

다음 예제에서는이 URL에 Jimmy Wong가 작성 한 이제 사용 중지 되지 MSDN 블로그 게시물에서 시작: `https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/`합니다.

이 예제에서는 SSIS를 사용 하 여 작업을 자동화 하는 방법을 보여 줍니다. SQL Server Management Studio를 사용 하 여 포함 된 R을 사용 하 여 저장된 프로시저를 생성 하 고 다음에서 이러한 저장된 프로시저를 실행 [T-SQL 실행 태스크](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) SSIS 패키지의 합니다.

이 예제를 단계별로 Management Studio, SSIS, SSIS 디자이너, 패키지를 디자인 하 고 T-SQL을 사용 하 여 친숙 해야 합니다. SSIS 패키지는 3 [T-SQL 실행 태스크](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) 학습 데이터 테이블에 삽입 하는 데이터를 모델링 및 예측을 출력할 데이터 점수 매기기입니다.

### <a name="create-tables"></a>테이블 만들기

몇 개의 테이블을 만들려면 SQL Server Management Studio에서 다음 스크립트 실행: 하나는 데이터 및 모델을 저장할 다른 저장 합니다. 운영 화 시나리오에서 학습 데이터와 작동 하도록 ssis_iris 테이블의 역할이입니다. 

```T-SQL
Use irissql
GO

Create table ssis_iris (
    id int not null identity primary key
    , "Sepal.Length" float not null, "Sepal.Width" float not null
    , "Petal.Length" float not null, "Petal.Width" float not null
    , "Species" varchar(100) null
);
GO

Create table ssis_iris_models (
    model_name varchar(30) not null default('default model') primary key,
    model varbinary(max) not null
);
GO
```

### <a name="create-a-stored-procedure-that-loads-training-data"></a>학습 데이터를 로드 하는 저장된 프로시저 만들기

이 스크립트는 기본 제공 R 데이터 집합을 사용 하 여 데이터 프레임으로 아이리스를 로드 하는 저장된 프로시저를 만듭니다.

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

### <a name="define-an-execute-sql-task-that-refreshes-the-model"></a>모델을 새로 고치는 SQL 실행 태스크를 정의 합니다.

SSIS 디자이너에서 만듭니다는 [SQL 실행 태스크](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task)합니다.

![데이터 삽입](../media/create-workflows-using-r-in-sql-server/ssis-exec-sql-insert-data.png "데이터 삽입")

SQLStatement에 대 한 스크립트는 다음과 같습니다. 스크립트는 기존 데이터를 제거 하 고 사용 하 여 새 데이터를 다시 로드 합니다 **load_iris** 이전 단계에서 만든 저장 프로시저입니다.

```T-SQL
truncate table ssis_iris;
insert into ssis_iris("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species")
exec dbo.load_iris;
```

### <a name="create-a-stored-procedure-that-generates-a-model"></a>모델을 생성 하는 저장된 프로시저 만들기

이 저장된 프로시저는 코드를 사용 하 여 선형 모델을 만드는 [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)합니다. RevoScaleR 및 revoscalepy 라이브러리는 SQL Server에서 R 및 Python 세션에서 자동으로 로드 됩니다.

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

### <a name="define-an-execute-sql-task-that-runs-the-model-generation-stored-procedure"></a>모델 생성 저장된 프로시저를 실행 하는 SQL 실행 태스크를 정의 합니다.

이 단계에서는 [SQL 실행 태스크](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task) 실행 합니다 **generate_iris_rx_model** 저장 프로시저를 모델을 만들고 ssis_iris_models 테이블에 삽입 합니다.

![선형 모델을 생성](../media/create-workflows-using-r-in-sql-server/ssis-exec-rxlinmod.png "선형 모델을 생성 합니다.")

```T-SQL
insert into ssis_iris_models (model)
exec generate_iris_rx_model;
update ssis_iris_models set model_name = 'rxLinMod' where model_name = 'default model';
```

이 작업에는 다음이 완료 되 면 이진 모델을 하나 포함 되어 있는지 확인 하려면 ssis_iris_models를 쿼리할 수 있습니다.

### <a name="predict-score-outcomes-using-the-trained-model"></a>"학습된" 모델을 사용 하 여 (점수) 결과 예측

이 간단한 예제에서는 가정은 해당 ssis_iris_model 학습된 된 모델입니다. 학습된 된 모델의 목적은 예측을 생성 하는 것을에서는 준비가 이제이 사용 하 여 예측을 실행 합니다. 

이 위해 트리거할 SQL 쿼리에서 R 스크립트를 저장 합니다 [rxPredict](https://docs.microsoft.com//machine-learning-server/r-reference/revoscaler/rxpredict) ssis_iris_model에 기본 제공 R 함수입니다. SQL Server에서 저장된 프로시저를 호출할 **predict_species_length** 이 작업을 수행 합니다.

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

### <a name="define-an-execute-sql-task-that-predicts-outcomes"></a>결과 예측 하는 SQL 실행 태스크를 정의 합니다.

사용 하 여 [SQL 실행 태스크](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task)를 실행 합니다 **predict_species_length** 예측된 꽃잎 길이 생성 하는 절차를 저장 합니다.

![예측을 생성할](../media/create-workflows-using-r-in-sql-server/ssis-exec-predictions.png "예측 생성")

```T-SQL
exec predict_species_length 'rxLinMod';
```

### <a name="run-the-solution"></a>솔루션 실행

SSIS 디자이너에서 f5 키를 눌러 패키지를 실행 합니다. 다음 스크린샷과 유사한 결과가 표시 됩니다.

![디버그 모드에서 실행 하려면 F5](../media/create-workflows-using-r-in-sql-server/ssis-exec-F5-run.png "f5를 눌러 디버그 모드에서 실행을")

<a name="bkmk_ssrs"></a> 

## <a name="use-ssrs-for-visualizations"></a>SSRS를 사용 하 여 시각화에 대 한

R 차트와 흥미로운 시각화를 만들 수는 있지만 각 차트 또는 그래프 개별적으로 생성 해야 하는 외부 데이터 원본과 잘 통합 된 아닙니다. 공유도 어려울 수 있습니다.

사용 하 여 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]를 통해 R에서 복잡 한 작업을 실행할 수 있습니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저, 다양 한 엔터프라이즈 보고 도구를 포함 하 여 쉽게 사용할 수 있는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 및 Power BI입니다.

### <a name="ssrs-example"></a>SSRS 예제

[Microsoft Reporting Services(SSRS)용 R 그래픽 장치](https://rgraphicsdevice.codeplex.com/)

CodePlex 프로젝트에서 사용할 수 있는 이미지로 R의 그래픽 출력을 렌더링 하는 코드는 사용자 지정 보고서 항목을 만들 수 있도록 제공 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서입니다.  사용자 지정 보고서 항목을 사용하여 다음을 수행할 수 있습니다.

+ R 그래픽 디바이스를 사용하여 만든 차트 및 그림을 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 대시보드에 게시

+ [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 매개 변수를 R 그림에 전달

> [!NOTE]
> 이 샘플에서는 Reporting Services 용 R 그래픽 장치를 지 원하는 코드를 Visual Studio 및 Reporting Services 서버에 설치 되어야 합니다. 수동 컴파일 및 구성도 필요합니다.

## <a name="next-steps"></a>다음 단계

이 문서의 예제 SSIS 및 SSRS에서는 포함 된 R 또는 Python 스크립트를 포함 하는 저장된 프로시저를 실행 하는 두 가지 경우를 보여 줍니다. 사용할 수 있는 R 또는 Python 스크립트 응용 프로그램 또는 저장된 프로시저의 실행 요청을 보낼 수 있는 도구에 요점은 수 있습니다. SSIS에 대 한 추가 코딩할은 자동화 하 고 작업의 체인에 포함 된 R 또는 Python 데이터 과학 기능을 사용 하 여 다양 한 범위의 데이터 취득, 정리, 조작 및 등 같은 작업을 예약 하는 패키지를 만들 수 있습니다. 자세한 내용 및 아이디어를 참조 하세요 [저장된 프로시저를 사용 하 여 SQL Server Machine Learning Services에서 조작 R 코드](operationalizing-your-r-code.md)합니다.