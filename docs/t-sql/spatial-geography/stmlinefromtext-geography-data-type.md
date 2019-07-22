---
title: STMLineFromText(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STMLineFromText (geography Data Type)
- STMLineFromText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STLineFromText method
ms.assetid: 66dfd722-a9bd-45d3-9788-f1946dd23e17
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 57d0edaed1d26de79813939c9606b9934646e5f7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68223654"
---
# <a name="stmlinefromtext-geography-data-type"></a>STMLineFromText(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

인스턴스에서 얻어진 Z(높이) 값 및 M(측정값) 값을 사용하여 보강된 OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현의 **geography** 인스턴스를 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
STMLineFromText ( 'multilinestring_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>인수  
 *multilinestring_tagged_text*  
 반환할 **geographyMultiLineString** 인스턴스의 WKT 표현입니다. *multilinestring_tagged_text*는 **nvarchar(max)** 식입니다.  
  
 *SRID*  
 반환할 **geographyMultiLineString** 인스턴스의 SRID(spatial reference ID)를 나타내는 **int** 식입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
 OGC 형식: **MultiLineString**  
  
## <a name="remarks"></a>Remarks  
 이 메서드는 입력이 잘못된 경우 **FormatException**을 throw합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `STMLineFromText()`를 사용하여 `geography` 인스턴스를 만듭니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STMLineFromText('MULTILINESTRING ((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653), (-122.357 47.654, -122.357 47.657, -122.349 47.657, -122.349 47.650, -122.357 47.654))', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>참고 항목  
 [OGC 정적 지리 메서드](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
