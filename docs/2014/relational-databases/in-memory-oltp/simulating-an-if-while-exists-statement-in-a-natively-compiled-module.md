---
title: 고유 하 게 컴파일된 저장된 프로시저의 EXISTS 절 시뮬레이션 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c0e187c1-cbd9-463c-b417-8a734574f102
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a5e4059f143de6353608603562ca80f3e0b7b0f8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48084163"
---
# <a name="simulating-an-exists-clause-in-a-natively-compiled-stored-procedure"></a>고유하게 컴파일된 저장 프로시저의 EXISTS 절 시뮬레이션
  고유하게 컴파일된 저장 프로시저는 `EXISTS` 절을 지원하지 않지만 해결 방법이 있습니다.  
  
```tsql  
DECLARE @exists BIT = 0  
SELECT TOP 1 @exists = 1 FROM MyTable WHERE …  
IF @exists = 1  
```  
  
## <a name="see-also"></a>관련 항목  
 [고유하게 컴파일된 저장 프로시저의 마이그레이션 문제](migration-issues-for-natively-compiled-stored-procedures.md)   
 [메모리 내 OLTP에서 지원되지 않는 Transact-SQL 구문](transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
