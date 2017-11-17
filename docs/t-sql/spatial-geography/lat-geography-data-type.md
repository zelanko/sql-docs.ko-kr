---
title: "Lat (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
- Lat
- Lat_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Lat method
ms.assetid: 051d66bc-04de-4c58-861c-760dc5b859b5
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 313419e50b1ff142cd9d47bddd93b1c8bdce2835
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="lat-geography-data-type"></a>Lat(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  위도 속성은 **geography** 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```  
.Lat  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]형식: **float**  
  
 CLR 형식: **SqlDouble**  
  
## <a name="remarks"></a>주의  
 Lat의 경우에 정의 OpenGIS 모델에서는 **geography** 인스턴스는 단일 지점으로 구성 합니다. 이 속성은 NULL이 반환 하는 경우 **geography** 인스턴스는 둘 이상의 단일 지점이 포함 합니다. 이 속성은 정확하며 읽기 전용입니다.  
  
## <a name="examples"></a>예  
 이 예에서는 지점을 만들고 지점의 위도를 반환합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.Lat;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Geography 인스턴스의 확장된 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  

