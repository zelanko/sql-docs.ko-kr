---
title: "AsTextZM (geography 데이터 형식) | Microsoft Docs"
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
f1_keywords:
- AsTextZM (geography Data Type)
- AsTextZM_TSQL
- AsTextZM
- AsTextZM_(geography_Data_Type)_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- AsTextZM method
ms.assetid: e9dc27f6-e945-4457-8498-7644db34008e
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ba824c4482f49d534d11666054a0a8d3a1669d2d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="astextzm-geography-data-type"></a>AsTextZM(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Open Geospatial Consortium (OGC) wkt (WELL-KNOWN Text) 표현을 반환는 **geography** 인스턴스 사용 하 여 보강 된 **Z** (높이) 및 **M** (측정값) 인스턴스에서 얻어진 값입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.AsTextZM ()  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **nvarchar (max)**  
  
 CLR 반환 형식: **SqlChars**  
  
## <a name="remarks"></a>주의  
  
## <a name="examples"></a>예  
 다음 예제에서는 한 `Point` 포함 된 인스턴스 **Z** (높이) 및 **M** (측정값) 값입니다. `STAsText()`선택 하는 WKT 값인 (-122.34900 47.65100); `AsTextZM()` 동일한 WKT 값을 선택 하 고에 대 한 값도 반환 **Z** 및 **M**122.34900 (-122.34900 47.65100 10.3 12).  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100 10.3 12)', 4326);  
SELECT @g.STAsText();  
SELECT @g.AsTextZM();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Geography 인스턴스의 확장된 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [M &#40; geography 데이터 형식 &#41;](../../t-sql/spatial-geography/m-geography-data-type.md)   
 [Z &#40; geography 데이터 형식 &#41;](../../t-sql/spatial-geography/z-geography-data-type.md)  
  
  

