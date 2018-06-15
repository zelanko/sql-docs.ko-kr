---
title: CurveToLineWithTolerance(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CurveToLineWithTolerance_TSQL
- CurveToLineWithTolerance
dev_langs:
- TSQL
helpviewer_keywords:
- CurveToLineWithTolerance method (geography)
ms.assetid: 74369c76-2cf6-42ae-b9cc-e7a051db2767
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e5445cce83bfc6328606b4a2fa0f55ffe37587f1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33061790"
---
# <a name="curvetolinewithtolerance-geography-data-type"></a>CurveToLineWithTolerance(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  원호 세그먼트가 포함된 **geography** 인스턴스의 다각형 근사값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.CurveToLineWithTolerance( tolerance, relative )  
```  
  
## <a name="arguments"></a>인수  
 *tolerance*  
 원래의 원호 세그먼트와 선형 근사값 사이의 최대 오차를 정의하는 **double** 식입니다.  
  
 *relative*  
 편차에 대해 극대값을 사용할지 여부를 나타내는 **bool** 식입니다. 극대값이 false(0)로 설정되면 선형 근사값이 가질 수 있는 편차에 대해 최대값이 설정됩니다.  극대값이 true(1)로 설정되면 허용 오차는 허용 오차 매개 변수와 공간 개체의 경계 상자 지름의 곱으로 계산됩니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="exceptions"></a>예외  
 허용 오차 <= 0를 설정하면 **ArgumentOutOfRange** 예외가 발생합니다.  
  
## <a name="remarks"></a>Remarks  
 이 메서드를 사용하면 결과 **LineString**에 대해 허용 오차 크기가 지정됩니다.  
  
 **CurveToLineWithTolerance** 메서드는 **CircularString** 또는 **CompoundCurve** 인스턴스에 대한 **LineString** 인스턴스와 **CurvePolygon** 인스턴스에 대한 **Polygon** 인스턴스를 반환합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-different-tolerance-values-on-a-circularstring-instance"></a>1. CircularString 인스턴스에 여러 허용 오차 값 사용  
 다음 예에서는 허용 오차를 설정하면 `CircularString` 인스턴스에서 반환된 `LineString`인스턴스가 어떤 영향을 받는지 보여 줍니다.  
  
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
 다음 예에서는 *relative*를 true로 설정하여 `CurvePolygon` 인스턴스를 사용해 `CurveToLineWithTolerance()`를 호출합니다.  
  
 ```
 DECLARE @g geography = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658), (-122.348 47.658, -122.358 47.658, -122.358 47.653)))';  
 SELECT @g.CurveToLineWithTolerance(.5,1).ToString();
 ```  
  
## <a name="see-also"></a>참고 항목  
 [지리 인스턴스의 확장 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
