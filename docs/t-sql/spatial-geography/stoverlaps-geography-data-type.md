---
title: "STOverlaps (geography 데이터 형식) | Microsoft Docs"
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
dev_langs:
- TSQL
helpviewer_keywords:
- STOverlaps method (geography)
ms.assetid: 2babbb9c-59ef-4494-9e6b-528cf296cbd7
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1a70088ef45b2cf8f5682e3779f5a9011d502c61
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="stoverlaps-geography-data-type"></a>STOverlaps(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  1을 반환는 **geography** 공간적으로 겹치면 다른 **geography** 인스턴스 또는 그렇지 않은 경우 0입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STOverlaps ( other_geography )  
```  
  
## <a name="arguments"></a>인수  
 *other_geography*  
 다른 **geography** 인스턴스와 비교할 인스턴스 `STOverlaps()` 가 호출 됩니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **비트**  
  
 CLR 반환 형식: **SqlBoolean**  
  
## <a name="remarks"></a>주의  
 항상 null이 반환 하는 경우의 spatial reference Id (Srid)는 **geography** 인스턴스 일치 하지 않습니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 `STOverlaps()` 두 테스트에 **geography** 겹쳐진 부분에 대 한 인스턴스.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::Parse('POLYGON ((-120.533 46.566, -118.283 46.1, -122.3 47.45, -120.533 46.566))');  
SET @h = geography::Parse('CURVEPOLYGON (COMPOUNDCURVE (CIRCULARSTRING (-122.200928 47.454094, -122.810669 47.00648, -122.942505 46.687131, -121.14624 45.786679, -119.119263 46.183634), (-119.119263 46.183634, -119.273071 47.107523), CIRCULARSTRING (-119.273071 47.107523, -120.640869 47.569114, -122.200928 47.454094)))');  
SELECT @g.STOverlaps(@h);  
```  
  
  
