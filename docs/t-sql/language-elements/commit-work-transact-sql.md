---
title: COMMIT WORK(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COMMIT_WORK_TSQL
- WORK_TSQL
- WORK
- COMMIT WORK
dev_langs:
- TSQL
helpviewer_keywords:
- ending transactions [SQL Server]
- transactions [SQL Server], ending
- marking end of transactions [SQL Server]
- COMMIT WORK statement
ms.assetid: 4de76f33-399e-4912-a617-6eb6c560a058
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 342d6a2ca2ea51de4e9f887acd39a829713fe275
ms.sourcegitcommit: 5ed48c7dc6bed153079bc2b23a1e0506841310d1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65982671"
---
# <a name="commit-work-transact-sql"></a>COMMIT WORK(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  트랜잭션의 끝을 표시합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
COMMIT [ WORK ]  
[ ; ]  
```  
  
## <a name="remarks"></a>Remarks  
 COMMIT TRANSACTION이 사용자 정의 트랜잭션 이름을 허용하는 것을 제외하면 이 문은 COMMIT TRANSACTION과 동일한 기능을 수행합니다. COMMIT 구문은 선택적인 키워드인 WORK의 지정 여부와 관계 없이 SQL-92와 호환이 가능합니다.  
  
## <a name="see-also"></a>참고 항목  
 [BEGIN DISTRIBUTED TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [BEGIN TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TransactION&#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [ROLLBACK TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [ROLLBACK WORK &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [SAVE TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/save-transaction-transact-sql.md)   
 [@@TRANCOUNT&#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  
