---
title: Azure Key Vault를 사용한 SQL Server TDE 확장 가능 키 관리 - 설정 단계 | Microsoft 문서
ms.custom: ''
ms.date: 08/24/2018
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- EKM, with key vault setup
- SQL Server Connector, setup
- SQL Server Connector
ms.assetid: c1f29c27-5168-48cb-b649-7029e4816906
author: aliceku
ms.author: aliceku
ms.openlocfilehash: 3d9b28b1723b5c984446be09336b24ff5e2d2bb0
ms.sourcegitcommit: 2efb0fa21ff8093384c1df21f0e8910db15ef931
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68316644"
---
# <a name="sql-server-tde-extensible-key-management-using-azure-key-vault---setup-steps"></a>Azure Key Vault를 사용한 SQL Server TDE 확장 가능 키 관리 - 설정 단계
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  다음 단계는 Azure Key Vault용 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]커넥터 설치 및 구성을 안내합니다.  
  
## <a name="before-you-start"></a>시작하기 전에  
 SQL Server에서 Azure 주요 자격 증명 모음을 사용하려면 몇 가지 필수 조건이 있습니다.  
  
-   Azure 구독이 있어야 합니다.  
  
-   최신 [Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/)(5.2.0 이상)을 설치하세요.  

-   Azure Active Directory 만들기  

-   [Azure 주요 자격 증명 모음을 사용한 확장 가능 키 관리 &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)를 검토하여 Azure 주요 자격 증명 모음을 사용하는 EKM 스토리지의 보안 주체를 파악합니다.  

-   실행 중인 SQL Server 버전에 적절한 재배포 가능한 Visual Studio C++의 최신 버전이 설치되어 있는지 확인하세요.
  
SQL Server 버전  |재배포 가능 설치 링크    
---------|--------- 
2008, 2008 R2, 2012, 2014 | [Visual Studio 2013용 Visual C++ 재배포 가능 패키지](https://www.microsoft.com/download/details.aspx?id=40784)    
2016 | [Visual Studio 2015용 Visual C++ 재배포 가능 패키지](https://www.microsoft.com/download/details.aspx?id=48145)    
 
  
## <a name="part-i-set-up-an-azure-active-directory-service-principal"></a>1부: Azure Active Directory 서비스 사용자 설정  
 Azure 주요 자격 증명 모음에 SQL Server 액세스 권한을 부여하려면 AAD(Azure Active Directory)의 서비스 사용자 계정이 필요합니다.  
  
1.  [Azure Portal](https://ms.portal.azure.com/)로 이동하고 로그인합니다.  
  
2.  Azure Active Directory에 애플리케이션을 등록합니다. 애플리케이션 등록에 대한 자세한 단계별 지침은 **Azure 주요 자격 증명 모음 블로그 게시물** 의 [애플리케이션의 ID 가져오기](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/)섹션을 참조하세요.  
  
3.  **클라이언트 ID** 및 **클라이언트 암호** 를 복사하여 이후 단계에서 주요 자격 증명 모음에 대한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 액세스 권한을 부여하는 데 사용합니다.  
  
 ![ekm-client-id](../../../relational-databases/security/encryption/media/ekm-client-id.png "ekm-client-id")  
  
 ![ekm-key-id](../../../relational-databases/security/encryption/media/ekm-key-id.png "ekm-key-id")  
  
## <a name="part-ii-create-a-key-vault-and-key"></a>2부: 주요 자격 증명 모음 및 키 만들기  
 여기에서 만드는 주요 자격 증명 모음 및 키는 암호화 키 보호에 대해 SQL Server 데이터베이스 엔진에서 사용됩니다.  
  
> [!IMPORTANT]  
>  주요 자격 증명 모음이 생성되는 구독은 Azure Active Directory 서비스 사용자가 생성된 동일한 기본 Azure Active Directory에 있어야 합니다. SQL Server 커넥터에 대한 서비스 보안 주체를 만들기 위한 기본 Active Directory가 아닌 다른 Active Directory를 사용하려는 경우 사용자 키 자격 증명 모음을 만들기 전에 Azure 계정에 기본 Active Directory를 변경해야 합니다. 사용할 디렉터리로 기본 Active Directory를 변경하는 방법을 알아보려면 SQL Server 커넥터 [FAQ](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixB)를 참조하세요.  
  
1.  **PowerShell 열기 및 로그인**  
  
     [최신 Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/)(5.2.0 이상)을 설치하고 시작합니다. 다음 명령을 사용하여 Azure 계정에 로그인합니다.  
  
    ```powershell  
    Connect-AzAccount  
    ```  
  
     문은 다음을 반환합니다.  
  
    ```  
    Environment           : AzureCloud  
    Account               : <account_name>  
    TenantId              : <tenant_id>  
    SubscriptionId        : <subscription_id>  
    CurrentStorageAccount :  
    ```  
  
    > [!NOTE]  
    >  구독이 여러 개 있는 상황에서 자격 증명 모음에 특정 구독 하나만 사용하도록 지정하려면 `Get-AzSubscription` 을 사용하여 구독을 표시하고, `Select-AzSubscription` 을 사용하여 올바른 구독을 선택합니다. 그러지 않으면 PowerShell에서 기본적으로 구독을 하나 선택합니다.  
  
2.  **새 리소스 그룹 만들기**  
  
     Azure Resource Manager를 통해 생성된 모든 Azure 리소스는 리소스 그룹에 포함되어야 합니다. 주요 자격 증명 모음을 보관하는 리소스 그룹을 만듭니다. 이 예에서는 `ContosoDevRG`를 사용합니다. 모든 주요 자격 증명 모음 이름은 전역적으로 고유하므로 **고유한** 리소스 그룹 및 주요 자격 증명 모음 이름을 선택합니다.  
  
    ```powershell  
    New-AzResourceGroup -Name ContosoDevRG -Location 'East Asia'  
    ```  
  
     문은 다음을 반환합니다.  
  
    ```  
    ResourceGroupName: ContosoDevRG  
    Location         : eastasia  
    ProvisioningState: Succeeded  
    Tags             :   
    ResourceId       : /subscriptions/<subscription_id>/  
                        resourceGroups/ContosoDevRG  
    ```  
  
    > [!NOTE]  
    >  `-Location parameter`의 경우 `Get-AzureLocation` 명령을 사용하여 이 예제의 리소스 그룹에 대체 위치를 지정하는 방법을 확인합니다. 자세한 내용을 보려면 다음을 입력합니다. `Get-Help Get-AzureLocation`  
  
3.  **주요 자격 증명 모음 만들기**  
  
     `New-AzKeyVault` cmdlet에는 리소스 그룹 이름, 주요 자격 증명 모음 이름, 지리적 위치가 필요합니다. 예를 들어 `ContosoDevKeyVault`라고 이름이 지정된 주요 자격 증명 모음의 경우 다음을 입력합니다.  
  
    ```powershell  
    New-AzKeyVault -VaultName 'ContosoDevKeyVault' `  
       -ResourceGroupName 'ContosoDevRG' -Location 'East Asia'  
    ```  
  
     주요 자격 증명 모음의 이름을 기록합니다.  
  
     문은 다음을 반환합니다.  
  
    ```  
    Vault Name                       : ContosoDevKeyVault  
    Resource Group Name              : ContosoDevRG  
    Location                         : East Asia  
    ResourceId                       : /subscriptions/<subscription_id>/  
                                        resourceGroups/ContosoDevRG/providers/  
                                        Microsoft/KeyVault/vaults/ContosoDevKeyVault  
    Vault URI: https://ContosoDevKeyVault.vault.azure.net  
    Tenant ID                        : <tenant_id>  
    SKU                              : Standard  
    Enabled For Deployment?          : False  
    Enabled For Template Deployment? : False  
    Enabled For Disk Encryption?     : False  
    Access Policies                  :  
             Tenant ID              : <tenant_id>  
             Object ID              : <object_id>  
             Application ID         :   
             Display Name           : <display_name>  
             Permissions to Keys    : get, create, delete, list, update, import,   
                                      backup, restore  
             Permissions to Secrets : all  
    Tags                             :  
    ```  
  
4.  **Azure Active Directory 서비스 사용자가 주요 자격 증명 모음에 액세스할 수 있는 권한 부여**  
  
     다른 사용자 및 애플리케이션이 사용자의 주요 자격 증명 모음을 사용하도록 권한을 부여할 수 있습니다.   
    이 경우 1부에서 만든 Azure Active Directory 서비스 사용자를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 권한을 부여해 봅시다.  
  
    > [!IMPORTANT]  
    >  Azure Active Directory 서비스 사용자는 Key Vault에 대해 적어도 `get`, `wrapKey` 및 `unwrapKey` 권한이 있어야 합니다.  
  
     아래와 같이 **매개 변수에 대해 1부의** 클라이언트 ID `ServicePrincipalName` 를 사용합니다. 성공적으로 실행되는 경우 `Set-AzKeyVaultAccessPolicy` 가 출력 없이 자동으로 실행됩니다.  
  
    ```powershell  
    Set-AzKeyVaultAccessPolicy -VaultName 'ContosoDevKeyVault'`  
      -ServicePrincipalName EF5C8E09-4D2A-4A76-9998-D93440D8115D `  
      -PermissionsToKeys get, wrapKey, unwrapKey  
    ```  
  
     `Get-AzKeyVault` cmdlet을 호출하여 권한을 확인합니다. 이 주요 자격 증명 모음에 대한 액세스 권한이 있는 다른 테넌트로 나열되는 AAD 애플리케이션 이름이 '액세스 정책' 아래의 명령문 출력에 표시되어야 합니다.  
  
       
5.  **주요 자격 증명 모음에서 비대칭 키 생성**  
  
     Azure Key Vault에서 키를 생성하는 방법은 1) 기존 키 가져오기 또는 2) 새 키 만들기 등 두 가지가 있습니다.  
                  
      > [!NOTE]
        >  SQL Server는 2048비트 RSA 키만 지원합니다.
        
    ### <a name="best-practice"></a>최선의 구현 방법:
    
    빠른 키 복구를 보장하고 Azure 외부의 데이터에 액세스하려면 다음 모범 사례를 권장합니다.
 
    1. 로컬 HSM 디바이스에 암호화 키를 로컬로 만듭니다. (이 키는 SQL Server가 지원할 수 있도록 비대칭, RSA 2048 키여야 합니다.)
    2. Azure Key Vault에 암호화 키를 가져옵니다. 작업을 수행하는 방법은 다음 단계를 참조하세요.
    3. Azure Key Vault에 키를 처음 사용하는 경우 먼저 Azure Key Vault 키 백업을 수행합니다. [백업-AzureKeyVaultKey](/sql/relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault) 명령에 대해 알아 봅니다.
    4. 키에 대한 어떤 변경이 발생할 때마다(예: ACL 추가, 태그 추가, 키 특성 추가) 다른 Azure Key Vault 키 백업을 수행해야 합니다.

        > [!NOTE]  
        >  키 백업 작업은 장소에 상관없이 저장할 수 있는 파일을 반환하는 Azure Key Vault 키 작업입니다.

    ### <a name="types-of-keys"></a>키의 유형:
    SQL Server와 작동할 Azure Key Vault에서 생성할 수 있는 키는 두 가지 유형입니다. 둘 다 비대칭 2048비트 RSA 키입니다.  
  
    -   **소프트웨어 보호:** 소프트웨어에서 처리되고 안전하게 암호화됩니다. 소프트웨어 보호된 키에 대한 작업은 Azure 가상 컴퓨터에서 발생합니다. 프로덕션 배포에 사용되지 않는 키의 경우 추천됩니다.  
  
    -   **HSM 보호:** 추가 보안을 위해 HSM(하드웨어 보안 모듈)에서 생성하고 보호합니다. 비용은 키 버전당 약 1달러입니다.  
  
        > [!IMPORTANT]  
        >  SQL Server 커넥터는 “a-z”, “A-Z”, “0-9” 및 “-” 문자만 키 이름에 사용할 수 있으며, 키 이름은 26자로 제한됩니다.   
        > Azure 주요 자격 증명 모음에서 동일한 키 이름의 여러 키 버전은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터와 함께 작동되지 않습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 사용되는 Azure Key Vault 키를 전환하려면 [SQL Server 커넥터 유지 관리 및 문제 해결](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)에서 키 롤오버 단계를 참조하세요.  

    ### <a name="import-an-existing-key"></a>기존 키 가져오기   
  
    기존 2048비트 RSA 소프트웨어 보호된 키가 있는 경우 키를 Azure Key Vault에 업로드할 수 있습니다. 예를 들어 `C:\\` 드라이브에 저장된 .PFX 파일(이름: `softkey.pfx` )이 있고 Azure Key Vault에 업로드하려는 경우에는 다음을 입력하여 .PFX 파일에 `securepfxpwd` 의 암호에 대한 `12987553` 변수를 설정합니다.  
  
    ``` powershell  
    $securepfxpwd = ConvertTo-SecureString -String '12987553' `  
      -AsPlainText -Force  
    ```  
  
    다음을 입력하여 .PFX 파일에서 키를 가져올 수 있습니다. 이렇게 하면 Key Vault 서비스에서 하드웨어(권장)로부터 키가 보호됩니다.  
  
    ``` powershell  
        Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' `  
          -Name 'ContosoFirstKey' -KeyFilePath 'c:\softkey.pfx' `  
          -KeyFilePassword $securepfxpwd $securepfxpwd  -Destination 'HSM'  
    ```  
 
    > [!IMPORTANT]  
    > 비대칭 키를 가져오면 관리자가 키 에스크로 시스템에 키를 위탁할 수 있으므로 비대칭 키를 가져오는 것은 프로덕션 시나리오에 매우 좋습니다. 프라이빗 키는 자격 증명 모음을 벗어날 수 없으므로 비대칭 키를 자격 증명 모음에서 만든 경우에는 키를 위탁할 수 없습니다. 중요한 데이터를 보호하는 데 사용되는 키는 위탁해야 합니다. 비대칭 키가 손실되는 경우 데이터가 영구적으로 손실됩니다.  

    ### <a name="create-a-new-key"></a>새 키 만들기
    #### <a name="example"></a>예:  
    또는 Azure Key Vault에 직접 새 암호화 키를 만들고 소프트웨어 보호 또는 HSM 보호를 설정할 수 있습니다.  이 예제에서는 `Add-AzureKeyVaultKey cmdlet`을 사용하여 소프트웨어 보호 키를 만들어 봅시다.  

    ``` powershell  
    Add-AzureKeyVaultKey -VaultName 'ContosoDevKeyVault' `  
      -Name 'ContosoRSAKey0' -Destination 'Software'  
    ```  
  
    문은 다음을 반환합니다.  
  
    ```  
    Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes  
    Key        :  {"kid":"https:contosodevKeyVault.azure.net/keys/  
                   ContosoRSAKey0/<guid>","dty":"RSA:,"key_ops": ...  
    VaultName  : contosodevkeyvault  
    Name       : contosoRSAKey0  
    Version    : <guid>  
    Id         : https://contosodevkeyvault.vault.azure.net:443/  
                 keys/ContosoRSAKey0/<guid>  
    ```  
 > [!IMPORTANT]  
 > 주요 자격 증명 모음은 동일한 이름이 지정된 키의 여러 버전을 지원하지만 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터에서 사용할 키는 버전이 지정되거나 여기저기 사용해서는 안 됩니다. 관리자가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 암호화에 사용된 키를 다른 곳에 사용하려는 경우, 자격 증명 모음에서 다른 이름으로 새 키를 만들어 DEK를 암호화하는 데 사용해야 합니다.  
   
  
## <a name="part-iii-install-the-includessnoversionincludesssnoversion-mdmd-connector"></a>3부: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터 설치  
 [Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/p/?LinkId=521700)에서 SQL Server 커넥터를 다운로드합니다. 이 작업은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 컴퓨터의 관리자가 수행해야 합니다.  

> [!NOTE]  
>  1\.0.0.440 및 이전 버전은 대체되었으며 프로덕션 환경에서 더 이상 지원되지 않습니다. [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=45344)를 방문하고 "SQL Server 커넥터 업그레이드" 아래의 [SQL Server 커넥터 유지 관리 및 문제 해결](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md) 페이지에 있는 지침을 사용하여 1.0.1.0 이상 버전으로 업그레이드하세요.

> [!NOTE]  
> 1\.0.5.0 버전의 경우 지문 알고리즘 측면에서 큰 변화가 있습니다. 1\.0.5.0 버전으로 업그레이드한 후 데이터베이스 복원 실패가 발생할 수 있습니다. [447099](https://support.microsoft.com/help/4470999/db-backup-problems-to-sql-server-connector-for-azure-1-0-5-0) KB 문서를 참조하세요.
  
 ![ekm-connector-install](../../../relational-databases/security/encryption/media/ekm-connector-install.png "ekm-connector-install")  
  
 기본적으로 커넥터는 C:\Program Files\SQL Server Connector for Microsoft Azure 주요 자격 증명 모음에 설치됩니다. 이 위치는 설치 중 변경할 수 있습니다. (변경할 경우 아래의 스크립트를 조정하세요.)  
  
 커넥터에 대한 인터페이스가 없는데도 성공적으로 설치되는 경우에는 컴퓨터에 **Microsoft.AzureKeyVaultService.EKM.dll** 이 설치되어 있기 때문입니다. 이것은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 문을 사용하여 `CREATE CRYPTOGRAPHIC PROVIDER` 에 등록해야 하는 암호화 EKM 공급자 DLL입니다.  
  
 SQL Server 커넥터를 설치하면 원할 경우 SQL Server 암호화를 위한 샘플 스크립트를 다운로드할 수도 있습니다.  
  
 SQL Server 커넥터에 대한 오류 코드 설명, 구성 설정 또는 유지 관리 작업을 보려면 이 항목의 맨 아래에 있는 부록을 참조하세요.  
  
-   [A. SQL Server 커넥터에 대한 유지 관리 지침](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixA)  
  
-   [C. SQL Server 커넥터에 대한 오류 코드 설명](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixC)  
  
  
## <a name="part-iv-configure-includessnoversionincludesssnoversion-mdmd"></a>4부: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성  
 이 섹션의 각 작업에 필요한 최소 권한 수준에 대한 정보를 보려면 [B. 질문과 대답](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixB)을 참조하세요.  
  
1.  **sqlcmd.exe 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Studio 실행**  
  
2.  **[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 을(를) 구성하여 EKM 사용**  
  
     다음 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 스크립트를 실행하여 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 을(를) 구성하고 EKM 공급자를 사용합니다.  
  
    ```sql  
    -- Enable advanced options.  
    USE master;  
    GO  
  
    sp_configure 'show advanced options', 1;  
    GO  
    RECONFIGURE;  
    GO  
  
    -- Enable EKM provider  
    sp_configure 'EKM provider enabled', 1;  
    GO  
    RECONFIGURE;  
    ```  
  
3.  **EKM 공급자로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터 등록(만들기) [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**  
  
     -- Azure 주요 자격 증명 모음에 대한 EKM 공급자인 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터를 사용하여 암호화 공급자를 만듭니다.    
    이 예제에서는 `AzureKeyVault_EKM_Prov`이름을 사용합니다.  
  
    ```sql  
    CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov   
    FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';  
    GO  
    ```  
  
    > [!NOTE]  
    >  파일 경로 길이는 256자를 초과할 수 없습니다.  
  
  
4.  **주요 자격 증명 모음을 사용하기 위해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인에 대해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 자격 증명 설정**  
  
     주요 자격 증명 모음에서 키를 사용하여 암호화를 수행할 각 로그인에 자격 증명을 추가해야 합니다. 여기에는 다음이 포함될 수 있습니다.  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 암호화 시나리오를 설정하고 관리하기 위해 주요 자격 증명 모음을 사용할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 관리자 로그인  
  
    -   TDE(투명한 데이터 암호화)를 사용하도록 설정할 수 있는 기타 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인 또는 기타 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 암호화 기능  
  
     자격 증명과 로그인은 일대일로 매핑됩니다. 즉 각 로그인에는 고유한 자격 증명이 있어야 합니다.  
  
     다음과 같이 아래 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 스크립트를 수정합니다.  
  
    -   Azure Key Vault를 가리키도록 `IDENTITY` 인수(`ContosoDevKeyVault`)를 편집합니다.
        - **전역 Azure**를 사용하는 경우 `IDENTITY` 인수를 파트 2의 Azure Key Vault 이름으로 바꿉니다.
        - **프라이빗 Azure 클라우드** (예: Azure Government, Azure China 또는 Azure Germany)를 사용하는 경우는 `IDENTITY` 인수를 파트 2의 3단계에서 반환된 자격 증명 모음 URI로 바꿉니다. 자격 증명 모음 URI에 "https://"를 포함하지 마세요.   
    -   `SECRET` 인수의 첫 번째 부분을 1부의 Azure Active Directory **클라이언트 ID** 로 바꿉니다. 이 예제에서 **클라이언트 ID** 는 `EF5C8E094D2A4A769998D93440D8115D`입니다.  
  
        > [!IMPORTANT]  
        >  **클라이언트 ID**에서 하이픈을 제거해야 합니다.  
  
    -   `SECRET` 인수의 두 번째 부분을 파트 1의 **클라이언트 암호** 를 사용하여 완성합니다. 이 예제에서 파트 1의 **클라이언트 암호** 는 `Replace-With-AAD-Client-Secret`입니다. `SECRET` 인수의 최종 문자열은 *하이픈 없는*문자 및 숫자의 긴 시퀀스가 됩니다.  
  
    ```sql  
    USE master;  
    CREATE CREDENTIAL sysadmin_ekm_cred   
        WITH IDENTITY = 'ContosoDevKeyVault', -- for public Azure
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.usgovcloudapi.net', -- for Azure Government
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.azure.cn', -- for Azure China
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.microsoftazure.de', -- for Azure Germany   
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DReplace-With-AAD-Client-Secret'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;  
  
    -- Add the credential to the SQL Server administrator's domain login   
    ALTER LOGIN [<domain>\<login>]  
    ADD CREDENTIAL sysadmin_ekm_cred;  
    ```  
  
     **CREATE CREDENTIAL** 인수에 대한 변수 사용과 클라이언트 ID에서 하이픈을 프로그래밍 방식으로 제거하는 예는 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)을 참조하세요.  
  
5.  **Azure 주요 자격 증명 모음 키 열기 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**  
  
     2부에 설명한 대로 비대칭 키를 가져온 경우 다음 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 스크립트에서 키 이름을 제공하여 키를 엽니다.  
  
    -   `CONTOSO_KEY`를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 사용하려는 키 이름으로 바꿉니다.  
  
    -   `ContosoRSAKey0` 을 Azure 주요 자격 증명 모음의 키 이름으로 바꿉니다.  
  
    ```sql  
    CREATE ASYMMETRIC KEY CONTOSO_KEY   
    FROM PROVIDER [AzureKeyVault_EKM_Prov]  
    WITH PROVIDER_KEY_NAME = 'ContosoRSAKey0',  
    CREATION_DISPOSITION = OPEN_EXISTING;  
    ```  
## <a name="next-step"></a>다음 단계  
  
이제 기본 구성을 완료했으므로 [SQL 암호화 기능을 통해 SQL Server 커넥터 사용](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)방법을 참조하세요.   
  
## <a name="see-also"></a>참고 항목  
 [Azure 키 자격 증명 모음을 사용한 확장 가능 키 관리](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)   
[SQL Server 커넥터 유지 관리 및 문제 해결](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)
