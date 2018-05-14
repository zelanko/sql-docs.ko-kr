---
title: 가용성 그룹에 대한 보조 데이터베이스 수동 준비(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.availabilitygroup.preparedbs.f1
- sql13.swb.availabilitygroup.configsecondarydbs.f1
helpviewer_keywords:
- secondary databases [SQL Server], in availability group
- secondary databases [SQL Server]
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], databases
ms.assetid: 9f2feb3c-ea9b-4992-8202-2aeed4f9a6dd
caps.latest.revision: 47
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ebdabe4ea402188340e46cd6ee71aec49cc7a909
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="manually-prepare-a-database-for-an-availability-group-sql-server"></a>가용성 그룹에 대한 보조 데이터베이스 수동 준비(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
이 항목에서는 [!INCLUDE[ssnoversion](../../../includes/ssnoversion-md.md)]에서 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]또는 PowerShell을 사용하여 Always On 가용성 그룹에 대한 데이터베이스를 준비하는 방법에 대해 설명합니다. 데이터베이스를 준비하는 데에는 다음 두 단계가 필요합니다. 

1. RESTORE WITH NORECOVERY를 사용하여 보조 복제본을 호스팅하는 각 서버 인스턴스에 주 데이터베이스의 최근 데이터베이스 백업과 후속 로그 백업을 복원합니다.
2. 가용성 그룹에 복원된 데이터베이스를 조인합니다.  
  
> [!TIP]  
>  기존 로그 전달 구성이 있는 경우 하나 이상의 보조 데이터베이스와 함께 로그 전달 주 데이터베이스를 가용성 그룹 주 복제본과 하나 이상의 보조 복제본으로 변환할 수 있습니다. 자세한 내용은 [로그 전달에서 Always On 가용성 그룹으로 마이그레이션하기 위한 필수 조건&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-migrating-log-shipping-to-always-on-availability-groups.md)을 참조하세요.  

##  <a name="Prerequisites"></a> 필수 조건 및 제한 사항  
  
-   데이터베이스를 배치할 시스템에 보조 데이터베이스를 위한 충분한 공간을 가진 디스크 드라이브가 있는지 확인합니다.  
  
-   보조 데이터베이스의 이름이 주 데이터베이스의 이름과 동일해야 합니다.  
  
-   모든 복원 작업에 대해 RESTORE WITH NORECOVERY를 사용합니다.  
  
-   보조 데이터베이스가 주 데이터베이스와 다른 파일 경로(드라이브 문자 포함)에 있어야 하는 경우 복원 명령에서 각 데이터베이스 파일에 대해 WITH MOVE 옵션을 사용하여 보조 데이터베이스의 경로를 지정해야 합니다.  
  
-   파일 그룹별로 데이터베이스 파일 그룹을 복원하는 경우에는 전체 데이터베이스를 복원해야 합니다.  
  
-   데이터베이스를 복원한 후 마지막으로 복원한 데이터 백업 이후에 만든 모든 로그 백업을 복원(WITH NORECOVERY)해야 합니다.  
  
##  <a name="Recommendations"></a> 권장 사항  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 독립 실행형 인스턴스의 경우 지정된 보조 데이터베이스의 드라이브 문자를 포함한 파일 경로는 가급적 해당 주 데이터베이스의 경로와 동일한 것이 좋습니다. 보조 데이터베이스를 만들 때 데이터베이스 파일을 이동하면 이후의 파일 추가 작업이 보조 데이터베이스에서 실패하고 보조 데이터베이스가 일시 중지될 수 있기 때문입니다.  
  
-   보조 데이터베이스를 준비하기 전에 보조 복제본의 초기화가 완료될 때까지 가용성 그룹에서 데이터베이스에 대한 예약된 로그 백업을 일시 중지하는 것이 좋습니다.  
  
###  <a name="Security"></a> 보안  
 데이터베이스를 백업하면 [TRUSTWORTHY 데이터베이스 속성](../../../relational-databases/security/trustworthy-database-property.md) 이 OFF로 설정됩니다. 따라서 새로 복원된 데이터베이스의 TRUSTWORTHY는 항상 OFF입니다.  
  
####  <a name="Permissions"></a> Permissions  
 BACKUP DATABASE 및 BACKUP LOG 권한은 기본적으로 **sysadmin** 고정 서버 역할과 **db_owner** 및 **db_backupoperator** 고정 데이터베이스 역할의 멤버로 설정됩니다. 자세한 내용은 [BACKUP&#40;Transact-SQL&#41;](../../../t-sql/statements/backup-transact-sql.md)을 참조하세요.  
  
 복원할 데이터베이스가 서버 인스턴스에 없으면 RESTORE 문에 CREATE DATABASE 권한이 있어야 합니다. 자세한 내용은 [RESTORE&#40;Transact-SQL&#41;](../../../t-sql/statements/restore-statements-transact-sql.md)를 통해 복원할 수 없습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
> [!NOTE]  
>  주 복제본을 호스트하는 서버 인스턴스와 보조 복제본을 호스트하는 모든 인스턴스 간에 백업 및 복원 파일 경로가 동일한 경우, [새 가용성 그룹 마법사](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md), [가용성 그룹에 복제본 추가 마법사](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md) 또는 [가용성 그룹에 데이터베이스 추가 마법사](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)를 사용하여 보조 복제본 데이터베이스를 만들 수 있어야 합니다.  
  
 **보조 데이터베이스를 준비하려면**  
  
1.  주 데이터베이스의 최근 데이터베이스 백업이 아직 없는 경우 전체 데이터베이스 백업 또는 차등 데이터베이스 백업을 새로 만듭니다. 이 백업과 모든 후속 로그 백업을 권장 네트워크 공유에 배치하는 것이 좋습니다.  
  
2.  주 데이터베이스의 로그 백업을 하나 이상 만듭니다.

   >[!NOTE]
   >이전에 트랜잭션 로그 백업이 주 복제본의 데이터베이스에서 캡처되지 않은 경우 트랜잭션 로그 백업이 필요하지 않을 수 있습니다. 새 데이터베이스가 가용성 그룹에 조인될 때마다 트랜잭션 로그 백업을 수행하는 것이 좋습니다. 
  
3.  보조 복제본을 호스팅하는 서버 인스턴스에서 주 데이터베이스의 전체 데이터베이스 백업과 원하는 차등 백업을 복원한 다음 모든 후속 로그 백업을 복원합니다.  
  
     **RESTORE DATABASE 옵션** 페이지에서 **데이터베이스를 비작동 상태로 유지하고 커밋되지 않은 트랜잭션을 롤백하지 않습니다. 추가 트랜잭션 로그를 복원할 수 있습니다(RESTORE WITH NORECOVERY).** 를 선택합니다.  
  
     주 데이터베이스와 보조 데이터베이스의 파일 경로가 다른 경우(예: 주 데이터베이스는 'F:' 드라이브에 있지만 보조 복제본을 호스트하는 서버 인스턴스에 F: 드라이브가 없는 경우) WITH 절에 MOVE 옵션을 포함합니다.  
  
4.  보조 데이터베이스 구성을 완료하려면 보조 데이터베이스를 가용성 그룹에 조인해야 합니다. 자세한 내용은 [가용성 그룹에 보조 데이터베이스 조인&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)을 참조하세요.  
  
> [!NOTE]  
>  이러한 백업 및 복원 작업 수행 방법은 이 섹션의 뒷부분에 나오는 [관련 백업 및 복원 태스크](#RelatedTasks)를 참조하세요.  
  
###  <a name="RelatedTasks"></a> 관련된 백업 및 복원 태스크  
 **데이터베이스 백업을 만들려면**  
  
-   [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [차등 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
 **로그 백업을 만들려면**  
  
-   [트랜잭션 로그 백업&#40;SQL Server&#41;](../../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
 **백업을 복원하려면**  
  
-   [Restore a Database Backup Using SSMS](../../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
-   [차등 데이터베이스 백업 복원&#40;SQL Server&#41;](../../../relational-databases/backup-restore/restore-a-differential-database-backup-sql-server.md)  
  
-   [트랜잭션 로그 백업 복원&#40;SQL Server&#41;](../../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
-   [데이터베이스를 새 위치로 복원&#40;SQL Server&#41;](../../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **보조 데이터베이스를 준비하려면**  
  
> [!NOTE]  
>  이 절차에 대한 예는 이 항목의 앞부분에 나오는 [예(Transact-SQL)](#ExampleTsql)를 참조하세요.  
  
1.  주 데이터베이스의 최근 전체 백업이 없는 경우 주 복제본을 호스팅하는 서버 인스턴스에 연결하고 전체 데이터베이스 백업을 만듭니다. 이 백업과 모든 후속 로그 백업을 권장 네트워크 공유에 배치하는 것이 좋습니다.  
  
2.  보조 복제본을 호스팅하는 서버 인스턴스에서 주 데이터베이스의 전체 데이터베이스 백업과 원하는 차등 백업을 복원한 다음 모든 후속 로그 백업을 복원합니다. 모든 복원 작업에 대해 WITH NORECOVERY를 사용합니다.  
  
     주 데이터베이스와 보조 데이터베이스의 파일 경로가 다른 경우(예: 주 데이터베이스는 'F:' 드라이브에 있지만 보조 복제본을 호스트하는 서버 인스턴스에 F: 드라이브가 없는 경우) WITH 절에 MOVE 옵션을 포함합니다.  
  
3.  필수 로그 백업 이후 주 데이터베이스에서 로그 백업이 수행된 경우 이러한 로그 백업도 보조 복제본을 호스팅하는 서버 인스턴스에 복사하여 가장 빠른 로그 백업부터 각각 보조 데이터베이스에 적용해야 합니다. 항상 RESTORE WITH NORECOVERY를 사용하세요.  
  
    > [!NOTE]  
    >  주 데이터베이스를 방금 만들었으며 아직 로그 백업이 수행되지 않은 경우 또는 복구 모델이 방금 SIMPLE에서 FULL로 변경된 경우에는 로그 백업이 존재하지 않습니다.  
  
4.  보조 데이터베이스 구성을 완료하려면 보조 데이터베이스를 가용성 그룹에 조인해야 합니다. 자세한 내용은 [가용성 그룹에 보조 데이터베이스 조인&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)을 참조하세요.  
  
> [!NOTE]  
>  이러한 백업 및 복원 작업 수행 방법은 이 항목의 뒷부분에 나오는 [관련 백업 및 복원 태스크](#RelatedTasks)를 참조하세요.  
  
###  <a name="ExampleTsql"></a> Transact-SQL 예  
 다음 예에서는 보조 데이터베이스를 준비합니다. 이 예에서는 기본적으로 단순 복구 모델을 사용하는 [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] 예제 데이터베이스를 사용합니다.  
  
1.  [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] 데이터베이스를 사용하려면 전체 복구 모델을 사용하도록 수정합니다.  
  
    ```  
    USE master;  
    GO  
    ALTER DATABASE MyDB1   
    SET RECOVERY FULL;  
    GO  
    ```  
  
2.  데이터베이스 복구 모델을 SIMPLE에서 FULL로 변경한 후 보조 데이터베이스를 만드는 데 사용할 수 있는 전체 백업을 만듭니다. 복구 모델이 방금 변경되었으므로 WITH FORMAT 옵션을 지정하여 새 미디어 세트를 만듭니다. 이 옵션은 단순 복구 모델에서 만든 이전 백업과 전체 복구 모델에서 만든 백업을 구분하는 데 유용합니다. 이 예에서는 백업 파일(C:\\[!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)].bak)이 데이터베이스와 같은 드라이브에서 생성됩니다.  
  
    > [!NOTE]  
    >  프로덕션 데이터베이스의 경우에는 항상 별도의 장치에 백업해야 합니다.  
  
     주 복제본(`INSTANCE01`)을 호스팅하는 서버 인스턴스에서 다음과 같이 주 데이터베이스의 전체 백업을 만듭니다.  
  
    ```  
    BACKUP DATABASE MyDB1   
        TO DISK = 'C:\MyDB1.bak'   
        WITH FORMAT  
    GO  
    ```  
  
3.  보조 복제본을 호스팅하는 서버 인스턴스에 전체 백업을 복사합니다.  
  
4.  RESTORE WITH NORECOVERY를 사용하여 보조 복제본을 호스팅하는 서버 인스턴스에 전체 백업을 복원합니다. 복원 명령은 주 데이터베이스와 보조 데이터베이스의 경로가 동일한지 여부에 따라 달라집니다.  
  
    -   **경로가 동일한 경우**  
  
         보조 복제본을 호스팅하는 컴퓨터에서 다음과 같이 전체 백업을 복원합니다.  
  
        ```  
        RESTORE DATABASE MyDB1   
            FROM DISK = 'C:\MyDB1.bak'   
            WITH NORECOVERY  
        GO  
        ```  
  
    -   **경로가 다른 경우**  
  
         보조 데이터베이스의 경로와 주 데이터베이스의 경로가 다른 경우(예: 드라이브 문자가 다른 경우) 보조 데이터베이스를 만들 때 복원 작업에 MOVE 절을 포함해야 합니다.  
  
        > [!IMPORTANT]  
        >  주 데이터베이스와 보조 데이터베이스의 경로 이름이 다른 경우 파일을 추가할 수 없습니다. 이는 파일 추가 작업에 대한 로그를 받을 때 보조 복제본의 서버 인스턴스가 주 데이터베이스에서 사용되는 것과 동일한 경로에 새 파일을 배치하기 때문입니다.  
  
         예를 들어 다음 명령은 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]의 기본 인스턴스에 대한 데이터 디렉터리(C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA)에 있는 주 데이터베이스의 백업을 복원합니다. 데이터베이스 복원 작업에서는 다른 클러스터 노드에 있는 보조 복제본을 호스트하는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] Always On1*이라는*의 원격 인스턴스에 대한 디렉터리로 데이터베이스를 이동해야 합니다. 데이터 및 로그 파일이 *C:\Program Files\Microsoft SQL Server\MSSQL13.Always On1\MSSQL\DATA* 디렉터리에 복원됩니다. 복원 작업에서는 WITH NORECOVERY를 사용하여 보조 데이터베이스를 복원 중인 데이터베이스에 그대로 둡니다.  
  
        ```  
        RESTORE DATABASE MyDB1  
          FROM DISK='C:\MyDB1.bak'  
         WITH NORECOVERY,   
            MOVE 'MyDB1_Data' TO   
             'C:\Program Files\Microsoft SQL Server\MSSQL13.Always On1\MSSQL\DATA\MyDB1_Data.mdf',   
            MOVE 'MyDB1_Log' TO  
             'C:\Program Files\Microsoft SQL Server\MSSQL13.Always On1\MSSQL\DATA\MyDB1_Data.ldf';  
        GO  
        ```  
  
5.  전체 백업을 복원한 후 주 데이터베이스에서 로그 백업을 만들어야 합니다. 예를 들어 다음 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문은 로그를 *E:\MyDB1_log.bak*라는 백업 파일에 백업합니다.  
  
    ```  
    BACKUP LOG MyDB1   
      TO DISK = 'E:\MyDB1_log.bak'   
    GO  
    ```  
  
6.  데이터베이스를 보조 복제본에 조인하려면 필수 로그 백업과 모든 후속 로그 백업을 적용해야 합니다.  
  
     예를 들어 다음 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문은 *C:\MyDB1.bak*에서 첫 번째 로그를 복원합니다.  
  
    ```  
    RESTORE LOG MyDB1   
      FROM DISK = 'E:\MyDB1_log.bak'   
        WITH FILE=1, NORECOVERY  
    GO  
    ```  
  
7.  데이터베이스에서 보조 복제본을 조인하기 전에 추가 로그 백업이 수행되면 해당 로그 백업도 RESTORE WITH NORECOVERY를 사용하여 보조 복제본을 호스팅하는 서버 인스턴스에 순서대로 복원해야 합니다.  
  
     예를 들어 다음 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문은 *E:\MyDB1_log.bak*에서 두 개의 로그를 추가로 복원합니다.  
  
    ```  
    RESTORE LOG MyDB1   
      FROM DISK = 'E:\MyDB1_log.bak'   
        WITH FILE=2, NORECOVERY  
    GO  
    RESTORE LOG MyDB1   
      FROM DISK = 'E:\MyDB1_log.bak'   
        WITH FILE=3, NORECOVERY  
    GO  
    ```  
  
##  <a name="PowerShellProcedure"></a> PowerShell 사용  
 **보조 데이터베이스를 준비하려면**  
  
1.  주 데이터베이스의 최근 백업을 만들어야 하는 경우 주 복제본을 호스트하는 서버 인스턴스로 디렉터리를 변경(**cd**)합니다.  
  
2.  **Backup-SqlDatabase** cmdlet을 사용하여 각 백업을 만듭니다.  
  
3.  보조 복제본을 호스팅하는 서버 인스턴스로 디렉터리를 변경(**cd**)합니다.  
  
4.  각 주 데이터베이스의 데이터베이스와 로그 백업을 복원하려면 **NoRecovery** 복원 매개 변수를 지정하여 **restore-SqlDatabase** cmdlet을 사용합니다. 또한 주 복제본을 호스팅하는 컴퓨터와 대상 보조 복제본을 호스팅하는 컴퓨터의 파일 경로가 다른 경우 **RelocateFile** 복원 매개 변수를 사용합니다.  
  
    > [!NOTE]  
    >  cmdlet의 구문을 보려면 **PowerShell 환경에서** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cmdlet을 사용합니다. 자세한 내용은 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)을 참조하세요.  
  
5.  보조 데이터베이스 구성을 완료하려면 보조 데이터베이스를 가용성 그룹에 조인해야 합니다. 자세한 내용은 [가용성 그룹에 보조 데이터베이스 조인&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)을 참조하세요.  
  
 **SQL Server PowerShell 공급자를 설정하고 사용하려면**  
  
-   [SQL Server PowerShell 공급자](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
###  <a name="ExamplePSscript"></a> 예제 백업 및 복원 스크립트와 명령  
 다음 PowerShell 명령은 전체 데이터베이스 백업과 트랜잭션 로그를 네트워크 공유에 백업하고 해당 공유에서 백업을 복원합니다. 이 예에서는 데이터베이스를 복원할 파일 경로가 데이터베이스를 백업한 파일 경로와 동일한 것으로 가정합니다.  
  
```  
# Create database backup  
Backup-SqlDatabase -Database "MyDB1" -BackupFile "\\share\backups\MyDB1.bak" -ServerInstance "SourceMachine\Instance"  
# Create log backup  
Backup-SqlDatabase -Database "MyDB1" -BackupAction "Log" -BackupFile "\\share\backups\MyDB1.trn" -ServerInstance "SourceMachine\Instance"  
# Restore database backup   
Restore-SqlDatabase -Database "MyDB1" -BackupFile "\\share\backups\MyDB1.bak" -NoRecovery -ServerInstance "DestinationMachine\Instance"  
# Restore log backup   
Restore-SqlDatabase -Database "MyDB1" -BackupFile "\\share\backups\MyDB1.trn" -RestoreAction "Log" -NoRecovery –ServerInstance "DestinationMachine\Instance"  
  
```  
  
##  <a name="FollowUp"></a> 다음 단계  
 보조 데이터베이스 구성을 완료하려면 새로 복원한 데이터베이스를 가용성 그룹에 조인합니다. 자세한 내용은 [가용성 그룹에 보조 데이터베이스 조인&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)인스턴스에 AlwaysOn 가용성 그룹을 만드는 방법을 설명합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [BACKUP&#40;Transact-SQL&#41;](../../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE 인수&#40;Transact-SQL&#41;](../../../t-sql/statements/restore-statements-arguments-transact-sql.md)   
 [RESTORE&#40;Transact-SQL&#41;](../../../t-sql/statements/restore-statements-transact-sql.md)   
 [실패한 파일 추가 작업 문제 해결&#40;Always On 가용성 그룹&#41;](../../../database-engine/availability-groups/windows/troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
  
