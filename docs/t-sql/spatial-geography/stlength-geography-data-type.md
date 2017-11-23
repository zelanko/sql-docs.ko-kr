---
title: "STLength (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
- STLength (geography Data Type)
- STLength_TSQL
dev_langs: TSQL
helpviewer_keywords: STLength method
ms.assetid: 774560ab-4a4a-4058-b043-1e67cf6fb9eb
caps.latest.revision: "12"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fa8b74ee4f1eec0b9bfb6f85dad0d8c335e15909
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="stlength-geography-data-type"></a>STLength(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  에 있는 요소의 총 길이 반환는 **geography** 인스턴스 또는 **geography** 인스턴스에 **GeometryCollection**합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STLength ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **float**  
  
 CLR 반환 형식: **SqlDouble**  
  
## <a name="remarks"></a>주의  
 경우는 **geography** 인스턴스가 닫혀, 길이가 인스턴스 주위 총 길이로 계산 됩니다; 모든 다각형의 길이 해당 둘레 및 점의 길이 0입니다. 길이 **GeometryCollection** 모든의 길이의 합을 계산 하 여 발견 되는 **geography** 컬렉션 내에 포함 된 인스턴스.  
  
 STLength()는 유효한 LineString과 잘못된 LineString 둘 다에서 작동합니다. 일반적으로 LineString은 겹치는 세그먼트로 인해 유효하지 않으며, 이는 부정확한 GPS 추적 같은 잘못된 부분 때문에 발생할 수 있습니다. STLength()는 겹친 세그먼트나 잘못된 세그먼트를 제거하지 않습니다. STLength()는 반환하는 길이 값에 겹치는 세그먼트 및 잘못된 세그먼트를 포함합니다. MakeValid() 메서드는 LineString에서 겹치는 세그먼트를 제거할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `LineString` 인스턴스를 만들고 `STLength()`를 사용하여 인스턴스의 길이를 구합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STLength();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [지리 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
