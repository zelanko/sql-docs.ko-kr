---
title: "필터 (geometry 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
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
- Filter
- Filter_TSQL
- Filter (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- Filter method
ms.assetid: 3d629a39-157e-4159-a3ca-a3c2e0ed4160
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e09f4ac5d6d4ecaf32f6b500aee9a3a50c772c02
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="filter-geometry-data-type"></a>Filter(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

여부를 확인 하는 빠른 인덱스 전용 교차 방법을 제공 하는 메서드는 **geometry** 다른 인스턴스와 교차 **기 하 도형** 인스턴스와 인덱스를 사용할 수 있습니다.
  
1을 반환는 **geometry** 교차 될 가능성이 다른 **geometry** 인스턴스. 이 메서드는 거짓 긍정 결과를 반환할 수 있으며 정확한 결과는 계획에 따라 다릅니다. 교차 부분이 있는 경우 정확한 0 값 (참 부정 결과)를 반환 **geometry** 인스턴스를 찾을 수 있습니다.
  
인덱스를 사용할 수 없거나는 사용 되지 않는 경우에서 메서드가 동일한 값으로 반환 됩니다 **stintersects ()** 동일한 매개 변수를 사용 하 여 호출 합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.Filter ( other_geometry )  
```  
  
## <a name="arguments"></a>인수  
 *other_geometry*  
 다른 **geometry** Filter() 호출 된 인스턴스에 대해 비교할 인스턴스입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **비트**  
  
 CLR 반환 형식: **SqlBoolean**  
  
## <a name="remarks"></a>주의  
 이 메서드는 비결정적이고 정확하지 않습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Filter()`를 사용하여 두 `geometry` 인스턴스가 서로 교차하는지 확인합니다.  
  
```  
CREATE TABLE sample (id int primary key, g geometry);  
GO  
INSERT INTO sample VALUES  
   (0, geometry::Point(0, 0, 0)),  
   (1, geometry::Point(0, 1, 0)),  
   (2, geometry::Point(0, 2, 0)),  
   (3, geometry::Point(0, 3, 0)),  
   (4, geometry::Point(0, 4, 0));  
  
CREATE SPATIAL INDEX sample_idx ON sample(g)  
WITH (bounding_box = (-8000, -8000, 8000, 8000));  
GO  
SELECT id  
FROM sample   
WHERE g.Filter(geometry::Parse('POLYGON((-1 -1, 1 -1, 1 1, -1 1, -1 -1))')) = 1;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Geometry 인스턴스의 확장된 메서드](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [STIntersects&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stintersects-geometry-data-type.md)  
  
  

