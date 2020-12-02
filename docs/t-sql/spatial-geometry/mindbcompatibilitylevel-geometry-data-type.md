---
description: MinDbCompatibilityLevel(geometry 데이터 형식)
title: MinDbCompatibilityLevel(geometry 데이터 형식) | Microsoft Docs
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
- MinDbCompatibilityLevel method (geometry)
ms.assetid: c848b974-8ccb-4c5c-a7eb-b019a9538d99
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 0136c2f53b70b6180bb380d72e1c9e4d70351ffb
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88427055"
---
# <a name="mindbcompatibilitylevel-geometry-data-type"></a>MinDbCompatibilityLevel(geometry 데이터 형식)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

**geometry** 데이터 형식 인스턴스를 인식하는 최소 데이터베이스 호환성 수준을 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.MinDbCompatibilityLevel ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **int**  
  
 CLR 반환 형식: **int**  
  
## <a name="remarks"></a>설명  
 데이터베이스의 호환성 수준을 변경하기 전에 `MinDbCompatibilityLevel()`을 사용하여 공간 개체의 호환성을 테스트할 수 있습니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-testing-circularstring-type-for-compatibility-with-compatibility-level-110"></a>A. 호환성 수준 110으로 CircularString 형식의 호환성 테스트  
 다음 예에서는 `CircularString` 인스턴스에 대해 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전과의 호환성을 테스트합니다.  
  
```
 DECLARE @g geometry = 'CIRCULARSTRING(3 4, 8 9, 5 6)'; 
 IF @g.MinDbCompatibilityLevel() <= 110 
 BEGIN 
 SELECT @g.ToString(); 
 END
 ```  
  
### <a name="b-testing-linestring-type-for-compatibility-with-compatibility-level-100"></a>B. 호환성 수준 100으로 LineString 형식의 호환성 테스트  
 다음 예에서는 `LineString` 인스턴스에 대해 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]과의 호환성을 테스트합니다.  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 9, 5 6)'; 
 IF @g.MinDbCompatibilityLevel() <= 100 
 BEGIN 
 SELECT @g.ToString(); 
 END
``` 
  
## <a name="see-also"></a>참고 항목  
 [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
  
  

