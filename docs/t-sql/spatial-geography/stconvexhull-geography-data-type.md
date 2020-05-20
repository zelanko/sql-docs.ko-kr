---
title: STConvexHull(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STConvexHull method (geography)
ms.assetid: fb435db7-31bb-4243-9d8b-35379184cfb4
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: b3d06da6d6f972c64d4bf196699b55a611b0f992
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68042474"
---
# <a name="stconvexhull-geography-data-type"></a>STConvexHull(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **geography** 인스턴스의 볼록 집합(convex hull)을 나타내는 개체를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STConvexHull ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="remarks"></a>설명  
 봉투 각도가 90보다 큰 **geography** 인스턴스에 대해 `FullGlobe` 개체를 반환합니다.  
  
 빈 **geography** 인스턴스에 대해 빈 **geography** 컬렉션을 반환합니다.  
  
 초기화되지 않은 **geography** 인스턴스에 대해 **null**을 반환합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-stconvexhull-on-an-uninitialized-geography-instance"></a>A. 초기화되지 않은 인스턴스에 STConvexHull() 사용  
 다음 예에서는 초기화되지 않은 **geography** 인스턴스에 `STConvexHull()`을 사용합니다.  
  
```
 DECLARE @g geography;  
 SELECT @g.STConvexHull();
 ```  
  
### <a name="b-using-stconvexhull-on-an-empty-geography-instance"></a>B. 빈 geography 인스턴스에 STConvexHull 사용  
 다음 예에서는 빈 `STConvexHull()` 인스턴스에 `Polygon`을 사용합니다.  
  
```
 DECLARE @g geography = 'POLYGON EMPTY';  
 SELECT @g.STConvexHull().ToString();
 ```  
  
### <a name="c-finding-the-convex-hull-of-a-non-convex-polygon-instance"></a>C. 비볼록 Polygon 인스턴스의 볼록 집합 찾기  
 다음 예에서는 `STConvexHull()`을 사용하여 비볼록 `Polygon` 인스턴스의 볼록 집합을 찾습니다.  
  
```  
 DECLARE @g geography;  
 SET @g = geography::Parse('POLYGON((-120.533 46.566, -118.283 46.1, -122.3 47.45, -120.533 46.566))');  
 SELECT @g.STConvexHull().ToString();  
```  
  
### <a name="d-finding-the-convex-hull-on-a-geography-instance-with-an-envelope-angle-larger-than-90-degrees"></a>D. 봉투 각도가 90보다 큰 geography 인스턴스에서 볼록 집합 찾기  
 다음 예에서는 봉투 각도가 90도보다 큰 **geography** 인스턴스에 `STConvexHull()`을 사용합니다.  
  
```
 DECLARE @g geography = 'POLYGON((20.533 46.566, -18.283 46.1, -22.3 47.45, 20.533 46.566))';  
 SELECT @g.STConvexHull().ToString();
 ```  
  
  
