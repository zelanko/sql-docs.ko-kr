---
title: SET IMPLICIT_TRANSACTIONS(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- IMPLICIT_TRANSACTIONS
- SET IMPLICIT_TRANSACTIONS
- IMPLICIT_TRANSACTIONS_TSQL
- SET_IMPLICIT_TRANSACTIONS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- implicit transactions
- transactions [SQL Server], implicit
- connections [SQL Server], implicit transaction mode
- SET IMPLICIT_TRANSACTIONS statement
- IMPLICIT_TRANSACTIONS option
ms.assetid: a300ac43-e4c0-4329-8b79-a1a05e63370a
caps.latest.revision: 45
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5ca98e975b031aa1bd9a20033e01a8c406c4eb89
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="set-implicittransactions-transact-sql"></a>SET IMPLICIT_TRANSACTIONS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  연결에 대해 BEGIN TRANSACTION 모드를 암시적(*implicit*)으로 설정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
SET IMPLICIT_TRANSACTIONS { ON | OFF }  
```  
  
## <a name="remarks"></a>Remarks  
 ON이면 시스템이 암시적(*implicit*) 트랜잭션 모드입니다. 즉, @@TRANCOUNT = 0이면 다음 Transact-SQL 문 중 하나가 새 트랜잭션을 시작합니다. 보이지 않는 BEGIN TRANSACTION이 먼저 실행되는 것과 같습니다.  
  
||||  
|-|-|-|  
|ALTER TABLE|FETCH|REVOKE|  
|BEGIN TRANSACTION|GRANT|SELECT(아래 예외 참조)|  
|CREATE|INSERT|TRUNCATE TABLE|  
|Delete|OPEN|UPDATE|  
|DROP|의 인스턴스에 액세스할 때마다 SQL Server 로그인을 제공할 필요가 없습니다.|의 인스턴스에 액세스할 때마다 SQL Server 로그인을 제공할 필요가 없습니다.|  
  
 OFF이면 앞의 T-SQL 문은 보이지 않는 BEGIN TRANSACTION 및 보이지 않는 COMMIT TRANSACTION 문으로 제한됩니다. OFF이면 트랜잭션 모드가 자동 커밋(*autocommit*)이라고 합니다. T-SQL 코드가 BEGIN TRANSACTION을 눈에 보이게 발급하면 트랜잭션 모드가 명시적(*explicit*)이라고 합니다.  
  
 다음은 명확한 이해가 필요한 몇 가지 요점입니다.  
  
-   트랜잭션 모드가 암시적일 때 @@trancount > 0이면 보이지 않는 BEGIN TRANSACTION이 발급되지 않습니다. 하지만 명시적인 BEGIN TRANSACTION 문은 @@TRANCOUNT를 여전히 증가시킵니다.  
  
-   INSERT 문 및 작업 단위의 다른 항목이 완료되면 @@TRANCOUNT가 0으로 감소될 때까지 COMMIT TRANSACTION 문을 실행해야 합니다. 또는 ROLLBACK TRANSACTION을 하나 실행할 수 있습니다.  
  
-   테이블에서 SELECT를 수행하지 않는 SELECT 문은 암시적 트랜잭션을 시작하지 않습니다. 예를 들어, `SELECT GETDATE();` 또는 `SELECT 1, 'ABC';`에는 트랜잭션이 필요하지 않습니다.  
  
-   ANSI 기본값으로 인해 암시적 트랜잭션이 갑자기 ON으로 설정될 수 있습니다. 자세한 내용은 [SET ANSI_DEFAULTS&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)를 참조하세요.  
  
     IMPLICIT_TRANSACTIONS ON은 많이 사용되지 않습니다. IMPLICIT_TRANSACTIONS가 ON인 대부분의 경우는 SET ANSI_DEFAULTS ON이 선택되었기 때문입니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 둘 다 연결될 때 IMPLICIT_TRANSACTIONS 옵션을 OFF로 자동으로 설정합니다. SET IMPLICIT_TRANSACTIONS는 SQLClient 관리 공급자와 연결하는 경우와 HTTP 엔드포인트를 통해 SOAP 요청을 받는 경우에는 OFF로 기본 설정됩니다.  
  
 IMPLICIT_TRANSACTION의 현재 설정을 보려면 다음 쿼리를 실행합니다.  
  
```  
DECLARE @IMPLICIT_TRANSACTIONS VARCHAR(3) = 'OFF';  
IF ( (2 & @@OPTIONS) = 2 ) SET @IMPLICIT_TRANSACTIONS = 'ON';  
SELECT @IMPLICIT_TRANSACTIONS AS IMPLICIT_TRANSACTIONS;  
```  
  
## <a name="examples"></a>예  
 다음 Transact-SQL 스크립트는 몇 가지 다른 테스트 사례를 실행합니다. 각 테스트 사례의 세부 동작과 결과를 보여주는 텍스트 출력도 제공됩니다.  
  
```sql  
-- Transact-SQL.  
go  
-- Preparations.  
SET NOCOUNT ON;  
SET IMPLICIT_TRANSACTIONS OFF;  
go  
WHILE (@@TranCount > 0) COMMIT TRANSACTION;  
go  
IF (OBJECT_ID(N'dbo.t1',N'U') IS NOT NULL) DROP TABLE dbo.t1;  
go  
CREATE table dbo.t1 (a int);  
go  
  
PRINT N'-------- [Test A] ---- OFF ----';  
PRINT N'[A.01] Now, SET IMPLICIT_TRANSACTIONS OFF.';  
PRINT N'[A.02] @@TranCount, at start, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
SET IMPLICIT_TRANSACTIONS OFF;  
go  
INSERT INTO dbo.t1 VALUES (11);  
INSERT INTO dbo.t1 VALUES (12);  
PRINT N'[A.03] @@TranCount, after INSERTs, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
go  
  
PRINT N' ';  
PRINT N'-------- [Test B] ---- ON ----';  
PRINT N'[B.01] Now, SET IMPLICIT_TRANSACTIONS ON.';  
PRINT N'[B.02] @@TranCount, at start, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
SET IMPLICIT_TRANSACTIONS ON;  
go  
INSERT INTO dbo.t1 VALUES (21);  
INSERT INTO dbo.t1 VALUES (22);  
PRINT N'[B.03] @@TranCount, after INSERTs, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
go  
COMMIT TRANSACTION;  
PRINT N'[B.04] @@TranCount, after COMMIT, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
go  
  
PRINT N' ';  
PRINT N'-------- [Test C] ---- ON, then BEGIN TRAN ----';  
PRINT N'[C.01] Now, SET IMPLICIT_TRANSACTIONS ON.';  
PRINT N'[C.02] @@TranCount, at start, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
SET IMPLICIT_TRANSACTIONS ON;  
go  
BEGIN TRANSACTION;  
INSERT INTO dbo.t1 VALUES (31);  
INSERT INTO dbo.t1 VALUES (32);  
PRINT N'[C.03] @@TranCount, after INSERTs, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
go  
COMMIT TRANSACTION;  
PRINT N'[C.04] @@TranCount, after a COMMIT, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
COMMIT TRANSACTION;  
PRINT N'[C.05] @@TranCount, after another COMMIT, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
go  
  
PRINT N' ';  
PRINT N'-------- [Test D] ---- ON, INSERT, BEGIN TRAN, INSERT ----';  
PRINT N'[D.01] Now, SET IMPLICIT_TRANSACTIONS ON.';  
PRINT N'[D.02] @@TranCount, at start, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
SET IMPLICIT_TRANSACTIONS ON;  
go  
INSERT INTO dbo.t1 VALUES (41);  
BEGIN TRANSACTION;  
INSERT INTO dbo.t1 VALUES (42);  
PRINT N'[D.03] @@TranCount, after INSERTs, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
go  
COMMIT TRANSACTION;  
PRINT N'[D.04] @@TranCount, after INSERTs, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
COMMIT TRANSACTION;  
PRINT N'[D.05] @@TranCount, after INSERTs, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
go  
  
-- Clean up.  
SET IMPLICIT_TRANSACTIONS OFF;  
go  
WHILE (@@TranCount > 0) COMMIT TRANSACTION;  
go  
DROP TABLE dbo.t1;  
go  
```  
  
 다음은 이전 Transact-SQL 스크립트의 텍스트 출력입니다.  
  
```sql  
-- Text output from Transact-SQL:  
  
-------- [Test A] ---- OFF ----  
[A.01] Now, SET IMPLICIT_TRANSACTIONS OFF.  
[A.02] @@TranCount, at start, == 0  
[A.03] @@TranCount, after INSERTs, == 0  
  
-------- [Test B] ---- ON ----  
[B.01] Now, SET IMPLICIT_TRANSACTIONS ON.  
[B.02] @@TranCount, at start, == 0  
[B.03] @@TranCount, after INSERTs, == 1  
[B.04] @@TranCount, after COMMIT, == 0  
  
-------- [Test C] ---- ON, then BEGIN TRAN ----  
[C.01] Now, SET IMPLICIT_TRANSACTIONS ON.  
[C.02] @@TranCount, at start, == 0  
[C.03] @@TranCount, after INSERTs, == 2  
[C.04] @@TranCount, after a COMMIT, == 1  
[C.05] @@TranCount, after another COMMIT, == 0  
  
-------- [Test D] ---- ON, INSERT, BEGIN TRAN, INSERT ----  
[D.01] Now, SET IMPLICIT_TRANSACTIONS ON.  
[D.02] @@TranCount, at start, == 0  
[D.03] @@TranCount, after INSERTs, == 2  
[D.04] @@TranCount, after INSERTs, == 1  
[D.05] @@TranCount, after INSERTs, == 0  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [BEGIN TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [DROP TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [FETCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [GRANT&#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [OPEN&#40;Transact-SQL&#41;](../../t-sql/language-elements/open-transact-sql.md)   
 [REVOKE&#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)   
 [@@TRANCOUNT&#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)   
 [TRUNCATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/truncate-table-transact-sql.md)   
 [UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  
  
  
