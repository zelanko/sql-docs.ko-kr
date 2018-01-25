---
title: "MakeValid (geometry 데이터 형식) | Microsoft Docs"
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
- MakeValid
- MakeValid_TSQL
dev_langs: TSQL
helpviewer_keywords: MakeValid (geometry Data Type)
ms.assetid: 38673010-ab77-4ebb-9c4d-b26b79e3b7ea
caps.latest.revision: "22"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0694b49b23d87d30e7134c822de295ec5b840544
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="makevalid-geometry-data-type"></a>MakeValid(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

잘못 된 변환 **geometry** 인스턴스는 **geometry** 유효한 Open Geospatial Consortium (OGC) 형식으로 인스턴스.
  
## <a name="syntax"></a>구문  
  
```  
  
.MakeValid ()  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **기 하 도형**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="remarks"></a>주의  
 이 메서드는 형식의에서 변경 발생할 수 있습니다는 **기 하 도형** 의 점이 뿐만 아니라 인스턴스를 한 **기 하 도형** 인스턴스 조금 이동할 수 있습니다.  
  
## <a name="examples"></a>예  
 첫 번째 예에서는 자체적으로 겹치는 잘못된 `LineString` 인스턴스를 만들고 `STIsValid()`를 사용하여 해당 인스턴스가 잘못되었음을 확인합니다. `STIsValid()`는 잘못된 인스턴스에 대해 값 0을 반환합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 1 1, 1 0, 1 1, 2 2)', 0);  
SELECT @g.STIsValid();  
```  
  
 두 번째 예에서는 `MakeValid()`를 사용하여 유효한 인스턴스를 만들고 이 인스턴스가 실제로 유효한지 테스트합니다. `STIsValid()`는 유효한 인스턴스에 대해 값 1을 반환합니다.  
  
```  
SET @g = @g.MakeValid();  
SELECT @g.STIsValid();  
```  
  
 세 번째 예에서는 인스턴스를 유효한 인스턴스로 만들도록 변경하는 방법을 확인합니다.  
  
```  
SELECT @g.ToString();  
```  
  
 이 예에서는 `LineString` 인스턴스가 선택되면 값이 유효한 `MultiLineString` 인스턴스로 반환됩니다.  
  
```  
MULTILINESTRING ((0 2, 1 1, 2 2), (1 1, 1 0))  
```  
  
 다음 예에서는 CircularString 인스턴스를 Point 인스턴스로 변환합니다.  
  
```  
DECLARE @g geometry = 'CIRCULARSTRING(1 1, 1 1, 1 1)';  
SELECT @g.MakeValid().ToString();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [STIsValid&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)   
 [geometry 인스턴스의 확장 메서드](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

