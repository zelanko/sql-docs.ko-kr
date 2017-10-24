---
title: "STSrid (geometry 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STSrid (geometry Data Type)
- STSrid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STSrid (geometry Data Type)
ms.assetid: 5e0de983-a0fe-48b7-9e08-30588d7271e2
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9e8e29a1a5446713c94462bdcf4d0c252875d7c0
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stsrid-geometry-data-type"></a>STSrid(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **STSrid** 는 인스턴스의 spatial reference identifier를 나타내는 정수입니다.  
  
이 속성은 수정할 수 있습니다.
  
## <a name="syntax"></a>구문  
  
```  
  
STSrid  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]형식: **int**  
  
 CLR 형식: **SqlInt32**  
  
## <a name="examples"></a>예  
 첫 번째 예제에서는 **기 하 도형** SRID 값을 가진 인스턴스 13 및 사용 하 여 `STSrid` SRID를 확인 합니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [STX&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stx-geometry-data-type.md)   
 [STY&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/sty-geometry-data-type.md)   
 [Geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


