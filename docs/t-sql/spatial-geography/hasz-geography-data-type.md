---
title: "HasZ (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 05/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- HasZ
- HasZ_TSQL
dev_langs: TSQL
helpviewer_keywords: HasZ geography
ms.assetid: 4c5e1669-a987-4dda-9ebf-f573ce615c34
caps.latest.revision: "7"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6f02ac5c15467cd04afca6b83fc9477372374719
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="hasz-geography-data-type"></a>HasZ(geography 데이터 형식)
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
  
```tsql  
DECLARE @p GEOGRAPHY = 'Point(1 1 1 1)'  
SELECT @p.HasZ   
--Returns: 1 (true)  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Geography 인스턴스의 확장된 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [Z &#40; geography 데이터 형식 &#41;](../../t-sql/spatial-geography/z-geography-data-type.md)  
  
  
