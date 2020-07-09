---
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
ms.openlocfilehash: dd2424bff6322ad388ef6980c0055b098433cf40
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85731126"
---
# <a name="long-geography-data-type"></a>Long(geography 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  **geography** 인스턴스의 경도 속성을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.Long  
```  
  
## <a name="return-value"></a>Return Value  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 형식: **float**  
  
 CLR 형식: **SqlDouble**  
  
## <a name="remarks"></a>설명  
 OpenGIS 모델에서는 하나의 점으로 구성된 **geography** 인스턴스에 대해서만 Long이 정의됩니다. **geography** 인스턴스에 둘 이상의 지점이 포함되어 있는 경우 이 속성은 NULL을 반환합니다. 이 속성은 정확하며 읽기 전용입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 **Point** 인스턴스를 만들고 점의 경도를 검색합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.Long;  
```  
  
## <a name="see-also"></a>참고 항목  
 [지리 인스턴스의 확장 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
