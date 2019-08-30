---
title: Azure에 대 한 관리 되는 백업 SQL Server-보존 및 저장소 설정 | Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: c4aa26ea-5465-40cc-8b83-f50603cb9db1
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 01baba17c4bff887b2d49bcd74b71765ffb401e7
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153978"
---
# <a name="sql-server-managed-backup-to-azure---retention-and-storage-settings"></a>Azure에 대 한 관리 되는 백업 SQL Server-보존 및 저장소 설정
  이 항목에서는 데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 을 구성하고 인스턴스에 대한 기본 설정을 구성하는 기본 단계에 대해 설명합니다. 이 항목에서는 인스턴스에 대한 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 서비스를 일시 중지하고 다시 시작하는 데 필요한 단계에 대해 설명합니다.  
  
 설정 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 에 대 한 전체 연습은 [azure에 대 한 관리 되는 백업 SQL Server 설정](../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md) 및 [가용성 그룹에 대 한 azure로 관리 되는 백업 SQL Server 설정](../../2014/database-engine/setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups.md)을 참조 하세요.  
  
 
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   현재 유지 관리 계획 또는 로그 전달을 사용하는 데이터베이스에서는 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 을 설정하지 마세요. 다른 SQL Server 기능과의 상호 운용성 및 공존 성에 대 한 자세한 [내용은 Azure에 대 한 Managed Backup SQL Server을 참조 하세요. 상호 운용성 및 공존 성](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)  
  
###  <a name="Prerequisites"></a> 필수 구성 요소  
  
-   SQL Server 에이전트가 실행 중이어야 합니다.  
  
    > [!WARNING]  
    >  SQL Server 에이전트가 일정 기간 동안 중지되었다가 다시 시작되면 SQL 에이전트가 중지된 후부터 시작될 때까지 경과된 시간에 따라 백업 작업이 증가할 수 있으며 실행 대기 중인 로그 백업의 백로그가 있을 수 있습니다. 시작 시 SQL Server 에이전트가 자동으로 시작되도록 구성해 보세요.  
  
-   를 구성 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]하기 전에 저장소 계정에 인증 정보를 저장 하는 Azure STORAGE 계정 및 SQL 자격 증명을 모두 만들어야 합니다. 자세한 내용은 **URL에 대 한 SQL Server 백업** 항목의 [주요 구성 요소 및 개념 소개](../relational-databases/backup-restore/sql-server-backup-to-url.md#intorkeyconcepts) 섹션을 참조 하 [고, 2 단원: SQL Server 자격 증명](../../2014/tutorials/lesson-2-create-a-sql-server-credential.md)을 만듭니다.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]은 백업을 저장하는 데 필요한 컨테이너를 만듭니다. 컨테이너 이름은 ' machine name-instance name ' 형식을 사용 하 여 만들어집니다. AlwaysOn 가용성 그룹의 경우 컨테이너의 이름은 가용성 그룹의 GUID를 사용하여 지정됩니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 을 사용 하도록 설정 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]하는 저장 프로시저를 실행 하려면 **ALTER ANY CREDENTIAL** 권한이 있는 `EXECUTE` **db_backupoperator** 데이터베이스 역할의 `System Administrator` 또는 멤버와 sp_delete_에 대 한 권한이 있어야 합니다.  **backuphistory**및 `smart_admin.sp_backup_master_switch` 저장 프로시저  일반적으로 기존 설정을 검토하는 데 사용되는 저장 프로시저 및 함수는 저장 프로시저에 대한 `Execute` 권한과 함수에 대한 `Select` 권한이 각각 필요합니다.  
  

  
###  <a name="Considerations"></a>데이터베이스 및 인스턴스에 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 대 한 사용 시 고려 사항  
 개별 데이터베이스에 대해 별도로 또는 전체 인스턴스에 대해 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]을 설정할 수 있습니다. 선택 항목은 인스턴스의 데이터베이스에 대 한 복구 가능성 요구 사항, 여러 데이터베이스 및 인스턴스를 관리 하기 위한 요구 사항, Azure storage를 전략적으로 사용 하기 위한 요구 사항에 따라 달라 집니다.  
  
#### <a name="enabling-includess_smartbackupincludesss-smartbackup-mdmd-at-the-database-level"></a>데이터베이스 수준에서 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 설정  
 데이터베이스에 인스턴스의 다른 데이터베이스와 다른 백업 및 보존 기간에 대한 특정 요구 사항(복구 기능 SLA)이 있는 경우 이 데이터베이스에 대해 데이터베이스 수준에서 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 을 구성합니다. 데이터베이스 수준 설정은 인스턴스 수준 구성 설정보다 우선 적용됩니다. 그러나 이러한 두 옵션을 동일한 인스턴스에서 함께 사용할 수 있습니다. 다음은 데이터베이스 수준에서 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 을 설정할 때의 이점 및 고려 사항 목록입니다.  
  
-   세분성: 각 데이터베이스의 구성 설정을 분리합니다. 개별 데이터베이스에 대해 서로 다른 보존 기간을 지원할 수 있습니다.  
  
-   데이터베이스에 대해 인스턴스 수준 설정을 재정의합니다.  
  
-   백업할 개별 데이터베이스를 선택하여 스토리지 비용을 줄이는 데 사용될 수 있습니다.  
  
-   각 데이터베이스 관리를 필요로 합니다.  
  
#### <a name="enabling-includess_smartbackupincludesss-smartbackup-mdmd-at-the-instance-level-with-default-settings"></a>기본 설정을 사용하여 인스턴스 수준에서 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 설정  
 인스턴스에 있는 대부분의 데이터베이스에 대한 백업 및 보존 정책 요구 사항이 동일한 경우 또는 새 데이터베이스 인스턴스를 생성 시 자동으로 백업할 경우 이 설정을 사용합니다. 정책에 예외인 몇 개의 데이터베이스를 개별적으로 구성할 수 있습니다. 다음은 인스턴스 수준에서 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 을 설정할 때의 이점 및 고려 사항 목록입니다.  
  
-   인스턴스 수준의 Automation: 이후에 추가된 새 데이터베이스에 대해 자동으로 적용되는 공통 설정입니다.  
  
-   새 데이터베이스는 인스턴스에서 생성되자마자 자동으로 백업됩니다.  
  
-   보존 기간 요구 사항이 동일한 데이터베이스에 적용될 수 있습니다.  
  
-   [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 이 기본 설정을 사용하여 인스턴스 수준에서 설정된 경우에도 다른 보존 기간이 필요한 개별 데이터베이스를 구성할 수 있습니다. 백업을 위해 Azure storage [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 를 사용 하지 않으려는 경우에는 데이터베이스에 대해 사용 하지 않도록 설정할 수도 있습니다.  
  
##  <a name="DatabaseConfigure"></a>데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 설정 및 구성  
 시스템 저장 프로시저 `smart_admin.sp_set_db_backup`은 특정 데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]을 설정하는 데 사용됩니다. [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 이 데이터베이스에서 처음으로 설정될 때 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]을 설정하는 것 외에도 다음 정보를 지정해야 합니다.  
  
-   데이터베이스의 이름입니다.  
  
-   보존 기간  
  
-   Azure 저장소 계정에 인증 하는 데 사용 되는 SQL 자격 증명입니다.  
  
-   *@encryption_algorithm* **NO_ENCRYPTION** 를 사용 하 여  = 암호화 하지 않도록 지정 하거나 지원 되는 암호화 알고리즘을 지정 하십시오. 암호화에 대한 자세한 내용은 [Backup Encryption](../relational-databases/backup-restore/backup-encryption.md)를 참조하세요.  
  
 데이터베이스 수준 구성에 대한 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]은 Transact-SQL을 통해서만 지원됩니다.  
  
 데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 이 설정되면 이 정보가 유지됩니다. 구성을 변경하는 경우 데이터베이스 이름과 변경하려는 설정만 필요합니다. [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 은 지정되지 않은 경우 다른 매개 변수의 기존 값을 유지합니다.  
  
> [!IMPORTANT]  
>  데이터베이스에서 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 을 구성하기 전에 기존 구성(있는 경우)을 사용하는 것이 유용할 수 있습니다. 데이터베이스에 대한 구성 설정을 검토하는 단계는 이 섹션의 뒷부분에서 설명합니다.  
  
-   **Transact-sql 사용:**  
  
     을 처음으로 사용 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 하도록 설정 하는 경우 필수 매개 변수 *@database_name* 는, *@credential_name* , *@encryption_algorithm* , *@enable_backup* *@storage_url* 매개 변수는 선택 사항입니다. @storage_url 매개 변수에 대 한 값을 제공 하지 않으면 SQL 자격 증명의 저장소 계정 정보를 사용 하 여 값이 파생 됩니다. 스토리지 URL을 제공하는 경우 스토리지 계정의 루트에 대한 URL만 제공해야 하고 지정한 SQL 자격 증명의 정보와 일치시켜야 합니다.  
  
    1.  [!INCLUDE[ssDE](../includes/ssde-md.md)]에 연결합니다.  
  
    2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
    3.  다음 예를 복사 하 여 쿼리 창에 붙여 넣고를 `Execute`클릭 합니다. 이 예에서는 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] ' testdb ' 데이터베이스에 대해를 사용 하도록 설정 합니다. 보존 기간은 30일로 설정됩니다. 이 예제에서는 암호화 알고리즘 및 암호기 정보를 지정하여 암호화 옵션을 사용합니다.  
  
    ```  
    Use msdb;  
    GO  
    EXEC smart_admin.sp_set_db_backup   
                    @database_name='TestDB'   
                    ,@enable_backup=1  
                    ,@retention_days =30   
                    ,@credential_name ='MyCredential'  
                    ,@encryption_algorithm ='AES_256'  
                    ,@encryptor_type= 'Certificate'  
                    ,@encryptor_name='MyBackupCert'  
    GO  
  
    ```  
  
    > [!IMPORTANT]  
    >  보존 기간은 1일에서 30일 사이의 값으로 설정될 수 있습니다.  
    >   
    >  암호화용 인증서 만들기에 대한 자세한 내용은 [Create an Encrypted Backup](../relational-databases/backup-restore/create-an-encrypted-backup.md)의 백업 인증서 만들기 단계를 참조하세요.  
  
     이 저장 프로시저에 대 한 자세한 내용은 smart_admin을 참조 하십시오 [. set _db_backup &#40;transact-sql&#41; ](https://msdn.microsoft.com/library/dn451013(v=sql.120).aspx)  
  
     데이터베이스에 대한 구성 설정을 검토하려면 다음 쿼리를 사용합니다.  
  
    ```  
    Use msdb  
    GO  
    SELECT * FROM smart_admin.fn_backup_db_config('TestDB')  
    ```  
  
##  <a name="InstanceConfigure"></a>인스턴스에 대 한 기본 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 설정 사용 및 구성  
 인스턴스 수준에서 기본 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 설정을  시스템 저장 프로시저 `smart_admin.set_instance_backup` 또는 **SQL Server Management Studio**을 사용 합니다. 두 가지 방법이 아래에 설명되어 있습니다.  
  
 **smart_admin _instance_backup:를 설정**합니다. *@enable_backup* 매개 변수에 값 **1** 을 지정 하면 백업을 사용 하도록 설정 하 고 기본 구성을 설정할 수 있습니다. 이러한 기본 설정은 인스턴스 수준에서 적용되면 이 인스턴스에 추가된 모든 새 데이터베이스에 적용됩니다.  [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 이 처음으로 설정될 때 인스턴스에서 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 을 설정하는 것 외에도 다음 정보를 제공해야 합니다.  
  
-   보존 기간  
  
-   Azure 저장소 계정에 인증 하는 데 사용 되는 SQL 자격 증명입니다.  
  
-   암호화 옵션. *@encryption_algorithm* **NO_ENCRYPTION** 를 사용 하 여  = 암호화 하지 않도록 지정 하거나 지원 되는 암호화 알고리즘을 지정 하십시오. 암호화에 대한 자세한 내용은 [Backup Encryption](../relational-databases/backup-restore/backup-encryption.md)를 참조하세요.  
  
 이러한 설정은 설정되면 유지됩니다. 구성을 변경하는 경우 데이터베이스 이름과 변경하려는 설정만 필요합니다. [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]은 지정되지 않은 경우 기존 값을 유지합니다.  
  
> [!IMPORTANT]  
>  인스턴스에서 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 을 구성하기 전에 기존 구성(있는 경우)을 확인하는 것이 유용할 수 있습니다. 데이터베이스에 대한 구성 설정을 검토하는 단계는 이 섹션의 뒷부분에서 설명합니다.  
  
 **SQL Server Management Studio:** SQL Server Management Studio에서이 작업을 수행 하려면 개체 탐색기로 이동 하 여 **관리** 노드를 확장 하 고 **관리 되는 백업**을 마우스 오른쪽 단추로 클릭 합니다. **구성**을 선택합니다. **관리되는 백업** 대화 상자가 열립니다. 이 대화 상자를 사용하여 보존 기간, SQL 자격 증명, 스토리지 URL 및 암호화 설정을 지정할 수 있습니다. 이 대화 상자에 대 한 특정 도움말은 [관리 되 &#40;는&#41;백업 SQL Server Management Studio 구성](configure-managed-backup-sql-server-management-studio.md)을 참조 하세요.  
  
#### <a name="using-transact-sql"></a>Transact-SQL 사용  
  
1.  [!INCLUDE[ssDE](../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사 하 여 쿼리 창에 붙여 넣고를 `Execute`클릭 합니다.  
  
```  
Use msdb;  
Go  
   EXEC smart_admin.sp_set_instance_backup  
                @retention_days=30   
                ,@credential_name='sqlbackuptoURL'  
                ,@encryption_algorithm ='AES_128'  
                ,@encryptor_type= 'Certificate'  
                ,@encryptor_name='MyBackupCert'  
                ,@enable_backup=1;  
GO  
  
```  
  
> [!IMPORTANT]  
>  보존 기간은 1일에서 30일 사이의 값으로 설정될 수 있습니다.  
>   
>  암호화용 인증서 만들기에 대한 자세한 내용은 [Create an Encrypted Backup](../relational-databases/backup-restore/create-an-encrypted-backup.md)의 백업 인증서 만들기 단계를 참조하세요.  
  
 인스턴스에 대한 기본 구성 설정을 보려면 다음 쿼리를 사용합니다.  
  
```  
Use msdb;  
GO  
SELECT * FROM smart_admin.fn_backup_instance_config ();  
  
```  
  
#### <a name="using-powershell"></a>PowerShell 사용  
  
1.  PowerShell 인스턴스를 시작합니다.  
  
2.  다음 스크립트를 설정에 맞게 수정한 후 실행합니다.  
  
    ```  
    C:\ PS> cd SQLSERVER:\SQL\Computer\MyInstance   
    $encryptionOption = New-SqlBackupEncryptionOption -EncryptionAlgorithm Aes128 -EncryptorType ServerCertificate -EncryptorName "MyBackupCert"  
    Get-SqlSmartAdmin | Set-SqlSmartAdmin -BackupEnabled $True -BackupRetentionPeriodInDays 10 -EncryptionOption $encryptionOption  
    ```  
  
> [!IMPORTANT]  
>  기본 설정을 구성한 후 새 데이터베이스를 만들면 기본 설정으로 데이터베이스가 구성되는 데 최대 15분이 걸릴 수 있습니다. 이는 **Simple** 에서 **Full** 또는 **Bulk-Logged** 복구 모델로 변경되는 데이터베이스에도 적용됩니다.  
  
##  <a name="DatabaseDisable"></a> 데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 해제  
 `sp_set_db_backup` 시스템 저장 프로시저를 사용하여 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 설정을 해제할 수 있습니다. 는 *@enableparameter* 특정 데이터베이스에 대 한 구성을 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 활성화 하거나 비활성화 하는 데 사용 됩니다. 여기서 1은 구성 설정을 설정 하 고 0은 사용 하지 않도록 설정 합니다.  
  
#### <a name="to-disable-includess_smartbackupincludesss-smartbackup-mdmd-for-a-specific-database"></a>특정 데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 을 해제하려면  
  
1.  [!INCLUDE[ssDE](../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사 하 여 쿼리 창에 붙여 넣고를 `Execute`클릭 합니다.  
  
```  
Use msdb;  
Go  
EXEC smart_admin.sp_set_db_backup   
                @database_name='TestDB'   
                ,@enable_backup=0;  
GO  
  
```  
  
##  <a name="DatabaseAllDisable"></a> 인스턴스의 모든 데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 해제  
 다음 절차는 인스턴스에서 현재 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 이 설정되어 있는 모든 데이터베이스의 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 구성 설정을 해제하려는 경우에 해당됩니다.  스토리지 URL, 보존 및 SQL 자격 증명과 같은 구성 설정은 메타데이터에 남아 있으며 나중에 데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 이 설정되는 경우 다시 사용할 수 있습니다. 일시적으로 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 서비스를 일시 중지하는 경우 이 항목의 뒷부분에 나오는 다음 섹션에서 설명하는 마스터 스위치를 사용할 수 있습니다.  
  
#### <a name="to-disable-includess_smartbackupincludesss-smartbackup-mdmdfor-all-the-databases"></a>모든 데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]을 해제하려면  
  
1.  [!INCLUDE[ssDE](../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사 하 여 쿼리 창에 붙여 넣고를 `Execute`클릭 합니다. 다음 예에서는 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]이 인스턴스 수준에서 구성되어 있는지 여부와 인스턴스에서 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]이 설정된 모든 데이터베이스를 식별하고 시스템 저장 프로시저 `sp_set_db_backup`을 실행하여 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]을 해제합니다.  
  
```  
-- Create a working table to store the database names  
Declare @DBNames TABLE  
  
       (  
             RowID int IDENTITY PRIMARY KEY  
             ,DBName varchar(500)  
  
       )  
-- Define the variables  
DECLARE @rowid int  
DECLARE @dbname varchar(500)  
DECLARE @SQL varchar(2000)  
-- Get the database names from the system function  
  
INSERT INTO @DBNames (DBName)  
  
SELECT db_name  
       FROM   
  
       smart_admin.fn_backup_db_config (NULL)  
       WHERE is_smart_backup_enabled = 1  
  
       --Select DBName from @DBNames  
  
       select @rowid = min(RowID)  
       FROM @DBNames  
  
       WHILE @rowID IS NOT NULL  
       Begin  
  
             Set @dbname = (Select DBName From @DBNames Where RowID = @rowid)  
             Begin  
             Set @SQL = 'EXEC smart_admin.sp_set_db_backup    
                @database_name= '''+'' + @dbname+ ''+''',   
                @enable_backup=0'  
  
            EXECUTE (@SQL)  
  
             END  
             Select @rowid = min(RowID)  
             From @DBNames Where RowID > @rowid  
  
       END  
  
```  
  
 인스턴스의 모든 데이터베이스에 대한 구성 설정을 보려면 다음 쿼리를 사용합니다.  
  
```  
Use msdb;  
GO  
SELECT * FROM smart_admin.fn_backup_db_config (NULL);  
GO  
  
```  
  
##  <a name="InstanceDisable"></a> 인스턴스에 대해 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 기본 설정 해제  
 인스턴스 수준의 기본 설정은 해당 인스턴스에 대해 만든 모든 새 데이터베이스에 적용됩니다.  더 이상 기본 설정이 필요하지 않는 경우 **smart_admin.sp_set_instance_backup** 시스템 저장 프로시저를 사용하여 이 구성을 해제할 수 있습니다. 해제하는 경우 스토리지 URL, 보존 설정, SQL 자격 증명 이름 등의 다른 구성 설정이 제거되지 않습니다. 이러한 설정은 나중에 인스턴스에 대해 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 이 설정되면 사용됩니다.  
  
#### <a name="to-disable-includess_smartbackupincludesss-smartbackup-mdmd-default-configuration-settings"></a>[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 기본 구성 설정을 해제하려면  
  
1.  [!INCLUDE[ssDE](../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사 하 여 쿼리 창에 붙여 넣고를 `Execute`클릭 합니다.  
  
    ```  
    Use msdb;  
    Go  
    EXEC smart_admin.sp_set_instance_backup  
                    @enable_backup=0;  
    GO  
  
    ```  
  
#### <a name="using-powershell"></a>PowerShell 사용  
  
1.  PowerShell 인스턴스를 시작합니다.  
  
2.  다음 스크립트를 실행합니다.  
  
    ```  
    C:\ PS> cd SQLSERVER:\SQL\Computer\MyInstance   
    Set-SqlSmartAdmin -BackupEnabled $False  
    ```  
  
##  <a name="InstancePause"></a> 인스턴스 수준에서 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 일시 중지  
 짧은 시간 동안 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 서비스를 일시 중지해야 하는 경우가 있습니다.  `smart_admin.sp_backup_master_switch` 시스템 저장 프로시저를 사용하여 인스턴스 수준에서 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 서비스를 해제할 수 있습니다.  동일한 저장 프로시저를 사용하여 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]을 다시 시작할 수 있습니다. @state 매개 변수는 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]을 설정해야 할지 해제해야 할지를 정의하는 데 사용됩니다.  
  
#### <a name="to-pause-includess_smartbackupincludesss-smartbackup-mdmd-services-using-transact-sql"></a>Transact-SQL을 사용하여 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 서비스를 일시 중지하려면  
  
1.  [!INCLUDE[ssDE](../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사 하 여 쿼리 창에 붙여 넣은 후 다음을 클릭 합니다.`Execute`  
  
```  
Use msdb;  
GO  
EXEC smart_admin.sp_backup_master_switch @new_state=0;  
Go  
  
```  
  
#### <a name="to-pause-includess_smartbackupincludesss-smartbackup-mdmd-using-powershell"></a>PowerShell을 사용하여 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 을 일시 중지하려면  
  
1.  PowerShell 인스턴스를 시작합니다.  
  
2.  다음 스크립트를 설정에 맞게 수정한 후 실행합니다.  
  
    ```  
    C:\ PS> cd SQLSERVER:\SQL\Computer\MyInstance   
    Get-SqlSmartAdmin | Set-SqlSmartAdmin -MasterSwitch $False  
    ```  
  
#### <a name="to-resume-includess_smartbackupincludesss-smartbackup-mdmd-using-transact-sql"></a>Transact-SQL을 사용하여 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 을 다시 시작하려면  
  
1.  [!INCLUDE[ssDE](../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사 하 여 쿼리 창에 붙여 넣은 후를 `Execute`클릭 합니다.  
  
```  
Use msdb;  
Go  
EXEC smart_admin. sp_backup_master_switch @new_state=1;  
GO  
  
```  
  
#### <a name="to-resume-includess_smartbackupincludesss-smartbackup-mdmd-using-powershell"></a>PowerShell을 사용하여 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 을 다시 시작하려면  
  
1.  PowerShell 인스턴스를 시작합니다.  
  
2.  다음 스크립트를 설정에 맞게 수정한 후 실행합니다.  
  
    ```  
    C:\ PS> cd SQLSERVER:\SQL\Computer\MyInstance   
    Get-SqlSmartAdmin | Set-SqlSmartAdmin -MasterSwitch $True  
    ```  
  
  
