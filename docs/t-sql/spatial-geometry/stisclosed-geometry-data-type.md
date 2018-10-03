---
title: STIsClosed(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIsClosed_TSQL
- STIsClosed (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIsClosed (geometry Data Type)
ms.assetid: 14edbb22-df7b-4b8a-b16c-ac477a5d32c1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5be28fe6b1533c6920c83171130a2d4104784fe2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47779147"
---
# <a name="stisclosed-geometry-data-type"></a>STIsClosed(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

주어진 **geometry** 인스턴스의 시작점 및 끝점이 동일하면 1을 반환합니다. 포함된 각 **geometry** 인스턴스가 닫혀 있으면 **geometrycollection** 형식에 대해 1을 반환하고, 인스턴스가 닫혀 있지 않으면 0을 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.STIsClosed ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **bit**  
  
 CLR 반환 형식: **SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 이 메서드는 **geometry** 인스턴스의 도형이 점이거나 인스턴스가 비어 있으면 0을 반환합니다.  
  
 모든 **Polygon** 인스턴스는 닫혀 있다고 간주됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `LineString` 인스턴스를 만들고 `STIsClosed()`를 사용하여 `LineString`이 닫혀 있는지 테스트합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STIsClosed();  
```  
  
## <a name="see-also"></a>참고 항목  
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

