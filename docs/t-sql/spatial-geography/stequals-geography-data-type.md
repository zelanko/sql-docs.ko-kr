---
title: "STEquals(geography 데이터 형식) | Microsoft Docs"
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
- STEquals_TSQL
- STEquals (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STEquals method
ms.assetid: 0766ff37-0b9e-49bf-83c0-019f4354fe44
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 43b86d121e1877f63465398ace833c84321c0096
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="stequals-geography-data-type"></a>STEquals(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  **geography** 인스턴스가 다른 **geography** 인스턴스와 동일한 점 집합을 나타내면 1을 반환합니다. 그렇지 않으면 0을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STEquals ( other_geography )  
```  
  
## <a name="arguments"></a>인수  
 *other_geography*  
 `STEquals()`가 호출되는 인스턴스와 비교할 다른 **geography** 인스턴스입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **bit**  
  
 CLR 반환 형식: **SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 이 메서드는 **geography** 인스턴스의 SRID(spatial Reference ID)가 일치하지 않으면 항상 Null을 반환합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 동일하지만 약간 다른 `geography`를 사용하여 두 개의 `STGeomFromText()` 인스턴스를 만들고 `STEquals()`를 사용하여 서로 같은지 테스트합니다. `LINESTRING`과 `POINT`가 `POLYGON` 내에 포함되므로 이들 인스턴스는 서로 같습니다.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('GEOMETRYCOLLECTION(POLYGON((-122.368 47.658, -122.338 47.649, -122.338 47.658, -122.368 47.658, -122.368 47.658)), LINESTRING(-122.360 47.656, -122.343 47.656), POINT (-122.35 47.656))', 4326);  
SET @h = geography::STGeomFromText('POLYGON((-122.368 47.658, -122.338 47.649, -122.338 47.658, -122.368 47.658, -122.368 47.658))', 4326);  
SELECT @g.STEquals(@h);  
```  
  
## <a name="see-also"></a>참고 항목  
 [지리 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
