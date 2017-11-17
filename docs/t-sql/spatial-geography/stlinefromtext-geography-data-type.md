---
title: "STLineFromText (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 07/30/2017
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
- STLineFromText (geography Data Type)
- STLineFromText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STLineFromText method
ms.assetid: e0c05bde-077d-4ce2-b4ec-8861db9b996d
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7137023a0c382a5114abae4676a5aead8c700f0d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stlinefromtext-geography-data-type"></a>STLineFromText(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

반환 된 **geography** Z (높이) 값 및 M (측정값) 값을 따르도록 Open Geospatial Consortium (OGC) wkt (WELL-KNOWN Text) 표현의 인스턴스는 인스턴스에서 얻어진 합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
STLineFromText ( 'linestring_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>인수  
 *linestring_tagged_text*  
 WKT 표현에서 **geographyLineString** 반환할 인스턴스. *linestring_tagged_text* 는 **nvarchar (max)** 식입니다.  
  
 *SRID*  
 이 **int** spatial 나타내는 식 참조의 ID (SRID)는 **geographyLineString** 반환할 인스턴스.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
 OGC 형식: **LineString**  
  
## <a name="remarks"></a>주의  
 이 메서드에서 throw 한 **FormatException** 입력이 잘못 된 경우.  
  
## <a name="examples"></a>예  
 다음 예에서는 `STLineFromText()`를 사용하여 `geography` 인스턴스를 만듭니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STLineFromText('LINESTRING(-122.360 47.656, -122.343 47.656 )', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [OGC 정적 지리 메서드](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  

