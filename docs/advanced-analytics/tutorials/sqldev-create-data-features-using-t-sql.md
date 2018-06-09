---
title: T-SQL 함수 (SQL Server 기계 학습)를 사용 하 여 4 합니다 데이터 기능 단원 | Microsoft Docs
description: SQL Server에서 R을 포함 하는 방법을 보여 주는 자습서 저장 프로시저 및 T-SQL 함수
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/07/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 98182e8e602b8bba8ca7d7fd58cf23f3fcaaa435
ms.sourcegitcommit: b52b5d972b1a180e575dccfc4abce49af1a6b230
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2018
ms.locfileid: "35249546"
---
# <a name="lesson-4-create-data-features-using-r-and-t-sql"></a>4 단원: R 및 T-SQL을 사용 하 여 데이터 기능 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 SQL Server에서 R을 사용 하는 방법에 대 한 SQL 개발자를 위한 자습서의 일부입니다.

이 단계에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수를 사용하여 원시 데이터에서 특성을 만드는 방법을 알아봅니다. 그런 다음 저장 프로시저에서 해당 함수를 호출하여 특성 값이 포함된 테이블을 만듭니다.

## <a name="about-feature-engineering"></a>특성 엔지니어링 정보

데이터 탐색을 여러 번 수행한 후 데이터에서 몇 가지 유용한 정보를 수집했으며 *특성 엔지니어링*으로 넘어갈 준비가 되었습니다.  원시 데이터에서 의미 있는 특성을 만드는 이 과정은 분석 모델을 만드는 중요한 단계입니다.

이 데이터 집합에 보고된 미터 거리를 기반으로 하며 이동한 지리적 거리 또는 실제 거리를 나타내는 것은 아닙니다. 따라서 NYC 택시 데이터 소스에서 사용 가능한 좌표를 사용하여 승차 위치와 하차 위치 사이의 직접 거리를 계산해야 합니다. 이렇게 하려면 사용자 지정 [함수에](https://en.wikipedia.org/wiki/Haversine_formula) Haversine 수식 [!INCLUDE[tsql](../../includes/tsql-md.md)] 을 사용합니다.

사용자 지정 T-SQL 함수 _fnCalculateDistance_를 사용하여 Haversine 수식을 통해 거리를 계산하고 두 번째 사용자 지정 T-SQL 함수 _fnEngineerFeatures_를 사용하여 모든 기능이 포함된 테이블을 만듭니다.

전체 프로세스는 다음과 같습니다.

- 계산을 수행 하는 T-SQL 함수 만들기

- 특성 데이터를 생성하는 함수를 호출합니다

- 특성 데이터를 테이블에 저장하기

## <a name="calculate-trip-distance-using-fncalculatedistance"></a>FnCalculateDistance를 사용한 여정 거리 계산

이 자습서 준비의 일부로 _fnCalculateDistance_ 함수를 다운로드하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 등록해야 합니다. 잠시 시간을 내어 코드를 검토하십시오.
  
1. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 **프로그래밍 기능**, **함수** , **스칼라 반환 함수**를 차례로 확장합니다.   

2. _fnCalculateDistance_를 마우스 오른쪽 단추로 클릭하고 **수정** 을 선택하여 새 쿼리 창에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 엽니다.
  
    ```SQL
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)  
    -- User-defined function that calculates the direct distance between two geographical coordinates.  
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
  
    - 함수는 스칼라 반환 함수이며, 미리 정의된 형식의 단일 데이터 값을 반환합니다.
  
    - 여정 승하차 위치에서 얻은 위도 및 경도 값을 입력으로 사용합니다. Haversine 수식은 위치를 라디안으로 변환하고 해당 값을 사용하여 두 위치 사이의 직접 거리(마일)를 계산합니다.

## <a name="generate-the-features-using-fnengineerfeatures"></a>_fnEngineerFeatures_ 를 사용하여 특성 생성

모델 학습에 사용할 수 있는 테이블에 계산된 값을 추가하려면 _fnEngineerFeatures_ 라는 다른 함수를 사용합니다. 새 함수는 이전에 생성된 T-SQL 함수 _fnCalculateDistance_ 를 호출하여 승차 지점과 하차 위치 사이의 직접적인 거리를 구합니다. 

1. 잠시 시간을 내어 이 연습을 준비하는 과정에서 작성해야 하는 사용자 정의 T-SQL 함수인 _fnEngineerFeatures_ 에 대한 코드를 검토하십시오.
  
    ```SQL
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

    + 이 테이블 반환 함수는 여러 열을 입력으로 취하고 여러 특성 열을 가진 테이블을 반환합니다.

    + 이 함수의 목적은 모델 작성에 사용할 새로운 특성을 만드는 것입니다.

2.  측정 거리가 0이지만 승차 및 하차 위치가 다른 이동의 지리적 거리 계산을 통해 이 함수가 작동하는지 확인할 수 있습니다.
  
    ```SQL
        SELECT tipped, fare_amount, passenger_count,(trip_time_in_secs/60) as TripMinutes,
        trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) AS direct_distance
        FROM nyctaxi_sample
        WHERE pickup_longitude != dropoff_longitude and pickup_latitude != dropoff_latitude and trip_distance = 0
        ORDER BY trip_time_in_secs DESC
    ```
  
    확인한 것처럼 미터에서 보고된 거리가 항상 지리적 거리와 일치하는 것은 아닙니다. 이런 이유로 특성 엔지니어링이 중요합니다. 이러한 향상된 데이터 특성으로 R을 사용한 Machine Learning 모델을 학습할 수 있습니다.

## <a name="next-lesson"></a>다음 단원

[5 단원: T-SQL을 사용하여 모델 학습 및 저장](../r/sqldev-train-and-save-a-model-using-t-sql.md)

## <a name="previous-lesson"></a>이전 단원

[3 단원: 탐색 하 고 R 및 저장된 프로시저를 사용 하 여 데이터를 시각화 합니다.](../tutorials/sqldev-explore-and-visualize-the-data.md)
