---
title: DB_ID(Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DB_ID_TSQL
- DB_ID
dev_langs:
- TSQL
helpviewer_keywords:
- viewing database ID numbers
- IDs [SQL Server], databases
- database IDs [SQL Server]
- identification numbers [SQL Server], databases
- displaying database ID numbers
- DB_ID function
ms.assetid: 7b3aef89-a6fd-4144-b468-bf87ebf381b8
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 152e471cf63efa09b0fc6dcb65acd28a191699b0
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="dbid-transact-sql"></a>DB_ID(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

데이터베이스 ID를 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DB_ID ( [ 'database_name' ] )   
```  
  
## <a name="arguments"></a>인수  
'*database_name*'  
해당 데이터베이스 ID를 반환하는 데 사용하는 데이터베이스 이름입니다. *database_name*은 **sysname**입니다. *database_name*을 생략하면 현재 데이터베이스 ID가 반환됩니다.
  
## <a name="return-types"></a>반환 형식
**int**
  
## <a name="permissions"></a>사용 권한  
**DB_ID**의 호출자가 데이터베이스의 소유자가 아니고 데이터베이스가 **master** 또는 **tempdb**가 아닐 경우 해당 행을 보려면 최소한 서버 수준의 ALTER ANY DATABASE 또는 VIEW ANY DATABASE 권한이 있거나 **master** 데이터베이스에서 CREATE DATABASE 권한이 있어야 합니다. 호출자가 연결된 데이터베이스는 항상 **sys.databases**에서 볼 수 있습니다.
  
> [!IMPORTANT]  
>  기본적으로 public 역할에는 모든 로그인이 데이터베이스 정보를 보도록 허용하는 VIEW ANY DATABASE 권한이 있습니다. 특정 로그인이 데이터베이스를 검색하지 못하게 하려면 public에서 VIEW ANY DATABASE 권한을 REVOKE하거나 개별 로그인에 대해 VIEW ANY DATABASE 권한을 DENY합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-returning-the-database-id-of-the-current-database"></a>1. 현재 데이터베이스의 데이터베이스 ID 반환  
다음 예에서는 현재 데이터베이스의 데이터베이스 ID를 반환합니다.
  
```sql
SELECT DB_ID() AS [Database ID];  
GO  
```  
  
### <a name="b-returning-the-database-id-of-a-specified-database"></a>2. 지정한 데이터베이스의 데이터베이스 ID 반환  
다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 데이터베이스 ID를 반환합니다.
  
```sql
SELECT DB_ID(N'AdventureWorks2008R2') AS [Database ID];  
GO  
```  
  
### <a name="c-using-dbid-to-specify-the-value-of-a-system-function-parameter"></a>3. DB_ID를 사용하여 시스템 함수 매개 변수 값 지정  
다음 예에서는 `DB_ID`를 사용하여 시스템 함수 `sys.dm_db_index_operational_stats`에서 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 데이터베이스 ID를 반환합니다. 함수는 데이터베이스 ID를 첫 번째 매개 변수로 사용합니다.
  
```sql
DECLARE @db_id int;  
DECLARE @object_id int;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.Person.Address');  
IF @db_id IS NULL   
  BEGIN;  
    PRINT N'Invalid database';  
  END;  
ELSE IF @object_id IS NULL  
  BEGIN;  
    PRINT N'Invalid object';  
  END;  
ELSE  
  BEGIN;  
    SELECT * FROM sys.dm_db_index_operational_stats(@db_id, @object_id, NULL, NULL);  
  END;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-return-the-id-of-the-current-database"></a>4. 현재 데이터베이스의 ID 반환  
다음 예에서는 현재 데이터베이스의 데이터베이스 ID를 반환합니다.
  
```sql
SELECT DB_ID();  
```  
  
### <a name="e-return-the-id-of-a-named-database"></a>5. 명명된 데이터베이스의 ID를 반환합니다.  
다음 예에서는 AdventureWorksDW2012 데이터베이스의 데이터베이스 ID를 반환합니다.
  
```sql
SELECT DB_ID('AdventureWorksPDW2012');  
```  
  
## <a name="see-also"></a>관련 항목:
[DB_NAME&#40;Transact-SQL&#41;](../../t-sql/functions/db-name-transact-sql.md)  
[메타데이터 함수&#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
[sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)
  
  

