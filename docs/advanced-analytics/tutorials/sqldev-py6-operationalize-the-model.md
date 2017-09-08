---
title: "6 단계: 모델을 운용 | Microsoft Docs"
ms.custom: 
ms.date: 05/25/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- python-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b33f3876f054d7e7150a18967d5cfa37dd2d82bf
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="step-6-operationalize-the-model"></a>6단계: 모델 운영화

이 단계에 알아봅니다를 *운영 화* 모델을 학습 하 고 이전 단계에서 저장 합니다. 이 경우 "모델 점수 매기기에 대 한 프로덕션 환경에 배포 하 는" 의미를 운영 화 합니다. Python 코드는 저장된 프로시저에 포함 되어 있으면 작업을 수행 하는 것과 쉽습니다. 그런 다음 새 관찰 예측을 할 응용 프로그램에서 저장된 프로시저를 호출할 수 있습니다.

저장된 프로시저에서 Python 모델을 호출 하는 두 가지 방법에 알아봅니다.

- **일괄 처리 점수 매기기 모드**: SELECT 쿼리를 사용하여 여러 행의 데이터를 제공합니다. 저장 프로시저에서 입력 사례에 해당하는 관찰 테이블을 반환합니다.
- **개별 점수 매기기 모드**: 개별 매개 변수 값 집합을 입력으로 전달합니다.  저장 프로시저에서 단일 행 또는 값을 반환합니다.

## <a name="scoring-using-the-scikit-learn-model"></a>scikit를 사용 하 여 점수 매기기-모델을 배우기

저장된 프로시저 _PredictTipSciKitPy_ 는 scikit를 사용 하 여-모델을 배우기. 이 저장된 프로시저는 저장된 프로시저에 대 한 Python 예측 호출을 배치 하기 위한 기본 구문을 보여 줍니다.

- 사용할 모델의 이름은 저장된 프로시저에 입력된 매개 변수로 제공 됩니다. 
- 저장된 프로시저는 데이터베이스 테이블에서 serialize 된 모델을 로드한 다음 `nyc_taxi_models`.table, 저장된 프로시저의 SELECT 문에 사용 합니다.
- Serialize 된 모델 Python 변수에 저장 `mod` 추가 처리를 위해 Python을 사용 하 여 합니다.
- 기록 하는 새 사례를 얻은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 에 지정 된 쿼리 `@input_data_1`합니다. 쿼리 데이터를 읽으면 행이 기본 데이터 프레임 `InputDataSet`에 저장됩니다.
- 이 데이터 프레임에 전달 되는 `predict_proba` 로지스틱 회귀 모델의 기능 `mod`, scikit를 사용 하 여 만든-모델을 배우기. 
- `predict_proba` 함수 (`probArray = mod.predict_proba(X)`) 반환는 **float** (시간 관계)의 팁 제공 될 확률을 나타내는입니다.
- 또한 저장된 프로시저는 정확도 메트릭에 AUC (곡선 아래의 영역)을 계산합니다. AUC 같은 정확도 메트릭은 대상 레이블 (예: 기울어진된 열)도 제공 하는 경우에 생성할 수 있습니다. 예측 대상 레이블에 필요는 없습니다 (변수 `y`)를 지원 하지만 정확도 메트릭 계산 않습니다.

  따라서를 매길 데이터에 대 한 대상 레이블을 설정 하지 않은 경우 AUC 계산을 제거 하려면 저장된 프로시저를 수정 하 수 단순히 기능에서 팁 확률을 반환할 (변수 `X` 저장된 프로시저에서).

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
        import pandas;
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

## <a name="scoring-using-the-revoscalepy-model"></a>Revoscalepy 모델을 사용 하 여 점수 매기기

저장된 프로시저 _PredictTipRxPy_ 사용 하 여 만든 모델을 사용 하 여 **revoscalepy** 라이브러리입니다. 거의 동일한 방법으로 작동는 _PredictTipSciKitPy_ 프로시저에 대 한 일부 변경 되어는 **revoscalepy** 함수입니다.

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
      import pandas;
      from sklearn import metrics
      from revoscalepy.functions.RxPredict import rx_predict_ex;
      
      mod = pickle.loads(lmodel2)
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      y = numpy.ravel(InputDataSet[["tipped"]])
      
      probArray = rx_predict_ex(mod, X)
      probList = []
      for i in range(len(probArray._results["tipped_Pred"])):
        probList.append((probArray._results["tipped_Pred"][i]))
      
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

## <a name="batch-scoring-using-a-select-query"></a>SELECT 쿼리를 사용하는 일괄 처리 점수 매기기

저장된 프로시저 **PredictTipSciKitPy** 및 **PredictTipRxPy** 두 개의 입력 매개 변수가 필요 합니다. 

- 점수 매기기에 대 한 데이터를 검색 하는 쿼리
- 학습된 된 모델의 이름

이 섹션에서는 모델 및 점수 매기기에 사용 되는 데이터를 쉽게 변경 하는 저장된 프로시저에 이러한 인수를 전달 하는 방법을 배웁니다.

1. 입력된 데이터를 정의 하 고 다음과 같이 점수 매기기에 대 한 저장된 프로시저를 호출 합니다. 이 예제에서는 상태 평가 대 한 PredictTipSciKitPy 저장된 프로시저를 사용 하 고 모델의 이름 및 쿼리 문자열에 전달

    ```SQL
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipSciKitPy] 'SciKit_model', @query_string;
    ```

    저장된 프로시저에서 입력 쿼리의 일환으로 전달 된 각 시에 대 한 예측된 확률을 반환 합니다. SSMS (SQL Server Management Studio)를 쿼리를 실행 하는 데 사용 하는 확률을 예측에 테이블로 표시 됩니다는 **결과** 창. **메시지** 창 출력 약 0.56 값의 정확도 메트릭을 (AUC 또는 곡선 아래의 영역이).

2. 사용 하 여 **revoscalepy** 점수 매기기에 대 한 모델, 저장된 프로시저를 호출 **PredictTipRxPy**모델 이름 및 쿼리 문자열에 전달 합니다.

    ```SQL
    EXEC [dbo].[PredictTipRxPy] 'revoscalepy_model', @query_string;
    ```

## <a name="score-individual-rows-using-scikit-learn-model"></a>Scikit를 사용 하 여 개별 행의 점수를 매길-모델을 배우기

경우에 따라 일괄 처리 점수 매기기 대신 전달 하려면 단일 사례에서 응용 프로그램에서 값 가져오기 하 고 해당 값을 기반으로 단일 결과 산출 합니다. 예를 들어 저장 프로시저를 호출하고 사용자가 입력 또는 선택한 입력을 제공하도록 Excel 워크시트, 웹 응용 프로그램 또는 Reporting Services 보고서를 설정할 수 있습니다.

이 섹션에서는 저장된 프로시저를 호출 하 여 단일 예측을 만드는 방법을 배웁니다.

1. 저장된 프로시저의 코드를 검토 하는 데 1 분 소요 [PredictTipSingleModeSciKitPy](#PredictTipSingleModeSciKitPy) 및 [PredictTipSingleModeRxPy](#PredictTipSingleModeRxPy)는 다운로드의 일부로 포함 됩니다. 이러한 저장된 프로시저는 scikit 사용-자세한 내용은 및 revoscalepy 모델 다음과 같이 점수 매기기를 수행 하 고:

  - 모델의 이름 및 여러 개의 단일 값을 입력으로 제공 됩니다. 이러한 입력 승객 개수, 여행 거리 등을 포함 합니다.
  - 테이블 반환 함수 `fnEngineerFeatures`에서는 입력된 값을 사용 하 고는 거리를 위 도와 경도 변환 합니다. [4 단원](sqldev-py4-create-data-features-using-t-sql.md) 이 테이블 반환 함수에 대 한 설명을 포함 합니다.
  - 외부 응용 프로그램에서 저장된 프로시저를 호출 하는 경우 입력된 데이터에 필요한 Python 모델의 입력된 기능와 일치 하는지 확인 합니다. 이 캐스팅 또는 Python 데이터 형식 또는 데이터 형식 유효성 검사 및 데이터 길이 입력된 데이터를 변환에 포함 될 수 있습니다.
  - 저장된 프로시저는 저장 된 Python 모델을 기반으로 하는 점수를 만듭니다.

### <a name="predicttipsinglemodescikitpy"></a>PredictTipSingleModeSciKitPy

사용 하 여 점수 매기기를 수행 하는 저장된 프로시저의 정의 다음과 같습니다는 **scikit-자세한** 모델입니다.

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
      import pandas;
      
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

다음은 사용 하 여 점수 매기기를 수행 하는 저장된 프로시저의 정의 **revoscalepy** 모델입니다.

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
      import pandas;
      from revoscalepy.functions.RxPredict import rx_predict_ex;
      
      # Load model and unserialize
      mod = pickle.loads(model)
      
      # Get features for scoring from input data
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      
      # Score data to get tip prediction probability as a list (of float)
      
      probArray = rx_predict_ex(mod, X)
      
      probList = []
      probList.append(probArray._results["tipped_Pred"])
      
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

2.  사용해 보려면, 새로운 열고 **쿼리** 창과 각 기능 열에 대 한 매개 변수를 입력 하 고 저장된 프로시저를 호출 합니다.

    ```SQL
    -- Call stored procedure PredictTipSingleModeSciKitPy to score using SciKit-Learn model
    EXEC [dbo].[PredictTipSingleModeSciKitPy] 'linear_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    -- Call stored procedure PredictTipSingleModeRxPy to score using revoscalepy model
    EXEC [dbo].[PredictTipSingleModeRxPy] 'revoscalepy_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```
    
    7 개의 값은 순서 대로 이러한 기능 열:
    
    -   *passenger_count*
    -   *trip_distance*
    -   *trip_time_in_secs*
    -   *pickup_latitude*
    -   *pickup_longitude*
    -   *dropoff_latitude*
    -   *dropoff_longitude*

3. 두 절차는 출력은 택시 여행 위의 매개 변수 또는 기능 사용에 대 한 비용을 지불 하지 팁의 확률입니다.

## <a name="conclusions"></a>결론

이 자습서에서는 저장된 프로시저에 포함 된 Python 코드를 사용 하는 방법을 배웠습니다. 와 통합 [!INCLUDE[tsql](../../includes/tsql-md.md)] 훨씬 쉽게 예측에 대 한 Python 모델을 배포 하 고 모델 재교육 엔터프라이즈 데이터 워크플로의 일부분으로 통합할 수 있습니다.

## <a name="previous-step"></a>이전 단계
[6단계: 모델 운영화](sqldev-py6-operationalize-the-model.md)

## <a name="see-also"></a>관련 항목:

[기계 학습 Python 사용 하 여 서비스](../python/sql-server-python-services.md)

