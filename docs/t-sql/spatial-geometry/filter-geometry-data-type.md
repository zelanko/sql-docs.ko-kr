---
title: Filter(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b38318d9ca38f5774f15cdac66b9407f2ce4a968
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47832610"
---
# <a name="filter-geometry-data-type"></a>Filter(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

인덱스를 사용할 수 있다고 가정하는 경우 **geometry** 인스턴스가 다른 **geometry** 인스턴스와 교차하는지 확인하는 빠른 인덱스 전용 교차법을 제공하는 메서드입니다.
  
**geometry** 인스턴스가 다른 **geometry** 인스턴스와 교차할 가능성이 있으면 1을 반환합니다. 이 메서드는 거짓 긍정 결과를 반환할 수 있으며 정확한 결과는 계획에 따라 다릅니다. **geometry** 인스턴스가 교차하지 않으면 정확한 0 값을 반환합니다(참 부정 반환).
  
인덱스를 사용할 수 없거나 사용하지 않는 경우 동일한 매개 변수로 호출되면 이 메서드에서 **STIntersects()** 와 동일한 값을 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.Filter ( other_geometry )  
```  
  
## <a name="arguments"></a>인수  
 *other_geometry*  
 Filter()가 호출되는 인스턴스와 비교할 다른 **geometry** 인스턴스입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **bit**  
  
 CLR 반환 형식: **SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
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
  
## <a name="see-also"></a>참고 항목  
 [Geometry 인스턴스의 확장 메서드](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [STIntersects&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stintersects-geometry-data-type.md)  
  
  

