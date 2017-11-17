---
title: DBCC INDEXDEFRAG (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- INDEXDEFRAG
- DBCC INDEXDEFRAG
- DBCC_INDEXDEFRAG_TSQL
- INDEXDEFRAG_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- defragmenting indexes
- DBCC INDEXDEFRAG statement
- leaf level defragmenting
- fragmentation [SQL Server]
- index defragmenting [SQL Server]
ms.assetid: 3c7df676-4843-44d0-8c1c-a9ab7e593b70
caps.latest.revision: 49
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 79750bc5f94a7a2b459d0b3e3266ea7ee91bc4dc
ms.contentlocale: ko-kr
ms.lasthandoff: 10/24/2017

---
# <a name="dbcc-indexdefrag-transact-sql"></a>DBCC INDEXDEFRAG(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

지정된 테이블 또는 뷰의 인덱스를 조각 모음합니다.
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]사용 하 여 [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) 대신 합니다.  
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해 [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658))
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DBCC INDEXDEFRAG  
(  
    { database_name | database_id | 0 }   
    , { table_name | table_id | view_name | view_id }   
    [ , { index_name | index_id } [ , { partition_number | 0 } ] ]  
)  
    [ WITH NO_INFOMSGS ]   
```  
  
## <a name="arguments"></a>인수  
 *a s e _* | *database_id* | 0  
 조각 모음할 인덱스가 들어 있는 데이터베이스입니다. 0을 지정하면 현재 데이터베이스가 사용됩니다. 데이터베이스 이름에 대 한 규칙을 준수 해야 [식별자](../../relational-databases/databases/database-identifiers.md)합니다.  
  
 *table_name* | *table_id* | *view_name* | *view_id*  
 조각 모음할 인덱스가 들어 있는 테이블 또는 뷰입니다. 테이블 및 뷰 이름은 식별자 규칙을 따라야 합니다.  
  
 *index_name* | *index_id*  
 조각 모음할 인덱스의 이름 또는 ID입니다. 이 인수를 지정하지 않으면 지정한 테이블이나 뷰의 모든 인덱스를 조각 모음합니다. 인덱스 이름은 식별자에 대한 규칙을 따라야 합니다.  
  
 *partition_number* | 0  
 조각 모음할 인덱스의 파티션 번호입니다. 지정하지 않거나 0을 지정하면 지정한 인덱스의 모든 파티션을 조각 모음합니다.  
  
 WITH NO_INFOMSGS  
 심각도가 0에서 10 사이인 모든 정보 메시지를 표시하지 않습니다.  
  
## <a name="remarks"></a>주의  
DBCC INDEXDEFRAG는 인덱스 검색 성능을 향상시키기 위해 페이지의 물리적 순서가 왼쪽에서 오른쪽으로 리프 노드의 논리적 순서와 일치하도록 인덱스 리프 수준의 조각을 모읍니다.
  
> [!NOTE]  
>  DBCC INDEXDEFRAG가 실행되면 인덱스 조각 모음이 직렬로 수행됩니다. 이는 하나의 인덱스에 대한 작업이 하나의 스레드를 통해 수행됨을 의미합니다. 병렬 처리는 수행되지 않습니다. 또한 동일한 DBCC INDEXDEFRAG 문에서 여러 개의 인덱스에 대해 작업을 실행하면 한 번에 한 인덱스씩 차례로 수행됩니다.  
  
DBCC INDEXDEFRAG는 또한 인덱스가 만들어졌을 때 지정된 채우기 비율을 고려하여 인덱스의 페이지를 압축합니다. 압축으로 인해 생성된 빈 페이지는 제거됩니다. 자세한 내용은 [인덱스의 채우기 비율 지정](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)을 참조하세요.
  
인덱스가 하나 이상의 파일에 걸쳐있을 경우 DBCC INDEXDEFRAG는 한 번에 한 파일씩 조각을 모으며 파일 간에 페이지를 마이그레이션할 수 없습니다.
  
DBCC INDEXDEFRAG는 5분마다 예상 완료율을 보고합니다. DBCC INDEXDEFRAG는 진행 도중 언제든지 종료할 수 있으며 완료된 작업은 모두 그대로 보존됩니다.
  
DBCC DBREINDEX나 일반적인 인덱스 작성 작업과 달리 DBCC INDEXDEFRAG는 온라인 작업이므로 장시간 잠금 상태를 유지하지 않습니다. 따라서 DBCC INDEXDEFRAG는 쿼리 또는 업데이트의 실행을 차단하지 않습니다. 조각 모음에 걸리는 시간은 조각화 정도와 관련이 있으므로 상대적으로 덜 조각난 인덱스는 새 인덱스를 만드는 것보다 빠르게 조각 모음을 실행할 수 있습니다. 심하게 조각난 인덱스는 새로 만드는 것보다 조각 모음을 실행하는 데 시간이 훨씬 많이 걸릴 수도 있습니다.
  
조각 모음은 데이터베이스 복구 모델 설정에 관계없이 항상 전체 로깅됩니다. 자세한 내용은 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)를 참조하세요. 심하게 조각난 인덱스를 조각 모음할 경우 인덱스 작성을 전체 로깅하는 것보다 더 큰 로그가 생성될 수 있습니다. 그러나 조각 모음은 일련의 짧은 트랜잭션으로 수행되므로 로그 백업을 자주 하거나 복구 모델 설정이 SIMPLE인 경우에는 큰 로그가 필요하지 않습니다.
  
## <a name="restrictions"></a>제한 사항  
DBCC INDEXDEFRAG는 인덱스 리프 페이지를 섞어 놓습니다. 따라서 인덱스가 디스크의 다른 인덱스와 인터리브된 경우 해당 인덱스에 대해 DBCC INDEXDEFRAG를 실행해도 인덱스의 모든 리프 페이지가 연결되지는 않습니다. 페이지의 클러스터링을 향상시키려면 인덱스를 다시 작성하십시오.
DBCC INDEXDEFRAG는 다음 인덱스를 조각 모음하는 데 사용할 수 없습니다.
-   비활성화된 인덱스입니다.  
-   페이지 잠금이 OFF로 설정된 인덱스입니다.  
-   공간 인덱스입니다.  
  
시스템 테이블에 대해 사용할 수 없습니다.
  
## <a name="result-sets"></a>결과 집합  
DBCC INDEXDEFRAG는 인덱스가 문에 지정되고 WITH NO_INFOMSGS를 지정하지 않은 경우 다음과 같은 결과 집합을 반환합니다. 값은 다를 수 있습니다.
  
```sql
Pages Scanned Pages Moved Pages Removed  
------------- ----------- -------------  
359           346         8  
  
(1 row(s) affected)  
  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissions  
호출자에 게 테이블을 소유 하거나의 멤버는 **sysadmin** 고정 서버 역할의 **db_owner** 고정 데이터베이스 역할 또는 **db_ddladmin** 고정된 데이터베이스 역할입니다.
  
## <a name="examples"></a>예  
### <a name="a-using-dbcc-indexdefrag-to-defragment-an-index"></a>1. DBCC INDEXDEFRAG를 사용하여 인덱스 조각 모음 수행  
다음 예제에는의 모든 파티션을 조각 모음는 `PK_Product_ProductID` 인덱스는 `Production.Product` 테이블에 `AdventureWorks` 데이터베이스입니다.
  
```sql  
DBCC INDEXDEFRAG (AdventureWorks2012, 'Production.Product', PK_Product_ProductID);  
GO  
```  
  
### <a name="b-using-dbcc-showcontig-and-dbcc-indexdefrag-to-defragment-the-indexes-in-a-database"></a>2. DBCC SHOWCONTIG 및 DBCC INDEXDEFRAG를 사용하여 데이터베이스에서 인덱스 조각 모음 수행  
 다음 예에서는 데이터베이스에서 선언된 임계값 이상으로 조각화된 모든 인덱스에 조각 모음을 수행하는 간단한 방법을 보여 줍니다.  
  
```sql  
/*Perform a 'USE <database name>' to select the database in which to run the script.*/  
-- Declare variables  
SET NOCOUNT ON;  
DECLARE @tablename varchar(255);  
DECLARE @execstr   varchar(400);  
DECLARE @objectid  int;  
DECLARE @indexid   int;  
DECLARE @frag      decimal;  
DECLARE @maxfrag   decimal;  
  
-- Decide on the maximum fragmentation to allow for.  
SELECT @maxfrag = 30.0;  
  
-- Declare a cursor.  
DECLARE tables CURSOR FOR  
   SELECT TABLE_SCHEMA + '.' + TABLE_NAME  
   FROM INFORMATION_SCHEMA.TABLES  
   WHERE TABLE_TYPE = 'BASE TABLE';  
  
-- Create the table.  
CREATE TABLE #fraglist (  
   ObjectName char(255),  
   ObjectId int,  
   IndexName char(255),  
   IndexId int,  
   Lvl int,  
   CountPages int,  
   CountRows int,  
   MinRecSize int,  
   MaxRecSize int,  
   AvgRecSize int,  
   ForRecCount int,  
   Extents int,  
   ExtentSwitches int,  
   AvgFreeBytes int,  
   AvgPageDensity int,  
   ScanDensity decimal,  
   BestCount int,  
   ActualCount int,  
   LogicalFrag decimal,  
   ExtentFrag decimal);  
  
-- Open the cursor.  
OPEN tables;  
  
-- Loop through all the tables in the database.  
FETCH NEXT  
   FROM tables  
   INTO @tablename;  
  
WHILE @@FETCH_STATUS = 0  
BEGIN  
-- Do the showcontig of all indexes of the table  
   INSERT INTO #fraglist   
   EXEC ('DBCC SHOWCONTIG (''' + @tablename + ''')   
      WITH FAST, TABLERESULTS, ALL_INDEXES, NO_INFOMSGS');  
   FETCH NEXT  
      FROM tables  
      INTO @tablename;  
END;  
  
-- Close and deallocate the cursor.  
CLOSE tables;  
DEALLOCATE tables;  
  
-- Declare the cursor for the list of indexes to be defragged.  
DECLARE indexes CURSOR FOR  
   SELECT ObjectName, ObjectId, IndexId, LogicalFrag  
   FROM #fraglist  
   WHERE LogicalFrag >= @maxfrag  
      AND INDEXPROPERTY (ObjectId, IndexName, 'IndexDepth') > 0;  
  
-- Open the cursor.  
OPEN indexes;  
  
-- Loop through the indexes.  
FETCH NEXT  
   FROM indexes  
   INTO @tablename, @objectid, @indexid, @frag;  
  
WHILE @@FETCH_STATUS = 0  
BEGIN  
   PRINT 'Executing DBCC INDEXDEFRAG (0, ' + RTRIM(@tablename) + ',  
      ' + RTRIM(@indexid) + ') - fragmentation currently '  
       + RTRIM(CONVERT(varchar(15),@frag)) + '%';  
   SELECT @execstr = 'DBCC INDEXDEFRAG (0, ' + RTRIM(@objectid) + ',  
       ' + RTRIM(@indexid) + ')';  
   EXEC (@execstr);  
  
   FETCH NEXT  
      FROM indexes  
      INTO @tablename, @objectid, @indexid, @frag;  
END;  
  
-- Close and deallocate the cursor.  
CLOSE indexes;  
DEALLOCATE indexes;  
  
-- Delete the temporary table.  
DROP TABLE #fraglist;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
[CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)
  
  


