---
title: "Null (geometry 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
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
- Null (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- Null (geometry Data Type)
ms.assetid: 67a4b019-9091-4443-85cc-f4836d0cb509
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a036b1801284fa43e4bdf7b690037711e9970638
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="null-geometry-data-type"></a>Null(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

null 인스턴스를 제공 하는 읽기 전용 속성은 **geometry** 유형입니다.
  
## <a name="syntax"></a>구문  
  
```  
  
Null  
```  
  
## <a name="arguments"></a>인수  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]형식: **기 하 도형**  
  
 CLR 형식: **SqlGeometry**  
  
## <a name="remarks"></a>주의  
  
## <a name="examples"></a>예  
 다음 예에서는 Null `geometry` 인스턴스를 검색합니다.  
  
```  
DECLARE @g geometry;   
SET @g = geometry::[Null];  
SELECT @g  
```  
  
## <a name="see-also"></a>관련 항목:  
 [확장 정적 기하 도형 메서드](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

