---
title: 6 단계 SQL Server를 사용 하 여 Python 모델을 운용 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: aedd6beeb720c24a6960950abc6a29c1bf89a5fa
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31203475"
---
# <a name="step-6-operationalize-the-python-model-using-sql-server"></a>6 단계: SQL Server를 사용 하 여 Python 모델을 운용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 자습서의 일부는 [SQL 개발자를 위해 데이터베이스에서 Python 분석](sqldev-in-database-python-for-sql-developers.md)합니다. 

이 단계에서는 방법을 배웁니다 *운영 화* 모델을 학습 하 고 이전 단계에서 저장 합니다.

이 시나리오에서는 해결해줍니다 점수를 매기기 위해 프로덕션 환경에 모델을 배포 하 의미 합니다. SQL Server와의 통합을 사용이 상당히 쉽게 있으므로 저장된 프로시저에서 Python 코드를 포함할 수 있습니다. 새 입력을 기반으로 모델에서 예측을 구하려면 응용 프로그램에서 저장된 프로시저를 호출 하 고 새 데이터를 전달 하기만 됩니다.

이 단원에서는 Python 모델을 기반으로 예측을 만드는 두 가지 방법을 보여 줍니다: 일괄 점수 매기기 및 행을 평가 합니다.

- **일괄 처리 점수 매기기:** 여러 행의 입력된 데이터를 제공 하려면 SELECT 쿼리를 인수로 저장된 프로시저에 전달 합니다. 결과 입력된 사례에 해당 하는 데이터의 테이블입니다.
- **개별 점수 매기기:** 개별 매개 변수 값 집합을 입력으로 전달 합니다.  저장 프로시저에서 단일 행 또는 값을 반환합니다.

점수 매기기에 필요한 모든 Python 코드는 저장된 프로시저의 일부로 제공 됩니다.

| 저장된 프로시저 이름 | 일괄 처리 또는 단일 | 모델 원본|
|----|----|----|
|PredictTipRxPy|일괄 처리(batch)| revoscalepy 모델|
|PredictTipSciKitPy|일괄 처리(batch) |scikit-모델을 배우기|
|PredictTipSingleModeRxPy|단일 행| revoscalepy 모델|
|PredictTipSingleModeSciKitPy|단일 행| scikit-모델을 배우기|

## <a name="batch-scoring"></a>일괄 처리 채점

처음 두 개의 저장된 프로시저는 저장된 프로시저에 대 한 Python 예측 호출을 배치 하기 위한 기본 구문을 보여 줍니다. 두 저장된 프로시저는 데이터 테이블을 입력으로 필요합니다.

- 사용할 정확한 모델의 이름은 저장된 프로시저에 입력된 매개 변수로 제공 됩니다. 저장된 프로시저는 데이터베이스 테이블에서 serialize 된 모델을 로드 `nyc_taxi_models`.table, 저장된 프로시저의 SELECT 문에 사용 합니다.
- Serialize 된 모델 Python 변수에 저장 `mod` 추가 처리를 위해 Python을 사용 하 여 합니다.
- 기록 하는 새 사례를 얻은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 에 지정 된 쿼리 `@input_data_1`합니다. 쿼리 데이터를 읽으면 행이 기본 데이터 프레임 `InputDataSet`에 저장됩니다.
- 두 저장된 프로시저에서 함수를 사용할 `sklearn` 는 정확도 메트릭에 AUC (곡선 아래의 영역)을 계산 하 합니다. AUC 같은 정확도 메트릭을 대상 레이블에 제공 하는 경우에 생성 수 (의 _크리스마스_ 열)입니다. 예측 대상 레이블에 필요는 없습니다 (변수 `y`)를 지원 하지만 정확도 메트릭 계산 않습니다.

    따라서를 매길 데이터에 대 한 대상 레이블을 설정 하지 않은 경우 AUC 계산을 제거 하려면 저장된 프로시저를 수정 하 수 기능에서 팁 확률만 반환 (변수 `X` 저장된 프로시저에서).

### <a name="predicttipscikitpy"></a>PredictTipSciKitPy

저장된 프로시저는 이미 만들어져 있습니다. 를 찾을 수 없는 경우 저장된 프로시저를 만드는 다음 T-SQL 문을 실행 합니다.

이 저장된 프로시저는 scikit를 기반으로 모델에 필요한 액세스 하는 패키지에 특정 함수를 사용 하기 때문에 패키지에 알아봅니다.

+ 입력을 포함 하는 데이터 프레임에 전달 되는 `predict_proba` 로지스틱 회귀 모델의 기능 `mod`합니다. `predict_proba` 함수 (`probArray = mod.predict_proba(X)`) 반환는 **float** (시간 관계)의 팁 제공 될 확률을 나타내는입니다.

```SQL
CREATE PROCEDURE [dbo].[PredictTipSciKitPy] (@model varchar(50), @inquery nvarchar(max))
AS
BEGIN
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
  EXEC sp_execute_external_script
    @language = N'Python',
    @script = N'
        import pickle;
        import numpy;
        from sklearn import metrics
        
        mod = pickle.loads(lmodel2)
        
        X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
        y = numpy.ravel(InputDataSet[["tipped"]])
        
        probArray = mod.predict_proba(X)
        probList = []
        for i in range(len(probArray)):
          probList.append((probArray[i])[1])
        
        probArray = numpy.asarray(probList)
        fpr, tpr, thresholds = metrics.roc_curve(y, probArray)
        aucResult = metrics.auc(fpr, tpr)
        print ("AUC on testing data is: " + str(aucResult))
        
        OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
        ',  
    @input_data_1 = @inquery,
    @input_data_1_name = N'InputDataSet',
    @params = N'@lmodel2 varbinary(max)',
    @lmodel2 = @lmodel2
  WITH RESULT SETS ((Score float));
END
GO
```

### <a name="predicttiprxpy"></a>PredictTipRxPy

이 저장된 프로시저 같은 입력을 사용 하 여를 이전 저장된 프로시저와 같은 유형의 점수를 생성 하지만에서 기능을 사용 하 여 **revoscalepy** 기계 학습 SQL Server와 함께 제공 되는 패키지입니다.

> [!NOTE] 
> 이 저장된 프로시저에 대 한 코드는 초기 릴리스 버전 및 revoscalepy 패키지에 대 한 변경 내용을 반영 하도록 RTM 버전 간에 약간 변경 되었습니다. 참조는 [변경](#changes) 세부 정보에 대 한 테이블입니다.

```SQL
CREATE PROCEDURE [dbo].[PredictTipRxPy] (@model varchar(50), @inquery nvarchar(max))
AS
BEGIN
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models2 where name = @model);

  EXEC sp_execute_external_script 
    @language = N'Python',
    @script = N'
      import pickle;
      import numpy;
      from sklearn import metrics
      from revoscalepy.functions.RxPredict import rx_predict;
      
      mod = pickle.loads(lmodel2)
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      y = numpy.ravel(InputDataSet[["tipped"]])
      
      probArray = rx_predict(mod, X)
      prob_list = prob_array["tipped_Pred"].values 
      
      probArray = numpy.asarray(probList)
      fpr, tpr, thresholds = metrics.roc_curve(y, probArray)
      aucResult = metrics.auc(fpr, tpr)
      print ("AUC on testing data is: " + str(aucResult))
      OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
      ',    
    @input_data_1 = @inquery,
    @input_data_1_name = N'InputDataSet',
    @params = N'@lmodel2 varbinary(max)',
    @lmodel2 = @lmodel2
  WITH RESULT SETS ((Score float));
END
GO
```

## <a name="run-batch-scoring-using-a-select-query"></a>일괄 처리 선택 쿼리를 사용 하 여 점수 매기기 실행

저장된 프로시저 **PredictTipSciKitPy** 및 **PredictTipRxPy** 두 개의 입력 매개 변수가 필요 합니다. 

- 점수 매기기에 대 한 데이터를 검색 하는 쿼리
- 학습된 된 모델의 이름

저장된 프로시저에 이러한 인수를 전달 하 여 특정 모델을 선택 하거나 점수 매기기에 사용 되는 데이터를 변경할 수 있습니다.

1. 사용 하는 **scikit-자세한** 점수 매기기에 대 한 모델, 저장된 프로시저를 호출 **PredictTipSciKitPy**모델 이름을 전달 하 고 입력으로 쿼리 문자열입니다.

    ```SQL
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipSciKitPy] 'SciKit_model', @query_string;
    ```

    저장된 프로시저에서 입력 쿼리의 일환으로 전달 된 각 시에 대 한 예측된 확률을 반환 합니다. 
    
    SSMS (SQL Server Management Studio)를 쿼리를 실행 하는 데 사용 하는 확률을 예측에 테이블로 표시 됩니다는 **결과** 창. **메시지** 창 출력 약 0.56 값의 정확도 메트릭을 (AUC 또는 곡선 아래의 영역이).

2. 사용 하 여 **revoscalepy** 점수 매기기에 대 한 모델, 저장된 프로시저를 호출 **PredictTipRxPy**모델 이름을 전달 하 고 쿼리 문자열을 입력으로 합니다.

    ```SQL
    EXEC [dbo].[PredictTipRxPy] 'revoscalepy_model', @query_string;
    ```

## <a name="single-row-scoring"></a>단일 행의 점수 매기기

경우에 따라 일괄 처리 점수 매기기 대신 수 전달 하려는 단일 사례에서 응용 프로그램에서 값을 가져오고 해당 값을 기반으로 하는 단일 결과 반환 합니다. 예를 들어는 Excel 워크시트, 웹 응용 프로그램 또는 보고서를 저장된 프로시저를 호출를 설정할 수 있습니다 및 형식화 된 또는 선택한 사용자가을 입력 하는 전달 합니다.

이 섹션에서는 두 개의 저장된 프로시저를 호출 하 여 단일 예측을 만드는 방법을 배웁니다.

+ [PredictTipSingleModeSciKitPy](#PredictTipSingleModeSciKitPy) 은 단일 행의 scikit를 사용 하 여 점수를 매기기 위해-모델을 배우기.
+ [PredictTipSingleModeRxPy](#PredictTipSingleModeRxPy) 단일 행 revoscalepy 모델을 사용 하 여 점수를 매기기 위해 설계 되었습니다.
+ 모델을 아직 학습 하지 않은 경우 돌아가서 [5 단계](sqldev-py5-train-and-save-a-model-using-t-sql.md)!

두 모델은 일련의 승객 개수, 여행 거리 등과 같은 단일 값을 입력으로 사용 합니다. 테이블 반환 함수 `fnEngineerFeatures`, 거리를 직접, 새로운 기능에 대 한 입력에서 위도 및 경도 값을 변환 하는 데 사용 됩니다. [4 단원](sqldev-py4-create-data-features-using-t-sql.md) 이 테이블 반환 함수에 대 한 설명을 포함 합니다.

두 저장된 프로시저는 Python 모델을 기반으로 한 점수를 작성 합니다.

> [!NOTE]
> 
> 외부 응용 프로그램에서 저장된 프로시저를 호출할 때 Python 모델에 필요한 모든 입력된 기능을 제공 하는 것입니다. 오류를 방지 하려면 캐스팅 하거나 입력된 데이터를 데이터 형식과 데이터 길이 유효성 검사 외에도 Python 데이터 형식으로 변환할 할 수 있습니다.

### <a name="predicttipsinglemodescikitpy"></a>PredictTipSingleModeSciKitPy

사용 하 여 점수 매기기를 수행 하는 저장된 프로시저의 코드를 검토는 **scikit-자세한** 모델입니다.

```SQL
CREATE PROCEDURE [dbo].[PredictTipSingleModeSciKitPy] (@model varchar(50), @passenger_count int = 0,
  @trip_distance float = 0,
  @trip_time_in_secs int = 0,
  @pickup_latitude float = 0,
  @pickup_longitude float = 0,
  @dropoff_latitude float = 0,
  @dropoff_longitude float = 0)
AS
BEGIN
  DECLARE @inquery nvarchar(max) = N'
  SELECT * FROM [dbo].[fnEngineerFeatures]( 
    @passenger_count,
    @trip_distance,
    @trip_time_in_secs,
    @pickup_latitude,
    @pickup_longitude,
    @dropoff_latitude,
    @dropoff_longitude)
    '
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models2 where name = @model);
  EXEC sp_execute_external_script 
    @language = N'Python',
    @script = N'
      import pickle;
      import numpy;
      
      # Load model and unserialize
      mod = pickle.loads(model)
      
      # Get features for scoring from input data
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      
      # Score data to get tip prediction probability as a list (of float)
      probList = []
      probList.append((mod.predict_proba(X)[0])[1])
      
      # Create output data frame
      OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
    ',
    @input_data_1 = @inquery,
    @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,
      @trip_time_in_secs int ,
      @pickup_latitude float ,
      @pickup_longitude float ,
      @dropoff_latitude float ,
      @dropoff_longitude float',
      @model = @lmodel2,
      @passenger_count =@passenger_count ,
      @trip_distance=@trip_distance,
      @trip_time_in_secs=@trip_time_in_secs,
      @pickup_latitude=@pickup_latitude,
      @pickup_longitude=@pickup_longitude,
      @dropoff_latitude=@dropoff_latitude,
      @dropoff_longitude=@dropoff_longitude
  WITH RESULT SETS ((Score float));
END
GO
```

### <a name="predicttipsinglemoderxpy"></a>PredictTipSingleModeRxPy

다음 저장된 프로시저를 사용 하 여 점수 매기기에서는 **revoscalepy** 모델입니다.

```SQL
CREATE PROCEDURE [dbo].[PredictTipSingleModeRxPy] (@model varchar(50), @passenger_count int = 0,
  @trip_distance float = 0,
  @trip_time_in_secs int = 0,
  @pickup_latitude float = 0,
  @pickup_longitude float = 0,
  @dropoff_latitude float = 0,
  @dropoff_longitude float = 0)
AS
BEGIN
  DECLARE @inquery nvarchar(max) = N'
    SELECT * FROM [dbo].[fnEngineerFeatures]( 
      @passenger_count,
      @trip_distance,
      @trip_time_in_secs,
      @pickup_latitude,
      @pickup_longitude,
      @dropoff_latitude,
      @dropoff_longitude)
    '
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models2 where name = @model);
  EXEC sp_execute_external_script 
    @language = N'Python',
    @script = N'
      import pickle;
      import numpy;
      from revoscalepy.functions.RxPredict import rx_predict;
      
      # Load model and unserialize
      mod = pickle.loads(model)
      
      # Get features for scoring from input data
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      
      # Score data to get tip prediction probability as a list (of float)
      
      probArray = rx_predict(mod, X)
      
      probList = []
      prob_list = prob_array["tipped_Pred"].values
      
      # Create output data frame
      OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
      ',
    @input_data_1 = @inquery,
    @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,
      @trip_time_in_secs int ,
      @pickup_latitude float ,
      @pickup_longitude float ,
      @dropoff_latitude float ,
      @dropoff_longitude float',
      @model = @lmodel2,
      @passenger_count =@passenger_count ,
      @trip_distance=@trip_distance,
      @trip_time_in_secs=@trip_time_in_secs,
      @pickup_latitude=@pickup_latitude,
      @pickup_longitude=@pickup_longitude,
      @dropoff_latitude=@dropoff_latitude,
      @dropoff_longitude=@dropoff_longitude
  WITH RESULT SETS ((Score float));
END
GO
```

### <a name="generate-scores-from-models"></a>모델에서 점수를 생성 합니다.

저장된 프로시저를 만든 후 어느 모델을 기반으로 하 여 점수를 생성 하기 쉽습니다. 새 열기만 **쿼리** 창과 각 기능 열에 대 한 매개 변수를 입력 하거나 붙여 넣습니다. 7 개의 순서에서 이러한 기능 열의 값이 필요 합니다.
    
+ *passenger_count*
+ *trip_distance* v*trip_time_in_secs*
+ *pickup_latitude*
+ *pickup_longitude*
+ *dropoff_latitude*
+ *dropoff_longitude*

1. 사용 하 여 예측을 생성 하는 **revoscalepy** 모델에서이 문을 실행 합니다.
  
    ```SQL
    EXEC [dbo].[PredictTipSingleModeRxPy] 'revoscalepy_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

2. 사용 하 여 점수를 생성 하는 **scikit-자세한** 모델에서이 문을 실행:

    ```SQL
    EXEC [dbo].[PredictTipSingleModeSciKitPy] 'linear_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

두 절차 모두에서 출력은 지정 된 매개 변수 또는 기능으로 택시 여행에 대 한 비용을 지불 하지 팁의 확률.

### <a name="changes"></a> 변경 내용

이 섹션에서는이 자습서에 사용 되는 코드 변경 내용을 나열 합니다. 최신 값을 반영 하는 변경 **revoscalepy** 버전입니다. API 도움말 참조 [Python 함수 라이브러리 참조](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)합니다.

| 세부 정보를 변경 합니다. | 참고|
| ----|----|
| 삭제 `import pandas` 모든 샘플의| 이제 기본적으로 로드 팬더|
| 함수 `rx_predict_ex` 로 변경 `rx_predict`| RTM 및 시험판 버전 필요 `rx_predict_ex`|
| 함수 `rx_logit_ex` 로 변경 `rx_logit`| RTM 및 시험판 버전 필요 `rx_logit_ex`|
| ` probList.append(probArray._results["tipped_Pred"])` 로 변경 `prob_list = prob_array["tipped_Pred"].values`| API에 대 한 업데이트|

시험판 버전의 SQL Server 2017를 사용 하 여 Python 서비스를 설치한 경우 업그레이드 하는 것이 좋습니다. 또한 학습 서버 컴퓨터의 최신 릴리스를 사용 하 여 방금 Python 및 R 구성 요소를 업그레이드할 수 있습니다. 자세한 내용은 참조 [바인딩을 사용 하 여 SQL Server의 인스턴스를 업그레이드 하려면](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다.

## <a name="conclusions"></a>결론

이 자습서에서는 저장된 프로시저에 포함 된 Python 코드를 사용 하는 방법을 배웠습니다. 와 통합 [!INCLUDE[tsql](../../includes/tsql-md.md)] 훨씬 쉽게 예측에 대 한 Python 모델을 배포 하 고 모델 재교육 엔터프라이즈 데이터 워크플로의 일부분으로 통합할 수 있습니다.

## <a name="previous-step"></a>이전 단계

[5 단계: 학습 및 Python 모델 저장](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="see-also"></a>참고 항목

[기계 학습 Python 사용 하 여 서비스](../python/sql-server-python-services.md)
