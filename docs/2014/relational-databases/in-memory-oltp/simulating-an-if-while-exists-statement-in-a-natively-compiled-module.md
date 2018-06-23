---
title: 고유 하 게 컴파일된 저장된 프로시저의 EXISTS 절 시뮬레이션 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c0e187c1-cbd9-463c-b417-8a734574f102
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: 68515c717fa39cfd626c83625dc7b95c24c68d69
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36093313"
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
  
  