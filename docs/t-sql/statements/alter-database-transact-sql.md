---
title: ALTER DATABASE (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/20/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_DATABASE_TSQL
- ALTER DATABASE
dev_langs: TSQL
helpviewer_keywords:
- databases [SQL Server], modifying
- ALTER DATABASE statement
- databases [SQL Server], renaming
- renaming databases
- database modifications [SQL Server]
- ALTER DATABASE statement, syntax described
- database names [SQL Server], ALTER DATABASE
- modifying databases
- collations [SQL Server], modifying
- database mirroring [SQL Server], Transact-SQL
ms.assetid: 15f8affd-8f39-4021-b092-0379fc6983da
caps.latest.revision: "282"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: b8e96cad90ff94b1f4e8f110d13b87668809606f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="alter-database-transact-sql"></a>ALTER DATABASE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스 또는 데이터베이스와 연관된 파일 및 파일 그룹을 수정합니다. 데이터베이스의 파일 및 파일 그룹 추가 또는 제거, 데이터베이스 또는 데이터베이스 내 파일 및 파일 그룹 특성 변경, 데이터베이스 데이터 정렬 변경 및 데이터베이스 옵션 설정을 수행합니다. 데이터베이스 스냅숏은 수정할 수 없습니다. 복제와 관련 된 데이터베이스 옵션을 수정 하려면 사용 하 여 [sp_replicationdboption](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)합니다.  
   
 ALTER DATABASE 구문은 설명할 항목이 많기 때문에 다음 항목으로 구분하여 설명됩니다.  
  
 ALTER DATABASE  
 현재 항목은 데이터베이스의 이름 및 데이터 정렬 변경을 위한 구문을 제공합니다.  
  
 [ALTER DATABASE 파일 및 파일 그룹 옵션](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)  
 데이터베이스의 파일과 파일 그룹을 추가 및 제거하고 파일과 파일 그룹의 특성을 변경하기 위한 구문을 제공합니다.  
  
 [ALTER DATABASE SET 옵션](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
 ALTER DATABASE의 SET 옵션을 사용하여 데이터베이스의 특성을 변경하기 위한 구문을 제공합니다.  
  
 [ALTER DATABASE 데이터베이스 미러링](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)  
 데이터베이스 미러링과 관련된 ALTER DATABASE의 SET 옵션에 대한 구문을 제공합니다.  
  
 [ALTER DATABASE SET HADR](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)  
 에 대 한 구문을 제공는 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] Always On 가용성 그룹의 보조 복제본에서 보조 데이터베이스를 구성 하기 위한 ALTER DATABASE의 옵션입니다.  
  
 [ALTER DATABASE 호환성 수준](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
 데이터베이스 호환성 수준과 관련된 ALTER DATABASE의 SET 옵션에 대한 구문을 제공합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
 
Azure SQL 데이터베이스에 대 한 참조 [ALTER database&#40; Azure SQL 데이터베이스 &#41;](../../t-sql/statements/alter-database-azure-sql-database.md)  
Azure SQL 데이터 웨어하우스를 참조 하세요. [ALTER database&#40; Azure SQL 데이터 웨어하우스 &#41; ](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md).  
병렬 데이터 웨어하우스에 대 한 참조 [ALTER database&#40; 병렬 데이터 웨어하우스 &#41; ](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md).
  
## <a name="syntax"></a>구문  
  
```  
-- SQL Server Syntax  
ALTER DATABASE { database_name  | CURRENT }  
{  
    MODIFY NAME = new_database_name   
  | COLLATE collation_name  
  | <file_and_filegroup_options>  
  | <set_database_options>  
}  
[;]  
  
<file_and_filegroup_options >::=  
  <add_or_modify_files>::=  
  <filespec>::=   
  <add_or_modify_filegroups>::=  
  <filegroup_updatability_option>::=  
  
<set_database_options>::=  
  <optionspec>::=   
  <auto_option> ::=   
  <change_tracking_option> ::=  
  <cursor_option> ::=   
  <database_mirroring_option> ::=   
  <date_correlation_optimization_option> ::=  
  <db_encryption_option> ::=  
  <db_state_option> ::=  
  <db_update_option> ::=  
  <db_user_access_option> ::=  <delayed_durability_option> ::=  <external_access_option> ::=  
  <FILESTREAM_options> ::=  
  <HADR_options> ::=    
  <parameterization_option> ::=  
  <query_store_options> ::=  
  <recovery_option> ::=   
  <service_broker_option> ::=  
  <snapshot_option> ::=  
  <sql_option> ::=   
  <termination> ::=  
  
```  
  
## <a name="arguments"></a>인수  
 *database_name*  
 수정할 데이터베이스의 이름입니다.  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 이 옵션을 사용할 수 없습니다.  
  
 CURRENT  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 현재 사용 중인 데이터베이스를 변경하도록 지정합니다.  
  
 MODIFY NAME  **=**  *new_database_name*  
 로 지정 된 이름의 데이터베이스를 이름을 바꿉니다. *new_database_name*합니다.  
  
 COLLATE *데이터 정렬 이름*  
 데이터베이스에 대한 데이터 정렬을 지정합니다. *데이터 정렬 이름* Windows 데이터 정렬 이름이 나 SQL 데이터 정렬 이름이 될 수 있습니다. 이를 지정하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 데이터 정렬이 지정됩니다.  
  
 기본 데이터 정렬이 아닌 데이터 정렬로 데이터베이스를 만들 경우 데이터베이스의 데이터는 항상 지정된 데이터 정렬을 따릅니다. 에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 내부 카탈로그 정보는를 사용 하 여 유지 관리는 포함 된 데이터베이스를 만들 때는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본 데이터 정렬, **Latin1_General_100_CI_AS_WS_KS_SC**합니다.  
  
 Windows 및 SQL 데이터 정렬 이름에 대 한 자세한 내용은 참조 하십시오. [collate&#40; Transact SQL &#41; ](~/t-sql/statements/collations.md).  
  
 **\<delayed_durability_option >:: =**  
 **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 자세한 내용은 참조 하십시오. [ALTER DATABASE SET 옵션 &#40; Transact SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md) 및 [트랜잭션 내 구성을 제어](../../relational-databases/logs/control-transaction-durability.md)합니다.  
  
 **\<file_and_filegroup_options >:: =**  
 자세한 내용은 참조 [ALTER DATABASE 파일 및 파일 그룹 옵션 &#40; Transact SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).  
  
## <a name="remarks"></a>주의  
 사용 하 여 데이터베이스를 제거 하려면 [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)합니다.  
  
 사용 하 여 데이터베이스의 크기를 줄이려면 [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)합니다.  
  
 ALTER DATABASE 문은 자동 커밋 모드(기본 트랜잭션 관리 모드)에서 실행되어야 하며 명시적 또는 암시적 트랜잭션에서는 허용되지 않습니다.  
  
 데이터베이스 파일의 상태(예: 온라인 또는 오프라인)는 데이터베이스의 상태와는 별도로 유지 관리됩니다. 자세한 내용은 참조 [파일 상태](../../relational-databases/databases/file-states.md)합니다. 전체 파일 그룹의 가용성은 파일 그룹 내 파일의 상태에 따라 결정됩니다. 파일 그룹을 사용하려면 파일 그룹 내의 모든 파일이 온라인 상태여야 합니다. 파일 그룹이 오프라인 상태인 경우 SQL 문을 사용한 파일 그룹 액세스 시도는 오류가 발생하며 실패하게 됩니다. SELECT 문에 대한 쿼리 계획을 작성할 때 쿼리 최적화 프로그램은 오프라인 파일 그룹에 있는 비클러스터형 인덱스와 인덱싱된 뷰는 피함으로써 이러한 문이 성공하도록 합니다. 그러나 오프라인 파일 그룹에 대상 테이블의 힙이나 클러스터형 인덱스가 있는 경우 SELECT 문은 실패합니다. 오프라인 파일 그룹의 인덱스를 사용하여 테이블을 수정하는 INSERT, UPDATE 또는 DELETE 문도 실패합니다.  
  
 데이터베이스가 RESTORING 상태에 있으면 ALTER DATABASE 문이 대부분 실패합니다. 단, 데이터베이스 미러링 옵션을 설정하는 경우는 예외입니다. 활성 복원 작업 중이나 데이터베이스 또는 로그 파일의 복원 작업이 손상된 백업 파일로 인해 실패할 경우 데이터베이스가 RESTORING 상태일 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에 대한 계획 캐시는 다음 옵션 중 하나를 설정하여 삭제됩니다.  
  
|||  
|-|-|  
|OFFLINE|READ_WRITE|  
|ONLINE|MODIFY FILEGROUP DEFAULT|  
|MODIFY_NAME|MODIFY FILEGROUP READ_WRITE|  
|COLLATE|MODIFY FILEGROUP READ_ONLY|  
|READ_ONLY|PAGE_VERIFY|  
  
 계획 캐시를 삭제하면 모든 후속 실행 계획이 다시 컴파일되며 일시적으로 갑자기 쿼리 성능이 저하될 수 있습니다. 계획 캐시의 삭제된 각 캐시스토어에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 "데이터베이스 유지 관리 또는 재구성 작업으로 인해 '%s' 캐시스토어(계획 캐시의 일부)에 대한 캐시스토어 플러시가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 %d번 발견되었습니다"라는 정보 메시지가 있습니다. 이 메시지는 캐시가 해당 시간 간격 내에 플러시되는 동안 5분마다 기록됩니다.  
  
 프로시저 캐시는 다음 시나리오에도 플러시됩니다.  
  
-   데이터베이스에서 AUTO_CLOSE 데이터베이스 옵션이 ON으로 설정되어 있습니다. 사용자 연결이 데이터베이스를 참조하거나 사용하지 않으면 백그라운드 작업에서 자동으로 데이터베이스를 닫고 종료하려고 합니다.  
  
-   기본 옵션이 있는 데이터베이스에 대해 여러 가지 쿼리를 실행합니다. 그러면 데이터베이스가 삭제됩니다.  
  
-   원본 데이터베이스에 대한 데이터베이스 스냅숏이 삭제됩니다.  
  
-   데이터베이스에 대한 트랜잭션 로그를 성공적으로 다시 작성합니다.  
  
-   데이터베이스 백업을 복원합니다.  
  
-   데이터베이스를 분리합니다.  
  
## <a name="changing-the-database-collation"></a>데이터베이스 데이터 정렬 변경  
 데이터베이스에 다른 데이터 정렬을 적용하기 전에 다음 조건이 충족되었는지 확인하세요.  
  
-   현재 데이터베이스를 사용하고 있는 다른 사용자가 없습니다.  
  
-   데이터베이스의 데이터 정렬에 종속된 스키마 바운드 개체가 없습니다.  
  
     데이터베이스 데이터 정렬에 의존할 경우에서 다음 개체를 ALTER DATABASE 데이터베이스에 존재 하는 경우*database_name*COLLATE 문은 실패 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 ALTER 동작을 차단하는 각 개체에 대해 오류 메시지를 반환합니다.  
  
    -   SCHEMABINDING으로 생성된 사용자 정의 함수 및 뷰  
  
    -   계산 열  
  
    -   CHECK 제약 조건  
  
    -   기본 데이터베이스 데이터 정렬에서 상속 받은 데이터 정렬을 사용하는 문자 열이 있는 테이블을 반환하는 테이블 반환 함수  
  
     비스키마 바운드 엔터티에 대한 종속성 정보는 데이터베이스 데이터 정렬이 변경될 때 자동으로 업데이트됩니다.  
  
 데이터베이스 데이터 정렬을 변경해도 데이터베이스 개체에 대한 시스템 이름이 중복되는 경우는 발생하지 않습니다. 데이터 정렬 변경 시 중복 이름이 발생하면 다음 네임스페이스에서 데이터베이스 데이터 정렬 변경이 실패할 수 있습니다.  
  
-   개체 이름(프로시저, 테이블, 트리거, 뷰 등)  
  
-   스키마 이름.  
  
-   보안 주체(그룹, 역할, 사용자 등)  
  
-   스칼라 유형 이름(시스템 및 사용자 정의 유형)  
  
-   전체 텍스트 카탈로그 이름  
  
-   개체 내의 열 또는 매개 변수 이름  
  
-   테이블 내의 인덱스 이름  
  
새로운 데이터 정렬로 중복 이름이 생성되는 경우 변경 동작은 실패하게 되며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 중복이 발견된 네임스페이스를 지정하는 오류 메시지를 반환합니다.  
  
## <a name="viewing-database-information"></a>데이터베이스 정보 보기  
 카탈로그 뷰, 시스템 함수 및 시스템 저장 프로시저를 사용하여 데이터베이스, 파일 및 파일 그룹에 대한 정보를 반환할 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 데이터베이스에 대한 ALTER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-changing-the-name-of-a-database"></a>1. 데이터베이스의 이름 변경  
 다음 예에서는 `AdventureWorks2012` 데이터베이스의 이름을 `Northwind`로 변경합니다.  
  
```  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
Modify Name = Northwind ;  
GO  
```  
  
### <a name="b-changing-the-collation-of-a-database"></a>2. 데이터베이스 데이터 정렬 변경  
 다음 예에서는 `testdb`S 데이터 정렬을 사용하여 `SQL_Latin1_General_CP1_CI_A`라는 데이터베이스를 만든 다음 `testdb` 데이터베이스의 데이터 정렬을 `COLLATE French_CI_AI`로 변경합니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
```  
USE master;  
GO  
  
CREATE DATABASE testdb  
COLLATE SQL_Latin1_General_CP1_CI_AS ;  
GO  
  
ALTER DATABASE testDB  
COLLATE French_CI_AI ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
- [ALTER database&#40; Azure SQL 데이터베이스 &#41;](alter-database-azure-sql-database.md)  
- [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
- [DATABASEPROPERTYEX&#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
- [DROP DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
- [SET TRANSACTION ISOLATION LEVEL&#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
- [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
- [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
- [sp_spaceused&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
- [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
- [sys.database_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
- [sys.database_mirroring_witnesses &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
- [sys.data_spaces &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
- [sys.filegroups &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
- [sys.master_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
- [시스템 데이터베이스](../../relational-databases/databases/system-databases.md)  
  
