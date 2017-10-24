---
title: "STNumCurves (geometry 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STNumCurves method (geometry)
ms.assetid: 20c2fa0b-656b-4519-b34c-cc8f094290d4
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 718289c6785bec8f9bba15ccec76507ac2501f47
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stnumcurves-geometry-data-type"></a>STNumCurves(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

이 메서드가 반환 있는 곡선 개수는 **기 하 도형** 인스턴스가 1 차원 공간 데이터 형식에 있으면 인스턴스. 1 차원 공간 데이터 형식에는 **LineString**, **CircularString**, 및 **CompoundCurve**합니다. `STNumCurves`(); 단순 형식 에서만 작동 작동 하지 않습니다 **geometry** 컬렉션 같은 **MultiLineString**합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.STNumCurves()  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **기 하 도형**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="remarks"></a>주의  
 빈 1 차원 **geometry** 인스턴스 0을 반환 합니다. **NULL** 때 반환 되는 **기 하 도형** 인스턴스가 1 차원 인스턴스가 아니거나 초기화 되지 않은 인스턴스.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [공간 데이터 형식 개요](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [Geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


