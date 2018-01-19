---
title: "HasZ (geometry 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 05/05/2017
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
helpviewer_keywords: HasZ geometry
ms.assetid: aa378943-252a-4079-848b-6c59344fcfce
caps.latest.revision: "6"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 71a46abe72ce0b9d354d59cfbf0f1f678514e7ad
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="hasz-geometry-datatype"></a>HasZ(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  공간 개체에 Z 값이 하나 이상 포함된 경우 1(true)을 반환하고, 그렇지 않으면 0(false)을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.HasZ  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **비트**  
  
 CLR 반환 형식: **부울**  
  
## <a name="remarks"></a>주의  
  
## <a name="examples"></a>예  
  
```sql  
DECLARE @p GEOMETRY = 'Point(1 1 1 1)'  
SELECT @p.HasZ   
--Returns: 1 (true)  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Geometry 인스턴스의 확장된 메서드](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [Z &#40; geometry 데이터 형식 &#41;](../../t-sql/spatial-geometry/z-geometry-data-type.md)  
  
  
