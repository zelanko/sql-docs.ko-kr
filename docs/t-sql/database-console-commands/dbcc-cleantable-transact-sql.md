---
title: DBCC CLEANTABLE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CLEANTABLE_TSQL
- DBCC_CLEANTABLE_TSQL
- DBCC CLEANTABLE
- CLEANTABLE
dev_langs:
- TSQL
helpviewer_keywords:
- disk space [SQL Server], reclaiming
- reclaiming space
- reallocating space
- removing columns
- DBCC CLEANTABLE statement
- space [SQL Server], reclaiming
- deleting columns
- dropping columns
ms.assetid: 0dbbc956-15b1-427b-812c-618a044d07fa
author: pmasl
ms.author: umajay
ms.openlocfilehash: 8cb3c1c0eba5c39083b6a6b39b4040639909808c
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68101972"
---
# <a name="dbcc-cleantable-transact-sql"></a>DBCC CLEANTABLE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
테이블 또는 인덱싱된 뷰의 삭제된 가변 길이 열에서 공간을 반환합니다.
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
  
DBCC CLEANTABLE  
(  
    { database_name | database_id | 0 }  
    , { table_name | table_id | view_name | view_id }  
    [ , batch_size ]  
)  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>인수  
 *database_name* | *database_id* | 0  
 정리될 테이블이 속한 데이터베이스입니다. 0을 지정하면 현재 데이터베이스가 사용됩니다. 데이터베이스 이름은 반드시 [식별자](../../relational-databases/databases/database-identifiers.md)에 적용되는 규칙을 준수해야 합니다.  
  
 *table_name* | *table_id* | *view_name*| *view_id*  
 정리될 테이블이나 인덱싱된 뷰입니다.  
  
 *batch_size*  
 트랜잭션당 처리되는 행 수입니다. 값을 지정하지 않거나 0을 지정하면 문은 한 트랜잭션에서 전체 테이블을 처리합니다.  
  
 WITH NO_INFOMSGS  
 모든 정보 메시지를 표시하지 않습니다.  
  
## <a name="remarks"></a>설명  
DBCC CLEANTABLE은 가변 길이 열이 삭제된 후에 공간을 반환합니다. 가변 길이 열은 **varchar**, **nvarchar**, **varchar(max)** , **nvarchar(max)** , **varbinary**, **varbinary(max)** , **text**, **ntext**, **image**, **sql_variant** 및 **xml** 데이터 형식 중 하나일 수 있습니다. 이 명령은 고정 길이 열이 삭제된 후에는 공간을 반환하지 않습니다.
삭제된 열이 행 내부에 저장된 경우 DBCC CLEANTABLE은 테이블의 IN_ROW_DATA 할당 단위에서 공간을 반환합니다. 열이 행 외부에 저장된 경우에는 삭제된 열의 데이터 형식에 따라 ROW_OVERFLOW_DATA 또는 LOB_DATA 할당 단위에서 공간이 반환됩니다. ROW_OVERFLOW_DATA 또는 LOB_DATA 페이지에서 공간을 반환하면 빈 페이지가 되고 DBCC CLEANTABLE이 해당 페이지를 제거합니다.
DBCC CLEANTABLE은 하나 이상의 트랜잭션으로 실행됩니다. 일괄 처리 크기를 지정하지 않으면 명령은 한 트랜잭션에서 전체 테이블을 처리하며 이 테이블은 작업하는 동안 배타적으로 잠깁니다. 일부 대형 테이블의 경우 한 트랜잭션의 길이와 필요한 로그 공간이 너무 많을 수도 있습니다. 일괄 처리 크기를 지정하면 이 명령은 각기 지정한 행 수를 포함한 일련의 트랜잭션으로 실행됩니다. 다른 트랜잭션 내의 트랜잭션으로 DBCC CLEANTABLE을 실행할 수는 없습니다.
이 작업은 모두 기록됩니다.
DBCC CLEANTABLE은 시스템 테이블, 임시 테이블 또는 테이블의 xVelocity 메모리 최적화 columnstore 인덱스 부분에 대해서는 사용할 수 없습니다.
  
## <a name="best-practices"></a>모범 사례  
일상적인 유지 관리 태스크로 DBCC CLEANTABLE을 실행하지 않도록 합니다. 대신 테이블 또는 인덱싱된 뷰의 가변 길이 열을 상당 부분 변경한 후에 DBCC CLEANTABLE을 사용하며 사용하지 않은 공간을 즉시 반환해야 합니다. 또는 테이블이나 뷰에 인덱스를 다시 작성할 수 있습니다. 그러나 이렇게 하려면 더 많은 리소스가 필요합니다.
  
## <a name="result-sets"></a>결과 집합  
DBCC CLEANTABLE은 다음을 반환합니다.
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>사용 권한  
 호출자는 테이블 또는 인덱싱된 뷰를 소유하거나, **sysadmin** 고정 서버 역할, **db_owner** 고정 데이터베이스 역할 또는 **db_ddladmin** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
## <a name="examples"></a>예  
### <a name="a-using-dbcc-cleantable-to-reclaim-space"></a>A. DBCC CLEANTABLE을 사용하여 공간 반환  
다음 예에서는 `Production.Document` 예제 데이터베이스의 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 테이블에 대해 DBCC CLEANTABLE을 실행합니다.
  
```sql  
DBCC CLEANTABLE (AdventureWorks2012,'Production.Document', 0)  
WITH NO_INFOMSGS;  
GO  
```  
  
### <a name="b-using-dbcc-cleantable-and-verifying-results"></a>B. DBCC CLEANTABLE 사용 및 결과 확인  
다음 예에서는 테이블을 만들고 여러 개의 가변 길이 열을 채웁니다. 그런 다음 이 중에서 두 개의 열을 삭제하고 DBCC CLEANTABLE을 실행하여 사용하지 않은 공간을 반환합니다. 쿼리를 실행하여 DBCC CLEANTABLE 명령을 실행하기 전후의 페이지 수 및 사용된 공간 값을 확인합니다.
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ('dbo.CleanTableTest', 'U') IS NOT NULL  
    DROP TABLE dbo.CleanTableTest;  
GO  
CREATE TABLE dbo.CleanTableTest  
    (FileName nvarchar(4000),   
    DocumentSummary nvarchar(max),  
    Document varbinary(max)  
    );  
GO  
-- Populate the table with data from the Production.Document table.  
INSERT INTO dbo.CleanTableTest  
    SELECT REPLICATE(FileName, 1000),   
           DocumentSummary,   
           Document  
    FROM Production.Document;  
GO  
-- Verify the current page counts and average space used in the dbo.CleanTableTest table.  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.dbo.CleanTableTest');  
SELECT alloc_unit_type_desc,   
       page_count,   
       avg_page_space_used_in_percent,   
       record_count  
FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL , 'Detailed');  
GO  
-- Drop two variable-length columns from the table.  
ALTER TABLE dbo.CleanTableTest  
DROP COLUMN FileName, Document;  
GO  
-- Verify the page counts and average space used in the dbo.CleanTableTest table  
-- Notice that the values have not changed.  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.dbo.CleanTableTest');  
SELECT alloc_unit_type_desc,   
       page_count,   
       avg_page_space_used_in_percent,   
       record_count  
FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL , 'Detailed');  
GO  
-- Run DBCC CLEANTABLE.  
DBCC CLEANTABLE (AdventureWorks2012,'dbo.CleanTableTest');  
GO  
-- Verify the values in the dbo.CleanTableTest table after the DBCC CLEANTABLE command.  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.dbo.CleanTableTest');  
SELECT alloc_unit_type_desc,   
       page_count,   
       avg_page_space_used_in_percent,   
       record_count  
FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL , 'Detailed');  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
 [sys.allocation_units&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)  
  
  
