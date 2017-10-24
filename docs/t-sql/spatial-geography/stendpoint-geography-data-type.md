---
title: "STEndpoint (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STEndpoint (geography Data Type)
- STEndpoint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STEndpoint method
ms.assetid: 8974cd07-8ec4-4126-8fc2-fdcf322ccedd
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 22432c6493c343124f6a60d0238d10f6417b7431
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stendpoint-geography-data-type"></a>STEndpoint(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  반환 끝점에는 **geography** 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STEndPoint ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
 열기 Geospatial Consortium (OGC) 입력: **지점**  
  
## <a name="remarks"></a>주의  
 STEndPoint() 같습니다 [STPointN](../../t-sql/spatial-geography/stpointn-geography-data-type.md)`(x.STNumPoints``())`합니다.  
  
 이 메서드는 비어 있는 메서드를 호출 하면 null을 반환 **geography** 인스턴스.  
  
## <a name="examples"></a>예  
 다음 예에서는 `LineString`를 사용하여 `STGeomFromText()` 인스턴스를 만들고 `STEndpoint()`를 사용하여 `LineString`의 끝점을 검색합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STEndPoint().ToString();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Geography 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  

