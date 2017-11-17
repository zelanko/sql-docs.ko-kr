---
title: "STCurveN (geometry 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveN method (geometry)
ms.assetid: 64adf1a1-3a41-41fb-b7d1-44390c3e4ea9
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: dd5b459bfa271d98844d30455e4e1a9e03d0e2cd
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stcurven-geometry-data-type"></a>STCurveN(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

지정한 곡선을 반환 합니다.는 **geometry** 인스턴스에서 **LineString**, **CircularString**, **CompoundCurve**, 또는  **MultiLineString**합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.STCurveN ( curve_index )  
```  
  
## <a name="arguments"></a>인수  
 *curve_index*  
 이 **int** 1 있는 곡선 개수 사이의 식은 **기 하 도형** 인스턴스.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **기 하 도형**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="exceptions"></a>예외  
 경우 *curve_index* < 1 아니라면 `ArgumentOutOfRangeException` throw 됩니다.  
  
## <a name="remarks"></a>주의  
 **NULL** 이 반환 됩니다는 다음에 발생 합니다.  
  
-   **geometry** 인스턴스가 선언 되지만 인스턴스화되지  
  
-   **geometry** 인스턴스 비어 있습니다.  
  
-   *curve_index* 있는 곡선 개수를 초과 **geometry** 인스턴스  
  
-   **geometry** 인스턴스가 **지점**, **MultiPoint**, **다각형**, **CurvePolygon**, 또는  **MultiPolygon**  
  
## <a name="examples"></a>예  
  
### <a name="a-using-stcurven-on-a-circularstring-instance"></a>1. CircularString 인스턴스에 STCurveN() 사용  
 다음 예에서는 `CircularString` 인스턴스에 두 번째 곡선을 반환합니다.  
  
```
 DECLARE @g geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 이 항목의 이전 예에서는 다음을 반환합니다.  
  
 `CIRCULARSTRING (3 6.3246, 0 7, -3 6.3246)`  
  
### <a name="b-using-stcurven-on-a-compoundcurve-instance-with-one-circularstring-instance"></a>2. CircularString 인스턴스 하나와 함께 CompoundCurve 인스턴스에 STCurveN() 사용  
 다음 예에서는 `CompoundCurve` 인스턴스에 두 번째 곡선을 반환합니다.  
  
```
 DECLARE @g geometry = 'COMPOUNDCURVE(CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 이 항목의 이전 예에서는 다음을 반환합니다.  
  
 `CIRCULARSTRING (3 6.3246, 0 7, -3 6.3246)`  
  
### <a name="c-using-stcurven-on-a-compoundcurve-instance-with-three-circularstring-instances"></a>3. CircularString 인스턴스 세 개와 함께 CompoundCurve 인스턴스에 STCurveN() 사용  
 다음 예에서는 별도의 `CompoundCurve` 인스턴스 세 개를 이전 예와 동일한 곡선 시퀀스에 조합하는 `CircularString` 인스턴스를 사용합니다.  
  
```
 DECLARE @g geometry = 'COMPOUNDCURVE (CIRCULARSTRING (0 0, 1 2.1082, 3 6.3246), CIRCULARSTRING(3 6.3246, 0 7, -3 6.3246), CIRCULARSTRING(-3 6.3246, -1 2.1082, 0 0))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 이 항목의 이전 예에서는 다음을 반환합니다.  
  
 `CIRCULARSTRING (3 6.3246, 0 7, -3 6.3246)`  
  
 이전의 세 가지 예와 결과가 동일합니다. 같은 곡선 시퀀스를 입력하기 위해 어떤 WKT(Well-known Text) 형식을 사용하건 간에 `STCurveN()` 인스턴스가 사용될 때 `CompoundCurve`에서 반환하는 결과는 같습니다.  
  
### <a name="d-validating-the-parameter-before-calling-stcurven"></a>4. STCurveN() 호출 전 매개 변수 유효성 검사  
 다음 예제에서는 있는지 확인 하는 방법을 보여 줍니다 `@n` 호출 하기 전에 올바른지는 `STCurveN()`메서드:  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [Stnumcurves&#40; geometry 데이터 형식 &#41;](../../t-sql/spatial-geometry/stnumcurves-geometry-data-type.md)   
 [Geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


