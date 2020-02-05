---
title: STNumCurves(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STNumCurves
- STNumCurves_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STNumCurves method (geography)
ms.assetid: e98a56c2-8496-4dfd-9b37-7f3c4ca9b2b5
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: f7a525dedd8f5cbfbf881da63b7bb40f461bc802
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68120927"
---
# <a name="stnumcurves-geography-data-type"></a>STNumCurves(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  1차원 **geography** 인스턴스의 곡선 수를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STNumCurves()  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="remarks"></a>설명  
 1차원 공간 데이터 형식에는 **LineString**, **CircularString** 및 **CompoundCurve**가 포함됩니다. 빈 1차원 **geography** 인스턴스는 0을 반환합니다.  
  
 `STNumCurves`()는 단순 형식에서만 작동하며 **MultiLineString**과 같은 **geography** 컬렉션에서는 작동하지 않습니다. **geography** 인스턴스가 1차원 데이터 형식이 아닌 경우에는 **NULL**이 반환됩니다.  
  
 초기화되지 않은 **geography** 인스턴스에 대해서는 **Null**이 반환됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-stnumcurves-on-a-circularstring-instance"></a>A. CircularString 인스턴스에 STNumCurves() 사용  
 다음 예에서는 `CircularString` 인스턴스의 곡선 수를 가져오는 방법을 보여 줍니다.  
  
```
 DECLARE @g geography; 
 SET @g = geography::Parse('CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)');  
 SELECT @g.STNumCurves();
 ```  
  
### <a name="b-using-stnumcurves-on-a-compoundcurve-instance"></a>B. CompoundCurve 인스턴스에 STNumCurves() 사용  
 다음 예에서는 `STNumCurves()`를 사용하여 `CompoundCurve` 인스턴스의 곡선 수를 반환합니다.  
  
```
 DECLARE @g geography;  
 SET @g = geography::Parse('COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))');  
 SELECT @g.STNumCurves();
 ```  
  
## <a name="see-also"></a>참고 항목  
 [공간 데이터 형식 개요](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [지리 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
