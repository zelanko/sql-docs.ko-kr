---
title: "Point(geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 07/30/2017
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
- Point
- Point_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Point method
- Point (geography Data Type)
ms.assetid: 0dc6f422-7aae-4016-b7f4-3289fa8f989c
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f37072d64159d5d8bfb1d44a64dd017adf0fceed
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="point-geography-data-type"></a>Point(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

해당 위도 및 경도 값과 SRID(Spatial Reference ID)로부터 **Point** 인스턴스를 나타내는 **geography** 인스턴스를 생성합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
Point ( Lat, Long, SRID )  
```  
  
## <a name="arguments"></a>인수  
 *Lat*  
 생성할 **Point**의 x 좌표를 나타내는 **float** 식입니다.  
  
 *Long*  
 생성할 **Point**의 y 좌표를 나타내는 **float** 식입니다. 유효한 위도와 경도 값에 대한 자세한 내용은 [Point](../../relational-databases/spatial/point.md)를 참조하세요.  
  
 *SRID*  
 반환하려는 **geography** 인스턴스의 SRID를 나타내는 **int** 식입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
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
  
## <a name="see-also"></a>참고 항목  
 [확장 정적 지리 메서드](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  
