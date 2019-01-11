---
title: URL에 대한 SQL Server 백업 | Microsoft 문서
ms.custom: ''
ms.date: 01/25/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 11be89e9-ff2a-4a94-ab5d-27d8edf9167d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d3911ab34a01b2da971aa602df37c8c559ed6390
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53359295"
---
# <a name="sql-server-backup-to-url"></a>URL에 대한 SQL Server 백업
  이 항목에서는 Windows Azure Blob 스토리지 서비스를 백업 대상으로 사용하는 데 필요한 개념, 요구 사항 및 구성 요소를 소개합니다. 백업 및 복원 기능은 디스크나 테이프를 사용하는 경우와 동일하거나 비슷하지만 몇 가지 차이점이 있습니다. 이러한 차이점과 주목할 만한 예외 및 몇 가지 코드 예가 이 항목에서 소개됩니다.  
  
## <a name="requirements-components-and-concepts"></a>요구 사항, 구성 요소 및 개념  
 **섹션 내용**  
  
-   [보안](#security)  
  
-   [주요 구성 요소 및 개념 소개](#intorkeyconcepts)  
  
-   [Windows Azure Blob Storage 서비스](#Blob)  
  
-   [SQL Server 구성 요소](#sqlserver)  
  
-   [제한 사항](#limitations)  
  
-   [Backup/Restore 문 지원](#Support)  
  
-   [SQL Server Management Studio에서 백업 태스크 사용](sql-server-backup-to-url.md#BackupTaskSSMS)  
  
-   [유지 관리 계획 마법사를 사용하여 URL로 SQL Server 백업](sql-server-backup-to-url.md#MaintenanceWiz)  
  
-   [SQL Server Management Studio를 사용하여 Windows Azure Storage에서 복원](sql-server-backup-to-url.md#RestoreSSMS)  
  
###  <a name="security"></a> 보안  
 다음은 Windows Azure Blob 스토리지 서비스로 백업하거나 복원하는 경우 보안 고려 사항과 요구 사항입니다.  
  
-   Windows Azure BLOB 스토리지 서비스의 컨테이너를 만들 때 액세스 권한을 **개인**으로 설정하는 것이 좋습니다. 액세스 권한을 개인으로 설정하면 사용자나 계정에 대한 액세스 시 필요한 정보를 제공해야 Windows Azure 계정 인증을 받을 수 있도록 제한됩니다.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 자격 증명에 Windows Azure 계정 이름과 액세스 키 인증을 저장해야 합니다. 이 정보는 백업 또는 복원 작업을 수행할 때 Windows Azure 계정 인증을 받는 데 사용됩니다.  
  
-   BACKUP 또는 RESTORE 명령을 실행하는 데 사용되는 사용자 계정은 **모든 자격 증명 변경** 권한이 있는 **db_backup operator** 데이터베이스 역할에 있어야 합니다.  
  
###  <a name="intorkeyconcepts"></a> 주요 구성 요소 및 개념 소개  
 다음 두 섹션에서는 Windows Azure Blob 스토리지 서비스와 Windows Azure Blob 스토리지 서비스로 백업하거나 복원하는 데 사용되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소를 소개합니다. 구성 요소와 Windows Azure Blob 스토리지 서비스로 백업하거나 복원할 때 구성 요소 간의 상호 작용을 이해하는 것이 중요합니다.  
  
 이 과정의 첫 단계는 Windows Azure 계정을 만드는 것입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 하는 **Windows Azure 저장소 계정 이름** 및 해당 **액세스 키** 인증 및 작성 하 고 읽는 blob 저장소 서비스에는 값입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 자격 증명은 이 인증 정보를 저장하며 백업 또는 복원 작업 중에 사용됩니다. 스토리지 계정을 만들고 간단한 복원을 수행하는 전체 연습은 [SQL Server 백업 및 복원에 Windows Azure 스토리지 서비스 사용 자습서](https://go.microsoft.com/fwlink/?LinkId=271615)를 참조하십시오.  
  
 ![sql 자격 증명에 저장소 계정 매핑](../../tutorials/media/backuptocloud-storage-credential-mapping.gif "sql 자격 증명에 저장소 계정 매핑")  
  
###  <a name="Blob"></a> Windows Azure Blob Storage 서비스  
 **저장소 계정:** 저장소 계정은 모든 저장소 서비스의 시작 지점입니다. Windows Azure Blob 스토리지 서비스에 액세스하려면 먼저 Windows Azure 스토리지 계정을 만듭니다. Windows Azure Blob 스토리지 서비스와 해당 구성 요소의 인증을 받으려면 **storage account name** 과 해당 **access key** 속성이 필요합니다.  
  
 **컨테이너:** 컨테이너에서는 그룹화된 blob 집합을 제공하며 blob을 무제한으로 저장할 수 있습니다. Microsoft Azure Blob service에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업을 쓰려면 적어도 루트 컨테이너가 만들어져 있어야 합니다.  
  
 **Blob:** 모든 형식과 크기의 파일입니다. Windows Azure Blob 스토리지 서비스에는 블록 Blob과 페이지 Blob이라는 두 가지 유형의 Blob을 저장할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업에서는 페이지 Blob을 Blob 유형으로 사용합니다. Blob은 다음 URL 형식을 사용 하 여 주소 지정 가능: https://\<저장소 계정 >.blob.core.windows.net/\<컨테이너 > /\<blob >  
  
 ![Azure Blob Storage](../../database-engine/media/backuptocloud-blobarchitecture.gif "Azure Blob Storage")  
  
 Windows Azure Blob 스토리지 서비스에 대한 자세한 내용은 [Windows Azure Blob 스토리지 서비스 사용 방법](http://www.windowsazure.com/develop/net/how-to-guides/blob-storage/)을 참조하십시오.  
  
 페이지 Blob에 대한 자세한 내용은 [블록 및 페이지 Blob 이해](https://msdn.microsoft.com/library/windowsazure/ee691964.aspx)를 참조하십시오.  
  
###  <a name="sqlserver"></a> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Components  
 **URL:** URL은 고유한 백업 파일에 대한 URI(Uniform Resource Identifier)를 지정합니다. URL은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 파일의 위치와 이름을 제공하는 데 사용됩니다. 이 구현에서는 Windows Azure 스토리지 계정의 페이지 Blob을 가리키는 URL만 유효합니다. URL은 컨테이너가 아닌 실제 Blob을 가리켜야 합니다. Blob이 없으면 만들어집니다. 기존 Blob 인 경우 지정 된, 백업 실패 "WITH FORMAT" 옵션을 지정 하지 않으면  
  
> [!WARNING]  
>  백업 파일을 복사하고 Windows Azure Blob 스토리지 서비스로 업로드하도록 선택하는 경우 페이지 Blob을 스토리지 옵션으로 사용하십시오. 블록 Blob에서 복원은 지원되지 않습니다. 블록 Blob 유형에서 RESTORE는 오류와 함께 실패합니다.  
  
 샘플 URL 값은: http[s]://ACCOUNTNAME.Blob.core.windows.net/\<컨테이너 > /\<FILENAME.bak >. HTTPS는 필수 사항은 아니지만 권장 사항입니다.  
  
 **자격 증명:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 자격 증명은 SQL Server 외부의 리소스에 연결하는 데 필요한 인증 정보를 저장하는 데 사용되는 개체입니다.  여기에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 및 복원 프로세스에서 자격 증명을 사용하여 Windows Azure Blob 스토리지 서비스의 인증을 받습니다. 자격 증명에는 스토리지 계정 이름과 스토리지 계정 **액세스 키** 값이 저장됩니다. 만든 자격 증명은 BACKUP/RESTORE 문을 실행할 때 WITH CREDENTIAL 옵션에 지정해야 합니다. 보기, 복사 또는 저장소 계정을 다시 생성 하는 방법에 대 한 자세한 내용은 **액세스 키**를 참조 하십시오 [저장소 계정 액세스 키](https://msdn.microsoft.com/library/windowsazure/hh531566.aspx)합니다.  
  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 자격 증명을 만드는 방법에 대한 단계별 지침은 이 항목 뒷부분의 [Create a Credential](#credential) 예제를 참조하십시오.  
  
 자격 증명에 대한 자세한 내용은 [자격 증명](../security/authentication-access/credentials-database-engine.md)을 참조하세요.  
  
 자격 증명이 사용되는 다른 예에 대한 정보는 [SQL Server 에이전트 프록시 만들기](../../ssms/agent/create-a-sql-server-agent-proxy.md)를 참조하세요.  
  
###  <a name="limitations"></a> 제한 사항  
  
-   Premium 스토리지로 백업은 지원 되지 않습니다.  
  
-   지원되는 최대 백업 크기는 1TB입니다.  
  
-   TSQL, SMO 또는 PowerShell cmdlet을 사용하여 백업 또는 복원 문을 실행할 수 있습니다. 현재 SQL Server Management Studio 백업 또는 복원 마법사로 Windows Azure Blob 스토리지 서비스로 백업하거나 복원할 수는 없습니다.  
  
-   논리적 디바이스 이름을 만들 수 없습니다. 따라서 SQL Server Management Studio나 sp_dumpdevice를 사용하여 URL을 백업 디바이스로 추가할 수 없습니다.  
  
-   기존 백업 Blob에 추가는 지원되지 않습니다. 기존 Blob으로 백업은 WITH FORMAT 옵션을 사용하여 덮어쓸 수만 있습니다.  
  
-   단일 백업 작업에서 여러 blob으로 백업은 지원되지 않습니다. 예를 들어 다음은 오류를 반환합니다.  
  
    ```  
    BACKUP DATABASE AdventureWorks2012   
    TO URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012_1.bak'   
       URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012_2.bak'   
          WITH CREDENTIAL = 'mycredential'   
         ,STATS = 5;  
    GO  
  
    ```  
  
-   `BACKUP`에 블록 크기 지정은 지원되지 않습니다.  
  
-   `MAXTRANSFERSIZE` 지정은 지원되지 않습니다.  
  
-   `RETAINDAYS`와 `EXPIREDATE` 백업 세트 옵션 지정은 지원되지 않습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 백업 장치 이름이 최대 259자로 제한됩니다. BACKUP TO URL에서 URL - ‘https://.blob.core.windows.net//.bak’를 지정하는 데 사용되는 필수 요소에 36자가 사용되며, 계정, 컨테이너 및 blob 이름에 사용할 수 있는 문자는 223자입니다.  
  
###  <a name="Support"></a> Backup/Restore 문 지원  
  
|||||  
|-|-|-|-|  
|Backup/Restore 문|지원됨|예외|주석|  
|BACKUP|???|BLOCKSIZE 및 MAXTRANSFERSIZE는 지원되지 않습니다.|WITH CREDENTIAL 지정 필요|  
|RESTORE|???||WITH CREDENTIAL 지정 필요|  
|RESTORE FILELISTONLY|???||WITH CREDENTIAL 지정 필요|  
|RESTORE HEADERONLY|???||WITH CREDENTIAL 지정 필요|  
|RESTORE LABELONLY|???||WITH CREDENTIAL 지정 필요|  
|RESTORE VERIFYONLY|???||WITH CREDENTIAL 지정 필요|  
|RESTORE REWINDONLY|???|||  
  
 구문과 Backup 문에 대한 자세한 내용은 [BACKUP&#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)을 참조하세요.  
  
 구문과 Restore 문에 대한 자세한 내용은 [RESTORE&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)을 참조하세요.  
  
### <a name="support-for-backup-arguments"></a>Backup 인수 지원  
  
|||||  
|-|-|-|-|  
|인수|지원됨|예외|주석|  
|DATABASE|???|||  
|LOG|???|||  
||  
|TO (URL)|???|DISK 및 TAPE와 달리 URL은 논리적 이름 지정 및 작성을 지원하지 않습니다.|이 인수는 백업 파일에 대한 URL 경로를 지정하는 데 사용됩니다.|  
|MIRROR TO|???|||  
|**WITH 옵션:**||||  
|CREDENTIAL|???||WITH CREDENTIAL은 BACKUP TO URL 옵션을 사용하여 Windows Azure Blob 스토리지 서비스로 백업할 때만 지원됩니다.|  
|DIFFERENTIAL|???|||  
|COPY_ONLY|???|||  
|COMPRESSION&#124;NO_COMPRESSION|???|||  
|DESCRIPTION|???|||  
|NAME|???|||  
|EXPIREDATE &#124; RETAINDAYS|???|||  
|NOINIT &#124; INIT|???||이 옵션은 사용 시 무시됩니다.<br /><br /> Blob에 추가는 불가능합니다. 백업을 덮어쓰려면 FORMAT 인수를 사용하십시오.|  
|NOSKIP &#124; SKIP|???|||  
|NOFORMAT &#124; FORMAT|???||이 옵션은 사용 시 무시됩니다.<br /><br /> WITH FORMAT을 지정하지 않으면 기존 blob으로 백업이 실패합니다. WITH FORMAT을 지정하면 기존 blob을 덮어씁니다.|  
|MEDIADESCRIPTION|???|||  
|MEDIANAME|???|||  
|BLOCKSIZE|???|||  
|BUFFERCOUNT|???|||  
|MAXTRANSFERSIZE|???|||  
|NO_CHECKSUM &#124; CHECKSUM|???|||  
|STOP_ON_ERROR &#124; CONTINUE_AFTER_ERROR|???|||  
|STATS|???|||  
|REWIND &#124; NOREWIND|???|||  
|UNLOAD &#124; NOUNLOAD|???|||  
|NORECOVERY &#124; STANDBY|???|||  
|NO_TRUNCATE|???|||  
  
 Backup 인수에 대한 자세한 내용은 [BACKUP&#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)을 참조하세요.  
  
### <a name="support-for-restore-arguments"></a>Restore 인수 지원  
  
|||||  
|-|-|-|-|  
|인수|지원됨|예외|주석|  
|DATABASE|???|||  
|LOG|???|||  
|FROM (URL)|???||FROM URL 인수는 백업 파일에 대한 URL 경로를 지정하는 데 사용됩니다.|  
|**WITH Options:**||||  
|CREDENTIAL|???||WITH CREDENTIAL은 RESTORE FROM URL 옵션을 사용하여 Windows Azure Blob 스토리지 서비스에서 복원할 때만 지원됩니다.|  
|PARTIAL|???|||  
|RECOVERY &#124; NORECOVERY &#124; STANDBY|???|||  
|LOADHISTORY|???|||  
|MOVE|???|||  
|REPLACE|???|||  
|RESTART|???|||  
|RESTRICTED_USER|???|||  
|FILE|???|||  
|PASSWORD|???|||  
|MEDIANAME|???|||  
|MEDIAPASSWORD|???|||  
|BLOCKSIZE|???|||  
|BUFFERCOUNT|???|||  
|MAXTRANSFERSIZE|???|||  
|CHECKSUM &#124; NO_CHECKSUM|???|||  
|STOP_ON_ERROR &#124; CONTINUE_AFTER_ERROR|???|||  
|FILESTREAM|???|||  
|STATS|???|||  
|REWIND &#124; NOREWIND|???|||  
|UNLOAD &#124; NOUNLOAD|???|||  
|KEEP_REPLICATION|???|||  
|KEEP_CDC|???|||  
|ENABLE_BROKER &#124; ERROR_BROKER_CONVERSATIONS &#124; NEW_BROKER|???|||  
|STOPAT &#124; STOPATMARK &#124; STOPBEFOREMARK|???|||  
  
 Restore 인수에 대한 자세한 내용은 [RESTORE 인수&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql)를 참조하세요.  
  
##  <a name="BackupTaskSSMS"></a> SQL Server Management Studio에서 백업 태스크 사용  
 SQL Server Management Studio의 백업 태스크는 대상 옵션 중 하나로 URL을 포함하고 Windows Azure 스토리지로 백업하는 데 필요한 다른 지원 개체(예: SQL 자격 증명)를 포함하도록 개선되었습니다.  
  
 다음 단계에서는 Windows Azure 스토리지로 백업할 수 있도록 변경된 데이터베이스 백업 태스크에 대해 설명합니다.  
  
1.  SQL Server Management Studio를 시작하고 SQL Server 인스턴스에 연결합니다.  백업을 마우스 오른쪽 단추로 클릭 하려는 데이터베이스를 선택 **태스크**, 선택한 **백업...** . 데이터베이스 백업 대화 상자가 열립니다.  
  
2.  일반 페이지에서 **URL** 옵션이 Windows Azure 스토리지에 백업을 만드는 데 사용됩니다. 이 옵션을 선택하면 이 페이지에서 다음과 같은 옵션을 사용할 수 있습니다.  
  
    1.  **파일 이름:** 백업 파일의 이름입니다.  
  
    2.  **SQL 자격 증명:** 기존 SQL Server 자격 증명을 지정 하거나를 클릭 하 여 새로 만들 수 있습니다 합니다 **만들기** SQL 자격 증명 상자 옆에 있습니다.  
  
        > [!IMPORTANT]  
        >  **만들기** 를 클릭하면 열리는 대화 상자에서는 관리 인증서나 구독용 게시 프로필이 필요합니다. SQL Server는 현재 프로필 버전 2.0 게시를 지원합니다. 게시 프로필의 지원되는 버전을 다운로드하려면 [게시 프로필 2.0 다운로드](https://go.microsoft.com/fwlink/?LinkId=396421)를 참조하세요.  
        >   
        >  관리 인증서나 게시 프로필에 액세스할 수 없는 경우 Transact-SQL이나 SQL Server Management Studio를 사용하여 스토리지 계정 이름을 지정하고 키 정보에 액세스하여 SQL 자격 증명을 만들 수 있습니다. [자격 증명 만들기](#credential) 섹션의 예제 코드를 보고 Transact-SQL을 사용하여 자격 증명을 만듭니다. 또는 SQL Server Management Studio를 사용하여 데이터베이스 엔진 인스턴스에서 **보안**을 마우스 오른쪽 단추로 클릭하고 **새로 만들기**, **자격 증명**을 차례로 선택합니다. **ID** 에 대한 저장소 계정 이름을 지정하고 **암호** 필드에 액세스 키를 지정합니다.  
  
    3.  **Azure 저장소 컨테이너:** 백업 파일을 저장할 Windows Azure 저장소 컨테이너의 이름입니다.  
  
    4.  **URL 접두사:** 이전 단계에서 설명하는 필드에서 지정된 정보를 사용하여 자동으로 만들어집니다. 이 값을 수동으로 편집하는 경우 이전에 제공한 다른 정보와 일치하는지 확인해야 합니다. 예를 들어 스토리지 URL을 수정하는 경우 SQL 자격 증명이 동일한 스토리지 계정에 인증하도록 설정되었는지 확인합니다.  
  
 URL을 대상으로 선택하는 경우 **미디어 옵션** 페이지의 특정 옵션을 사용할 수 없습니다.  다음 항목에서는 데이터베이스 백업 대화 상자에 대한 자세한 정보를 제공합니다.  
  
 [데이터베이스 백업&#40;일반 페이지&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
 [데이터베이스 백업&#40;미디어 옵션 페이지&#41;](back-up-database-media-options-page.md)  
  
 [데이터베이스 백업&#40;백업 옵션 페이지&#41;](back-up-database-backup-options-page.md)  
  
 [자격 증명 만들기 - Azure Storage 인증](create-credential-authenticate-to-azure-storage.md)  
  
##  <a name="MaintenanceWiz"></a> 유지 관리 계획 마법사를 사용하여 URL로 SQL Server 백업  
 이전에 설명한 백업 태스크와 마찬가지로, SQL Server Management Studio의 유지 관리 계획 마법사는 대상 옵션 중 하나로 **URL** 을 포함하고 Windows Azure 스토리지로 백업하는 데 필요한 다른 지원 개체(예: SQL 자격 증명)를 포함하도록 개선되었습니다. 자세한 내용은 **Using Maintenance Plan Wizard** 의 [백업 태스크 정의](../maintenance-plans/use-the-maintenance-plan-wizard.md#SSMSProcedure)를 참조하세요.  
  
##  <a name="RestoreSSMS"></a> Windows Azure storage Using SQL Server Management Studio에서 복원  
 데이터베이스를 복원하는 경우 **URL** 이 복원할 원본 디바이스로 포함됩니다. 다음 단계에서는 Windows Azure 스토리지에서 복원할 수 있도록 변경된 복원 태스크에 대해 설명합니다.  
  
1.  SQL Server Management Studio에 있는 복원 태스크의 **일반** 페이지에서 **디바이스** 를 선택하면 **URL** 이 백업 미디어 유형으로 포함된 **백업 디바이스 선택** 대화 상자가 표시됩니다.  
  
2.  **URL** 을 선택하고 **추가**를 클릭하면 **Azure 저장소에 연결** 대화 상자가 열립니다. Windows Azure 스토리지에 인증하기 위한 SQL 자격 증명 정보를 지정합니다.  
  
3.  이렇게 하면 SQL Server는 제공한 SQL 자격 증명 정보를 사용하여 Windows Azure 스토리지에 연결하고 **Windows Azure에서 백업 파일 찾기** 대화 상자를 엽니다. 스토리지에 있는 백업 파일이 이 페이지에 표시됩니다. 복원하는 데 사용할 파일을 선택하고 **확인**을 클릭합니다. **백업 장치 선택** 대화 상자가 표시됩니다. 이 대화 상자에서 **확인** 을 클릭하면 복원을 완료할 수 있는 기본 **복원** 대화 상자가 표시됩니다.  자세한 내용은 다음 항목을 참조하십시오.  
  
     [데이터베이스 복원&#40;일반 페이지&#41;](restore-database-general-page.md)  
  
     [데이터베이스 복원&#40;파일 페이지&#41;](restore-database-files-page.md)  
  
     [데이터베이스 복원&#40;옵션 페이지&#41;](restore-database-options-page.md)  
  
##  <a name="Examples"></a> 코드 예제  
 이 섹션에서는 다음과 같은 예를 보여 줍니다.  
  
-   [자격 증명 만들기](#credential)  
  
-   [전체 데이터베이스 백업](#complete)  
  
-   [데이터베이스 및 로그 백업](#databaselog)  
  
-   [주 파일 그룹의 전체 파일 백업 만들기](#filebackup)  
  
-   [주 파일 그룹의 차등 파일 백업 만들기](#differential)  
  
-   [데이터베이스 복원 및 파일 이동](#restoredbwithmove)  
  
-   [STOPAT를 사용하여 지정 시간으로 복원](#PITR)  
  
###  <a name="credential"></a> 자격 증명 만들기  
 다음 예에서는 Windows Azure 스토리지 인증 정보를 저장하는 자격 증명을 만듭니다.  
  
1.  **tsql**  
  
    ```  
    IF NOT EXISTS  
    (SELECT * FROM sys.credentials   
    WHERE credential_identity = 'mycredential')  
    CREATE CREDENTIAL mycredential WITH IDENTITY = 'mystorageaccount'  
    ,SECRET = '<storage access key>' ;  
  
    ```  
  
2.  **C#**  
  
    ```  
    // Connect to default sql server instance on local machine  
    Server server = new Server(".");  
    string identity = "mystorageaccount";  
    string secret = "<storage access key>";  
  
    // Create a Credential  
    string credentialName = "mycredential";  
    Credential credential = new Credential(server, credentialName);  
    credential.Create(identity, secret);  
    ```  
  
3.  **PowerShell**  
  
    ```  
    # create variables  
    $storageAccount = "mystorageaccount"  
    $storageKey = "<storage access key>"  
    $secureString = convertto-securestring $storageKey  -asplaintext -force  
    $credentialName = "mycredential"  
  
    $srvPath = "SQLSERVER:\SQL\COMPUTERNAME\INSTANCENAME"  
    # for default instance, the $srvpath variable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
    # Create a credential  
     New-SqlCredential -Name $credentialName -Path $srvpath -Identity $storageAccount -Secret $secureString  
  
    ```  
  
###  <a name="complete"></a> 전체 데이터베이스 백업  
 다음 예에서는 Windows Azure Blob 스토리지 서비스에 AdventureWorks2012 데이터베이스를 백업합니다.  
  
1.  **tsql**  
  
    ```  
    BACKUP DATABASE AdventureWorks2012   
    TO URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012.bak'   
          WITH CREDENTIAL = 'mycredential'   
         ,COMPRESSION  
         ,STATS = 5;  
    GO  
  
    ```  
  
1.  **C#**  
  
    ```  
    // Connect to default sql server instance on local machine  
    Server server = new Server(".");  
    string identity = "mystorageaccount";  
  
    string credentialName = "mycredential";  
    string dbName = "AdventureWorks2012";  
    string blobContainerName = "mycontainer";  
  
    // Generate Unique Url  
    string url = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup to Url  
    Backup backup = new Backup();  
    backup.CredentialName = credentialName;  
    backup.Database = dbName;  
    backup.CompressionOption = BackupCompressionOptions.On;  
    backup.Devices.AddDevice(url, DeviceType.Url);  
    backup.SqlBackup(server);  
    ```  
  
2.  **PowerShell**  
  
    ```  
    # create variables  
    $backupUrlContainer = "https://mystorageaccount.blob.core.windows.net/mycontainer/"  
    $credentialName = "mycredential"  
    $srvPath = "SQLSERVER:\SQL\COMPUTERNAME\INSTANCENAME"   
    # for default instance, the $srvpath varilable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
    # navigate to SQL Server Instance  
    CD $srvPath   
    $backupFile = $backupUrlContainer + "AdventureWorks2012" +  ".bak"  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName -CompressionOption On  
  
    ```  
  
###  <a name="databaselog"></a> 데이터베이스 및 로그 백업  
 다음 예에서는 기본적으로 단순 복구 모델을 사용하는 AdventureWorks2012 예제 데이터베이스를 백업하고 로그 백업을 지원하기 위해 전체 복구 모델을 사용하도록 AdventureWorks2012 데이터베이스를 수정합니다. 마지막으로 Windows Azure Blob에 대한 전체 데이터베이스 백업을 만들고 업데이트 작업 기간이 경과된 후 로그를 백업합니다. 이 예에서는 날짜/시간 스탬프를 포함한 백업 파일 이름을 만듭니다.  
  
1.  **tsql**  
  
    ```  
    -- To permit log backups, before the full database backup, modify the database   
    -- to use the full recovery model.  
    USE master;  
    GO  
    ALTER DATABASE AdventureWorks2012  
       SET RECOVERY FULL;  
    GO  
  
    -- Back up the full AdventureWorks2012 database.  
           -- First create a file name for the backup file with DateTime stamp  
  
    DECLARE @Full_Filename AS VARCHAR (300);  
    SET @Full_Filename = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012_Full_'+   
    REPLACE (REPLACE (REPLACE (CONVERT (VARCHAR (40), GETDATE (), 120), '-','_'),':', '_'),' ', '_') + '.bak';   
    --Back up Adventureworks2012 database  
  
    BACKUP DATABASE AdventureWorks2012  
    TO URL =  @Full_Filename  
    WITH CREDENTIAL = 'mycredential';  
    ,COMPRESSION  
    GO  
    -- Back up the AdventureWorks2012 log.  
    DECLARE @Log_Filename AS VARCHAR (300);  
    SET @Log_Filename = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012_Log_'+   
    REPLACE (REPLACE (REPLACE (CONVERT (VARCHAR (40), GETDATE (), 120), '-','_'),':', '_'),' ', '_') + '.trn';  
    BACKUP LOG AdventureWorks2012  
     TO URL = @Log_Filename  
    WITH CREDENTIAL = 'mycredential'  
    ,COMPRESSION;  
    GO  
    ```  
  
2.  **C#**  
  
    ```  
    // Connect to default sql server instance on local machine  
    Server server = new Server(".");  
    string identity = "mystorageaccount";  
  
    string credentialName = "mycredential";  
    string dbName = "AdventureWorks2012";  
    string blobContainerName = "mycontainer";  
  
    // Generate Unique Url for data backup  
    string urlDataBackup = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}_Data-{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup Database to Url  
    Backup backupData = new Backup();  
    backupData.CredentialName = credentialName;  
    backupData.Database = dbName;  
    backup.CompressionOption = BackupCompressionOptions.On;  
    backupData.Devices.AddDevice(urlDataBackup, DeviceType.Url);  
    backupData.SqlBackup(server);  
  
    // Generate Unique Url for data backup  
    string urlLogBackup = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}_Log-{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup Database Log to Url  
    Backup backupLog = new Backup();  
    backupLog.CredentialName = credentialName;  
    backupLog.Database = dbName;  
    backup.CompressionOption = BackupCompressionOptions.On;  
    backupLog.Devices.AddDevice(urlLogBackup, DeviceType.Url);  
    backupLog.Action = BackupActionType.Log;  
    backupLog.SqlBackup(server);  
    ```  
  
3.  **PowerShell**  
  
    ```  
  
    #create variables  
    $backupUrlContainer = "https://mystorageaccount.blob.core.windows.net/mycontainer/"  
    $credentialName = "mycredential"  
    $srvPath = "SQLSERVER:\SQL\COMPUTERNAME\INSTANCENAME"  
    # for default instance, the $srvpath variable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
    # navigate to theSQL Server Instance  
  
    CD $srvPath   
    #Create a unique file name for the full database backup  
    $backupFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".bak"  
  
    #Backup Database to URL  
  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName -CompressionOption On -BackupAction Database    
  
    #Create a unique file name for log backup  
  
    $backupFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".trn"  
  
    #Backup Log to URL  
  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName -CompressionOption On -BackupAction Log  
  
    ```  
  
###  <a name="filebackup"></a> 주 파일 그룹의 전체 파일 백업 만들기  
 다음 예에서는 PRIMARY 파일 그룹의 전체 파일 백업을 만듭니다.  
  
1.  **tsql**  
  
    ```  
    --Back up the files in Primary:  
    BACKUP DATABASE AdventureWorks2012  
       FILEGROUP = 'Primary'  
       TO URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012files.bck'  
       WITH CREDENTIAL = 'mycredential'  
       ,COMPRESSION;  
    GO  
    ```  
  
2.  **C#**  
  
    ```  
    // Connect to default sql server instance on local machine  
    Server server = new Server(".");  
    string identity = "mystorageaccount";  
  
    string credentialName = "mycredential";  
    string dbName = "AdventureWorks2012";  
    string blobContainerName = "mycontainer";  
  
    // Generate Unique Url  
    string url = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-{3}.bck",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup to Url  
    Backup backup = new Backup();  
    backup.CredentialName = credentialName;  
    backup.Database = dbName;  
    backup.Action = BackupActionType.Files;  
    backup.DatabaseFileGroups.Add("PRIMARY");  
    backup.CompressionOption = BackupCompressionOptions.On;  
    backup.Devices.AddDevice(url, DeviceType.Url);  
    backup.SqlBackup(server);  
  
    ```  
  
3.  **PowerShell**  
  
    ```  
  
    #create variables  
    $backupUrlContainer = "https://mystorageaccount.blob.core.windows.net/mycontainer/"  
    $credentialName = "mycredential"  
    $srvPath = "SQLSERVER:\SQL\COMPUTERNAME\INSTANCENAME"  
    # for default instance, the $srvpath variable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
    # navigate to the SQL Server Instance  
  
    CD $srvPath   
    #Create a unique file name for the file backup  
    $backupFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".bck"  
  
    #Backup Primary File Group to URL  
  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName -CompressionOption On -BackupAction Files -DatabaseFileGroup Primary  
  
    ```  
  
###  <a name="differential"></a> 주 파일 그룹의 차등 파일 백업 만들기  
 다음 예에서는 PRIMARY 파일 그룹의 차등 파일 백업을 만듭니다.  
  
1.  **tsql**  
  
    ```  
    --Back up the files in Primary:  
    BACKUP DATABASE AdventureWorks2012  
       FILEGROUP = 'Primary'  
       TO URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012filesdiff.bck'  
       WITH   
          CREDENTIAL = 'mycredential'  
          ,COMPRESSION  
      ,DIFFERENTIAL;  
    GO  
  
    ```  
  
2.  **C#**  
  
    ```  
    // Connect to default sql server instance on local machine  
    Server server = new Server(".");  
    string identity = "mystorageaccount";  
  
    string credentialName = "mycredential";  
    string dbName = "AdventureWorks2012";  
    string blobContainerName = "mycontainer";  
  
    // Generate Unique Url  
    string url = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup to Url  
    Backup backup = new Backup();  
    backup.CredentialName = credentialName;  
    backup.Database = dbName;  
    backup.Action = BackupActionType.Files;  
    backup.DatabaseFileGroups.Add("PRIMARY");  
    backup.Incremental = true;  
    backup.CompressionOption = BackupCompressionOptions.On;  
    backup.Devices.AddDevice(url, DeviceType.Url);  
    backup.SqlBackup(server);  
  
    ```  
  
3.  **PowerShell**  
  
    ```  
  
    #create variables  
    $backupUrlContainer = "https://mystorageaccount.blob.core.windows.net/mycontainer/"  
    $credentialName = "mycredential"  
    $srvPath = "SQLSERVER:\SQL\COMUTERNAME\INSTANCENAME"  
    # for default instance, the $srvpath variable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
    # navigate to SQL Server Instance  
  
    CD $srvPath   
  
    #create a unique file name for the full backup  
    $backupdbFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".bak"  
  
    #Create a differential backup of the primary filegroup  
  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName -CompressionOption On -BackupAction Files -DatabaseFileGroup Primary -Incremental  
  
    ```  
  
###  <a name="restoredbwithmove"></a> 데이터베이스를 복원 및 파일 이동  
 전체 데이터베이스 백업을 복원하고 C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Data 디렉터리로 복원한 데이터베이스를 이동하려면 다음 단계를 수행합니다.  
  
1.  **tsql**  
  
    ```  
    -- Backup the tail of the log first  
  
    DECLARE @Log_Filename AS VARCHAR (300);  
    SET @Log_Filename = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012_Log_'+   
    REPLACE (REPLACE (REPLACE (CONVERT (VARCHAR (40), GETDATE (), 120), '-','_'),':', '_'),' ', '_') + '.trn';  
    BACKUP LOG AdventureWorks2012  
     TO URL = @Log_Filename  
    WITH CREDENTIAL = 'mycredential'  
    ,NORECOVERY;  
    GO  
  
    RESTORE DATABASE AdventureWorks2012 FROM URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012.bak'  
    WITH CREDENTIAL = 'mycredential'  
    ,MOVE 'AdventureWorks2012_data' to 'C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.mdf'  
    ,MOVE 'AdventureWorks2012_log' to 'C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.ldf'  
    ,STATS = 5  
  
    ```  
  
2.  **C#**  
  
    ```  
    // Connect to default sql server instance on local machine  
    Server server = new Server(".");  
    string identity = "mystorageaccount";  
  
    string credentialName = "mycredential";  
    string dbName = "AdventureWorks2012";  
    string blobContainerName = "mycontainer";  
  
    // Generate Unique Url  
    string urlBackupData = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-Data{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup to Url  
    Backup backup = new Backup();  
    backup.CredentialName = credentialName;  
    backup.Database = dbName;  
    backup.Devices.AddDevice(urlBackupData, DeviceType.Url);  
    backup.SqlBackup(server);  
  
    // Generate Unique Url for tail log backup  
    string urlTailLogBackup = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-TailLog{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup Tail Log to Url  
    Backup backupTailLog = new Backup();  
    backupTailLog.CredentialName = credentialName;  
    backupTailLog.Database = dbName;  
    backupTailLog.Action = BackupActionType.Log;  
    backupTailLog.NoRecovery = true;  
    backupTailLog.Devices.AddDevice(urlTailLogBackup, DeviceType.Url);  
    backupTailLog.SqlBackup(server);  
  
    // Restore a database and move files  
    string newDataFilePath = server.MasterDBLogPath  + @"\" + dbName + DateTime.Now.ToString("s").Replace(":", "-") + ".mdf";  
    string newLogFilePath = server.MasterDBLogPath  + @"\" + dbName + DateTime.Now.ToString("s").Replace(":", "-") + ".ldf";  
  
    Restore restore = new Restore();  
    restore.CredentialName = credentialName;  
    restore.Database = dbName;  
    restore.ReplaceDatabase = true;  
    restore.Devices.AddDevice(urlBackupData, DeviceType.Url);  
    restore.RelocateFiles.Add(new RelocateFile(dbName, newDataFilePath));  
    restore.RelocateFiles.Add(new RelocateFile(dbName+ "_Log", newLogFilePath));  
    restore.SqlRestore(server);  
  
    ```  
  
3.  **PowerShell**  
  
    ```  
  
    #create variables  
    $backupUrlContainer = "https://mystorageaccount.blob.core.windows.net/mycontainer/"  
    $credentialName = "mycredential"  
    $srvPath = "SQLSERVER:\SQL\COMPUTERNAME\INSTNACENAME"  
    # for default instance, the $srvpath variable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
    # navigate to SQL Server Instance   
  
    CD $srvPath   
  
    #create a unique file name for the full backup  
    $backupdbFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".bak"  
  
    # Full database backup to URL  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupdbFile  -SqlCredential $credentialName -CompressionOption On      
  
    #Create a unique file name for the tail log backup  
    $backuplogFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".trn"  
  
    #Backup tail log to URL  
  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName  -BackupAction Log -NoRecovery    
  
    # Restore Database and move files  
  
    $newDataFilePath = New-Object Microsoft.SqlServer.Management.Smo.RelocateFile ("AdventureWorks_Data","C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.mdf")  
    $newLogFilePath = New-Object Microsoft.SqlServer.Management.Smo.RelocateFile("AdventureWorks_Log","C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.ldf")  
  
    Restore-SqlDatabase -Database AdventureWorks2012 -SqlCredential $credentialName -BackupFile $backupdbFile -RelocateFile @($newDataFilePath,$newLogFilePath)  
  
    ```  
  
###  <a name="PITR"></a> STOPAT를 사용하여 지정 시간으로 복원  
 다음 예에서는 지정 시간의 상태로 데이터베이스를 복원하고 복원 작업을 보여 줍니다.  
  
1.  **tsql**  
  
    ```  
    RESTORE DATABASE AdventureWorks FROM URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012.bak'   
    WITH   
     CREDENTIAL = 'mycredential'  
    ,MOVE 'AdventureWorks2012_data' to 'C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.mdf'  
    ,Move 'AdventureWorks2012_log' to 'C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.ldf'  
    ,NORECOVERY  
    --,REPLACE  
    ,STATS = 5;  
    GO   
  
    RESTORE LOG AdventureWorks FROM URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012.trn'   
    WITH CREDENTIAL = 'mycredential'  
    ,RECOVERY   
    ,STOPAT = 'Oct 23, 2012 5:00 PM'   
    GO  
    ```  
  
2.  **C#**  
  
    ```  
    // Connect to default sql server instance on local machine  
    Server server = new Server(".");  
    string identity = "mystorageaccount";  
  
    string credentialName = "mycredential";  
    string dbName = "AdventureWorks2012";  
    string blobContainerName = "mycontainer";  
  
    // Generate Unique Url  
    string urlBackupData = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-Data{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup to Url  
    Backup backup = new Backup();  
    backup.CredentialName = credentialName;  
    backup.Database = dbName;  
    backup.Devices.AddDevice(urlBackupData, DeviceType.Url);  
    backup.SqlBackup(server);  
  
    // Generate Unique Url for Tail Log backup  
    string urlTailLogBackup = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-TailLog{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup Tail Log to Url  
    Backup backupTailLog = new Backup();  
    backupTailLog.CredentialName = credentialName;  
    backupTailLog.Database = dbName;  
    backupTailLog.Action = BackupActionType.Log;  
    backupTailLog.NoRecovery = true;  
    backupTailLog.Devices.AddDevice(urlTailLogBackup, DeviceType.Url);  
    backupTailLog.SqlBackup(server);  
  
    // Restore a database and move files  
    string newDataFilePath = server.MasterDBLogPath + @"\" + dbName + DateTime.Now.ToString("s").Replace(":", "-") + ".mdf";  
    string newLogFilePath = server.MasterDBLogPath + @"\" + dbName + DateTime.Now.ToString("s").Replace(":", "-") + ".ldf";  
  
    Restore restore = new Restore();  
    restore.CredentialName = credentialName;  
    restore.Database = dbName;  
    restore.ReplaceDatabase = true;  
    restore.NoRecovery = true;  
    restore.Devices.AddDevice(urlBackupData, DeviceType.Url);  
    restore.RelocateFiles.Add(new RelocateFile(dbName, newDataFilePath));  
    restore.RelocateFiles.Add(new RelocateFile(dbName + "_Log", newLogFilePath));  
    restore.SqlRestore(server);  
  
    // Restore transaction Log with stop at   
    Restore restoreLog = new Restore();  
    restoreLog.CredentialName = credentialName;  
    restoreLog.Database = dbName;  
    restoreLog.Action = RestoreActionType.Log;  
    restoreLog.Devices.AddDevice(urlBackupData, DeviceType.Url);  
    restoreLog.ToPointInTime = DateTime.Now.ToString();   
    restoreLog.SqlRestore(server);  
  
    ```  
  
3.  **PowerShell**  
  
    ```  
  
    #create variables  
    $backupUrlContainer = "https://mystorageaccount.blob.core.windows.net/mycontainer/"  
    $credentialName = "mycredential"  
    $srvPath = "SQLSERVER:\SQL\COMPUTERNAME\INSTANCENAME"  
    # for default instance, the $srvpath variable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
    # Navigate to SQL Server Instance Directory  
  
    CD $srvPath   
  
    #create a unique file name for the full backup  
    $backupdbFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".bak"  
  
    # Full database backup to URL  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupdbFile  -SqlCredential $credentialName -CompressionOption On     
  
    #Create a unique file name for the tail log backup  
    $backuplogFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".trn"  
  
    #Backup tail log to URL  
  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName  -BackupAction Log -NoRecovery     
  
    # Restore Database and move files  
  
    $newDataFilePath = New-Object Microsoft.SqlServer.Management.Smo.RelocateFile ("AdventureWorks_Data","C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.mdf")  
    $newLogFilePath = New-Object Microsoft.SqlServer.Management.Smo.RelocateFile("AdventureWorks_Log","C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.ldf")  
  
    Restore-SqlDatabase -Database AdventureWorks2012 -SqlCredential $credentialName -BackupFile $backupdbFile -RelocateFile @($newDataFilePath,$newLogFilePath) -NoRecovery    
  
    # Restore Transaction log with Stop At:  
    Restore-SqlDatabase -Database AdventureWorks2012 -SqlCredential $credentialName -BackupFile $backuplogFile  -ToPointInTime (Get-Date).ToString()  
  
    ```  
  
## <a name="see-also"></a>관련 항목  
 [URL에 대한 SQL Server 백업 - 최상의 방법 및 문제 해결](sql-server-backup-to-url-best-practices-and-troubleshooting.md)   
 [시스템 데이터베이스 백업 및 복원&#40;SQL Server&#41;](back-up-and-restore-of-system-databases-sql-server.md)   
 [자습서: Windows Azure Blob Storage Service로 SQL Server 백업 및 복원](../tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)  
  
  
