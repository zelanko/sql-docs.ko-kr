---
title: STGeomCollFromText(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- STGeomCollFromText_TSQL
- STGeomCollFromText (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STGeomCollFromText (geometry Data Type)
ms.assetid: 19e757b3-cb2e-4852-87b9-40a815ab707e
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f014f37142e82cc1c0bbcd85e35b09fa3215cbe8
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36240105"
---
# <a name="stgeomcollfromtext-geometry-data-type"></a>STGeomCollFromText(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

인스턴스에서 얻어진 Z(높이) 값 및 M(측정값) 값을 사용하여 보강된 OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현의 **geometry** 인스턴스를 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
STGeomCollFromText ( 'geometrycollection_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>인수  
 *geometrycollection_tagged_text*  
 반환할 **geometry** 인스턴스의 WKT 표현입니다. *geometry_tagged_text*는 **nvarchar(max)** 식입니다.  
  
 *SRID*  
 반환하려는 **geometry** 인스턴스의 SRID(Spatial Reference ID)를 나타내는 **int** 식입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geometry**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 `STGeomCollFromText()`에 의해 반환되는 **geometry** 인스턴스의 OGC 형식은 해당 WKT 입력으로 설정됩니다.  
  
 이 메서드는 입력이 잘못된 경우 예외를 throw합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `STGeomCollFromText()`를 사용하여 geometry 인스턴스를 만듭니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomCollFromText('GEOMETRYCOLLECTION ( POLYGON((5 5, 10 5, 10 10, 5 5)), POINT(10 10) )', 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>참고 항목  
 [OGC 정적 기하 도형 메서드](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

