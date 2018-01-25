---
title: "4 단원: T-SQL을 사용 하 여 데이터 기능 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2016
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2016
dev_langs:
- R
- TSQL
ms.assetid: 5b2f4c44-6192-40df-abf1-fc983844f1d0
caps.latest.revision: "10"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 1690e397903ce5c0a5776b6c5c87110f195930aa
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="lesson-4-create-data-features-using-t-sql"></a>4 단원: T-SQL을 사용 하 여 데이터 기능 만들기

이 문서는 SQL Server에서 R을 사용 하는 방법에 대 한 SQL 개발자를 위한 자습서의 일부입니다.

이 단계에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수를 사용하여 원시 데이터에서 기능을 만드는 방법을 알아봅니다. 그런 다음 저장 프로시저에서 해당 함수를 호출하여 기능 값이 포함된 테이블을 만듭니다.

## <a name="about-feature-engineering"></a>기능 엔지니어링 팀에 대 한

데이터 탐색을 여러 번 수행한 후 데이터에서 몇 가지 유용한 정보를 수집했으며 *기능 엔지니어링*으로 넘어갈 준비가 되었습니다. 원시 데이터에서 의미 있는 기능을 만드는이 과정은 분석 모델을 만드는 중요 한 단계입니다.

이 데이터 집합에 거리 값 미터 보고 된 거리에 기반 하며 지리적 거리 또는 짧아 지도록에 실제 거리가 반드시 나타내지 마세요. 따라서 원본 NYC Taxi 데이터 집합에서 사용할 수 있는 좌표를 통해 승하차 지점 사이의 직접 거리를 계산해야 합니다. 이렇게 하려면 사용자 지정 [함수에](https://en.wikipedia.org/wiki/Haversine_formula) Haversine 수식 [!INCLUDE[tsql](../../includes/tsql-md.md)] 을 사용합니다.

사용자 지정 T-SQL 함수 _fnCalculateDistance_를 사용하여 Haversine 수식을 통해 거리를 계산하고 두 번째 사용자 지정 T-SQL 함수 _fnEngineerFeatures_를 사용하여 모든 기능이 포함된 테이블을 만듭니다.

전체 프로세스는 다음과 같습니다.

- 계산을 수행 하는 T-SQL 함수 만들기

- 기능 데이터를 생성 하는 함수를 호출 합니다.

- 기능 데이터를 테이블에 저장

## <a name="calculate-trip-distance-using-fncalculatedistance"></a>FnCalculateDistance를 사용 하 여 여행 거리를 계산 합니다.

함수 _fnCalculateDistance_ 해야 다운로드 되 고 등록 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이 자습서를 준비 하는 과정의 일환으로 합니다. 코드를 검토 하는 데 1 분을 소요 됩니다.
  
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

## <a name="generate-the-features-using-fnengineerfeatures"></a>사용 하 여 기능 생성 _fnEngineerFeatures_

모델 학습에 사용할 수 있는 테이블에 계산 된 값을 추가 하려면 다른 함수를 사용 합니다 _fnEngineerFeatures_합니다. 이전에 만든된 T-SQL 함수를 호출 하는 새 함수 _fnCalculateDistance_, 선택 및 자동 전송 위치 간에 직접 거리를 얻으려고 합니다. 

1. 이 연습을 위한 준비 과정에서 만들어진 사용자 지정 T-SQL 함수 _fnEngineerFeatures_의 코드를 검토합니다.
  
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

    + 입력으로 여러 열을 사용 하 고 여러 기능 열이 있는 테이블을 출력 하는이 테이블 반환 함수입니다.

    + 이러한 함수의 용도 모델 작성에 사용 하기 위해 새로운 기능을 만드는 것입니다.

2.  이 함수에서 작동 하는지를 확인 하려면 요금된 거리는 않았지만 곳에서 선택 및 자동 전송 위치 다른 이러한 왕복에 대 한 지리적 거리를 계산 하려면 사용 합니다.
  
    ```SQL
        SELECT tipped, fare_amount, passenger_count,(trip_time_in_secs/60) as TripMinutes,
        trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) AS direct_distance
        FROM nyctaxi_sample
        WHERE pickup_longitude != dropoff_longitude and pickup_latitude != dropoff_latitude and trip_distance = 0
        ORDER BY trip_time_in_secs DESC
    ```
  
    확인한 것처럼 미터에서 보고된 거리가 항상 지리적 거리와 일치하는 것은 아닙니다. 이 때문에 기능 엔지니어링이 중요합니다. 오른쪽을 사용 하 여 기계 학습 모델을 학습 하 이러한 향상 된 데이터 기능을 사용할 수 있습니다.

## <a name="next-lesson"></a>다음 단원

[5 단원: 학습 및 T-SQL을 사용 하 여 모델 저장](../r/sqldev-train-and-save-a-model-using-t-sql.md)

## <a name="previous-lesson"></a>이전 단원

[3 단원: 탐색 하 고 데이터를 시각화 합니다.](../tutorials/sqldev-explore-and-visualize-the-data.md)
