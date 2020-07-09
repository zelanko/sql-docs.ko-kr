---
title: STLineFromText(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STLineFromText (geometry Data Type)
- STLineFromText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STLineFromText (geometry Data Type)
ms.assetid: 430508ad-207b-4dee-a4d1-4ddf25e6b4a9
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 786bae63444499d440133411f6b6ed8bf5c820cc
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85762360"
---
# <a name="stlinefromtext-geometry-data-type"></a>STLineFromText(geometry 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

인스턴스에서 얻어진 Z(높이) 값 및 M(측정값) 값을 사용하여 보강된 OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현의 **geometry** 인스턴스를 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
STLineFromText ( 'linestring_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>인수  
 *linestring_tagged_text*  
 반환하려는 **geometryLineString** 인스턴스의 WKT 표현입니다. *linestring_tagged_text*는 **nvarchar(max)** 식입니다.  
  
 *SRID*  
 반환하려는 **geometryLineString** 인스턴스의 SRID(spatial reference ID)를 나타내는 **int** 식입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geometry**  
  
 CLR 반환 형식: **SqlGeometry**  
  
 OGC 형식: **LineString**  
  
## <a name="remarks"></a>설명  
이 메서드는 입력이 잘못된 경우 **FormatException**을 throw합니다. Open Geospatial Consortium(OGC) Simple Features for SQL Specification 버전 1.2.1에서 제공하는 3차원 및 측정된 기하 도형 WKT 표기법은 지원되지 않습니다. Z(높이) 및 M(측정) 값에 지원되는 표현에 대한 예를 참조하세요.
  
## <a name="examples"></a>예  
 다음 예에서는 `STLineFromText()`를 사용하여 `geometry` 인스턴스를 만듭니다.

### <a name="example-1-two-dimension-geometry-wkt"></a>예제 1: 2차원 기하 도형 WKT
```  
DECLARE @g geometry;  
SET @g = geometry::STLineFromText('LINESTRING (100 100, 200 200)', 0);  
SELECT @g.ToString();  
```  
  
### <a name="example-2-three-dimension-geometry-wkt"></a>예제 2: 3차원 기하 도형 WKT
```  
DECLARE @g geometry;  
SET @g = geometry::STLineFromText('LINESTRING (100 100 100, 200 200 200)', 0);  
SELECT @g.ToString();  
``` 

### <a name="example-3-two-dimension-measured-geometry-wkt"></a>예 3: 2차원 측정된 기하 도형 WKT
```  
DECLARE @g geometry;  
SET @g = geometry::STLineFromText('LINESTRING (100 100 NULL 100, 200 200 NULL 200)', 0);  
SELECT @g.ToString();  
``` 

### <a name="example-4-three-dimension-measured-geometry-wkt"></a>예 4: 3차원 측정된 기하 도형 WKT
```  
DECLARE @g geometry;  
SET @g = geometry::STLineFromText('LINESTRING (100 100 100 100, 200 200 200 200)', 0);  
SELECT @g.ToString();  
``` 
## <a name="see-also"></a>참고 항목  
 [OGC 정적 기하 도형 메서드](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

