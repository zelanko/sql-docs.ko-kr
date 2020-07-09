---
title: InstanceOf(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- InstanceOf
- InstanceOf_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- InstanceOf method
ms.assetid: 1eaed0e4-1c72-45a9-9926-5b513335cf33
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 3a6939de145d3e63341bddda70d6fa04d9af9b69
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85731153"
---
# <a name="instanceof-geography-data-type"></a>InstanceOf(geography 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

**geography** 인스턴스가 지정된 유형과 동일한지 여부를 테스트합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
  
.InstanceOf ( 'geography_type')  
```  
  
## <a name="arguments"></a>인수  
*geography_type*  
**geography** 형식 계층에 노출되는 16개의 형식 중 하나를 지정하는 **nvarchar(4000)** 문자열입니다.  
  
## <a name="return-types"></a>반환 형식  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **bit**  
  
CLR 반환 형식: **SqlBoolean**  
  
## <a name="remarks"></a>설명  
**geography** 인스턴스의 유형이 지정된 유형과 동일하거나 지정된 유형이 인스턴스 유형의 상위 항목이면 1을 반환하고, 그렇지 않으면 0을 반환합니다.  
  
이 **geography** 데이터 형식 메서드는 **FullGlobe** 인스턴스 또는 반구보다 큰 공간 인스턴스를 지원합니다.  
  
메서드의 입력은 다음 유형 중 하나여야 합니다. Geometry, Point, Curve, LineString,CircularString, Surface, Polygon, CurvePolygon, **GeometryCollection**, **MultiSurface**, **MultiPolygon, MultiCurve, MultiLineString**, **MultiPoint** 또는 **FullGlobe**.  
  
이 메서드는 다른 문자열이 입력에 사용되면 `ArgumentException`을 throw합니다.  
  
이 메서드는 정확하지 않습니다.  
  
## <a name="examples"></a>예  
다음 예에서는 `MultiPoint` 인스턴스를 만들고 `InstanceOf()`를 사용하여 인스턴스가 `GeometryCollection`인지 확인합니다.  
  
```sql  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('MULTIPOINT(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.InstanceOf('GEOMETRYCOLLECTION');  
```  
  
## <a name="see-also"></a>참고 항목  
 [지리 인스턴스의 확장 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
