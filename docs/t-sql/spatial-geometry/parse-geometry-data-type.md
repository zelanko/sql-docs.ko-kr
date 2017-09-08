---
title: "Parse (geometry 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
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
- Parse (geometry Data Type)
ms.assetid: 6e080919-4b64-46cd-8dd2-254a9c232e53
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 64adf9398a6ea63203f75714aa97ccf2653e947b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="parse-geometry-data-type"></a>Parse(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

반환 된 **geometry** Open Geospatial Consortium (OGC) wkt (WELL-KNOWN Text) 표현의 인스턴스. `Parse()`에 해당 [STGeomFromText()](../../t-sql/spatial-geometry/parse-geometry-data-type.md), 가정 spatial 예외로 SRID 0을 매개 변수로 참조 합니다. 입력은 Z(높이) 값과 M(측정값) 값을 선택적으로 포함할 수 있습니다.
  
## <a name="syntax"></a>구문  
  
```  
  
Parse ( 'geometry_tagged_text' )  
```  
  
## <a name="arguments"></a>인수  
 *geometry_tagged_text*  
 WKT 표현에서 **기 하 도형** 반환할 인스턴스. *geometry_tagged_text* 는 **nvarchar** 식입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **기 하 도형**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="remarks"></a>주의  
 OGC 형식은 **geometry** 에서 반환한 인스턴스 `Parse()` 해당 WKT 입력으로 설정 됩니다.  
  
 'Null'으로 해석 됩니다 null 문자열 **geometry** 인스턴스.  
  
 이 메서드는 throw 된 **FormatException** 입력이 잘못 된 경우.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Parse()`를 사용하여 `geometry` 인스턴스를 만듭니다.  
  
```  
DECLARE @g geometry;   
SET @g = geometry::Parse('LINESTRING (100 100, 20 180, 180 180)');  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [STGeomFromText](../../t-sql/spatial-geometry/parse-geometry-data-type.md)   
 [확장 정적 기 하 도형 메서드](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  


