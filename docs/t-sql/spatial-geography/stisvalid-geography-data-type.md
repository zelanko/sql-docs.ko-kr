---
description: STIsValid(geography 데이터 형식)
title: STIsValid(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STIsValid method (geography)
ms.assetid: 1bfe787f-ddf0-4fc7-af6a-570a58faab23
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: a75d380ce9eed834f24eee2d8e643f3abd5748b0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88445204"
---
# <a name="stisvalid-geography-data-type"></a>STIsValid(geography 데이터 형식)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  **geography** 인스턴스가 해당 OGC(Open Geospatial Consortium) 형식을 기반으로 올바르게 형식이 지정되었으며 올바른 geography 개체로 인식되는 경우 True를 반환합니다. **geography** 인스턴스의 형식이 잘못되었으면 False를 반환합니다. 이 메서드는 정확합니다.  
  
 이 geography 데이터 형식 메서드는 **FullGlobe** 인스턴스 또는 반구보다 큰 공간 인스턴스를 지원합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STIsValid ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **bit**  
  
 CLR 반환 형식: **SqlBoolean**  
  
## <a name="remarks"></a>설명  
 **geography** 인스턴스의 OGC 형식은 [STGeometryType()](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md)을 호출하여 확인할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 올바른 **geography** 인스턴스만 생성하지만 잘못된 인스턴스의 스토리지 및 검색을 허용합니다. 잘못된 인스턴스의 동일한 점 집합을 나타내는 올바른 인스턴스는 `MakeValid()` 메서드를 사용하여 검색할 수 있습니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `geography` 인스턴스를 만들고 `STIsValid()`를 사용하여 인스턴스가 올바른지 테스트합니다.  
  
```  
DECLARE @g geography = geography::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 4326);  
SELECT @g.STIsValid();  
DECLARE @g geography  
```  
  
## <a name="see-also"></a>참고 항목  
 [STGeometryType&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md)   
 [MakeValid&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/makevalid-geography-data-type.md)   
 [Geography 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
