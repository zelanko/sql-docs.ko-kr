---
title: STLength(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STLength (geography Data Type)
- STLength_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STLength method
ms.assetid: 774560ab-4a4a-4058-b043-1e67cf6fb9eb
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 56a0c72b86e6dcb671b0f18197e7d0046cb2f36e
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65936745"
---
# <a name="stlength-geography-data-type"></a>STLength(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  **geography** 인스턴스 또는 **GeometryCollection** 내의 **geography** 인스턴스에 있는 요소의 총 길이를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STLength ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **float**  
  
 CLR 반환 형식: **SqlDouble**  
  
## <a name="remarks"></a>Remarks  
 **geography** 인스턴스가 닫힌 경우 해당 길이는 인스턴스의 총 둘레 길이로 계산됩니다. 즉, 모든 다각형의 길이는 해당 둘레의 길이이며 점의 길이는 0입니다. **GeometryCollection**의 길이는 컬렉션 내에 포함된 모든 **geography** 인스턴스의 길이 합계를 계산하여 구합니다.  
  
 STLength()는 유효한 LineString과 잘못된 LineString 둘 다에서 작동합니다. 일반적으로 LineString은 겹치는 세그먼트로 인해 유효하지 않으며, 이는 부정확한 GPS 추적 같은 잘못된 부분 때문에 발생할 수 있습니다. STLength()는 겹친 세그먼트나 잘못된 세그먼트를 제거하지 않습니다. STLength()는 반환하는 길이 값에 겹치는 세그먼트 및 잘못된 세그먼트를 포함합니다. MakeValid() 메서드는 LineString에서 겹치는 세그먼트를 제거할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `LineString` 인스턴스를 만들고 `STLength()`를 사용하여 인스턴스의 길이를 구합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STLength();  
```  
  
## <a name="see-also"></a>참고 항목  
 [지리 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
