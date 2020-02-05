---
title: STCurveToLine(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveToLine method (geometry)
ms.assetid: abc80b32-4152-4e10-b816-798b901e0ac5
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 5bc1bdb1ece65113422af1e9a8ebe09de0db1fa1
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67930304"
---
# <a name="stcurvetoline-geometry-data-type"></a>STCurveToLine(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

원호 세그먼트가 포함된 **geometry** 인스턴스의 다각형 근사값을 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.STCurveToLine ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geometry**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="remarks"></a>설명  
 빈 **geometry** 인스턴스 변수에 대해 빈 **GeometryCollection** 인스턴스를 반환하고 초기화되지 않은 **geometry** 변수에 대해 **NULL**을 반환합니다.  
  
 메서드가 반환하는 다각형 근사값은 메서드 호출에 사용하는 **geometry** 인스턴스에 따라 다릅니다.  
  
-   **CircularString** 또는 **CompoundCurve** 인스턴스에 대해 **LineString** 인스턴스를 반환합니다.  
  
-   **CurvePolygon** 인스턴스에 대해 **Polygon** 인스턴스를 반환합니다.  
  
-   해당 인스턴스가 **CircularString**, **CompoundCurve**, 또는 **CurvePolygon** 인스턴스가 아닌 경우 **geometry** 인스턴스 복사본을 반환합니다. 예를 들어 `STCurveToLine` 메서드는 **점** 인스턴스인 **geometry** 인스턴스에 대해 **점** 인스턴스를 반환합니다.  
  
 SQL/MM 사양과 달리 `STCurveToLine` 메서드는 다각형 근사값을 계산할 때 z-좌표 값을 사용하지 않습니다. 이 메서드는 **geometry** 인스턴스를 호출할 때 제공되는 모든 z-좌표 값을 무시합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-an-uninitialized-geometry-variable-and-empty-instance"></a>A. 초기화되지 않은 Geometry 변수 및 빈 인스턴스 사용  
 다음 예제에서는 첫 번째 **SELECT** 문이 초기화되지 않은 **geometry** 인스턴스를 사용하여 `STCurveToLine` 메서드를 호출하고 두 번째 **SELECT** 문이 빈 **geometry** 인스턴스를 사용합니다. 따라서 메서드는 첫 번째 문에 **NULL**을 반환하고 두 번째 문에 **GeometryCollection** 컬렉션을 반환합니다.  
  
```
 DECLARE @g geometry; 
 SET @g = @g.STCurveToLine(); 
 SELECT @g.STGeometryType(); 
 SET @g = geometry::Parse('LINESTRING EMPTY'); 
 SELECT @g.STGeometryType();
 ```  
  
### <a name="b-using-a-linestring-instance"></a>B. LineString 인스턴스 사용  
 다음 예의 **SELECT** 문은 **LineString** 인스턴스를 사용하여 STCurveToLine 메서드를 호출합니다. 따라서 메서드는 **LineString** 인스턴스를 반환합니다.  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('LINESTRING(1 3, 5 5, 4 3, 1 3)'); 
 SET @g = @g.STCurveToLine(); 
 SELECT @g.STGeometryType();
 ```  
  
### <a name="c-using-a-circularstring-instance"></a>C. CircularString 인스턴스 사용  
 다음 예의 **SELECT** 문은 **CircularString** 인스턴스를 사용하여 STCurveToLine 메서드를 호출합니다. 따라서 메서드는 **LineString** 인스턴스를 반환합니다. 또한 이 **SELECT** 문은 거의 같은 두 인스턴스의 길이를 비교합니다.  마지막으로 두 번째 **SELECT** 문이 각 인스턴스의 점 개수를 반환합니다.  **CircularString** 인스턴스에 대해서는 점을 5개만 반환하지만 **LineString** 인스턴스에 대해서는 65개를 반환합니다.  
  
```
 DECLARE @g1 geometry, @g2 geometry; 
 SET @g1 = geometry::Parse('CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0)'); 
 SET @g2 = @g1.STCurveToLine(); 
 SELECT @g1.STGeometryType() AS [G1 Type], @g2.STGeometryType() AS [G2 Type], @g1.STLength() AS [G1 Perimeter], @g2.STLength() AS [G2 Perimeter], @g2.ToString() AS [G2 Def]; 
 SELECT @g1.STNumPoints(), @g2.STNumPoints();
 ```  
  
### <a name="d-using-a-curvepolygon-instance"></a>D. CurvePolygon 인스턴스 사용  
 다음 예의 **SELECT** 문은 **CurvePolygon** 인스턴스를 사용하여 STCurveToLine 메서드를 호출합니다. 따라서 메서드는 **다각형** 인스턴스를 반환합니다.  
  
```
 DECLARE @g1 geometry, @g2 geometry; 
 SET @g1 = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0))'); 
 SET @g2 = @g1.STCurveToLine(); 
 SELECT @g1.STGeometryType() AS [G1 Type], @g2.STGeometryType() AS [G2 Type];
 ```  
  
## <a name="see-also"></a>참고 항목  
 [공간 데이터 형식 개요](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [STLength&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stlength-geometry-data-type.md)   
 [STNumPoints&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stnumpoints-geometry-data-type.md)   
 [STGeometryType&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)  
  
  

