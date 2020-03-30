---
title: Parse(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Parse (geometry Data Type)
ms.assetid: 6e080919-4b64-46cd-8dd2-254a9c232e53
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 91bcf58df4f8dd9651f077c200d69eea2c1f7660
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68101049"
---
# <a name="parse-geometry-data-type"></a>Parse(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현의 **geometry** 인스턴스를 반환합니다. SRID(Spatial Reference ID) 0을 매개 변수로 가정한다는 점을 제외하고 `Parse()`는 [STGeomFromText()](../../t-sql/spatial-geometry/parse-geometry-data-type.md)와 동일합니다. 입력은 Z(높이) 값과 M(측정값) 값을 선택적으로 포함할 수 있습니다.
  
## <a name="syntax"></a>구문  
  
```  
  
Parse ( 'geometry_tagged_text' )  
```  
  
## <a name="arguments"></a>인수  
 *geometry_tagged_text*  
 반환할 **geometry** 인스턴스의 WKT 표현입니다. *geometry_tagged_text*는 **nvarchar** 식입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geometry**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="remarks"></a>설명  
 **에 의해 반환되는** geometry`Parse()` 인스턴스의 OGC 형식은 해당 WKT 입력으로 설정됩니다.  
  
 문자열 'Null'은 Null **geometry** 인스턴스로 해석됩니다.  
  
 이 메서드는 입력이 잘못된 경우 **FormatException**을 throw합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Parse()`를 사용하여 `geometry` 인스턴스를 만듭니다.  
  
```  
DECLARE @g geometry;   
SET @g = geometry::Parse('LINESTRING (100 100, 20 180, 180 180)');  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>참고 항목  
 [STGeomFromText](../../t-sql/spatial-geometry/parse-geometry-data-type.md)   
 [확장 정적 기하 도형 메서드](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

