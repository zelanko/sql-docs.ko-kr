---
title: CurveToLineWithTolerance(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- CurveToLineWithTolerance method (geometry)
ms.assetid: 96871075-1998-4cd9-86b1-3fc55577aee4
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8bae33f7d9dcd3770719f692b84d0499f042c33f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33064020"
---
# <a name="curvetolinewithtolerance-geometry-data-type"></a>CurveToLineWithTolerance(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

원호 세그먼트가 포함된 **geometry** 인스턴스의 다각형 근사값을 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.CurveToLineWithTolerance ( tolerance, relative )  
```  
  
## <a name="arguments"></a>인수  
 *tolerance*  
 원래의 원호 세그먼트와 선형 근사값 사이의 최대 오차를 정의하는 **double** 식입니다.  
  
 *relative*  
 편차에 대해 극대값을 사용할지 여부를 나타내는 **bool** 식입니다. 극대값이 false(0)로 설정되면 선형 근사값이 가질 수 있는 편차에 대해 최대값이 설정됩니다. 극대값이 true(1)로 설정되면 허용 오차는 허용 오차 매개 변수와 공간 개체의 경계 상자 지름의 곱으로 계산됩니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geometry**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="exceptions"></a>예외  
 허용 오차를 <= 0으로 설정하면 `ArgumentOutOfRange` 예외가 발생합니다.  
  
## <a name="remarks"></a>Remarks  
 이 메서드는 결과 **LineString**의 허용 오차 크기를 지정할 수 있습니다.  
  
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
|원호 세그먼트가 포함되지 않은 단일 인스턴스가 있는 **GeometryCollection**|**GeometryCollection**에 포함된 인스턴스가 반환된 인스턴스의 유형을 결정합니다.|  
|단일 1차원 원호 세그먼트 인스턴스가 있는 **GeometryCollection**(**CircularString**, **CompoundCurve**)|**LineString** 인스턴스|  
|단일 2차원 원호 세그먼트 인스턴스가 있는 **GeometryCollection**(**CurvePolygon**)|**다각형** 인스턴스|  
|여러 1차원 인스턴스가 있는 **GeometryCollection**|**MultiLineString** 인스턴스|  
|여러 2차원 인스턴스가 있는 **GeometryCollection**|**MultiPolygon** 인스턴스|  
|다른 차원의 여러 인스턴스가 있는 **GeometryCollection**|**GeometryCollection** 인스턴스|  
  
## <a name="examples"></a>예  
  
### <a name="a-using-different-tolerance-values-on-a-circularstring-instance"></a>1. CircularString 인스턴스에 여러 허용 오차 값 사용  
 다음 예에서는 허용 오차를 설정하면 `CircularString` 인스턴스에서 반환된 `LineString`인스턴스가 어떤 영향을 받는지 보여 줍니다.  
  
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
 다음 예에서는 *relative*를 true로 설정하여 `CurvePolygon` 인스턴스를 사용해 `CurveToLineWithTolerance()`를 호출합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [CurveToLineWithTolerance &#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/curvetolinewithtolerance-geography-data-type.md)   
 [STCurveToLine &#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stcurvetoline-geometry-data-type.md)  
  
  

