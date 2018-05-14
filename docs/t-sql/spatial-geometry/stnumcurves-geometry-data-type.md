---
title: STNumCurves(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STNumCurves method (geometry)
ms.assetid: 20c2fa0b-656b-4519-b34c-cc8f094290d4
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: eec3bd116f3d8f3a5a6dd485cbd02c5de5201fe3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="stnumcurves-geometry-data-type"></a>STNumCurves(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

이 메서드는 인스턴스가 1차원 공간 데이터 형식일 때 **geometry** 인스턴스의 곡선 수를 반환합니다. 1차원 공간 데이터 형식에는 **LineString**, **CircularString** 및 **CompoundCurve**가 포함됩니다. `STNumCurves`()는 단순 형식에서만 작동하며 **MultiLineString**과 같은 **geometry** 컬렉션에서는 작동하지 않습니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.STNumCurves()  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geometry**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 빈 1차원 **geometry** 인스턴스는 0을 반환합니다. **geometry** 인스턴스가 1차원 인스턴스가 아니거나 초기화되지 않은 인스턴스일 경우 **NULL**이 반환됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-stnumcurves-on-a-circularstring-instance"></a>1. CircularString 인스턴스에 STNumCurves() 사용  
 다음 예에서는 `CircularString` 인스턴스의 곡선 수를 가져오는 방법을 보여 줍니다.  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::Parse('CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0)');  
 SELECT @g.STNumCurves();
 ```  
  
### <a name="b-using-stnumcurves-on-a-compoundcurve-instance"></a>2. CompoundCurve 인스턴스에 STNumCurves() 사용  
 다음 예에서는 `STNumCurves()`를 사용하여 `CompoundCurve` 인스턴스의 곡선 수를 반환합니다.  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0))');  
 SELECT @g.STNumCurves();
 ```  
  
## <a name="see-also"></a>참고 항목  
 [공간 데이터 형식 개요](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

