---
title: DEALLOCATE (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: fb05fdd9da2f4f724976092bf027f5dde5edd412
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="deallocate-transact-sql"></a>DEALLOCATE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  커서 참조를 제거합니다. 커서를 구성 하는 데이터 구조에서 해제 하는 마지막 커서 참조가 할당 해제 된 경우 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DEALLOCATE { { [ GLOBAL ] cursor_name } | @cursor_variable_name }  
```  
  
## <a name="arguments"></a>인수  
 *cursor_name*  
 이미 선언된 커서의 이름입니다. 전역 및 로컬 커서 함께 존재 하는 경우 *cursor_name* 해당 이름으로 *cursor_name* GLOBAL이 지정 되지 않은 경우 GLOBAL이 지정 하는 경우 전역 커서와 로컬 커서를 참조 합니다.  
  
 @*cursor_variable_name*  
 이름인는 **커서** 변수입니다. @*cursor_variable_name* 형식 이어야 합니다 **커서**합니다.  
  
## <a name="remarks"></a>주의  
 커서에서 실행되는 문은 커서 이름이나 커서 변수를 사용하여 커서를 참조합니다. DEALLOCATE는 커서와 커서 이름 또는 커서 변수 간의 관계를 제거합니다. 커서를 참조하는 마지막 이름이나 변수의 경우 커서가 할당 해제되고 해당 커서에서 사용하던 모든 리소스가 해제됩니다. DEALLOCATE를 실행하면 인출의 격리를 보호하는 데 사용되는 스크롤 잠금이 해제됩니다. 그러나 해당 커서를 통한 현재 위치 업데이트를 포함하여 업데이트를 보호하는 트랜잭션 잠금은 트랜잭션이 종료될 때까지 유지됩니다.  
  
 DECLARE CURSOR 문은 커서 이름을 사용하여 커서를 할당하고 연결합니다.  
  
```  
DECLARE abc SCROLL CURSOR FOR  
SELECT * FROM Person.Person;  
```  
  
 커서에 연결된 커서 이름은 해당 커서를 할당 해제할 때까지 같은 범위(GLOBAL 또는 LOCAL)의 다른 커서에 사용할 수 없습니다.  
  
 커서 변수를 커서에 연결하려면 다음 중 한 가지 방법을 사용합니다.  
  
-   이름으로 커서를 커서 변수에 설정하는 SET 문을 사용합니다.  
  
    ```  
    DECLARE @MyCrsrRef CURSOR;  
    SET @MyCrsrRef = abc;  
    ```  
  
-   커서 이름을 정의하지 않고도 커서를 만들고 변수와 연결할 수 있습니다.  
  
    ```  
    DECLARE @MyCursor CURSOR;  
    SET @MyCursor = CURSOR LOCAL SCROLL FOR  
    SELECT * FROM Person.Person;  
    ```  
  
 DEALLOCATE @*cursor_variable_name* 문은 커서에 지정 된 변수 참조만 제거 합니다. 변수는 일괄 처리, 저장 프로시저, 트리거가 종료되어 범위를 벗어날 때까지 할당 해제되지 않습니다. DEALLOCATE @ 후*cursor_variable_name* 문, 변수와 연결할 수는 SET 문을 사용 하 여 다른 커서입니다.  
  
```  
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
  
## <a name="permissions"></a>Permissions  
 DEALLOCATE 권한은 기본적으로 모든 유효한 사용자에게 부여됩니다.  
  
## <a name="examples"></a>예  
 다음은 마지막 커서 이름이나 이를 참조하는 변수가 할당 해제될 때까지 커서가 유지되는 방법을 나타내는 스크립트입니다.  
  
```  
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
  
## <a name="see-also"></a>관련 항목:  
 [닫기 &#40; Transact SQL &#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [커서](../../relational-databases/cursors.md)   
 [DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [FETCH &#40; Transact SQL &#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [열기 &#40; Transact SQL &#41;](../../t-sql/language-elements/open-transact-sql.md)  
  
  
