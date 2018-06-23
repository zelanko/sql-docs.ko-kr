---
title: CurvePolygon | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e000a1d8-a049-4542-bfeb-943fd6ab3969
caps.latest.revision: 18
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: a772fba6776195e914d9e4109a7973f355f3a270
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36184020"
---
# <a name="curvepolygon"></a>CurvePolygon
  `CurvePolygon`은 외부 경계 링과 0개 이상의 내부 링에서 정의하는 토폴로지 방식으로 닫힌 표면입니다.  
  
> [!IMPORTANT]  
>  자세한 설명 및 예제에 도입 된 공간 기능에 대 한 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]를 포함 하 여는 `CurvePolygon` 하위 형식, 백서를 다운로드 [SQL Server 2012의 새로운 공간 기능](http://go.microsoft.com/fwlink/?LinkId=226407)합니다.  
  
 특성을 정의 하는 다음 조건을 `CurvePolygon` 인스턴스:  
  
-   `CurvePolygon` 인스턴스의 경계는 외부 링과 모든 내부 링으로 정의됩니다.  
  
-   `CurvePolygon` 인스턴스의 내부는 외부 링과 모든 내부 링 사이의 공간입니다.  
  
 A `CurvePolygon` 에서 다른 인스턴스는 `Polygon` 인스턴스와 `CurvePolygon` 인스턴스는 원호 세그먼트인 포함 될 수 있습니다: `CircularString` 및 `CompoundCurve`합니다.  
  
## <a name="compoundcurve-instances"></a>CompoundCurve 인스턴스  
 아래 그림 유효한 `CurvePolygon` 수치:  
  
### <a name="accepted-instances"></a>허용되는 인스턴스  
 에 대 한는 `CurvePolygon` 인스턴스가 허용 되려면, 되어야 하거나 비어 있거나 허용 되는 원호 링만 포함 합니다. 허용되는 원호 링은 다음 요구 사항을 충족합니다.  
  
1.  허용되는 `LineString`, `CircularString` 또는 `CompoundCurve` 인스턴스여야 합니다. 허용되는 인스턴스에 대한 자세한 내용은 [LineString](linestring.md), [CircularString](circularstring.md)및 [CompoundCurve](compoundcurve.md)를 참조하십시오.  
  
2.  4개 이상의 점이 있어야 합니다.  
  
3.  시작점과 끝점의 X 및 Y 좌표가 동일해야 합니다.  
  
    > [!NOTE]  
    >  Z 및 M 값이 무시되어야 합니다.  
  
 다음 예에서는 허용 된 `CurvePolygon` 인스턴스.  
  
```  
DECLARE @g1 geometry = 'CURVEPOLYGON EMPTY';  
DECLARE @g2 geometry = 'CURVEPOLYGON((0 0, 0 0, 0 0, 0 0))';  
DECLARE @g3 geometry = 'CURVEPOLYGON((0 0 1, 0 0 2, 0 0 3, 0 0 3))'  
DECLARE @g4 geometry = 'CURVEPOLYGON(CIRCULARSTRING(1 3, 3 5, 4 7, 7 3, 1 3))';  
DECLARE @g5 geography = 'CURVEPOLYGON((-122.3 47, 122.3 -47, 125.7 -49, 121 -38, -122.3 47))';  
```  
  
 `@g3` 이 허용됩니다. `geography` 유형 인스턴스가 유효하지 않아도 `@g5`가 허용됩니다.  
  
 다음 예에서는 `System.FormatException`이 발생합니다.  
  
```  
DECLARE @g1 geometry = 'CURVEPOLYGON((0 5, 0 0, 0 0, 0 0))';  
DECLARE @g2 geometry = 'CURVEPOLYGON((0 0, 0 0, 0 0))';  
```  
  
 `@g1` 이 허용되지 않습니다. `@g2` 가 허용되지 않습니다.  
  
### <a name="valid-instances"></a>유효한 인스턴스  
 에 대 한는 `CurvePolygon` 인스턴스가 유효 하려면 외부 및 내부 링에는 다음 조건을 충족 해야 합니다.  
  
1.  이 두 링은 단일 탄젠트 점에서만 접할 수 있습니다.  
  
2.  이 두 링은 서로 교차할 수 없습니다.  
  
3.  각 링에 4개 이상의 점이 있어야 합니다.  
  
4.  각 링이 허용 가능한 곡선 유형이어야 합니다.  
  
 `CurvePolygon` 인스턴스는 또한 인지 여부에 따라 특정 조건을 충족 해야 `geometry` 또는 `geography` 데이터 형식입니다.  
  
#### <a name="geometry-data-type"></a>Geometry 데이터 형식  
 유효한 **geometryCurvePolygon** 인스턴스는 다음 특성을 포함해야 합니다.  
  
1.  모든 내부 링은 외부 링에 포함되어야 합니다.  
  
2.  내부 링이 여러 개일 수 있지만 내부 링은 다른 내부 링을 포함할 수 없습니다.  
  
3.  링은 자체적으로 또는 다른 링을 교차할 수 없습니다.  
  
4.  링은 단일 탄젠트 점(링 접촉이 한정된 점 수)에서만 접할 수 있습니다.  
  
5.  다각형 내부는 연결되어야 합니다.  
  
 다음 예에서는 유효한 **geometryCurvePolygon** 인스턴스를 보여 줍니다.  
  
```  
DECLARE @g1 geometry = 'CURVEPOLYGON EMPTY';  
DECLARE @g2 geometry = 'CURVEPOLYGON(CIRCULARSTRING(1 3, 3 5, 4 7, 7 3, 1 3))';  
SELECT @g1.STIsValid(), @g2.STIsValid();  
```  
  
 CurvePolygon 인스턴스의 유효성 규칙은 Polygon 인스턴스의 유효성 규칙과 동일합니다. 단, CurvePolygon 인스턴스는 새 원호 세그먼트 유형을 허용할 수 있습니다. 유효하거나 유효하지 않은 인스턴스에 대한 다른 예는 [Polygon](polygon.md)을 참조하십시오.  
  
#### <a name="geography-data-type"></a>Geography 데이터 형식  
 유효한 **geographyCurvePolygon** 인스턴스는 다음 특성을 포함해야 합니다.  
  
1.  다각형 내부는 왼쪽 규칙을 사용하여 연결됩니다.  
  
2.  링은 자체적으로 또는 다른 링을 교차할 수 없습니다.  
  
3.  링은 단일 탄젠트 점(링 접촉이 한정된 점 수)에서만 접할 수 있습니다.  
  
4.  다각형 내부는 연결되어야 합니다.  
  
 다음 예에서는 유효한 geography CurvePolygon 인스턴스를 보여 줍니다.  
  
```  
DECLARE @g geography = 'CURVEPOLYGON((-122.3 47, 122.3 47, 125.7 49, 121 38, -122.3 47))';  
SELECT @g.STIsValid();  
```  
  
## <a name="examples"></a>예  
  
### <a name="a-instantiating-a-geometry-instance-with-an-empty-curvepolygon"></a>1. 빈 CurvePolygon을 사용하여 Geometry 인스턴스 인스턴스화  
 이 예에서는 빈 `CurvePolygon` 인스턴스를 만드는 방법을 보여 줍니다.  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CURVEPOLYGON EMPTY');  
```  
  
### <a name="b-declaring-and-instantiating-a-geometry-instance-with-a-curvepolygon-in-the-same-statement"></a>2. 동일한 문에서 CurvePolygon을 사용하여 Geometry 인스턴스 선언 및 인스턴스화  
 이 코드 조각에서는 선언 하 고 사용 하 여 geometry 인스턴스를 초기화 하는 방법을 보여 줍니다.는 `CurvePolygon` 동일한 문에서:  
  
```tsql  
DECLARE @g geometry = 'CURVEPOLYGON(CIRCULARSTRING(2 4, 4 2, 6 4, 4 6, 2 4))'  
```  
  
### <a name="c-instantiating-a-geography-instance-with-a-curvepolygon"></a>3. CurvePolygon을 사용하여 Geography 인스턴스 인스턴스화  
 이 코드 조각에서는 선언 하 고 초기화 하는 방법을 보여 줍니다.는 `geography` 인스턴스는 `CurvePolygon`:  
  
```tsql  
DECLARE @g geography = 'CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
```  
  
### <a name="d-storing-a-curvepolygon-with-only-an-exterior-bounding-ring"></a>4. 외부 경계 링만 사용하여 CurvePolygon 저장  
 이 예에서는 단순 원을 `CurvePolygon` 인스턴스에 저장하는 방법을 보여 줍니다. 외부 경계 링만 사용하여 원을 정의합니다.  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(2 4, 4 2, 6 4, 4 6, 2 4))');  
SELECT @g.STArea() AS Area;  
```  
  
### <a name="e-storing-a-curvepolygon-containing-interior-rings"></a>5. 내부 링을 포함하는 CurvePolygon 저장  
 이 예에서는 도넛형을 만듭니다는 `CurvePolygon` 인스턴스 (둘 다 외부 경계 링과 내부 링 여 도넛형을 정의 사용 됨):  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(0 4, 4 0, 8 4, 4 8, 0 4), CIRCULARSTRING(2 4, 4 2, 6 4, 4 6, 2 4))');  
SELECT @g.STArea() AS Area;  
```  
  
 이 예제에서는 모두 유효한 `CurvePolygon` 인스턴스 및 내부 링을 사용 하는 경우 잘못 된 인스턴스:  
  
```tsql  
DECLARE @g1 geometry, @g2 geometry;  
SET @g1 = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(0 5, 5 0, 0 -5, -5 0, 0 5), (-2 2, 2 2, 2 -2, -2 -2, -2 2))');  
IF @g1.STIsValid() = 1  
  BEGIN  
     SELECT @g1.STArea();  
  END  
SET @g2 = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(0 5, 5 0, 0 -5, -5 0, 0 5), (0 5, 5 0, 0 -5, -5 0, 0 5))');  
IF @g2.STIsValid() = 1  
  BEGIN  
     SELECT @g2.STArea();  
  END  
SELECT @g1.STIsValid() AS G1, @g2.STIsValid() AS G2;  
```  
  
 @g1과 @g2 모두 동일한 외부 경계 링을 사용합니다. 이 원의 반지름은 5이고 둘 다 내부 링에 대해 사각형을 사용합니다.  그러나 @g1 인스턴스는 유효하고 @g2 인스턴스는 유효하지 않습니다.  @g2가 유효하지 않은 이유는 내부 링이 외부 링에 의해 경계가 지정된 내부 공간을 4개의 개별 영역으로 분할하기 때문입니다.  다음 그림에서는 이를 실행한 결과를 보여 줍니다.  
  
## <a name="see-also"></a>관련 항목  
 [Polygon](polygon.md)   
 [CircularString](circularstring.md)   
 [CompoundCurve](compoundcurve.md)   
 [geometry 데이터 형식 메서드 참조](/sql/t-sql/spatial-geometry/spatial-types-geometry-transact-sql)   
 [geography 데이터 형식 메서드 참조](/sql/t-sql/spatial-geography/spatial-types-geography)   
 [공간 데이터 형식 개요](spatial-data-types-overview.md)  
  
  
