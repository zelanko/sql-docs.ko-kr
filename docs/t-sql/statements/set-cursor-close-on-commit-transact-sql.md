---
description: SET CURSOR_CLOSE_ON_COMMIT(Transact-SQL)
title: SET CURSOR_CLOSE_ON_COMMIT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CURSOR_CLOSE_ON_COMMIT
- SET CURSOR_CLOSE_ON_COMMIT
- CURSOR_CLOSE_ON_COMMIT_TSQL
- SET_CURSOR_CLOSE_ON_COMMIT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CURSOR_CLOSE_ON_COMMIT option
- transactions [SQL Server], cursors
- closing cursors
- cursors [SQL Server], closing
- SET CURSOR_CLOSE_ON_COMMIT statement
ms.assetid: 7b976154-98ce-4a06-bbae-7e59c34211f7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 320b3ed7656ea7862e2f1d90818930646c865a01
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541255"
---
# <a name="set-cursor_close_on_commit-transact-sql"></a>SET CURSOR_CLOSE_ON_COMMIT(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)] COMMIT TRANSACTION 문의 동작을 제어합니다. 이 설정의 기본값은 OFF입니다. 즉, 트랜잭션을 커밋할 때 서버가 커서를 닫지 않습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
  
SET CURSOR_CLOSE_ON_COMMIT { ON | OFF }  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="remarks"></a>설명
 CURSOR_CLOSE_ON_COMMIT 옵션이 ON이면 ISO에 따라 커밋 또는 롤백될 때 열려 있는 모든 커서를 닫습니다. SET CURSOR_CLOSE_ON_COMMIT 옵션이 OFF이면 트랜잭션이 커밋될 때 커서가 닫히지 않습니다.  
  
> [!NOTE]  
>  SET CURSOR_CLOSE_ON_COMMIT 옵션이 ON이면 롤백이 SAVE TRANSACTION 문에서 savepoint_name에 적용될 때 롤백 시 열려 있는 커서를 닫지 않습니다.  
  
 SET CURSOR_CLOSE_ON_COMMIT 옵션이 OFF이면 ROLLBACK 문은 완전히 채워지지 않은 열려 있는 비동기 커서만 닫습니다. 수정 후 연 STATIC 또는 INSENSITIVE 커서는 수정 사항이 롤백되는 경우의 데이터 상태를 더 이상 반영하지 않습니다.  
  
 SET CURSOR_CLOSE_ON_COMMIT 옵션은 CURSOR_CLOSE_ON_COMMIT 데이터베이스 옵션과 같은 동작을 제어합니다. CURSOR_CLOSE_ON_COMMIT 옵션을 ON이나 OFF로 설정하면 이 설정이 연결에 사용됩니다. SET CURSOR_CLOSE_ON_COMMIT 옵션을 지정하지 않으면 **sys.databases** 카탈로그 뷰의 **is_cursor_close_on_commit_on** 열 값이 적용됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 Native Client OLE DB 공급자[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 둘 다 연결될 때 CURSOR_CLOSE_ON_COMMIT 옵션을 OFF로 설정합니다. DB-Library는 CURSOR_CLOSE_ON_COMMIT 값을 자동으로 설정하지 않습니다.  
  
 SET ANSI_DEFAULTS 옵션이 ON이면 SET CURSOR_CLOSE_ON_COMMIT 옵션이 설정됩니다.  
  
 SET CURSOR_CLOSE_ON_COMMIT 옵션은 실행 시간 또는 런타임에 설정되며, 구문 분석 시에는 설정되지 않습니다.  
  
 이 설정에 대한 현재 설정을 보려면 다음 쿼리를 실행합니다.  
  
```sql
DECLARE @CURSOR_CLOSE VARCHAR(3) = 'OFF';  
IF ( (4 & @@OPTIONS) = 4 ) SET @CURSOR_CLOSE = 'ON';  
SELECT @CURSOR_CLOSE AS CURSOR_CLOSE_ON_COMMIT;  
```  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 트랜잭션에서 커서를 정의하고 트랜잭션이 커밋된 후 커서 사용을 시도합니다.  
  
```sql
-- SET CURSOR_CLOSE_ON_COMMIT  
-------------------------------------------------------------------------------  
SET NOCOUNT ON;  
  
CREATE TABLE t1 (a INT);  
GO   
  
INSERT INTO t1   
VALUES (1), (2);  
GO  
  
PRINT '-- SET CURSOR_CLOSE_ON_COMMIT ON';  
GO  
SET CURSOR_CLOSE_ON_COMMIT ON;  
GO  
PRINT '-- BEGIN TRAN';  
BEGIN TRAN;  
PRINT '-- Declare and open cursor';  
DECLARE testcursor CURSOR FOR  
    SELECT a FROM t1;  
OPEN testcursor;  
PRINT '-- Commit tran';  
COMMIT TRAN;  
PRINT '-- Try to use cursor';  
FETCH NEXT FROM testcursor;  
CLOSE testcursor;  
DEALLOCATE testcursor;  
GO  
PRINT '-- SET CURSOR_CLOSE_ON_COMMIT OFF';  
GO  
SET CURSOR_CLOSE_ON_COMMIT OFF;  
GO  
PRINT '-- BEGIN TRAN';  
BEGIN TRAN;  
PRINT '-- Declare and open cursor';  
DECLARE testcursor CURSOR FOR  
    SELECT a FROM t1;  
OPEN testcursor;  
PRINT '-- Commit tran';  
COMMIT TRAN;  
PRINT '-- Try to use cursor';  
FETCH NEXT FROM testcursor;  
CLOSE testcursor;  
DEALLOCATE testcursor;  
GO  
DROP TABLE t1;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER DATABASE &#40;Transact-SQL &#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [BEGIN TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [CLOSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [COMMIT TransactION&#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [ROLLBACK TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)  
  
  
