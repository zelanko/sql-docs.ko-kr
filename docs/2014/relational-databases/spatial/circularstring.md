---
title: CircularString | Microsoft 문서
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 9fe06b03-d98c-4337-9f89-54da98f49f9f
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: b3eacaba2ad0ddc2c0475d29b151d0a50be98fc0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72688712"
---
# <a name="circularstring"></a>CircularString
  
  `CircularString`은 0개 이상의 연속 원호 세그먼트 컬렉션입니다. 원호 세그먼트는 2차원 평면에서 3개의 점으로 정의되는 곡선 세그먼트입니다. 첫 번째 점은 세 번째 점과 같을 수 없습니다. 원호 세그먼트의 세 점 모두가 공선상에 있는 경우 원호 세그먼트가 선분으로 처리됩니다.  
  
> [!IMPORTANT]  
>  하위 유형을 포함 하 여에 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]도입 된 새로운 공간 기능에 대 한 자세한 설명 및 예를 보려면 [SQL Server 2012의 새로운 공간 기능](https://go.microsoft.com/fwlink/?LinkId=226407)백서를 다운로드 하세요. `CircularString`  
  
## <a name="circularstring-instances"></a>CircularString 인스턴스  
 다음 그림에서는 유효한 `CircularString` 인스턴스를 보여 줍니다.  
  
 ![](../../database-engine/media/5ff17e34-b578-4873-9d33-79500940d0bc.png "5ff17e34-b578-4873-9d33-79500940d0bc")  
  
### <a name="accepted-instances"></a>허용되는 인스턴스  
 인스턴스 `CircularString` 는 비어 있거나 홀수의 지점 수 n을 포함 하는 경우에 허용 됩니다. 여기서 n > 1입니다. 다음 `CircularString` 인스턴스가 허용됩니다.  
  
```sql
DECLARE @g1 geometry = 'CIRCULARSTRING EMPTY';  
DECLARE @g2 geometry = 'CIRCULARSTRING(1 1, 2 0, -1 1)';  
DECLARE @g3 geometry = 'CIRCULARSTRING(1 1, 2 0, 2 0, 2 0, 1 1)';  
```  
  
 
  `@g3`에서는 `CircularString` 인스턴스를 허용할 수 있지만 유효하지 않음을 보여 줍니다. 다음 CircularString 인스턴스 선언은 허용되지 않습니다. 이 선언에서는 `System.FormatException`이 발생합니다.  
  
```sql
DECLARE @g geometry = 'CIRCULARSTRING(1 1, 2 0, 2 0, 1 1)';  
```  
  
### <a name="valid-instances"></a>유효한 인스턴스  
 유효한 `CircularString` 인스턴스는 비어 있거나 다음 특성을 포함해야 합니다.  
  
-   이러한 인스턴스는 하나 이상의 원호 세그먼트(즉, 최소 3개의 점)를 포함해야 합니다.  
  
-   마지막 세그먼트를 제외하고 시퀀스에 있는 각 원호 세그먼트의 마지막 엔드포인트는 시퀀스에 있는 다음 세그먼트의 첫 번째 엔드포인트가어야 합니다.  
  
-   이 인스턴스에는 홀수 점이 있어야 합니다.  
  
-   이 인스턴스는 일정 간격으로 겹치면 안 됩니다.  
  
-   
  `CircularString` 인스턴스에 선분이 포함될 수 있지만 이러한 선분은 3개의 공선점으로 정의되어야 합니다.  
  
 다음 예에서는 유효한 `CircularString` 인스턴스를 보여 줍니다.  
  
```sql
DECLARE @g1 geometry = 'CIRCULARSTRING EMPTY';  
DECLARE @g2 geometry = 'CIRCULARSTRING(1 1, 2 0, -1 1)';  
DECLARE @g3 geometry = 'CIRCULARSTRING(1 1, 2 0, 2 0, 1 1, 0 1)';  
DECLARE @g4 geometry = 'CIRCULARSTRING(1 1, 2 2, 2 2)';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(),@g4.STIsValid();  
```  
  
 
  `CircularString` 인스턴스는 하나의 완전한 원을 정의하기 위해 두 개 이상의 원호 세그먼트를 포함해야 합니다. 
  `CircularString` 인스턴스는 (1 1, 3 1, 1 1)과 같은 하나의 원호 세그먼트를 사용하여 하나의 완전한 원을 정의할 수 없습니다. (1 1, 2 2, 3 1, 2 0, 1 1)을 사용하여 원을 정의합니다.  
  
 다음 예에서는 유효하지 않은 CircularString 인스턴스를 보여 줍니다.  
  
```sql
DECLARE @g1 geometry = 'CIRCULARSTRING(1 1, 2 0, 1 1)';  
DECLARE @g2 geometry = 'CIRCULARSTRING(0 0, 0 0, 0 0)';  
SELECT @g1.STIsValid(), @g2.STIsValid();  
```  
  
### <a name="instances-with-collinear-points"></a>공선점을 포함하는 인스턴스  
 다음 경우에는 원호 세그먼트가 선분으로 처리됩니다.  
  
-   3개의 점이 모두 공선상에 있는 경우(예: (1 3, 4 4, 7 5))  
  
-   첫 번째 및 중간 점이 동일하지만 세 번째 점이 다른 경우(예: (1 3, 1 3, 7 5))  
  
-   중간 및 마지막 점이 동일하지만 첫 번째 점이 다른 경우(예: (1 3, 4 4, 4 4))  
  
## <a name="examples"></a>예  
  
### <a name="a-instantiating-a-geometry-instance-with-an-empty-circularstring"></a>A. 빈 CircularString을 사용하여 Geometry 인스턴스 인스턴스화  
 이 예에서는 빈 `CircularString` 인스턴스를 만드는 방법을 보여 줍니다.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CIRCULARSTRING EMPTY');  
```  
  
### <a name="b-instantiating-a-geometry-instance-using-a-circularstring-with-one-circular-arc-segment"></a>B. 원호 세그먼트가 하나인 경우 CircularString을 사용하여 Geometry 인스턴스 인스턴스화  
 다음 예에서는 단일 원호 세그먼트(반원)를 사용하여 `CircularString` 인스턴스를 만드는 방법을 보여 줍니다.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry:: STGeomFromText('CIRCULARSTRING(2 0, 1 1, 0 0)', 0);  
SELECT @g.ToString();  
```  
  
### <a name="c-instantiating-a-geometry-instance-using-a-circularstring-with-multiple-circular-arc-segments"></a>C. 원호 세그먼트가 여러 개인 경우 CircularString을 사용하여 Geometry 인스턴스 인스턴스화  
 다음 예에서는 두 개 이상의 원호 세그먼트(완전한 원)를 사용하여 `CircularString` 인스턴스를 만드는 방법을 보여 줍니다.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CIRCULARSTRING(2 1, 1 2, 0 1, 1 0, 2 1)');  
SELECT 'Circumference = ' + CAST(@g.STLength() AS NVARCHAR(10));    
```  
  
 이 구문은 4∏에 해당하는  
  
```  
Circumference = 6.28319  
```  
  
 
  `LineString` 대신 `CircularString`을 사용하는 경우의 출력과 비교합니다.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(2 1, 1 2, 0 1, 1 0, 2 1)', 0);  
SELECT 'Perimeter = ' + CAST(@g.STLength() AS NVARCHAR(10));  
```  
  
 이 구문은 4∏에 해당하는  
  
```  
Perimeter = 5.65685  
```  
  
 `CircularString` 예제의 값은 원의 실제 원주 인 2&#x03c0; (2 * pi)에 가깝습니다.  
  
### <a name="d-declaring-and-instantiating-a-geometry-instance-with-a-circularstring-in-the-same-statement"></a>D. 동일한 문에서 CircularString을 사용하여 Geometry 인스턴스 선언 및 인스턴스화  
 이 조각은 동일한 문에서 `geometry`을 사용하여 `CircularString` 인스턴스를 선언하고 인스턴스화하는 방법을 보여 줍니다.  
  
```sql  
DECLARE @g geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';  
```  
  
### <a name="e-instantiating-a-geography-instance-with-a-circularstring"></a>E. CircularString을 사용하여 Geography 인스턴스 인스턴스화  
 다음 예에서는 `geography`을 사용하여 `CircularString` 인스턴스를 선언하고 인스턴스화하는 방법을 보여 줍니다.  
  
```sql  
DECLARE @g geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
```  
  
### <a name="f-instantiating-a-geometry-instance-with-a-circularstring-that-is-a-straight-line"></a>F. 직선인 CircularString을 사용하여 Geometry 인스턴스 인스턴스화  
 다음 예에서는 직선인 `CircularString` 인스턴스를 만드는 방법을 보여 줍니다.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('CIRCULARSTRING(0 0, 1 2, 2 4)', 0);  
```  
  
## <a name="see-also"></a>참고 항목  
 [공간 데이터 형식 개요](spatial-data-types-overview.md)   
 [CompoundCurve](compoundcurve.md)   
 [MakeValid&#40;geography 데이터 형식&#41;](/sql/t-sql/spatial-geography/makevalid-geography-data-type)   
 [MakeValid&#40;geometry 데이터 형식&#41;](/sql/t-sql/spatial-geometry/makevalid-geometry-data-type)   
 [STIsValid&#40;geometry 데이터 형식&#41;](/sql/t-sql/spatial-geometry/stisvalid-geometry-data-type)   
 [STIsValid&#40;geography 데이터 형식&#41;](/sql/t-sql/spatial-geography/stisvalid-geography-data-type)   
 [STLength&#40;geometry 데이터 형식&#41;](/sql/t-sql/spatial-geometry/stlength-geometry-data-type)   
 [STStartPoint&#40;geometry 데이터 형식&#41;](/sql/t-sql/spatial-geometry/ststartpoint-geometry-data-type)   
 [STEndpoint&#40;geometry 데이터 형식&#41;](/sql/t-sql/spatial-geometry/stendpoint-geometry-data-type)   
 [STPointN&#40;geometry 데이터 형식&#41;](/sql/t-sql/spatial-geometry/stpointn-geometry-data-type)   
 [STNumPoints&#40;geometry 데이터 형식&#41;](/sql/t-sql/spatial-geometry/stnumpoints-geometry-data-type)   
 [STIsRing&#40;geometry 데이터 형식&#41;](/sql/t-sql/spatial-geometry/stisring-geometry-data-type)   
 [STIsClosed&#40;geometry 데이터 형식&#41;](/sql/t-sql/spatial-geometry/stisclosed-geometry-data-type)   
 [STPointOnSurface&#40;geometry 데이터 형식&#41;](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type)   
 [LineString](linestring.md)  
  
  
