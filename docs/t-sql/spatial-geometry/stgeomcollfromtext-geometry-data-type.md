---
title: "STGeomCollFromText (geometry 데이터 형식) | Microsoft Docs"
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
- STGeomCollFromText_TSQL
- STGeomCollFromText (geometry Data Type)
dev_langs: TSQL
helpviewer_keywords: STGeomCollFromText (geometry Data Type)
ms.assetid: 19e757b3-cb2e-4852-87b9-40a815ab707e
caps.latest.revision: "22"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c315862712379ef2e08d25803c5dce2c668b0158
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="stgeomcollfromtext-geometry-data-type"></a>STGeomCollFromText(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

반환 된 **geometry** Z (높이) 값 및 M (측정값) 값을 따르도록 Open Geospatial Consortium (OGC) wkt (WELL-KNOWN Text) 표현의 인스턴스는 인스턴스에서 얻어진 합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
STGeomCollFromText ( 'geometrycollection_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>인수  
 *geometrycollection_tagged_text*  
 WKT 표현에서 **기 하 도형** 반환할 인스턴스. *geometry_tagged_text* 는 **nvarchar (max)** 식입니다.  
  
 *SRID*  
 이 **int** spatial 나타내는 식 참조의 ID (SRID)는 **geometry** 반환할 인스턴스.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **기 하 도형**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="remarks"></a>주의  
 OGC 형식은 **geometry** 에서 반환한 인스턴스 `STGeomCollFromText()` 해당 WKT 입력으로 설정 됩니다.  
  
 이 메서드는 입력이 잘못된 경우 예외를 throw합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `STGeomCollFromText()`를 사용하여 geometry 인스턴스를 만듭니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomCollFromText('GEOMETRYCOLLECTION ( POLYGON((5 5, 10 5, 10 10, 5 5)), POINT(10 10) )', 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [OGC 정적 기하 도형 메서드](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

