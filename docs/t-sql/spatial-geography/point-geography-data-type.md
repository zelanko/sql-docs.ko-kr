---
title: "진입점 (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Point
- Point_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Point method
- Point (geography Data Type)
ms.assetid: 0dc6f422-7aae-4016-b7f4-3289fa8f989c
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7cefb6e199bbd4617b1fc2f6f71d9bb3997445dc
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="point-geography-data-type"></a>Point(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

생성 된 **geography** 인스턴스를 나타내는 **지점** 해당 위도 및 경도 값 및 spatial reference ID (SRID)에서 인스턴스.
  
## <a name="syntax"></a>구문  
  
```  
  
Point ( Lat, Long, SRID )  
```  
  
## <a name="arguments"></a>인수  
 *Lat*  
 이 **float** 의 x 좌표를 나타내는 식은 **지점** 생성 되 고 합니다.  
  
 *긴*  
 이 **float** 의 y 좌표를 나타내는 식은 **지점** 생성 되 고 합니다. 유효한 위 도와 경도 값에 대 한 자세한 내용은 참조 하십시오. [지점](../../relational-databases/spatial/point.md)합니다.  
  
 *SRID*  
 이 **int** SRID를 나타내는 식은 **geography** 반환할 인스턴스.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
> [!NOTE]  
>  진입점(geography 데이터 형식) 메서드에 대한 인수의 좌표는 WKT에 비해 반전되었습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Point()`를 사용하여 `geography` 인스턴스를 만듭니다.  
  
```  
DECLARE @g geography;   
SET @g = geography::Point(47.65100, -122.34900, 4326)  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [확장 정적 지리 메서드](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  

