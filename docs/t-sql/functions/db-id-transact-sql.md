---
description: DB_ID(Transact-SQL)
title: DB_ID(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/13/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6742ad9d5dae61ffcdbefe5d8f66bcbe8cd5078e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88310939"
---
# <a name="db_id-transact-sql"></a>DB_ID(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

이 함수는 지정된 데이터베이스의 데이터베이스 ID 번호를 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DB_ID ( [ 'database_name' ] )   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
'*database_name*'  
데이터베이스 ID 번호 `DB_ID`가 반환하는 데이터베이스의 이름입니다. `DB_ID`에 대한 호출이 *database_name*을 생략하는 경우 `DB_ID`는 현재 데이터베이스의 ID를 반환합니다.
  
## <a name="return-types"></a>반환 형식
**int**

## <a name="remarks"></a>설명
`DB_ID`는 Azure SQL Database에서 현재 데이터베이스의 데이터베이스 식별자를 반환하는 데만 사용할 수 있습니다. 지정된 데이터베이스 이름이 현재 데이터베이스가 아닌 경우 NULL이 반환됩니다.

> [!NOTE]
> Azure SQL Database와 함께 사용하는 경우 `DB_ID`는 **sys.databases**에서 `database_id` 쿼리의 경우와 동일한 결과를 반환하지 않을 수 있습니다. `DB_ID`의 호출자가 결과를 다른 **sys** 뷰와 비교하는 경우 **sys.databases**를 대신 쿼리해야 합니다.
  
## <a name="permissions"></a>사용 권한  
`DB_ID`의 호출자가 특정 비**마스터** 또는 비**tempdb** 데이터베이스를 소유하지 않는 경우 최소한 `ALTER ANY DATABASE` 또는 `VIEW ANY DATABASE` 서버 수준 사용 권한이 해당 `DB_ID` 행을 확인하는 데 필요합니다. **마스터** 데이터베이스의 경우 `DB_ID`는 최소한 `CREATE DATABASE` 사용 권한이 필요합니다. 호출자가 연결하는 데이터베이스는 항상 **sys.databases**에 나타납니다.
  
> [!IMPORTANT]  
>  기본적으로 public 역할에는 모든 로그인이 데이터베이스 정보를 보도록 허용하는 `VIEW ANY DATABASE` 권한이 있습니다. 로그인이 데이터베이스를 검색하지 않게 하려면 public에서 `VIEW ANY DATABASE` 권한을 `REVOKE`하거나 로그인에 대한 `DENY` 권한을 `VIEW ANY DATABASE`합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-returning-the-database-id-of-the-current-database"></a>A. 현재 데이터베이스의 데이터베이스 ID 반환  
이 예에서는 현재 데이터베이스의 데이터베이스 ID를 반환합니다.
  
```sql
SELECT DB_ID() AS [Database ID];  
GO  
```  
  
### <a name="b-returning-the-database-id-of-a-specified-database"></a>B. 지정한 데이터베이스의 데이터베이스 ID 반환  
이 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 데이터베이스 ID를 반환합니다.
  
```sql
SELECT DB_ID(N'AdventureWorks2008R2') AS [Database ID];  
GO  
```  
  
### <a name="c-using-db_id-to-specify-the-value-of-a-system-function-parameter"></a>C. DB_ID를 사용하여 시스템 함수 매개 변수 값 지정  
이 예에서는 `DB_ID`를 사용하여 시스템 함수 `sys.dm_db_index_operational_stats`에서 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 데이터베이스 ID를 반환합니다. 함수는 데이터베이스 ID를 첫 번째 매개 변수로 사용합니다.
  
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
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-return-the-id-of-the-current-database"></a>D. 현재 데이터베이스의 ID 반환  
이 예에서는 현재 데이터베이스의 데이터베이스 ID를 반환합니다.
  
```sql
SELECT DB_ID();  
```  
  
### <a name="e-return-the-id-of-a-named-database"></a>E. 명명된 데이터베이스의 ID를 반환합니다.  
이 예에서는 AdventureWorksDW2012 데이터베이스의 데이터베이스 ID를 반환합니다.
  
```sql
SELECT DB_ID('AdventureWorksPDW2012');  
```  
  
## <a name="see-also"></a>참고 항목
[DB_NAME&#40;Transact-SQL&#41;](../../t-sql/functions/db-name-transact-sql.md)  
[메타데이터 함수&#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
[sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)
  
  

