---
title: R-SQL Server Machine Learning Services를 사용 하 여 SSIS 및 SSRS 워크플로 만들기
description: 통합 시나리오를 SQL Server Machine Learning Services 및 R Services, Reporting Services (SSRS) 및 SQL Server Integration Services (SSIS)를 결합 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/17/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 5d480b7cd24200b051fa2626fc41fa757703eaf8
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58512390"
---
# <a name="create-ssis-and-ssrs-workflows-with-r-on-sql-server"></a>SQL Server에서 R을 사용 하 여 SSIS 및 SSRS 워크플로 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 두 가지 중요 한 SQL Server 기능을 사용 하 여 SQL Server Machine Learning Services의 언어 및 데이터 과학 기능을 사용 하는 포함 된 R 및 Python 스크립트를 사용 하는 방법을 설명 합니다. SQL Server Integration Services (SSIS) 및 SQL Server Reporting Services SSRS 합니다. SQL Server에서 R 및 Python 라이브러리 통계 및 예측 함수를 제공합니다. SSIS 및 SSRS 조정 된 ETL 변환 및 시각화를 각각 제공 합니다. 이 문서에서는이 워크플로 패턴에 이러한 모든 기능 작업을 함께 배치 하는 방법에 설명 합니다.

> [!div class="checklist"]
> * 실행 R 또는 Python을 포함 하는 저장된 프로시저 만들기
> * SSIS 또는 SSRS에서 저장된 프로시저를 실행 합니다.

이 문서의 예제에서는 R 및 SSIS에 대 한 대부분 되지만 개념과 단계는 Python에 동일 하 게 적용 합니다. 두 번째 섹션 SSRS 시각화에 대 한 지침과 링크를 제공합니다.

<a name="bkmk_ssis"></a> 

## <a name="use-ssis-for-automation"></a>SSIS를 사용 하 여 자동화

데이터 과학 워크플로는 반복이 매우 빈번하며, 크기 조정, 집계, 확률 계산, 특성 병합 및 이름 변경을 비롯한 데이터 변환이 많이 이루어집니다. 데이터 과학자는 R, Python 또는 기타 언어로 이러한 작업을 대부분 수행하지만 엔터프라이즈 데이터로 이러한 워크플로를 실행하려면 ETL 도구 및 프로세스와의 원활한 통합이 필요합니다.

때문에 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] TRANSACT-SQL 및 저장된 프로시저를 통해 R에서 복잡 한 작업을 실행할 수 있도록 기존 ETL 프로세스를 사용 하 여 데이터 과학 작업을 통합할 수 있습니다. 대신 메모리 사용량이 많은 작업의 체인을 수행 하는 보다 데이터 준비를 최적화할 수 있습니다를 비롯 한 가장 효율적인 도구를 사용 하 여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 고 [!INCLUDE[tsql](../../includes/tsql-md.md)]입니다. 

다음은 데이터 처리를 자동화할 수 있습니다 하는 방법에 대 한 몇 가지 아이디어 및 모델링에 사용 하 여 파이프라인 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:

+ 온-프레미스 데이터를 추출 하거나 학습 데이터를 작성 하는 원본 클라우드 
+ 빌드 및 데이터 통합 워크플로의 일부로 R 또는 Python 모델 실행
+ (예약 된) 정기적으로 모델 다시 학습
+ R 또는 Python 스크립트에서 결과 Excel, Power BI, Oracle 및 Teradata 등 등과 같은 다른 대상에 로드
+ SSIS 태스크를 사용 하 여 SQL database에 데이터 기능 만들기
+ R 및 Python 작업에 대 한 계산 컨텍스트를 전환 하려면 조건부 분기를 사용 합니다.

## <a name="ssis-example"></a>SSIS 예제

다음 예제에서는이 URL에 Jimmy Wong가 작성 한 이제 사용 중지 되지 MSDN 블로그 게시물에서 시작 합니다. `https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/`

이 예제에서는 SSIS를 사용 하 여 작업을 자동화 하는 방법을 보여 줍니다. SQL Server Management Studio를 사용 하 여 포함 된 R을 사용 하 여 저장된 프로시저를 생성 하 고 다음에서 이러한 저장된 프로시저를 실행 [T-SQL 실행 태스크](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) SSIS 패키지의 합니다.

이 예제를 단계별로 Management Studio, SSIS, SSIS 디자이너, 패키지를 디자인 하 고 T-SQL을 사용 하 여 친숙 해야 합니다. SSIS 패키지는 3 [T-SQL 실행 태스크](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) 학습 데이터 테이블에 삽입 하는 데이터를 모델링 및 예측을 출력할 데이터 점수 매기기입니다.

### <a name="load-training-data"></a>학습 데이터를 로드 합니다.

데이터 저장용 테이블을 만들려면 SQL Server Management Studio에서 다음 스크립트를 실행 합니다. 만들 하 고이 연습에 대 한 테스트 데이터베이스를 사용 해야 합니다. 

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

데이터 프레임으로 학습 데이터를 로드 하는 저장된 프로시저를 만듭니다. 이 예제에서는 기본 제공 아이리스 데이터 집합을 사용 하는. 

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

SSIS 디자이너에서 만듭니다는 [SQL 실행 태스크](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task) 방금 정의한 저장된 프로시저를 실행 하는 합니다. 에 대 한 스크립트 **SQLStatement** 기존 데이터를 제거, 데이터를 삽입 하려면 지정 다음 데이터를 제공 하는 저장된 프로시저를 호출 합니다.

```T-SQL
truncate table ssis_iris;
insert into ssis_iris("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species")
exec dbo.load_iris;
```

![데이터 삽입](../media/create-workflows-using-r-in-sql-server/ssis-exec-sql-insert-data.png "데이터 삽입")

### <a name="generate-a-model"></a>모델 생성

모델을 저장 하는 테이블을 만들려면 SQL Server Management Studio에서 다음 스크립트를 실행 합니다. 

```T-SQL
Use test-db
GO

Create table ssis_iris_models (
    model_name varchar(30) not null default('default model') primary key,
    model varbinary(max) not null
);
GO
```

사용 하 여 선형 모델을 생성 하는 저장된 프로시저를 만듭니다 [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)합니다. RevoScaleR 및 revoscalepy 라이브러리 SQL Server에서 R 및 Python 세션에서 자동으로 제공 되므로 라이브러리를 가져올 필요가 없습니다.

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

SSIS 디자이너에서 만듭니다는 [SQL 실행 태스크](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task) 실행 하는 **generate_iris_rx_model** 저장 프로시저입니다. 모델을 직렬화 하 고 ssis_iris_models 테이블에 저장 합니다. 스크립트가 **SQLStatement** 는 다음과 같습니다.

```T-SQL
insert into ssis_iris_models (model)
exec generate_iris_rx_model;
update ssis_iris_models set model_name = 'rxLinMod' where model_name = 'default model';
```

![선형 모델을 생성](../media/create-workflows-using-r-in-sql-server/ssis-exec-rxlinmod.png "선형 모델을 생성 합니다.")

이 작업에는 다음이 완료 되 면 검사점으로 하나의 이진 모델에 포함 되어 있는지 확인 하려면 ssis_iris_models를 쿼리할 수 있습니다.

### <a name="predict-score-outcomes-using-the-trained-model"></a>"학습된" 모델을 사용 하 여 (점수) 결과 예측

학습 데이터를 로드 하 고 모델을 생성 하는 코드를가지고 단계만 왼쪽은 예측을 생성 하려면 모델을 사용 합니다. 

이 위해 트리거할 SQL 쿼리에서 R 스크립트를 저장 합니다 [rxPredict](https://docs.microsoft.com//machine-learning-server/r-reference/revoscaler/rxpredict) ssis_iris_model에 기본 제공 R 함수입니다. 저장된 프로시저를 호출할 **predict_species_length** 이 작업을 수행 합니다.

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

SSIS 디자이너에서 만듭니다는 [SQL 실행 태스크](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task) 실행 하는 합니다 **predict_species_length** 예측된 꽃잎 길이 생성 하는 절차를 저장 합니다.

```T-SQL
exec predict_species_length 'rxLinMod';
```

![예측을 생성할](../media/create-workflows-using-r-in-sql-server/ssis-exec-predictions.png "예측 생성")

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