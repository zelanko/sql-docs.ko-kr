---
title: 전체 데이터베이스 백업 만들기(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backing up databases [SQL Server], full backups
- backing up databases [SQL Server], SQL Server Management Studio
- backups [SQL Server], creating
- database backups [SQL Server], SQL Server Management Studio
ms.assetid: 586561fc-dfbb-4842-84f8-204a9100a534
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c43fbe12b8449fb231ee9a2f479ff17ac0281493
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62922277"
---
# <a name="create-a-full-database-backup-sql-server"></a>전체 데이터베이스 백업 만들기(SQL Server)
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]또는 PowerShell을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 전체 데이터베이스 백업을 만드는 방법에 대해 설명합니다.  
  
> [!NOTE]  
>  Windows Azure Blob 저장소 서비스로 SQL Server 백업하는 방법에 대한 자세한 내용은 [Windows Azure Blob 저장소 서비스로 SQL Server 백업 및 복원](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)을 참조하십시오.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **전체 데이터베이스를 만들려면 사용 하 여 백업:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   [관련 태스크](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   명시적 또는 암시적 트랜잭션에서는 BACKUP 문을 사용할 수 없습니다.  
  
-   최신 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 만든 백업은 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 복원할 수 없습니다.  
  
-   자세한 내용은 [백업 개요&#40;SQL Server&#41;](backup-overview-sql-server.md)을 참조하세요.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   데이터베이스가 커짐에 따라 전체 데이터베이스 백업은 완료하는 데 시간이 오래 걸리고 스토리지 공간도 더 많이 필요하게 됩니다. 따라서 큰 데이터베이스의 경우 *차등 데이터베이스 백업*으로 전체 데이터베이스 백업을 보완할 수 있습니다. 자세한 내용은 [차등 백업&#40;SQL Server&#41;](differential-backups-sql-server.md)을 참조하세요.  
  
-   [sp_spaceused](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql) 시스템 저장 프로시저를 사용하여 전체 데이터베이스 백업의 크기를 예측할 수 있습니다.  
  
-   기본적으로 백업 작업을 성공적으로 수행할 때마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그와 시스템 이벤트 로그에 항목이 추가됩니다. 로그를 자주 백업하는 경우 이러한 성공 메시지는 바로 누적되므로 엄청난 오류 로그가 쌓여 다른 메시지를 찾기 힘들 수 있습니다. 이 경우 스크립트가 이러한 로그 항목에 종속되지 않을 경우 추적 플래그 3226을 사용하여 이러한 항목을 표시하지 않을 수 있습니다. 자세한 내용은 [추적 플래그&#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql)를 참조하세요.  
  
###  <a name="Security"></a> 보안  
 데이터베이스 백업에서 TRUSTWORTHY는 OFF로 설정되어 있습니다. TRUSTWORTHY를 ON으로 설정하는 방법은 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)을 참조하세요.  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 `PASSWORD` 및 `MEDIAPASSWORD` 옵션은 백업을 만드는 데 지원되지 않습니다. 암호를 사용하여 만든 백업은 계속 복원할 수 있습니다.  
  
####  <a name="Permissions"></a> Permissions  
 BACKUP DATABASE 및 BACKUP LOG 권한은 기본적으로 **sysadmin** 고정 서버 역할과 **db_owner** 및 **db_backupoperator** 고정 데이터베이스 역할의 멤버로 설정됩니다.  
  
 백업 디바이스의 물리적 파일에서 발생하는 소유권과 사용 권한 문제는 백업 작업에 영향을 미칠 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 장치를 읽고 쓸 수 있어야 하므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스가 실행되는 계정에는 쓰기 권한이 있어야 합니다. 그러나 시스템 테이블의 백업 디바이스에 대한 항목을 추가하는 [sp_addumpdevice](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)는 파일 액세스 권한을 확인하지 않습니다. 백업 디바이스의 물리적 파일에서 발생하는 이러한 문제는 백업 또는 복원을 시도할 때 실제 리소스를 액세스하기 전까지는 발생하지 않습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 백업 태스크를 지정할 때 **스크립트** 단추를 클릭하고 스크립트 대상을 선택하여 해당되는 [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](/sql/t-sql/statements/backup-transact-sql) 스크립트를 생성할 수 있습니다.  
  
#### <a name="to-back-up-a-database"></a>데이터베이스를 백업하려면  
  
1.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 해당 인스턴스에 연결한 다음 개체 탐색기에서 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 해당 데이터베이스에 따라 사용자 데이터베이스를 선택하거나 **시스템 데이터베이스** 를 확장한 다음 시스템 데이터베이스를 선택합니다.  
  
3.  데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**를 가리킨 다음 **백업**을 클릭합니다. **데이터베이스 백업** 대화 상자가 나타납니다.  
  
4.  에 `Database` 목록 상자에서 데이터베이스 이름을 확인 합니다. 필요에 따라 목록에서 다른 데이터베이스를 선택할 수 있습니다.  
  
5.  모든 복구 모델(**전체**, **대량 로그** 또는 **단순**)에서 데이터베이스 백업을 수행할 수 있습니다.  
  
6.  **백업 유형** 목록 상자에서 **전체**를 선택합니다.  
  
     전체 데이터베이스 백업을 만든 후 차등 데이터베이스 백업을 만들 수 있습니다. 자세한 내용은 [차등 데이터베이스 백업 만들기&#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)를 참조하세요.  
  
7.  필요한 경우 **복사 전용 백업**을 선택하여 복사 전용 백업을 만들 수도 있습니다. *복사 전용 백업*은 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 시퀀스와 독립적인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업입니다. 자세한 내용은 [복사 전용 백업&#40;SQL Server&#41;](copy-only-backups-sql-server.md)를 참조하세요.  
  
    > [!NOTE]  
    >  **차등** 옵션을 선택하는 경우 복사 전용 백업을 만들 수 없습니다.  
  
8.  에 대 한 **Backup 구성 요소**, 클릭 `Database`합니다.  
  
9. **이름** 입력란에 제시된 기본 백업 세트 이름을 사용하거나 다른 이름을 입력합니다.  
  
10. 필요에 따라 **설명** 입력란에 백업 세트에 대한 설명을 입력합니다.  
  
11. **디스크**, **테이프** 또는 **URL**을 클릭하여 백업 대상의 유형을 선택합니다. **추가**를 클릭하면 단일 미디어 세트를 포함하는 디스크나 테이프 드라이브에 대한 경로를 64개까지 선택할 수 있습니다. 선택한 경로는 **백업 대상** 목록 상자에 표시됩니다.  
  
     백업 대상을 제거하려면 해당 대상을 선택한 다음 **제거**를 클릭합니다. 백업 대상의 내용을 보려면 선택한 다음 **내용**을 클릭합니다.  
  
12. 미디어 옵션을 보거나 선택하려면 **페이지 선택** 창에서 **미디어 옵션** 을 클릭합니다.  
  
13. 다음 중 하나를 클릭하여 **미디어 덮어쓰기** 옵션을 선택합니다.  
  
    -   **기존 미디어 세트에 백업**  
  
         이 옵션에는 **기존 백업 세트에 추가** 또는 **기존 백업 세트 모두 덮어쓰기**를 클릭합니다. 자세한 내용은 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)을 참조하세요.  
  
         필요에 따라 **미디어 세트 이름 및 백업 세트 만료 확인** 을 선택하여 백업 작업에서 미디어 세트와 백업 세트가 만료되는 날짜와 시간을 확인하도록 합니다.  
  
         필요에 따라 **미디어 세트 이름** 입력란에 이름을 입력합니다. 이름을 지정하지 않는 경우 이름이 비어 있는 미디어 세트가 생성됩니다. 미디어 세트 이름을 지정하는 경우 미디어(테이프 또는 디스크)를 선택하여 실제 이름과 여기에서 입력한 이름이 일치하는지 여부를 확인합니다.  
  
        > [!IMPORTANT]  
        >  **일반** 페이지에서 **URL** 을 백업 대상으로 선택한 경우 이 옵션을 사용할 수 없습니다. 자세한 내용은 [데이터베이스 백업&#40;미디어 옵션 페이지&#41;](back-up-database-media-options-page.md)을 참조하세요.  
        >   
        >  암호화를 사용할 계획인 경우 이 옵션을 선택하지 마세요. 이 옵션을 선택하면 **백업 옵션** 페이지의 암호화 옵션을 사용할 수 없게 됩니다. 기존 백업 세트에 추가할 때는 암호화가 지원되지 않습니다.  
  
    -   **새 미디어 세트에 백업하고 기존 백업 세트 모두 지우기**  
  
         이 옵션에는 **새 미디어 세트 이름** 입력란에 이름을 입력하고 필요에 따라 **새 미디어 세트 설명** 입력란에 미디어 세트에 대한 설명을 입력합니다.  
  
        > [!IMPORTANT]  
        >  **일반** 페이지에서 **URL** 을 선택한 경우 이 옵션을 사용할 수 없습니다. 이러한 작업은 Windows Azure 스토리지에 백업하는 경우 지원되지 않습니다.  
  
14. **안정성** 섹션에서 필요에 따라 다음을 선택합니다.  
  
    -   **완료 시 백업 확인**  
  
    -   **미디어에 쓰기 전에 체크섬 수행**및 필요에 따라 **체크섬 오류 발생 시 계속**. 체크섬에 대한 자세한 내용은 [백업 및 복원 중 발생 가능한 미디어 오류&#40;SQL Server&#41;](possible-media-errors-during-backup-and-restore-sql-server.md)를 참조하세요.  
  
15. **일반** 페이지의 **대상** 섹션에서 지정한 대로 테이프 드라이브에 백업하는 경우 **백업 후 테이프 언로드** 옵션이 활성화됩니다. 이 옵션을 클릭하면 **언로드 전에 테이프 되감기** 옵션이 활성화됩니다.  
  
    > [!NOTE]  
    >  **일반** 페이지의 **백업 유형** 섹션에서 지정한 대로 트랜잭션 로그를 백업하지 않으면 **트랜잭션 로그** 섹션의 옵션이 비활성화됩니다.  
  
16. 백업 옵션을 보거나 선택하려면 **페이지 선택** 창에서 **백업 옵션** 을 클릭합니다.  
  
17. 백업 세트가 만료되고 명시적으로 만료 날짜 확인을 생략할 필요 없이 덮어쓸 수 있는 시기를 지정합니다.  
  
    -   백업 세트가 특정 일수가 지난 후에 만료되도록 하려면 **다음 이후** (기본 옵션)를 클릭한 다음 백업 세트를 만든 후 백업 세트가 만료되기까지 경과해야 하는 일수를 입력합니다. 이 값은 0일에서 99999일 사이일 수 있습니다. 값 0일은 백업 세트 기간 제한이 없음을 의미합니다.  
  
         기본값은 데이터베이스 설정 페이지에 있는 **서버 속성** 대화 상자의 **백업 미디어 기본 보존 기간(일)** 옵션에 설정되어 있습니다. 이 페이지에 액세스하려면 개체 탐색기에서 서버 이름을 마우스 오른쪽 단추로 클릭하고 속성을 선택한 다음 **데이터베이스 설정** 페이지를 선택합니다.  
  
    -   백업 세트가 특정 일자에 만료되게 하려면 **날짜**를 클릭한 다음 백업 세트가 만료될 날짜를 입력합니다.  
  
         백업 만료 날짜에 대한 자세한 내용은 [BACKUP&#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)을 참조하세요.  
  
18. [!INCLUDE[ssEnterpriseEd10](../../../includes/ssenterpriseed10-md.md)] 이상에서는 [백업 압축](backup-compression-sql-server.md)을 지원합니다. 기본적으로 백업은 **백업-압축 기본값** 서버 구성 옵션의 값에 따라 압축됩니다. 그러나 현재 서버 수준 기본값에 관계없이 **백업 압축**을 선택하여 백업을 압축하고, **백업 압축 안 함**을 선택하여 압축을 방지할 수 있습니다.  
  
     **확인 하거나 현재 백업 압축 기본값을 변경 하려면**  
  
    -   [backup compression default 서버 구성 옵션 보기 또는 구성](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
19. 백업에 암호화를 사용할지 여부를 지정합니다. 암호화 단계에 사용할 암호화 알고리즘을 선택하고 기존 인증서 또는 비대칭 키 목록의 인증서 또는 비대칭 키를 제공합니다. 암호화는 SQL Server 2014 이상에서 지원됩니다. 암호화 옵션에 대한 자세한 내용은 [데이터베이스 백업&#40;백업 옵션 페이지&#41;](back-up-database-backup-options-page.md)을 참조하세요.  
  
> [!NOTE]  
>  또는 유지 관리 계획 마법사를 사용하여 데이터베이스 백업을 만들 수 있습니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-create-a-full-database-backup"></a>전체 데이터베이스 백업을 만들려면  
  
1.  BACKUP DATABASE 문을 실행하여 전체 데이터베이스 백업을 만듭니다. 이때 다음을 지정합니다.  
  
    -   백업할 데이터베이스의 이름  
  
    -   전체 데이터베이스 백업이 기록되는 백업 디바이스  
  
     전체 데이터베이스 백업의 기본 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문은 다음과 같습니다.  
  
     BACKUP DATABASE *database*  
  
     TO *backup_device* [ **,** ...*n* ]  
  
     [ WITH *with_options* [ **,** ...*o* ] ] ;  
  
    |옵션|Description|  
    |------------|-----------------|  
    |*database*|백업할 데이터베이스입니다.|  
    |*backup_device* [ **,** ...*n* ]|백업 작업에 사용할 1-64개의 백업 디바이스 목록을 지정합니다. 물리적 백업 디바이스를 지정하거나, 이미 정의된 경우 해당 논리적 백업 디바이스를 지정할 수 있습니다. 물리적 백업 디바이스를 지정하려면 다음 DISK 또는 TAPE 옵션을 사용합니다.<br /><br /> { DISK &#124; TAPE } **=** _physical_backup_device_name_<br /><br /> 자세한 내용은 [백업 장치&#40;SQL Server&#41;](backup-devices-sql-server.md)인스턴스에서 가져온 경우에 필요합니다.|  
    |WITH *with_options* [ **,** ...*o* ]|필요에 따라 *o*등과 같은 하나 이상의 추가 옵션을 지정합니다. 몇 가지 WITH의 기본 옵션에 대한 자세한 내용은 2단계를 참조하세요.|  
  
2.  필요에 따라 한 개 이상의 WITH 옵션을 지정합니다. 몇 가지 WITH의 기본 옵션은 이 페이지에 설명되어 있습니다. 모든 WITH 옵션에 대한 자세한 내용은 [BACKUP&#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)을 참조하세요.  
  
    -   기본 백업 세트 WITH 옵션  
  
         { COMPRESSION | NO_COMPRESSION }  
         [!INCLUDE[ssEnterpriseEd10](../../../includes/ssenterpriseed10-md.md)] 이상에서만 사용 가능. 이 백업에서 [백업 압축](backup-compression-sql-server.md) 을 수행하고 서버 수준 기본값을 재정의할지 여부를 지정합니다.  
  
         ENCRYPTION (ALGORITHM, SERVER CERTIFICATE |ASYMMETRIC KEY)  
         SQL Server 2014 이상에서만 사용할 암호화 알고리즘과 암호화 보안에 사용할 인증서 또는 비대칭 키를 지정합니다.  
  
         설명을 **=** {0} **' *`text`* '**  |  **@** _text_ 변수_ }  
         백업 세트를 설명하는 자유 형식의 텍스트를 지정합니다. 문자열을 최대 255자까지 지정할 수 있습니다.  
  
         NAME **=** { *backup_set_name* |  **@** _backup_set_name_var_ }  
         백업 세트의 이름을 지정합니다. 이름은 최대 128자까지 지정할 수 있습니다. NAME을 지정하지 않으면 공백이 됩니다.  
  
    -   기본 백업 세트 WITH 옵션  
  
         기본적으로 BACKUP은 기존 백업 세트를 유지하면서 기존 미디어 세트에 백업을 추가합니다. 이것을 명시적으로 지정하려면 NOINIT 옵션을 사용합니다. 기존 백업 세트에 추가하는 방법은 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)을 참조하세요.  
  
         또는 백업 미디어의 형식을 지정하기 위해 FORMAT 옵션을 사용합니다.  
  
         FORMAT [ **,** MEDIANAME **=** { *media_name* |  **@** _media_name_variable_ } ] [ **,** MEDIADESCRIPTION **=** { *text* |  **@** _text_variable_ } ]  
         미디어를 처음 사용하거나 기존의 모든 데이터를 덮어쓰려고 하는 경우 FORMAT 절을 사용합니다. 필요에 따라 새 미디어에 미디어 이름과 설명을 지정합니다.  
  
        > [!IMPORTANT]  
        >  BACKUP 문의 FORMAT 절을 사용하는 경우 백업 미디어에 이전에 저장된 백업이 모두 삭제되므로 각별히 주의해야 합니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
  
#### <a name="a-backing-up-to-a-disk-device"></a>1\. 디스크 디바이스에 백업  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 을 사용하여 새 미디어 세트를 만들어 `FORMAT` 데이터베이스 전체를 디스크에 백업합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.Bak'  
   WITH FORMAT,  
      MEDIANAME = 'Z_SQLServerBackups',  
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
#### <a name="b-backing-up-to-a-tape-device"></a>2\. 테이프 디바이스에 백업  
 다음 예에서는 이전 백업에 백업을 추가하여 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]데이터베이스 전체를 테이프에 백업합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
   TO TAPE = '\\.\Tape0'  
   WITH NOINIT,  
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
#### <a name="c-backing-up-to-a-logical-tape-device"></a>3\. 논리적 테이프 디바이스에 백업  
 다음 예에서는 테이프 드라이브에 대한 논리적 백업 디바이스를 만듭니다. 그런 다음 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스 전체를 이 디바이스에 백업합니다.  
  
```sql  
-- Create a logical backup device,   
-- AdventureWorks2012_Bak_Tape, for tape device \\.\tape0.  
USE master;  
GO  
EXEC sp_addumpdevice 'tape', 'AdventureWorks2012_Bak_Tape', '\\.\tape0'; USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
   TO AdventureWorks2012_Bak_Tape  
   WITH FORMAT,  
      MEDIANAME = 'AdventureWorks2012_Bak_Tape',  
      MEDIADESCRIPTION = '\\.\tape0',   
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
##  <a name="PowerShellProcedure"></a> PowerShell 사용  
  
1.  `Backup-SqlDatabase` cmdlet을 사용합니다. 명시적으로 전체 데이터베이스 백업 임을 나타내기 위해를 지정 합니다 **-BackupAction** 매개 변수는 기본값을 사용 하 여 `Database`. 전체 데이터베이스 백업의 경우 이 매개 변수는 선택 사항입니다.  
  
     다음 예에서는 서버 인스턴스 `MyDB` 의 기본 백업 위치에 `Computer\Instance`데이터베이스의 전체 데이터베이스 백업을 만듭니다. 선택 사항으로, 이 예에서는 `-BackupAction Database`를 지정합니다.  
  
    ```  
    --Enter this command at the PowerShell command prompt, C:\PS>  
    Backup-SqlDatabase -ServerInstance Computer\Instance -Database MyDB -BackupAction Database  
    ```  
  
 **SQL Server PowerShell 공급자를 설정하고 사용하려면**  
  
-   [SQL Server PowerShell 공급자](../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [데이터베이스 백업(SQL Server)](create-a-full-database-backup-sql-server.md)  
  
-   [차등 데이터베이스 백업 만들기&#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)  
  
-   [데이터베이스 백업 복원 &#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [단순 복구 모델에서 데이터베이스 백업 복원&#40;Transact-SQL&#41;](restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)  
  
-   [전체 복구 모델에서 특정 오류 지점으로 데이터베이스 복원&#40;Transact-SQL&#41;](restore-database-to-point-of-failure-full-recovery.md)  
  
-   [데이터베이스를 새 위치로 복원&#40;SQL Server&#41;](restore-a-database-to-a-new-location-sql-server.md)  
  
-   [유지 관리 계획 마법사 사용](../maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
## <a name="see-also"></a>관련 항목  
 [백업 개요&#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [트랜잭션 로그 백업&#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)   
 [sp_addumpdevice&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)   
 [BACKUP&#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [데이터베이스 백업&#40;일반 페이지&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)   
 [데이터베이스 백업&#40;백업 옵션 페이지&#41;](back-up-database-backup-options-page.md)   
 [차등 백업&#40;SQL Server&#41;](differential-backups-sql-server.md)   
 [전체 데이터베이스 백업&#40;SQL Server&#41;](full-database-backups-sql-server.md)  
  
  
