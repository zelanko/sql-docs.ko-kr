---
title: "STCurveN (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STCurveN
- STCurveN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveN method (geography)
ms.assetid: 99ef7100-2c4b-4f07-8d66-b343da94b023
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d33b8e6752ac8aca3bc6846a4558af4830373081
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stcurven-geography-data-type"></a>STCurveN(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  지정한 곡선을 반환 합니다.는 **geography** 인스턴스에서 **LineString**, **CircularString**, 또는 **CompoundCurve**합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STCurveN( n )  
```  
  
## <a name="arguments"></a>인수  
 *n*  
 이 **int** 1 있는 곡선 개수 사이의 식은 **geography** 인스턴스.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="exceptions"></a>예외  
 경우 n < 1 아니라면 **ArgumentOutOfRangeException** throw 됩니다.  
  
## <a name="remarks"></a>주의  
 **NULL** 때 반환 되는 다음 조건을 발생 합니다.  
  
-   **geography** 인스턴스가 선언 되지만 인스턴스화되지 않습니다  
  
-   **geography** 인스턴스 비어 있습니다.  
  
-   n 있는 곡선 개수를 초과 **geography** 인스턴스 (참조 [STNumCurves &#40; geography 데이터 형식 &#41;](../../t-sql/spatial-geography/stnumcurves-geography-data-type.md)  
  
-   에 대 한 차원에서 **geography** 인스턴스 같지 않음 (참조 [STDimension &#40; geography 데이터 형식 &#41;](../../t-sql/spatial-geography/stdimension-geography-data-type.md)  
  
## <a name="examples"></a>예  
  
### <a name="a-using-stcurven-on-a-circularstring"></a>1. CircularString에 STCurveN() 사용  
 두 번째 곡선을 반환 하는 다음 예제는 **CircularString** 인스턴스:  
  
```
 DECLARE @g geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 이 예에서는 다음을 반환합니다.  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
### <a name="b-using-stcurven-on-a-compoundcurve"></a>2. CompoundCurve에 STCurveN() 사용  
 두 번째 곡선을 반환 하는 다음 예제는 **CompoundCurve** 인스턴스:  
  
```
 DECLARE @g geography = 'COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 이 예에서는 다음을 반환합니다.  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
### <a name="c-using-stcurven-on-a-compoundcurve-containing-three-circularstrings"></a>3. 세 개의 CircularString이 포함된 CompoundCurve에 STCurveN() 사용  
 다음 예제에서는 한 **CompoundCurve** 세 개의 개별 결합 하는 인스턴스 **CircularString** 인스턴스를 동일한 곡선 시퀀스 앞의 예제:  
  
```
 DECLARE @g geography = 'COMPOUNDCURVE (CIRCULARSTRING (-122.358 47.653, -122.348 47.649, -122.348 47.658), CIRCULARSTRING(-122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 이 예에서는 다음을 반환합니다.  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
 `STCurveN()`은 사용되는 WKT(Well-Known Text) 형식과 관계없이 같은 결과를 반환합니다.  
  
### <a name="d-testing-for-validity-before-calling-stcurve"></a>4. STCurve()를 호출하기 전에 유효성 테스트  
 다음 예제에서는 다음 사항을 확인 하는 방법을 보여 줍니다  *n*  stcurven () 메서드를 호출 하기 전에:  
  
```
 DECLARE @g geography;  
 DECLARE @n int;  
 SET @n = 2;  
 SET @g = geography::Parse('LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)');  
 IF @n >= 1 AND @n <= @g.STNumCurves()  
 BEGIN  
 SELECT @g.STCurveN(@n).ToString();  
 END
  ```  
  
## <a name="see-also"></a>관련 항목:  
 [Geography 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  

