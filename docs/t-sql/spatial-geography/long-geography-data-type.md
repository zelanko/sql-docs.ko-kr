---
description: Long(geography 데이터 형식)
title: Long(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Long_TSQL
- Long
dev_langs:
- TSQL
helpviewer_keywords:
- Long method
ms.assetid: bedbeced-70b8-4569-84f3-f86bfb04ce50
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 774ea7421e7616976bcedc1c848620accf8c07d7
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88467501"
---
# <a name="long-geography-data-type"></a>Long(geography 데이터 형식)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  **geography** 인스턴스의 경도 속성을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
.Long  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-value"></a>Return Value  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 형식: **float**  
  
 CLR 유형: **SqlDouble**  
  
## <a name="remarks"></a>설명  
 OpenGIS 모델에서는 하나의 점으로 구성된 **geography** 인스턴스에 대해서만 Long이 정의됩니다. **geography** 인스턴스에 둘 이상의 지점이 포함되어 있는 경우 이 속성은 NULL을 반환합니다. 이 속성은 정확하며 읽기 전용입니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 **Point** 인스턴스를 만들고 점의 경도를 검색합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.Long;  
```  
  
## <a name="see-also"></a>참고 항목  
 [지리 인스턴스의 확장 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
