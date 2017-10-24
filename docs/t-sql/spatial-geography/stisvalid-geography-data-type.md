---
title: "STIsValid (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STIsValid method (geography)
ms.assetid: 1bfe787f-ddf0-4fc7-af6a-570a58faab23
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2149008613cf38f1d4e3ac138afd776e16f4250b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stisvalid-geography-data-type"></a>STIsValid(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  이면 true를 반환은 **geography** 인스턴스가 잘 구성 되 고 해당 Open Geospatial Consortium (OGC) 형식을 기반으로 올바른 geography 개체로 인식 합니다. 되었으면 false를 반환 된 **geography** 인스턴스 형식이 잘못 되었습니다. 이 메서드는 정확합니다.  
  
 이 geography 데이터 형식 메서드 지원 **FullGlobe** 인스턴스 또는 반구 보다 큰 공간 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STIsValid ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **비트**  
  
 CLR 반환 형식: **SqlBoolean**  
  
## <a name="remarks"></a>주의  
 OGC 형식은 **geography** 를 호출 하 여 인스턴스를 확인할 수 있습니다 [stgeometrytype ()](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md)합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]유효한 생성 **geography** 인스턴스에 하지만 검색의 잘못 된 인스턴스 확인 하 고 저장소에 대 한 허용 합니다. 잘못된 인스턴스의 동일한 점 집합을 나타내는 올바른 인스턴스는 `MakeValid()` 메서드를 사용하여 검색할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `geography` 인스턴스를 만들고 `STIsValid()`를 사용하여 인스턴스가 올바른지 테스트합니다.  
  
```  
DECLARE @g geography = geography::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 4326);  
SELECT @g.STIsValid();  
DECLARE @g geography  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Stgeometrytype&#40; geography 데이터 형식 &#41;](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md)   
 [MakeValid&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/makevalid-geography-data-type.md)   
 [Geography 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  

