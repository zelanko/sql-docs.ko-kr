---
description: ConvexHullAggregate(geometry 데이터 형식)
title: ConvexHullAggregate(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- ConvexHullAggregate method (geometry)
ms.assetid: ca3d3b55-e02d-4599-8817-a54f5e047db8
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: f5f27e06872c72244361fe2973b005924a2b85d5
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96128172"
---
# <a name="convexhullaggregate-geometry-data-type"></a>ConvexHullAggregate(geometry 데이터 형식)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

제공된 **geometry** 개체 집합에 대한 볼록 집합(convex hull)을 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
ConvexHullAggregate ( geometry_operand )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *geometry_operand*  
 기하 도형 개체 집합을 나타내는 **geometry** 형식 테이블 열입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geometry**  
  
## <a name="exception"></a>예외  
 유효하지 않은 입력 값이 있는 경우 `FormatException`을 발생시킵니다. [STIsValid &#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md) 참조  
  
## <a name="remarks"></a>설명  
 이 메서드는 입력이 비어 있거나 입력에 다른 SRID가 있는 경우 **null** 을 반환합니다. [Spatial Reference Identifier&#40;SRIDs&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md) 참조  
  
 이 메서드는 **null** 입력을 무시합니다.  
  
> [!NOTE]  
>  이 메서드는 모든 입력 값이 **null** 인 경우 **null** 을 반환합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 테이블 변수 열에 있는 geometry 개체 집합에 대한 볼록 집합(convex hull)을 반환합니다.  
  
 ```
 -- Setup table variable for ConvexHullAggregate example  
 DECLARE @Geom TABLE  
 (  
 shape geometry,  
 shapeType nvarchar(50)  
 )  
 INSERT INTO @Geom(shape,shapeType) VALUES('CURVEPOLYGON(CIRCULARSTRING(2 3, 4 1, 6 3, 4 5, 2 3))', 'Circle'),  
 ('POLYGON((1 1, 4 1, 4 5, 1 5, 1 1))', 'Rectangle');  
 -- Perform ConvexHullAggregate on @Geom.shape column  
 SELECT geometry::ConvexHullAggregate(shape).ToString()  
 FROM @Geom;
 ```  
  
## <a name="see-also"></a>참고 항목  
 [확장 정적 기하 도형 메서드](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

