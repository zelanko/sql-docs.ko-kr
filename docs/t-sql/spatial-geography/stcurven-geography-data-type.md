---
title: "STCurveN(geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
f1_keywords:
- STCurveN
- STCurveN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveN method (geography)
ms.assetid: 99ef7100-2c4b-4f07-8d66-b343da94b023
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 59709f07fa84c24942ed14a8f8af7e776643913f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="stcurven-geography-data-type"></a>STCurveN(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **LineString**, **CircularString** 또는 **CompoundCurve**인 **geography** 인스턴스에서 지정된 곡선을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STCurveN( n )  
```  
  
## <a name="arguments"></a>인수  
 *n*  
 1과 **geography** 인스턴스에 있는 곡선의 개수 사이의 **int** 식입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="exceptions"></a>예외  
 n < 1인 경우, **ArgumentOutOfRangeException**이 throw 됩니다.  
  
## <a name="remarks"></a>Remarks  
 다음 조건에서는 **NULL**이 반환됩니다.  
  
-   **geography** 인스턴스가 선언되었지만 인스턴스화되지 않았습니다.  
  
-   **geography** 인스턴스가 비어 있습니다.  
  
-   n은 **geography** 인스턴스의 커브 수를 초과합니다([STNumCurves &#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stnumcurves-geography-data-type.md) 참조).  
  
-   **geography** 인스턴스의 차원이 동일하지 않습니다([STDimension &#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stdimension-geography-data-type.md) 참조).  
  
## <a name="examples"></a>예  
  
### <a name="a-using-stcurven-on-a-circularstring"></a>1. CircularString에 STCurveN() 사용  
 다음 예제에서는 **CircularString** 인스턴스에 두 번째 곡선을 반환합니다.  
  
```
 DECLARE @g geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 이 예에서는 다음을 반환합니다.  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
### <a name="b-using-stcurven-on-a-compoundcurve"></a>2. CompoundCurve에 STCurveN() 사용  
 다음 예제에서는 **CompoundCurve** 인스턴스에서 두 번째 곡선을 반환합니다.  
  
```
 DECLARE @g geography = 'COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 이 예에서는 다음을 반환합니다.  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
### <a name="c-using-stcurven-on-a-compoundcurve-containing-three-circularstrings"></a>3. 세 개의 CircularString이 포함된 CompoundCurve에 STCurveN() 사용  
 다음 예제에서는 별도의 **CircularString** 인스턴스 세 개를 이전 예와 동일한 곡선 시퀀스로 조합하는 **CompoundCurve** 인스턴스를 사용합니다.  
  
```
 DECLARE @g geography = 'COMPOUNDCURVE (CIRCULARSTRING (-122.358 47.653, -122.348 47.649, -122.348 47.658), CIRCULARSTRING(-122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 이 예에서는 다음을 반환합니다.  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
 `STCurveN()`은 사용되는 WKT(Well-Known Text) 형식과 관계없이 같은 결과를 반환합니다.  
  
### <a name="d-testing-for-validity-before-calling-stcurve"></a>4. STCurve()를 호출하기 전에 유효성 테스트  
 다음 예제에서는 STCurveN() 메서드를 호출하기 전에 *n*이 유효한지 확인하는 방법을 보여 줍니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [지리 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
