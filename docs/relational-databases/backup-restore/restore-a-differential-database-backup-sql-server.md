---
title: "차등 데이터베이스 백업 복원(SQL Server) | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- full differential backups [SQL Server]
- restoring databases [SQL Server], full differential backups
- database backups [SQL Server], full differential backups
- database restores [SQL Server], full differential backups
- backing up databases [SQL Server], full differential backups
ms.assetid: 0dd971a4-ee38-4dd3-9f30-ef77fc58dd11
caps.latest.revision: "46"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: d1d40ffcd25c8a6e72e364f93167a1747dd932fb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="restore-a-differential-database-backup-sql-server"></a>차등 데이터베이스 백업 복원(SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 차등 데이터베이스 백업을 복원하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [제한 사항](#Restrictions)  
  
     [필수 구성 요소](#Prerequisites)  
  
     [보안](#Security)  
  
-   **차등 데이터베이스 백업을 복원하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [관련 태스크](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   RESTORE는 명시적 또는 암시적 트랜잭션에서 사용할 수 없습니다.  
  
-   최신 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 만든 백업은 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 복원할 수 없습니다.  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전을 사용하여 만든 데이터베이스 백업에서 사용자 데이터베이스를 복원할 수 있습니다.  
  
###  <a name="Prerequisites"></a> 필수 구성 요소  
  
-   전체 복구 모델 또는 대량 로그 복구 모델의 경우 데이터베이스를 복원하려면 먼저 활성 트랜잭션 로그(비상 로그라고도 함)를 백업해야 합니다. 자세한 내용은 [트랜잭션 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)에 미러 데이터베이스를 준비하는 방법에 대해 설명합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 복원할 데이터베이스가 없으면 CREATE DATABASE 권한이 있어야 RESTORE를 실행할 수 있습니다. 데이터베이스가 있으면 RESTORE 권한은 기본적으로 **sysadmin** 및 **dbcreator** 고정 서버 역할의 멤버와 데이터베이스의 소유자(**dbo**)에 설정됩니다. FROM DATABASE_SNAPSHOT 옵션의 경우 데이터베이스가 항상 있습니다.  
  
 멤버 자격 정보를 서버에서 항상 사용할 수 있는 역할에 RESTORE 권한이 제공됩니다. 고정 데이터베이스 역할의 멤버 자격은 데이터베이스가 액세스 가능한 상태이며 손상되지 않은 경우에만 확인할 수 있는데, RESTORE 실행 시 데이터베이스가 항상 이러한 상태인 것은 아니므로 **db_owner** 고정 데이터베이스 역할의 멤버에게는 RESTORE 권한이 없습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-restore-a-differential-database-backup"></a>차등 데이터베이스 백업을 복원하려면  
  
1.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 해당 인스턴스에 연결한 다음 개체 탐색기에서 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
2.  **데이터베이스**를 확장합니다. 데이터베이스에 따라 사용자 데이터베이스를 선택하거나 **시스템 데이터베이스**를 확장한 다음 시스템 데이터베이스를 선택합니다.  
  
3.  데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**를 가리킨 다음 **복원**을 가리키고 **데이터베이스**를 클릭합니다.  
  
4.  **일반** 페이지에서 **원본** 섹션을 사용하여 복원할 백업 집합의 원본과 위치를 지정합니다. 다음 옵션 중 하나를 선택합니다.  
  
    -   **데이터베이스**  
  
         복원할 데이터베이스를 드롭다운 목록에서 선택합니다. 목록에는 **msdb** 백업 기록에 따라 백업된 데이터베이스만 포함되어 있습니다.  
  
    > [!NOTE]  
    >  백업을 다른 서버에서 가져온 경우 대상 서버에 지정한 데이터베이스에 대한 백업 기록 정보가 없습니다. 이 경우 **장치** 를 선택하여 복원할 파일이나 장치를 수동으로 지정합니다.  
  
    -   **장치**  
  
         찾아보기(**...**) 단추를 클릭하여 **백업 장치 선택** 대화 상자를 엽니다. **백업 미디어 유형** 상자에서 나열된 장치 유형 중 하나를 선택합니다. **백업 미디어** 상자에 대해 하나 이상의 장치를 선택하려면 **추가**를 클릭합니다.  
  
         원하는 장치를 **백업 미디어** 목록 상자에 추가한 후 **확인** 을 클릭하여 **일반** 페이지로 돌아갑니다.  
  
         **원본: 장치: 데이터베이스** 목록 상자에서 복원할 데이터베이스의 이름을 선택합니다.  
  
         **참고** 이 목록은 **장치** 를 선택한 경우에만 사용할 수 있습니다. 선택한 장치에 백업이 있는 데이터베이스만 사용할 수 있습니다.  
  
5.  **대상** 섹션의 **데이터베이스** 상자에는 복원할 데이터베이스의 이름이 자동으로 채워집니다. 데이터베이스의 이름을 변경하려면 **데이터베이스** 상자에 새 이름을 입력합니다.  
  
    > [!NOTE]  
    >  특정 시점에 복원을 중지하려면 **시간대** 를 클릭하여 **백업 시간대** 대화 상자에 액세스합니다. 특정 시점의 데이터베이스 복원 중지에 대한 도움말은 [SQL Server 데이터베이스를 지정 시간으로 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)을 참조하세요.  
  
6.  **복원에 사용할 백업 세트** 표에서 차등 백업을 통해 복원할 백업을 선택합니다.  
  
     **복원에 사용할 백업 세트** 표의 열에 대한 자세한 내용은 [데이터베이스 복원&#40;일반 페이지&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)을 참조하세요.  
  
7.  상황에 따라 **옵션** 페이지의 **복원 옵션** 패널에서 다음 옵션 중 하나를 선택할 수 있습니다.  
  
    -   **기존 데이터베이스 덮어쓰기(WITH REPLACE)**  
  
    -   **복제 설정 유지(WITH KEEP_REPLICATION)**  
  
    -   **각 백업 복원 전에 확인**  
  
    -   **복원된 데이터베이스에 대한 액세스 제한(WITH RESTRICTED_USER)**  
  
     이러한 옵션에 대한 자세한 내용은 [데이터베이스 복원&#40;옵션 페이지&#41;](../../relational-databases/backup-restore/restore-database-options-page.md)을 참조하세요.  
  
8.  **복구 상태** 상자에 대한 옵션을 선택합니다. 이 상자에서 복원 작업 후 데이터베이스의 상태를 확인합니다.  
  
    -   **RESTORE WITH RECOVERY** 는 커밋되지 않은 트랜잭션을 롤백하여 데이터베이스를 사용 준비가 된 상태로 유지하는 기본 동작입니다. 추가 트랜잭션 로그를 복원할 수 없습니다. 필요한 모든 백업을 지금 복원하는 경우 이 옵션을 선택합니다.  
  
    -   **RESTORE WITH NORECOVERY** 는 데이터베이스를 비작동 상태로 유지하고 커밋되지 않은 트랜잭션을 롤백하지 않습니다. 추가 트랜잭션 로그를 복원할 수 데이터베이스는 복구할 때까지 사용할 수 없습니다.  
  
    -   **RESTORE WITH STANDBY** 는 읽기 전용 모드로 데이터베이스를 유지합니다. 이 옵션은 커밋되지 않은 트랜잭션의 실행을 취소하지만, 복구 결과를 되돌릴 수 있도록 실행 취소 동작을 대기 파일에 저장합니다.  
  
     옵션에 대한 설명은 [데이터베이스 복원&#40;옵션 페이지&#41;](../../relational-databases/backup-restore/restore-database-options-page.md)을 참조하세요.  
  
9. 데이터베이스에 대한 활성 연결이 있으면 복원 작업이 실패합니다. **기존 연결 닫기** 옵션을 선택하여 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 와 데이터베이스 간의 모든 활성 연결을 닫습니다.  
  
10. 각 복원 작업 사이에 확인 메시지를 표시하려면 **각 백업 복원 전에 확인** 을 선택합니다. 데이터베이스가 크고 복원 작업의 상태를 모니터링하려는 경우가 아니면 이 옵션은 일반적으로 필요하지 않습니다.  
  
11. 필요에 따라 **파일** 페이지를 사용하여 데이터베이스를 새 위치로 복원합니다. 데이터베이스 이동과 관련된 도움말을 보려면 [데이터베이스를 새 위치로 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)을 참조하세요.  
  
12. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-restore-a-differential-database-backup"></a>차등 데이터베이스 백업을 복원하려면  
  
1.  NORECOVERY 절을 지정하고 RESTORE DATABASE 문을 실행하여 차등 데이터베이스 백업에 앞서 전체 데이터베이스 백업을 복원합니다. 자세한 내용은 [방법: 전체 백업 복원](../../relational-databases/backup-restore/restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)을 참조하세요.  
  
2.  RESTORE DATABASE 문을 실행하여 차등 데이터베이스 백업을 복원합니다. 이때 다음을 지정합니다.  
  
    -   차등 데이터베이스 백업이 적용될 데이터베이스의 이름  
  
    -   차등 데이터베이스 백업을 복원하는 백업 장치  
  
    -   차등 데이터베이스 백업이 복원된 후 적용할 트랜잭션 로그 백업이 있을 경우 NORECOVERY 절, 그렇지 않으면 RECOVERY 절  
  
3.  전체 복구 모델이나 대량 로그 복구 모델을 사용할 경우 차등 데이터베이스 백업을 복원하면 차등 데이터베이스 백업이 완료된 시점까지 데이터베이스가 복원됩니다. 오류 지점까지 복구하려면 마지막 차등 데이터베이스 백업이 생성된 후에 만든 트랜잭션 로그 백업을 모두 적용해야 합니다. 자세한 내용은 [트랜잭션 로그 백업 적용&#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)을 참조하세요.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
  
#### <a name="a-restoring-a-differential-database-backup"></a>1. 차등 데이터베이스 백업 복원  
 다음은 `MyAdvWorks` 데이터베이스의 데이터베이스 및 차등 데이터베이스 백업을 복원하는 예입니다.  
  
```tsql  
-- Assume the database is lost, and restore full database,   
-- specifying the original full database backup and NORECOVERY,   
-- which allows subsequent restore operations to proceed.  
RESTORE DATABASE MyAdvWorks  
   FROM MyAdvWorks_1  
   WITH NORECOVERY;  
GO  
-- Now restore the differential database backup, the second backup on   
-- the MyAdvWorks_1 backup device.  
RESTORE DATABASE MyAdvWorks  
   FROM MyAdvWorks_1  
   WITH FILE = 2,  
   RECOVERY;  
GO  
```  
  
#### <a name="b-restoring-a-database-differential-database-and-transaction-log-backup"></a>2. 데이터베이스, 차등 데이터베이스, 트랜잭션 로그 백업 복원  
 다음은 `MyAdvWorks` 데이터베이스의 데이터베이스, 차등 데이터베이스 및 트랜잭션 로그 백업을 복원하는 예입니다.  
  
```tsql  
-- Assume the database is lost at this point. Now restore the full   
-- database. Specify the original full database backup and NORECOVERY.  
-- NORECOVERY allows subsequent restore operations to proceed.  
RESTORE DATABASE MyAdvWorks  
   FROM MyAdvWorks_1  
   WITH NORECOVERY;  
GO  
-- Now restore the differential database backup, the second backup on   
-- the MyAdvWorks_1 backup device.  
RESTORE DATABASE MyAdvWorks  
   FROM MyAdvWorks_1  
   WITH FILE = 2,  
   NORECOVERY;  
GO  
-- Now restore each transaction log backup created after  
-- the differential database backup.  
RESTORE LOG MyAdvWorks  
   FROM MyAdvWorks_log1  
   WITH NORECOVERY;  
GO  
RESTORE LOG MyAdvWorks  
   FROM MyAdvWorks_log2  
   WITH RECOVERY;  
GO  
```  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [차등 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
-   [트랜잭션 로그 백업 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [차등 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)   
 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
