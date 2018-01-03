---
title: "AsBinaryZM (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
- AsBinaryZM
- AsBinaryZM_TSQL
dev_langs: TSQL
helpviewer_keywords:
- AsBinaryZM, geography
- AsBinaryZM
ms.assetid: 37246adb-814d-4113-9983-4d336de8182c
caps.latest.revision: "7"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9abdf15e501c014a53c587799c6f246113567cb9
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/02/2018
---
# <a name="asbinaryzm-geography-data-type"></a>AsBinaryZM(geography 데이터 형식)
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
  
```sql  
DECLARE @g1 GEOGRAPHY = 'Point(1 1 2 3)';  
  
SELECT @g1.STAsBinary();  
-- Returns: 0x0101000000000000000000F03F000000000000F03F  
  
SELECT @g1.AsBinaryZM();  
--Returns: 0x01B90B0000000000000000F03F000000000000F03F00000000000000400000000000000840  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Geography 인스턴스의 확장된 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [M &#40; geography 데이터 형식 &#41;](../../t-sql/spatial-geography/m-geography-data-type.md)   
 [Z &#40; geography 데이터 형식 &#41;](../../t-sql/spatial-geography/z-geography-data-type.md)  
  
  
