---
title: "사용자 데이터베이스 이동 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- disaster recovery [SQL Server], moving database files
- database files [SQL Server], moving
- data files [SQL Server], moving
- editions [SQL Server], moving databases between
- moving full-text catalogs
- scheduled disk maintenace [SQL Server]
- moving databases
- full-text catalogs [SQL Server], moving
- moving database files
- moving user databases
- relocating database files
- planned database relocations [SQL Server]
- databases [SQL Server], moving
ms.assetid: ad9a4e92-13fb-457d-996a-66ffc2d55b79
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: eb72a2d6947406c8fc14d40571ada79151668422
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="move-user-databases"></a>사용자 데이터베이스 이동
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 문의 FILENAME 절에 새 파일 위치를 지정하여 사용자 데이터베이스의 데이터, 로그 및 전체 텍스트 카탈로그 파일을 새 위치로 이동할 수 있습니다. 이 방법은 동일한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스 내에서 데이터베이스 파일을 이동하는 경우에 적용됩니다. 데이터베이스를 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스나 다른 서버로 이동하려면 [백업 및 복원](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md) 작업이나 [분리/연결](../../relational-databases/databases/move-a-database-using-detach-and-attach-transact-sql.md)작업을 사용합니다.  
  
## <a name="considerations"></a>고려 사항  
 데이터베이스를 다른 서버 인스턴스로 이동하는 경우 사용자와 응용 프로그램에 일관된 환경을 제공하려면 데이터베이스의 일부 또는 모든 메타데이터를 다시 만들어야 할 수도 있습니다. 자세한 내용은 [다른 서버 인스턴스에서 데이터베이스를 사용할 수 있도록 할 때 메타데이터 관리&#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)을 참조하세요.  
  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 일부 기능 중 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 데이터베이스 파일의 정보를 저장하는 방법이 변경되었습니다. 이러한 기능은 특정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전으로 제한됩니다. 이러한 기능을 포함하는 데이터베이스는 이러한 기능이 지원되지 않는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전으로 이동할 수 없습니다. 현재 데이터베이스에 설정된 모든 버전별 기능 목록을 보려면 sys.dm_db_persisted_sku_features 동적 관리 뷰를 사용합니다.  
  
 이 항목의 절차를 사용하려면 데이터베이스 파일의 논리적 이름이 필요합니다. 논리적 파일 이름을 구하려면 [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md) 카탈로그 뷰의 name 열을 쿼리합니다.  
  
 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]에서 시작하여 전체 텍스트 카탈로그는 파일 시스템에 저장되는 대신 데이터베이스에 통합됩니다. 데이터베이스를 이동할 때 전체 텍스트 카탈로그는 이제 자동으로 이동합니다.  
  
## <a name="planned-relocation-procedure"></a>계획된 재배치 절차  
 계획된 재배치의 일부로 데이터 또는 로그 파일을 이동하려면 다음 단계를 따릅니다.  
  
1.  다음 문을 실행합니다.  
  
    ```  
    ALTER DATABASE database_name SET OFFLINE;  
    ```  
  
2.  파일을 새 위치로 이동합니다.  
  
3.  이동한 각 파일에 대해 다음 문을 실행합니다.  
  
    ```  
    ALTER DATABASE database_name MODIFY FILE ( NAME = logical_name, FILENAME = 'new_path\os_file_name' );  
    ```  
  
4.  다음 문을 실행합니다.  
  
    ```  
    ALTER DATABASE database_name SET ONLINE;  
    ```  
  
5.  다음 쿼리를 실행하여 파일 변경 내용을 확인합니다.  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'<database_name>');  
    ```  
  
## <a name="relocation-for-scheduled-disk-maintenance"></a>예약된 디스크 유지 관리를 위한 재배치  
 예약된 디스크 유지 관리 프로세스의 일부로 파일을 재배치하려면 다음 단계를 따릅니다.  
  
1.  이동할 각 파일에 대해 다음 문을 실행합니다.  
  
    ```  
    ALTER DATABASE database_name MODIFY FILE ( NAME = logical_name , FILENAME = 'new_path\os_file_name' );  
    ```  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 중지하거나 시스템을 종료하여 유지 관리를 수행합니다. 자세한 내용은 [Start, Stop, Pause, Resume, Restart the Database Engine, SQL Server Agent, or SQL Server Browser Service](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)을 참조하세요.  
  
3.  파일을 새 위치로 이동합니다.  
  
4.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스나 서버를 다시 시작합니다. 자세한 내용은 [데이터베이스 엔진, SQL Server 에이전트 또는 SQL Server Browser 서비스 시작, 중지, 일시 중지, 재개 및 다시 시작](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)를 참조하세요  
  
5.  다음 쿼리를 실행하여 파일 변경 내용을 확인합니다.  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'<database_name>');  
    ```  
  
## <a name="failure-recovery-procedure"></a>오류 복구 절차  
 하드웨어 오류로 인해 파일을 이동해야 하는 경우 다음 단계에 따라 파일을 새 위치에 재배치합니다.  
  
> [!IMPORTANT]  
>  데이터베이스가 주의 대상 모드에 있거나 복구할 수 없는 상태여서 시작할 수 없는 경우에는 sysadmin 고정 역할의 멤버만 파일을 이동할 수 있습니다.  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 시작된 경우 중지합니다.  
  
2.  명령 프롬프트에서 다음 명령 중 하나를 입력하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 마스터 전용 복구 모드로 시작합니다.  
  
    -   기본(MSSQLSERVER) 인스턴스의 경우 다음 명령을 실행합니다.  
  
        ```  
        NET START MSSQLSERVER /f /T3608  
        ```  
  
    -   명명된 인스턴스의 경우 다음 명령을 실행합니다.  
  
        ```  
        NET START MSSQL$instancename /f /T3608  
        ```  
  
     자세한 내용은 [Start, Stop, Pause, Resume, Restart the Database Engine, SQL Server Agent, or SQL Server Browser Service](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)을 참조하세요.  
  
3.  이동할 각 파일에 대해 **sqlcmd** 명령 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 다음 문을 실행합니다.  
  
    ```  
    ALTER DATABASE database_name MODIFY FILE( NAME = logical_name , FILENAME = 'new_path\os_file_name' );  
    ```  
  
     **sqlcmd** 유틸리티 사용 방법은 [sqlcmd 유틸리티 사용](../../relational-databases/scripting/sqlcmd-use-the-utility.md)을 참조하세요.  
  
4.  **sqlcmd** 유틸리티 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 종료합니다.  
  
5.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 중지합니다.  
  
6.  파일을 새 위치로 이동합니다.  
  
7.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 시작합니다. 예를 들어 `NET START MSSQLSERVER`을 실행합니다.  
  
8.  다음 쿼리를 실행하여 파일 변경 내용을 확인합니다.  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'<database_name>');  
    ```  
  
## <a name="examples"></a>예  
 다음 예에서는 계획된 재배치의 일부로 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 로그 파일을 새 위치로 이동합니다.  
  
```  
USE master;  
GO  
-- Return the logical file name.  
SELECT name, physical_name AS CurrentLocation, state_desc  
FROM sys.master_files  
WHERE database_id = DB_ID(N'AdventureWorks2012')  
    AND type_desc = N'LOG';  
GO  
ALTER DATABASE AdventureWorks2012 SET OFFLINE;  
GO  
-- Physically move the file to a new location.  
-- In the following statement, modify the path specified in FILENAME to  
-- the new location of the file on your server.  
ALTER DATABASE AdventureWorks2012   
    MODIFY FILE ( NAME = AdventureWorks2012_Log,   
                  FILENAME = 'C:\NewLoc\AdventureWorks2012_Log.ldf');  
GO  
ALTER DATABASE AdventureWorks2012 SET ONLINE;  
GO  
--Verify the new location.  
SELECT name, physical_name AS CurrentLocation, state_desc  
FROM sys.master_files  
WHERE database_id = DB_ID(N'AdventureWorks2012')  
    AND type_desc = N'LOG';  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [데이터베이스 분리 및 연결&#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [시스템 데이터베이스 이동](../../relational-databases/databases/move-system-databases.md)   
 [데이터베이스 파일 이동](../../relational-databases/databases/move-database-files.md)   
 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [데이터베이스 엔진, SQL Server 에이전트 또는 SQL Server Browser 서비스 시작, 중지, 일시 중지, 재개 및 다시 시작](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
  
