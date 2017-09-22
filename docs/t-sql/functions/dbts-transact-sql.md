---
title: '@@DBTS (Transact SQL) | Microsoft Docs'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@DBTS_TSQL'
- '@@DBTS'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@DBTS function'
- timestamp data type
ms.assetid: 91842ddd-91c0-4445-a03f-116f6bc991d0
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 4a90150c55cdeb89788fdb86faf8aef8a1efdcd2
ms.contentlocale: ko-kr
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40dbts-transact-sql"></a>& #x 40; & &#40;x; DBTS (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

현재 데이터베이스의 현재 **timestamp** 데이터 형식 값을 반환합니다. 이 타임스탬프는 데이터베이스에서 고유합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```
@@DBTS  
```  
  
## <a name="return-types"></a>반환 형식
**varbinary**
  
## <a name="remarks"></a>주의  
@@DBTS 현재 데이터베이스의 타임 스탬프를 마지막으로 사용 된 값을 반환 합니다. 새 타임스탬프 값은 **timestamp** 열의 행이 삽입되거나 업데이트될 때 생성됩니다.
  
@@DBTS 함수 트랜잭션 격리 수준에 있는 변경 내용의 영향을 받지 않습니다.
  
## <a name="examples"></a>예  
다음 예에서는 현재 반환 **타임 스탬프** 에서 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스입니다.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT @@DBTS;  
```  
  
## <a name="see-also"></a>참고 항목
[구성 함수 &#40; Transact SQL &#41;](../../t-sql/functions/configuration-functions-transact-sql.md)  
[커서 동시성 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-cursors/properties/cursor-concurrency-odbc.md)  
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[MIN_ACTIVE_ROWVERSION &#40; Transact SQL &#41;](../../t-sql/functions/min-active-rowversion-transact-sql.md)
  
  

