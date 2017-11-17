---
title: "STNumCurves (geography 데이터 형식) | Microsoft Docs"
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
- STNumCurves
- STNumCurves_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STNumCurves method (geography)
ms.assetid: e98a56c2-8496-4dfd-9b37-7f3c4ca9b2b5
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c92c6dec90faf08d69ed49de506ba8c4371141ba
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stnumcurves-geography-data-type"></a>STNumCurves(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  1 차원 곡선 수를 반환 합니다. **geography** 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STNumCurves()  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="remarks"></a>주의  
 1 차원 공간 데이터 형식에는 **LineString**, **CircularString**, 및 **CompoundCurve**합니다. 빈 1 차원 **geography** 인스턴스 0을 반환 합니다.  
  
 `STNumCurves`(); 단순 형식 에서만 작동 작동 하지 않습니다 **geography** 컬렉션 같은 **MultiLineString**합니다. **NULL** 이 반환 됩니다는 **geography** 인스턴스가 1 차원 데이터 형식이 아닙니다.  
  
 **Null** 초기화 되지 않은 코드가 반환 됩니다 **geography** 인스턴스.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-stnumcurves-on-a-circularstring-instance"></a>1. CircularString 인스턴스에 STNumCurves() 사용  
 다음 예에서는 `CircularString` 인스턴스의 곡선 수를 가져오는 방법을 보여 줍니다.  
  
```
 DECLARE @g geography; 
 SET @g = geography::Parse('CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)');  
 SELECT @g.STNumCurves();
 ```  
  
### <a name="b-using-stnumcurves-on-a-compoundcurve-instance"></a>2. CompoundCurve 인스턴스에 STNumCurves() 사용  
 다음 예에서는 `STNumCurves()`를 사용하여 `CompoundCurve` 인스턴스의 곡선 수를 반환합니다.  
  
```
 DECLARE @g geography;  
 SET @g = geography::Parse('COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))');  
 SELECT @g.STNumCurves();
 ```  
  
## <a name="see-also"></a>관련 항목:  
 [공간 데이터 형식 개요](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [Geography 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  

