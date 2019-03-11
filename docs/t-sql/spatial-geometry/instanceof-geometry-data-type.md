---
title: InstanceOf(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- InstanceOf
- InstanceOf_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- InstanceOf (geometry Data Type)
ms.assetid: fdea1248-29a4-4bab-a60d-a1b359b5e109
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d093331425443a0879d5f59f5a2d03fdebcb2abd
ms.sourcegitcommit: ad3b2133585bc14fc6ef8be91f8b74ee2f498b64
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/20/2019
ms.locfileid: "56425758"
---
# <a name="instanceof-geometry-data-type"></a>InstanceOf(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

**geometry** 인스턴스가 지정된 형식과 동일한 경우 테스트하는 메서드입니다. **geometry** 인스턴스의 형식이 지정된 형식과 동일한 경우 1을 반환합니다. 또한 이 메서드는 지정된 형식이 인스턴스 형식의 상위 항목이면 1을 반환합니다. 그렇지 않으면 이 메서드는 0을 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.InstanceOf (geometry_type )  
```  
  
## <a name="arguments"></a>인수  
*geometry_type*  
**geometry** 형식 계층 구조에 노출되는 15개 형식 중 하나를 지정하는 **nvarchar(4000)** 문자열입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **bit**  
  
 CLR 반환 형식: **SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 메서드의 입력은 **Geometry**, **Point**, **Curve**, **LineString**, **CircularString**, **CompoundCurve**, **Surface**, **Polygon**, **CurvePolygon**, **GeometryCollection**, **MultiSurface**, **MultiPolygon**, **MultiCurve**, **MultiLineString** 및 **MultiPoint** 형식 중 하나여야 합니다. 이 메서드는 다른 문자열이 입력에 사용되면 **ArgumentException**을 throw합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `MultiPoint` 인스턴스를 만들고 `InstanceOf()`를 사용하여 인스턴스가 `GeometryCollection`인지 확인합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('MULTIPOINT(0 0, 13.5 2, 7 19)', 0);  
SELECT @g.InstanceOf('GEOMETRYCOLLECTION');  
```  
  
## <a name="see-also"></a>참고 항목  
 [geometry 인스턴스의 확장 메서드](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

