---
title: STIsSimple(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIsSimple_TSQL
- STIsSimple (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIsSimple (geometry Data Type)
ms.assetid: da8f45d4-4f9c-405d-b883-760eb5344a71
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 0b91fdde3c6940ffa0a7f2e77591e05578e005c4
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67894914"
---
# <a name="stissimple-geometry-data-type"></a>STIsSimple(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

OGC(Open Geospatial Consortium)에 의해 정의된 대로 **geometry** 인스턴스가 단순하면 1을 반환합니다. **geometry** 인스턴스가 비어 있지 않으면 0을 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.STIsSimple ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **bit**  
  
 CLR 반환 형식: **SqlBoolean**  
  
## <a name="remarks"></a>설명  
 **geometry** 인스턴스를 단순하게 만들려면 다음의 모든 요구 사항을 충족해야 합니다.  
  
-   인스턴스의 각 도형은 엔드포인트를 제외하고 자체 교차해서는 안 됩니다.  
  
-   인스턴스의 도형 두 개가 양쪽의 경계가 아닌 점에서는 서로 교차하지 않아야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 자체 교차하는 복잡한 `LineString` 인스턴스를 만들고 `STIsSimple()`을 사용하여 `LineString`이 단순한지 테스트합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 0 2, 2 0)', 0);  
SELECT @g.STIsSimple();  
```  
  
## <a name="see-also"></a>참고 항목  
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

