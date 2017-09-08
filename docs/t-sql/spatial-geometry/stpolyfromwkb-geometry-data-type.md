---
title: "STPolyFromWKB (geometry 데이터 형식) | Microsoft Docs"
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
- STPolyFromWKB_TSQL
- STPolyFromWKB (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STPolyFromWKB (geometry Data Type)
ms.assetid: 8e8f0c41-0c62-4919-9d4c-d37c93fdd31c
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 30351047adfb97874a48c12f7d7d6221ff301d66
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stpolyfromwkb-geometry-data-type"></a>STPolyFromWKB(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

반환 된 **geometryPolygon** Open Geospatial Consortium (OGC) wkb (WELL-KNOWN Binary) 표현의 인스턴스.
  
## <a name="syntax"></a>구문  
  
```  
  
STPolyFromWKB ( 'WKB_polygon' , SRID )  
```  
  
## <a name="arguments"></a>인수  
 *WKB_polygon*  
 WKB 표현에서 **geometryPolygon** 반환할 인스턴스. *WKB_polygon* 는 **varbinary (max)** 식입니다.  
  
 *SRID*  
 이 **int** spatial 나타내는 식 참조의 ID (SRID)는 **geometryPolygon** 반환할 인스턴스.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **기 하 도형**  
  
 CLR 반환 형식: **SqlGeometry**  
  
 OGC 형식: **다각형**  
  
## <a name="remarks"></a>주의  
 이 메서드는 throw 된 **FormatException** 입력이 잘못 된 경우.  
  
## <a name="examples"></a>예  
 다음 예에서는 `STPolyFromWKB()`를 사용하여 `geometry` 인스턴스를 만듭니다.  
  
```  
DECLARE @g geometry;   
SET @g = geometry::STPolyFromWKB(0x0103000000010000000400000000000000000014400000000000001440000000000000244000000000000014400000000000002440000000000000244000000000000014400000000000001440, 0);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [OGC 정적 기 하 도형 메서드](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  


