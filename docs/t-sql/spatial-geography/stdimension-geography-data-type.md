---
title: "STDimension (geography 데이터 형식) | Microsoft Docs"
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
- STDimension (geography Data Type)
- STDimension_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STDimension method
ms.assetid: 4368b0f6-0678-4ade-87dc-b43d8b2e8d92
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0026ae44feb99e398a4502488d52594dac3b6bd4
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stdimension-geography-data-type"></a>STDimension(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  최대 차원을 반환는 **geography** 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STDimension ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **int**  
  
 CLR 반환 형식: **SqlInt32**  
  
## <a name="remarks"></a>주의  
 STDimension()-1을 반환 하는 경우는 **geography** 인스턴스가 비어 있습니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 `STDimension()` 를 보유 하는 테이블 변수를 만들려면 `geography` 인스턴스와 삽입 한 `Point`, `LineString`, 및 `Polygon`합니다.  
  
```  
DECLARE @temp table ([name] varchar(10), [geom] geography);  
  
INSERT INTO @temp values ('Point', geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326));  
INSERT INTO @temp values ('LineString', geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326));  
INSERT INTO @temp values ('Polygon', geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326));  
  
SELECT [name], [geom].STDimension() as [dim]  
FROM @temp;  
```  
  
 이 예에서는 다음 각각의 크기를 반환 `geography`인스턴스.  
  
|name|dim|  
|----------|---------|  
|점|0|  
|LineString|1.|  
|다각형|2|  
  
## <a name="see-also"></a>관련 항목:  
 [Geography 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  

