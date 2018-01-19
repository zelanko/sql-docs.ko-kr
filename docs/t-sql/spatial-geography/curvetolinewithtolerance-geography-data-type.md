---
title: "CurveToLineWithTolerance (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CurveToLineWithTolerance_TSQL
- CurveToLineWithTolerance
dev_langs: TSQL
helpviewer_keywords: CurveToLineWithTolerance method (geography)
ms.assetid: 74369c76-2cf6-42ae-b9cc-e7a051db2767
caps.latest.revision: "11"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 497daed444f29db051ac11f6f0c2c2b87011fd80
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="curvetolinewithtolerance-geography-data-type"></a>CurveToLineWithTolerance(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  다각형 근사값을 반환 합니다.는 **geography** 원호 세그먼트가 포함 된 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```  
  
.CurveToLineWithTolerance( tolerance, relative )  
```  
  
## <a name="arguments"></a>인수  
 *tolerance*  
 이 **double** 원래의 원호 세그먼트와 선형 근사값 사이의 최대 오차를 정의 하는 식입니다.  
  
 *relative*  
 이 **bool** 편차에 대해 극대를 사용할지 여부를 나타내는 식입니다. 극대값이 false(0)로 설정되면 선형 근사값이 가질 수 있는 편차에 대해 최대값이 설정됩니다.  극대값이 true(1)로 설정되면 허용 오차는 허용 오차 매개 변수와 공간 개체의 경계 상자 지름의 곱으로 계산됩니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="exceptions"></a>예외  
 허용 오차를 설정 < = 0는 **ArgumentOutOfRange** 예외입니다.  
  
## <a name="remarks"></a>주의  
 이 메서드를 사용 하면 결과 대 한 지정 된 허용 오차 크기가 **LineString**합니다.  
  
 **CurveToLineWithTolerance** 메서드는 반환 된 **LineString** 에 대 한 인스턴스는 **CircularString** 또는 **CompoundCurve** 인스턴스와 **다각형** 에 대 한 인스턴스는 **CurvePolygon** 인스턴스.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-different-tolerance-values-on-a-circularstring-instance"></a>1. CircularString 인스턴스에 여러 허용 오차 값 사용  
 다음 예제에서는 영향을 어떻게 설정 된 허용 오차는 `LineString`에서 반환 된 인스턴스는 `CircularString` 인스턴스:  
  
 ```
 DECLARE @g geography;  
 SET @g = geography::Parse('CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)');  
 SELECT @g.CurveToLineWithTolerance(0.1,0).STNumPoints(), @g.CurveToLineWithTolerance(0.01, 0).STNumPoints();
```  
  
### <a name="b-using-the-method-on-a-multilinestring-instance-containing-one-linestring"></a>2. LineString 하나를 포함하는 MultiLineString 인스턴스에 메서드 사용  
 다음 예에서는 `MultiLineString` 인스턴스 하나만 포함하는 `LineString` 인스턴스에서 반환되는 결과를 보여 줍니다.  
  
 ```
 DECLARE @g geography;  
 SET @g = geography::Parse('MULTILINESTRING((-122.358 47.653, -122.348 47.649))');  
 SELECT @g.CurveToLineWithTolerance(0.1,0).ToString();
 ```  
  
### <a name="c-using-the-method-on-a-multilinestring-instance-containing-multiple-linestrings"></a>3. 여러 LineString을 포함하는 MultiLineString 인스턴스에 메서드 사용  
 다음 예에서는 `MultiLineString` 인스턴스를 둘 이상 포함하는 `LineString` 인스턴스에서 반환되는 결과를 보여 줍니다.  
  
 ```
 DECLARE @g geography;  
 SET @g = geography::Parse('MULTILINESTRING((-122.358 47.653, -122.348 47.649),(-123.358 47.653, -123.348 47.649))');  
 SELECT @g.CurveToLineWithTolerance(0.1,0).ToString();
 ```  
  
### <a name="d-setting-relative-to-true-for-an-invoking-curvepolygon-instance"></a>4. 호출하는 CurvePolygon 인스턴스에 대해 극대값을 true로 설정  
 다음 예제에서는 한 `CurvePolygon` 호출 하는 인스턴스 `CurveToLineWithTolerance()` 와 *상대* true로 설정:  
  
 ```
 DECLARE @g geography = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658), (-122.348 47.658, -122.358 47.658, -122.358 47.653)))';  
 SELECT @g.CurveToLineWithTolerance(.5,1).ToString();
 ```  
  
## <a name="see-also"></a>관련 항목:  
 [지리 인스턴스의 확장 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
