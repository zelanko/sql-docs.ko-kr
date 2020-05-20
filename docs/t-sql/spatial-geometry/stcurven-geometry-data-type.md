---
title: STCurveN(geometry 데이터 형식) | Microsoft Docs
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
- STCurveN method (geometry)
ms.assetid: 64adf1a1-3a41-41fb-b7d1-44390c3e4ea9
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 9b9e958085af5f70d4dedb1f9a44866c04918343
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67930139"
---
# <a name="stcurven-geometry-data-type"></a>STCurveN(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

**LineString**, **CircularString**, **CompoundCurve** 또는 **MultiLineString**인 **geography** 인스턴스에서 지정된 곡선을 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.STCurveN ( curve_index )  
```  
  
## <a name="arguments"></a>인수  
 *curve_index*  
 1과 **geometry** 인스턴스에 있는 곡선 개수 사이의 **int** 식입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geometry**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="exceptions"></a>예외  
 *curve_index* < 1인 경우는 `ArgumentOutOfRangeException`을 throw합니다.  
  
## <a name="remarks"></a>설명  
 다음 상황에서는 **NULL**이 반환됩니다.  
  
-   **geometry** 인스턴스가 선언되지만 인스턴스화되지 않는 경우  
  
-   **geometry** 인스턴스가 비어있는 경우  
  
-   *curve_index*가 **geometry** 인스턴스에 있는 곡선 개수를 초과하는 경우  
  
-   **geometry** 인스턴스가 **Point**, **MultiPoint**, **Polygon**, **CurvePolygon** 또는 **MultiPolygon**인 경우  
  
## <a name="examples"></a>예  
  
### <a name="a-using-stcurven-on-a-circularstring-instance"></a>A. CircularString 인스턴스에 STCurveN() 사용  
 다음 예에서는 `CircularString` 인스턴스에 두 번째 곡선을 반환합니다.  
  
```
 DECLARE @g geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 이 항목의 이전 예에서는 다음을 반환합니다.  
  
 `CIRCULARSTRING (3 6.3246, 0 7, -3 6.3246)`  
  
### <a name="b-using-stcurven-on-a-compoundcurve-instance-with-one-circularstring-instance"></a>B. CircularString 인스턴스 하나와 함께 CompoundCurve 인스턴스에 STCurveN() 사용  
 다음 예에서는 `CompoundCurve` 인스턴스에 두 번째 곡선을 반환합니다.  
  
```
 DECLARE @g geometry = 'COMPOUNDCURVE(CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 이 항목의 이전 예에서는 다음을 반환합니다.  
  
 `CIRCULARSTRING (3 6.3246, 0 7, -3 6.3246)`  
  
### <a name="c-using-stcurven-on-a-compoundcurve-instance-with-three-circularstring-instances"></a>C. CircularString 인스턴스 세 개와 함께 CompoundCurve 인스턴스에 STCurveN() 사용  
 다음 예에서는 별도의 `CompoundCurve` 인스턴스 세 개를 이전 예와 동일한 곡선 시퀀스에 조합하는 `CircularString` 인스턴스를 사용합니다.  
  
```
 DECLARE @g geometry = 'COMPOUNDCURVE (CIRCULARSTRING (0 0, 1 2.1082, 3 6.3246), CIRCULARSTRING(3 6.3246, 0 7, -3 6.3246), CIRCULARSTRING(-3 6.3246, -1 2.1082, 0 0))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 이 항목의 이전 예에서는 다음을 반환합니다.  
  
 `CIRCULARSTRING (3 6.3246, 0 7, -3 6.3246)`  
  
 이전의 세 가지 예와 결과가 동일합니다. 같은 곡선 시퀀스를 입력하기 위해 어떤 WKT(Well-known Text) 형식을 사용하건 간에 `STCurveN()` 인스턴스가 사용될 때 `CompoundCurve`에서 반환하는 결과는 같습니다.  
  
### <a name="d-validating-the-parameter-before-calling-stcurven"></a>D. STCurveN() 호출 전 매개 변수 유효성 검사  
 다음 예에서는 `STCurveN()`메서드를 호출하기 전에 `@n`이 올바른지 확인하는 방법을 보여 줍니다.  
  
```
 DECLARE @g geometry;  
 DECLARE @n int;  
 SET @n = 3;  
 SET @g = geometry::Parse('CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)');  
 IF @n >= 1 AND @n <= @g.STNumCurves()  
 BEGIN  
 SELECT @g.STCurveN(@n).ToString();  
 END
 ```  
  
## <a name="see-also"></a>참고 항목  
 [STNumCurves &#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stnumcurves-geometry-data-type.md)   
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

