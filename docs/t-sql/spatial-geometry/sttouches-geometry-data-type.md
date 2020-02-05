---
title: STTouches(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STTouches (geometry Data Type)
- STTouches_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STTouches (geometry Data Type)
ms.assetid: af3650b4-26da-4600-9cc2-1be71dd76a14
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 93ea5be3c2f9a4ecdd415471da16ca21eb1f08c9
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68066240"
---
# <a name="sttouches-geometry-data-type"></a>STTouches(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

**geometry** 인스턴스가 다른 **geometry** 인스턴스와 공간적으로 만나면 1을 반환합니다. 그렇지 않으면 0을 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.STTouches ( other_geometry )  
```  
  
## <a name="arguments"></a>인수  
 *other_geometry*  
 **를 호출할 인스턴스와 비교할 다른** geometry`STTouches()` 인스턴스입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **bit**  
  
 CLR 반환 형식: **SqlBoolean**  
  
## <a name="remarks"></a>설명  
 두 **geometry** 인스턴스의 점 집합이 교차하지만 내부는 교차되지 않는 경우 두 인스턴스가 만나게 됩니다.  
  
 이 메서드는 **geometry** 인스턴스의 SRID(spatial Reference ID)가 일치하지 않으면 항상 Null을 반환합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `STTouches()`를 사용하여 두 `geometry` 인스턴스가 만나는지 테스트합니다.  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0, 4 2)', 0);  
SET @h = geometry::STGeomFromText('POINT(1 1)', 0);  
SELECT @g.STTouches(@h);  
```  
  
## <a name="see-also"></a>참고 항목  
 [공간 인덱스 개요](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

