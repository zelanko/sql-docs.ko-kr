---
title: "CurveToLineWithTolerance (geometry 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords: CurveToLineWithTolerance method (geometry)
ms.assetid: 96871075-1998-4cd9-86b1-3fc55577aee4
caps.latest.revision: "16"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: caa3a00f6ed962122288fa0d71a4f2d2f92bd6f7
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="curvetolinewithtolerance-geometry-data-type"></a>CurveToLineWithTolerance(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

다각형 근사값을 반환 합니다.는 **geometry** 원호 세그먼트가 포함 된 인스턴스.
  
## <a name="syntax"></a>구문  
  
```  
  
.CurveToLineWithTolerance ( tolerance, relative )  
```  
  
## <a name="arguments"></a>인수  
 *허용 오차*  
 이 **double** 원래의 원호 세그먼트와 선형 근사값 사이의 최대 오차를 정의 하는 식입니다.  
  
 *상대*  
 이 **bool** 편차에 대해 극대 사용할 것인지를 나타내는 식입니다. 극대값이 false(0)로 설정되면 선형 근사값이 가질 수 있는 편차에 대해 최대값이 설정됩니다. 극대값이 true(1)로 설정되면 허용 오차는 허용 오차 매개 변수와 공간 개체의 경계 상자 지름의 곱으로 계산됩니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **기 하 도형**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="exceptions"></a>예외  
 허용 오차를 <= 0으로 설정하면 `ArgumentOutOfRange` 예외가 발생합니다.  
  
## <a name="remarks"></a>주의  
 이 메서드는 결과 허용 오차 크기를 지정할 수 **LineString**합니다.  
  
 다음 표에서는 여러 유형에 대해 `CurveToLineWithTolerance()`에서 반환하는 인스턴스 유형을 보여 줍니다.  
  
|호출 인스턴스 유형|반환되는 공간 유형|  
|----------------------------|---------------------------|  
|빈 geometry 인스턴스|빈 **GeometryCollection** 인스턴스|  
|**지점** 및 **MultiPoint**|**지점** 인스턴스|  
|**MultiPoint**|**지점** 또는 **MultiPoint** 인스턴스|  
|**CircularString**, **CompoundCurve**, 또는 **LineString**|**LineString** 인스턴스|  
|**MultiLineString**|**LineString** 또는 **MultiLineString** 인스턴스|  
|**CurvePolygon** 및 **다각형**|**다각형** 인스턴스|  
|**MultiPolygon**|**다각형** 또는 **MultiPolygon** 인스턴스|  
|**GeometryCollection** 원호 세그먼트를 포함 하지 않는 단일 인스턴스를 사용|에 포함 된 인스턴스는 **GeometryCollection** 반환 된 인스턴스의 유형을 결정 합니다.|  
|**GeometryCollection** 단일 1 차원 원호 세그먼트 인스턴스 (**CircularString**, **CompoundCurve**)|**LineString** 인스턴스|  
|**GeometryCollection** 단일 2 차원 원호 세그먼트 인스턴스 (**CurvePolygon**)|**다각형** 인스턴스|  
|**GeometryCollection** 여러 1 차원 인스턴스가 있는|**MultiLineString** 인스턴스|  
|**GeometryCollection** 와 여러 2 차원 인스턴스가|**MultiPolygon** 인스턴스|  
|**GeometryCollection** 서로 다른 차원의 여러 인스턴스가 있는|**GeometryCollection** 인스턴스|  
  
## <a name="examples"></a>예  
  
### <a name="a-using-different-tolerance-values-on-a-circularstring-instance"></a>1. CircularString 인스턴스에 여러 허용 오차 값 사용  
 다음 예제에서는 영향을 어떻게 설정 된 허용 오차는 `LineString`에서 반환 된 인스턴스는 `CircularString` 인스턴스:  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)'); 
 SELECT @g.CurveToLineWithTolerance(0.1,0).STNumPoints(), @g.CurveToLineWithTolerance(0.01, 0).STNumPoints();
 ```  
  
### <a name="b-using-the-method-on-a-multilinestring-instance-containing-one-linestring"></a>2. LineString 하나를 포함하는 MultiLineString 인스턴스에 메서드 사용  
 다음 예에서는 `MultiLineString` 인스턴스 하나만 포함하는 `LineString` 인스턴스에서 반환되는 결과를 보여 줍니다.  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('MULTILINESTRING((1 3, 4 8, 6 9))'); 
 SELECT @g.CurveToLineWithTolerance(0.1,0).ToString();
 ```  
  
### <a name="c-using-the-method-on-a-multilinestring-instance-containing-multiple-linestrings"></a>3. 여러 LineString을 포함하는 MultiLineString 인스턴스에 메서드 사용  
 다음 예에서는 `MultiLineString` 인스턴스를 둘 이상 포함하는 `LineString` 인스턴스에서 반환되는 결과를 보여 줍니다.  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('MULTILINESTRING((1 3, 4 8, 6 9),(4 4, 9 18))'); 
 SELECT @g.CurveToLineWithTolerance(0.1,0).ToString();
 ```  
  
### <a name="d-setting-relative-to-true-for-an-invoking-curvepolygon-instance"></a>4. 호출하는 CurvePolygon 인스턴스에 대해 극대값을 true로 설정  
 다음 예제에서는 한 `CurvePolygon` 호출 하는 인스턴스 `CurveToLineWithTolerance()` 와 *상대* true로 설정:  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.CurveToLineWithTolerance(.5,1).ToString();
 ```  
  
### <a name="e-using-the-method-on-a-geometrycollection-instance"></a>5. GeometryCollection 인스턴스에 메서드 사용  
 다음 예에서는 2차원 `CurveToLineWithTolerance()` 인스턴스와 1차원 `GeometryCollection` 인스턴스가 포함된 `CurvePolygon`에서 `CircularString`를 호출합니다. `CurveToLineWithTolerance()`는 원호 세그먼트 유형을 둘 다 선분 유형으로 변환하여 `GeometryCollection` 유형으로 반환합니다.  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('GEOMETRYCOLLECTION(CURVEPOLYGON( COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), (4 2, 0 2))), CIRCULARSTRING(4 4, 8 6, 9 5))'); 
 SELECT @g.CurveToLineWithTolerance(0.1,0).STNumPoints(), @g.CurveToLineWithTolerance(0.1, 0).ToString();
 ```  
  
## <a name="see-also"></a>관련 항목:  
 [CurveToLineWithTolerance &#40; geography 데이터 형식 &#41;](../../t-sql/spatial-geography/curvetolinewithtolerance-geography-data-type.md)   
 [STCurveToLine &#40; geometry 데이터 형식 &#41;](../../t-sql/spatial-geometry/stcurvetoline-geometry-data-type.md)  
  
  

