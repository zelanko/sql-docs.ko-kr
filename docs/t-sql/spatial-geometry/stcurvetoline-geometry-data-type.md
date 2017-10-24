---
title: "STCurveToLine (geometry 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveToLine method (geometry)
ms.assetid: abc80b32-4152-4e10-b816-798b901e0ac5
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2a0601e93e3763ca184ecf599da2cc7f9b36dd6f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stcurvetoline-geometry-data-type"></a>STCurveToLine(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

다각형 근사값을 반환 합니다.는 **geometry** 원호 세그먼트가 포함 된 인스턴스.
  
## <a name="syntax"></a>구문  
  
```  
  
.STCurveToLine ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **기 하 도형**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="remarks"></a>주의  
 빈 반환 **GeometryCollection**인스턴스에 대해 빈 **geometry** 인스턴스 변수 및 반환 **NULL** 초기화 되지 않음에 대 한 **기하도형** 변수입니다.  
  
 메서드가 반환 하는 다각형 근사값 의존는 **geometry** 메서드를 호출 하는 데 사용 하는 인스턴스:  
  
-   반환 된 **LineString** 에 대 한 인스턴스는 **CircularString** 또는 **CompoundCurve** 인스턴스.  
  
-   반환 된 **다각형** 에 대 한 인스턴스는 **CurvePolygon** 인스턴스.  
  
-   복사본을 반환 된 **geometry** 해당 인스턴스가 아닌 경우 인스턴스는 **CircularString**, **CompoundCurve**, 또는 **CurvePolygon** 인스턴스 . 예를 들어는 `STCurveToLine` 메서드가 반환 되는 **지점** 에 대 한 인스턴스는 **geometry** 인스턴스에서 **지점** 인스턴스.  
  
 SQL/MM 사양과 달리는 `STCurveToLine` 메서드는 다각형 근사값을 계산할 z 좌표 값을 사용 하지 않습니다. 메서드 호출에 있는 모든 z 좌표 값을 무시 **geometry** 인스턴스.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-an-uninitialized-geometry-variable-and-empty-instance"></a>1. 초기화되지 않은 Geometry 변수 및 빈 인스턴스 사용  
 다음 예에서 첫 번째 **선택** 초기화 되지 않은 문에서 사용 하 여 **geometry** 호출 하는 인스턴스는 `STCurveToLine` 메서드와 두 번째 **선택** 사용 하 여 빈 **geometry** 인스턴스. 따라서 메서드가 반환 **NULL** 첫 번째 문으로 및 **GeometryCollection** 두 번째 문에 컬렉션입니다.  
  
```
 DECLARE @g geometry; 
 SET @g = @g.STCurveToLine(); 
 SELECT @g.STGeometryType(); 
 SET @g = geometry::Parse('LINESTRING EMPTY'); 
 SELECT @g.STGeometryType();
 ```  
  
### <a name="b-using-a-linestring-instance"></a>2. LineString 인스턴스 사용  
 **선택** 문은 다음 예제에서 사용 하 여는 **LineString** 인스턴스 STCurveToLine 메서드를 호출 합니다. 따라서 메서드가 반환 된 **LineString** 인스턴스.  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('LINESTRING(1 3, 5 5, 4 3, 1 3)'); 
 SET @g = @g.STCurveToLine(); 
 SELECT @g.STGeometryType();
 ```  
  
### <a name="c-using-a-circularstring-instance"></a>3. CircularString 인스턴스 사용  
 첫 번째 **선택** 문은 다음 예제에서 사용 하 여는 **CircularString** 인스턴스 STCurveToLine 메서드를 호출 합니다. 따라서 메서드가 반환 된 **LineString** 인스턴스. 이 **선택** 문 또한 동일 약 요소인 두 인스턴스의 길이 비교 합니다.  마지막으로, 두 번째 **선택** 문이 각 인스턴스의 점 개수를 반환 합니다.  에 대 한 점을 5 개만 반환 된 **CircularString** 인스턴스 중 하나로 대해서는 65 개는 **LineString**인스턴스.  
  
```
 DECLARE @g1 geometry, @g2 geometry; 
 SET @g1 = geometry::Parse('CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0)'); 
 SET @g2 = @g1.STCurveToLine(); 
 SELECT @g1.STGeometryType() AS [G1 Type], @g2.STGeometryType() AS [G2 Type], @g1.STLength() AS [G1 Perimeter], @g2.STLength() AS [G2 Perimeter], @g2.ToString() AS [G2 Def]; 
 SELECT @g1.STNumPoints(), @g2.STNumPoints();
 ```  
  
### <a name="d-using-a-curvepolygon-instance"></a>4. CurvePolygon 인스턴스 사용  
 **선택** 문은 다음 예제에서 사용 하 여는 **CurvePolygon** 인스턴스 STCurveToLine 메서드를 호출 합니다. 따라서 메서드가 반환 된 **다각형** 인스턴스.  
  
```
 DECLARE @g1 geometry, @g2 geometry; 
 SET @g1 = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0))'); 
 SET @g2 = @g1.STCurveToLine(); 
 SELECT @g1.STGeometryType() AS [G1 Type], @g2.STGeometryType() AS [G2 Type];
 ```  
  
## <a name="see-also"></a>관련 항목:  
 [공간 데이터 형식 개요](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [STLength&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stlength-geometry-data-type.md)   
 [STNumPoints&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stnumpoints-geometry-data-type.md)   
 [STGeometryType&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)  
  
  


