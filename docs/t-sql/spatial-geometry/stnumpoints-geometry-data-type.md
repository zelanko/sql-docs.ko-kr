---
title: STNumPoints(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STNumPoints_TSQL
- STNumPoints (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STNumPoints (geometry Data Type)
ms.assetid: a19520fc-7f91-4a2c-856f-4d8b99a7e496
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f135ce5a68cade2180a837562deae0129dc6cbab
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47683700"
---
# <a name="stnumpoints-geometry-data-type"></a>STNumPoints(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  **geometry** 인스턴스의 각 도형에 있는 점의 총 개수를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STNumPoints ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **int**  
  
 CLR 반환 형식: **SqlInt32**  
  
## <a name="remarks"></a>Remarks  
 이 메서드는 **geometry** 인스턴스의 설명에 있는 점을 셉니다. 중복 점도 개수에 포함됩니다. 이 인스턴스가 **collection** 형식인 경우 이 메서드는 컬렉션의 각 요소에 있는 점의 총 개수를 반환합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `LineString` 인스턴스를 만들고 `STNumPoints()`를 사용하여 인스턴스의 설명에 사용된 점의 수를 확인합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STNumPoints();  
```  
  
## <a name="see-also"></a>참고 항목  
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
