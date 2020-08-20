---
description: STCurveN(geography 데이터 형식)
title: STCurveN(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STCurveN
- STCurveN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveN method (geography)
ms.assetid: 99ef7100-2c4b-4f07-8d66-b343da94b023
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 18d3a992b3f3d5eeecb09a16ce3fb6d582ee2fb2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88479368"
---
# <a name="stcurven-geography-data-type"></a>STCurveN(geography 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  **LineString**, **CircularString** 또는 **CompoundCurve**인 **geography** 인스턴스에서 지정된 곡선을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STCurveN( n )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *n*  
 1과 **geography** 인스턴스에 있는 곡선의 개수 사이의 **int** 식입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="exceptions"></a>예외  
 n < 1인 경우, **ArgumentOutOfRangeException**이 throw 됩니다.  
  
## <a name="remarks"></a>설명  
 다음 조건에서는 **NULL**이 반환됩니다.  
  
-   **geography** 인스턴스가 선언되었지만 인스턴스화되지 않았습니다.  
  
-   **geography** 인스턴스가 비어 있습니다.  
  
-   n은 **geography** 인스턴스의 커브 수를 초과합니다([STNumCurves &#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stnumcurves-geography-data-type.md) 참조).  
  
-   **geography** 인스턴스의 차원이 동일하지 않습니다([STDimension &#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stdimension-geography-data-type.md) 참조).  
  
## <a name="examples"></a>예제  
  
### <a name="a-using-stcurven-on-a-circularstring"></a>A. CircularString에 STCurveN() 사용  
 다음 예제에서는 **CircularString** 인스턴스에 두 번째 곡선을 반환합니다.  
  
```
 DECLARE @g geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 이 예에서는 다음을 반환합니다.  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
### <a name="b-using-stcurven-on-a-compoundcurve"></a>B. CompoundCurve에 STCurveN() 사용  
 다음 예제에서는 **CompoundCurve** 인스턴스에서 두 번째 곡선을 반환합니다.  
  
```
 DECLARE @g geography = 'COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 이 예에서는 다음을 반환합니다.  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
### <a name="c-using-stcurven-on-a-compoundcurve-containing-three-circularstrings"></a>C. 세 개의 CircularString이 포함된 CompoundCurve에 STCurveN() 사용  
 다음 예제에서는 별도의 **CircularString** 인스턴스 세 개를 이전 예와 동일한 곡선 시퀀스로 조합하는 **CompoundCurve** 인스턴스를 사용합니다.  
  
```
 DECLARE @g geography = 'COMPOUNDCURVE (CIRCULARSTRING (-122.358 47.653, -122.348 47.649, -122.348 47.658), CIRCULARSTRING(-122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 이 예에서는 다음을 반환합니다.  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
 `STCurveN()`은 사용되는 WKT(Well-Known Text) 형식과 관계없이 같은 결과를 반환합니다.  
  
### <a name="d-testing-for-validity-before-calling-stcurve"></a>D. STCurve()를 호출하기 전에 유효성 테스트  
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
 [Geography 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
