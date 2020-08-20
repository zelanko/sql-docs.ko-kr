---
description: Filter(geography 데이터 형식)
title: Filter(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Filter
- Filter_TSQL
- Filter (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- Filter method
ms.assetid: 82a8f54a-3a47-4e20-b13a-b148029c5448
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 4a5e5ff41504184bd8c1aa0805267f38566b5162
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88479361"
---
# <a name="filter-geography-data-type"></a>Filter(geography 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  인덱스를 사용할 수 있다고 가정하는 경우 **geography** 인스턴스가 다른 **geography** 인스턴스와 교차하는지 확인하는 빠른 인덱스 전용 교차법을 제공하는 메서드입니다.  
  
 **geography** 인스턴스가 다른 **geography** 인스턴스와 잠재적으로 교차할 수 있는 경우 1을 반환합니다. 이 메서드는 거짓 긍정 결과를 반환할 수 있으며 정확한 결과는 계획에 따라 다릅니다. **geography** 인스턴스가 교차하지 않으면 정확한 0 값을 반환합니다(참 부정 반환).  
  
 인덱스를 사용할 수 없거나 사용하지 않는 경우 동일한 매개 변수로 호출되면 이 메서드에서 **STIntersects()** 와 동일한 값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.Filter ( other_geography )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *other_geography*  
 Filter()가 호출되는 인스턴스와 비교할 다른 **geography** 인스턴스입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **bit**  
  
 CLR 반환 형식: **SqlBoolean**  
  
## <a name="remarks"></a>설명  
 이 메서드는 비결정적이고 정확하지 않습니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `Filter()`를 사용하여 두 `geography` 인스턴스가 서로 교차하는지 확인합니다.  
  
```  
CREATE TABLE sample (id int primary key, g geography);  
INSERT INTO sample VALUES  
   (0, geography::Point(45, -120, 4326)),  
   (1, geography::Point(45, -120.1, 4326)),  
   (2, geography::Point(45, -120.2, 4326)),  
   (3, geography::Point(45, -120.3, 4326)),  
   (4, geography::Point(45, -120.4, 4326));  
  
CREATE SPATIAL INDEX sample_idx on sample(g);  
SELECT id  
FROM sample   
WHERE g.Filter(geography::Parse(  
   'POLYGON((-120.1 44.9, -119.9 44.9, -119.9 45.1, -120.1 45.1, -120.1 44.9))')) = 1;  
```  
  
## <a name="see-also"></a>참고 항목  
 [지리 인스턴스의 확장 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [STIntersects&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stintersects-geography-data-type.md)  
  
  
