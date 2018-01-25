---
title: "ToString (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: ToString (geography Data Type)
dev_langs: TSQL
helpviewer_keywords: ToString method
ms.assetid: 045c12fa-8fc6-441a-9500-7021cb4ff13e
caps.latest.revision: "18"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bcec246b4358b3d8b59467975bb836ea226463ab
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="tostring-geography-data-type"></a>ToString(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Open Geospatial Consortium (OGC) wkt (WELL-KNOWN Text) 표현을 반환는 **geography** 인스턴스에 의해 수행 되는 인스턴스의 Z (높이) 값 및 M (측정값) 값을 따르도록 합니다.  
  
 이 geography 데이터 형식 메서드 지원 **FullGlobe** 인스턴스 또는 반구 보다 큰 공간 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```  
  
.ToString ()  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **nvarchar (max)**  
  
 CLR 반환 형식: **SqlString**  
  
## <a name="remarks"></a>주의  
 이 메서드는 Null 인스턴스에서 호출되면 문자열 "Null"을 반환합니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], 서버에서 얻을 수 있는 결과 집합이 확장 되었습니다 **FullGlobe** 인스턴스. 이 메서드는 `AsTextZM()`과 동일한 값을 반환합니다.  
  
 이 메서드는 정확하지 않습니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 만들기는 `LineString` 인스턴스 및 사용 하 여 `ToString()` 인스턴스의 텍스트 설명을 반환 하 합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Geography 인스턴스의 확장된 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [AsTextZM&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/astextzm-geography-data-type.md)  
  
  
