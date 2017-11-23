---
title: "STMLineFromWKB (geometry 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STMLineFromWKB (geometry Data Type)
- STMLineFromWKB_TSQL
dev_langs: TSQL
helpviewer_keywords: STMLineFromWKB (geometry Data Type)
ms.assetid: 00a8a8e7-11d6-47a0-b971-00e60f7877ce
caps.latest.revision: "17"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3d8b283da368ca98b851180e150ee125890984f3
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="stmlinefromwkb-geometry-data-type"></a>STMLineFromWKB(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

반환 된 **geometryMultiLineString** Open Geospatial Consortium (OGC) wkb (WELL-KNOWN Binary) 표현의 인스턴스.
  
## <a name="syntax"></a>구문  
  
```  
  
STMLineFromWKB ( 'WKB_multilinestring' , SRID )  
```  
  
## <a name="arguments"></a>인수  
 *WKB_multilinestring*  
 WKB 표현입니다는 **geometryMultiLineString** 인스턴스를 반환 합니다. *WKB_multilinestring* 는 **varbinary (max)** 식입니다.  
  
 *SRID*  
 **int** spatial 나타내는 식 참조의 ID (SRID)는 **geometryMultiLineString** 인스턴스를 반환 합니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **기 하 도형**  
  
 CLR 반환 형식: **SqlGeometry**  
  
 OGC 형식: **MultiLineString**  
  
## <a name="remarks"></a>주의  
 이 메서드는 throw 된 **FormatException** 입력이 잘못 된 경우.  
  
## <a name="examples"></a>예  
 다음 예에서는 `STMLineFromWKB()`를 사용하여 `geometry` 인스턴스를 만듭니다.  
  
```  
DECLARE @g geometry;   
SET @g = geometry::STMLineFromWKB(0x0105000000020000000102000000020000000000000000005940000000000000594000000000000069400000000000006940010200000003000000000000000000084000000000000010400000000000001C40000000000000204000000000000024400000000000002440, 0);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [OGC 정적 기하 도형 메서드](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

