---
title: '@@ROWCOUNT(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 08/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: bd62f7cd06f1d8d233b47d525ab05054d397b59a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083366"
---
# <a name="x40x40rowcount-transact-sql"></a>&#x40;&#x40;ROWCOUNT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  최근 실행된 문의 영향을 받은 행 수를 반환합니다. 행 수가 20억 개보다 많을 경우 [ROWCOUNT_BIG](../../t-sql/functions/rowcount-big-transact-sql.md)을 사용하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
@@ROWCOUNT  
```  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 다음과 같은 방법으로 @@ROWCOUNT의 값을 설정할 수 있습니다.  
  
-   @@ROWCOUNT을 영향을 받거나 읽은 행의 수로 설정합니다. 행은 클라이언트로 전송될 수도 그렇지 않을 수도 있습니다.  
  
-   이전에 실행한 문의 @@ROWCOUNT을 유지합니다.  
  
-   @@ROWCOUNT을 0으로 다시 설정하지만 클라이언트에게 값을 반환하지 않습니다.  
  
 단순한 할당을 수행하는 문은 항상 @@ROWCOUNT 값을 1로 설정합니다. 클라이언트에게 행은 보내지지 않습니다. 이러한 명령문의 예는 다음과 같습니다. SET @*local_variable*, RETURN, READTEXT가 있고 SELECT GETDATE() 또는 SELECT **'***제네릭 텍스트***'** 와 같이 쿼리 문이 없이 선택합니다.  
  
 쿼리에서 할당을 수행하거나 쿼리에 RETURN을 사용하는 문은 @@ROWCOUNT 값을 쿼리의 영향을 받거나 쿼리가 읽은 행 수로 설정합니다. 예: SELECT @*local_variable* = c1 FROM t1  
  
 DML(데이터 조작 언어) 문은 @@ROWCOUNT 값을 쿼리의 영향을 받는 행 수로 설정하고 해당 값을 클라이언트에 반환합니다. DML 문은 클라이언트에게 행을 보내지 않을 수도 있습니다.  
  
 DECLARE CURSOR와 FETCH는 @@ROWCOUNT 값을 1로 설정합니다.  
  
 EXECUTE 문은 이전 @@ROWCOUNT을 유지합니다.  
  
 USE, SET \<option>, DEALLOCATE CURSOR, CLOSE CURSOR, PRINT, RAISERROR, BEGIN TRANSACTION 또는 COMMIT TRANSACTION과 같은 문은 ROWCOUNT 값을 0으로 다시 설정합니다.  
  
 고유하게 컴파일된 저장 프로시저는 이전 @@ROWCOUNT을 보존합니다. 고유하게 컴파일된 저장 프로시저 내의 [!INCLUDE[tsql](../../includes/tsql-md.md)]문은 @@ROWCOUNT을 설정하지 않습니다. 자세한 내용은 [고유하게 컴파일된 저장 프로시저](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)를 참조하세요.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [시스템 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [SET ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/statements/set-rowcount-transact-sql.md)  
  
  
