---
title: 파일 및 파일 그룹 백업(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 08/03/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backing up filegroups [SQL Server]
- file backups [SQL Server], how-to topics
- backing up files [SQL Server]
- backups [SQL Server], creating
- filegroups [SQL Server], backing up
ms.assetid: a0d3a567-7d8b-4cfe-a505-d197b9a51f70
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1b6127bbc02c85276292da1ada5748fbb2d7923f
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59241931"
---
# <a name="back-up-files-and-filegroups-sql-server"></a>파일 및 파일 그룹 백업(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]또는 PowerShell을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 파일 및 파일 그룹을 백업하는 방법에 대해 설명합니다. 데이터베이스 크기와 성능 요구 사항으로 인해 전체 데이터베이스 백업이 불가능할 경우 이를 대신하여 파일 백업을 만들 수 있습니다. *파일 백업* 에는 하나 이상의 파일(또는 파일 그룹)에 있는 모든 데이터가 포함됩니다. 파일 백업에 대한 자세한 내용은 [전체 파일 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md) 및 [차등 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)을 참조하세요.  

  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   명시적 또는 암시적 트랜잭션에서는 BACKUP 문을 사용할 수 없습니다.  
  
-   단순 복구 모델에서 읽기/쓰기 파일은 모두 함께 백업해야 합니다. 이렇게 하면 데이터베이스를 일정한 지정 시간으로 복원할 수 있습니다. 각 읽기/쓰기 파일 또는 파일 그룹을 개별적으로 지정하는 대신 READ_WRITE_FILEGROUPS 옵션을 사용하세요. 이 옵션은 데이터베이스의 모든 읽기/쓰기 파일 그룹을 백업합니다. READ_WRITE_FILEGROUPS를 지정하여 만드는 백업을 *부분 백업*이라고 합니다. 자세한 내용은 [부분 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/partial-backups-sql-server.md)을 참조하세요.  
  
-   제한 사항에 대한 자세한 내용은 [백업 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)을 참조하세요.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   기본적으로 백업 작업을 성공적으로 수행할 때마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그와 시스템 이벤트 로그에 항목이 추가됩니다. 로그를 자주 백업하는 경우 이러한 성공 메시지는 바로 누적되므로 엄청난 오류 로그가 쌓여 다른 메시지를 찾기 힘들 수 있습니다. 이 경우 스크립트가 이러한 로그 항목에 종속되지 않을 경우 추적 플래그 3226을 사용하여 이러한 항목을 표시하지 않을 수 있습니다. 자세한 내용은 [추적 플래그&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)를 참조하세요.  
  
 
##  <a name="Permissions"></a> 사용 권한  
 BACKUP DATABASE 및 BACKUP LOG 권한은 기본적으로 **sysadmin** 고정 서버 역할과 **db_owner** 및 **db_backupoperator** 고정 데이터베이스 역할의 멤버로 설정됩니다.  
  
 백업 디바이스의 물리적 파일에서 발생하는 소유권과 사용 권한 문제는 백업 작업에 영향을 미칠 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 디바이스를 읽고 쓸 수 있어야 하므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스가 실행되는 계정에는 쓰기 권한이 있어야 합니다. 그러나 시스템 테이블의 백업 디바이스에 대한 항목을 추가하는 [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)는 파일 액세스 권한을 확인하지 않습니다. 백업 디바이스의 물리적 파일에서 발생하는 이러한 문제는 백업 또는 복원을 시도할 때 실제 리소스를 액세스하기 전까지는 발생하지 않습니다.  

[!INCLUDE[Freshness](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="back-up-files-and-filegroups-using-ssms"></a>SSMS를 사용하여 파일 및 파일 그룹 백업   
  
1.  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 해당 인스턴스에 연결한 다음 개체 탐색기에서 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 해당 데이터베이스에 따라 사용자 데이터베이스를 선택하거나 **시스템 데이터베이스** 를 확장한 다음 시스템 데이터베이스를 선택합니다.  
  
3.  데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**를 가리킨 다음 **백업**을 클릭합니다. **데이터베이스 백업** 대화 상자가 나타납니다.  
  
4.  **데이터베이스** 목록에서 데이터베이스 이름을 확인합니다. 필요에 따라 목록에서 다른 데이터베이스를 선택할 수 있습니다.  
  
5.  **백업 유형** 목록에서 **전체** 또는 **차등**을 선택합니다.  
  
6.  **백업 구성 요소** 옵션에서 **파일 및 파일 그룹**을 클릭합니다.  
  
7.  **파일 및 파일 그룹 선택** 대화 상자에서 백업할 파일 및 파일 그룹을 선택합니다. 개별 파일을 하나 이상 선택하거나 파일 그룹의 확인란을 선택하여 해당 파일 그룹의 모든 파일을 자동으로 선택할 수 있습니다.  
  
8.  **이름** 입력란에 제시된 기본 백업 세트 이름을 사용하거나 다른 이름을 입력합니다.  
  
9. 필요에 따라 **설명** 입력란에 백업 세트에 대한 설명을 입력합니다.  
  
10. 백업 세트가 만료될 시기를 다음과 같이 지정합니다.  
  
    -   백업 세트가 특정 일 수 후에 만료되게 하려면 **다음 이후** (기본 옵션)를 클릭합니다. 그런 다음 세트를 만든 후 세트가 만료되는 일 수를 입력합니다. 이 값은 0일에서 99999일 사이일 수 있습니다. 값 0일은 백업 세트 기간 제한이 없음을 의미합니다.  
  
         기본값은 **서버 속성** 대화 상자( **데이터베이스 설정** 페이지)의**백업 미디어 기본 보존 기간(일)** 옵션에 설정되어 있습니다. 이 옵션에 액세스하려면 개체 탐색기에서 서버 이름을 마우스 오른쪽 단추로 클릭하고 속성을 선택한 다음 **데이터베이스 설정** 페이지를 선택합니다.  
  
    -   백업 세트가 특정 일자에 만료되게 하려면 **날짜**를 클릭한 다음 백업 세트가 만료될 날짜를 입력합니다.  
  
11. **디스크** 나 **테이프**를 클릭하여 백업 대상 유형을 선택합니다. **추가**를 클릭하면 단일 미디어 세트가 들어 있는 디스크나 테이프 드라이브에 대한 경로를 64개까지 선택할 수 있습니다. 선택한 경로는 **백업할 위치** 목록에 표시됩니다.  
  
    >**참고:** 백업 대상을 제거하려면 해당 대상을 선택한 다음 **제거**를 클릭합니다. 백업 대상의 내용을 보려면 선택한 다음 **내용**을 클릭합니다.  
  
12. 고급 옵션을 보거나 선택하려면 **페이지 선택** 창에서 **옵션** 을 클릭합니다.  
  
13. 다음 중 하나를 클릭하여 **미디어 덮어쓰기** 옵션을 선택합니다.  
  
    -   **기존 미디어 세트에 백업**  
  
         이 옵션에는 **기존 백업 세트에 추가** 또는 **기존 백업 세트 모두 덮어쓰기**를 클릭합니다. 기존 미디어 세트에 백업에 대한 자세한 내용은 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)를 참조하세요.  
  
         필요에 따라 **미디어 세트 이름 및 백업 세트 만료 확인** 을 선택하여 백업 작업에서 미디어 세트와 백업 세트가 만료되는 날짜와 시간을 확인하도록 합니다.  
  
         필요에 따라 **미디어 세트 이름** 입력란에 이름을 입력합니다. 이름을 지정하지 않는 경우 이름이 비어 있는 미디어 세트가 생성됩니다. 미디어 세트 이름을 지정하는 경우 실제 이름과 입력한 이름이 일치하는지 확인하기 위해 미디어(테이프 또는 디스크)를 확인합니다.  
  
         미디어 이름을 비워 두고 검사하도록 확인란을 선택한 경우 미디어에서 미디어 이름을 비워 두는 것과 같은 결과가 나타납니다.  
  
    -   **새 미디어 세트에 백업하고 기존 백업 세트 모두 지우기**  
  
         이 옵션에는 **새 미디어 세트 이름** 입력란에 이름을 입력하고 필요에 따라 **새 미디어 세트 설명** 입력란에 미디어 세트에 대한 설명을 입력합니다. 새 미디어 세트 만들기에 대한 자세한 내용은 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)를 참조하세요.  
  
14. **안정성** 섹션에서 필요에 따라 다음을 선택합니다.  
  
    -   **완료 시 백업 확인**  
  
    -   **미디어에 쓰기 전에 체크섬 수행**및 필요에 따라 **체크섬 오류 발생 시 계속**. 체크섬에 대한 자세한 내용은 [백업 및 복원 중 발생 가능한 미디어 오류&#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)를 참조하세요.  
  
15. **일반** 페이지의 **대상** 섹션에서 지정한 대로 테이프 드라이브에 백업하는 경우 **백업 후 테이프 언로드** 옵션이 활성화됩니다. 이 옵션을 클릭하면 **언로드 전에 테이프 되감기** 옵션이 활성화됩니다.  
  
    > **참고:** **일반** 페이지의 **백업 유형** 섹션에서 지정한 대로 트랜잭션 로그를 백업하지 않으면 **트랜잭션 로그** 섹션의 옵션이 비활성화됩니다.  
  
16. [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 이상 버전에서는 [백업 압축](../../relational-databases/backup-restore/backup-compression-sql-server.md)을 지원합니다. 기본적으로 백업은 **백업-압축 기본값** 서버 구성 옵션의 값에 따라 압축됩니다. 그러나 현재 서버 수준 기본값에 관계없이 **백업 압축**을 선택하여 백업을 압축하고, **백업 압축 안 함**을 선택하여 압축을 방지할 수 있습니다.  
  
     **현재 백업 압축 기본값을 보려면**  
  
    -   [backup compression default 서버 구성 옵션 보기 또는 구성](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
  
## <a name="back-up-files-and-filegroups-using-t-sql"></a>T-SQL을 사용하여 파일 및 파일 그룹 백업
  
1.  파일 또는 파일 그룹 백업을 만들려면 [BACKUP DATABASE <file_or_filegroup>](../../t-sql/statements/backup-transact-sql.md) 문을 사용합니다. 최소한 이 문은 다음 항목을 지정해야 합니다.  
  
    -   데이터베이스 이름입니다.  
  
    -   각 파일 또는 파일 그룹에 대한 각각의 FILE 또는 FILEGROUP 절  
  
    -   전체 백업이 기록될 백업 디바이스  
  
     파일 백업의 기본 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문은 다음과 같습니다.  
  
     BACKUP DATABASE *database*  
  
     { FILE _=_*logical_file_name* | FILEGROUP _=_*logical_filegroup_name* } [ **,**...*f* ]  
  
     TO *backup_device* [ **,**...*n* ]  
  
     [ WITH *with_options* [ **,**...*o* ] ] ;  
  
    |옵션|설명|  
    |------------|-----------------|  
    |*database*|트랜잭션 로그, 일부 데이터베이스, 전체 데이터베이스가 백업되는 데이터베이스입니다.|  
    |FILE _=_*logical_file_name*|파일 백업에 포함할 파일의 논리적 이름을 지정합니다.|  
    |FILEGROUP _=_*logical_filegroup_name*|파일 백업에 포함할 파일 그룹의 논리적 이름을 지정합니다. 단순 복구 모델에서 파일 그룹 백업은 읽기 전용 파일 그룹에만 사용할 수 있습니다.|  
    |[ **,**...*f* ]|여러 개의 파일 및 파일 그룹을 지정할 수 있음을 나타내는 자리 표시자입니다. 이때 파일 또는 파일 그룹의 수는 제한이 없습니다.|  
    |*backup_device* [ **,**...*n* ]|백업 작업에 사용할 1-64개의 백업 디바이스 목록을 지정합니다. 물리적 백업 디바이스를 지정하거나, 이미 정의된 경우 해당 논리적 백업 디바이스를 지정할 수 있습니다. 물리적 백업 디바이스를 지정하려면 다음 DISK 또는 TAPE 옵션을 사용합니다.<br /><br /> { DISK &#124; TAPE } _=_*physical_backup_device_name*<br /><br /> 자세한 내용은 [백업 디바이스&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)를 참조하세요.|  
    |WITH *with_options* [ **,**...*o* ]|필요에 따라 DIFFERENTIAL과 같은 하나 이상의 추가 옵션을 지정합니다.<br /><br /> 참고: 차등 파일 백업에는 기반으로 전체 파일 백업이 필요합니다. 자세한 내용은 [차등 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)를 참조하세요.|  
  
2.  전체 복구 모델에서는 트랜잭션 로그도 백업해야 합니다. 전체 파일 백업의 전체 세트를 사용하여 데이터베이스를 복원하려면 첫 번째 파일 백업을 시작할 때부터 모든 파일 백업을 포함할 정도의 충분한 로그 백업이 있어야 합니다. 자세한 내용은 [트랜잭션 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)에 미러 데이터베이스를 준비하는 방법에 대해 설명합니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 예에서는 `Sales` 데이터베이스의 보조 파일 그룹에 있는 하나 이상의 파일을 백업합니다. 이 데이터베이스는 전체 복구 모델을 사용하고 다음과 같은 보조 파일 그룹을 포함합니다.  
  
-   `SalesGroup1` 및 `SGrp1Fi1` 파일을 포함하는 `SGrp1Fi2`파일 그룹  
  
-   `SalesGroup2` 및 `SGrp2Fi1` 파일을 포함하는 `SGrp2Fi2`파일 그룹  
  
#### <a name="a-create-a-file-backup-of-two-files"></a>1. 두 파일의 파일 백업 만들기  
 다음 예에서는 `SGrp1Fi2` 의 `SalesGroup1` 파일과 `SGrp2Fi2` 파일 그룹의 `SalesGroup2` 파일에 대해서만 차등 파일 백업을 만듭니다.  
  
```sql  
--Backup the files in the SalesGroup1 secondary filegroup.  
BACKUP DATABASE Sales  
   FILE = 'SGrp1Fi2',   
   FILE = 'SGrp2Fi2'   
   TO DISK = 'G:\SQL Server Backups\Sales\SalesGroup1.bck';  
GO  
```  
  
#### <a name="b-create-a-full-file-backup-of-the-secondary-filegroups"></a>2. 보조 파일 그룹의 전체 파일 백업 만들기  
 다음 예에서는 두 보조 파일 그룹에 있는 모든 파일의 전체 파일 백업을 만듭니다.  
  
```sql  
--Back up the files in SalesGroup1.  
BACKUP DATABASE Sales  
   FILEGROUP = 'SalesGroup1',  
   FILEGROUP = 'SalesGroup2'  
   TO DISK = 'C:\MySQLServer\Backups\Sales\SalesFiles.bck';  
GO  
```  
  
#### <a name="c-create-a-differential-file-backup-of-the-secondary-filegroups"></a>C. 보조 파일 그룹의 차등 파일 백업 만들기  
 다음 예에서는 두 보조 파일 그룹에 있는 모든 파일의 차등 파일 백업을 만듭니다.  
  
```sql  
--Back up the files in SalesGroup1.  
BACKUP DATABASE Sales  
   FILEGROUP = 'SalesGroup1',  
   FILEGROUP = 'SalesGroup2'  
   TO DISK = 'C:\MySQLServer\Backups\Sales\SalesFiles.bck'  
   WITH   
      DIFFERENTIAL;  
GO  
```  
  
##  <a name="PowerShellProcedure"></a> PowerShell 사용  
  
1.  **Backup-SqlDatabase** cmdlet을 사용하고 **-BackupAction** 매개 변수의 값으로 **Files** 를 지정합니다. 또한 다음 매개 변수 중 하나를 지정합니다.  
  
    -   특정 파일을 백업하려면 _-DatabaseFile_*String* 매개 변수를 지정합니다. 여기서 *String* 은 백업할 하나 이상의 데이터베이스 파일입니다.  
  
    -   지정된 파일 그룹의 모든 파일을 백업하려면 _-DatabaseFileGroup_*String* 매개 변수를 지정합니다. 여기서 *String* 은 백업할 하나 이상의 데이터베이스 파일 그룹입니다.  
  
     다음 예에서는 `MyDB` 데이터베이스의 보조 파일 그룹 'FileGroup1' 및 'FileGroup2'에 있는 모든 파일의 전체 파일 백업을 만듭니다. 백업은 서버 인스턴스 `Computer\Instance`의 기본 백업 위치에 만들어집니다.  
  
    ```sql  
    --Enter this command at the PowerShell command prompt, C:\PS>  
    Backup-SqlDatabase -ServerInstance Computer\Instance -Database MyDB -BackupAction Files -DatabaseFileGroup "FileGroup1","FileGroup2"  
    ```  
  
 **SQL Server PowerShell 공급자 설정 및 사용**  
  
-   [SQL Server PowerShell Provider](../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
## <a name="see-also"></a>관련 항목:  
 [백업 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [백업 기록 및 헤더 정보&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)   
 [데이터베이스 백업&#40;일반 페이지&#41;](../../relational-databases/backup-restore/back-up-database-general-page.md)   
 [데이터베이스 백업&#40;백업 옵션 페이지&#41;](../../relational-databases/backup-restore/back-up-database-backup-options-page.md)   
 [전체 파일 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md)   
 [차등 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)   
 [파일 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [파일 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)  
  
  
