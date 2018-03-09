---
title: "Null (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Null (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- Null (geography Data Type)
- Null method
ms.assetid: bb464b06-86e0-4b8b-ad78-04bd33b6069c
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0e0b8bd71e8c9ed3066e7d632423162cd165f6a5
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="null-geography-data-type"></a>Null(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

null 인스턴스를 제공 하는 읽기 전용 속성은 **geography** 유형입니다.
  
## <a name="syntax"></a>구문  
  
```  
  
Null  
```  
  
## <a name="arguments"></a>인수  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]형식: **geography**  
  
 CLR 형식: **SqlGeography**  
  
## <a name="remarks"></a>주의  
  
## <a name="examples"></a>예  
 다음 예에서는 Null `geography` 인스턴스를 검색합니다.  
  
```  
DECLARE @g geography;   
SET @g = geography::[Null];  
SELECT @g  
```  
  
## <a name="see-also"></a>관련 항목:  
 [확장 정적 지리 메서드](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  
