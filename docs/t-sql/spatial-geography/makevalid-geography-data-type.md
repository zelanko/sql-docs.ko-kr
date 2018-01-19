---
title: "MakeValid (geography 데이터 형식) | Microsoft Docs"
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
dev_langs: TSQL
helpviewer_keywords: MakeValid method (geography)
ms.assetid: f67038e3-4f62-4465-994e-e95ac27d8ada
caps.latest.revision: "14"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 796b06fb230cffbfe813d204017dc58c24d8c5b2
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="makevalid-geography-data-type"></a>MakeValid(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  변환는 **geography** 을 유효한 유효 하지 않은 인스턴스 **geography** 유효한 Open Geospatial Consortium (OGC) 형식으로 인스턴스.  
  
 입력된 개체 STIsValid()에 대 한 False를 반환 하는 경우 `MakeValid()` 올바른 인스턴스를 유효 하지 않은 인스턴스를 변환 합니다.  
  
 이 geography 데이터 형식 메서드 지원 **FullGlobe** 인스턴스 또는 반구 보다 큰 공간 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```  
  
.MakeValid ()  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="remarks"></a>주의  
 이 메서드는 유형의 변경 될 수 있습니다는 **geography** 인스턴스. 또한 요소는 **geography** 인스턴스 약간 이동할 수도 있습니다. NumPoint() 같은 몇 가지 방법 중에서 결과 변경할 수 있습니다.  
  
 = 180 인 경우 여기서 잘못 된 공간 인스턴스가 적도 교차 되었으며는 EnvelopeAngle()는 **FullGlobe** 인스턴스가 반환 됩니다. `MakeValid()` **geography** 데이터 형식 메서드는 유효한 인스턴스가 반환에서 최적의 시도 하면 되지만 결과가 정확 하 게 또는 정확 하 게 되도록 정렬 되지 않습니다.  
  
> [!NOTE]  
>  유효하지 않은 개체가 데이터베이스에 저장될 수 있습니다. 잘못 된 인스턴스에서 실행할 수 있는 메서드는 유효성을 검사 하거나 내보내기를 허용 하는 메서드는 (이러한 인스턴스는 STIsValid() False 반환): STIsValid(), makevalid (), stastext (), STAsBinary(), tostring (), AsTextZM(), 및 AsGml() 합니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [STIsValid&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)   
 [지리 인스턴스의 확장 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
