---
title: STSymDifference(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- STSymDifference (geography Data Type)
- STSymDifference_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STSymDifference (geography Data Type)
ms.assetid: 82bbfa2c-a61b-4f41-9bf8-6f720f363bae
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4dc604d7e30288f71d5f84acce52aee8ee0c5c54
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36255025"
---
# <a name="stsymdifference-geography-data-type"></a>STSymDifference(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  특정 **geography** 인스턴스 또는 다른 **geography** 인스턴스에 있지만 두 인스턴스 모두에 있지는 않은 모든 점을 나타내는 개체를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STSymDifference ( other_geography )  
```  
  
## <a name="arguments"></a>인수  
 *other_geography*  
 STSymDistance()가 호출되는 인스턴스 외의 다른 **geography** 인스턴스입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 이 메서드는 **geography** 인스턴스의 SRID(satial reference identifier)가 일치하지 않으면 항상 Null을 반환합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 반구보다 큰 공간 인스턴스를 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 서버에서 얻을 수 있는 결과 집합이 **FullGlobe** 인스턴스까지 확장되었습니다.  
  
 입력 인스턴스에 원호 세그먼트가 있을 경우에만 결과에 원호 세그먼트가 포함될 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-computing-the-symmetric-difference-of-two-polygons"></a>1. 두 Polygon 사이의 대칭 차이 계산  
 다음 예에서는 `STSymDifference()`를 사용하여 두 `Polygon` 인스턴스의 대칭 차이를 계산합니다.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SET @h = geography::STGeomFromText('POLYGON((-122.351 47.656, -122.341 47.656, -122.341 47.661, -122.351 47.661, -122.351 47.656))', 4326);  
SELECT @g.STSymDifference(@h).ToString();  
```  
  
### <a name="b-computing-the-symmetric-difference-with-fullglobe"></a>2. FullGlobe와의 대칭 차이 계산  
 다음 예에서는 `Polygon`와 `FullGlobe`의 대칭 차이를 비교합니다.  
  
```
 DECLARE @g geography = 'POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.STSymDifference('FULLGLOBE').ToString();
 ```  
  
## <a name="see-also"></a>참고 항목  
 [지리 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
