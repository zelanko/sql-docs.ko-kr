---
title: DBCC OPENTRAN(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC_OPENTRAN_TSQL
- DBCC OPENTRAN
- OPENTRAN_TSQL
- OPENTRAN
dev_langs:
- TSQL
helpviewer_keywords:
- status information [SQL Server], transactions
- transactions [SQL Server], status information
- DBCC OPENTRAN statement
- open transactions
- displaying transaction information
- checking open transactions
- oldest transactions [SQL Server]
ms.assetid: 63163843-226f-42d3-9e2c-b634fbf06943
author: pmasl
ms.author: umajay
ms.openlocfilehash: 7075de83b3f2d13d80d0eb08db1d780827eddeec
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68039086"
---
# <a name="dbcc-opentran-transact-sql"></a>DBCC OPENTRAN(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

DBCC OPENTRAN은 로그 잘림을 발생하지 못하게 할 수 있는 활성 트랜잭션을 식별하는 데 도움이 됩니다. DBCC OPENTRAN은 지정된 데이터베이스의 트랜잭션 로그 내에서 가장 오래된 활성 트랜잭션과 가장 오래된 분산 및 비분산 복제 트랜잭션에 대한 정보를 표시합니다. 로그에 존재하는 활성 트랜잭션이 있거나 데이터베이스에 복제 정보가 포함된 경우에만 결과가 표시됩니다. 로그에 활성 트랜잭션이 없을 경우 정보 메시지가 표시됩니다.
  
> [!NOTE]
>  DBCC OPENTRAN은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외의 게시자에 대해 지원되지 않습니다.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DBCC OPENTRAN   
[   
    ( [ database_name | database_id | 0 ] )   
    { [ WITH TABLERESULTS ]  
      [ , [ NO_INFOMSGS ] ]  
    }  
]   
```  
  
## <a name="arguments"></a>인수  
 *database_name* | *database_id*| 0  
 가장 오래된 트랜잭션 정보를 표시할 데이터베이스의 이름 또는 ID입니다. 아무 값도 지정하지 않거나 0을 지정하면 현재 데이터베이스가 사용됩니다. 데이터베이스 이름은 [식별자](../../relational-databases/databases/database-identifiers.md)에 대한 규칙을 준수해야 합니다.  
  
 TABLERESULTS  
 결과를 테이블에 로드될 수 있는 테이블 형식으로 표시합니다. 이 옵션을 사용하면 테이블에 삽입하여 비교할 수 있는 결과 테이블이 생성됩니다. 이 옵션을 지정하지 않으면 결과가 읽기 쉬운 형식으로 표시됩니다.  
  
 NO_INFOMSGS  
 모든 정보 메시지를 표시하지 않습니다.  
  
## <a name="remarks"></a>설명  
DBCC OPENTRAN을 사용하여 트랜잭션 로그 내에 열린 트랜잭션이 존재하는지 확인할 수 있습니다. BACKUP LOG 문을 사용할 때 열린 트랜잭션이 있으면 로그가 완전히 잘리지 않고 로그의 비활성 부분만 잘릴 수 있습니다. 열린 트랜잭션을 식별하려면 sp_who를 사용하여 시스템 프로세스 ID를 얻습니다.
  
## <a name="result-sets"></a>결과 집합  
열린 트랜잭션이 없을 경우 DBCC OPENTRAN은 다음 결과 집합을 반환합니다.
  
```sql
No active open transactions.  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>사용 권한  
**sysadmin** 고정 서버 역할의 멤버 또는 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.
  
## <a name="examples"></a>예  
### <a name="a-returning-the-oldest-active-transaction"></a>A. 가장 오래된 활성 트랜잭션 반환  
다음 예에서는 현재 데이터베이스에 대한 트랜잭션 정보를 얻습니다. 결과는 다를 수 있습니다.
  
```sql  
CREATE TABLE T1(Col1 int, Col2 char(3));  
GO  
BEGIN TRAN  
INSERT INTO T1 VALUES (101, 'abc');  
GO  
DBCC OPENTRAN;  
ROLLBACK TRAN;  
GO  
DROP TABLE T1;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Transaction information for database 'master'.
Oldest active transaction:
SPID (server process ID) : 52
UID (user ID) : -1
Name          : user_transaction
LSN           : (518:1576:1)
Start time    : Jun  1 2004  3:30:07:197PM
SID           : 0x010500000000000515000000a065cf7e784b9b5fe77c87709e611500
DBCC execution completed. If DBCC printed error messages, contact your system administrator.
```
  
> [!NOTE]  
>  "UID(사용자 ID)" 결과는 의미가 없으며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이후 버전에서는 제거될 예정입니다.  
  
### <a name="b-specifying-the-with-tableresults-option"></a>B. WITH TABLERESULTS 옵션 지정  
다음 예에서는 DBCC OPENTRAN 명령의 결과를 임시 테이블로 로드합니다.
  
```sql  
-- Create the temporary table to accept the results.  
CREATE TABLE #OpenTranStatus (  
   ActiveTransaction varchar(25),  
   Details sql_variant   
   );  
-- Execute the command, putting the results in the table.  
INSERT INTO #OpenTranStatus   
   EXEC ('DBCC OPENTRAN WITH TABLERESULTS, NO_INFOMSGS');  
  
-- Display the results.  
SELECT * FROM #OpenTranStatus;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
[BEGIN TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)  
[COMMIT TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)  
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DB_ID&#40;Transact-SQL&#41;](../../t-sql/functions/db-id-transact-sql.md)  
[ROLLBACK TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)
  
  
