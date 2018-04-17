---
title: 모델에서 예측 및 플롯(SQL에서 R 빠른 시작) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 3809b8f6dbf84de04b84c7f4a6bdd5c492e2bdcd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="predict-and-plot-from-model-r-in-sql-quickstart"></a>모델에서 예측 및 플롯 (SQL에서 R 빠른 시작)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

새로운 데이터를 사용한 _채점(scoring)_ 을 위해서 테이블로부터 훈련된 모델 중 하나를 가져온 다음 예측을 기반으로 새로운 데이터 집합을 호출합니다. 채점이란 훈련된 모델에 주어진 새로운 데이터에 기반한 예측, 확률, 혹은 기타 값을 생성함을 의미하는 데이터 과학에서 종종 사용되는 용어입니다.

## <a name="create-the-table-of-new-speeds"></a>새로운 속도에 대한 테이블 만들기

원래 학습 데이터가 25mph(마일/시간)의 속도에서 중지된 것을 알아차리셨나요? 이는 원래 데이터가 1920년의 실험을 기준으로 하기 때문입니다.

자동차가 60mph 또는 100mph의 속도로 빠르게 달릴 수 있다고 가정하면 1920년대의 자동차가 중지하는 데 얼마나 오랜 시간이 걸릴지 궁금할 것입니다. 이 질문에 답하기 위해 몇 가지 새로운 속도 값을 제공해야 합니다.

```sql
CREATE TABLE [dbo].[NewCarSpeed]([speed] [int] NOT NULL,
    [distance] [int]  NULL) ON [PRIMARY]
GO
INSERT [dbo].[NewCarSpeed] (speed)
VALUES (40),  (50),  (60), (70), (80), (90), (100)
```

## <a name="predict-stopping-distance"></a>중지 거리 예측

지금까지 테이블에는 여러 R 모델이 포함되고 모든 모델은 서로 다른 매개 변수 또는 알고리즘을 사용하여 빌드되거나 다양한 데이터 하위 집합을 기반으로 훈련됩니다.

![rsql_basictut_listofmodels](media/rsql-basictut-listofmodels.png)

하나의 특정 모델을 기반으로 예측을 가져오려면 다음 작업을 수행 하는 SQL 스크립트를 작성 해야 합니다.

1. 원하는 모델을 가져옵니다.
2. 새 입력 데이터를 가져옵니다.
3. 해당 모델과 호환되는 R 예측 함수를 호출합니다.

이 예제에서는 **RevoScaleR** 패키지의 일부로 제공되는 **rxLinMod** 알고리즘에 기반한 모델이므로 일반 R의 [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) 함수 대신 `predict` 함수를 호출합니다.

```sql
DECLARE @speedmodel varbinary(max) = (SELECT model FROM [dbo].[stopping_distance_models] WHERE model_name = 'latest model');
EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'
            current_model <- unserialize(as.raw(speedmodel));
            new <- data.frame(NewCarData);
            predicted.distance <- rxPredict(current_model, new);
            str(predicted.distance);
            OutputDataSet <- cbind(new, ceiling(predicted.distance));
            '
    , @input_data_1 = N' SELECT speed FROM [dbo].[NewCarSpeed] '
    , @input_data_1_name = N'NewCarData'
    , @params = N'@speedmodel varbinary(max)'
    , @speedmodel = @speedmodel
WITH RESULT SETS (([new_speed] INT, [predicted_distance] INT))
```

+ SELECT 문을 사용하여 테이블에서 단일 모델을 가져오고 입력 매개 변수로 전달합니다.
+  테이블에서 모델을 검색한 후 모델에서 `unserialize` 함수를 호출합니다.

    > [!TIP] 
    > [실시간 점수 매기기](../../advanced-analytics/real-time-scoring.md)를 지원하는 RevoScaleR의 [serialization 함수](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)도 확인해보세요.
+  모델에 필요한 인수들로 `rxPredict` 함수를 적용하고 새 입력 데이터를 제공합니다.
+  예제에서 추가된 `str` 함수는 테스트 단계에 R에서 반환되는 데이터의 스키마를 확인하기 위한 용도입니다. 나중에 제거할 수 있습니다.
+ R 스크립트에 사용된 열 이름은 저장 프로시저 출력으로 반드시 전달되지는 않습니다. 새 열 이름을 정의하는 WITH RESULTS 절을 사용했습니다.

**결과**

![rsql_basictut_scoringresults_smalldata](media/rsql-basictut-scoringresults-smalldata.PNG)

## <a name="perform-scoring-in-parallel"></a>병렬로 평가 수행

작은 데이터 집합에서는 예측이 상당히 빠르게 반환됩니다. 하지만 많은 예측을 매우 빠르게 해야 한다고 가정해 보겠습니다. QL Server에서 처리 속도를 높이는 방법은 여러 가지가 있으며, 작업을 병렬로 처리할 수 있다면 더 많이 있습니다. 특히 채점(scoring)을 하기 위해서는 `sp_execute_external_script`에 *@parallel* 매개변수를 추가하고 값을 **1**로 설정합니다.

수십만 개의 값이 들어있는 자동차 속도에 대한 훨씬 더 큰 테이블을 가지고 있다고 가정해 보겠습니다. 숫자 테이블을 생성하도록 도와주는 커뮤니티의 많은 샘플 T-SQL 스크립트가 있으므로 여기서는 그러한 스크립트를 재현하지 않겠습니다. 많은 정수가 포함된 열이 있고 모델에 `speed`에 대한 입력으로 이 열을 사용하는 경우를 고려해 보겠습니다.

이렇게 하려면 동일한 예측 쿼리를 실행하되 큰 데이터 집합으로 대체하고 `@parallel = 1` 인수를 추가합니다.

```sql
DECLARE @speedmodel varbinary(max) = (select model from [dbo].[stopping_distance_models] where model_name = 'default model');
EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'
            current_model <- unserialize(as.raw(speedmodel));
            new <- data.frame(NewCarData);
            predicted.distance <- rxPredict(current_model, new);
            OutputDataSet <- cbind(new, ceiling(predicted.distance));
            '
    , @input_data_1 = N' SELECT [speed] FROM [dbo].[HugeTableofCarSpeeds] '
    , @input_data_1_name = N'NewCarData'
    , @parallel = 1
    , @params = N'@speedmodel varbinary(max)'
    , @speedmodel = @speedmodel
WITH RESULT SETS (([new_speed] INT, [predicted_distance] INT))
```

+ 병렬 실행은 일반적으로 매우 큰 데이터로 작업할 때만 이득을 제공합니다. SQL 데이터베이스 엔진에서는 병렬 실행이 불필요하다고 판단할 수도 있습니다. 게다가 데이터를 가져오는 SQL 쿼리가 병렬 쿼리 계획을 생성할 수 있어야 합니다.

+ 병렬 실행을 위해 옵션을 사용할 때 **반드시** WITH RESULT SETS 절을 사용해서 먼저 출력 결과 스키마를 지정해야 합니다. 이렇게 함으로써 SQL Server에서 알 수 없는 스키마가 포함될 수 있는 다중 병렬 데이터 집합의 결과를 집계할 수 있도록 허용합니다.

+ *채점(scoring)* 대신 *훈련* 을 시키는 경우엔 이 매개변수가 효과가 없을 수도 있습니다. 모델 유형에 따라 모델 생성 시 요약을 만들기 전에 모든 행을 읽어야 할 수 있습니다.

+ 모델을 훈련할 때 병렬 처리 이득을 취하기 위해서 **RevoScaleR** 알고리즘 중의 하나를 사용하기를 권장합니다. 이 알고리즘은 `sp_execute_external_script`에<code>@parallel =1</code>을 지정하지 않더라도 자동으로 분산 처리하도록 설계되었습니다. RevoScaleR 알고리즘의 최적 성능을 얻기 위한 방법에 관한 지침으로 [분산 및 Microsoft R에서 ScaleR와 병렬 컴퓨팅](https://docs.microsoft.com/r-server/r/how-to-revoscaler-distributed-computing)을 참조하십시오.

## <a name="create-an-r-plot-of-the-model"></a>모델의 R 플롯 만들기

SQL Server Management Studio를 비롯한 많은 클라이언트는 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용하여 생성된 그림을 직접 표시할 수 없습니다. 대신, R 플롯을 생성하기 위한 일반적인 프로세스는 R 코드의 일부로 플롯을 생성한 다음 파일에 이미지를 작성하는 것입니다.

또는 이미지를 표시할 수 있는 모든 응용 프로그램에 직렬화된 이진 plot 개체를 반환할 수 있습니다.

다음 예제에서는 R에 기본적으로 포함된 플로팅 함수를 사용하여 간단한 그래픽을 만드는 방법을 보여줍니다. 이미지는 지정된 파일로 출력되며 저장 프로시저를 통해 SQL 변수로도 출력됩니다.

```sql
 EXECUTE sp_execute_external_script
 @language = N'R'
 , @script = N'
     imageDir <- ''C:\\temp\\plots'';
     image_filename = tempfile(pattern = "plot_", tmpdir = imageDir, fileext = ".jpg")
     print(image_filename);
     jpeg(filename=image_filename,  width=600, height = 800);
     print(plot(distance~speed, data=InputDataSet, xlab="Speed", ylab="Stopping distance", main = "1920 Car Safety"));
     abline(lm(distance~speed, data = InputDataSet));
     dev.off();
     OutputDataSet <- data.frame(data=readBin(file(image_filename, "rb"), what=raw(), n=1e6));
     '
  , @input_data_1 = N'SELECT speed, distance from [dbo].[CarSpeed]'
  WITH RESULT SETS ((plot varbinary(max)));
```

+ `tempfile` 함수는 파일 이름으로 사용할 수 있는 문자열을 반환하지만 파일이 아직 생성되지 않았습니다.
+ `tempfile`에 인수로 접두사 및 파일 확장명과 디렉터리를 지정할 수 있습니다. 완성된 파일 이름과 경로를 확인하기 위해 `str()`를 사용해서 메시지로 출력합니다.
+ `jpeg` 함수는 지정된 매개 변수로 R 장치를 만듭니다.
+ 플롯을 만든 후에 더 많은 시각적 기능을 추가할 수 있습니다. 이번 경우엔 `abline`을 사용해서 회귀선을 추가합니다.
+ 플롯 기능 추가를 완료하면 `dev.off()` 함수를 사용하여 그래픽 장치를 닫아야 합니다.
+ `readBin` 함수는 읽을 파일, 파일 형식 사양 및 레코드 수를 가집니다. `rb`**' 파일이 텍스트가 아닌 이진임을 나타냅니다.

**결과**

![rsql_basictut_plotresult_small](media/rsql-basictut-plotresult-small.png)

R용의 몇 가지 좋은 그래픽 패키지를 사용하여 더 정교한 플롯을 수행하고 싶다면 다음 기사들을 권장합니다. 둘 모두 인기있는 **ggplot2** 패키지가 필요합니다.

+ [Loan Classification using SQL Server 2016 R Services](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2016/09/27/loan-classification-using-sql-server-2016-r-services/)(SQL Server 2016 R Services를 사용한 대출 분류): 보험 데이터를 기반으로 하는 전체 과정 연습 시나리오입니다. **reshape**패키지가 필요합니다.
+ [R을 사용하여 그래프 및 플롯 만들기](../../advanced-analytics/tutorials/walkthrough-create-graphs-and-plots-using-r.md)

## <a name="conclusions"></a>결론

R 및 SQL Server를 통합하면 고성능 데이터 처리 및 빠른 R 분석을 위해 R 및 관계형 데이터베이스의 최고 기능을 이용하여 R 솔루션을 대규모로 더 쉽게 배포할 수 있습니다. 

R 예제에 대한 자세한 내용은 다음 추가 리소스를 참조하십시오.

+  [SQL Server R 자습서](../../advanced-analytics/tutorials/sql-server-r-tutorials.md)

    Microsoft 데이터 과학 및 R 서비스 개발 팀에서 만든 전체 과정 연습 시나리오를 통해 SQL Server와 R을 사용한 솔루션에 대해서 계속 학습합니다.

+ [SQL Server Python 자습서](../../advanced-analytics/tutorials/sql-server-python-tutorials.md)

    SQL Server 2017 년에 대 한 Python 언어와 함께 원격 계산 컨텍스트 및 확장 가능한 알고리즘의 기능을 사용 합니다.

+ [자습서 및 Microsoft R에 대 한 예제 데이터](https://docs.microsoft.com/r-server/r/tutorial-introduction)

    새 RevoScaleR 패키지를 사용하여 모델을 만들고 데이터를 변환하는 방법에 알아봅니다.

+ [MicrosoftML 시작](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)

    Microsoft Research로부터 신속하고 확장 가능한 Machine Learning 알고리즘을 배웁니다.
