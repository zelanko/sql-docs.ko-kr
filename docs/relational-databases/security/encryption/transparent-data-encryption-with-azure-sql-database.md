---
title: "Azure SQL Database를 사용한 투명한 데이터 암호화 | Microsoft 문서"
ms.custom:
- SQL2016_New_Updated
- MSDN content
- MSDN - SQL DB
ms.date: 09/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.service: sql-database
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- TDE, SQL Database
- encryption (SQL Database), TDE
- Transparent Data Encryption, SQL Database
ms.assetid: 0bf7e8ff-1416-4923-9c4c-49341e208c62
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1c607015f1ead5b19d4c32c5bac62eb624b0578b
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="transparent-data-encryption-with-azure-sql-database"></a>Azure SQL Database를 사용한 투명한 데이터 암호화
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx_md](../../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] 투명한 데이터 암호화를 사용하면 응용 프로그램을 변경할 필요 없이 사용하지 않는 데이터베이스, 연결된 백업 및 트랜잭션 로그 파일에 대한 실시간 암호화 및 암호 해독을 수행하여 악의적인 활동의 위협을 방지할 수 있습니다.  
  
 TDE는 데이터베이스 암호화 키라는 대칭 키를 사용하여 전체 데이터베이스의 저장소를 암호화합니다. [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] 에서 데이터베이스 암호화 키는 기본 제공 서버 인증서로 보호됩니다. 기본 제공 서버 인증서는 각 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] 서버에 대해 고유합니다. GeoDR 관계에 있는 데이터베이스는 각 서버에서 다른 키로 보호됩니다. 두 개의 데이터베이스가 동일한 서버에 연결된 경우에는 동일한 기본 제공 인증서를 공유합니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 는 적어도 90일마다 이러한 인증서를 자동으로 회전시킵니다. TDE에 대한 일반적인 설명은 [투명한 데이터 암호화&#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption-tde.md)를 참조하세요.  
  
 [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] 는 TDE와의 Azure 주요 자격 증명 모음 통합을 지원하지 않습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 주요 자격 증명 모음의 비대칭 키를 사용할 수 있습니다. 자세한 내용은 [Azure 주요 자격 증명 모음을 사용한 확장 가능 키 관리&#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)에서 암호화 키 계층 및 키 백업을 포함한 키 관리를 처리할 수 있습니다.  
  
##  <a name="Permissions"></a> 사용 권한  
 REST API나 PowerShell을 사용하여 Azure 포털을 통해 TDE를 구성하려면 Azure 소유자, 참가자 또는 SQL 보안 관리자로 연결되어 있어야 합니다.  
  
 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 을 사용하여 TDE를 구성하려면 다음 요구 사항이 충족되어야 합니다.  
  
-   SET 옵션을 사용하여 ALTER DATABASE 문을 실행하려면 **dbmanager** 역할에서 구성원 자격이 있어야 합니다.  
  
##  <a name="Preview"></a> 포털을 사용하여 데이터베이스에 대해 TDE를 사용하도록 설정  
  
1.  Azure 포털( [https://portal.azure.com](https://portal.azure.com) )에 방문하고 Azure 관리자 또는 참가자 계정으로 로그인합니다.  
  
2.  왼쪽 배너에서 **찾아보기**를 클릭한 다음 **SQL 데이터베이스**를 클릭합니다.  
  
3.  왼쪽 창에서 **SQL 데이터베이스** 를 선택한 상태로 사용자 데이터베이스를 클릭합니다.  
  
4.  데이터베이스 블레이드에서 **모든 설정**을 클릭합니다.  
  
5.  **설정** 블레이드에서 **투명한 데이터 암호화** 부분을 클릭하여 **투명한 데이터 암호화** 블레이드를 엽니다.  
  
6.  **데이터 암호화** 블레이드에서 **데이터 암호화** 단추를 **켜기**로 이동한 다음 페이지 맨 위의 **저장** 을 클릭하여 설정을 적용합니다. **암호화 상태** 는 투명한 데이터 암호화의 진행률과 비슷합니다.  
  
     ![SQL Database TDE 시작 암호화](../../../relational-databases/security/encryption/media/sqldb-tde-encrypt.png "SQL Database TDE Start Encryption")  
  
     [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] VIEW DATABASE STATE [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 권한이 있는 데이터베이스 사용자로 **와 같은 쿼리 도구를 사용하여** 에 연결하는 방법으로도 암호화 진행률을 모니터링할 수 있습니다. **sys.dm_database_encryption_keys** 뷰의 [encryption_state](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) 열을 쿼리합니다.  
  
##  <a name="Encrypt"></a> Transact-SQL을 사용하여 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] 에서 TDE 사용 설정  
 다음 단계를 수행하면 TDE가 사용하도록 설정됩니다.  
  
###  <a name="TsqlProcedure"></a>  
  
1.  관리자 또는 master 데이터베이스의 **dbmanager** 역할 구성원인 로그인을 사용하여 데이터베이스에 연결합니다.  
  
2.  다음 문을 실행하여 데이터베이스를 암호화합니다.  
  
    ```  
    -- Enable encryption  
    ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;  
    GO  
    ```  
  
3.  [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]에서 암호화 진행률을 모니터링하기 위해 **VIEW DATABASE STATE** 권한이 있는 데이터베이스 사용자가 **sys.dm_database_encryption_keys** 뷰의 [encryption_state](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) 열을 쿼리할 수 있습니다.  
  
##  <a name="EncryptPS"></a> PowerShell을 사용하여 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] 에 대해 TDE를 사용하거나 사용하지 않도록 설정  
 Azure PowerShell을 사용하면 다음 명령을 실행하여 TDE를 설정하거나 해제할 수 있습니다. 명령을 실행하기 전에 계정을 PS 창에 연결해야 합니다. `ServerName`, `ResourceGroupName`및 `DatabaseName` 매개 변수에 실제 값을 사용하도록 예제를 사용자 지정하세요. PowerShell에 대한 자세한 내용은 [Azure PowerShell을 설치 및 구성하는 방법](http://azure.microsoft.com/documentation/articles/powershell-install-configure/)을 참조하세요.  
  
> [!NOTE]  
>  계속 진행하려면 Auzre PowerShell 버전 1.0을 설치하고 구성해야 합니다. 버전 0.9.8을 사용할 수도 있지만 이 버전은 더 이상 사용되지 않으며, 이 버전을 사용하려면 `PS C:\> Switch-AzureMode -Name AzureResourceManager` 명령을 통해 AzureResourceManager cmdlet으로 전환해야 합니다.  
  
###  <a name="PSlProcedure"></a>  
  
1.  TDE를 사용하도록 설정하려면 TDE 상태를 반환하고 암호화 작업을 확인합니다.  
  
    ```  
    PS C:\> Set-AzureRMSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1" -State "Enabled"  
  
    PS C:\> Get-AzureRMSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1"  
  
    PS C:\> Get-AzureRMSqlDatabaseTransparentDataEncryptionActivity -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1"  
    ```  
  
     버전 0.9.8을 사용하는 경우에는 Set-AzureSqlDatabaseTransparentDataEncryption, Get-AzureSqlDatabaseTransparentDataEncryption 및 Get-AzureSqlDatabaseTransparentDataEncryptionActivity 명령을 사용합니다.  
  
2.  TDE를 사용하지 않도록 설정하려면 다음을 수행합니다.  
  
    ```  
    PS C:\> Set-AzureRMSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1" -State "Disabled"  
  
    ```  
  
     버전 0.9.8을 사용하는 경우에는 Set-AzureSqlDatabaseTransparentDataEncryption 명령을 사용합니다.  
  
##  <a name="Decrypt"></a> 다음에서 TDE로 보호되는 데이터베이스 암호 해독: [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]  
  
#### <a name="to-disable-tde-by-using-the-azure-portal"></a>Azure 포털을 사용하여 TDE를 사용하지 않도록 설정하려면  
  
1.  Azure 포털( [https://portal.azure.com](https://portal.azure.com) )에 방문하고 Azure 관리자 또는 참가자 계정으로 로그인합니다.  
  
2.  왼쪽 배너에서 **찾아보기**를 클릭한 다음 **SQL 데이터베이스**를 클릭합니다.  
  
3.  왼쪽 창에서 **SQL 데이터베이스** 를 선택한 상태로 사용자 데이터베이스를 클릭합니다.  
  
4.  데이터베이스 블레이드에서 **모든 설정**을 클릭합니다.  
  
5.  **설정** 블레이드에서 **투명한 데이터 암호화** 부분을 클릭하여 **투명한 데이터 암호화** 블레이드를 엽니다.  
  
6.  **투명한 데이터 암호화** 블레이드에서 **데이터 암호화** 단추를 **끄기**로 이동한 다음 페이지 맨 위의 **저장** 을 클릭하여 설정을 적용합니다. **암호화 상태** 는 투명한 데이터 암호 해독의 진행률과 비슷합니다.  
  
     [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] VIEW DATABASE STATE [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 권한이 있는 데이터베이스 사용자로 **와 같은 쿼리 도구를 사용하여** 에 연결하는 방법으로도 암호 해독의 진행률을 모니터링할 수 있습니다. **sys.dm_database_encryption_keys** 뷰의 [encryption_state](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) 열을 쿼리합니다.  
  
#### <a name="to-disable-tde-by-using-transact-sql"></a>Transact-SQL을 사용하여 TDE를 사용하지 않도록 설정하려면  
  
1.  관리자 또는 master 데이터베이스의 **dbmanager** 역할 구성원인 로그인을 사용하여 데이터베이스에 연결합니다.  
  
2.  다음 문을 실행하여 데이터베이스의 암호를 해독합니다.  
  
    ```  
    -- Enable encryption  
    ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;  
    GO  
    ```  
  
3.  [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]에서 암호화 진행률을 모니터링하기 위해 **VIEW DATABASE STATE** 권한이 있는 데이터베이스 사용자가 **sys.dm_database_encryption_keys** 뷰의 [encryption_state](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) 열을 쿼리할 수 있습니다.  
  
##  <a name="Working"></a> 다음에서 TDE로 보호되는 데이터베이스 이동: [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]  
 Azure 내에서의 작업을 위해 데이터베이스 암호를 해독할 필요는 없습니다. 원본 데이터베이스 또는 주 데이터베이스의 TDE 설정은 대상에서 투명하게 상속됩니다. 여기에는 다음과 관련된 작업이 포함됩니다.  
  
-   지리적 복원  
  
-   셀프 서비스 특정 시점 복원  
  
-   삭제된 데이터베이스 복원  
  
-   활성 지역 복제  
  
-   데이터베이스 복사본 만들기  
  
 [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] 포털 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사에서 데이터베이스 내보내기 함수를 사용하여 TDE로 보호되는 데이터베이스를 내보내는 경우 데이터베이스에서 내보낸 내용이 암호화되지 않습니다. 내보낸 이 콘텐츠는 암호화되지 않은.bacpac 파일에 저장됩니다. 새 데이터베이스 가져오기가 완료되면 .bacpac 파일을 적절하게 보호하고 TDE를 사용하도록 설정해야 합니다. 
 
 예를 들어 .bacpac 파일을 온-프레미스 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 내보낼 경우 새 데이터베이스의 가져온 콘텐츠는 자동으로 암호화되지 않습니다. 마찬가지로 [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] 에서 온-프레미스 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]로 .bacpac 파일을 내보낸 경우 새 데이터베이스도 자동으로 암호화되지 않습니다.  
 
 [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] 에서 내보내거나 대상으로 내보내는 경우 한 가지 예외 사항으로 TDE가 새 데이터베이스에서 사용하도록 설정되지만 .bacpac 파일 자체는 여전히 암호화되지 않습니다.
  
## <a name="related-sql-server-topic"></a>관련 SQL Server 항목  
 [EKM을 사용하여 SQL Server에서 TDE를 사용하도록 설정](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
## <a name="see-also"></a>참고 항목  
 [투명한 데이터 암호화&#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption-tde.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-transact-sql.md)  
  
  

