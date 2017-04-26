---
title: "EKM을 사용하여 SQL Server에서 TDE를 사용하도록 설정 | Microsoft 문서"
ms.custom: 
ms.date: 04/15/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- encryption [SQL Server], TDE using an EKM
- TDE, EKM how to
- EKM, TDE how to
- Transparent Data Encryption, using EKM
ms.assetid: b892e7a7-95bd-4903-bf54-55ce08e225af
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d8c98c5335ab148d1d36f56c1375ec1f89219908
ms.lasthandoff: 04/11/2017

---
# <a name="enable-tde-on-sql-server-using-ekm"></a>EKM을 사용하여 SQL Server에서 TDE를 사용하도록 설정
  이 항목에서는 EKM(확장 가능 키 관리) 모듈에 저장된 비대칭 키를 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 에 사용하여 데이터베이스 암호화 키를 보호하기 위해 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 TDE(투명한 데이터 암호화)를 사용하도록 설정하는 방법에 대해 설명합니다.  
  
 TDE는 데이터베이스 암호화 키라는 대칭 키를 사용하여 전체 데이터베이스의 저장소를 암호화합니다. 또한 master 데이터베이스의 데이터베이스 마스터 키로 보호되는 인증서를 사용하여 데이터베이스 암호화 키를 보호할 수도 있습니다. 데이터베이스 마스터 키를 사용하여 데이터베이스 암호화 키를 보호하는 방법은 [TDE&#40;투명한 데이터 암호화&#41;](../../../relational-databases/security/encryption/transparent-data-encryption-tde.md)를 참조하세요. Azure VM에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]이 실행 중인 경우 TDE 구성 방법은 [Azure 주요 자격 증명 모음을 사용한 확장 가능 키 관리&#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)를 참조하세요. Azure 주요 자격 증명 모음의 키를 사용하여 TDE를 구성하는 방법은 [SQL 암호화 기능을 통해 SQL Server 커넥터 사용](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)을 참조하세요. 

  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   데이터베이스 암호화 키를 만들고 데이터베이스를 암호화하려면 시스템 관리자와 같은 높은 권한이 필요합니다. 해당 사용자는 EKM 모듈로 인증될 수 있어야 합니다.  
  
-   [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 시작 시 데이터베이스를 열어야 합니다. 이를 위해서는 EKM에서 인증할 인증서를 만들고 비대칭 키를 기반으로 하는 로그인에 인증서를 추가해야 합니다. 사용자는 이 로그인을 사용하여 로그인할 수 없지만 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 은 이를 사용하여 EKM 장치에서 인증할 수 있습니다.  
  
-   EKM 모듈에 저장된 비대칭 키를 분실한 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 해당 데이터베이스를 열 수 없습니다. EKM 공급자가 비대칭 키를 백업할 수 있도록 허용하는 경우 백업을 만들고 안전한 위치에 저장해야 합니다.  
  
-   EKM 공급자에 필요한 옵션 및 매개 변수는 아래 코드 예에 제공된 것과 다를 수 있습니다. 자세한 내용은 해당 EKM 공급자를 참조하십시오.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 이 항목에서는 다음 권한이 사용됩니다.  
  
-   구성 옵션을 변경하고 RECONFIGURE 문을 실행하려면 ALTER SETTINGS 서버 수준 권한이 있어야 합니다. **sysadmin** 및 **serveradmin** 고정 서버 역할은 ALTER SETTINGS 권한을 암시적으로 보유하고 있습니다.  
  
-   ALTER ANY CREDENTIAL 권한이 필요합니다.  
  
-   ALTER ANY LOGIN 권한이 필요합니다.  
  
-   CREATE ASYMMETRIC KEY 권한이 필요합니다.  
  
-   데이터베이스를 암호화하려면 데이터베이스에 대한 CONTROL 권한이 필요합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-enable-tde-using-ekm"></a>EKM을 사용하여 TDE를 사용하도록 설정하려면  
  
1.  EKM 공급자가 제공하는 파일을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 컴퓨터의 적절한 위치에 복사합니다. 이 예에서는 **C:\EKM** 폴더를 사용합니다.  
  
2.  EKM 공급자의 요구 사항에 따라 컴퓨터에 인증서를 설치합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 는 EKM 공급자를 제공하지 않습니다. 각 EKM 공급자에 따라 사용자 설치, 구성 및 권한 부여에 대한 절차가 다릅니다.  이 단계를 수행하려면 해당 EKM 공급자 설명서를 참조하십시오.  
  
3.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
4.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
5.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- Enable advanced options.  
    sp_configure 'show advanced options', 1 ;  
    GO  
    RECONFIGURE ;  
    GO  
    -- Enable EKM provider  
    sp_configure 'EKM provider enabled', 1 ;  
    GO  
    RECONFIGURE ;  
    GO  
    -- Create a cryptographic provider, which we have chosen to call "EKM_Prov," based on an EKM provider  
  
    CREATE CRYPTOGRAPHIC PROVIDER EKM_Prov   
    FROM FILE = 'C:\EKM_Files\KeyProvFile.dll' ;  
    GO  
  
    -- Create a credential that will be used by system administrators.  
    CREATE CREDENTIAL sa_ekm_tde_cred   
    WITH IDENTITY = 'Identity1',   
    SECRET = 'q*gtev$0u#D1v'   
    FOR CRYPTOGRAPHIC PROVIDER EKM_Prov ;  
    GO  
  
    -- Add the credential to a high privileged user such as your   
    -- own domain login in the format [DOMAIN\login].  
    ALTER LOGIN Contoso\Mary  
    ADD CREDENTIAL sa_ekm_tde_cred ;  
    GO  
    -- create an asymmetric key stored inside the EKM provider  
    USE master ;  
    GO  
    CREATE ASYMMETRIC KEY ekm_login_key   
    FROM PROVIDER [EKM_Prov]  
    WITH ALGORITHM = RSA_512,  
    PROVIDER_KEY_NAME = 'SQL_Server_Key' ;  
    GO  
  
    -- Create a credential that will be used by the Database Engine.  
    CREATE CREDENTIAL ekm_tde_cred   
    WITH IDENTITY = 'Identity2'   
    , SECRET = 'jeksi84&sLksi01@s'   
    FOR CRYPTOGRAPHIC PROVIDER EKM_Prov ;  
  
    -- Add a login used by TDE, and add the new credential to the login.  
    CREATE LOGIN EKM_Login   
    FROM ASYMMETRIC KEY ekm_login_key ;  
    GO  
    ALTER LOGIN EKM_Login   
    ADD CREDENTIAL ekm_tde_cred ;  
    GO  
  
    -- Create the database encryption key that will be used for TDE.  
    USE AdventureWorks2012 ;  
    GO  
    CREATE DATABASE ENCRYPTION KEY  
    WITH ALGORITHM  = AES_128  
    ENCRYPTION BY SERVER ASYMMETRIC KEY ekm_login_key ;  
    GO  
  
    -- Alter the database to enable transparent data encryption.  
    ALTER DATABASE AdventureWorks2012   
    SET ENCRYPTION ON ;  
    GO  
    ```  
  
 자세한 내용은 다음 항목을 참조하세요.  
  
-   [sp_configure &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
-   [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-cryptographic-provider-transact-sql.md)  
  
-   [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)  
  
-   [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
  
-   [CREATE LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/create-login-transact-sql.md)  
  
-   [CREATE DATABASE ENCRYPTION KEY&#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-encryption-key-transact-sql.md)  
  
-   [ALTER LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-login-transact-sql.md)  
  
-   [ALTER DATABASE&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-transact-sql.md)  
  
## <a name="see-also"></a>참고 항목  
 [Azure SQL 데이터베이스를 사용한 투명한 데이터 암호화](../../../relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database.md)  
  
  

