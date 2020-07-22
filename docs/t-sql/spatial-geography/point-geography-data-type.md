---
title: Point(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 10/10/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 04db3c6617669010f63e173415de0ebf6b7a3dca
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86556167"
---
# <a name="point-geography-data-type"></a>Point(geography 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

해당 위도 및 경도 값과 SRID(Spatial Reference ID)로부터 **Point** 인스턴스를 나타내는 **geography** 인스턴스를 생성합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
Point ( Lat, Long, SRID )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *Lat*  
 생성할 **Point**의 y 좌표를 나타내는 **float** 식입니다.  
  
 *Long*  
 생성할 **Point**의 x 좌표를 나타내는 **float** 식입니다. 유효한 위도와 경도 값에 대한 자세한 내용은 [Point](../../relational-databases/spatial/point.md)를 참조하세요.  
  
 *SRID*  
 반환할 **geography** 인스턴스의 [SRID(Spatial Reference Identifier)](https://docs.microsoft.com/sql/relational-databases/spatial/spatial-reference-identifiers-srids)를 나타내는 **int** 식입니다.  
  
> [!NOTE]  
>  진입점(geography 데이터 형식) 메서드에 대한 인수의 좌표는 WKT에 비해 반전되었습니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="examples"></a>예  
 다음 예에서는 `Point()`를 사용하여 `geography` 인스턴스를 만듭니다.  
  
```  
DECLARE @g geography;   
SET @g = geography::Point(47.65100, -122.34900, 4326)  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>참고 항목  
 [확장 정적 지리 메서드](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
