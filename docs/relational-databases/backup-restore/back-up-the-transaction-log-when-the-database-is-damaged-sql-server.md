---
title: "데이터베이스가 손상된 경우 트랜잭션 로그 백업(SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "데이터베이스 [SQL Server], 손상됨"
  - "백업 [SQL Server]. 손상된 데이터베이스"
  - "트랜잭션 로그 백업 [SQL Server], 손상된 데이터베이스"
ms.assetid: 9b8873cc-df54-4336-ab9b-8f525132c2b0
caps.latest.revision: 29
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 29
---
# 데이터베이스가 손상된 경우 트랜잭션 로그 백업(SQL Server)
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 데이터베이스가 손상되었을 때 트랜잭션 로그를 백업하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [제한 사항](#Restrictions)  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 데이터베이스가 손상되었을 때 트랜잭션 로그를 백업합니다.**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   명시적 또는 암시적 트랜잭션에서는 BACKUP 문을 사용할 수 없습니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   전체 또는 대량 로그 복구 모델을 사용하는 데이터베이스의 경우 대개 데이터베이스를 복원하기 전에 비상 로그를 백업해야 합니다. 또한 로그 전달 구성의 장애 조치를 수행하기 전에 주 데이터베이스의 비상 로그를 백업해야 합니다. 데이터베이스를 복구하기 전에 비상 로그 백업을 최종 로그 백업으로 복원하면 오류 후 작업 손실이 방지됩니다. 비상 로그 백업에 대한 자세한 내용은 [비상 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)을 참조하세요.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 BACKUP DATABASE 및 BACKUP LOG 권한은 기본적으로 **sysadmin** 고정 서버 역할과 **db_owner** 및 **db_backupoperator** 고정 데이터베이스 역할의 멤버로 설정됩니다.  
  
 백업 장치의 물리적 파일에서 발생하는 소유권과 사용 권한 문제는 백업 작업에 영향을 미칠 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 장치를 읽고 쓸 수 있어야 하므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스가 실행되는 계정에는 쓰기 권한이 있어야 합니다. 그러나 시스템 테이블의 백업 장치에 대한 항목을 추가하는 [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)는 파일 액세스 권한을 확인하지 않습니다. 백업 장치의 물리적 파일에서 발생하는 이러한 문제는 백업 또는 복원을 시도할 때 실제 리소스를 액세스하기 전까지는 발생하지 않습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### 트랜잭션 비상 로그를 백업하려면  
  
1.   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 해당 인스턴스에 연결한 다음 개체 탐색기에서 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 해당 데이터베이스에 따라 사용자 데이터베이스를 선택하거나 **시스템 데이터베이스** 를 확장한 다음 시스템 데이터베이스를 선택합니다.  
  
3.  데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**를 가리킨 다음 **백업**을 클릭합니다. **데이터베이스 백업** 대화 상자가 나타납니다.  
  
4.  **데이터베이스** 목록 상자에서 데이터베이스 이름을 확인합니다. 필요에 따라 목록에서 다른 데이터베이스를 선택할 수 있습니다.  
  
5.  복구 모델이 **FULL** 또는 **BULK_LOGGED**인지 확인합니다.  
  
6.  **백업 유형** 목록 상자에서 **트랜잭션 로그**를 선택합니다.  
  
7.  **복사 전용 백업** 을 선택하지 않은 상태로 둡니다.  
  
8.  **백업 세트** 영역에서 **이름** 입력란에 제시된 기본 백업 세트 이름을 사용하거나 다른 백업 세트 이름을 입력합니다.  
  
9. **설명** 입력란에 비상 로그 백업에 대한 설명을 입력합니다.  
  
10. 백업 세트가 만료될 시기를 다음과 같이 지정합니다.  
  
    -   백업 세트가 특정 일수가 지난 후에 만료되도록 하려면 **다음 이후**(기본 옵션)를 클릭한 다음 백업 세트를 만든 후 백업 세트가 만료되기까지 경과해야 하는 일수를 입력합니다. 이 값은 0일에서 99999일 사이일 수 있습니다. 값 0일은 백업 세트 기간 제한이 없음을 의미합니다.  
  
         기본값은 **서버 속성** 대화 상자(**데이터베이스 설정** 페이지)의 **백업 미디어 기본 보존 기간(일)** 옵션에 설정되어 있습니다. 이 대화 상자에 액세스하려면 개체 탐색기에서 서버 이름을 마우스 오른쪽 단추로 클릭하고 속성을 선택한 다음 **데이터베이스 설정** 페이지를 선택합니다.  
  
    -   백업 세트가 특정 일자에 만료되게 하려면 **날짜**를 클릭한 다음 백업 세트가 만료될 날짜를 입력합니다.  
  
11. **디스크** 나 **테이프**를 클릭하여 백업 대상 유형을 선택합니다. **추가**를 클릭하면 단일 미디어 세트를 포함하는 디스크나 테이프 드라이브에 대한 경로를 64개까지 선택할 수 있습니다. 선택한 경로는 **백업 대상** 목록 상자에 표시됩니다.  
  
     백업 대상을 제거하려면 해당 대상을 선택한 다음 **제거**를 클릭합니다. 백업 대상의 내용을 보려면 선택한 다음 **내용**을 클릭합니다.  
  
12. **옵션** 페이지에서 다음 중 하나를 클릭하여 **미디어 덮어쓰기** 옵션을 선택합니다.  
  
    -   **기존 미디어 세트에 백업**  
  
         이 옵션에는 **기존 백업 세트에 추가** 또는 **기존 백업 세트 모두 덮어쓰기**를 클릭합니다.  
  
         필요에 따라 **미디어 세트 이름 및 백업 세트 만료 확인** 을 선택하여 백업 작업에서 미디어 세트와 백업 세트가 만료되는 날짜와 시간을 확인하도록 합니다.  
  
         필요에 따라 **미디어 세트 이름** 입력란에 이름을 입력합니다. 이름을 지정하지 않는 경우 이름이 비어 있는 미디어 세트가 생성됩니다. 미디어 세트 이름을 지정하는 경우 미디어(테이프 또는 디스크)를 선택하여 실제 이름과 여기에서 입력한 이름이 일치하는지 여부를 확인합니다.  
  
         미디어 이름을 비워 두고 검사하도록 확인란을 선택한 경우 미디어에서 미디어 이름을 비워 두는 것과 같은 결과가 나타납니다.  
  
    -   **새 미디어 세트에 백업하고 기존 백업 세트 모두 지우기**  
  
         이 옵션에는 **새 미디어 세트 이름** 입력란에 이름을 입력하고 필요에 따라 **새 미디어 세트 설명** 입력란에 미디어 세트에 대한 설명을 입력합니다.  
  
     미디어 세트 옵션에 대한 자세한 내용은 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)를 참조하세요.  
  
13. **안정성** 섹션에서 필요에 따라 다음을 선택합니다.  
  
    -   **완료 시 백업 확인**  
  
    -   **미디어에 쓰기 전에 체크섬 수행**  
  
    -   **체크섬 오류 발생 시 계속**  
  
     체크섬에 대한 자세한 내용은 [백업 및 복원 중 발생 가능한 미디어 오류&#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)를 참조하세요.  
  
14. **트랜잭션 로그** 섹션에서 **비상 로그 백업을 수행하고 복원 중인 상태로 데이터베이스 유지**를 선택합니다.  
  
     이는 다음 [BACKUP](../../t-sql/statements/backup-transact-sql.md) 문을 지정하는 것과 같습니다.  
  
     `BACKUP LOG <database_name> TO <backup_device> WITH NORECOVERY`  
  
    > [!IMPORTANT]  
    >  복원 시 데이터베이스 복원 대화 상자에 비상 로그 백업의 유형이 **트랜잭션 로그(복사 전용)**로 표시됩니다.  
  
15. **일반** 페이지의 **대상** 섹션에서 지정한 대로 테이프 드라이브에 백업하는 경우 **백업 후 테이프 언로드** 옵션이 활성화됩니다. 이 옵션을 클릭하면 **언로드 전에 테이프 되감기** 옵션이 활성화됩니다.  
  
16. [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 이상에서는 [백업 압축](../../relational-databases/backup-restore/backup-compression-sql-server.md)을 지원합니다. 기본적으로 백업은 **백업-압축 기본값** 서버 구성 옵션의 값에 따라 압축됩니다. 그러나 현재 서버 수준 기본값에 관계없이 **백업 압축**을 선택하여 백업을 압축하고, **백업 압축 안 함**을 선택하여 압축을 방지할 수 있습니다.  
  
     **현재 백업 압축 기본값을 보려면**  
  
    -   [backup compression default 서버 구성 옵션 보기 또는 구성](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### 현재 활성화된 트랜잭션 로그의 백업을 만들려면  
  
1.  BACKUP LOG 문을 실행하여 현재 활성화되어 있는 트랜잭션 로그를 백업합니다. 이 때 다음을 지정합니다.  
  
    -   백업할 트랜잭션 로그가 속한 데이터베이스의 이름  
  
    -   트랜잭션 로그 백업이 기록될 백업 장치  
  
    -   NO_TRUNCATE 절  
  
         트랜잭션 로그 파일이 액세스 가능하며 손상되지 않은 경우 이 절을 사용하면 데이터베이스에 액세스할 수 없는 경우에도 트랜잭션 로그의 활성 부분을 백업할 수 있습니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
  
> [!NOTE]  
>  이 예에서는 단순 복구 모델을 사용하는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]를 사용합니다. 로그 백업을 허용하기 위해 전체 데이터베이스를 백업하기 전에 전체 복구 모델을 사용하도록 데이터베이스를 설정했습니다. 자세한 내용은 [데이터베이스 복구 모델 보기 또는 변경&#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)을 참조하세요.  
  
 이 예에서는 데이터베이스가 손상되어 액세스할 수 없고 트랜잭션 로그가 손상되지 않았고 액세스할 수 있는 경우 현재 활성 트랜잭션 로그를 백업합니다.  
  
```scr  
BACKUP LOG AdventureWorks2012  
   TO MyAdvWorks_FullRM_log1  
   WITH NO_TRUNCATE;  
GO  
```  
  
## 참고 항목  
 [트랜잭션 로그 백업 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)   
 [SQL Server 데이터베이스를 지정 시간으로 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)   
 [데이터베이스 백업&#40;백업 옵션 페이지&#41;](../../relational-databases/backup-restore/back-up-database-backup-options-page.md)   
 [데이터베이스 백업&#40;일반 페이지&#41;](../../relational-databases/backup-restore/back-up-database-general-page.md)   
 [트랜잭션 로그 백업 적용&#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [파일 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [파일 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)  
  
  