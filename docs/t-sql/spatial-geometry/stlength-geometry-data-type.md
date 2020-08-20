---
description: STLength(geometry 데이터 형식)
title: STLength(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STLength_TSQL
- STLength (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STLength (geometry Data Type)
ms.assetid: e34dc620-2a65-4248-b099-fff91830ab98
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 713e423d0ef388ea63089bc2b4a203b8affa0fad
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488127"
---
# <a name="stlength-geometry-data-type"></a>STLength(geometry 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

**geometry** 인스턴스에 있는 요소의 총 길이를 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.STLength ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **float**  
  
 CLR 반환 형식: **SqlDouble**  
  
## <a name="remarks"></a>설명  
 **geometry** 인스턴스가 닫힌 경우 해당 길이는 인스턴스의 총 둘레 길이로 계산됩니다. 즉, 모든 다각형의 길이는 해당 둘레의 길이이며 점의 길이는 0입니다. 모든 **geometrycollection** 형식의 길이는 해당 형식의 포함된 **geometry** 인스턴스 길이의 합계입니다.  
  
 STLength()는 유효한 LineString과 잘못된 LineString 둘 다에서 작동합니다. 일반적으로 LineString은 겹치는 세그먼트로 인해 유효하지 않으며, 이는 부정확한 GPS 추적 같은 잘못된 부분 때문에 발생할 수 있습니다. STLength()는 겹친 세그먼트나 잘못된 세그먼트를 제거하지 않습니다. STLength()는 반환하는 길이 값에 겹치는 세그먼트 및 잘못된 세그먼트를 포함합니다. MakeValid() 메서드는 LineString에서 겹치는 세그먼트를 제거할 수 있습니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `LineString` 인스턴스를 만들고 `STLength()`를 사용하여 인스턴스의 길이를 구합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STLength();  
```  
  
## <a name="see-also"></a>참고 항목  
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

