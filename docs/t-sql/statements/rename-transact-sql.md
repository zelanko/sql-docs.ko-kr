---
title: RENAME(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2019
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.topic: language-reference
ms.assetid: 0907cfd9-33a6-4fa6-91da-7d6679fee878
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 624131beece632cffd13bde3d6ad378f67b3a340
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68141269"
---
# <a name="rename-transact-sql"></a>RENAME(Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]에서 사용자가 만든 테이블의 이름을 바꿉니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서 사용자가 만든 테이블 또는 데이터베이스의 이름을 바꿉니다.

> [!NOTE]
> [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]에서 데이터베이스의 이름을 바꾸려면 [ALTER DATABASE(Azure SQL Data Warehouse](alter-database-transact-sql.md?view=aps-pdw-2016-au7)를 사용합니다. Azure SQL Database에서 데이터베이스의 이름을 바꾸려면 [ALTER DATABASE(Azure SQL Database)](alter-database-transact-sql.md?view=azuresqldb-mi-current) 문을 사용합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터베이스의 이름을 바꾸려면 저장 프로시저 [sp_renamedb](../../relational-databases/system-stored-procedures/sp-renamedb-transact-sql.md)를 사용합니다.

## <a name="syntax"></a>구문

```
-- Syntax for Azure SQL Data Warehouse

-- Rename a table.
RENAME OBJECT [::] [ [ database_name . [schema_name ] ] . ] | [schema_name . ] ] table_name TO new_table_name
[;]

```

```
-- Syntax for Analytics Platform System

-- Rename a table
RENAME OBJECT [::] [ [ database_name . [ schema_name ] . ] | [ schema_name . ] ] table_name TO new_table_name
[;]

-- Rename a database
RENAME DATABASE [::] database_name TO new_database_name
[;]
```

## <a name="arguments"></a>인수

RENAME OBJECT [::] [ [*database_name* . [ *schema_name* ] . ] | [ *schema_name* . ] ]*table_name* TO *new_table_name*
**적용 대상:** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

사용자 정의 테이블의 이름을 변경합니다. 이름을 변경할 테이블을 하나, 둘 또는 세 부분으로 지정합니다. 새 테이블 *new_table_name*을 한 부분 이름으로 지정합니다.

RENAME DATABASE [::] [ *database_name* TO *new_database_name*
**적용 대상:** [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

*database_name*에서 사용자 정의 데이터베이스의 이름을 *new_database_name*으로 변경합니다. 데이터베이스 이름은 이러한 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]예약된 데이터베이스 이름으로 바꿀 수 없습니다.

- master
- model
- msdb
- tempdb
- pdwtempdb1
- pdwtempdb2
- DWConfiguration
- DWDiagnostics
- DWQueue

## <a name="permissions"></a>사용 권한

이 명령을 실행하려면 이 권한이 필요합니다.

- 테이블에 대한 **ALTER** 권한

## <a name="limitations-and-restrictions"></a>제한 사항

### <a name="cannot-rename-an-external-table-indexes-or-views"></a>외부 테이블, 인덱스 또는 뷰 이름을 바꿀 수 없음

외부 테이블, 인덱스 또는 보기 이름을 바꿀 수 없습니다. 이름을 바꾸는 대신 외부 테이블, 인덱스 또는 뷰를 삭제한 다음, 새 이름으로 다시 만들 수 있습니다.

### <a name="cannot-rename-a-table-in-use"></a>사용 중인 테이블 이름을 바꿀 수 없음

사용 중일 때는 테이블 또는 데이터베이스 이름을 바꿀 수 없습니다. 테이블 이름을 변경하려면 테이블에 대해 배타적 잠금이 필요합니다. 테이블이 사용 중인 경우 테이블을 사용 중인 세션을 종료해야 합니다. KILL 명령을 사용하여 세션을 종료할 수 있습니다. 세션이 종료될 때 커밋되지 않은 모든 작업은 롤백될 수 있으므로 KILL은 신중하게 사용합니다. SQL Data Warehouse의 세션 앞에 ‘SID’를 붙입니다. KILL 명령을 호출할 때 'SID'와 세션 수를 포함합니다. 이 예제에서는 활성 또는 유휴 세션의 목록을 본 다음, ‘SID1234’ 세션을 종료합니다.

### <a name="views-are-not-updated"></a>뷰는 업데이트되지 않습니다.

데이터베이스의 이름을 바꾸면 이전 데이터베이스 이름을 사용하는 모든 뷰가 무효화됩니다. 이 동작은 데이터베이스의 내부 및 외부 모두에 대한 보기에 적용됩니다. 예를 들어 판매 데이터베이스의 이름을 바꾸면 `SELECT * FROM Sales.dbo.table1`을 포함하는 뷰는 유효하지 않게 됩니다. 이 문제를 해결하려면 보기에서 세 부분으로 된 이름을 사용하지 않거나, 새 데이터베이스 이름을 참조하도록 보기를 업데이트합니다.

테이블의 이름을 바꾸면 뷰는 새 테이블 이름을 참조하도록 업데이트되지 않습니다. 이전 테이블 이름을 참조하는 데이터베이스의 내부 또는 외부의 각 뷰는 유효하지 않게 됩니다. 이 문제를 해결하기 위해 새 테이블 이름을 참조하도록 각 보기를 업데이트할 수 있습니다.

## <a name="locking"></a>잠금

테이블 이름 바꾸기는 DATABASE 개체에 대한 공유 잠금, SCHEMA 개체에 대한 공유 잠금 및 테이블에 대한 배타적 잠금을 사용합니다.

## <a name="examples"></a>예

### <a name="a-rename-a-database"></a>A. 데이터베이스 이름 바꾸기

**적용 대상:** [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]만 해당

이 예제에서는 사용자 정의 데이터베이스 AdWorks의 이름을 AdWorks2로 바꿉니다.

```sql
-- Rename the user defined database AdWorks
RENAME DATABASE AdWorks to AdWorks2;

```

 테이블 이름을 바꿀 때 해당 테이블과 연결된 모든 개체 및 속성은 새 테이블 이름을 참조하도록 업데이트됩니다. 예를 들어, 테이블 정의, 인덱스, 제약 조건 및 권한이 업데이트됩니다. 뷰는 업데이트되지 않습니다.

### <a name="b-rename-a-table"></a>B. 테이블 이름 바꾸기

**적용 대상:** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

이 예제에서는 Customer 테이블의 이름을 Customer1로 바꿉니다.

```sql
-- Rename the customer table
RENAME OBJECT Customer TO Customer1;

RENAME OBJECT mydb.dbo.Customer TO Customer1;
```

테이블 이름을 바꿀 때 해당 테이블과 연결된 모든 개체 및 속성은 새 테이블 이름을 참조하도록 업데이트됩니다. 예를 들어, 테이블 정의, 인덱스, 제약 조건 및 권한이 업데이트됩니다. 뷰는 업데이트되지 않습니다.

### <a name="c-move-a-table-to-a-different-schema"></a>C. 다른 스키마로 테이블 이동

**적용 대상:** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

의도를 다른 스키마로 이동하려는 경우 [ALTER SCHEMA](../../t-sql/statements/alter-schema-transact-sql.md)를 사용합니다. 예를 들어 다음 명령문은 테이블 항목을 제품 스키마에서 dbo 스키마로 이동시킵니다.

```sql
ALTER SCHEMA dbo TRANSFER OBJECT::product.item;
```

### <a name="d-terminate-sessions-before-renaming-a-table"></a>D. 테이블 이름 변경 전에 세션 종료

**적용 대상:** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

테이블은 사용하는 동안에는 이름을 바꿀 수 없습니다. 테이블의 이름을 변경하려면 테이블에 대해 배타적 잠금이 필요합니다. 테이블이 사용 중인 경우 테이블을 사용 중인 세션을 종료해야 합니다. KILL 명령을 사용하여 세션을 종료할 수 있습니다. 세션이 종료될 때 커밋되지 않은 모든 작업은 롤백될 수 있으므로 KILL은 신중하게 사용합니다. SQL Data Warehouse의 세션 앞에 ‘SID’를 붙입니다. KILL 명령을 호출할 때 'SID'와 세션 수를 포함해야 합니다. 이 예제에서는 활성 또는 유휴 세션의 목록을 본 다음, ‘SID1234’ 세션을 종료합니다.

```sql
-- View a list of the current sessions
SELECT session_id, login_name, status
FROM sys.dm_pdw_exec_sessions
WHERE status='Active' OR status='Idle';

-- Terminate a session using the session_id.
KILL 'SID1234';
```