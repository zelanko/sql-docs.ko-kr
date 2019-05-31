---
title: AsTextZM(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- AsTextZM_TSQL
- AsTextZM
- AsTextZM (geometry Data Type)
- AsTextZM_(geometry_Data_Type)_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- AsTextZM (geometry Data Type)
ms.assetid: 08ac8aa0-aff7-4b22-87e0-1a1d55dcbc04
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 642c3cb7a6158856ad77761cab731be10d459270
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65939173"
---
# <a name="astextzm-geometry-data-type"></a>AsTextZM(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

인스턴스에서 얻어진 **Z**(높이) 값 및 **M**(측정값) 값을 사용하여 보강된 geometry 인스턴스의 OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현을 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.AsTextZM ()  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **nvarchar(max)**  
  
 CLR 반환 형식: **SqlChars**  
  
## <a name="remarks"></a>Remarks  
  
## <a name="examples"></a>예  
 다음 예에서는 **Z**(높이) 값 및 **M**(측정값) 값을 포함하는 `Point` 인스턴스를 만듭니다. `STAsText()`는 WKT 값인 (1 2)을 선택하며 `AsTextZM()`도 동일한 WKT 값을 선택하여 **Z** 및 **M**의 값을 반환하여 (1 2 3 4)를 반환합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(1 2 3 4)', 0);  
SELECT @g.STAsText();  
SELECT @g.AsTextZM();  
```  
  
## <a name="see-also"></a>참고 항목  
 [Geometry 인스턴스의 확장 메서드](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [M&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/m-geometry-data-type.md)   
 [Z&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/z-geometry-data-type.md)  
  
  

