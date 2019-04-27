---
title: Azure SQL Database를 사용한 투명한 데이터 암호화 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- TDE, SQL Database
- Transparent Data Encryption, SQL Database
- encryption (SQL Database) TDE
ms.assetid: 0bf7e8ff-1416-4923-9c4c-49341e208c62
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 3551cf4db3ab1b84f04ba13dea414943fbb2ef44
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62773893"
---
# <a name="transparent-data-encryption-with-azure-sql-database"></a>Azure SQL 데이터베이스를 사용한 투명한 데이터 암호화
  [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] 투명한 데이터 암호화(미리 보기)는 응용 프로그램을 변경할 필요 없이 사용하지 않는 데이터베이스, 연결된 백업 및 트랜잭션 로그 파일에 대한 실시간 암호화 및 암호 해독을 수행하여 악의적인 활동의 위협으로부터 보호하도록 도와줍니다.  
  
 TDE는 데이터베이스 암호화 키라는 대칭 키를 사용하여 전체 데이터베이스의 스토리지를 암호화합니다. [!INCLUDE[ssSDS](../includes/sssds-md.md)] 에서 데이터베이스 암호화 키는 기본 제공 서버 인증서로 보호됩니다. 기본 제공 서버 인증서는 각 [!INCLUDE[ssSDS](../includes/sssds-md.md)] 서버에 대해 고유합니다. GeoDR 관계에 있는 데이터베이스는 각 서버에서 다른 키로 보호됩니다. 두 개의 데이터베이스가 동일한 서버에 연결된 경우에는 동일한 기본 제공 인증서를 공유합니다. [!INCLUDE[msCoName](../includes/msconame-md.md)] 는 적어도 90일마다 이러한 인증서를 자동으로 회전시킵니다. TDE에 대한 일반적인 설명은 [투명한 데이터 암호화&#40;TDE&#41;](../relational-databases/security/encryption/transparent-data-encryption.md)를 참조하세요.  
  
 [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] 는 TDE와의 Azure 주요 자격 증명 모음 통합을 지원하지 않습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 주요 자격 증명 모음의 비대칭 키를 사용할 수 있습니다. 자세한 내용은 참조 하세요. [예 1: Key Vault에서 비대칭 키를 사용 하 여 투명 한 데이터 암호화](../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md#ExampleA)합니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[sqldbesa](../includes/sqldbesa-md.md)] ([일부 지역에서는 미리 보기](http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)).|  
  
> [!IMPORTANT]  
>  현재 미리 보기 기능입니다. 내 데이터베이스에서의 [!INCLUDE[ssSDS](../includes/sssds-md.md)] 투명한 데이터 암호화 구현에는 사용권 계약의 미리 보기 약관(예: 기업계약, Microsoft Azure 계약 또는 Microsoft 온라인 정기가입 계약)과 해당 [Microsoft Azure Preview 추가 사용 약관](http://azure.microsoft.com/support/legal/preview-supplemental-terms/)이 적용됨을 확인하고 이에 동의합니다.  
  
 TDE 상태 미리보기는 [!INCLUDE[ssSDS](../includes/sssds-md.md)] 의 버전 제품군 V12가 현재 일반 가용성 상태에 있다고 알려진 지역의 하위 집합에도 적용됩니다. [!INCLUDE[ssSDS](../includes/sssds-md.md)] 에 대한 TDE는 [!INCLUDE[msCoName](../includes/msconame-md.md)] 이(가) TDE가 미리보기에서 GA로 승격되었음을 알릴 때까지 제품 데이터베이스에서 사용하기 위한 것이 아닙니다. [!INCLUDE[ssSDS](../includes/sssds-md.md)] V12에 대한 자세한 내용은 [Azure SQL 데이터베이스의 새로운 소식](http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/)을 참조합니다.  
  
##  <a name="Permissions"></a> Permissions  
 미리 보기에 등록하고 REST API나 PowerShell을 사용하여 Azure 포털을 통해 TDE를 구성하려면 Azure 소유자, 참가자 또는 SQL 보안 관리자로 연결되어 있어야 합니다.  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] 을 사용하여 TDE를 구성하려면 다음 요구 사항이 충족되어야 합니다.  
  
-   이미 TDE 미리 보기에 등록되어 있어야 합니다.  
  
-   데이터베이스 암호화 키를 만들려면 [!INCLUDE[ssSDS](../includes/sssds-md.md)] 관리자여야 하거나 master 데이터베이스의 **dbmanager** 역할 구성원이고 데이터베이스에 대한 **CONTROL** 권한이 있어야 합니다.  
  
-   SET 옵션을 사용하여 ALTER DATABASE 문을 실행하려면 **dbmanager** 역할에서 구성원 자격만 있으면 됩니다.  
  
##  <a name="Preview"></a> 데이터베이스에 대해 TDE를 사용 하도록 설정 TDE의 미리 보기 등록  
  
1.  Azure Portal을 방문 [ https://portal.azure.com ](https://portal.azure.com) 및 Azure 관리자 또는 참가자 계정으로 로그인 합니다.  
  
2.  왼쪽 배너에서 **찾아보기**를 클릭한 다음 **SQL 데이터베이스**를 클릭합니다.  
  
3.  왼쪽 창에서 **SQL 데이터베이스** 를 선택한 상태로 사용자 데이터베이스를 클릭합니다.  
  
4.  데이터베이스 블레이드에서 **모든 설정**을 클릭합니다.  
  
5.  **설정** 블레이드에서 **투명한 데이터 암호화(미리 보기)** 부분을 클릭하여 **투명한 데이터 암호화 미리 보기** 블레이드를 엽니다. TDE 미리 보기에 아직 등록하지 않은 경우 등록을 완료할 때까지 데이터 암호화가 사용되지 않도록 설정됩니다.  
  
6.  **미리 보기 조건**을 클릭합니다.  
  
7.  미리 보기 약관을 읽고 조건에 동의 하면 합니다 **투명 한 데이터 encryptionPreview 용어** 확인란을 선택한 다음 클릭 **확인** 페이지의 아래쪽 합니다. 반환 합니다 **데이터 encryptionPREVIEW** 블레이드에서 여기서 합니다 **데이터 암호화** 단추가 이제 활성화 되어야 합니다.  
  
8.  **데이터 암호화 미리 보기** 블레이드에서 **데이터 암호화** 단추를 **켬**으로 이동한 다음 페이지 위쪽의 **저장** 을 클릭하여 설정을 적용합니다. **암호화 상태** 는 투명한 데이터 암호화의 진행률과 비슷합니다.  
  
     ![SQLDB_TDE_TermsNewUI](../../2014/database-engine/media/sqldb-tde-termsnewui.png "SQLDB_TDE_TermsNewUI")  
  
     [!INCLUDE[ssSDS](../includes/sssds-md.md)] VIEW DATABASE STATE [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 권한이 있는 데이터베이스 사용자로 **와 같은 쿼리 도구를 사용하여** 에 연결하는 방법으로도 암호화 진행률을 모니터링할 수 있습니다. 쿼리는 `encryption_state` 의 열을 [sys.dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql) 보기.  
  
##  <a name="Encrypt"></a> Transact-SQL을 사용하여 [!INCLUDE[ssSDS](../includes/sssds-md.md)] 에서 TDE 사용 설정  
 다음 단계에서는 미리 보기에 이미 등록된 상태인 것으로 가정합니다.  
  
###  <a name="TsqlProcedure"></a>  
  
1.  관리자 또는 master 데이터베이스의 **dbmanager** 역할 구성원인 로그인을 사용하여 데이터베이스에 연결합니다.  
  
2.  다음 문을 실행하여 데이터베이스 암호화 키를 만들고 데이터베이스를 암호화합니다.  
  
    ```  
    -- Create the database encryption key that will be used for TDE.  
    CREATE DATABASE ENCRYPTION KEY   
    WITH ALGORITHM = AES_256   
    ENCRYPTION BY SERVER CERTIFICATE ##MS_TdeCertificate##;  
  
    -- Enable encryption  
    ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;  
    GO  
    ```  
  
3.  암호화 진행률을 모니터링 하기 위해 [!INCLUDE[ssSDS](../includes/sssds-md.md)], 데이터베이스 사용자가를 **VIEW DATABASE STATE** 권한을 쿼리할 수는 `encryption_state` 열의 [sys.dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql) 보기입니다.  
  
## <a name="enabling-tde-on-sql-database-by-using-powershell"></a>PowerShell을 사용하여 SQL Database에서 TDE 사용 설정  
 Azure PowerShell을 사용하면 다음 명령을 실행하여 TDE를 설정하거나 해제할 수 있습니다. 명령을 실행하기 전에 계정을 PS 창에 연결해야 합니다. 다음 단계에서는 미리 보기에 이미 등록된 상태인 것으로 가정합니다. PowerShell에 대한 자세한 내용은 [Azure PowerShell을 설치 및 구성하는 방법](http://azure.microsoft.com/documentation/articles/powershell-install-configure/)을 참조하세요.  
  
1.  TDE를 사용하도록 설정하려면 TDE 상태를 반환하고 암호화 작업을 봅니다.  
  
    ```  
    PS C:\> Switch-AzureMode -Name AzureResourceManager  
  
    PS C:\> Set-AzureSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1" -State "Enabled"  
  
    PS C:\> Get-AzureSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1"  
  
    PS C:\> Get-AzureSqlDatabaseTransparentDataEncryptionActivity -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1"  
  
    ```  
  
2.  TDE를 사용하지 않도록 설정하려면 다음을 수행합니다.  
  
    ```  
    PS C:\> Set-AzureSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1" -State "Disabled"  
  
    PS C:\> Switch-AzureMode -Name AzureServiceManagement  
    ```  
  
##  <a name="Decrypt"></a> 다음에서 TDE로 보호되는 데이터베이스 암호 해독: [!INCLUDE[ssSDS](../includes/sssds-md.md)]  
  
#### <a name="to-disable-tde-by-using-the-azure-portal"></a>Azure 포털을 사용하여 TDE를 사용하지 않도록 설정하려면  
  
1.  Azure Portal을 방문 [ https://portal.azure.com ](https://portal.azure.com) 및 Azure 관리자 또는 참가자 계정으로 로그인 합니다.  
  
2.  왼쪽 배너에서 **찾아보기**를 클릭한 다음 **SQL 데이터베이스**를 클릭합니다.  
  
3.  왼쪽 창에서 **SQL 데이터베이스** 를 선택한 상태로 사용자 데이터베이스를 클릭합니다.  
  
4.  데이터베이스 블레이드에서 **모든 설정**을 클릭합니다.  
  
5.  **설정** 블레이드에서 **투명한 데이터 암호화(미리 보기)** 부분을 클릭하여 **투명한 데이터 암호화 미리 보기** 블레이드를 엽니다.  
  
6.  **투명한 데이터 암호화 미리 보기** 블레이드에서 **데이터 암호화** 단추를 **끔**으로 이동한 다음 페이지 상단의 **저장** 을 클릭하여 설정을 적용합니다. **암호화 상태** 는 투명한 데이터 암호 해독의 진행률과 비슷합니다.  
  
     [!INCLUDE[ssSDS](../includes/sssds-md.md)] VIEW DATABASE STATE [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 권한이 있는 데이터베이스 사용자로 **와 같은 쿼리 도구를 사용하여** 에 연결하는 방법으로도 암호 해독의 진행률을 모니터링할 수 있습니다. 쿼리는 `encryption_state` 의 열을 [sys.dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql)보기.  
  
#### <a name="to-disable-tde-by-using-transact-sql"></a>Transact-SQL을 사용하여 TDE를 사용하지 않도록 설정하려면  
  
1.  관리자 또는 master 데이터베이스의 **dbmanager** 역할 구성원인 로그인을 사용하여 데이터베이스에 연결합니다.  
  
2.  다음 문을 실행하여 데이터베이스의 암호를 해독합니다.  
  
    ```  
    -- Enable encryption  
    ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;  
    GO  
    ```  
  
3.  암호화 진행률을 모니터링 하기 위해 [!INCLUDE[ssSDS](../includes/sssds-md.md)], 데이터베이스 사용자가를 **VIEW DATABASE STATE** 권한을 쿼리할 수는 `encryption_state` 열의 [sys.dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql) 보기입니다.  
  
##  <a name="Working"></a> TDE 사용 하 여 작업에서 데이터베이스 보호 [!INCLUDE[ssSDS](../includes/sssds-md.md)]  
 Azure 내에서의 작업을 위해 데이터베이스 암호를 해독할 필요는 없습니다. 원본 데이터베이스 또는 주 데이터베이스의 TDE 설정은 대상에서 투명하게 상속됩니다. 여기에는 다음과 관련된 작업이 포함됩니다.  
  
-   지리적 복원  
  
-   셀프 서비스 특정 시점 복원  
  
-   삭제된 데이터베이스 복원  
  
-   활성 지역 복제  
  
-   데이터베이스 복사본 만들기  
  
##  <a name="Moving"></a> 사용 하 여 TDE 보호 데이터베이스를 이동 합니다. Bacpac 파일  
 [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] 포털 또는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사에서 데이터베이스 내보내기 함수를 사용하여 TDE로 보호되는 데이터베이스를 내보내는 경우 데이터베이스의 내용이 암호화되지 않습니다. 암호화되지 않은.bacpac 파일에 내용이 저장됩니다.  새 데이터베이스 가져오기가 완료되면 .bacpac 파일을 적절하게 보호하고 TDE를 사용하도록 설정해야 합니다.  
  
## <a name="related-sql-server-topic"></a>관련 SQL Server 항목  
 [EKM을 사용하여 TDE 설정](../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
## <a name="see-also"></a>관련 항목  
 [투명한 데이터 암호화&#40;TDE&#41;](../relational-databases/security/encryption/transparent-data-encryption.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)   
 [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-database-encryption-key-transact-sql)   
 [ALTER DATABASE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)  
  
  
