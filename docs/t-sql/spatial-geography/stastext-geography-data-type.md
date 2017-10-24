---
title: "STAsText (geography 데이터 형식) | Microsoft Docs"
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
- STAsText (geography Data Type)
- STAsText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STAsText method
ms.assetid: d3d2635d-ca6c-4205-9d6c-eb939ee314fd
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4f29024f7ac82979771fc897a9efc6860af08a9a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stastext-geography-data-type"></a>STAsText(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Open Geospatial Consortium (OGC) wkt (WELL-KNOWN Text) 표현을 반환는 **geography** 인스턴스. 이 텍스트에는 인스턴스에서 얻어진 Z(높이) 값 또는 M(측정값) 값이 포함되지 않습니다.  
  
 이 **geography** 데이터 형식 메서드 지원 **FullGlobe** 인스턴스 또는 반구 보다 큰 공간 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STAsText ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **nvarchar (max)**  
  
 CLR 반환 형식: **SqlChars**  
  
## <a name="remarks"></a>주의  
 OGC 형식은 **geography** 를 호출 하 여 인스턴스를 확인할 수 있습니다 [stgeometrytype ()](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md)합니다.  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], 서버에서 반환 된 결과 집합이 확장 되었습니다 **FullGlobe** 인스턴스.  
  
## <a name="examples"></a>예  
 다음 예제에서는 `STAsText()` 만들려는 `LineString``geography` 에서 인스턴스 (122.360, 47.656)을 (-122.343, 47.656) 텍스트에서 합니다. 그런 다음 텍스트로 결과를 반환합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Geography 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  

