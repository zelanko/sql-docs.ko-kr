---
title: '@@ROWCOUNT (Transact SQL) | Microsoft Docs'
ms.custom: 
ms.date: 08/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@ROWCOUNT_TSQL'
- '@@ROWCOUNT'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@ROWCOUNT function'
- number of rows affected by statement
- row affected by statements [SQL Server]
- statements [SQL Server], last statement
- counting rows
ms.assetid: 97a47998-81d9-4331-a244-9eb8b6fe4a56
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 411dc7eb628ddff52eb2f9426488e05860c9d279
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="x40x40rowcount-transact-sql"></a>& #x 40; & #x 40; 행 개수 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  최근 실행된 문의 영향을 받은 행 수를 반환합니다. 행 수가 2 십억 개 이상의 경우 사용 하 여 [ROWCOUNT_BIG](../../t-sql/functions/rowcount-big-transact-sql.md)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
@@ROWCOUNT  
```  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
## <a name="remarks"></a>주의  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]문은 @에서 값을 설정할 수@ROWCOUNT 다음과 같은 방법으로:  
  
-   설정@ROWCOUNT 행의 수에 영향을 받거나 읽은 합니다. 행은 클라이언트로 전송될 수도 그렇지 않을 수도 있습니다.  
  
-   유지@ROWCOUNT 이전 문 실행에서 합니다.  
  
-   재설정@ROWCOUNT 0으로 클라이언트에 값을 반환 하지는 않습니다.  
  
 항상 설정 단순한 할당을 수행 하는 문에 @@ROWCOUNT 값을 1로 합니다. 클라이언트에게 행은 보내지지 않습니다. 이러한 문의 예로: @ 설정*local_variable*, RETURN, READTEXT 그리고 없이 select getdate () 또는 SELECT 문은 쿼리 **'***일반 텍스트* **'**.  
  
 쿼리에서 할당 확인 또는 RETURN 쿼리 집합을 사용 하는 문에 @@ROWCOUNT 값 행의 수에 영향을 받거나 예를 들어 쿼리에 의해 읽은: @ 선택*local_variable* = c1 FROM t1.  
  
 데이터 조작 언어 (DML) 문 집합의 @@ROWCOUNT 값 쿼리에 의해 영향을 받는 행의 수 및 클라이언트에 값을 반환 합니다. DML 문은 클라이언트에게 행을 보내지 않을 수도 있습니다.  
  
 DECLARE CURSOR 및 설정 하는 FETCH는 @@ROWCOUNT 값을 1로 합니다.  
  
 EXECUTE 문은 이전 @ 유지@ROWCOUNT합니다.  
  
 문 사용 예: 설정 \<옵션 >, DEALLOCATE CURSOR, CLOSE CURSOR, BEGIN TRANSACTION 또는 COMMIT TRANSACTION는 ROWCOUNT 값은 0으로 다시 설정 합니다.  
  
 고유 하 게 컴파일된 저장된 프로시저는 이전 @ 유지@ROWCOUNT합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)]고유 하 게 컴파일된 저장된 프로시저 내의 문은 설정 하지 않으면@ROWCOUNT합니다. 자세한 내용은 참조 [Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `UPDATE` 문을 실행하고 `@@ROWCOUNT`를 사용하여 변경된 행이 있는지 확인합니다.  
  
```  
USE AdventureWorks2012;  
GO  
UPDATE HumanResources.Employee   
SET JobTitle = N'Executive'  
WHERE NationalIDNumber = 123456789  
IF @@ROWCOUNT = 0  
PRINT 'Warning: No rows were updated';  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [SET ROWCOUNT &#40; Transact SQL &#41;](../../t-sql/statements/set-rowcount-transact-sql.md)  
  
  

