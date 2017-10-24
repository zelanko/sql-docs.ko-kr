---
title: "STIsClosed (geometry 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STIsClosed_TSQL
- STIsClosed (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIsClosed (geometry Data Type)
ms.assetid: 14edbb22-df7b-4b8a-b16c-ac477a5d32c1
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1fca12de9a05ff424532fa488fda7a306b8a9c37
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stisclosed-geometry-data-type"></a>STIsClosed(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

경우 1을 반환의 시작점 및 끝점은 주어진 **geometry** 인스턴스는 동일 합니다. 에 대 한 1 반환 **geometrycollection** 형식이 지정 된 포함 된 각 **geometry** 인스턴스가 닫혀 있습니다. 인스턴스가 닫혀 있지 않으면 0을 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.STIsClosed ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **비트**  
  
 CLR 반환 형식: **SqlBoolean**  
  
## <a name="remarks"></a>주의  
 이 메서드가 있는 경우 0을 반환의 수치는 **기 하 도형** 인스턴스 요소가 이거나 인스턴스가 비어 있습니다.  
  
 모든 **다각형** 인스턴스는 닫혀 있다고 간주 됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `LineString` 인스턴스를 만들고 `STIsClosed()`를 사용하여 `LineString`이 닫혀 있는지 테스트합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STIsClosed();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


