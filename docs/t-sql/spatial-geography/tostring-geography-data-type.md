---
description: ToString(geography 데이터 형식)
title: ToString(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ToString (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- ToString method
ms.assetid: 045c12fa-8fc6-441a-9500-7021cb4ff13e
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 491c548960fde425b8f2c021d69dce94b95a7b21
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88472588"
---
# <a name="tostring-geography-data-type"></a>ToString(geography 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  인스턴스에서 얻어진 Z(높이) 값 및 M(측정값) 값을 사용하여 보강된 **geography** 인스턴스의 OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현을 반환합니다.  
  
 이 geography 데이터 형식 메서드는 **FullGlobe** 인스턴스 또는 반구보다 큰 공간 인스턴스를 지원합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.ToString ()  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **nvarchar(max)**  
  
 CLR 반환 형식: **SqlString**  
  
## <a name="remarks"></a>설명  
 이 메서드는 Null 인스턴스에서 호출되면 문자열 "Null"을 반환합니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서는 서버에서 얻을 수 있는 결과 집합이 **FullGlobe** 인스턴스까지 확장되었습니다. 이 메서드는 `AsTextZM()`과 동일한 값을 반환합니다.  
  
 이 메서드는 정확하지 않습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `LineString` 인스턴스를 만들고 `ToString()`을 사용하여 인스턴스의 텍스트 설명을 반환합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>관련 항목  
 [지리 인스턴스의 확장 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [AsTextZM&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/astextzm-geography-data-type.md)  
  
  
