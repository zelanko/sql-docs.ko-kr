---
title: IF 시뮬레이션-고유하게 컴파일된 모듈에서 WHILE EXISTS 문 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c0e187c1-cbd9-463c-b417-8a734574f102
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 691e91fe8e78d89d98dc8624aef2ecc83da0b5b9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="simulating-an-if-while-exists-statement-in-a-natively-compiled-module"></a>IF 시뮬레이션-고유하게 컴파일된 모듈에서 WHILE EXISTS 문
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  고유하게 컴파일된 저장 프로시저는 IF 및 WHILE 절과 같은 조건문에서 **EXISTS** 을 지원하지 않습니다.  
  
 다음 예제에서는 EXISTS 절을 시뮬레이션하도록 SELECT 문으로 BIT 변수를 사용하여 문제를 해결하는 방법을 보여줍니다.  
  
```sql  
DECLARE @exists BIT = 0  
SELECT TOP 1 @exists = 1 FROM MyTable WHERE …  
IF @exists = 1  
```  
  
## <a name="see-also"></a>참고 항목  
 [고유하게 컴파일된 저장 프로시저의 마이그레이션 문제](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)   
 [메모리 내 OLTP에서 지원되지 않는 Transact-SQL 구문](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
