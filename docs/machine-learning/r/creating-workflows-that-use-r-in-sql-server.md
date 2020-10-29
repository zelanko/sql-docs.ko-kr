---
title: R을 사용하여 SSIS 및 SSRS 워크플로 만들기
description: SQL Server Machine Learning Services 및 R Services, Reporting Services(SSRS) 및 SSIS(SQL Server Integration Services)를 조합하는 통합 시나리오입니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 08/28/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: cdb11607fe7424c8c1159ba767e6f8292361065f
ms.sourcegitcommit: ef20f39a17fd4395dd2dd37b8dd91b57328a751c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2020
ms.locfileid: "92793760"
---
# <a name="create-ssis-and-ssrs-workflows-with-r-on-sql-server"></a>SQL Server에서 R을 사용하여 SSIS 및 SSRS 워크플로 만들기
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

이 문서에서는 2가지 중요한 SQL Server 기능인 SSIS(SQL Server Integration Services) 및 SSRS(SQL Server Reporting Services)를 사용하여 SQL Server Machine Learning Services의 언어 및 데이터 과학 기능과 함께 포함된 R 및 Python 스크립트를 사용하는 방법을 설명합니다. SQL Server의 R 및 Python 라이브러리는 통계 및 예측 함수를 제공합니다. SSIS 및 SSRS는 각각 조정된 ETL 변환 및 시각화를 제공합니다. 이 문서에서는 이러한 모든 기능을 이 워크플로 패턴에 함께 포함하는 방법을 설명합니다.

> [!div class="checklist"]
> * R 또는 Python 실행 파일을 포함하는 저장 프로시저 만들기
> * SSIS 또는 SSRS에서 저장 프로시저 실행

이 문서의 예제는 대부분 R 및 SSIS에 대한 것이지만, 개념과 단계는 Python에도 동일하게 적용됩니다. 두 번째 섹션에서는 SSRS 시각화에 대한 지침과 링크를 제공합니다.

<a name="bkmk_ssis"></a> 

## <a name="use-ssis-for-automation"></a>Automation에 SSIS 사용

데이터 과학 워크플로는 반복이 매우 빈번하며, 크기 조정, 집계, 확률 계산, 특성 병합 및 이름 변경을 비롯한 데이터 변환이 많이 이루어집니다. 데이터 과학자는 R, Python 또는 기타 언어로 이러한 작업을 대부분 수행하지만 엔터프라이즈 데이터로 이러한 워크플로를 실행하려면 ETL 도구 및 프로세스와의 원활한 통합이 필요합니다.

Transact-SQL 및 저장 프로시저를 통해 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]을 사용하여 R로 복잡한 작업을 실행할 수 있기 때문에 데이터 과학 작업과 기존 ETL 프로세스를 통합할 수 있습니다. 메모리를 많이 사용하는 일련의 작업을 수행하는 대신 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 및 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 비롯한 가장 효율적인 도구를 사용하여 데이터 준비를 최적화할 수 있습니다. 

다음은 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 사용하여 데이터 처리 및 모델링 파이프라인을 자동화할 수 있는 몇 가지 방법입니다.

+ 온-프레미스 또는 클라우드 원본에서 데이터를 추출하여 학습 데이터 작성 
+ 데이터 통합 워크플로의 일부로 R 또는 Python 모델 빌드 및 실행
+ 정기적으로(예약된) 모델 다시 학습
+ R 또는 Python 스크립트의 결과를 Excel, Power BI, Oracle, Teradata 등의 다른 대상으로 로드
+ SSIS 작업을 사용하여 SQL Database에서 데이터 기능 만들기
+ 조건부 분기를 사용하여 R 및 Python 작업에 대한 컴퓨팅 컨텍스트 전환

## <a name="ssis-example"></a>SSIS 예제

다음 예제는 `https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/` URL에서 Jimmy Wong이 작성한 현재 사용 중지된 MSDN 블로그 게시물에서 가져왔습니다.

이 예제에서는 SSIS를 사용하여 작업을 자동화하는 방법을 보여 줍니다. SQL Server Management Studio를 사용하여 포함된 R로 저장 프로시저를 만든 다음, SSIS 패키지의 [T-SQL 실행 태스크](../../integration-services/control-flow/execute-t-sql-statement-task.md)에서 해당 저장 프로시저를 실행합니다.

이 예제를 단계별로 실행하려면 Management Studio, SSIS, SSIS 디자이너, 패키지 디자인 및 T-SQL에 대해 잘 알고 있어야 합니다. SSIS 패키지는 학습 데이터를 테이블에 삽입하고, 데이터를 모델링하고, 데이터에 점수를 매겨 예측 출력을 가져오는 세 가지 [T-SQL 실행 태스크](../../integration-services/control-flow/execute-t-sql-statement-task.md)를 사용합니다.

### <a name="load-training-data"></a>학습 데이터 로드

SQL Server Management Studio에서 다음 스크립트를 실행하여 데이터를 저장하기 위한 테이블을 만듭니다. 이 연습에서는 테스트 데이터베이스를 만들어 사용해야 합니다. 

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

데이터 프레임에 학습 데이터를 로드하는 저장 프로시저를 만듭니다. 이 예제에서는 기본 제공되는 Iris 데이터 세트를 사용합니다. 

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

SSIS 디자이너에서 방금 정의한 저장 프로시저를 실행하는 [SQL 실행 태스크](../../integration-services/control-flow/execute-sql-task.md)를 만듭니다. **SQLStatement** 의 스크립트는 기존 데이터를 제거하고 삽입할 데이터를 지정한 다음, 저장 프로시저를 호출하여 데이터를 제공합니다.

```T-SQL
truncate table ssis_iris;
insert into ssis_iris("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species")
exec dbo.load_iris;
```

![데이터 삽입](../media/create-workflows-using-r-in-sql-server/ssis-exec-sql-insert-data.png "데이터 삽입")

### <a name="generate-a-model"></a>모델 생성

SQL Server Management Studio에서 다음 스크립트를 실행하여 모델을 저장하는 테이블을 만듭니다. 

```T-SQL
Use test-db
GO

Create table ssis_iris_models (
    model_name varchar(30) not null default('default model') primary key,
    model varbinary(max) not null
);
GO
```

[rxLinMod](/machine-learning-server/r-reference/revoscaler/rxlinmod)를 사용하여 선형 모델을 생성하는 저장 프로시저를 만듭니다. RevoScaleR 및 revoscalepy 라이브러리는 SQL Server의 R 및 Python 세션에서 자동으로 사용할 수 있으므로 라이브러리를 가져올 필요가 없습니다.

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

SSIS 디자이너에서 [SQL 실행 태스크](../../integration-services/control-flow/execute-sql-task.md)를 만들어 **generate_iris_rx_model** 저장 프로시저를 실행합니다. 모델이 serialize되어 ssis_iris_models 테이블에 저장됩니다. **SQLStatement** 에 대한 스크립트는 다음과 같습니다.

```T-SQL
insert into ssis_iris_models (model)
exec generate_iris_rx_model;
update ssis_iris_models set model_name = 'rxLinMod' where model_name = 'default model';
```

![선형 모델 생성](../media/create-workflows-using-r-in-sql-server/ssis-exec-rxlinmod.png "선형 모델 생성")

이 작업이 완료된 후에 검사점으로서 ssis_iris_models를 쿼리하여 이진 모델이 하나 포함되어 있는지 확인할 수 있습니다.

### <a name="predict-score-outcomes-using-the-trained-model"></a>"학습된" 모델을 사용하여 결과 예측(점수 매기기)

이제 학습 데이터를 로드하고 모델을 생성하는 코드를 만들었으므로 남은 단계는 이 모델을 사용해서 예측을 생성하는 것입니다. 

이렇게 하려면 SQL 쿼리에 R 스크립트를 추가하여 ssis_iris_model에서 [rxPredict](/machine-learning-server/r-reference/revoscaler/rxpredict) 기본 제공 R 함수를 트리거합니다. **predict_species_length** 저장 프로시저가 이 작업을 수행합니다.

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

SSIS 디자이너에서 **predict_species_length** 저장 프로시저를 실행하여 예측된 꽃잎 길이를 생성하는 [SQL 실행 태스크](../../integration-services/control-flow/execute-sql-task.md)를 만듭니다.

```T-SQL
exec predict_species_length 'rxLinMod';
```

![예측 생성](../media/create-workflows-using-r-in-sql-server/ssis-exec-predictions.png "예측 생성")

### <a name="run-the-solution"></a>솔루션 실행

SSIS 디자이너에서 F5 키를 눌러 패키지를 실행합니다. 다음 스크린샷과 비슷한 내용이 출력됩니다.

![디버그 모드에서 실행하기 위한 F5 키](../media/create-workflows-using-r-in-sql-server/ssis-exec-F5-run.png "디버그 모드에서 실행하기 위한 F5 키")

<a name="bkmk_ssrs"></a> 

## <a name="use-ssrs-for-visualizations"></a>시각화에 SSRS 사용

R로 차트와 흥미로운 시각화를 만들 수 있지만, 외부 데이터 원본과 잘 통합되지 않기 때문에 각 차트와 그래프를 개별적으로 생성해야 합니다. 공유도 어려울 수 있습니다.

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]을 사용하면 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저를 통해 R로 복잡한 작업을 실행할 수 있기 때문에, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 및 Power BI를 비롯한 다양한 엔터프라이즈 보고 도구에서 쉽게 사용할 수 있습니다.

## <a name="next-steps"></a>다음 단계

이 문서의 SSIS 및 SSRS 예제에서는 포함된 R 또는 Python 스크립트를 포함하는 저장 프로시저를 실행하는 두 가지 사례를 보여 줍니다. 핵심 요점은 저장 프로시저에 실행 요청을 보낼 수 있는 모든 애플리케이션이 나 도구에서 R 또는 Python 스크립트를 사용하도록 할 수 있다는 것입니다. SSIS에 대한 추가적인 사항은 작업 체인에 포함된 R 또는 Python 데이터 과학 기능을 사용하여 데이터 취득, 정리, 조작 등의 광범위한 작업을 자동화하고 예약하는 패키지를 만들 수 있다는 것입니다. 자세한 내용 및 아이디어를 보려면 [SQL Server Machine Learning Services에서 저장 프로시저를 사용하여 R 코드 운영](operationalizing-your-r-code.md)을 참조하세요.