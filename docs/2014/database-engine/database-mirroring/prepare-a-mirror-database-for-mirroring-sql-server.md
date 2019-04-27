---
title: 미러 데이터베이스의 미러링 준비(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], preparing for mirroring
- logins [SQL Server], database mirroring
- mirror database [SQL Server]
ms.assetid: 8676f9d8-c451-419b-b934-786997d46c2b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 844879c0e1b02bc9b6fd88ab153cb2a5dbd6ebe6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62754780"
---
# <a name="prepare-a-mirror-database-for-mirroring-sql-server"></a>미러 데이터베이스의 미러링 준비(SQL Server)
  데이터베이스 미러링 세션을 시작하기 전에 데이터베이스 소유자나 시스템 관리자는 미러 데이터베이스가 생성되었으며 미러링 준비가 완료되었는지 확인해야 합니다. 새 미러 데이터베이스를 만들려면 최소한 주 데이터베이스의 전체 백업과 후속 로그 백업이 필요하며 WITH NORECOVERY를 사용하여 두 백업을 모두 미러 서버 인스턴스로 복원해야 합니다.  
  
 이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에 미러 데이터베이스를 준비하는 방법에 대해 설명합니다.  
  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Requirements"></a> 요구 사항  
  
-   주 서버와 미러 서버 인스턴스가 같은 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 실행되고 있어야 합니다. 미러 서버에 상위 버전의 SQL Server가 있을 수 있지만 이 구성은 세심하게 계획된 업그레이드 프로세스 중에만 권장됩니다. 이 구성에서 자동 장애 조치(failover)가 발생할 수 있습니다. 이 경우 데이터를 하위 버전의 SQL Server로 옮길 수 없으므로 데이터 이동이 자동으로 중지됩니다. 자세한 내용은 [서버 인스턴스 업그레이드 시 미러된 데이터베이스의 작동 중단 최소화](upgrading-mirrored-instances.md)을 참조하세요.  
  
-   주 서버와 미러 서버 인스턴스가 같은 에디션의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 실행되고 있어야 합니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 데이터베이스 미러링 지원에 대한 자세한 내용은 [SQL Server 2014 버전에서 지원하는 기능](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)을 참조하세요.  
  
-   이 데이터베이스는 전체 복구 모델을 사용해야 합니다.  
  
     자세한 내용은 [데이터베이스 복구 모델 보기 또는 변경&#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md) 또는 [sys.databases&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) 및 [ALTER DATABASE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)를 참조하세요.  
  
-   미러 데이터베이스의 이름은 주 데이터베이스의 이름과 같아야 합니다.  
  
-   미러링이 작동하려면 미러 데이터베이스가 RESTORING 상태여야 합니다. 미러 데이터베이스를 준비할 때는 모든 복원 작업에 대해 RESTORE WITH NORECOVERY를 사용해야 합니다. 최소한 NORECOVERY를 사용하여 주 데이터베이스의 전체 백업을 복원하고 이후의 모든 로그 백업을 복원해야 합니다.  
  
-   미러 데이터베이스를 만들려는 시스템에 미러 데이터베이스를 저장할 공간이 충분한 디스크 드라이브가 있어야 합니다.  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   **master**, **msdb**, **temp**또는 **model** 시스템 데이터베이스는 미러링할 수 없습니다.  
  
-   에 속한 데이터베이스는 미러링할 수 없습니다는 [AlwaysOn 가용성 그룹 (SQL Server)](../availability-groups/windows/always-on-availability-groups-sql-server.md)합니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   주 데이터베이스의 아주 최근 전체 데이터베이스 백업 또는 최근 차등 데이터베이스 백업을 사용합니다.  
  
-   로그 백업 작업이 주 데이터베이스에서 자주 실행되도록 예약한 경우 미러링이 시작할 때까지 백업 작업을 사용하지 않도록 설정해야 할 수 있습니다.  
  
-   가능한 경우 드라이브 문자를 포함한 미러 데이터베이스의 경로가 주 데이터베이스의 경로와 같아야 합니다.  
  
     주 데이터베이스는 'F:' 드라이브에 있는데 미러 시스템에는 F: 드라이브가 없는 경우 등 파일 경로가 달라야 하는 경우에는 RESTORE STATEMENT에 MOVE 옵션을 포함해야 합니다.  
  
    > [!IMPORTANT]  
    >  미러링 세션에 영향을 주지 않고 해당 세션 중 파일을 추가하려면 파일의 경로가 두 서버 모두에 있어야 합니다. 따라서 미러 데이터베이스를 만들 때 데이터베이스 파일을 이동하면 나중에 미러 데이터베이스에 파일을 추가할 수 없고 미러링이 일시 중지될 수 있습니다. 실패한 파일 생성 작업을 처리하는 방법은 [데이터베이스 미러링 구성 문제 해결&#40;SQL Server&#41;](troubleshoot-database-mirroring-configuration-sql-server.md)을 참조하세요.  
  
-   주 데이터베이스에 전체 텍스트 카탈로그가 있는 경우 [데이터베이스 미러링 및 전체 텍스트 카탈로그&#40;SQL Server&#41;](database-mirroring-and-full-text-catalogs-sql-server.md)를 참조하는 것이 좋습니다.  
  
-   프로덕션 데이터베이스의 경우에는 항상 별도의 디바이스에 백업해야 합니다.  
  
###  <a name="Security"></a> 보안  
 데이터베이스를 백업하면 TRUSTWORTHY가 OFF로 설정됩니다. 따라서 새 미러 데이터베이스의 TRUSTWORTHY는 항상 OFF입니다. 장애 조치(Failover) 후 데이터베이스를 신뢰할 수 있어야 하는 경우에는 추가 설정 단계가 필요합니다. 자세한 내용은 [Trustworthy 속성을 사용하도록 미러 데이터베이스 설정&#40;Transact-SQL&#41;](set-up-a-mirror-database-to-use-the-trustworthy-property-transact-sql.md)에 미러 데이터베이스를 준비하는 방법에 대해 설명합니다.  
  
 미러 데이터베이스의 데이터베이스 마스터 키 자동 암호 해독을 설정하는 방법은 [암호화된 미러 데이터베이스 설정](set-up-an-encrypted-mirror-database.md)을 참조하세요.  
  
####  <a name="Permissions"></a> Permissions  
 데이터베이스 소유자 또는 시스템 관리자입니다.  
  
##  <a name="PrepareToRestartMirroring"></a> 미러링을 다시 시작하기 위해 기존 미러 데이터베이스를 준비하려면  
 미러링이 제거되었고 미러 데이터베이스가 아직 RECOVERING 상태인 경우 미러링을 다시 시작할 수 있습니다.  
  
1.  주 데이터베이스에서 하나 이상의 로그 백업을 수행합니다. 자세한 내용은 [트랜잭션 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)에 미러 데이터베이스를 준비하는 방법에 대해 설명합니다.  
  
2.  미러 데이터베이스에서 RESTORE WITH NORECOVERY를 사용하여, 미러링이 제거된 후에 주 데이터베이스에서 수행한 모든 로그 백업을 복원합니다. 자세한 내용은 [트랜잭션 로그 백업 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)에 미러 데이터베이스를 준비하는 방법에 대해 설명합니다.  
  
##  <a name="CombinedProcedure"></a> 새 미러 데이터베이스를 준비하려면  
 **미러 데이터베이스를 준비하려면**  
  
> [!NOTE]  
>  이 절차에 대한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 예는 이 섹션의 뒷부분에 나오는 [예(Transact-SQL)](#TsqlExample)를 참조하세요.  
  
1.  주 서버 인스턴스에 연결합니다.  
  
2.  주 데이터베이스의 전체 데이터베이스 백업 또는 차등 데이터베이스 백업을 만듭니다.  
  
    -   [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
    -   [차등 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
3.  일반적으로 주 데이터베이스에서 하나 이상의 로그 백업을 수행해야 합니다. 그러나 데이터베이스를 방금 만들었으며 아직 로그 백업이 수행되지 않은 경우 또는 복구 모델이 방금 SIMPLE에서 FULL로 변경된 경우에는 로그 백업이 필요하지 않을 수도 있습니다.  
  
    -   [트랜잭션 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
4.  두 시스템에서 액세스할 수 있는 네트워크 드라이브에 백업이 있지 않으면 데이터베이스 백업과 로그 백업을 미러 서버 인스턴스를 호스팅할 시스템에 복사합니다.  
  
5.  미러 서버 인스턴스에 연결합니다.  
  
6.  RESTORE WITH NORECOVERY를 통해 전체 데이터베이스 백업 및 필요에 따라 가장 최근의 차등 데이터베이스 백업을 미러 서버 인스턴스에 복원하여 미러 데이터베이스를 만듭니다.  
  
    > [!NOTE]  
    >  파일 그룹별로 데이터베이스 파일 그룹을 복원하는 경우에는 전체 데이터베이스를 복원해야 합니다.  
  
    -   [데이터베이스 백업 복원 &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
    -   [RESTORE&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql) 및 [RESTORE 인수&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql)에 미러 데이터베이스를 준비하는 방법에 대해 설명합니다.  
  
7.  RESTORE WITH NORECOVERY를 사용하여 처리 중인 로그 백업을 미러 데이터베이스에 적용합니다.  
  
    -   [트랜잭션 로그 백업 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 데이터베이스 미러링 세션이 시작되기 전에 미러 데이터베이스를 만들어야 합니다. 이 작업은 미러링 세션을 시작하기 직전에 수행해야 합니다.  
  
 이 예에서는 기본적으로 단순 복구 모델을 사용하는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예제 데이터베이스를 사용합니다.  
  
1.  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에서 데이터베이스 미러링을 사용하려면 전체 복구 모델을 사용하도록 수정합니다.  
  
    ```  
    USE master;  
    GO  
    ALTER DATABASE AdventureWorks   
    SET RECOVERY FULL;  
    GO  
    ```  
  
2.  데이터베이스 복구 모델을 SIMPLE에서 FULL로 변경한 후 미러 데이터베이스를 만드는 데 사용할 수 있는 전체 백업을 만듭니다. 복구 모델이 방금 변경되었으므로 WITH FORMAT 옵션을 지정하여 새 미디어 세트를 만듭니다. 이 옵션은 단순 복구 모델에서 만든 이전 백업과 전체 복구 모델에서 만든 백업을 구분하는 데 유용합니다. 이 예에서는 백업 파일(`C:\AdventureWorks.bak`)이 데이터베이스와 같은 드라이브에서 생성됩니다.  
  
    > [!NOTE]  
    >  프로덕션 데이터베이스의 경우에는 항상 별도의 디바이스에 백업해야 합니다.  
  
     `PARTNERHOST1`의 주 서버 인스턴스에서 주 데이터베이스의 전체 백업을 다음과 같이 만듭니다.  
  
    ```  
    BACKUP DATABASE AdventureWorks   
        TO DISK = 'C:\AdventureWorks.bak'   
        WITH FORMAT  
    GO  
    ```  
  
3.  전체 백업을 미러 서버에 복사합니다.  
  
4.  RESTORE WITH NORECOVERY를 사용하여 전체 백업을 미러 서버 인스턴스에 복원합니다. 복원 명령은 주 데이터베이스와 미러 데이터베이스의 경로가 동일한지 여부에 따라 달라집니다.  
  
    -   **경로가 동일한 경우**  
  
         `PARTNERHOST5`의 미러 서버 인스턴스에서 전체 백업을 다음과 같이 복원합니다.  
  
        ```  
        RESTORE DATABASE AdventureWorks   
            FROM DISK = 'C:\AdventureWorks.bak'   
            WITH NORECOVERY  
        GO  
        ```  
  
    -   **경로가 다른 경우**  
  
         미러 데이터베이스의 경로와 주 데이터베이스의 경로가 다른 경우(예: 드라이브 문자가 다른 경우) 미러 데이터베이스를 만들 때 복원 작업에 MOVE 절을 포함해야 합니다.  
  
        > [!IMPORTANT]  
        >  주 데이터베이스 및 미러 데이터베이스의 경로 이름이 다른 경우 파일을 추가할 수 없습니다. 이는 파일 추가 작업에 대한 로그를 받을 때 미러 서버 인스턴스가 주 데이터베이스에서 사용하는 위치에 새 파일을 배치하기 때문입니다.  
  
         예를 들어 다음 명령은 C:\Program Files\Microsoft SQL Server\MSSQL.*n*\MSSQL\Data\에 있는 주 데이터베이스의 백업을 미러 데이터베이스가 배치될 다른 위치인 D:\Program Files\Microsoft SQL Server\MSSQL.*n*\MSSQL\Dat`a\`로 복원합니다.  
  
        ```  
        RESTORE DATABASE AdventureWorks  
           FROM DISK='C:\AdventureWorks.bak'  
           WITH NORECOVERY,   
              MOVE 'AdventureWorks_Data' TO   
                 'D:\Program Files\Microsoft SQL Server\MSSQL.n\MSSQL\Data\AdventureWorks_Data.mdf',   
              MOVE 'AdventureWorks_Log' TO  
                 'D:\Program Files\Microsoft SQL Server\MSSQL.n\MSSQL\Data\AdventureWorks_Log.ldf';  
        GO  
        ```  
  
5.  전체 백업을 만든 후 주 데이터베이스에서 로그 백업을 만들어야 합니다. 예를 들어 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 앞의 전체 백업에 사용된 파일에 로그를 백업합니다.  
  
    ```  
    BACKUP LOG AdventureWorks   
        TO DISK = 'C:\AdventureWorks.bak'   
    GO  
    ```  
  
6.  미러링을 시작하기 전에 필수 로그 백업 및 모든 후속 로그 백업을 적용해야 합니다.  
  
     예를 들어 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 `C:\AdventureWorks.bak`에서 첫 번째 로그를 복원합니다.  
  
    ```  
    RESTORE LOG AdventureWorks   
        FROM DISK = 'C:\AdventureWorks.bak'   
        WITH FILE=1, NORECOVERY  
    GO  
    ```  
  
7.  미러링을 시작하기 전에 추가 로그 백업이 수행되면 이러한 로그 백업도 WITH NORECOVERY를 사용하여 순서대로 미러 서버로 복원해야 합니다.  
  
     예를 들어 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 `C:\AdventureWorks.bak`에서 두 개의 로그를 추가로 복원합니다.  
  
    ```  
    RESTORE LOG AdventureWorks   
        FROM DISK = 'C:\AdventureWorks.bak'   
        WITH FILE=2, NORECOVERY  
    GO  
    RESTORE LOG AdventureWorks   
        FROM DISK = 'C:\AdventureWorks.bak'   
        WITH FILE=3, NORECOVERY  
    GO  
    ```  
  
 보안 설정 표시, 미러 데이터베이스 준비, 파트너 설정 및 미러링 모니터 서버 추가 등의 작업을 수행하는 전체 예제는 [데이터베이스 미러링 설정&#40;SQL Server&#41;](database-mirroring-sql-server.md)에 미러 데이터베이스를 준비하는 방법에 대해 설명합니다.  
  
##  <a name="FollowUp"></a> 후속 작업: 미러 데이터베이스를 준비한 후  
  
1.  대부분의 최근 RESTORE LOG 작업을 수행한 이후 추가 로그 백업이 수행된 경우 RESTORE WITH NORECOVERY를 사용하여 모든 추가 로그 백업을 수동으로 적용해야 합니다.  
  
2.  미러링 추적을 시작합니다. 자세한 내용은 [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md) 을 사용하여 [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;Transact-SQL&#41;](database-mirroring-establish-session-windows-authentication.md)에 미러 데이터베이스를 준비하는 방법에 대해 설명합니다.  
  
3.  주 데이터베이스에서 백업 작업을 해제한 경우 작업을 다시 설정합니다.  
  
4.  장애 조치(Failover) 후 데이터베이스를 신뢰할 수 있어야 하는 경우에는 미러링이 시작된 다음 추가 설정 단계가 필요합니다. 자세한 내용은 [Trustworthy 속성을 사용하도록 미러 데이터베이스 설정&#40;Transact-SQL&#41;](set-up-a-mirror-database-to-use-the-trustworthy-property-transact-sql.md)에 미러 데이터베이스를 준비하는 방법에 대해 설명합니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [트랜잭션 로그 백업 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
-   [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
-   [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;Transact-SQL&#41;](database-mirroring-establish-session-windows-authentication.md)  
  
-   [암호화된 미러 데이터베이스 설정](set-up-an-encrypted-mirror-database.md)  
  
-   [Trustworthy 속성을 사용하도록 미러 데이터베이스 설정&#40;Transact-SQL&#41;](set-up-a-mirror-database-to-use-the-trustworthy-property-transact-sql.md)  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 미러링&#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [데이터베이스 미러링 및 AlwaysOn 가용성 그룹에 대 한 전송 보안 &#40;SQL Server&#41;](transport-security-database-mirroring-always-on-availability.md)   
 [데이터베이스 미러링 설정&#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [전체 텍스트 카탈로그와 인덱스 백업 및 복원](../../relational-databases/indexes/indexes.md)   
 [데이터베이스 미러링 및 전체 텍스트 카탈로그&#40;SQL Server&#41;](database-mirroring-and-full-text-catalogs-sql-server.md)   
 [데이터베이스 미러링 및 복제&#40;SQL Server&#41;](database-mirroring-and-replication-sql-server.md)   
 [BACKUP&#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [RESTORE&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [RESTORE 인수&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql)  
  
  
