---
title: "IF 시뮬레이션-고유하게 컴파일된 모듈에서 WHILE EXISTS 문 | Microsoft 문서"
ms.custom: SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c0e187c1-cbd9-463c-b417-8a734574f102
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 344c7581c9265eca529d4749b5614a66d4e60239
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="simulating-an-if-while-exists-statement-in-a-natively-compiled-module"></a>IF 시뮬레이션-고유하게 컴파일된 모듈에서 WHILE EXISTS 문
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  고유하게 컴파일된 저장 프로시저는 IF 및 WHILE 절과 같은 조건문에서 **EXISTS** 을 지원하지 않습니다.  
  
 다음 예제에서는 EXISTS 절을 시뮬레이션하도록 SELECT 문으로 BIT 변수를 사용하여 문제를 해결하는 방법을 보여줍니다.  
  
```tsql  
DECLARE @exists BIT = 0  
SELECT TOP 1 @exists = 1 FROM MyTable WHERE …  
IF @exists = 1  
```  
  
## <a name="see-also"></a>참고 항목  
 [고유하게 컴파일된 저장 프로시저의 마이그레이션 문제](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)   
 [메모리 내 OLTP에서 지원되지 않는 Transact-SQL 구문](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
