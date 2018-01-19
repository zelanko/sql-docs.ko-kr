---
title: "Parse (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 07/30/2017
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
helpviewer_keywords:
- Parse method
- Parse (geography Data Type)
ms.assetid: 21c402fa-fd0f-4d09-a097-49cee0316d4e
caps.latest.revision: "18"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 32d8925fdf53a1d0bcac33719348138b354376c2
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="parse-geography-data-type"></a>Parse(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

반환 된 **geography** Open Geospatial Consortium (OGC) wkt (WELL-KNOWN Text) 표현의 인스턴스. Parse ()가 같음 [STGeomFromText](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md)spatial reference ID ()의 SRID 4326 매개 변수로 가정 한다는 점을 제외 하면, 합니다. 입력은 Z(높이) 값과 M(측정값) 값을 선택적으로 포함할 수 있습니다.
  
이 **geography** 데이터 형식 메서드 지원 **FullGlobe** 인스턴스 또는 반구 보다 큰 공간 인스턴스.
  
## <a name="syntax"></a>구문  
  
```  
  
Parse ( 'geography_tagged_text' )  
```  
  
## <a name="arguments"></a>인수  
 *geography_tagged_text*  
 WKT 표현입니다는 **geography** 인스턴스를 반환 합니다. *geography_tagged_text* 는 **nvarchar** 식입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="remarks"></a>주의  
 OGC 형식은 **geography** 에서 반환한 인스턴스 `Parse()` 해당 WKT 입력으로 설정 됩니다.  
  
 'Null'으로 해석 됩니다 null 문자열 **geography** 인스턴스.  
  
 이 메서드는 throw **ArgumentException** 입력에 대척점 가장자리를 포함 하는 경우.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Parse()`를 사용하여 `geography` 인스턴스를 만듭니다.  
  
```  
DECLARE @g geography;   
SET @g = geography::Parse('LINESTRING(-122.360 47.656, -122.343 47.656)');  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [확장 정적 지리 메서드](../../t-sql/spatial-geography/extended-static-geography-methods.md)   
 [STGeomFromText&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md)  
  
  
