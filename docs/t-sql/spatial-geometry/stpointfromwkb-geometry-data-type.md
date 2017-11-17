---
title: "STPointFromWKB (geometry 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
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
- STPointFromWKB (geometry Data Type)
- STPointFromWKB_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STPointFromWKB (geometry Data Type)
ms.assetid: 1157c172-2dc7-4393-bae6-b85406171a34
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e32527bb0878f21ae255d72ba715024fd05c031d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stpointfromwkb-geometry-data-type"></a>STPointFromWKB(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

반환 된 **geometryPoint** Open Geospatial Consortium (OGC) wkb (WELL-KNOWN Binary) 표현의 인스턴스.
  
## <a name="syntax"></a>구문  
  
```  
  
STPointFromWKB ( 'WKB_point' , SRID )  
```  
  
## <a name="arguments"></a>인수  
 *WKB_point*  
 WKB 표현에서 **geometryPoint** 반환할 인스턴스. *WKB_point* 는 **varbinary (max)** 식입니다.  
  
 *SRID*  
 이 **int** spatial 나타내는 식 참조의 ID (SRID)는 **geometryPoint** 반환할 인스턴스.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **기 하 도형**  
  
 CLR 반환 형식: **SqlGeometry**  
  
 OGC 형식: **지점**  
  
## <a name="remarks"></a>주의  
 이 메서드는 throw 된 **FormatException** 입력이 잘못 된 경우.  
  
## <a name="examples"></a>예  
 다음 예에서는 `STPointFromWKB()`를 사용하여 `geometry` 인스턴스를 만듭니다.  
  
```  
DECLARE @g geometry;   
SET @g = geometry::STPointFromWKB(0x010100000000000000000059400000000000005940, 0);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [OGC 정적 기 하 도형 메서드](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  


