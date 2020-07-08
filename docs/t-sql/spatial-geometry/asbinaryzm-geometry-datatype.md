---
title: AsBinaryZM(geometry 데이터 형식) | Microsoft Docs
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
- AsBinaryZM geometry
ms.assetid: 5eae2872-adca-4b8f-8b04-4ee91ced98f1
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: dc97cf967c645db6f647266190000252fd2d9022
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85700948"
---
# <a name="asbinaryzm-geometry-datatype"></a>AsBinaryZM(geometry 데이터 형식)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

인스턴스에서 얻어진 **Z**(높이) 값 및 **M**(측정값) 값을 사용하여 보강된 **geometry** 인스턴스의 OGC(Open Geospatial Consortium) WKB(Well-Known Binary) 표현을 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.AsBinaryZM()  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **varbinary(max)**  
  
 CLR 반환 형식: **SqlBytes**  
  
## <a name="remarks"></a>설명  
  
## <a name="examples"></a>예  
  
```sql  
DECLARE @g1 GEOMETRY = 'Point(1 1 2 3)';  
  
SELECT @g1.STAsBinary();  
-- Returns: 0x0101000000000000000000F03F000000000000F03F  
  
SELECT @g1.AsBinaryZM();  
--Returns: 0x01B90B0000000000000000F03F000000000000F03F00000000000000400000000000000840  
```  
  
## <a name="see-also"></a>참고 항목  
 [Geometry 인스턴스의 확장 메서드](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [M&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/m-geometry-data-type.md)   
 [Z&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/z-geometry-data-type.md)  
  
  

