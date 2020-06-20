---
title: 고유 하 게 컴파일된 저장 프로시저에서 EXISTS 절 시뮬레이션 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c0e187c1-cbd9-463c-b417-8a734574f102
author: rothja
ms.author: jroth
ms.openlocfilehash: 7b16491b9a3729ad4df71c7ddceaee6db21777ff
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049948"
---
# <a name="simulating-an-exists-clause-in-a-natively-compiled-stored-procedure"></a>고유하게 컴파일된 저장 프로시저의 EXISTS 절 시뮬레이션
  고유하게 컴파일된 저장 프로시저는 `EXISTS` 절을 지원하지 않지만 해결 방법이 있습니다.  
  
```sql  
DECLARE @exists BIT = 0  
SELECT TOP 1 @exists = 1 FROM MyTable WHERE ...  
IF @exists = 1  
```  
  
## <a name="see-also"></a>참고 항목  
 [고유 하 게 컴파일된 저장 프로시저의 마이그레이션 문제](migration-issues-for-natively-compiled-stored-procedures.md)   
 [메모리 내 OLTP에서 지원되지 않는 Transact-SQL 구문](transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
