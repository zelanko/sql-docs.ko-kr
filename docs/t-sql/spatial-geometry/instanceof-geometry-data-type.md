---
title: "InstanceOf (geometry 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
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
- InstanceOf
- InstanceOf_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- InstanceOf (geometry Data Type)
ms.assetid: fdea1248-29a4-4bab-a60d-a1b359b5e109
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a7106339cc346cbd49b3cbfc3905ea3a2a941c15
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="instanceof-geometry-data-type"></a>InstanceOf(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

테스트 하는 메서드는 **기 하 도형** 인스턴스는 지정 된 형식과 동일 합니다. 1을 반환 형식의 **기 하 도형** 인스턴스는 지정된 된 형식으로 동일 또는 지정된 된 형식의 인스턴스 유형의 상위 항목이 면 그렇지 않으면 0을 반환 합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.InstanceOf (geometry_type )  
```  
  
## <a name="arguments"></a>인수  
 *geometry_type*  
 이 **nvarchar (4000)** 에 노출 되는 15 유형 중 하나를 지정 하는 문자열의 **기 하 도형** 형식 계층 구조입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **비트**  
  
 CLR 반환 형식: **SqlBoolean**  
  
## <a name="remarks"></a>주의  
 메서드에 대 한 입력은 다음 중 하나 여야 합니다: **Geometry**, **지점**, **곡선**, **LineString**,  **CircularString**, **CompoundCurve**, **화면**, **다각형**, **CurvePolygon**, **GeometryCollection**, **MultiSurface**, **MultiPolygon**, **MultiCurve**, **MultiLineString**, 및 **MultiPoint**합니다. 이 메서드에서 throw 된 **ArgumentException** 이면 다른 모든 문자열 입력에 사용 됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `MultiPoint` 인스턴스를 만들고 `InstanceOf()`를 사용하여 인스턴스가 `GeometryCollection`인지 확인합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('MULTIPOINT(0 0, 13.5 2, 7 19)', 0);  
SELECT @g.InstanceOf('GEOMETRYCOLLECTION');  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Geometry 인스턴스의 확장된 메서드](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  


