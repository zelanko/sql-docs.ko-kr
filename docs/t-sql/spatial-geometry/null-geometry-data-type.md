---
title: Null(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Null (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- Null (geometry Data Type)
ms.assetid: 67a4b019-9091-4443-85cc-f4836d0cb509
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: ccf081a6f1bac088c4a7539d4efd367f3bb7fade
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65937494"
---
# <a name="null-geometry-data-type"></a>Null(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

**geometry** 형식의 Null 인스턴스를 제공하는 읽기 전용 속성입니다.
  
## <a name="syntax"></a>구문  
  
```  
  
Null  
```  
  
## <a name="arguments"></a>인수  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 형식: **geometry**  
  
 CLR 유형: **SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
  
## <a name="examples"></a>예  
 다음 예에서는 Null `geometry` 인스턴스를 검색합니다.  
  
```  
DECLARE @g geometry;   
SET @g = geometry::[Null];  
SELECT @g  
```  
  
## <a name="see-also"></a>참고 항목  
 [확장 정적 기하 도형 메서드](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

