---
title: "STNumGeometries (geometry 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STNumGeometries (geometry Data Type)
- STNumGeometries_TSQL
dev_langs: TSQL
helpviewer_keywords: STNumGeometries (geometry Data Type)
ms.assetid: 9402b03d-3039-42ca-ac59-f96b7f1a48de
caps.latest.revision: "22"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0feeee76b0d8da2f3636f6f66e49c350bee1c243
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="stnumgeometries-geometry-data-type"></a>STNumGeometries(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

구성 하는 geometries의 개수를 반환 합니다.는 **geometry** 인스턴스.
  
## <a name="syntax"></a>구문  
  
```  
  
.STNumGeometries ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **int**  
  
 CLR 반환 형식: **SqlInt32**  
  
## <a name="remarks"></a>주의  
 이 메서드는 경우 1을 반환는 **geometry** 인스턴스가 않습니다는 **MultiPoint**, **MultiLineString**, **MultiPolygon**, 또는  **GeometryCollection** 인스턴스와 인 경우 0은 **geometry** 인스턴스가 비어 있습니다.  
  
> [!NOTE]  
>  경우는 **GeometryCollection** 비어 있는 요소에 중첩 된 `STNumGeometries()` 0을 반환 하지 것입니다. 하지만의 요소는 **GeometryCollection** 비어 있는 인스턴스, 인스턴스 자체는 빈 집합 않습니다.  
  
  

