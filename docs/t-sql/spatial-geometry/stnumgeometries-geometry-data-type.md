---
title: STNumGeometries(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STNumGeometries (geometry Data Type)
- STNumGeometries_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STNumGeometries (geometry Data Type)
ms.assetid: 9402b03d-3039-42ca-ac59-f96b7f1a48de
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 3bd050fc07c39dc33781a2c9c1ec09128540f216
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85762279"
---
# <a name="stnumgeometries-geometry-data-type"></a>STNumGeometries(geometry 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

**geometry** 인스턴스를 구성하는 기하 도형의 개수를 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.STNumGeometries ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **int**  
  
 CLR 반환 형식: **SqlInt32**  
  
## <a name="remarks"></a>설명  
 이 메서드는 **geometry** 인스턴스가 **MultiPoint**, **MultiLineString**, **MultiPolygon** 또는 **GeometryCollection** 인스턴스가 아닌 경우 1을 반환하고, **geometry** 인스턴스가 비어 있으면 0을 반환합니다.  
  
> [!NOTE]  
>  **GeometryCollection**에 중첩된 빈 요소가 있으면 `STNumGeometries()`은 0을 반환하지 않습니다. **GeometryCollection** 인스턴스에 빈 요소가 있어도 인스턴스 자체가 빈 집합은 아닙니다.  
  
  

