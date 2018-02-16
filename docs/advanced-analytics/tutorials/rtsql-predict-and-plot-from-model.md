---
title: "예측 및 플롯 모델 (SQL 빠른 시작에서 R)에서 | Microsoft Docs"
ms.custom: 
ms.date: 08/20/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
dev_langs:
- R
- SQL
ms.assetid: 46babd8a-a331-44fc-bbd6-24daf58865e1
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 835e7d4901fc3d58edfedaea4474e9b523b71620
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2018
---
# <a name="predict-and-plot-from-model-r-in-sql-quickstart"></a>예측 하 고 모델 (SQL 빠른 시작에서 R)에서 출력
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

수행 하려면 _점수 매기기_ 테이블에서 학습된 된 모델 중 하나를 가져오는 새 데이터를 사용 하 고 다음 새로운 예측을 기반으로 사용할 데이터 집합이 호출 합니다. 점수 매기기는 경우에 따라 사용 되는 데이터 과학에서을 생성 하는 예측, 확률 또는 학습된 된 모델에 새 데이터에 따라 다른 값을 의미 합니다.

## <a name="create-the-table-of-new-speeds"></a>새로운 속도에 대한 테이블 만들기

원래 학습 데이터가 25mph(마일/시간)의 속도에서 중지된 것을 알아차리셨나요? 이는 원래 데이터가 1920년의 실험을 기준으로 하기 때문입니다.

자동차가 60mph 또는 100mph의 속도로 빠르게 달릴 수 있다고 가정하면 1920년대의 자동차가 중지하는 데 얼마나 오랜 시간이 걸릴지 궁금할 것입니다. 이 질문의 답 몇 가지 새로운 속도 값을 제공 해야 합니다.

```sql
CREATE TABLE [dbo].[NewCarSpeed]([speed] [int] NOT NULL,
    [distance] [int]  NULL) ON [PRIMARY]
GO
INSERT [dbo].[NewCarSpeed] (speed)
VALUES (40),  (50),  (60), (70), (80), (90), (100)
```

## <a name="predict-stopping-distance"></a>중지 거리 예측

지금까지 테이블에는 여러 R 모델이 포함되고 모든 모델은 서로 다른 매개 변수 또는 알고리즘을 사용하여 빌드되거나 다양한 데이터 하위 집합을 기반으로 학습됩니다.

![rsql_basictut_listofmodels](media/rsql-basictut-listofmodels.png)

하나의 특정 모델을 기반으로 예측을 가져오려면 다음 작업을 수행 하는 SQL 스크립트를 작성 해야 합니다.

1. 원하는 모델을 가져옵니다.
2. 새 입력 데이터를 가져옵니다.
3. 해당 모델과 호환되는 R 예측 함수를 호출합니다.

이 예제에서는 모델에 기반 하므로 **rxLinMod** 알고리즘의 일부로 제공 되는 **RevoScaleR** 호출 패키지는 [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) 함수를 보다는 제네릭 R `predict` 함수입니다.

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
    > 또한 체크 아웃 새 [serialization 함수](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) RevoScaleR을 지 원하는 제공한 [실시간 점수 매기기](../../advanced-analytics/real-time-scoring.md)합니다.
+  적절한 인수를 사용하여 `rxPredict` 함수를 적용하고 새 입력 데이터를 제공합니다.
+  예제에서는 `str` 함수는 오른쪽에서 반환 되는 데이터의 스키마를 확인 하려면 테스트 단계 추가 나중에 문을 제거할 수 있습니다.
+ R 스크립트에 사용 되는 열 이름은 반드시 저장된 프로시저 출력에 전달 되지 않습니다. 여기 몇 가지 새 열 이름을 정의 하는 결과와 절을 사용 했습니다.

**결과**

![rsql_basictut_scoringresults_smalldata](media/rsql-basictut-scoringresults-smalldata.PNG)

## <a name="perform-scoring-in-parallel"></a>병렬로 평가 수행

이 작은 데이터 집합에서는 예측이 상당히 빠르게 반환됩니다. 하지만 매우 빠르게 많은 예측을 생성해야 했다고 가정해 보겠습니다. 여러 가지 방법으로 속도를 높이기 위해 SQL Server에서에서 작업 하므로 더 작업을 병렬로 처리할 수 있으면. 특히 평가의 경우 한 가지 쉬운 방법은 *@parallel* 매개 변수를 `sp_execute_external_script`에 추가하고 값을 **1**로 설정하는 것입니다.

수백만 개의 값을 포함하는 가능한 자동차 속도에 대한 훨씬 더 큰 테이블을 얻었다고 가정해 보겠습니다. 숫자 테이블을 생성하도록 도와주는 커뮤니티의 많은 샘플 T-SQL 스크립트가 있으므로 여기서는 이러한 스크립트를 재현하지 않습니다. 많은 정수가 포함된 열이 있고 모델에서 `speed`에 대한 입력으로 이 열을 사용하는 경우를 고려해 보겠습니다.

이 수행 하려면 방금 동일한 예측 쿼리를 실행 하지만 큰 데이터 집합을 대체 추가 `@parallel = 1` 인수입니다.

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

+ 일반적으로 병렬 실행 매우 큰 데이터로 작업 하는 경우에 혜택을 제공 합니다. SQL 데이터베이스 엔진 병렬 실행은 필요 하지 않습니다 결정할 수 있습니다. 게다가 데이터를 가져오는 SQL 쿼리는 병렬 쿼리 계획을 생성할 수 있어야 합니다.

+ 병렬 실행 옵션을 사용할 경우 WITH RESULT SETS 절을 사용하여 미리 출력 결과 스키마를 지정**해야 합니다**. 출력 스키마를 미리 지정하면 SQL Server에서 알 수 없는 스키마가 포함될 수 있는 여러 병렬 데이터 집합의 결과를 집계할 수 있습니다.

+ 있다면 *학습* 대신 모델 *점수 매기기*,이 매개 변수 종종 않습니다는 효과가 있습니다. 모델 유형에 따라 모델을 만들려면 요약을 만들기 전에 모든 행을 읽어야 할 수 있습니다.

+ 모델을 학습 하는 경우 병렬 처리의 이점을 얻으려면 중 하나를 사용 하는 권장는 **RevoScaleR** 알고리즘입니다. 지정 하지 않은 경우에 이러한 알고리즘 자동으로 처리를 분산 하도록 디자인 된 <code>@parallel =1</code> 에 대 한 호출에서 `sp_execute_external_script`합니다. RevoScaleR 알고리즘으로 최적의 성능을 얻습니다 하는 방법에 대 한 지침을 참조 하십시오. [분산 및 Microsoft R에서 ScaleR와 병렬 컴퓨팅](https://docs.microsoft.com/r-server/r/how-to-revoscaler-distributed-computing)합니다.

## <a name="create-an-r-plot-of-the-model"></a>모델의 R 그림 만들기

SQL Server Management Studio를 비롯한 많은 클라이언트는 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용하여 생성된 그림을 직접 표시할 수 없습니다. 대신, R 플롯을 생성 하기 위한 일반적인 프로세스는 R 코드의 일부로 플롯을 생성 한 다음 파일에 이미지를 작성할입니다.

또는 이미지를 표시할 수 있는 모든 응용 프로그램에 직렬화 된 이진 plot 개체를 반환할 수 있습니다.

다음 예제에서는 R에 기본적으로 포함된 그리기 함수를 사용하여 간단한 그래픽을 만드는 방법을 보여 줍니다. 이미지는 지정된 파일의 출력이고 저장 프로시저를 통한 SQL 변수의 출력이기도 합니다.

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

+ `tempfile` 함수를 파일 이름으로 사용할 수 있는 문자열을 반환 하지만 파일이 아직 생성 되지 않았습니다.
+ 에 대 한 인수가 `tempfile`, 접두사 및 파일 확장명으로 디렉터리를 지정할 수 있습니다. 전체 파일 이름 및 경로 확인 하려면 사용 하 여 메시지를 인쇄 `str()`합니다.
+ `jpeg` 함수는 지정된 매개 변수를 사용하여 R 장치를 만듭니다.
+ 플롯을 만든 후에 더 많은 시각적 기능을 추가할 수 있습니다. 이 경우 한 회귀선을 사용 하 여 추가 됩니다 `abline`합니다.
+ 그림 기능 추가를 완료한 경우 `dev.off()` 함수를 사용하여 그래픽 장치를 닫아야 합니다.
+ `readBin` 함수는 읽을 파일, 서식 사양 및 레코드 수를 사용합니다. `rb`* * ' 키워드 파일은 텍스트 대신 이진을 나타냅니다.

**결과**

![rsql_basictut_plotresult_small](media/rsql-basictut-plotresult-small.png)

유용한 R용 그래픽 패키지를 사용하여 더 정교한 그리기를 수행하려면 이러한 아티클을 권장합니다. 두 경우에 모두 많이 사용되는 **ggplot2** 패키지가 필요합니다.

+ [Loan Classification using SQL Server 2016 R Services](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2016/09/27/loan-classification-using-sql-server-2016-r-services/)(SQL Server 2016 R Services를 사용한 대출 분류): 보험 데이터를 기반으로 하는 종단 간 시나리오입니다. 필요는 **변형** 패키지 합니다.
+ [그래프 및 R을 사용 하는 점도 만들기](../../advanced-analytics/tutorials/walkthrough-create-graphs-and-plots-using-r.md)

## <a name="conclusions"></a>결론

R 및 SQL Server를 통합하면 고성능 데이터 처리 및 빠른 R 분석을 위해 R 및 관계형 데이터베이스의 최고 기능을 이용하여 R 솔루션을 대규모로 더 쉽게 배포할 수 있습니다. 

이러한 추가 리소스에 대 한 자세한 R 예제 참조:

+  [SQL Server R 자습서](../../advanced-analytics/tutorials/sql-server-r-tutorials.md)

    SQL server에서는 R을 사용 하 여 종단 간 시나리오를 Microsoft 데이터 과학 및 R 서비스 개발 팀에서 만든 솔루션에 대 한 학습을 계속 합니다.

+ [SQL Server Python 자습서](../../advanced-analytics/tutorials/sql-server-python-tutorials.md)

    SQL Server 2017 년에 대 한 Python 언어와 함께 원격 계산 컨텍스트 및 확장 가능한 알고리즘의 기능을 사용 합니다.

+ [자습서 및 Microsoft R에 대 한 예제 데이터](https://docs.microsoft.com/r-server/r/tutorial-introduction)

    새 RevoScaleR 패키지를 사용 하 여 모델을 만들고 데이터를 변환 하는 방법에 알아봅니다.

+ [MicrosoftML 시작](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)

    학습 알고리즘 Microsoft Research에서 신속 하 고 확장 가능한 컴퓨터에 대해 자세히 알아보기
