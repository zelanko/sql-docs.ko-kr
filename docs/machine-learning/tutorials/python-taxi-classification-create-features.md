---
title: 'Python 자습서: 데이터 기능 만들기'
titleSuffix: SQL machine learning
description: 이 5부 자습서 시리즈의 3부에서는 SQL Machine Learning을 통해 Python 기계 학습 모델에서 사용할 저장 프로시저에 계산을 추가합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/29/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||>=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: b50750368dd5c8b9d558a587699fde1e7d94af15
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88180357"
---
# <a name="python-tutorial-create-data-features-using-t-sql"></a>Python 자습서: T-SQL을 사용하여 데이터 기능 만들기
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

이 5부 자습서 시리즈의 3부에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수를 사용하여 원시 데이터에서 기능을 만드는 방법을 알아봅니다. 그런 다음 SQL 저장 프로시저에서 해당 함수를 호출하여 기능 값이 포함된 테이블을 만듭니다.

원시 데이터에서 기능을 만드는 이 기능 엔지니어링 프로세스는 고급 분석 모델링에서 중요한 단계가 될 수 있습니다.

이 문서에서는 다음을 수행합니다.

> [!div class="checklist"]
> + 사용자 지정 함수를 수정하여 이동 거리 계산
> + 다른 사용자 지정 함수를 사용하여 기능 저장

[1부](python-taxi-classification-introduction.md)에서는 사전 요구 사항을 설치하고 샘플 데이터베이스를 복원했습니다.

[2부](python-taxi-classification-explore-data.md)에서는 샘플 데이터를 검토하고 몇 가지 플롯을 생성했습니다.

[4부](python-taxi-classification-train-model.md)에서는 SQL Server 저장 프로시저를 통해 모듈을 로드하고 필요한 함수를 호출하여 모델을 만들고 학습시킵니다.

[5부](python-taxi-classification-deploy-model.md)에서는 4부에서 학습시키고 저장한 모델을 운영하는 방법을 알아봅니다.

## <a name="define-the-function"></a>함수 정의

원래 데이터에 보고된 거리 값은 보고된 미터 거리를 기반으로 하며 지리적 거리 또는 이동한 거리를 나타내지 않을 수도 있습니다. 따라서 원본 NYC Taxi 데이터 세트에서 사용할 수 있는 좌표를 통해 승하차 지점 사이의 직접 거리를 계산해야 합니다. 이렇게 하려면 사용자 지정 [함수에](https://en.wikipedia.org/wiki/Haversine_formula) Haversine 수식 [!INCLUDE[tsql](../../includes/tsql-md.md)] 을 사용합니다.

사용자 지정 T-SQL 함수 _fnCalculateDistance_를 사용하여 Haversine 수식을 통해 거리를 컴퓨팅하고 두 번째 사용자 지정 T-SQL 함수 _fnEngineerFeatures_를 사용하여 모든 기능이 포함된 테이블을 만듭니다.

### <a name="calculate-trip-distance-using-fncalculatedistance"></a>fnCalculateDistance를 사용하여 트립 거리 계산

1. _fnCalculateDistance_ 함수는 샘플 데이터베이스에 포함되어 있습니다. 코드를 검토하는 데 몇 분 정도가 걸립니다.
  
2. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 **프로그래밍 기능**, **함수** , **스칼라 반환 함수**를 차례로 확장합니다.
   _fnCalculateDistance_를 마우스 오른쪽 단추로 클릭하고 **수정** 을 선택하여 새 쿼리 창에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 엽니다.
  
   ```sql
   CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)
   -- User-defined function that calculates the direct distance between two geographical coordinates
   RETURNS float
   AS
   BEGIN
     DECLARE @distance decimal(28, 10)
     -- Convert to radians
     SET @Lat1 = @Lat1 / 57.2958
     SET @Long1 = @Long1 / 57.2958
     SET @Lat2 = @Lat2 / 57.2958
     SET @Long2 = @Long2 / 57.2958
     -- Calculate distance
     SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
     --Convert to miles
     IF @distance <> 0
     BEGIN
       SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
     END
     RETURN @distance
   END
   GO
   ```

**참고:**

+ 함수는 스칼라 반환 함수이며, 미리 정의된 형식의 단일 데이터 값을 반환합니다.
+ 여정 승하차 위치에서 얻은 위도 및 경도 값을 입력으로 사용합니다. Haversine 수식은 위치를 라디안으로 변환하고 해당 값을 사용하여 두 위치 사이의 직접 거리(마일)를 컴퓨팅합니다.

모델 학습에 사용할 수 있는 테이블에 계산 값을 추가하려면 다른 함수 _fnEngineerFeatures_를 사용합니다.

### <a name="save-the-features-using-_fnengineerfeatures_"></a>_fnEngineerFeatures_를 사용하여 기능 저장

1. 잠시 시간을 내어 샘플 데이터베이스에 포함된 사용자 지정 T-SQL 함수 _fnEngineerFeatures_의 코드를 검토해 보세요.
  
   이 함수는 여러 열을 입력으로 사용하고 여러 기능 열이 있는 테이블을 출력하는 테이블 반환 함수입니다.  이 함수는 모델 작성에 사용할 기능 집합을 만드는 데 사용됩니다. _fnEngineerFeatures_ 함수는 이전에 만든 T-SQL 함수 _fnCalculateDistance_를 호출하여 승하차 위치 사이의 직접 거리를 가져옵니다.
  
   ```sql
   CREATE FUNCTION [dbo].[fnEngineerFeatures] (
   @passenger_count int = 0,
   @trip_distance float = 0,
   @trip_time_in_secs int = 0,
   @pickup_latitude float = 0,
   @pickup_longitude float = 0,
   @dropoff_latitude float = 0,
   @dropoff_longitude float = 0)
   RETURNS TABLE
   AS
     RETURN
     (
     -- Add the SELECT statement with parameter references here
     SELECT
       @passenger_count AS passenger_count,
       @trip_distance AS trip_distance,
       @trip_time_in_secs AS trip_time_in_secs,
       [dbo].[fnCalculateDistance](@pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude) AS direct_distance
     )
   GO
   ```
  
2. 이 함수가 작동하는지 확인하려면 함수를 사용하여 미터 거리가 0이지만 승하차 위치가 서로 다른 여정의 지리적 거리를 계산합니다.
  
   ```sql
       SELECT tipped, fare_amount, passenger_count,(trip_time_in_secs/60) as TripMinutes,
       trip_distance, pickup_datetime, dropoff_datetime,
       dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) AS direct_distance
       FROM nyctaxi_sample
       WHERE pickup_longitude != dropoff_longitude and pickup_latitude != dropoff_latitude and trip_distance = 0
       ORDER BY trip_time_in_secs DESC
   ```
  
   확인한 것처럼 미터에서 보고된 거리가 항상 지리적 거리와 일치하는 것은 아닙니다. 이 때문에 기능 엔지니어링이 중요합니다.

다음 부분에서는 이러한 데이터 기능을 통해 Python을 사용하여 가계 학습 모델을 만들고 학습하는 방법을 알아봅니다.

## <a name="next-steps"></a>다음 단계

이 문서에서는 다음 작업을 수행합니다.

> [!div class="checklist"]
> + 이동 거리를 계산하는 사용자 지정 함수 수정
> + 다른 사용자 지정 함수를 사용하여 기능 저장

> [!div class="nextstepaction"]
> [Python 자습서: T-SQL을 사용하여 Python 모델 학습 및 저장](python-taxi-classification-train-model.md)