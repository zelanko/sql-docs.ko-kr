---
title: MakeValid(geometry 데이터 형식) | Miciosoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- MakeValid
- MakeValid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MakeValid (geometry Data Type)
ms.assetid: 38673010-ab77-4ebb-9c4d-b26b79e3b7ea
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 7b966741a1a6183379f7f2b1f4fa45c37e8044eb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65937531"
---
# <a name="makevalid-geometry-data-type"></a>MakeValid(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

잘못된 **geometry** 인스턴스를 유효한 OGC(Open Geospatial Consortium) 형식의 **geometry** 인스턴스로 변환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.MakeValid ()  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geometry**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 이 메서드로 인해 **geometry** 인스턴스의 점이 약간 변경될 수 있을 뿐만 아니라 **geometry** 인스턴스의 형식 자체가 변경될 수 있습니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [STIsValid&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)   
 [geometry 인스턴스의 확장 메서드](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

