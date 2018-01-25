---
title: "AsTextZM (geometry 데이터 형식) | Microsoft Docs"
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
- AsTextZM_TSQL
- AsTextZM
- AsTextZM (geometry Data Type)
- AsTextZM_(geometry_Data_Type)_TSQL
dev_langs: TSQL
helpviewer_keywords: AsTextZM (geometry Data Type)
ms.assetid: 08ac8aa0-aff7-4b22-87e0-1a1d55dcbc04
caps.latest.revision: "20"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 88403972b53bbefecabde04606f9211c3160ab32
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="astextzm-geometry-data-type"></a>AsTextZM(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

사용 하 여 보강 된 geometry 인스턴스의 Open Geospatial Consortium (OGC) wkt (WELL-KNOWN Text) 표현을 반환 **Z** (높이) 및 **M** (측정값) 값 인스턴스에서 얻어진 합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.AsTextZM ()  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **nvarchar (max)**  
  
 CLR 반환 형식: **SqlChars**  
  
## <a name="remarks"></a>주의  
  
## <a name="examples"></a>예  
 다음 예제에서는 한 `Point` 포함 된 인스턴스 **Z** (높이) 및 **M** (측정값) 값입니다. `STAsText()`WKT 값인 (1 2);를 선택합니다. `AsTextZM()` 동일한 WKT 값을 선택 하 고에 대 한 값도 반환 **Z** 및 **M**, (1 2 3 4)의 차이 계산 합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(1 2 3 4)', 0);  
SELECT @g.STAsText();  
SELECT @g.AsTextZM();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Geometry 인스턴스의 확장된 메서드](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [M &#40; geometry 데이터 형식 &#41;](../../t-sql/spatial-geometry/m-geometry-data-type.md)   
 [Z &#40; geometry 데이터 형식 &#41;](../../t-sql/spatial-geometry/z-geometry-data-type.md)  
  
  

