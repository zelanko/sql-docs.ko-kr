---
description: ToString(geometry 데이터 형식)
title: ToString(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ToString (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- ToString (geometry Data Type)
ms.assetid: 2e55fa98-aa22-4baa-a516-7c233a33e212
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: d5b8e9d4c027dd364c9aaf84b4b8e56680548d0c
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88305663"
---
# <a name="tostring-geometry-data-type"></a>ToString(geometry 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

인스턴스에서 얻어진 Z(높이) 값 및 M(측정값) 값을 사용하여 보강된 geometry 인스턴스의 OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현을 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.ToString ()  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **nvarchar(max)**  
  
 CLR 반환 형식: **SqlString**  
  
## <a name="remarks"></a>설명  
 이 메서드는 Null 인스턴스가 호출되면 문자열 "Null"을 반환합니다.  
  
 Null이 아닌 인스턴스에서 이 메서드는 `AsTextZM().`을 사용하는 것과 동일합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `LineString` 인스턴스를 만들고 `ToString()`을 사용하여 인스턴스의 텍스트 설명을 인출합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 0 1, 1 0)', 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>관련 항목  
 [STAsText&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stastext-geometry-data-type.md)   
 [geometry 인스턴스의 확장 메서드](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

