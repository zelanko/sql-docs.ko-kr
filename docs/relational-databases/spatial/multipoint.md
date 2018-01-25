---
title: "MultiPoint | Microsoft 문서"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: spatial
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-spatial
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: MultiPoint geometry subtype [SQL Server]
ms.assetid: 2aaab211-3aba-4dbd-90b7-095d997b1f62
caps.latest.revision: "15"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a88fe4695cf9de09cbd9b43ae9fd476508fb46fe
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="multipoint"></a>MultiPoint
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] **MultiPoint**는 0개 이상의 점 컬렉션입니다. **MultiPoint** 인스턴스의 경계는 비어 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 SRID가 23이며 두 개의 점이 있는 `geometry MultiPoint` 인스턴스를 만듭니다. 한 점의 좌표는 (2, 3)이고, 다른 한 점의 좌표는 (7, 8)이며, Z 값은 9.5입니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('MULTIPOINT((2 3), (7 8 9.5))', 23);  
```  
  
 이 `MultiPoint` 인스턴스는 아래에 표시된 대로 `STMPointFromText()` 를 사용하여 표현할 수도 있습니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STMPointFromText('MULTIPOINT((2 3), (7 8 9.5))', 23);  
```  
  
 다음 예에서는 `STGeometryN()` 메서드를 사용하여 컬렉션에서 첫째 점의 설명을 검색합니다.  
  
```  
SELECT @g.STGeometryN(1).STAsText();  
```  
  
## <a name="see-also"></a>참고 항목  
 [점](../../relational-databases/spatial/point.md)   
 [공간 데이터&#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
