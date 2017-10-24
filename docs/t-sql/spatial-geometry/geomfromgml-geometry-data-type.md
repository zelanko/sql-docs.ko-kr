---
title: "GeomFromGml (geometry 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GeomFromGML_TSQL
- GeomFromGML
dev_langs:
- TSQL
helpviewer_keywords:
- GeomFromGML (geometry Data Type)
ms.assetid: a3f2c84b-a49f-4ce3-ba25-b903fb0c99b4
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b16e57ed05ba2d0bccf46db95b1e515a7d1d0efd
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="geomfromgml-geometry-data-type"></a>GeomFromGml(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

생성 한 **기 하 도형** 표현이 지정 된 인스턴스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하위 집합의는 언어 GML (Geography Markup).
  
Geography Markup Language에 대한 자세한 내용은 다음 Open Geospatial Consortium Specifications를 참조하세요.
  
[OGC Specifications, Geography Markup Language](http://go.microsoft.com/fwlink/?LinkId=93629)
  
## <a name="syntax"></a>구문  
  
```  
  
GeomFromGml ( GML_input, SRID )  
```  
  
## <a name="arguments"></a>인수  
 *GML_input*  
 GML이 값을 반환하는 데 사용되는 XML 입력입니다.  
  
 *SRID*  
 이 **int** spatial 나타내는 식 참조의 ID (SRID)는 **geometry** 반환할 인스턴스.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **기 하 도형**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="remarks"></a>주의  
 이 메서드는 throw 된 **FormatException** 입력이 잘못 된 경우.  
  
## <a name="examples"></a>예  
 다음 예에서는 `GeomFromGml()`를 사용하여 `geometry` 인스턴스를 만듭니다.  
  
```  
DECLARE @g geometry;  
DECLARE @x xml;  
SET @x = '<LineString xmlns="http://www.opengis.net/gml"> <posList>100 100 20 180 180 180</posList> </LineString>';  
SET @g = geometry::GeomFromGml(@x, 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [확장 정적 기 하 도형 메서드](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  


