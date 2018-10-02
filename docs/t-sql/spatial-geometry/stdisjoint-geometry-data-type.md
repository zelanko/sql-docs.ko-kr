---
title: STDisjoint(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STDisjoint_TSQL
- STDisjoint (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STDisjoint (geometry Data Type)
ms.assetid: 90acdb21-e826-4d81-afe8-45a71f33282a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c93cc745315885e560f5ff1bee654ef721898ea9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47620441"
---
# <a name="stdisjoint-geometry-data-type"></a>STDisjoint(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  **geometry** 인스턴스가 다른 **geometry** 인스턴스와 공간적으로 분리되어 있으면 1을 반환합니다. 그렇지 않으면 0을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STDisjoint ( other_geometry )  
```  
  
## <a name="arguments"></a>인수  
 *other_geometry*  
 `STDisjoint()`를 호출할 인스턴스와 비교할 다른 **geometry** 인스턴스입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **bit**  
  
 CLR 반환 형식: **SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 두 **geometry** 인스턴스의 점 집합에 대한 교차점이 비어 있으면 두 인스턴스가 분리된 것입니다.  
  
 이 메서드는 **geometry** 인스턴스의 SRID(spatial Reference ID)가 일치하지 않으면 항상 Null을 반환합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `STDisjoint()`를 사용하여 두 **geometry** 인스턴스가 공간적으로 분리되어 있는지 테스트합니다.  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0, 4 2)', 0);  
SET @h = geometry::STGeomFromText('POINT(1 1)', 0);  
SELECT @g.STDisjoint(@h);  
```  
  
## <a name="see-also"></a>참고 항목  
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
