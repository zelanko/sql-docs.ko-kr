---
description: STWithin(geometry 데이터 형식)
title: STWithin(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STWithin_TSQL
- STWithin (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STWithin (geometry Data Type)
ms.assetid: f845d28c-8029-4e2b-bcf0-71c52a592501
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: f0a9d615fcb05ed6b1c9ada74a98038de9f84e66
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488115"
---
# <a name="stwithin-geometry-data-type"></a>STWithin(geometry 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

**geometry** 인스턴스가 다른 **geometry** 인스턴스에 완전히 포함되면 1을 반환하고, 그렇지 않으면 0을 반환합니다. `STWithin` 명령은 대/소문자를 구분합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.STWithin ( other_geometry )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *other_geometry*  
 `STWithin()`를 호출할 인스턴스와 비교할 다른 **geometry** 인스턴스입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **bit**  
  
 CLR 반환 형식: **SqlBoolean**  
  
## <a name="remarks"></a>설명  
 이 메서드는 **geometry** 인스턴스의 SRID(spatial Reference ID)가 일치하지 않으면 항상 Null을 반환합니다.
  
## <a name="examples"></a>예제  
 다음 예에서는 `STWithin()`을 사용하여 두 `geometry` 인스턴스를 테스트하여 첫 번째 인스턴스가 두 번째 인스턴스에 완전히 포함되는지 확인합니다.  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 2 0, 2 2, 0 2, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POLYGON((1 1, 3 1, 3 3, 1 3, 1 1))', 0);  
SELECT @g.STWithin(@h);  
```  
  
## <a name="see-also"></a>관련 항목  
 [공간 인덱스 개요](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

