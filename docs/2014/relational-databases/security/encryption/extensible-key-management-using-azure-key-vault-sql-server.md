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
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: 852f65073a55cbe6e8d29b1dc17981cb5356d95f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63011522"
---
# <a name="extensible-key-management-using-azure-key-vault-sql-server"></a>Azure 키 자격 증명 모음(SQL Server)을 사용한 확장 가능 키 관리
  합니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Connector for [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Azure Key Vault를 통해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Azure Key Vault 서비스를 활용 하 여 암호화를 [확장 가능 키 관리 &#40;EKM&#41; ](extensible-key-management-ekm.md) 보호 하기 위해 공급자 해당 암호화 키입니다.  
  
 이 항목의 내용:  
  
-   [EKM 사용](#Uses)  
  
-   [1단계: SQL Server에서 사용할 Key Vault 설정](#Step1)  
  
-   [2단계: SQL Server 커넥터를 설치합니다.](#Step2)  
  
-   [3단계: 키 자격 증명 모음에 EKM 공급자를 사용 하도록 SQL Server 구성](#Step3)  
  
-   [A: 예 Key Vault에서 비대칭 키를 사용 하 여 투명 한 데이터 암호화](#ExampleA)  
  
-   [예 2: Key Vault에서 비대칭 키를 사용 하 여 백업 암호화](#ExampleB)  
  
-   [예 3: Key Vault에서 비대칭 키를 사용 하 여 열 수준 암호화](#ExampleC)  
  
##  <a name="Uses"></a> EKM 사용  
 조직에서 중요한 데이터를 보호하기 위해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 암호화를 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 암호화를 포함 [투명 한 데이터 암호화 &#40;TDE&#41;](transparent-data-encryption.md)합니다 [열 수준 암호화](/sql/t-sql/functions/cryptographic-functions-transact-sql) (CLE) 및 [백업 암호화](../../backup-restore/backup-encryption.md). 이 암호화들에서는 모두 데이터가 대칭 데이터 암호화 키를 사용하여 암호화되고, 이 대칭 데이터 암호화 키는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 저장된 키의 계층 구조로 암호화하여 추가적으로 보호하게 됩니다. EKM 공급자 아키텍처를 사용 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 외부에 저장 된 비대칭 키를 사용 하 여 데이터 암호화 키를 보호 하기 위해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 외부 암호화 공급자에 있습니다. EKM 공급자 아키텍처를 사용하면 추가적인 보안 계층이 생기고 조직은 키와 데이터의 관리를 분리할 수 있습니다.  
  
 Azure Key Vault용 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터를 사용하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 확장성과 성능이 뛰어난 고가용성 Key Vault 서비스를 암호화 키 보호를 위한 EKM 공급자로 활용합니다. Key vault 서비스를 사용할 수 있습니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Azure Virtual Machines 및 온-프레미스 서버에 대 한 합니다. 키 자격 증명 모음 서비스에서는 더 높은 수준의 비대칭 암호화 키 보호를 위해 세부적인 제어 및 모니터링이 이루어지는 HSM(하드웨어 보안 모듈)을 사용할 수도 있습니다. 주요 자격 증명 모음에 대한 자세한 내용은 [Azure 주요 자격 증명 모음](https://go.microsoft.com/fwlink/?LinkId=521401)을 참조하세요.  
  
 다음 이미지에 키 자격 증명 모음을 사용한 EKM의 프로세스 흐름이 요약되어 있습니다. 이미지의 프로세스 단계 번호는 이미지에서 설명하는 설정 단계 번호와 일치하지 않습니다.  
  
 ![Azure Key Vault를 사용하는 SQL Server EKM](../../../database-engine/media/ekm-using-azure-key-vault.png "SQL Server EKM using the Azure Key Vault")  
  
##  <a name="Step1"></a> 1단계: SQL Server에서 사용할 Key Vault 설정  
 다음 단계를 사용하여 암호화 키 보호를 위해 [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]에 사용할 자격 증명 모음 키를 설정하세요. 자격 증명 모음은 이미 조직에 사용 중일 수 있습니다. 자격 증명 모음을 존재 하지 않는 경우 암호화 키를 관리 하도록 지정 하 여 조직에서 Azure 관리자 자격 증명 모음 만들기, 자격 증명 모음에서 비대칭 키를 생성를 만든 다음 권한을 부여할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 키를 사용 하도록 합니다. 자격 증명 모음 서비스에 대해 이해하려면 [Azure 키 자격 증명 모음 시작](https://go.microsoft.com/fwlink/?LinkId=521402)(영문), 및 PowerShell [Azure 키 자격 증명 모음 Cmdlet](/powershell/module/azurerm.keyvault/) (영문) 참조를 검토하세요.  
  
> [!IMPORTANT]  
>  여러 Azure 구독이 있는 경우에 포함 하는 구독을 사용 해야 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다.  
  
1.  **자격 증명 모음을 만듭니다.** 지침을 사용 하 여 자격 증명 모음을 만들 합니다 **key vault를 만듭니다** 부분 [Azure Key Vault를 사용 하 여 시작](https://go.microsoft.com/fwlink/?LinkId=521402)합니다. 자격 증명 모음의 이름은 기록합니다. 이 항목에서는 **ContosoKeyVault** 를 키 자격 증명 모음 이름으로 사용합니다.  
  
2.  **자격 증명 모음에서 비대칭 키를 생성 합니다.** Key vault의 비대칭 키를 보호 하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 암호화 키입니다. 비대칭 키의 공개 부분만 자격 증명 모음을 떠나고 비공개 부분은 자격 증명 모음에서 내보내지 않습니다. 비대칭 키를 사용하는 모든 암호화 작업은 Azure 키 자격 증명 모음에 위임되며, 키 자격 증명 모음 보안에 의해 보호됩니다.  
  
     비대칭 키를 생성하여 자격 증명 모음에 저장하는 방법에는 여러 가지가 있습니다. 외부에서 키를 생성한 다음 해당 키를 자격 증명 모음에 .pfx 파일로 가져올 수 있습니다. 또는 키 자격 증명 모음 API를 사용하여 자격 증명 모음에서 키를 직접 만들 수 있습니다.  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터가 필요 2048 비트 RSA를 비대칭 키 및 키 이름을 사용 하 여 문자 "a-z", "A-z", "0-9", 및 "-"입니다. 이 문서에서 비대칭 키의 이름은 **ContosoMasterKey**라고 하고 있습니다. 이 이름은 키에 사용하고 싶은 고유 이름으로 대체하세요.  
  
    > [!IMPORTANT]  
    >  비대칭 키를 가져오면 관리자가 키 에스크로 시스템에 키를 위탁할 수 있으므로 비대칭 키를 가져오는 것은 프로덕션 시나리오에 매우 좋습니다. 개인 키는 자격 증명 모음을 벗어날 수 없으므로 비대칭 키를 자격 증명 모음에서 만든 경우에는 키를 위탁할 수 없습니다. 중요한 데이터를 보호하는 데 사용되는 키는 위탁해야 합니다. 비대칭 키가 손실되는 경우 데이터를 영구적으로 복구할 수 없습니다.  
  
    > [!IMPORTANT]  
    >  키 자격 증명 모음에서는 여러 버전의 동일한 이름 키를 지원합니다. 사용할 키 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터 버전이 지정 되거나 여기저기 않아야 합니다. 관리자가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 암호화에 사용된 키를 다른 곳에 사용하려는 경우, 자격 증명 모음에서 다른 이름으로 새 키를 만들어 DEK를 암호화하는 데 사용해야 합니다.  
  
     키를 키 자격 증명 모음에 가져오는 방법이나 키 자격 증명 모음에서 키를 만드는 방법(프로덕션 환경에는 권장하지 않음)에 대한 자세한 내용은 **Azure 키 자격 증명 모음 시작**[(영문)의 Add a key or secret to the key vault(키 또는 암호를 키 자격 증명 모음에 추가)](https://go.microsoft.com/fwlink/?LinkId=521402)섹션을 참조하세요.  
  
3.  **SQL Server에 사용할 Azure Active Directory 서비스 주체를 가져옵니다.** 조직은 Microsoft 클라우드 서비스에 등록할 때 Azure Active Directory를 가져옵니다. 만들 **서비스 주체** 에 대 한 Azure Active Directory에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] key vault에 액세스 하는 동안 (Azure Active Directory 인증) 하는 데 있습니다.  
  
    -   하나의 **서비스 주체** 필요로 하 게 됩니다는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 하는 동안 자격 증명 모음에 액세스 하려면 관리자 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 암호화를 사용 하도록 합니다.  
  
    -   다른 **서비스 주체** 필요로 하 게 됩니다 합니다 [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)] 에서 사용 되는 래핑 해제 키에 대 한 자격 증명 모음 액세스 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 암호화 합니다.  
  
     애플리케이션을 등록하고 서비스 사용자를 생성하는 방법에 대한 자세한 내용은 **Azure 키 자격 증명 모음 시작** (영문)의 [Register an Application with Azure Active Directory(Azure Active Directory로 애플리케이션 등록)](https://go.microsoft.com/fwlink/?LinkId=521402)섹션을 참조하세요. 등록 프로세스에서는 각 Azure Active Directory **서비스 사용자** 에 대해 **애플리케이션 ID**( **클라이언트 ID** 라고도 함) 및 **인증 키**( **비밀**이라고도 함)를 반환합니다. 에 사용 되는 경우는 `CREATE CREDENTIAL` 문을에서 하이픈 제거 해야 합니다 **클라이언트 ID**. 아래의 스크립트에서 사용할 수 있도록 기록해 두세요.  
  
    -   **서비스 주체** 에 대 한는 **sysadmin** 로그인: **CLIENTID_sysadmin_login** 고 **SECRET_sysadmin_login**  
  
    -   **서비스 주체** 에 대 한는 [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]: **CLIENTID_DBEngine** 하 고 **SECRET_DBEngine**합니다.  
  
4.  **Key Vault에 액세스 하려면 서비스 주체에 권한을 부여 합니다.** 모두를 **CLIENTID_sysadmin_login** 및 **clientid_dbengine 주체** 필요 합니다 **가져오기**를 **목록**,  **wrapKey**, 및 **unwrapKey** key vault에 대 한 사용 권한. 통해 키를 생성 하려는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 부여 해야 합니다 **만들기** 키 자격 증명 모음에 대 한 사용 권한.  
  
    > [!IMPORTANT]  
    >  사용자가 키 자격 증명 모음에 적어도 **wrapKey** 및 **unwrapKey** 작업을 사용할 수 있어야 합니다.  
  
     자격 증명 모음에 사용 권한을 부여하는 방법에 대한 자세한 내용은 **Azure 키 자격 증명 모음 시작**[(영문)의 Authorize the application to use the key or secret(키 또는 암호를 사용할 수 있도록 애플리케이션에 권한 부여)](https://go.microsoft.com/fwlink/?LinkId=521402)섹션을 참조하세요.  
  
     Azure 키 자격 증명 모음 설명서 링크  
  
    -   [Azure 키 자격 증명 모음이란?](https://go.microsoft.com/fwlink/?LinkId=521401)  
  
    -   [Azure 키 자격 증명 모음 시작](https://go.microsoft.com/fwlink/?LinkId=521402)  
  
    -   PowerShell [Azure 주요 자격 증명 모음 Cmdlet](https://go.microsoft.com/fwlink/?LinkId=521403) 참조  
  
##  <a name="Step2"></a> 2단계: SQL Server 커넥터를 설치 합니다.  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터를 다운로드 및 관리자가 설치 된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 컴퓨터. 합니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터에서 다운로드할 수는 [Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/p/?LinkId=521700)합니다.  **Microsoft Azure 키 자격 증명 모음용 SQL Server 커넥터**를 검색하고, 세부 정보, 시스템 요구 사항 및 설치 지침을 검토하고, 커넥터를 다운로드하도록 선택하고 **실행**을 사용하여 설치를 시작하세요. 라이선스를 검토한 다음 라이선스를 수락하고 계속합니다.  
  
 기본적으로 커넥터는 **C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault**에 설치됩니다. 이 위치는 설치 중 변경할 수 있습니다. (변경할 경우 아래의 스크립트를 조정하세요.)  
  
 설치를 완료하면 다음 항목이 컴퓨터에 설치됩니다.  
  
-   **Microsoft.AzureKeyVaultService.EKM.dll**: 이 암호화 EKM 공급자를 등록 해야 하는 DLL [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CREATE CRYPTOGRAPHIC PROVIDER 문을 사용 하 여 합니다.  
  
-   **Azure Key Vault SQL Server 커넥터**: Key vault를 사용 하 여 통신 하는 암호화 EKM 공급자를 사용 하도록 설정 하는 Windows 서비스입니다.  
  
 합니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터 설치 또한 필요에 따라 샘플 스크립트를 다운로드할 수 있습니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 암호화 합니다.  
  
##  <a name="Step3"></a> 3 단계: 키 자격 증명 모음에 EKM 공급자를 사용 하도록 SQL Server 구성  
  
###  <a name="Permissions"></a> Permissions  
 이 전체 프로세스를 완료하려면 **sysadmin** 고정 서버 역할에 CONTROL SERVER 권한이나 멤버 자격이 있어야 합니다. 특정 작업에는 다음 권한이 필요합니다.  
  
-   암호화 공급자를 만들려면 **sysadmin** 고정 서버 역할에 CONTROL SERVER 권한 또는 멤버 자격이 있어야 합니다.  
  
-   구성 옵션을 변경하고 RECONFIGURE 문을 실행하려면 ALTER SETTINGS 서버 수준 권한이 있어야 합니다. **sysadmin** 및 **serveradmin** 고정 서버 역할은 ALTER SETTINGS 권한을 암시적으로 보유하고 있습니다.  
  
-   자격 증명을 만들려면 ALTER ANY CREDENTIAL 권한이 필요합니다.  
  
-   자격 증명을 로그인에 추가하려면 ALTER ANY LOGIN 권한이 필요합니다.  
  
-   비대칭 키를 만들려면 CREATE ASYMMETRIC KEY 권한이 필요합니다.  
  
###  <a name="TsqlProcedure"></a> 암호화 공급자를 사용 하도록 SQL Server를 구성 하려면  
  
1.  [!INCLUDE[ssDE](../../../includes/ssde-md.md)]을 구성하여 EKM을 사용하고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 암호화 공급자를 등록합니다(만들기).  
  
    ```  
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
  
2.  설치를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에 대 한 자격 증명을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설정 및 관리 하기 위해 key vault를 사용 하려면 관리자 로그인 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 암호화 시나리오입니다.  
  
    > [!IMPORTANT]  
    >  합니다 **IDENTITY** 인수의 `CREATE CREDENTIAL` 키 자격 증명 모음 이름이 필요 합니다. **비밀** 인수의 `CREATE CREDENTIAL` 필요 합니다  *\<클라이언트 ID >* (하이픈 없이) 및  *\<비밀 >* 전달할 사이 공백을 없이 함께.  
  
     다음 예제에서 **클라이언트 ID** (`EF5C8E09-4D2A-4A76-9998-D93440D8115D`)는 하이픈이 제거되어 문자열 `EF5C8E094D2A4A769998D93440D8115D` 로 입력되어 있으며 **암호** 는 문자열 *SECRET_sysadmin_login*으로 표현되었습니다.  
  
    ```  
    USE master;  
    CREATE CREDENTIAL sysadmin_ekm_cred   
        WITH IDENTITY = 'ContosoKeyVault',   
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DSECRET_sysadmin_login'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;  
  
    -- Add the credential to the SQL Server administrators domain login   
    ALTER LOGIN [<domain>/<login>]  
    ADD CREDENTIAL sysadmin_ekm_cred;  
    ```  
  
     에 대 한 변수를 사용 하는 예는 `CREATE CREDENTIAL` 인수 및 클라이언트 ID에서 하이픈을 제거 하는 프로그래밍 방식으로 참조 [CREATE CREDENTIAL &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql).  
  
3.  섹션 3 의 1단계에서 설명한 대로 비대칭 키를 가져온 경우, 다음 예제에서 키 이름을 제공하여 키를 엽니다.  
  
    ```  
    CREATE ASYMMETRIC KEY CONTOSO_KEY   
    FROM PROVIDER [AzureKeyVault_EKM_Prov]  
    WITH PROVIDER_KEY_NAME = 'ContosoMasterKey',  
    CREATION_DISPOSITION = OPEN_EXISTING;  
    ```  
  
     (키를 내보낼 수 없으므로)프로덕션 환경에 권장되지는 않지만, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 자격 증명 모음에 바로 비대칭 키를 만들 수 있습니다. 앞에서 키를 가져오지 않았으면 다음 스크립트를 사용하여 테스트용으로 키 자격 증명 모음에 비대칭 키를 만드세요. **sysadmin_ekm_cred** 자격 증명으로 프로비저닝된 로그인을 사용하여 스크립트를 실행합니다.  
  
    ```  
    CREATE ASYMMETRIC KEY CONTOSO_KEY   
    FROM PROVIDER [AzureKeyVault_EKM_Prov]  
    WITH ALGORITHM = RSA_2048,  
    PROVIDER_KEY_NAME = 'ContosoMasterKey';  
    ```  
  
> [!TIP]  
>  오류 메시지를 수신 하는 사용자가 **공급자에서 공개 키를 내보낼 수 없습니다. 공급자 오류 코드: 2053.** 키 자격 증명 모음에서 **get**, CLE( CLE( **list**, CLE( CLE( **wrapKey**, CLE( CLE( and **unwrapKey** 권한을 필요로 합니다.  
  
 자세한 내용은 다음 항목을 참조하세요.  
  
-   [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
-   [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-cryptographic-provider-transact-sql)  
  
-   [CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)  
  
-   [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)  
  
-   [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)  
  
-   [ALTER LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-login-transact-sql)  
  
## <a name="examples"></a>예제  
  
###  <a name="ExampleA"></a> A: 예 Key Vault에서 비대칭 키를 사용 하 여 투명 한 데이터 암호화  
 위의 단계를 완료했으면 자격 증명과 로그인을 만들고, 키 자격 증명 모음에 비대칭 키로 보호되는 데이터베이스 암호화 키를 만듭니다. 데이터베이스 암호화 키를 사용하여 TDE로 데이터베이스를 암호화합니다.  
  
 데이터베이스를 암호화하려면 데이터베이스에 대한 CONTROL 권한이 필요합니다.  
  
##### <a name="to-enable-tde-using-ekm-and-the-key-vault"></a>EKM 및 키 자격 증명 모음을 사용한 TDE 사용 설정  
  
1.  데이터베이스 로드 동안 키 자격 증명 모음 EKM에 액세스할 때 사용할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]용 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 자격 증명을 만듭니다.  
  
    > [!IMPORTANT]  
    >  합니다 **IDENTITY** 인수의 `CREATE CREDENTIAL` 키 자격 증명 모음 이름이 필요 합니다. **비밀** 인수의 `CREATE CREDENTIAL` 필요 합니다  *\<클라이언트 ID >* (하이픈 없이) 및  *\<비밀 >* 전달할 사이 공백을 없이 함께.  
  
     다음 예제에서 **클라이언트 ID** (`EF5C8E09-4D2A-4A76-9998-D93440D8115D`)는 하이픈이 제거되어 문자열 `EF5C8E094D2A4A769998D93440D8115D` 로 입력되어 있으며 **암호** 는 문자열 *SECRET_DBEngine*으로 표현되었습니다.  
  
    ```  
    USE master;  
    CREATE CREDENTIAL Azure_EKM_TDE_cred   
        WITH IDENTITY = 'ContosoKeyVault',   
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DSECRET_DBEngine'   
        FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;  
    ```  
  
2.  TDE용으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 사용할 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 로그인을 만들고 여기에 자격 증명을 추가합니다. 이 예제에서는 위에 있는 [섹션 3의 3단계](#Step3) 에 설명된 대로 master 데이터베이스용으로 이전에 가져왔거나 만든 키 자격 증명 모음에 저장된 CONTOSO_KEY 비대칭 키를 사용합니다.  
  
    ```  
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
  
    ```  
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
  
     자세한 내용은 다음 항목을 참조하세요.  
  
    -   [CREATE DATABASE ENCRYPTION KEY&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-database-encryption-key-transact-sql)  
  
    -   [ALTER DATABASE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
###  <a name="ExampleB"></a> 예 2: Key Vault에서 비대칭 키를 사용 하 여 백업 암호화  
 암호화된 백업은 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]부터 지원됩니다. 다음 예제에서는 키 자격 증명 모음에서 비대칭 키로 보호되는 데이터 암호화 키로 암호화된 백업을 만들고 복원합니다.  
  
```  
USE master;  
BACKUP DATABASE [DATABASE_TO_BACKUP]  
TO DISK = N'[PATH TO BACKUP FILE]'   
WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,   
ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);  
GO  
```  
  
 샘플 복원 코드입니다.  
  
```  
RESTORE DATABASE [DATABASE_TO_BACKUP]  
FROM DISK = N'[PATH TO BACKUP FILE]' WITH FILE = 1, NOUNLOAD, REPLACE;  
GO  
```  
  
 백업 옵션에 대 한 자세한 내용은 참조 하세요. [백업 &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)합니다.  
  
###  <a name="ExampleC"></a> 예 3: Key Vault에서 비대칭 키를 사용 하 여 열 수준 암호화  
 다음 예제에서는 키 자격 증명 모음에 비대칭 키로 보호되는 대칭 키를 만듭니다. 그런 다음 데이터베이스에서 대칭 키를 사용하여 데이터를 암호화합니다.  
  
 이 예제에서는 위에 있는 [섹션 3의 3단계](#Step3) 에 설명된 대로 앞에서 가져왔거나 만든 키 자격 증명 모음에 저장된 CONTOSO_KEY 비대칭 키를 사용합니다. `ContosoDatabase` 데이터베이스에서 이 비대칭 키를 사용하려면 다시 CREATE ASYMMETRIC KEY 문을 실행하여 `ContosoDatabase` 데이터베이스에 키에 대한 참조를 제공해야 합니다.  
  
```  
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
  
## <a name="see-also"></a>관련 항목  
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-cryptographic-provider-transact-sql)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-symmetric-key-transact-sql)   
 [확장 가능 키 관리 &#40;EKM&#41;](extensible-key-management-ekm.md)   
 [EKM을 사용 하 여 TDE를 사용 하도록 설정](enable-tde-on-sql-server-using-ekm.md)   
 [백업 암호화](../../backup-restore/backup-encryption.md)   
 [암호화된 백업 만들기](../../backup-restore/create-an-encrypted-backup.md)  
  
  
