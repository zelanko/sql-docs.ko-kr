---
title: STSrid(geometry 데이터 형식) | Miciosoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STSrid (geometry Data Type)
- STSrid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STSrid (geometry Data Type)
ms.assetid: 5e0de983-a0fe-48b7-9e08-30588d7271e2
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: e2611f5bfee1a74e961fee69af3dfb58d0530fcd
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85762172"
---
# <a name="stsrid-geometry-data-type"></a>STSrid(geometry 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  **STSrid**는 인스턴스의 Spatial Reference Identifier를 나타내는 정수입니다.  
  
이 속성은 수정할 수 있습니다.
  
## <a name="syntax"></a>구문  
  
```  
  
STSrid  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 형식: **int**  
  
 CLR 형식: **SqlInt32**  
  
## <a name="examples"></a>예  
 첫 번째 예제에서는 SRID 값이 13인 **geometry** 인스턴스를 만들고 `STSrid`를 사용하여 SRID를 확인합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0))', 13);  
SELECT @g.STSrid;  
```  
  
 두 번째 예에서는 `STSrid`를 사용하여 인스턴스의 SRID 값을 23으로 변경한 다음 수정된 SRID 값을 확인합니다.  
  
```  
SET @g.STSrid = 23;  
SELECT @g.STSrid;  
```  
  
## <a name="see-also"></a>참고 항목  
 [STX&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stx-geometry-data-type.md)   
 [STY&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/sty-geometry-data-type.md)   
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

