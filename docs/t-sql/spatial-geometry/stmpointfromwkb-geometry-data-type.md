---
title: "STMPointFromWKB (geometry 데이터 형식) | Microsoft Docs"
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
- STMPointFromWKB (geometry Data Type)
- STMPointFromWKB_TSQL
dev_langs: TSQL
helpviewer_keywords: STMPointFromWKB (geometry Data Type)
ms.assetid: 01d4117f-01a0-4bc3-8762-7382a1cdbd6c
caps.latest.revision: "17"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f1b303505c596892d183c33365e51cd0b7cfa85a
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="stmpointfromwkb-geometry-data-type"></a>STMPointFromWKB(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

반환 된 **geometryMultiPoint** Open Geospatial Consortium (OGC) wkb (WELL-KNOWN Binary) 표현의 인스턴스.
  
## <a name="syntax"></a>구문  
  
```  
  
STMPointFromWKB ( 'WKB_multipoint' , SRID )  
```  
  
## <a name="arguments"></a>인수  
 *WKB_multipoint*  
 WKB 표현에서 **geometryMultiPoint** 반환할 인스턴스. *WKB_multipoint* 는 **varbinary (max)** 식입니다.  
  
 *SRID*  
 이 **int** spatial 나타내는 식 참조의 ID (SRID)는 **geometryMultiPoint** 반환할 인스턴스.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **기 하 도형**  
  
 CLR 반환 형식: **SqlGeometry**  
  
 OGC 형식: **MultiPoint**  
  
## <a name="remarks"></a>주의  
 이 메서드는 throw 된 **FormatException** 입력이 잘못 된 경우.  
  
## <a name="examples"></a>예  
 다음 예에서는 `STMPointFromWKB()`를 사용하여 `geometry` 인스턴스를 만듭니다.  
  
```  
DECLARE @g geometry;   
SET @g = geometry::STMPointFromWKB(0x010400000002000000010100000000000000000059400000000000005940010100000000000000000069400000000000006940, 0);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [OGC 정적 기하 도형 메서드](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

