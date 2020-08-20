---
description: STAsText(geometry 데이터 형식)
title: STAsText(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STAsText_TSQL
- STAsText (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STAsText (geometry Data Type)
ms.assetid: e0decf5e-2858-4c56-b61a-6123f47fb51c
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: b04948983ca371a457f7908f48544a73a268ded5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488255"
---
# <a name="stastext-geometry-data-type"></a>STAsText(geometry 데이터 형식)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

**geometry** 인스턴스의 OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현을 반환합니다. 이 텍스트에는 인스턴스에서 얻어진 Z(높이) 값 또는 M(측정값) 값이 포함되지 않습니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.STAsText ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **nvarchar(max)**  
  
 CLR 반환 형식: **SqlChars**  
  
## <a name="examples"></a>예제  
 다음 예에서는 텍스트에서 `LineString` geometry 인스턴스((0,0) - (2,3))를 만듭니다. `STAsText()`는 결과를 텍스트로 반환합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 3)', 0);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>참고 항목  
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

