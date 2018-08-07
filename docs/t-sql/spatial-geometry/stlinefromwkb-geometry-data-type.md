---
title: STLineFromWKB(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, pdw, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- STLineFromWKB (geometry Data Type)
- STLineFromWKB_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STLineFromWKB (geometry Data Type)
ms.assetid: e674c8c4-c67f-4fc1-9873-d9c2ed46c659
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: ba89a46c419c2289de4c3e24f103e61f7e7146f2
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39451468"
---
# <a name="stlinefromwkb-geometry-data-type"></a>STLineFromWKB(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

OGC(Open Geospatial Consortium) WKB(Well-Known Binary) 표현에서 **geometryLineString** 인스턴스를 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
STLineFromWKB ( 'WKB_linestring' , SRID )  
```  
  
## <a name="arguments"></a>인수  
 *WKB_linestring*  
 반환하려는 **geometryLineString** 인스턴스의 WKB 표현입니다. *WKB_linestring*은 **varbinary(max)** 식입니다.  
  
 *SRID*  
 반환하려는 **geometryLineString** 인스턴스의 SRID(spatial reference ID)를 나타내는 **int** 식입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geometry**  
  
 CLR 반환 형식: **SqlGeometry**  
  
 OGC 형식: **LineString**  
  
## <a name="remarks"></a>Remarks  
 이 메서드는 입력이 잘못된 경우 **FormatException**을 throw합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `STLineFromWKB()`를 사용하여 `geometry` 인스턴스를 만듭니다.  
  
```  
DECLARE @g geometry;   
SET @g = geometry::STLineFromWKB(0x0102000000020000000000000000005940000000000000594000000000000069400000000000006940, 0);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>참고 항목  
 [OGC 정적 기하 도형 메서드](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

