---
description: STIsClosed(geography 데이터 형식)
title: STIsClosed(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIsClosed (geography Data Type)
- STIsClosed_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STIsClosed method
ms.assetid: eba1643f-07c4-4500-8643-b7e90f908147
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 8c6643b37d421a5283cd8d44e3fadaf73ae69eab
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88445222"
---
# <a name="stisclosed-geography-data-type"></a>STIsClosed(geography 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  주어진 **geography** 인스턴스의 시작점 및 끝점이 동일하면 1을 반환합니다. 포함된 각 **geography** 인스턴스가 닫혀 있으면 **geography** 컬렉션 형식에 대해 1을 반환합니다. 인스턴스가 닫혀 있지 않으면 0을 반환합니다.  
  
 이 **geography** 데이터 형식 메서드는 **FullGlobe** 인스턴스 또는 반구보다 큰 공간 인스턴스를 지원합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STIsClosed ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **bit**  
  
 CLR 반환 형식: **SqlBoolean**  
  
## <a name="remarks"></a>설명  
 이 메서드는 **geography** 인스턴스의 도형이 점이거나 인스턴스가 비어 있으면 0을 반환합니다.  
  
 이 메서드는 **FullGlobe** 인스턴스가 또는 **Polygon** 또는 다른 유형의 인스턴스인 경우 True를 반환합니다.  
  
 모든 **Polygon** 인스턴스는 닫혀 있다고 간주됩니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `Polygon` 인스턴스를 만들고 `STIsClosed()`를 사용하여 `Polygon`이 닫혀 있는지 테스트합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SELECT @g.STIsClosed();  
```  
  
## <a name="see-also"></a>참고 항목  
 [Geography 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
