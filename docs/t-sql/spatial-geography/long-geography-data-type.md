---
title: "Long (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Long_TSQL
- Long
dev_langs: TSQL
helpviewer_keywords: Long method
ms.assetid: bedbeced-70b8-4569-84f3-f86bfb04ce50
caps.latest.revision: "14"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d88f9cdf318296b48a47efdd6b9e9b13c1ac2e43
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="long-geography-data-type"></a>Long(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  경도 속성은 **geography** 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```  
  
.Long  
```  
  
## <a name="return-value"></a>반환 값  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]형식: **float**  
  
 CLR 형식: **SqlDouble**  
  
## <a name="remarks"></a>주의  
 OpenGIS 모델에서 장기 정의 경우에 **geography** 인스턴스는 단일 지점으로 구성 합니다. 이 속성은 NULL이 반환 하는 경우 **geography** 인스턴스는 둘 이상의 단일 지점이 포함 합니다. 이 속성은 정확하며 읽기 전용입니다.  
  
## <a name="examples"></a>예  
 이 예제에서는 만듭니다는 **가리킨** 인스턴스 하 고 점의 경도 검색 합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.Long;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [지리 인스턴스의 확장 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
