---
title: "STSrid (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
- STSrid (geography Data Type)
- STSrid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STSrid method
ms.assetid: 6b04f5a7-2e69-4d34-901e-b61ba6ca9c14
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2adbcda7fb699fc4690e0bf9d9b21e83a121508a
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="stsrid-geography-data-type"></a>STSrid(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **STSrid** 는 인스턴스의 spatial reference identifier (SRID)을 나타내는 정수입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STSrid  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]형식: **int**  
  
 CLR 형식: **SqlInt32**  
  
## <a name="remarks"></a>주의  
 이 속성은 수정할 수 있습니다.  
  
## <a name="examples"></a>예  
 첫 번째 예에서는 SRID 값이 4326(WGS84)인 `geography` 인스턴스를 만들고 `STSrid`를 사용하여 SRID를 확인합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STSrid;  
```  
  
 두 번째 예에서는 `STSrid`를 사용하여 인스턴스의 SRID 값을 4267(NAD27)로 변경한 다음 수정된 SRID 값을 확인합니다.  
  
```  
SET @g.STSrid = 4267;  
SELECT @g.STSrid;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Geography 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)   
 [Spatial Reference Identifier &#40; Srid &#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)  
  
  
