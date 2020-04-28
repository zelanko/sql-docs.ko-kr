---
title: Azure Key Vault를 사용한 확장 가능 키 관리(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- EKM, with key vault
- TDE, EKM and key vault
- Extensible Key Management with key vault
- Key Management with key vault
- Transparent Data Encryption, using EKM and key vault
ms.assetid: 3efdc48a-8064-4ea6-a828-3fbf758ef97c
author: jaszymas
ms.author: jaszymas
manager: craigg
ms.openlocfilehash: f826ce7ff54bb28738f79fbf22c8c8435035008c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "79289451"
---
# <a name="extensible-key-management-using-azure-key-vault-sql-server"></a>Azure 키 자격 증명 모음(SQL Server)을 사용한 확장 가능 키 관리
  Azure Key Vault [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 용 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 커넥터를 사용 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 하 여 암호화를 사용 하면 암호화 키를 보호 하기 위해 [EKM&#41;공급자로 확장 가능 키 관리 &#40;](extensible-key-management-ekm.md) Azure Key Vault 서비스를 활용할 수 있습니다.

 이 항목의 내용:

-   [EKM 사용](#Uses)

-   [1단계: SQL Server에서 사용할 수 있도록 키 자격 증명 모음 설정](#Step1)

-   [2단계: SQL Server 커넥터 설치](#Step2)

-   [3단계: 키 자격 증명 모음에 EKM 공급자를 사용하도록 SQL Server 구성](#Step3)

-   [예 1: 키 자격 증명 모음에서 비대칭 키를 사용한 투명한 데이터 암호화](#ExampleA)

-   [예 2: 키 자격 증명 모음에서 비대칭 키를 사용한 백업 암호화](#ExampleB)

-   [예 3: 키 자격 증명 모음에서 비대칭 키를 사용한 열 수준 암호화](#ExampleC)

##  <a name="uses-of-ekm"></a><a name="Uses"></a>EKM 사용
 조직에서 중요한 데이터를 보호하기 위해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 암호화를 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]암호화에는 [투명한 데이터 암호화 &#40;TDE&#41;](transparent-data-encryption.md), CLE ( [열 수준 암호화](/sql/t-sql/functions/cryptographic-functions-transact-sql) ) 및 [백업 암호화](../../backup-restore/backup-encryption.md)가 포함 됩니다. 이 암호화들에서는 모두 데이터가 대칭 데이터 암호화 키를 사용하여 암호화되고, 이 대칭 데이터 암호화 키는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 저장된 키의 계층 구조로 암호화하여 추가적으로 보호하게 됩니다. 이렇게 하는 대신, EKM 공급자 아키텍처를 사용하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 외부 암호화 공급자에 있는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 외부에 저장된 비대칭 키를 사용하여 데이터 암호화 키를 보호합니다. EKM 공급자 아키텍처를 사용하면 추가적인 보안 계층이 생기고 조직은 키와 데이터의 관리를 분리할 수 있습니다.

 Azure Key Vault용 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터를 사용하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 확장성과 성능이 뛰어난 고가용성 Key Vault 서비스를 암호화 키 보호를 위한 EKM 공급자로 활용합니다. 키 자격 증명 모음 서비스는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Azure 가상 컴퓨터의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 설치와 함께 온-프레미스 서버용으로 사용할 수 있습니다. 키 자격 증명 모음 서비스에서는 더 높은 수준의 비대칭 암호화 키 보호를 위해 세부적인 제어 및 모니터링이 이루어지는 HSM(하드웨어 보안 모듈)을 사용할 수도 있습니다. Key Vault에 대한 자세한 내용은 [Azure Key Vault](https://go.microsoft.com/fwlink/?LinkId=521401)를 참조하세요.

 다음 이미지에 키 자격 증명 모음을 사용한 EKM의 프로세스 흐름이 요약되어 있습니다. 이미지의 프로세스 단계 번호는 이미지에서 설명하는 설정 단계 번호와 일치하지 않습니다.

 ![Azure Key Vault를 사용하는 SQL Server EKM](../../../database-engine/media/ekm-using-azure-key-vault.png "Azure Key Vault를 사용하는 SQL Server EKM")

##  <a name="step-1-set-up-the-key-vault-for-use-by-sql-server"></a><a name="Step1"></a>1 단계:에서 사용할 Key Vault 설정 SQL Server
 다음 단계를 사용하여 암호화 키 보호를 위해 [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)] 에 사용할 자격 증명 모음 키를 설정하세요. 자격 증명 모음은 이미 조직에 사용 중일 수 있습니다. 자격 증명 모음이 존재하지 않으면 암호화 키를 관리하도록 지정된 조직 내 Azure 관리자가 자격 증명 모음을 만들고, 이 자격 증명 모음에서 비대칭 키를 생성한 다음 키를 사용할 수 있는 권한을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에 부여합니다. Vault 서비스에 대해 이해하려면 [Azure Key Vault 시작](https://go.microsoft.com/fwlink/?LinkId=521402)(영문), 및 PowerShell [Azure Key Vault Cmdlet](https://docs.microsoft.com/powershell/module/azurerm.keyvault)(영문) 참조를 검토하세요.

> [!IMPORTANT]
>  여러 Azure 구독이 있는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]가 포함된 구독을 사용해야 합니다.

1.  **Vault 만들기:**[Azure Key Vault 시작](https://go.microsoft.com/fwlink/?LinkId=521402)의 **Key Vault 만들기** 섹션에 있는 지침을 사용하여 Vault를 만듭니다. 자격 증명 모음의 이름은 기록합니다. 이 항목에서는 **ContosoKeyVault** 를 키 자격 증명 모음 이름으로 사용합니다.

2.  **자격 증명 모음에서 비대칭 키 생성:** 키 자격 증명 모음에 있는 비대칭 키는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 암호화 키를 보호하는 데 사용됩니다. 비대칭 키의 퍼블릭 부분만 자격 증명 모음을 떠나고 프라이빗 부분은 자격 증명 모음에서 내보내지 않습니다. 비대칭 키를 사용하는 모든 암호화 작업은 Azure 키 자격 증명 모음에 위임되며, 키 자격 증명 모음 보안에 의해 보호됩니다.

     비대칭 키를 생성하여 자격 증명 모음에 저장하는 방법에는 여러 가지가 있습니다. 외부에서 키를 생성한 다음 해당 키를 자격 증명 모음에 .pfx 파일로 가져올 수 있습니다. 또는 키 자격 증명 모음 API를 사용하여 자격 증명 모음에서 키를 직접 만들 수 있습니다.

     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터를 사용하려면 비대칭 키가 2048비트 RSA여야 하며, 키 이름에는 문자 "a-z", "A-Z", "0-9" 및 "-"만 사용할 수 있습니다. 이 문서에서 비대칭 키의 이름은 **ContosoMasterKey**라고 하고 있습니다. 이 이름은 키에 사용하고 싶은 고유 이름으로 대체하세요.

    > [!IMPORTANT]
    >  비대칭 키를 가져오면 관리자가 키 에스크로 시스템에 키를 위탁할 수 있으므로 비대칭 키를 가져오는 것은 프로덕션 시나리오에 매우 좋습니다. 프라이빗 키는 자격 증명 모음을 벗어날 수 없으므로 비대칭 키를 자격 증명 모음에서 만든 경우에는 키를 위탁할 수 없습니다. 중요한 데이터를 보호하는 데 사용되는 키는 위탁해야 합니다. 비대칭 키가 손실되는 경우 데이터를 영구적으로 복구할 수 없습니다.

    > [!IMPORTANT]
    >  키 자격 증명 모음에서는 여러 버전의 동일한 이름 키를 지원합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터에서 사용할 키는 버전이 지정되거나 여기저기 사용해서는 안 됩니다. 관리자가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 암호화에 사용된 키를 다른 곳에 사용하려는 경우, 자격 증명 모음에서 다른 이름으로 새 키를 만들어 DEK를 암호화하는 데 사용해야 합니다.

     키를 주요 자격 증명 모음으로 가져오거나 키 자격 증명 모음에 키를 만드는 방법에 대 한 자세한 내용은 [Azure Key Vault 시작](https://go.microsoft.com/fwlink/?LinkId=521402)의 키 **자격 증명 모음에 키 또는 암호 추가** 섹션을 참조 하세요.

3.  **SQL Server에 사용할 Azure Active Directory 서비스 보안 주체 가져오기:** 조직은 Microsoft 클라우드 서비스에 등록할 때 Azure Active Directory를 가져옵니다. 키 자격 증명 모음에 액세스할 때 **에서 사용(Azure Active Directory에 인증받기 위해)할** 서비스 사용자 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 Azure Active Directory에서 만드세요.

    -   **** 관리자가 암호화를 사용하기 위해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 구성할 때 자격 증명 모음에 액세스하는 데 한 서비스 사용자 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가 필요하며,

    -   **** 암호화에 사용된 키의 래핑 해제를 위해 자격 증명 모음에 액세스하기 위해 [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)] 에서 또 다른 서비스 사용자 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 필요로 하게 됩니다.

     애플리케이션을 등록하고 서비스 사용자를 생성하는 방법에 대한 자세한 내용은 [Azure Key Vault 시작](https://go.microsoft.com/fwlink/?LinkId=521402)(영문)의 **Register an Application with Azure Active Directory(Azure Active Directory로 애플리케이션 등록)** 섹션을 참조하세요. 등록 프로세스에서는 각 Azure Active Directory **서비스 사용자** 에 대해 **애플리케이션 ID**( **클라이언트 ID** 라고도 함) 및 **인증 키**( **비밀**이라고도 함)를 반환합니다. `CREATE CREDENTIAL` 문에서 사용 하는 경우 **클라이언트 ID**에서 하이픈을 제거 해야 합니다. 아래의 스크립트에서 사용할 수 있도록 기록해 두세요.

    -   **sysadmin** 로그인용 **서비스 사용자** : **CLIENTID_sysadmin_login** 및 **SECRET_sysadmin_login**

    -   **용** 서비스 사용자 [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]: **CLIENTID_DBEngine** 및 **SECRET_DBEngine**.

4.  **서비스 사용자가 키 자격 증명 모음에 액세스할 수 있는 권한 부여:****CLIENTID_sysadmin_login** 및 **CLIENTID_DBEngine서비스 사용자** 는 모두 키 자격 증명 모음에서 **get**, **list**, **wrapKey**, 및 **unwrapKey** 권한을 필요로 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 통해 키를 생성하려는 경우 키 자격 증명 모음에서 **만들기** 권한도 부여해야 합니다.

    > [!IMPORTANT]
    >  사용자가 키 자격 증명 모음에 적어도 **wrapKey** 및 **unwrapKey** 작업을 사용할 수 있어야 합니다.

     Vault에 사용 권한을 부여하는 방법에 대한 자세한 내용은 [Azure Key Vault 시작](https://go.microsoft.com/fwlink/?LinkId=521402)(영문)의 **Authorize the application to use the key or secret(키 또는 암호를 사용할 수 있도록 애플리케이션에 권한 부여)** 섹션을 참조하세요.

     Azure 키 자격 증명 모음 설명서 링크

    -   [Azure Key Vault란?](https://go.microsoft.com/fwlink/?LinkId=521401)

    -   [Azure Key Vault 시작](https://go.microsoft.com/fwlink/?LinkId=521402)

    -   PowerShell [Azure Key Vault Cmdlet](https://docs.microsoft.com/powershell/module/azurerm.keyvault) 참조

##  <a name="step-2-install-the-sql-server-connector"></a><a name="Step2"></a>2 단계: SQL Server 커넥터 설치
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 컴퓨터의 관리자가 다운로드하여 설치합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터는 [Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/p/?LinkId=521700)에서 다운로드할 수 있습니다.  **Microsoft Azure Key Vault 용 SQL Server 커넥터**를 검색하고, 세부 정보, 시스템 요구 사항 및 설치 지침을 검토하고, 커넥터를 다운로드하도록 선택하고 **실행**을 사용하여 설치를 시작하세요. 라이선스를 검토한 다음 라이선스를 수락하고 계속합니다.

 기본적으로 커넥터는 **C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault**에 설치됩니다. 이 위치는 설치 중 변경할 수 있습니다. (변경할 경우 아래의 스크립트를 조정하세요.)

 설치를 완료하면 다음 항목이 컴퓨터에 설치됩니다.

-   **Microsoft.AzureKeyVaultService.EKM.dll**: 이것은 CREATE CRYPTOGRAPHIC PROVIDER 문을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에 등록해야 하는 암호화 EKM 공급자 DLL입니다.

-   **Azure Key Vault SQL Server 커넥터**: 암호화 EKM 공급자가 키 자격 증명 모음과 통신할 수 있도록 해주는 Windows 서비스입니다.

 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터를 설치하면 원할 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 암호화를 위한 샘플 스크립트를 다운로드할 수도 있습니다.

##  <a name="step-3-configure-sql-server-to-use-an-ekm-provider-for-the-key-vault"></a><a name="Step3"></a>3 단계: Key Vault에 대 한 EKM 공급자를 사용 하도록 SQL Server 구성

###  <a name="permissions"></a><a name="Permissions"></a> 권한
 이 전체 프로세스를 완료하려면 **sysadmin** 고정 서버 역할에 CONTROL SERVER 권한이나 멤버 자격이 있어야 합니다. 특정 작업에는 다음 권한이 필요합니다.

-   암호화 공급자를 만들려면 **sysadmin** 고정 서버 역할에 CONTROL SERVER 권한 또는 멤버 자격이 있어야 합니다.

-   구성 옵션을 변경하고 RECONFIGURE 문을 실행하려면 ALTER SETTINGS 서버 수준 권한이 있어야 합니다. **sysadmin** 및 **serveradmin** 고정 서버 역할은 ALTER SETTINGS 권한을 암시적으로 보유하고 있습니다.

-   자격 증명을 만들려면 ALTER ANY CREDENTIAL 권한이 필요합니다.

-   자격 증명을 로그인에 추가하려면 ALTER ANY LOGIN 권한이 필요합니다.

-   비대칭 키를 만들려면 CREATE ASYMMETRIC KEY 권한이 필요합니다.

###  <a name="to-configure-sql-server-to-use-a-cryptographic-provider"></a><a name="TsqlProcedure"></a>암호화 공급자를 사용 하도록 SQL Server를 구성 하려면

1.  [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 을 구성하여 EKM을 사용하고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 암호화 공급자를 등록합니다(만들기).

    ```sql
    -- Enable advanced options.
    USE master;
    GO

    sp_configure 'show advanced options', 1 ;
    GO
    RECONFIGURE ;
    GO
    -- Enable EKM provider
    sp_configure 'EKM provider enabled', 1 ;
    GO
    RECONFIGURE ;
    GO

    -- Create a cryptographic provider, using the SQL Server Connector
    -- which is an EKM provider for the Azure Key Vault. This example uses 
    -- the name AzureKeyVault_EKM_Prov.

    CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov 
    FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';
    GO
    ```

2.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 암호화 시나리오를 설정 및 관리하려면 키 자격 증명 모음을 사용하도록 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 관리자 로그인용 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 자격 증명을 설정합니다.

    > [!IMPORTANT]
    >  `CREATE CREDENTIAL` 의 **IDENTITY** 인수에는 키 자격 증명 모음 이름이 필요 합니다. `CREATE CREDENTIAL` 의 **secret** 인수에는 * \<클라이언트 ID>* (하이픈이 없는)와 * \<비밀>* 사이에 공백 없이 함께 전달 되어야 합니다.

     다음 예제에서 **클라이언트 ID** (`EF5C8E09-4D2A-4A76-9998-D93440D8115D`)는 하이픈을 제거 하 고 문자열로 `EF5C8E094D2A4A769998D93440D8115D` 입력 되며 **암호** 는 *SECRET_sysadmin_login*문자열로 표시 됩니다.

    ```sql
    USE master;
    CREATE CREDENTIAL sysadmin_ekm_cred 
        WITH IDENTITY = 'ContosoKeyVault', 
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DSECRET_sysadmin_login' 
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;

    -- Add the credential to the SQL Server administrators domain login 
    ALTER LOGIN [<domain>/<login>]
    ADD CREDENTIAL sysadmin_ekm_cred;
    ```

     `CREATE CREDENTIAL` 인수에 대 한 변수를 사용 하 고 클라이언트 ID에서 하이픈을 프로그래밍 방식으로 제거 하는 예는 [CREATE CREDENTIAL &#40;transact-sql&#41;](/sql/t-sql/statements/create-credential-transact-sql)를 참조 하세요.

3.  섹션 3 의 1단계에서 설명한 대로 비대칭 키를 가져온 경우, 다음 예제에서 키 이름을 제공하여 키를 엽니다.

    ```sql
    CREATE ASYMMETRIC KEY CONTOSO_KEY 
    FROM PROVIDER [AzureKeyVault_EKM_Prov]
    WITH PROVIDER_KEY_NAME = 'ContosoMasterKey',
    CREATION_DISPOSITION = OPEN_EXISTING;
    ```

     (키를 내보낼 수 없으므로)프로덕션 환경에 권장되지는 않지만, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 자격 증명 모음에 바로 비대칭 키를 만들 수 있습니다. 앞에서 키를 가져오지 않았으면 다음 스크립트를 사용하여 테스트용으로 키 자격 증명 모음에 비대칭 키를 만드세요. **sysadmin_ekm_cred** 자격 증명으로 프로비저닝된 로그인을 사용하여 스크립트를 실행합니다.

    ```sql
    CREATE ASYMMETRIC KEY CONTOSO_KEY 
    FROM PROVIDER [AzureKeyVault_EKM_Prov]
    WITH ALGORITHM = RSA_2048,
    PROVIDER_KEY_NAME = 'ContosoMasterKey';
    ```

> [!TIP]
>  나타나는 오류 메시지: **공급자에서 공개 키를 내보낼 수 없습니다. 공급자 오류 코드: 2053.** 키 자격 증명 모음에서 **get**, CLE( CLE( **list**, CLE( CLE( **wrapKey**, CLE( CLE( and **unwrapKey** 권한을 필요로 합니다.

 자세한 내용은

-   [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)

-   [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-cryptographic-provider-transact-sql)

-   [CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)

-   [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)

-   [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)

-   [ALTER LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-login-transact-sql)

## <a name="examples"></a>예

###  <a name="example-a-transparent-data-encryption-by-using-an-asymmetric-key-from-the-key-vault"></a><a name="ExampleA"></a>예 A: Key Vault에서 비대칭 키를 사용 하 여 투명한 데이터 암호화
 위의 단계를 완료했으면 자격 증명과 로그인을 만들고, 키 자격 증명 모음에 비대칭 키로 보호되는 데이터베이스 암호화 키를 만듭니다. 데이터베이스 암호화 키를 사용하여 TDE로 데이터베이스를 암호화합니다.

 데이터베이스를 암호화하려면 데이터베이스에 대한 CONTROL 권한이 필요합니다.

##### <a name="to-enable-tde-using-ekm-and-the-key-vault"></a>EKM 및 키 자격 증명 모음을 사용한 TDE 사용 설정

1.  데이터베이스 로드 동안 키 자격 증명 모음 EKM에 액세스할 때 사용할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 용 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 자격 증명을 만듭니다.

    > [!IMPORTANT]
    >  `CREATE CREDENTIAL` 의 **IDENTITY** 인수에는 키 자격 증명 모음 이름이 필요 합니다. `CREATE CREDENTIAL` 의 **secret** 인수에는 * \<클라이언트 ID>* (하이픈이 없는)와 * \<비밀>* 사이에 공백 없이 함께 전달 되어야 합니다.

     다음 예제에서 **클라이언트 ID** (`EF5C8E09-4D2A-4A76-9998-D93440D8115D`)는 하이픈을 제거 하 고 문자열로 `EF5C8E094D2A4A769998D93440D8115D` 입력 되며 **암호** 는 *SECRET_DBEngine*문자열로 표시 됩니다.

    ```sql
    USE master;
    CREATE CREDENTIAL Azure_EKM_TDE_cred 
        WITH IDENTITY = 'ContosoKeyVault', 
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DSECRET_DBEngine' 
        FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;
    ```

2.  TDE용으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서 사용할 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 로그인을 만들고 여기에 자격 증명을 추가합니다. 이 예제에서는 위에 있는 [섹션 3의 3단계](#Step3) 에 설명된 대로 master 데이터베이스용으로 이전에 가져왔거나 만든 키 자격 증명 모음에 저장된 CONTOSO_KEY 비대칭 키를 사용합니다.

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

3.  TDE에 사용할 DEK(데이터베이스 암호화 키)를 만듭니다. DEK는 SQL Server에서 지원되는 알고리즘 또는 키 길이를 사용하여 만들 수 있습니다. DEK는 키 자격 증명 모음에 있는 비대칭 키에 의해 보호됩니다.

     이 예제에서는 위에 있는 [섹션 3의 3단계](#Step3) 에 설명된 대로 앞에서 가져왔거나 만든 키 자격 증명 모음에 저장된 CONTOSO_KEY 비대칭 키를 사용합니다.

    ```sql
    USE ContosoDatabase;
    GO

    CREATE DATABASE ENCRYPTION KEY 
    WITH ALGORITHM = AES_128 
    ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;
    GO

    -- Alter the database to enable transparent data encryption.
    ALTER DATABASE ContosoDatabase 
    SET ENCRYPTION ON ;
    GO
    ```

     자세한 내용은

    -   [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-database-encryption-key-transact-sql)

    -   [ALTER DATABASE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)

###  <a name="example-b-encrypting-backups-by-using-an-asymmetric-key-from-the-key-vault"></a><a name="ExampleB"></a>예 2: Key Vault에서 비대칭 키를 사용 하 여 백업 암호화
 암호화된 백업은 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]부터 지원됩니다. 다음 예제에서는 키 자격 증명 모음에서 비대칭 키로 보호되는 데이터 암호화 키로 암호화된 백업을 만들고 복원합니다.

```sql
USE master;
BACKUP DATABASE [DATABASE_TO_BACKUP]
TO DISK = N'[PATH TO BACKUP FILE]' 
WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD, 
ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);
GO
```

 샘플 복원 코드입니다.

```sql
RESTORE DATABASE [DATABASE_TO_BACKUP]
FROM DISK = N'[PATH TO BACKUP FILE]' WITH FILE = 1, NOUNLOAD, REPLACE;
GO
```

 백업 옵션에 대 한 자세한 내용은 [backup &#40;transact-sql&#41;](/sql/t-sql/statements/backup-transact-sql)을 참조 하세요.

###  <a name="example-c-column-level-encryption-by-using-an-asymmetric-key-from-the-key-vault"></a><a name="ExampleC"></a>예 C: Key Vault의 비대칭 키를 사용한 열 수준 암호화
 다음 예제에서는 키 자격 증명 모음에 비대칭 키로 보호되는 대칭 키를 만듭니다. 그런 다음 데이터베이스에서 대칭 키를 사용하여 데이터를 암호화합니다.

 이 예제에서는 위에 있는 [섹션 3의 3단계](#Step3) 에 설명된 대로 앞에서 가져왔거나 만든 키 자격 증명 모음에 저장된 CONTOSO_KEY 비대칭 키를 사용합니다. `ContosoDatabase` 데이터베이스에서 이 비대칭 키를 사용하려면 다시 CREATE ASYMMETRIC KEY 문을 실행하여 `ContosoDatabase` 데이터베이스에 키에 대한 참조를 제공해야 합니다.

```sql
USE [ContosoDatabase];
GO

-- Create a reference to the key in the key vault
CREATE ASYMMETRIC KEY CONTOSO_KEY 
FROM PROVIDER [AzureKeyVault_EKM_Prov]
WITH PROVIDER_KEY_NAME = 'ContosoMasterKey',
CREATION_DISPOSITION = OPEN_EXISTING;

-- Create the data encryption key.
-- The data encryption key can be created using any SQL Server 
-- supported algorithm or key length.
-- The DEK will be protected by the asymmetric key in the key vault

CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY
    WITH ALGORITHM=AES_256
    ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

DECLARE @DATA VARBINARY(MAX);

--Open the symmetric key for use in this session
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY 
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

--Encrypt syntax
SELECT @DATA = ENCRYPTBYKEY(KEY_GUID('DATA_ENCRYPTION_KEY'), CONVERT(VARBINARY,'Plain text data to encrypt'));

-- Decrypt syntax
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));

--Close the symmetric key
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;
```

## <a name="see-also"></a>참고 항목
 [암호화 공급자 &#40;transact-sql&#41;](/sql/t-sql/statements/create-cryptographic-provider-transact-sql) [create CREDENTIAL&#41;&#40;](/sql/t-sql/statements/create-credential-transact-sql) transact-sql &#40;create 대칭 키&#41;transact-sql &#40;create 대칭 키&#41;[transact-sql &#40;create](/sql/t-sql/statements/create-asymmetric-key-transact-sql) [대칭 키](/sql/t-sql/statements/create-symmetric-key-transact-sql)&#41;[확장 가능 키 관리 EKM](extensible-key-management-ekm.md) ekm [백업 암호화](../../backup-restore/backup-encryption.md) 를 [사용 하 여 tde를 사용 하도록 설정](enable-tde-on-sql-server-using-ekm.md) [암호화 된 백업 만들기](../../backup-restore/create-an-encrypted-backup.md)
