---
title: ROLLBACK WORK (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ROLLBACK WORK
- ROLLBACK_WORK_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- transaction rollbacks [SQL Server]
- erasing data modifications [SQL Server]
- ROLLBACK WORK statement
- roll back transactions [SQL Server]
- rolling back transactions, ROLLBACK WORK
- savepoints [SQL Server]
ms.assetid: 2071dbd3-53d5-4510-be8d-26e80f2553b4
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d1a4eadefc731dd403b7900af4b5d2e32d4c358d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="rollback-work-transact-sql"></a>ROLLBACK WORK(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  사용자가 지정한 트랜잭션을 시작 부분으로 롤백합니다.  
  
 
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
ROLLBACK [ WORK ]  
[ ; ]  
```  
  
## <a name="remarks"></a>주의  
 ROLLBACK TRANSACTION이 사용자 정의 트랜잭션 이름을 허용하는 것을 제외하면 이 문은 ROLLBACK TRANSACTION과 동일한 기능을 수행합니다. ROLLBACK 구문은 선택적으로 지정할 수 있는 WORK 키워드와 함께 ISO와 호환됩니다.  
  
 트랜잭션을 중첩할 경우 ROLLBACK WORK 항상 롤백합니다 가장 바깥쪽 BEGIN TRANSACTION 문 및 감소는 @@TRANCOUNT 시스템 함수를 0으로 합니다.  
  
## <a name="permissions"></a>Permissions  
 ROLLBACK WORK 권한은 기본적으로 모든 유효한 사용자에게 부여됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [BEGIN DISTRIBUTED TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [BEGIN TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [커밋 작업 &#40; Transact SQL &#41;](../../t-sql/language-elements/commit-work-transact-sql.md)   
 [ROLLBACK TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [SAVE TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/save-transaction-transact-sql.md)  
  
  

