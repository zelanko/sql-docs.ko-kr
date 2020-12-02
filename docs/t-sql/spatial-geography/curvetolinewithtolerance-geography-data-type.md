---
description: CurveToLineWithTolerance(geography 데이터 형식)
title: CurveToLineWithTolerance(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CurveToLineWithTolerance_TSQL
- CurveToLineWithTolerance
dev_langs:
- TSQL
helpviewer_keywords:
- CurveToLineWithTolerance method (geography)
ms.assetid: 74369c76-2cf6-42ae-b9cc-e7a051db2767
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: d4852ff1e43bb561cffa7d001df33793e5f00e81
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96124342"
---
# <a name="curvetolinewithtolerance-geography-data-type"></a>CurveToLineWithTolerance(geography 데이터 형식)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

원호 세그먼트가 포함된 **geography** 인스턴스의 다각형 근사값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.CurveToLineWithTolerance( tolerance, relative )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
_tolerance_  
원래의 원호 세그먼트와 선형 근사값 사이의 최대 오차를 정의하는 **double** 식입니다.  
  
_relative_  
편차에 대해 극대값을 사용할지 여부를 나타내는 **bool** 식입니다. 극대값이 false(0)이면 선형 근삿값이 가질 수 있는 편차에 대해 최댓값이 설정됩니다. 극대값이 true(1)이면 허용 오차는 허용 오차 매개 변수와 공간 개체의 경계 상자 지름의 곱으로 계산됩니다.  
  
## <a name="return-types"></a>반환 형식  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
CLR 반환 형식: **SqlGeography**  
  
## <a name="exceptions"></a>예외  
허용 오차 <= 0를 설정하면 **ArgumentOutOfRange** 예외가 발생합니다.  
  
## <a name="remarks"></a>설명  
이 메서드를 사용하면 결과 **LineString** 에 대해 허용 오차 크기가 지정됩니다.  
  
**CurveToLineWithTolerance** 메서드는 **CircularString** 또는 **CompoundCurve** 인스턴스에 대한 **LineString** 인스턴스와 **CurvePolygon** 인스턴스에 대한 **Polygon** 인스턴스를 반환합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-using-different-tolerance-values-on-a-circularstring-instance"></a>A. CircularString 인스턴스에 여러 허용 오차 값 사용  
다음 예에서는 허용 오차를 설정하면 `CircularString` 인스턴스에서 반환된 `LineString`인스턴스가 어떤 영향을 받는지 보여 줍니다.  
  
```
DECLARE @g geography;  
SET @g = geography::Parse('CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)');  
SELECT @g.CurveToLineWithTolerance(0.1,0).STNumPoints(), @g.CurveToLineWithTolerance(0.01, 0).STNumPoints();
```  
  
### <a name="b-using-the-method-on-a-multilinestring-instance-containing-one-linestring"></a>B. LineString 하나를 포함하는 MultiLineString 인스턴스에 메서드 사용  
다음 예에서는 `MultiLineString` 인스턴스 하나만 포함하는 `LineString` 인스턴스에서 반환되는 결과를 보여 줍니다.  
  
```
DECLARE @g geography;  
SET @g = geography::Parse('MULTILINESTRING((-122.358 47.653, -122.348 47.649))');  
SELECT @g.CurveToLineWithTolerance(0.1,0).ToString();
```  
  
### <a name="c-using-the-method-on-a-multilinestring-instance-containing-multiple-linestrings"></a>C. 여러 LineString을 포함하는 MultiLineString 인스턴스에 메서드 사용  
다음 예에서는 `MultiLineString` 인스턴스를 둘 이상 포함하는 `LineString` 인스턴스에서 반환되는 결과를 보여 줍니다.  
  
```
DECLARE @g geography;  
SET @g = geography::Parse('MULTILINESTRING((-122.358 47.653, -122.348 47.649),(-123.358 47.653, -123.348 47.649))');  
SELECT @g.CurveToLineWithTolerance(0.1,0).ToString();
```  
  
### <a name="d-setting-relative-to-true-for-an-invoking-curvepolygon-instance"></a>D. 호출하는 CurvePolygon 인스턴스에 대해 극대값을 true로 설정  
다음 예에서는 *relative* 를 true로 설정하여 `CurvePolygon` 인스턴스를 사용해 `CurveToLineWithTolerance()`를 호출합니다.  
  
```
DECLARE @g geography = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658), (-122.348 47.658, -122.358 47.658, -122.358 47.653)))';  
SELECT @g.CurveToLineWithTolerance(.5,1).ToString();
```  
  
## <a name="see-also"></a>참고 항목  
[지리 인스턴스의 확장 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
