---
title: MakeValid (geography Data Type) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- MakeValid method (geography)
ms.assetid: f67038e3-4f62-4465-994e-e95ac27d8ada
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: d913a0e7bbe29ab6f6f303519c73304238afd7df
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68127401"
---
# <a name="makevalid-geography-data-type"></a>MakeValid(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  잘못된 **geography** 인스턴스를 유효한 OGC(Open Geospatial Consortium) 형식의 **geography** 인스턴스로 변환합니다.  
  
 입력 개체가 STIsValid()에 대해 False를 반환하면 `MakeValid()`가 잘못된 인스턴스를 유효한 인스턴스로 변환합니다.  
  
 이 geography 데이터 형식 메서드는 **FullGlobe** 인스턴스 또는 반구보다 큰 공간 인스턴스를 지원합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.MakeValid ()  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="remarks"></a>설명  
 이 메서드는 **geography** 인스턴스의 유형을 변경할 수 있습니다. 또한 **geography** 인스턴스의 지점이 약간 이동할 수도 있습니다. 이로 인해 NumPoint()와 같은 일부 메서드의 결과가 변경될 수 있습니다.  
  
 잘못된 공간 인스턴스가 적도를 교차하고 EnvelopeAngle() = 180인 경우 **FullGlobe** 인스턴스가 반환됩니다. `MakeValid()`**geography** 데이터 형식 메서드는 유효한 인스턴스가 반환되지만 결과의 정확성이 보장되지 않는 경우에 가장 적합합니다.  
  
> [!NOTE]  
>  유효하지 않은 개체가 데이터베이스에 저장될 수 있습니다. 잘못된 인스턴스(STIsValid()에서 False를 반환하는 인스턴스)에서 실행될 수 있는 메서드는 유효성을 검사하거나 내보내기를 허용하는 메서드로서, STIsValid(), MakeValid(), STAsText(), STAsBinary(), ToString(), AsTextZM() 및 AsGml()이 해당합니다.  
  
 이 메서드는 정확하지 않습니다.  
  
## <a name="examples"></a>예  
 첫 번째 예에서는 자체적으로 겹치는 잘못된 `LineString` 인스턴스를 만들고 `STIsValid()`를 사용하여 해당 인스턴스가 잘못되었음을 확인합니다. `STIsValid()`는 잘못된 인스턴스에 대해 값 0을 반환합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(0 2, 1 1, 1 0, 1 1, 2 2)', 4326);  
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
  
## <a name="see-also"></a>참고 항목  
 [STIsValid&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)   
 [지리 인스턴스의 확장 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
