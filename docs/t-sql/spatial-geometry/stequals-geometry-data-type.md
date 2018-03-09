---
title: "STEquals (geometry 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
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
- STEquals (geometry Data Type)
- STEquals_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STEquals (geometry Data Type)
ms.assetid: 808f0e25-9e68-4ba7-9329-07ec950698f3
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8e7aadcdf5d0527fe46337f56c5e98017afc4dd7
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="stequals-geometry-data-type"></a>STEquals(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

1을 반환는 **geometry** 인스턴스가 동일한 점 집합으로 다른 나타내는 **기 하 도형** 인스턴스. 그렇지 않으면 0을 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.STEquals ( other_geometry )  
```  
  
## <a name="arguments"></a>인수  
 *other_geometry*  
 다른 **geometry** 인스턴스와 비교할 인스턴스 `STEquals()` 가 호출 됩니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **비트**  
  
 CLR 반환 형식: **SqlBoolean**  
  
## <a name="remarks"></a>주의  
 항상 null이 반환 하는 경우의 spatial reference Id (Srid)는 **geometry** 인스턴스 일치 하지 않습니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 두 개의 `geometry` 인스턴스 `STGeomFromText()` 는 동일 하지만 약간 다른을 사용 하 여 `STEquals()` 같은지 테스트 합니다.  
  
```  
DECLARE @g geometry  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0, 4 2)', 0);  
SET @h = geometry::STGeomFromText('MULTILINESTRING((4 2, 2 0), (0 2, 2 0))', 0);  
SELECT @g.STEquals(@h);  
```  
  
## <a name="see-also"></a>관련 항목:  
 [공간 인덱스 개요](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

