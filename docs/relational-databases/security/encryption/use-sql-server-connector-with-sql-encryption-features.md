---
title: Azure Key Vault와 함께 SQL Server 커넥터 암호화 사용
description: Azure Key Vault를 사용하는 TDE, 백업 암호화, 열 수준 암호화 등의 일반적인 암호화 기능과 함께 SQL Server 커넥터를 사용하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 09/12/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Connector, using
- EKM, with SQL Server Connector
ms.assetid: 58fc869e-00f1-4d7c-a49b-c0136c9add89
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: 0fc954228aff75940e66f976f19d1414118e1a8e
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558518"
---
# <a name="use-sql-server-connector-with-sql-encryption-features"></a>SQL 암호화 기능을 통해 SQL Server 커넥터 사용
[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Azure 주요 자격 증명 모음으로 보호되는 비대칭 키를 사용하는 일반적인 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 암호화 작업에는 다음 세 가지 영역이 포함됩니다.  
  
-   Azure 주요 자격 증명 모음에서 비대칭 키를 사용한 투명한 데이터 암호화  
  
-   키 자격 증명 모음에서 비대칭 키를 사용한 백업 암호화  
  
-   키 자격 증명 모음에서 비대칭 키를 사용한 열 수준 암호화  
  
 이 항목의 단계를 수행하기 전에 [Azure 주요 자격 증명 모음을 사용한 확장 가능 키 관리 설정 단계](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)항목의 1 ~ 4부를 완료합니다.  
 
> [!NOTE]  
>  1\.0.0.440 및 이전 버전은 대체되었으며 프로덕션 환경에서 더 이상 지원되지 않습니다. [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=45344)를 방문하고 "SQL Server 커넥터 업그레이드" 아래의 [SQL Server 커넥터 유지 관리 및 문제 해결](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md) 페이지에 있는 지침을 사용하여 1.0.1.0 이상 버전으로 업그레이드하세요.  
  
## <a name="transparent-data-encryption-by-using-an-asymmetric-key-from-azure-key-vault"></a>Azure 주요 자격 증명 모음에서 비대칭 키를 사용한 투명한 데이터 암호화

Azure 주요 자격 증명 모음을 사용한 확장 가능 키 관리 설정 단계 항목의 1~4부를 완료한 후, Azure 주요 자격 증명 모음 키를 사용하여 TDE를 사용하는 데이터베이스 암호화 키를 암호화합니다. Powershell을 사용하여 키를 순환하는 방법에 대한 자세한 내용은 [PowerShell을 사용하여 TDE(투명한 데이터 암호화) 보호기 순환](/azure/sql-database/transparent-data-encryption-byok-azure-sql-key-rotation)을 참조하세요.
 
자격 증명 및 로그인을 만들고 데이터베이스의 데이터 및 로그를 암호화할 데이터베이스 암호화 키를 만듭니다. 데이터베이스를 암호화하려면 데이터베이스에 대한 **CONTROL** 권한이 필요합니다. 다음 그래픽에서는 Azure 주요 자격 증명 모음을 사용하는 경우 암호화 키의 계층 구조를 보여 줍니다.  
  
 ![ekm&#45;key&#45;hierarchy&#45;with&#45;akv](../../../relational-databases/security/encryption/media/ekm-key-hierarchy-with-akv.png "ekm-key-hierarchy-with-akv")  
  
1.  **TDE에 사용할 데이터베이스 엔진의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 자격 증명 만들기**  
  
     데이터베이스 엔진은 데이터베이스 로드 중에 자격 증명을 사용하여 주요 자격 증명 모음에 액세스합니다. 부여되는 주요 자격 증명 모음 사용 권한을 제한하려면, **의 경우 1부에서 다른 Azure Active Directory** 클라이언트 ID **및** 암호 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]를 만드는 것이 좋습니다.  
  
     다음과 같이 아래 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 스크립트를 수정합니다.  
  
    -   Azure Key Vault를 가리키도록 `IDENTITY` 인수(`ContosoDevKeyVault`)를 편집합니다.
        - **전역 Azure**를 사용하는 경우 `IDENTITY` 인수를 파트 2의 Azure Key Vault 이름으로 바꿉니다.
        - **프라이빗 Azure 클라우드** (예: Azure Government, Azure 중국 21Vianet 또는 Azure 독일)를 사용하는 경우 `IDENTITY` 인수를 파트 2, 3단계에서 반환된 자격 증명 모음 URI로 바꿉니다. 자격 증명 모음 URI에 "https://"를 포함하지 마세요.   
  
    -   `SECRET` 인수의 첫 번째 부분을 1부의 Azure Active Directory **클라이언트 ID** 로 바꿉니다. 이 예제에서 **클라이언트 ID** 는 `EF5C8E094D2A4A769998D93440D8115D`입니다.  
  
        > [!IMPORTANT]  
        >  **클라이언트 ID**에서 하이픈을 제거해야 합니다.  
  
    -   `SECRET` 인수의 두 번째 부분을 파트 1의 **클라이언트 암호** 를 사용하여 완성합니다. 이 예제에서 파트 1의 **클라이언트 암호** 는 `Replace-With-AAD-Client-Secret`입니다. `SECRET` 인수의 최종 문자열은 *하이픈 없는*문자 및 숫자의 긴 시퀀스가 됩니다.  
  
    ```sql  
    USE master;  
    CREATE CREDENTIAL Azure_EKM_TDE_cred   
        WITH IDENTITY = 'ContosoDevKeyVault', -- for global Azure
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.usgovcloudapi.net', -- for Azure Government
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.azure.cn', -- for Azure China 21Vianet
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.microsoftazure.de', -- for Azure Germany   
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DReplace-With-AAD-Client-Secret'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;  
    ```  
  
2.  **TDE의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에 대한 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 로그인 만들기**  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인을 만들고 1단계의 자격 증명을 여기에 추가합니다. 이 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 예제에서는 앞에서 가져온 것과 동일한 키를 사용합니다.  
  
    ```sql  
    USE master;  
    -- Create a SQL Server login associated with the asymmetric key   
    -- for the Database engine to use when it loads a database   
    -- encrypted by TDE.  
    CREATE LOGIN TDE_Login   
    FROM ASYMMETRIC KEY CONTOSO_KEY;  
    GO   
  
    -- Alter the TDE Login to add the credential for use by the   
    -- Database Engine to access the key vault  
    ALTER LOGIN TDE_Login   
    ADD CREDENTIAL Azure_EKM_TDE_cred ;  
    GO  
    ```  
  
3.  **DEK(데이터베이스 암호화 키) 만들기**  
  
     DEK은 데이터베이스 인스턴스의 데이터 및 로그 파일을 암호화하고, Azure 주요 자격 증명 모음 비대칭 키로 암호화될 수 있습니다. DEK는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서 지원되는 알고리즘 또는 키 길이를 사용하여 만들 수 있습니다.  
  
    ```sql  
    USE ContosoDatabase;  
    GO  
  
    CREATE DATABASE ENCRYPTION KEY   
    WITH ALGORITHM = AES_256   
    ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;  
    GO  
    ```  
  
4.  **TDE 설정**  
  
    ```sql  
    -- Alter the database to enable transparent data encryption.  
    ALTER DATABASE ContosoDatabase   
    SET ENCRYPTION ON;  
    GO  
    ```  
  
     [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]을(를) 사용하여, 개체 탐색기에서 데이터베이스에 연결하여 TDE가 켜져 있는지 확인합니다. 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**가리킨 다음 **데이터베이스 암호화 관리**를 클릭합니다.  
  
     ![ekm&#45;tde&#45;object&#45;explorer](../../../relational-databases/security/encryption/media/ekm-tde-object-explorer.png "ekm-tde-object-explorer")  
  
     **데이터베이스 암호화 관리** 대화 상자에서 TDE가 켜져 있고 DEK를 암호화하는 비대칭 키가 무엇인지 확인합니다.  
  
     ![ekm&#45;tde&#45;dialog&#45;box](../../../relational-databases/security/encryption/media/ekm-tde-dialog-box.png "ekm-tde-dialog-box")  
  
     또는 다음 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 스크립트를 실행할 수 있습니다. 암호화 상태 3은 암호화된 데이터베이스를 나타냅니다.  
  
    ```sql  
    USE MASTER  
    SELECT * FROM sys.asymmetric_keys  
  
    -- Check which databases are encrypted using TDE  
    SELECT d.name, dek.encryption_state   
    FROM sys.dm_database_encryption_keys AS dek  
    JOIN sys.databases AS d  
         ON dek.database_id = d.database_id;  
    ```  
  
    > [!NOTE]  
    >  `tempdb` 데이터베이스는 데이터베이스에서 TDE를 사용할 때마다 자동으로 암호화됩니다.  
  
## <a name="encrypting-backups-by-using-an-asymmetric-key-from-the-key-vault"></a>키 자격 증명 모음에서 비대칭 키를 사용한 백업 암호화  
 암호화된 백업은 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]부터 지원됩니다. 다음 예제에서는 키 자격 증명 모음에서 비대칭 키로 보호되는 데이터 암호화 키로 암호화된 백업을 만들고 복원합니다.  
[!INCLUDE[ssDE](../../../includes/ssde-md.md)] 은(는) 데이터베이스 로드 중 주요 자격 증명 모음에 액세스할 때 자격 증명이 필요합니다. 부여되는 주요 자격 증명 모음 사용 권한을 제한하려면, 데이터베이스 엔진의 경우 1부에서 다른 Azure Active Directory 클라이언트 ID 및 암호를 만드는 것이 좋습니다.  
  
1.  **백업 암호화에 사용할 데이터베이스 엔진의 SQL Server 자격 증명 만들기**  
  
     다음과 같이 아래 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 스크립트를 수정합니다.  
  
    -   Azure Key Vault를 가리키도록 `IDENTITY` 인수(`ContosoDevKeyVault`)를 편집합니다.
        - **전역 Azure**를 사용하는 경우 `IDENTITY` 인수를 파트 2의 Azure Key Vault 이름으로 바꿉니다.
        - **프라이빗 Azure 클라우드** (예: Azure Government, Azure 중국 21Vianet 또는 Azure 독일)를 사용하는 경우 `IDENTITY` 인수를 파트 2, 3단계에서 반환된 자격 증명 모음 URI로 바꿉니다. 자격 증명 모음 URI에 "https://"를 포함하지 마세요.    
  
    -   `SECRET` 인수의 첫 번째 부분을 1부의 Azure Active Directory **클라이언트 ID** 로 바꿉니다. 이 예제에서 **클라이언트 ID** 는 `EF5C8E094D2A4A769998D93440D8115D`입니다.  
  
        > [!IMPORTANT]  
        >  **클라이언트 ID**에서 하이픈을 제거해야 합니다.  
  
    -   `SECRET` 인수의 두 번째 부분을 파트 1의 **클라이언트 암호** 를 사용하여 완성합니다. 이 예제에서 파트 1의 **클라이언트 암호** 는 `Replace-With-AAD-Client-Secret`입니다. `SECRET` 인수의 최종 문자열은 *하이픈 없는*문자 및 숫자의 긴 시퀀스가 됩니다.   
  
        ```sql  
        USE master;  
  
        CREATE CREDENTIAL Azure_EKM_Backup_cred   
            WITH IDENTITY = 'ContosoDevKeyVault', -- for global Azure
            -- WITH IDENTITY = 'ContosoDevKeyVault.vault.usgovcloudapi.net', -- for Azure Government
            -- WITH IDENTITY = 'ContosoDevKeyVault.vault.azure.cn', -- for Azure China 21Vianet
            -- WITH IDENTITY = 'ContosoDevKeyVault.vault.microsoftazure.de', -- for Azure Germany   
            SECRET = 'EF5C8E094D2A4A769998D93440D8115DReplace-With-AAD-Client-Secret'   
        FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;    
        ```  
  
2.  **백업 암호화의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에 대해 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 로그인 만들기**  
  
     암호화 백업에 대해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서 사용할 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]로그인을 만들고 1단계의 자격 증명을 여기에 추가합니다. 이 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 예제에서는 앞에서 가져온 것과 동일한 키를 사용합니다.  
  
    > [!IMPORTANT]  
    >  이미 TDE(위 예제) 또는 열 수준 암호화(아래 예제)에 해당 키를 사용한 경우 백업 암호화에 대해 동일한 비대칭 키를 사용할 수 없습니다.  
  
     이 예제에서는 앞의 5단계 4부에서 master 데이터베이스용으로 미리 가져오거나 만들 수 있는 주요 자격 증명 모음에 저장된 `CONTOSO_KEY_BACKUP` 비대칭 키를 사용합니다.  
  
    ```sql  
    USE master;  
  
    -- Create a SQL Server login associated with the asymmetric key   
    -- for the Database engine to use when it is encrypting the backup.  
    CREATE LOGIN Backup_Login   
    FROM ASYMMETRIC KEY CONTOSO_KEY_BACKUP;  
    GO   
  
    -- Alter the Encrypted Backup Login to add the credential for use by   
    -- the Database Engine to access the key vault  
    ALTER LOGIN Backup_Login   
    ADD CREDENTIAL Azure_EKM_Backup_cred ;  
    GO  
    ```  
  
3.  **데이터베이스 백업**  
  
     Key Vault에 저장된 비대칭 키를 사용하여 암호화를 지정하는 데이터베이스를 백업합니다.
     
     아래 예제에서 데이터베이스가 이미 TDE로 암호화되어 있고 비대칭 키 `CONTOSO_KEY_BACKUP`이 TDE 비대칭 키와 다른 경우 백업은 TDE 비대칭 키 및 `CONTOSO_KEY_BACKUP` 모두를 사용하여 암호화됩니다. 대상 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에서 백업 암호를 해독하려면 두 키가 모두 필요합니다.
  
    ```sql  
    USE master;  
  
    BACKUP DATABASE [DATABASE_TO_BACKUP]  
    TO DISK = N'[PATH TO BACKUP FILE]'   
    WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,   
    ENCRYPTION(ALGORITHM = AES_256,   
    SERVER ASYMMETRIC KEY = [CONTOSO_KEY_BACKUP]);  
    GO  
    ```  
  
4.  **데이터베이스 복원**  
    
    TDE로 암호화된 데이터베이스 백업을 복원하려면 먼저 대상 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 암호화에 사용된 비대칭 Key Vault 키의 사본이 있어야 합니다. 이 작업을 수행하는 방법은 다음과 같습니다.  
    
    - TDE에 사용된 원래 비대칭 키가 더 이상 Key Vault에 없는 경우 Key Vault 키 백업을 복원하거나 로컬 HSM에서 키를 다시 가져옵니다. **중요:** 키 지문이 데이터베이스 백업에 기록된 지문과 일치하도록 하려면 키의 원래 이름이 **동일한 Key Vault 키 이름**과 동일해야 합니다.
    
    - 대상 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 1단계와 2단계를 적용합니다.
    
    - 대상 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 백업을 암호화하는 데 사용된 비대칭 키에 액세스한 다음 서버에서 데이터베이스를 복원합니다.
    
     샘플 복원 코드:  
  
    ```sql  
    RESTORE DATABASE [DATABASE_TO_BACKUP]  
    FROM DISK = N'[PATH TO BACKUP FILE]'   
        WITH FILE = 1, NOUNLOAD, REPLACE;  
    GO  
    ```  
  
     백업 옵션에 대한 자세한 내용은 [BACKUP(Transact-SQL)](../../../t-sql/statements/backup-transact-sql.md)을 참조하세요.  
  
## <a name="column-level-encryption-by-using-an-asymmetric-key-from-the-key-vault"></a>키 자격 증명 모음에서 비대칭 키를 사용한 열 수준 암호화  
 다음 예제에서는 키 자격 증명 모음에 비대칭 키로 보호되는 대칭 키를 만듭니다. 그런 다음 데이터베이스에서 대칭 키를 사용하여 데이터를 암호화합니다.  
  
> [!IMPORTANT]  
>  이미 TDE 또는 백업 암호화(이전 예제)에 해당 키를 사용한 경우 백업 암호화에 대해 동일한 비대칭 키를 사용할 수 없습니다.  
  
 이 예제에서는 `CONTOSO_KEY_COLUMNS` Azure 주요 자격 증명 모음을 사용한 확장 가능 키 관리 설정 단계 [의 섹션 3, 3단계에 설명된 대로 미리 가져오거나 만들 수 있는 주요 자격 증명 모음에 저장된](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)비대칭 키를 사용합니다. `ContosoDatabase` 데이터베이스에서 이 비대칭 키를 사용하려면 다시 `CREATE ASYMMETRIC KEY` 문을 실행하여 `ContosoDatabase` 데이터베이스에 키에 대한 참조를 제공해야 합니다.  
  
```sql  
USE [ContosoDatabase];  
GO  
  
-- Create a reference to the key in the key vault  
CREATE ASYMMETRIC KEY CONTOSO_KEY_COLUMNS   
FROM PROVIDER [AzureKeyVault_EKM_Prov]  
WITH PROVIDER_KEY_NAME = 'ContosoDevRSAKey2',  
CREATION_DISPOSITION = OPEN_EXISTING;  
  
-- Create the data encryption key.  
-- The data encryption key can be created using any SQL Server   
-- supported algorithm or key length.  
-- The DEK will be protected by the asymmetric key in the key vault  
  
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY  
    WITH ALGORITHM=AES_256  
    ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY_COLUMNS;  
  
DECLARE @DATA VARBINARY(MAX);  
  
--Open the symmetric key for use in this session  
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY   
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY_COLUMNS;  
  
--Encrypt syntax  
SELECT @DATA = ENCRYPTBYKEY  
    (  
    KEY_GUID('DATA_ENCRYPTION_KEY'),   
    CONVERT(VARBINARY,'Plain text data to encrypt')  
    );  
  
-- Decrypt syntax  
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));  
  
--Close the symmetric key  
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;  
```  
  
## <a name="see-also"></a>참고 항목  
 [Azure 주요 자격 증명 모음을 사용한 확장 가능 키 관리 설정 단계](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)   
 [Azure Key Vault를 사용한 확장 가능 키 관리](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
 [EKM provider enabled 서버 구성 옵션](../../../database-engine/configure-windows/ekm-provider-enabled-server-configuration-option.md)   
 [SQL Server 커넥터 유지 관리 및 문제 해결](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)  
  
  
