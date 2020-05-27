---
title: DEALLOCATE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DEALLOCATE
- DEALLOCATE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- locking [SQL Server], cursors
- DEALLOCATE statement
- deallocations [SQL Server]
- deleting cursor references
- removing cursor references
ms.assetid: c75cf73d-0268-4c57-973d-b8a84ff801fa
author: rothja
ms.author: jroth
ms.openlocfilehash: 92153155be5761e804c6d62cece4d392b40a1412
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67894896"
---
# <a name="deallocate-transact-sql"></a>DEALLOCATE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  커서 참조를 제거합니다. 마지막 커서 참조가 할당 취소되면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 커서를 구성하는 데이터 구조의 할당을 취소합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
DEALLOCATE { { [ GLOBAL ] cursor_name } | @cursor_variable_name }  
```  
  
## <a name="arguments"></a>인수  
 *cursor_name*  
 이미 선언된 커서의 이름입니다. 글로벌 커서와 지역 커서에 모두 해당 이름으로 *cursor_name*이 있는 경우 `GLOBAL`이 지정되면 *cursor_name*이 글로벌 커서를 참조하고, `GLOBAL`이 지정되지 않으면 지역 커서를 참조합니다.  
  
 @*cursor_variable_name*  
 **cursor** 변수의 이름입니다. @*cursor_variable_name*은 **cursor** 형식이어야 합니다.  
  
## <a name="remarks"></a>설명  
커서에서 실행되는 문은 커서 이름이나 커서 변수를 사용하여 커서를 참조합니다. `DEALLOCATE`는 커서와 커서 이름 또는 커서 변수 간의 연결을 제거합니다. 커서를 참조하는 마지막 이름이나 변수의 경우 커서가 할당 해제되고 해당 커서에서 사용하던 모든 리소스가 해제됩니다. `DEALLOCATE`를 실행하면 인출의 격리를 보호하는 데 사용되는 스크롤 잠금이 해제됩니다. 그러나 해당 커서를 통한 현재 위치 업데이트를 포함하여 업데이트를 보호하는 트랜잭션 잠금은 트랜잭션이 종료될 때까지 유지됩니다.  
  
`DECLARE CURSOR` 문은 커서 이름을 사용하여 커서를 할당하고 연결합니다.  
  
```sql  
DECLARE abc SCROLL CURSOR FOR  
SELECT * FROM Person.Person;  
```  
  
커서 이름이 커서와 연결된 후 이 커서를 할당 해제할 때까지 해당 이름은 같은 범위(글로벌 또는 지역)의 다른 커서에 사용할 수 없습니다.  
  
 커서 변수를 커서에 연결하려면 다음 중 한 가지 방법을 사용합니다.  
  
-   이름으로 커서를 커서 변수에 설정하는 `SET` 문을 사용합니다.  
  
    ```sql  
    DECLARE @MyCrsrRef CURSOR;  
    SET @MyCrsrRef = abc;  
    ```  
  
-   커서 이름을 정의하지 않고도 커서를 만들고 변수와 연결할 수 있습니다.  
  
    ```sql  
    DECLARE @MyCursor CURSOR;  
    SET @MyCursor = CURSOR LOCAL SCROLL FOR  
    SELECT * FROM Person.Person;  
    ```  
  
 `DEALLOCATE <@cursor_variable_name>` 문은 커서에 대해 명명된 변수의 참조만 제거합니다. 변수는 일괄 처리, 저장 프로시저, 트리거가 종료되어 범위를 벗어날 때까지 할당 해제되지 않습니다. `DEALLOCATE <@cursor_variable_name>` 문을 실행한 후 SET 문을 사용하여 변수를 다른 커서와 연결할 수 있습니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
  
DECLARE @MyCursor CURSOR;  
SET @MyCursor = CURSOR LOCAL SCROLL FOR  
    SELECT * FROM Sales.SalesPerson;  
  
DEALLOCATE @MyCursor;  
  
SET @MyCursor = CURSOR LOCAL SCROLL FOR  
    SELECT * FROM Sales.SalesTerritory;  
GO  
```  
  
커서 변수는 명시적으로 할당 해제할 필요가 없으며 범위를 벗어나면 암시적으로 할당 해제됩니다.  
  
## <a name="permissions"></a>사용 권한  
 `DEALLOCATE` 권한은 기본적으로 모든 유효한 사용자에게 부여됩니다.  
  
## <a name="examples"></a>예  
 다음은 마지막 커서 이름이나 이를 참조하는 변수가 할당 해제될 때까지 커서가 유지되는 방법을 나타내는 스크립트입니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
-- Create and open a global named cursor that  
-- is visible outside the batch.  
DECLARE abc CURSOR GLOBAL SCROLL FOR  
    SELECT * FROM Sales.SalesPerson;  
OPEN abc;  
GO  
-- Reference the named cursor with a cursor variable.  
DECLARE @MyCrsrRef1 CURSOR;  
SET @MyCrsrRef1 = abc;  
-- Now deallocate the cursor reference.  
DEALLOCATE @MyCrsrRef1;  
-- Cursor abc still exists.  
FETCH NEXT FROM abc;  
GO  
-- Reference the named cursor again.  
DECLARE @MyCrsrRef2 CURSOR;  
SET @MyCrsrRef2 = abc;  
-- Now deallocate cursor name abc.  
DEALLOCATE abc;  
-- Cursor still exists, referenced by @MyCrsrRef2.  
FETCH NEXT FROM @MyCrsrRef2;  
-- Cursor finally is deallocated when last referencing  
-- variable goes out of scope at the end of the batch.  
GO  
-- Create an unnamed cursor.  
DECLARE @MyCursor CURSOR;  
SET @MyCursor = CURSOR LOCAL SCROLL FOR  
SELECT * FROM Sales.SalesTerritory;  
-- The following statement deallocates the cursor  
-- because no other variables reference it.  
DEALLOCATE @MyCursor;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [CLOSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [커서](../../relational-databases/cursors.md)   
 [DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [FETCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [OPEN&#40;Transact-SQL&#41;](../../t-sql/language-elements/open-transact-sql.md)  
  
  
