---
title: DBCC CLONEDATABASE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2018
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CLONEDATABASE
- CLONE DATABASE
- DBCC_CLONEDATABASE_TSQL
- DBCC CLONEDATABASE
- DBCC CLONE DATABASE
- CLONEDATABASE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database cloning [SQL Server]
- cloning databases
- clone databases
- cloning database
- clone database
- copying databases
- copy databases
- copying database
- copy database
- NO_STATISTICS option
- NO_QUERYSTORE option
- VERIFY_CLONEDB option
- BACKUP_CLONEDB option
- database copying [SQL Server]
- database cloning [SQL Server]
- DBCC CLONEDATABASE statement
ms.assetid: ''
caps.latest.revision: ''
author: pamela
ms.author: pamela
manager: amitban
ms.openlocfilehash: 00c1d492b8fd4b2315d825c2b74bac701781e9bd
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36258415"
---
# <a name="dbcc-clonedatabase-transact-sql"></a>DBCC CLONEDATABASE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

쿼리 최적화 프로그램과 관련된 성능 문제를 조사하기 위해 DBCC CLONEDATABASE를 사용하여 데이터베이스의 스키마 전용 클론을 생성합니다.

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```
DBCC CLONEDATABASE   
(  
    source_database_name
    ,  target_database_name
    [ WITH { [ NO_STATISTICS ] [ , NO_QUERYSTORE ] [ , VERIFY_CLONEDB ] [ , BACKUP_CLONEDB ] } ]   
)  
```  
  
## <a name="arguments"></a>인수  
*source_database_name*  
복사할 데이터베이스의 이름입니다. 
  
*target_database_name*  
원본 데이터베이스를 복사할 데이터베이스의 이름입니다. 이 데이터베이스는 DBCC CLONEDATABASE로 만들며, 이미 존재하지 않아야 합니다. 
  
NO_STATISTICS  
클론에서 테이블/인덱스 통계를 제외해야 하는지 여부를 지정합니다. 이 옵션을 지정하지 않으면 테이블/인덱스 통계가 자동으로 포함됩니다. 이 옵션은 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 CU3 및 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1부터 사용할 수 있습니다.

NO_QUERYSTORE는 클론에서 쿼리 저장소 데이터를 제외해야 하는지 여부를 지정합니다. 이 옵션을 지정하지 않으면 원본 데이터베이스에 쿼리 저장소가 활성화된 경우 쿼리 저장소 데이터가 클론에 복사됩니다. 이 옵션은 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1부터 사용할 수 있습니다.

VERIFY_CLONEDB  
새로운 데이터베이스의 일관성을 확인합니다.  이 옵션은 복제된 데이터베이스가 프로덕션용일 경우에 필요합니다.  VERIFY_CLONEDB를 활성화하면 통계 및 쿼리 저장소 컬렉션도 비활성화되므로 WITH VERIFY_CLONEDB, NO_STATISTICS, NO_QUERYSTORE를 실행하는 것과 동일합니다.  이 옵션은 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2부터 사용할 수 있습니다.

> [!NOTE]  
> 다음 명령을 사용하여 복제된 데이터베이스가 프로덕션용인지 확인할 수 있습니다. <br/>`SELECT DATABASEPROPERTYEX('clone_database_name', 'IsVerifiedClone')`

BACKUP_CLONEDB  
복제 데이터베이스의 백업을 만들고 확인합니다.  VERIFY_CLONEDB와 함께 사용하는 경우 백업을 수행하기 전에 복제 데이터베이스가 확인됩니다.  이 옵션은 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2부터 사용할 수 있습니다.
  
## <a name="remarks"></a>Remarks
DBCC CLONEDATABASE에 의해 다음 유효성 검사가 수행됩니다. 유효성 검사 중 하나라도 실패할 경우 명령이 실패합니다.
- 원본 데이터베이스는 사용자 데이터베이스여야 합니다. 시스템 데이터베이스(master, model, msdb, tempdb, 배포 데이터베이스 등)의 복제는 허용되지 않습니다.
- 원본 데이터베이스는 온라인 상태이거나 읽을 수 있어야 합니다.
- 복제 데이터베이스와 동일한 이름을 사용하는 데이터베이스가 없어야 합니다.
- 이 명령은 사용자 트랜잭션에 없습니다.

모든 유효성 검사가 성공할 경우 다음 작업을 통해 원본 데이터베이스의 복제가 수행됩니다.
- 원본과 동일한 파일 레이아웃을 사용하되 model 데이터베이스의 기본 파일 크기를 사용하는 새 대상 데이터베이스를 만듭니다.
- 원본 데이터베이스의 내부 스냅숏을 만듭니다.
- 원본에서 대상 데이터베이스로 시스템 메타데이터를 복사합니다.
- 원본에서 대상 데이터베이스로 모든 개체의 모든 스키마를 복사합니다.
- 원본에서 대상 데이터베이스로 모든 인덱스의 통계를 복사합니다.

> [!NOTE]  
> DBCC CLONEDATABASE에서 생성된 새 데이터베이스는 주로 문제 해결 및 진단을 위한 것입니다.  복제된 데이터베이스를 프로덕션 데이터베이스로 사용하도록 지원하려면 VERIFY_CLONEDB 옵션을 사용해야 합니다.

대상 데이터베이스의 모든 파일은 model 데이터베이스에서 크기 및 증가 설정을 상속합니다. 대상 데이터베이스의 파일 이름은 source_file_name _underscore_random number 규칙을 따릅니다. 생성된 파일 이름이 대상 폴더에 이미 있을 경우 DBCC CLONEDATABASE가 실패합니다.

DBCC CLONEDATABASE는 model 데이터베이스에서 생성된 사용자 개체(테이블, 인덱스, 스키마, 역할 등)가 있는 경우 클론 생성을 지원하지 않습니다. model 데이터베이스에 사용자 개체가 있는 경우 다음 오류 메시지와 함께 데이터베이스 복제가 실패합니다.

```
Msg 2601, Level 14, State 1, Line 1
Cannot insert duplicate key row in object <system table> with unique index 'index name'. The duplicate key value is <key value>   
```

> [!IMPORTANT]
> columnstore 인덱스가 있는 경우 [복제 데이터베이스에서 columnstore 인덱스로 쿼리를 조정할 때 고려 사항](https://blogs.msdn.microsoft.com/sql_server_team/considerations-when-tuning-your-queries-with-columnstore-indexes-on-clone-databases/)을 참조하여 **DBCC CLONEDATABASE** 명령을 실행하기 전에 columnstore 인덱스 통계를 업데이트하세요.

복제된 데이터베이스의 데이터 보안과 관련된 자세한 내용은 [복제 된 데이터베이스의 데이터 보안 이해](https://blogs.msdn.microsoft.com/sql_server_team/understanding-data-security-in-cloned-databases-created-using-dbcc-clonedatabase/)를 참조하세요.

## <a name="internal-database-snapshot"></a>내부 데이터베이스 스냅숏
DBCC CLONEDATABASE는 복사를 수행하는 데 필요한 트랜잭션 일관성을 위해 원본 데이터베이스의 내부 데이터베이스 스냅숏을 사용합니다. 이 스냅숏을 사용하면 이러한 명령이 실행될 때 차단 및 동시성 문제를 방지할 수 있습니다. 스냅숏을 만들 수 없는 경우 DBCC CLONEDATABASE가 실패합니다. 

복사 프로세스의 다음 단계 동안 데이터베이스 수준 잠금이 유지됩니다.
- 원본 데이터베이스 유효성 검사
- 원본 데이터베이스에 대한 S 잠금 가져오기
- 원본 데이터베이스의 스냅숏 만들기
- 복제 데이터베이스 만들기(model 데이터베이스에서 상속되는 빈 데이터베이스)
- 복제 데이터베이스에 대한 X 잠금 가져오기
- 복제 데이터베이스에 메타데이터 복사
- 모든 DB 잠금 해제

명령 실행이 종료되는 즉시 내부 스냅숏이 삭제됩니다. 복제된 데이터베이스에서 TRUSTWORTHY 및 DB_CHAINING 옵션이 해제됩니다. 

## <a name="supported-objects"></a>지원되는 개체
대상 데이터베이스에서 다음 개체만 복제할 수 있습니다. 암호화된 개체가 복제되지만 복제 데이터베이스에서 사용할 수 없습니다. 다음 섹션에 나열되지 않은 모든 개체는 클론에서 지원되지 않습니다. 
- APPLICATION ROLE
- AVAILABILITY GROUP
- COLUMNSTORE INDEX
- CDB
- CDC
- CLR([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 CU3, [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 이상 버전부터)
- DATABASE PROPERTIES
- DEFAULT
- FILES AND FILEGROUPS
- 전체 텍스트([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU2부터)
- FUNCTION
- INDEX
- Login
- PARTITION FUNCTION
- PARTITION SCHEME
- PROCEDURE   
> [!NOTE]   
> [!INCLUDE[tsql](../../includes/tsql-md.md)] 프로시저는 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2부터 모든 릴리스에서 지원됩니다. CLR 프로시저는 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 CU3부터 지원됩니다. 고유하게 컴파일된 프로시저는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1부터 지원됩니다.  

- QUERY STORE([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1부터)   
> [!NOTE]   
> 쿼리 저장소 데이터는 원본 데이터베이스에 활성화된 경우에만 복사됩니다. 쿼리 저장소의 일부로 최신 런타임 통계를 복사하려면 DBCC CLONEDATABASE를 실행하기 전에 sp_query_store_flush_db를 실행하여 쿼리 저장소에 런타임 통계를 플러시합니다.  

- ROLE
- RULE
- SCHEMA
- SEQUENCE
- SPATIAL INDEX
- STATISTICS
- SYNONYM
- TABLE
- MEMORY OPTIMIZED TABLES([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 이상 버전에서만).
- FILESTREAM AND FILETABLE OBJECTS([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 CU3, [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 이상 버전부터). 
- TRIGGER
- TYPE
- UPGRADED DB
- User
- VIEW
- XML INDEX
- XML SCHEMA COLLECTION  

## <a name="permissions"></a>사용 권한  
**sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.

## <a name="error-log-messages"></a>오류 로그 메시지
다음 메시지는 복제 프로세스 중에 오류 로그에 기록되는 메시지의 예입니다.

```
2018-03-26 15:33:56.05 spid53 Database cloning for 'sourcedb' has started with target as 'sourcedb_clone'.

2018-03-26 15:33:56.46 spid53 Starting up database 'sourcedb_clone'.

2018-03-26 15:33:57.80 spid53 Setting database option TRUSTWORTHY to OFF for database 'sourcedb_clone'.

2018-03-26 15:33:57.80 spid53 Setting database option DB_CHAINING to OFF for database 'sourcedb_clone'.

2018-03-26 15:33:57.88 spid53 Starting up database 'sourcedb_clone'.

2018-03-26 15:33:57.91 spid53 Database 'sourcedb_clone' is a cloned database. A cloned database should be used for diagnostic purposes only and is not supported for use in a production environment.

2018-03-26 15:33:57.92 spid53 Database cloning for 'sourcedb' has finished. Cloned database is 'sourcedb_clone'.
```

## <a name="database-properties"></a>데이터베이스 속성
`DATABASEPROPERTYEX('dbname', 'IsClone')`는 데이터베이스가 DBCC CLONEDATABASE를 사용하여 생성된 경우에 1을 반환합니다.

`DATABASEPROPERTYEX('dbname', 'IsVerifiedClone')`는 데이터베이스가 WITH VERIFY_CLONEDB를 사용하여 성공적으로 확인된 경우에 1을 반환합니다.

## <a name="examples"></a>예  
  
### <a name="a-creating-a-clone-of-a-database-that-includes-schema-statistics-and-query-store"></a>1. 스키마, 통계 및 쿼리 저장소를 포함하는 데이터베이스의 클론 만들기 
다음 예에서는 스키마, 통계 및 쿼리 저장소 데이터를 포함하는 AdventureWorks 데이터베이스의 클론을 만듭니다([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 이상 버전).

```sql  
DBCC CLONEDATABASE (AdventureWorks, AdventureWorks_Clone);    
GO 
```  
  
### <a name="b-creating-a-schema-only-clone-of-a-database-without-statistics"></a>2. 통계가 없는 데이터베이스의 스키마 전용 클론 만들기 
다음 예에서는 통계를 포함하지 않는 AdventureWorks 데이터베이스의 클론을 만듭니다([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 CU3 이상 버전).

```sql  
DBCC CLONEDATABASE (AdventureWorks, AdventureWorks_Clone) WITH NO_STATISTICS;    
GO 
```  

### <a name="c-creating-a-schema-only-clone-of-a-database-without-statistics-and-query-store"></a>3. 통계 및 쿼리 저장소가 없는 데이터베이스의 스키마 전용 클론 만들기 
다음 예에서는 통계 및 쿼리 저장소 데이터를 포함하지 않는 AdventureWorks 데이터베이스의 클론을 만듭니다([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 이상 버전).

```sql  
DBCC CLONEDATABASE (AdventureWorks, AdventureWorks_Clone) WITH NO_STATISTICS, NO_QUERYSTORE;    
GO 
```  

### <a name="d-creating-a-clone-of-a-database-that-is-verified-for-production-use"></a>4. 프로덕션용으로 확인된 데이터베이스의 클론 만들기
다음 예에서는 프로덕션 데이터베이스로 사용하도록 확인되었고, 통계 및 쿼리 저장소가 없는 AdventureWorks 데이터베이스의 스키마 전용 클론을 만듭니다([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 이상 버전).

```sql  
DBCC CLONEDATABASE (AdventureWorks, AdventureWorks_Clone) WITH VERIFY_CLONEDB;    
GO 
```  
  
### <a name="e-creating-a-clone-of-a-database-that-is-verified-for-production-use-that-includes-a-backup-of-the-cloned-database"></a>5. 프로덕션용으로 확인되었고, 복제된 데이터베이스의 백업을 포함하는 데이터베이스 클론 만들기
다음 예에서는 프로덕션 데이터베이스로 사용하도록 확인되었고, 통계 및 쿼리 저장소가 없는 AdventureWorks 데이터베이스의 스키마 전용 클론을 만듭니다.  복제된 데이터베이스의 확인된 백업도 생성됩니다([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 이상 버전).

```sql  
DBCC CLONEDATABASE (AdventureWorks, AdventureWorks_Clone) WITH VERIFY_CLONEDB, BACKUP_CLONEDB;    
GO 
```

## <a name="see-also"></a>참고 항목
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)    
[SQL Server에서 필요한 데이터베이스 메타데이터의 스크립트를 생성하여 통계 전용 데이터베이스를 만드는 방법](http://support.microsoft.com/help/914288)   

