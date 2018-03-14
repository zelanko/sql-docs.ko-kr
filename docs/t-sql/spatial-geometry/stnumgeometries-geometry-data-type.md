---
title: "STNumGeometries(geometry 데이터 형식) | Microsoft Docs"
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
- STNumGeometries (geometry Data Type)
- STNumGeometries_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STNumGeometries (geometry Data Type)
ms.assetid: 9402b03d-3039-42ca-ac59-f96b7f1a48de
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f4094aa647ddfa3bf5ffaf191896c9e65677f027
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="stnumgeometries-geometry-data-type"></a>STNumGeometries(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

**geometry** 인스턴스를 구성하는 기하 도형의 개수를 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.STNumGeometries ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **int**  
  
 CLR 반환 형식: **SqlInt32**  
  
## <a name="remarks"></a>Remarks  
 이 메서드는 **geometry** 인스턴스가 **MultiPoint**, **MultiLineString**, **MultiPolygon** 또는 **GeometryCollection** 인스턴스가 아닌 경우 1을 반환하고, **geometry** 인스턴스가 비어 있으면 0을 반환합니다.  
  
> [!NOTE]  
>  **GeometryCollection**에 중첩된 빈 요소가 있으면 `STNumGeometries()`은 0을 반환하지 않습니다. **GeometryCollection** 인스턴스에 빈 요소가 있어도 인스턴스 자체가 빈 집합은 아닙니다.  
  
  

