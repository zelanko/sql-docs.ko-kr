---
title: "STGeomFromText (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 07/30/2017
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
- STGeomFromText (geography Data Type)
- STGeomFromText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full globe
- STGeomFromText method
ms.assetid: 3717987b-77d8-4ccf-a1db-5a8016ac1083
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bdd52d6a9dc928d47db871ec9a84648797e64fe8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stgeomfromtext-geography-data-type"></a>STGeomFromText(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

반환 된 **geography** Z (높이) 값 및 M (측정값) 값을 따르도록 Open Geospatial Consortium (OGC) wkt (WELL-KNOWN Text) 표현의 인스턴스는 인스턴스에서 얻어진 합니다.
  
이 **geography** 데이터 형식 메서드 지원 **FullGlobe** 인스턴스 또는 반구 보다 큰 공간 인스턴스.
  
## <a name="syntax"></a>구문  
  
```  
  
STGeomFromText ( 'geography_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>인수  
 *geography_tagged_text*  
 WKT 표현입니다는 **geography** 인스턴스를 반환 합니다. *geography_tagged_text* 는 **nvarchar (max)** 식입니다.  
  
 *SRID*  
 **int** spatial 나타내는 식 참조의 ID (SRID)는 **geography** 인스턴스를 반환 합니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="remarks"></a>주의  
 OGC 형식은 **geography** 인스턴스 STGeomFromText()에서 반환 된 해당 WKT 입력로 설정 됩니다.  
  
 이 메서드는 throw 된 **ArgumentException** 입력에 대척점 가장자리를 포함 하는 경우.  
  
## <a name="examples"></a>예  
 다음 예에서는 `STGeomFromText()`를 사용하여 `geography` 인스턴스를 만듭니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [OGC 정적 지리 메서드](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  

