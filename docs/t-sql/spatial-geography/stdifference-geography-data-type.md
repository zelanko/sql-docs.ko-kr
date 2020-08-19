---
description: STDifference(geography 데이터 형식)
title: STDifference(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STDifference_TSQL
- STDifference (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STDifference (geography Data Type)
ms.assetid: 1cde5054-b91a-41bb-812a-08c9308738af
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 067d49755229cad03fe77ae981cf7673d68f536a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88417039"
---
# <a name="stdifference-geography-data-type"></a>STDifference(geography 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  다른 **geography** 인스턴스 밖에 있는 특정 **geogrphy** 인스턴스에서 점 집합을 나타내는 개체를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STDifference ( other_geography )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *other_geography*  
 STDifference()가 호출되는 인스턴스에서 제거할 점을 나타내는 다른 **geometry** 인스턴스입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="exceptions"></a>예외  
 인스턴스에 대척점 끝이 있을 경우 메서드는 **ArgumentException**을 throw합니다.  
  
## <a name="remarks"></a>설명  
 이 메서드는 **geography** 인스턴스의 SRID(satial reference identifier)가 일치하지 않으면 항상 Null을 반환합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 서버에서 반환될 수 있는 결과 집합이 **FullGlobe** 인스턴스까지 확장되었습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 반구보다 큰 공간 인스턴스를 지원합니다. 입력 인스턴스에 원호 세그먼트가 있을 경우에만 결과에 원호 세그먼트가 포함될 수 있습니다. 이 메서드는 정확하지 않습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-computing-the-difference-between-two-geography-instances"></a>A. 두 geography 인스턴스 간의 차이 계산  
 다음 예제에서는 `STDifference()`를 사용하여 두 **geography** 인스턴스 간의 차이를 컴퓨팅합니다.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SET @h = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STDifference(@h).ToString();  
```  
  
### <a name="b-using-a-fullglobe-with-stdifference"></a>B. STDifference()에 FullGlobe 사용  
 다음 예에서는 `FullGlobe` 인스턴스를 사용합니다. 첫 번째 결과는 빈 `GeometryCollection`이고 두 번째 결과는 `Polygon` 인스턴스입니다. `STDifference()` 인스턴스가 매개 변수인 경우 `GeometryCollection`는 빈 `FullGlobe`을 반환합니다. 호출하는 `geography` 인스턴스의 모든 점이 `FullGlobe` 인스턴스에 포함됩니다.  
  
```
 DECLARE @g geography = 'POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 DECLARE @h geography = 'FULLGLOBE';  
 SELECT @g.STDifference(@h).ToString(),  
 @h.STDifference(@g).ToString();
 ```  
  
## <a name="see-also"></a>참고 항목  
 [geography 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
