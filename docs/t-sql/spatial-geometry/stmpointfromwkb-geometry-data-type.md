---
title: STMPointFromWKB(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STMPointFromWKB (geometry Data Type)
- STMPointFromWKB_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STMPointFromWKB (geometry Data Type)
ms.assetid: 01d4117f-01a0-4bc3-8762-7382a1cdbd6c
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 86f995fc650460bdbda6004917c974377cd1b2f3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67894866"
---
# <a name="stmpointfromwkb-geometry-data-type"></a>STMPointFromWKB(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

OGC(Open Geospatial Consortium) WKB(Well-Known Binary) 표현에서 **geometryMultiPoint** 인스턴스를 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
STMPointFromWKB ( 'WKB_multipoint' , SRID )  
```  
  
## <a name="arguments"></a>인수  
 *WKB_multipoint*  
 반환하려는 **geometryMultiPoint** 인스턴스의 WKB 표현입니다. *WKB_multipoint*은 **varbinary(max)** 식입니다.  
  
 *SRID*  
 반환하려는 **geometryMultiPoint** 인스턴스의 SRID(Spatial Reference ID)를 나타내는 **int** 식입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geometry**  
  
 CLR 반환 형식: **SqlGeometry**  
  
 OGC 형식: **MultiPoint**  
  
## <a name="remarks"></a>Remarks  
 이 메서드는 입력이 잘못된 경우 **FormatException**을 throw합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `STMPointFromWKB()`를 사용하여 `geometry` 인스턴스를 만듭니다.  
  
```  
DECLARE @g geometry;   
SET @g = geometry::STMPointFromWKB(0x010400000002000000010100000000000000000059400000000000005940010100000000000000000069400000000000006940, 0);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>참고 항목  
 [OGC 정적 기하 도형 메서드](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

