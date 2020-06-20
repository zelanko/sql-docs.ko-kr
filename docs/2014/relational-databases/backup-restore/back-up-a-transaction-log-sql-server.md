---
title: 트랜잭션 로그 백업(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- transaction log backups [SQL Server], SQL Server Management Studio
- backups [SQL Server], creating
- backing up transaction logs [SQL Server], SQL Server Management Studio
ms.assetid: 3426b5eb-6327-4c7f-88aa-37030be69fbf
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b57ca40b08718cda5095249991e0d424e6593a24
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84959908"
---
# <a name="back-up-a-transaction-log-sql-server"></a>트랜잭션 로그 백업(SQL Server)
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]또는 PowerShell을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 트랜잭션 로그를 백업하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **트랜잭션 로그를 백업하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
    > [!NOTE]  
    >   또는[유지 관리 계획 마법사](../maintenance-plans/use-the-maintenance-plan-wizard.md)를 사용하여 데이터베이스 백업을 만들 수 있습니다.  
  
-   [관련 작업](#RelatedTasks)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   명시적 또는 암시적 트랜잭션에서는 BACKUP 문을 사용할 수 없습니다.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 권장 사항  
  
-   데이터베이스에서 전체 또는 대량 로그 복구 모델을 사용하는 경우 데이터를 보호하고 트랜잭션 로그가 채워지지 않도록 트랜잭션 로그를 정기적으로 백업해야 합니다. 그러면 로그가 잘리고 특정 시점에 데이터베이스를 복원할 수 있습니다.  
  
-   기본적으로 백업 작업을 성공적으로 수행할 때마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그와 시스템 이벤트 로그에 항목이 추가됩니다. 로그를 자주 백업하는 경우 이러한 성공 메시지는 바로 누적되므로 엄청난 오류 로그가 쌓여 다른 메시지를 찾기 힘들 수 있습니다. 이 경우 스크립트가 이러한 로그 항목에 종속되지 않을 경우 추적 플래그 3226을 사용하여 이러한 항목을 표시하지 않을 수 있습니다. 자세한 내용은 [추적 플래그&#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql)를 참조하세요.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 BACKUP DATABASE 및 BACKUP LOG 권한은 기본적으로 **sysadmin** 고정 서버 역할과 **db_owner** 및 **db_backupoperator** 고정 데이터베이스 역할의 멤버로 설정됩니다.  
  
 백업 디바이스의 물리적 파일에서 발생하는 소유권과 사용 권한 문제는 백업 작업에 영향을 미칠 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 디바이스를 읽고 쓸 수 있어야 하므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스가 실행되는 계정에는 쓰기 권한이 있어야 합니다. 그러나 시스템 테이블의 백업 디바이스에 대한 항목을 추가하는 [sp_addumpdevice](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)는 파일 액세스 권한을 확인하지 않습니다. 백업 디바이스의 물리적 파일에서 발생하는 이러한 문제는 백업 또는 복원을 시도할 때 실제 리소스를 액세스하기 전까지는 발생하지 않습니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-back-up-a-transaction-log"></a>트랜잭션 로그를 백업하려면  
  
1.  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 해당 인스턴스에 연결한 다음 개체 탐색기에서 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 해당 데이터베이스에 따라 사용자 데이터베이스를 선택하거나 **시스템 데이터베이스** 를 확장한 다음 시스템 데이터베이스를 선택합니다.  
  
3.  데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**를 가리킨 다음 **백업**을 클릭합니다. **데이터베이스 백업** 대화 상자가 나타납니다.  
  
4.  **데이터베이스** 목록 상자에서 데이터베이스 이름을 확인합니다. 필요에 따라 목록에서 다른 데이터베이스를 선택할 수 있습니다.  
  
5.  복구 모델이 **FULL** 또는 **BULK_LOGGED**인지 확인합니다.  
  
6.  **백업 유형** 목록 상자에서 **트랜잭션 로그**를 선택합니다.  
  
7.  필요한 경우 **복사 전용 백업**을 선택하여 복사 전용 백업을 만들 수도 있습니다. *복사 전용 백업*은 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 시퀀스와 독립적인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업입니다. 자세한 내용은 [복사 전용 백업&#40;SQL Server&#41;](copy-only-backups-sql-server.md)를 참조하세요.  
  
    > [!NOTE]  
    >  **차등** 옵션을 선택하는 경우 복사 전용 백업을 만들 수 없습니다.  
  
8.  **이름** 입력란에 제시된 기본 백업 세트 이름을 사용하거나 다른 이름을 입력합니다.  
  
9. 필요에 따라 **설명** 입력란에 백업 세트에 대한 설명을 입력합니다.  
  
10. 백업 세트가 만료될 시기를 다음과 같이 지정합니다.  
  
    -   백업 세트가 특정 일수가 지난 후에 만료되도록 하려면 **다음 이후** (기본 옵션)를 클릭한 다음 백업 세트를 만든 후 백업 세트가 만료되기까지 경과해야 하는 일수를 입력합니다. 이 값은 0일에서 99999일 사이일 수 있습니다. 값 0일은 백업 세트 기간 제한이 없음을 의미합니다.  
  
         기본값은 **서버 속성** 대화 상자( **데이터베이스 설정** 페이지)의**백업 미디어 기본 보존 기간(일)** 옵션에 설정되어 있습니다. 이 대화 상자에 액세스하려면 개체 탐색기에서 서버 이름을 마우스 오른쪽 단추로 클릭하고 속성을 선택한 다음 **데이터베이스 설정** 페이지를 선택합니다.  
  
    -   백업 세트가 특정 일자에 만료되게 하려면 **날짜**를 클릭한 다음 백업 세트가 만료될 날짜를 입력합니다.  
  
11. **디스크**, **URL** 또는 **테이프**를 클릭하여 백업 대상 유형을 선택합니다. **추가**를 클릭하면 단일 미디어 세트를 포함하는 디스크나 테이프 드라이브에 대한 경로를 64개까지 선택할 수 있습니다. 선택한 경로는 **백업 대상** 목록 상자에 표시됩니다.  
  
     백업 대상을 제거하려면 해당 대상을 선택한 다음 **제거**를 클릭합니다. 백업 대상의 내용을 보려면 선택한 다음 **내용**을 클릭합니다.  
  
12. 고급 옵션을 보거나 선택하려면 **페이지 선택** 창에서 **옵션** 을 클릭합니다.  
  
13. 다음 중 하나를 클릭하여 **미디어 덮어쓰기** 옵션을 선택합니다.  
  
    -   **기존 미디어 세트에 백업**  
  
         이 옵션에는 **기존 백업 세트에 추가** 또는 **기존 백업 세트 모두 덮어쓰기**를 클릭합니다. 자세한 내용은 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)을 참조하세요.  
  
         필요에 따라 **미디어 세트 이름 및 백업 세트 만료 확인** 을 선택하여 백업 작업에서 미디어 세트와 백업 세트가 만료되는 날짜와 시간을 확인하도록 합니다.  
  
         필요에 따라 **미디어 세트 이름** 입력란에 이름을 입력합니다. 이름을 지정하지 않는 경우 이름이 비어 있는 미디어 세트가 생성됩니다. 미디어 세트 이름을 지정하는 경우 미디어(테이프 또는 디스크)를 선택하여 실제 이름과 여기에서 입력한 이름이 일치하는지 여부를 확인합니다.  
  
         미디어 이름을 비워 두고 검사하도록 확인란을 선택한 경우 미디어에서 미디어 이름을 비워 두는 것과 같은 결과가 나타납니다.  
  
    -   **새 미디어 세트에 백업하고 기존 백업 세트 모두 지우기**  
  
         이 옵션에는 **새 미디어 세트 이름** 입력란에 이름을 입력하고 필요에 따라 **새 미디어 세트 설명** 입력란에 미디어 세트에 대한 설명을 입력합니다. 자세한 내용은 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)을 참조하세요.  
  
14. **안정성** 섹션에서 필요에 따라 다음을 선택합니다.  
  
    -   **완료 시 백업 확인**  
  
    -   **미디어에 쓰기 전에 체크섬 수행**및 필요에 따라 **체크섬 오류 발생 시 계속**. 체크섬에 대한 자세한 내용은 [백업 및 복원 중 발생 가능한 미디어 오류&#40;SQL Server&#41;](possible-media-errors-during-backup-and-restore-sql-server.md)를 참조하세요.  
  
15. **트랜잭션 로그** 섹션에서 다음을 수행합니다.  
  
    -   일상적인 로그 백업의 경우 기본 선택인 **비활성 항목을 제거하여 트랜잭션 로그 잘라내기**를 유지합니다.  
  
    -   비상 로그, 즉 활성 로그를 백업하려면 **비상 로그 백업을 수행하고 복원 중인 상태로 데이터베이스 유지**를 선택합니다.  
  
         비상 로그 백업은 작업 손실을 방지하기 위해 비상 로그 백업에 실패한 후에 적용됩니다. 실패 후, 데이터베이스 복원 시작 전 또는 보조 데이터베이스로 장애 조치(Failover)할 때 활성 로그를 백업합니다(비상 로그 백업). 이 옵션을 선택하는 것은 Transact-SQL의 BACKUP LOG 문에서 NORECOVERY 옵션을 지정하는 것과 동일합니다. 비상 로그 백업에 대한 자세한 내용은 [비상 로그 백업&#40;SQL Server&#41;](tail-log-backups-sql-server.md)을 참조하세요.  
  
16. **일반** 페이지의 **대상** 섹션에서 지정한 대로 테이프 드라이브에 백업하는 경우 **백업 후 테이프 언로드** 옵션이 활성화됩니다. 이 옵션을 클릭하면 **언로드 전에 테이프 되감기** 옵션이 활성화됩니다.  
  
17. [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 이상에서는 [백업 압축](backup-compression-sql-server.md)을 지원합니다. 기본적으로 백업은 **백업-압축 기본값** 서버 구성 옵션의 값에 따라 압축됩니다. 그러나 현재 서버 수준 기본값에 관계없이 **백업 압축**을 선택하여 백업을 압축하고, **백업 압축 안 함**을 선택하여 압축을 방지할 수 있습니다.  
  
     **현재 백업 압축 기본값을 보려면**  
  
    -   [backup compression default 서버 구성 옵션 보기 또는 구성](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
 **암호화**  
  
 백업 파일을 암호화하려면 **백업 암호화** 확인란을 선택합니다. 백업 파일을 암호화하는 데 사용할 암호화 알고리즘을 선택하고 인증서 또는 비대칭 키를 제공합니다. 사용 가능한 암호화 알고리즘은 다음과 같습니다.  
  
-   AES 128  
  
-   AES 192  
  
-   AES 256  
  
-   Triple DES  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-back-up-a-transaction-log"></a>트랜잭션 로그를 백업하려면  
  
1.  BACKUP LOG 문을 실행하여 트랜잭션 로그를 백업하며 다음을 지정합니다.  
  
    -   백업할 트랜잭션 로그가 속한 데이터베이스의 이름  
  
    -   트랜잭션 로그 백업이 기록될 백업 디바이스  
  
###  <a name="example-transact-sql"></a><a name="TsqlExample"></a> 예(Transact-SQL)  
  
> [!IMPORTANT]  
>  이 예에서는 단순 복구 모델을 사용하는 [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] 데이터베이스를 사용합니다. 로그 백업을 허용하기 위해 전체 데이터베이스를 백업하기 전에 전체 복구 모델을 사용하도록 데이터베이스를 설정했습니다. 자세한 내용은 [데이터베이스 복구 모델 보기 또는 변경&#40;SQL Server&#41;](view-or-change-the-recovery-model-of-a-database-sql-server.md)을 참조하세요.  
  
 이 예에서는 이전에 만든 명명된 백업 디바이스 [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] 에 `MyAdvWorks_FullRM_log1`데이터베이스의 트랜잭션 로그 백업을 만듭니다.  
  
```sql  
BACKUP LOG AdventureWorks2012  
   TO MyAdvWorks_FullRM_log1;  
GO  
```  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> PowerShell 사용  
  
`Backup-SqlDatabase` 매개 변수의 값으로 `Log`를 지정하여 `-BackupAction` cmdlet을 실행합니다.  
  
다음 예에서는 서버 인스턴스 `MyDB` 의 기본 백업 위치에 `Computer\Instance`데이터베이스의 로그 백업을 만듭니다.  
  
    ```powershell
    Backup-SqlDatabase -ServerInstance Computer\Instance -Database MyDB -BackupAction Log  
    ```  
  
SQL Server PowerShell 공급자를 설정 하 고 사용 하려면 [SQL Server PowerShell 공급자](../../powershell/sql-server-powershell-provider.md)를 참조 하세요.
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 관련 작업  
  
-   [트랜잭션 로그 백업 복원&#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)  
  
-   [SQL Server 데이터베이스를 지정 시간으로 복원&#40;전체 복구 모델&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
-   [꽉 찬 트랜잭션 로그 문제 해결&#40;SQL Server 오류 9002&#41;](../logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
## <a name="see-also"></a>참고 항목  
 [BACKUP&#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [트랜잭션 로그 백업 적용&#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [유지 관리 계획](../maintenance-plans/maintenance-plans.md)   
 [전체 파일 백업&#40;SQL Server&#41;](full-file-backups-sql-server.md)  
