---
title: "STMPolyFromText (geometry 데이터 형식) | Microsoft Docs"
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
- STMPolyFromText (geometry Data Type)
- STMPolyFromText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STMPolyFromText (geometry Data Type)
ms.assetid: f087a61c-f063-4fb8-8f1c-251a2fed76a1
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8cc4ef5cbe61b6ccea9b898707814dd398838f5f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stmpolyfromtext-geometry-data-type"></a>STMPolyFromText(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

반환 된 **geometry** Z (높이) 값 및 M (측정값) 값을 포함 하는 Open Geospatial Consortium (OGC) wkt (WELL-KNOWN Text) 표현에서 인스턴스는 인스턴스에서 얻어진 합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
STMPolyFromText ( 'multipolygon_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>인수  
 *multipolygon_tagged_text*  
 WKT 표현에서 **geometryMultiPolygon** 반환할 인스턴스. *multipolygon_tagged_text* 는 **nvarchar (max)** 식입니다.  
  
 *SRID*  
 이 **int** spatial 나타내는 식 참조의 ID (SRID)는 **geometryMultiPolygon** 반환할 인스턴스.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **기 하 도형**  
  
 CLR 반환 형식: **Sql Geometry**  
  
 OGC 형식: **MultiPolygon**  
  
## <a name="remarks"></a>주의  
 이 메서드는 throw 된 **FormatException** 입력이 잘못 된 경우.  
  
## <a name="examples"></a>예  
 다음 예에서는 `STMPolyFromText()`를 사용하여 `geometry` 인스턴스를 만듭니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STMPolyFromText('MULTIPOLYGON (((5 5, 10 5, 10 10, 5 5)), ((10 10, 100 10, 200 200, 30 30, 10 10)))', 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [OGC 정적 기 하 도형 메서드](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  


