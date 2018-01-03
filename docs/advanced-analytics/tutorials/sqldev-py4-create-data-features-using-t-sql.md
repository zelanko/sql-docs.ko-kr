---
title: "4단계: T-SQL을 사용하여 데이터 기능 만들기 | Microsoft 문서"
ms.custom: 
ms.date: 10/17/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: "2"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 8768c420e8cb2911a2e48d93944430e67dceb3fb
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2017
---
# <a name="step-4-create-data-features-using-t-sql"></a>4단계: T-SQL을 사용하여 데이터 기능 만들기

데이터 탐색 후 데이터에서 몇 가지 정보를 수집 하 고이로 이동 준비가 *엔지니어링 기능*합니다. 이 프로세스는 원시 데이터에서 기능을 만드는 모델링 하는 고급 분석에 중요 한 단계 될 수 있습니다.

이 문서는 자습서의 일부는 [SQL 개발자를 위해 데이터베이스에서 Python 분석](sqldev-in-database-python-for-sql-developers.md)합니다. 

이 단계에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수를 사용하여 원시 데이터에서 기능을 만드는 방법을 알아봅니다. 그런 다음 저장 프로시저에서 해당 함수를 호출하여 기능 값이 포함된 테이블을 만듭니다.

## <a name="define-the-function"></a>함수 정의

원래 데이터에 보고된 거리 값은 보고된 미터 거리를 기반으로 하며 지리적 거리 또는 이동한 거리를 나타내지 않을 수도 있습니다. 따라서 원본 NYC Taxi 데이터 집합에서 사용할 수 있는 좌표를 통해 승하차 지점 사이의 직접 거리를 계산해야 합니다. 이렇게 하려면 사용자 지정 [함수에](https://en.wikipedia.org/wiki/Haversine_formula) Haversine 수식 [!INCLUDE[tsql](../../includes/tsql-md.md)] 을 사용합니다.

사용자 지정 T-SQL 함수 _fnCalculateDistance_를 사용하여 Haversine 수식을 통해 거리를 계산하고 두 번째 사용자 지정 T-SQL 함수 _fnEngineerFeatures_를 사용하여 모든 기능이 포함된 테이블을 만듭니다.

### <a name="calculate-trip-distance-using-fncalculatedistance"></a>FnCalculateDistance를 사용 하 여 여행 거리를 계산 합니다.

1.  이 연습을 위한 준비 과정에서 _fnCalculateDistance_ 함수를 다운로드하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 등록한 상태여야 합니다. 코드를 검토 하는 데 1 분을 소요 됩니다.
  
    [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 **프로그래밍 기능**, **함수** , **스칼라 반환 함수**를 차례로 확장합니다.
    _fnCalculateDistance_를 마우스 오른쪽 단추로 클릭하고 **수정** 을 선택하여 새 쿼리 창에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 엽니다.
  
    ```SQL
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

- 함수는 스칼라 반환 함수이며, 미리 정의된 형식의 단일 데이터 값을 반환합니다.
- 여정 승하차 위치에서 얻은 위도 및 경도 값을 입력으로 사용합니다. Haversine 수식은 위치를 라디안으로 변환하고 해당 값을 사용하여 두 위치 사이의 직접 거리(마일)를 계산합니다.

모델 학습에 사용할 수 있는 테이블에 계산 값을 추가하려면 다른 함수 _fnEngineerFeatures_를 사용합니다.

### <a name="save-the-features-using-fnengineerfeatures"></a>사용 하 여 기능 저장 _fnEngineerFeatures_

1.  이 연습을 위한 준비 과정에서 만들어진 사용자 지정 T-SQL 함수 _fnEngineerFeatures_의 코드를 검토합니다.
  
    이 함수는 여러 열을 입력으로 사용하고 여러 기능 열이 있는 테이블을 출력하는 테이블 반환 함수입니다.  이 함수는 모델 작성에 사용할 기능 집합을 만드는 데 사용됩니다. _fnEngineerFeatures_ 함수는 이전에 만든 T-SQL 함수 _fnCalculateDistance_를 호출하여 승하차 위치 사이의 직접 거리를 가져옵니다.
  
    ```
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
  
    ```
        SELECT tipped, fare_amount, passenger_count,(trip_time_in_secs/60) as TripMinutes,
        trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) AS direct_distance
        FROM nyctaxi_sample
        WHERE pickup_longitude != dropoff_longitude and pickup_latitude != dropoff_latitude and trip_distance = 0
        ORDER BY trip_time_in_secs DESC
    ```
  
    확인한 것처럼 미터에서 보고된 거리가 항상 지리적 거리와 일치하는 것은 아닙니다. 이 때문에 기능 엔지니어링 팀이 중요 합니다.

다음 단계에서 이러한 데이터 기능을 만들고 학습 Python을 사용 하는 기계 학습 모델을 사용 하는 방법을 설명 합니다.

## <a name="next-step"></a>다음 단계

[5 단계: 학습 및 T-SQL을 사용 하 여 Python 모델 저장](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="previous-step"></a>이전 단계

[3단계: 데이터 탐색 및 시각화](sqldev-py3-explore-and-visualize-the-data.md)


