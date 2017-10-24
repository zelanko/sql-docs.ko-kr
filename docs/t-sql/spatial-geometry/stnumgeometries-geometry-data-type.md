---
title: "STNumGeometries (geometry 데이터 형식) | Microsoft Docs"
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
- STNumGeometries (geometry Data Type)
- STNumGeometries_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STNumGeometries (geometry Data Type)
ms.assetid: 9402b03d-3039-42ca-ac59-f96b7f1a48de
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c8ca87eeff2f807b55754d9d9adf19ebf03a4fd8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stnumgeometries-geometry-data-type"></a>STNumGeometries(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

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
  
  


