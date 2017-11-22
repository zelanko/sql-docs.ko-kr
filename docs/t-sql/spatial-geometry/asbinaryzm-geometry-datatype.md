---
title: "AsBinaryZM (geometry 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
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
helpviewer_keywords: AsBinaryZM geometry
ms.assetid: 5eae2872-adca-4b8f-8b04-4ee91ced98f1
caps.latest.revision: "6"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1a509d7e6297081816cfdd146ea10afc90be7e60
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="asbinaryzm-geometry-datatype"></a>AsBinaryZM(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Open Geospatial Consortium (OGC) wkb (WELL-KNOWN Binary) 표현을 반환는 **geometry** 인스턴스 사용 하 여 보강 된 **Z** (높이) 및 **M** (측정값) 인스턴스에서 얻어진 값입니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.AsBinaryZM()  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **varbinary (max)**  
  
 CLR 반환 형식: **SqlBytes**  
  
## <a name="remarks"></a>주의  
  
## <a name="examples"></a>예  
  
```tsql  
DECLARE @g1 GEOMETRY = 'Point(1 1 2 3)';  
  
SELECT @g1.STAsBinary();  
-- Returns: 0x0101000000000000000000F03F000000000000F03F  
  
SELECT @g1.AsBinaryZM();  
--Returns: 0x01B90B0000000000000000F03F000000000000F03F00000000000000400000000000000840  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Geometry 인스턴스의 확장된 메서드](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [M &#40; geometry 데이터 형식 &#41;](../../t-sql/spatial-geometry/m-geometry-data-type.md)   
 [Z &#40; geometry 데이터 형식 &#41;](../../t-sql/spatial-geometry/z-geometry-data-type.md)  
  
  

