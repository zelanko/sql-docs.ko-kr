---
title: NumRings(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- NumRings_TSQL
- NumRings
dev_langs:
- TSQL
helpviewer_keywords:
- NumRings method
ms.assetid: 0e4e4fa2-b608-4cc4-98ba-0845ddb4214c
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 0b85a8842a7bc33753394c5de96582ca41b9d635
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552501"
---
# <a name="numrings-geography-data-type"></a>NumRings(geography 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  **Polygon** 인스턴스에 있는 링의 총 개수를 반환합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **geography** 형식에서는 모든 링을 외부 링으로 사용할 수 있으므로 외부 링과 내부 링이 구분되지 않습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.NumRings ()  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-type"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **int**  
  
 CLR 반환 형식: **SqlInt32**  
  
## <a name="remarks"></a>설명  
 이 메서드는 인스턴스가 **Polygon** 인스턴스가 아니면 NULL을 반환하고 인스턴스가 비어 있으면 0을 반환합니다. 이 메서드는 정확합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 두 개의 링이 있는 `Polygon` 인스턴스를 만들고 링이 두 개인지 확인합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653), (-122.357 47.654, -122.357 47.657, -122.349 47.657, -122.349 47.650, -122.357 47.654))', 4326);  
SELECT @g.NumRings();  
```  
  
## <a name="see-also"></a>참고 항목  
 [지리 인스턴스의 확장 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
