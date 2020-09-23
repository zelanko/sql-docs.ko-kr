---
title: Azure Key Vault를 사용하여 TDE(투명한 데이터 암호화) 확장 가능 키 관리 설정
description: Azure Key Vault용 SQL Server 커넥터를 설치하고 구성합니다.
ms.custom: seo-lt-2019
ms.date: 08/12/2020
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Extensible Key Management
- EKM, with key vault setup
- SQL Server Connector, setup
- SQL Server Connector
ms.assetid: c1f29c27-5168-48cb-b649-7029e4816906
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: e5b18c46f602d24339c092b8f3e622b2a915baeb
ms.sourcegitcommit: f7c9e562d6048f89d203d71685ba86f127d8d241
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2020
ms.locfileid: "90042888"
---
# <a name="set-up-sql-server-tde-extensible-key-management-by-using-azure-key-vault"></a>Azure Key Vault를 사용하여 SQL Server TDE 확장 가능 키 관리 설정

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

이 문서에서는 Azure Key Vault용 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터를 설치 및 구성합니다.  
  
## <a name="prerequisites"></a>필수 구성 요소

SQL Server 인스턴스에서 Azure Key Vault를 사용하기 전에 다음 필수 조건을 충족해야 합니다.  
  
- Azure 구독이 있어야 합니다.
  
- [Azure PowerShell 버전 5.2.0 이상](https://azure.microsoft.com/documentation/articles/powershell-install-configure/)을 설치합니다.  

- Azure AD(Azure Active Directory) 인스턴스를 만듭니다.

- [Azure Key Vault를 사용한 EKM(SQL Server)](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)을 검토하여 Azure Key Vault를 사용하는 EKM(확장 가능 키 관리) 스토리지의 원리를 숙지합니다.  

- 실행 중인 SQL Server 버전을 기준으로 하는 Visual Studio C++ 재배포 가능 패키지 버전을 설치합니다.
  
  SQL Server 버전  | Visual Studio C++ 재배포 가능 패키지 버전
  ---------|---------
  2008, 2008 R2, 2012, 2014 | [Visual Studio 2013용 Visual C++ 재배포 가능 패키지](https://www.microsoft.com/download/details.aspx?id=40784)
  2016 | [Visual Studio 2015용 Visual C++ 재배포 가능 패키지](https://www.microsoft.com/download/details.aspx?id=48145)

## <a name="step-1-set-up-an-azure-ad-service-principal"></a>1단계: Azure AD 서비스 주체 설정

SQL Server 인스턴스에 Azure key vault에 대한 액세스 권한을 부여하려면 Azure AD에서 서비스 주체 계정이 필요합니다.  
  
1. [Azure Portal](https://ms.portal.azure.com/)에 로그인하고 다음 중 하나를 수행합니다.

    - **Azure Active Directory** 단추를 선택합니다.

      ![“Azure 서비스” 창 스크린샷](../../../relational-databases/security/encryption/media/ekm/ekm-part1-login-portal.png)

    - **더 많은 서비스**를 선택한 다음, **모든 서비스** 상자에 **Azure Active Directory**를 입력합니다.

      ![“모든 Azure 서비스” 창 스크린샷](../../../relational-databases/security/encryption/media/ekm/ekm-part1-select-aad.png)  

1. 다음을 수행하여 Azure Active Directory에 애플리케이션을 등록합니다. 자세한 단계별 지침을 보려면 [Azure Key Vault 블로그 게시물](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/)의 “Get an identity for the application”(애플리케이션의 ID 가져오기) 섹션을 참조하세요.

    a. **Azure Active Directory 개요** 창에서 **앱 등록**을 선택합니다.

    ![“Azure Active Directory 개요” 창 스크린샷](../../../relational-databases/security/encryption/media/ekm/ekm-part1-aad-app-register.png)

    b. **앱 등록** 창에서 **새 등록**을 선택합니다.

    ![“앱 등록” 창 스크린샷](../../../relational-databases/security/encryption/media/ekm/ekm-part1-aad-new-registration.png)  

    다. **애플리케이션 등록** 창에서 앱에 대한 사용자 이름을 입력하고 **등록**을 선택합니다.

    ![“애플리케이션 등록” 창 스크린샷](../../../relational-databases/security/encryption/media/ekm/ekm-part1-aad-register.png)

    d. 왼쪽 창에서 **인증서 및 암호**를 선택하고 **새 클라이언트 암호**를 선택합니다.

    ![“인증서 및 암호” 창 스크린샷](../../../relational-databases/security/encryption/media/ekm/ekm-part1-aad-certs-secrets.png)  

    e. **클라이언트 암호 추가**에서 설명과 적절한 만료 시간을 입력하고 **추가**를 선택합니다.

    ![“클라이언트 암호 추가” 섹션 스크린샷](../../../relational-databases/security/encryption/media/ekm/ekm-part1-aad-add-secret.png)  

    f. **인증서 및 암호** 창의 **“값”** 에서 SQL Server에 비대칭 키를 만드는 데 사용할 클라이언트 암호 값 옆에 있는 **복사** 단추를 선택합니다.

    ![“인증서 및 암호” 창 스크린샷](../../../relational-databases/security/encryption/media/ekm/ekm-part1-aad-new-secret.png)  

    g. 왼쪽 창에서 **개요**를 선택하고 **애플리케이션(클라이언트) ID** 상자에서 SQL Server에 비대칭 키를 만드는 데 사용할 값을 복사합니다.

    ![개요 창의 “애플리케이션(클라이언트) ID” 값 스크린샷](../../../relational-databases/security/encryption/media/ekm/ekm-part1-aad-appid.png)  

## <a name="step-2-create-a-key-vault"></a>2단계: 키 자격 증명 모음 만들기

키 자격 증명 모음을 만드는 데 사용할 방법을 선택합니다.

## <a name="azure-portal"></a>[Azure Portal](#tab/portal)

### <a name="create-a-key-vault-by-using-the-azure-portal"></a>Azure Portal을 사용하여 키 자격 증명 모음 만들기

Azure Portal을 사용하여 키 자격 증명 모음을 만든 다음, Azure AD 주체를 추가할 수 있습니다.

1. 리소스 그룹을 만듭니다.

   Azure Portal을 통해 만든 모든 Azure 리소스는 키 자격 증명 모음을 보관하기 위해 만든 리소스 그룹에 포함되어야 합니다. 이 예제의 리소스 이름은 *ContosoDevRG*입니다. 모든 키 자격 증명 모음 이름은 전역적으로 고유해야 하므로 고유한 리소스 그룹 및 키 자격 증명 모음 이름을 선택합니다.

   **리소스 그룹 만들기** 창의 **프로젝트 세부 정보**에서 값을 입력하고 **검토 + 만들기**를 선택합니다.

      ![“리소스 그룹 만들기” 창 스크린샷](../../../relational-databases/security/encryption/media/ekm/ekm-part2-create-resource-group.png)  

1. 키 자격 증명 모음을 만듭니다.

    **키 자격 증명 모음 만들기** 창에서 **기본 사항** 탭을 선택하고 적절한 값을 입력한 다음, **검토 + 만들기**를 선택합니다.

    ![“키 자격 증명 모음 만들기” 창 스크린샷](../../../relational-databases/security/encryption/media/ekm/ekm-part2-create-key-vault.png)  

1. **액세스 정책** 창에서 **액세스 정책 추가**를 선택합니다.

    ![“액세스 정책” 창에서 “액세스 정책 추가” 링크 스크린샷](../../../relational-databases/security/encryption/media/ekm/ekm-part2-add-access-policy.png)  

1. **액세스 정책 추가** 창에서 다음을 수행합니다.
  
    a. **템플릿에서 구성(선택 사항)** 드롭다운 목록에서 **키 관리**를 선택합니다.

    b. 왼쪽 창에서 **키 사용 권한** 탭을 선택하고 **가져오기**, **목록**, **키 래핑 해제**, **키 래핑** 확인란을 선택했는지 확인합니다.

    다. **추가**를 선택합니다.

    ![“액세스 정책 추가” 창 스크린샷](../../../relational-databases/security/encryption/media/ekm/ekm-part2-access-policy-permission.png)

1. 왼쪽 창에서 **보안 주체 선택** 탭을 선택하고 다음을 수행합니다.

    a. **보안 주체** 창의 **선택**에서 Azure AD 애플리케이션의 이름을 입력한 다음, 결과 목록에서 추가하려는 애플리케이션을 선택합니다.

    ![보안 주체 창의 애플리케이션 검색 상자 스크린샷](../../../relational-databases/security/encryption/media/ekm/ekm-part2-select-principal.png)  

    b. **선택** 단추를 선택하고 키 자격 증명 모음에 보안 주체를 추가합니다.

    ![보안 주체 창의 선택 단추 스크린샷](../../../relational-databases/security/encryption/media/ekm/ekm-part2-save-principal.png)

    다. 왼쪽 아래에서 **추가**를 선택하여 변경 내용을 저장합니다.

    ![“액세스 정책 추가” 창의 추가 단추 스크린샷](../../../relational-databases/security/encryption/media/ekm/ekm-part2-select-principal-new.png)

1. **키 자격 증명 모음** 창에서 **키**를 선택하고 키 자격 증명 모음 이름을 입력합니다. 키 유형 **RSA**와 RSA 키 크기 **2048**을 사용합니다. 활성화 날짜와 만료 날짜를 적절하게 설정하고 **사용하시겠습니까?** 를 **예**로 설정합니다.

   !["키 만들기" 창의 스크린샷](../../../relational-databases/security/encryption/media/ekm/ekm-part2-add-key-vault-key.png)  

1. **액세스 정책** 창에서 **저장**을 선택합니다.
  
   ![“액세스 정책 추가” 창의 저장 단추 스크린샷](../../../relational-databases/security/encryption/media/ekm/ekm-part2-save-access-policy.png)  

## <a name="powershell"></a>[PowerShell](#tab/powershell)

### <a name="create-a-key-vault-and-key-by-using-powershell"></a>PowerShell을 사용하여 키 자격 증명 모음 및 키 만들기

여기에서 만드는 키 자격 증명 모음 및 키는 SQL Server 데이터베이스 엔진에서 암호화 키 보호를 위해 사용됩니다.  
  
> [!IMPORTANT]
> 키 자격 증명 모음이 생성되는 구독은 Azure AD 서비스 주체를 만든 동일한 기본 Azure AD 인스턴스에 있어야 합니다. SQL Server 커넥터에 대한 서비스 주체를 만들기 위해 기본 인스턴스가 아닌 Azure AD 인스턴스를 사용하려는 경우에는 키 자격 증명 모음을 만들기 전에 Azure 계정에서 기본 Azure AD 인스턴스를 변경해야 합니다. 기본 Azure AD 인스턴스를 사용하려는 인스턴스로 변경하는 방법에 대한 자세한 내용은 [SQL Server 커넥터 유지 관리 및 문제 해결](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixB)에서 “질문과 대답” 섹션을 참조하세요.  
  
1. 다음 명령을 사용하여 [Azure PowerShell 5.2.0 이상](https://azure.microsoft.com/documentation/articles/powershell-install-configure/)을 설치하고 로그인합니다.  
  
    ```powershell  
    Connect-AzAccount  
    ```  
  
    문은 다음을 반환합니다.  
  
    ```console  
    Environment           : AzureCloud  
    Account               : <account_name>  
    TenantId              : <tenant_id>  
    SubscriptionId        : <subscription_id>  
    CurrentStorageAccount :  
    ```  
  
    > [!NOTE]  
    > 구독이 여러 개 있으며 자격 증명 모음에 사용할 하나의 구독만 지정하려면 `Get-AzSubscription`을 실행하여 구독을 표시하고, `Select-AzSubscription`을 실행하여 올바른 구독을 선택합니다. 그러지 않으면 PowerShell에서 기본적으로 구독을 하나 선택합니다.  
  
1. 리소스 그룹을 만듭니다.

    PowerShell을 통해 만든 모든 Azure 리소스는 키 자격 증명 모음을 보관하기 위해 만든 리소스 그룹에 포함되어야 합니다. 이 예제의 리소스 이름은 *ContosoDevRG*입니다. 모든 키 자격 증명 모음 이름은 전역적으로 고유해야 하므로 고유한 리소스 그룹 및 키 자격 증명 모음 이름을 선택합니다.  
  
    ```powershell  
    New-AzResourceGroup -Name ContosoDevRG -Location 'East Asia'  
    ```  
  
    문은 다음을 반환합니다.  
  
    ```console
    ResourceGroupName: ContosoDevRG  
    Location         : eastasia  
    ProvisioningState: Succeeded  
    Tags             :
    ResourceId       : /subscriptions/<subscription_id>/  
                        resourceGroups/ContosoDevRG  
    ```  
  
    > [!NOTE]
    > `-Location` 매개 변수의 경우 `Get-AzureLocation` 명령을 사용하여 이 예제에 있는 위치 이외의 위치를 지정하는 방법을 식별합니다. 자세한 내용을 보려면 **Get-Help Get-AzureLocation**을 입력합니다.  
  
1. 키 자격 증명 모음을 만듭니다.

    `New-AzKeyVault` cmdlet에는 리소스 그룹 이름, 주요 자격 증명 모음 이름, 지리적 위치가 필요합니다. 예를 들어 `ContosoEKMKeyVault`라고 이름이 지정된 키 자격 증명 모음의 경우 다음을 실행합니다.  
  
    ```powershell  
    New-AzKeyVault -VaultName 'ContosoEKMKeyVault' `  
       -ResourceGroupName 'ContosoDevRG' -Location 'East Asia'  
    ```  
  
    주요 자격 증명 모음의 이름을 기록합니다.  
  
    문은 다음을 반환합니다.

    ```console
    Vault Name                       : ContosoEKMKeyVault  
    Resource Group Name              : ContosoDevRG  
    Location                         : East Asia  
    ResourceId                       : /subscriptions/<subscription_id>/  
                                        resourceGroups/ContosoDevRG/providers/  
                                        Microsoft/KeyVault/vaults/ContosoEKMKeyVault  
    Vault URI: https://ContosoEKMKeyVault.vault.azure.net  
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
  
1. Azure AD 서비스 주체가 Azure Key Vault에 액세스할 수 있는 권한을 부여합니다.  
  
    다른 사용자 및 애플리케이션이 사용자의 주요 자격 증명 모음을 사용하도록 권한을 부여할 수 있습니다.  이 예제에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 권한을 부여하기 위해 [1단계: Azure AD 서비스 주체 설정](#step-1-set-up-an-azure-ad-service-principal)에서 만든 서비스 주체를 사용하세요.  
  
    > [!IMPORTANT]
    > Azure AD 서비스 주체는 키 자격 증명 모음에 대해 적어도 *get*, *list*,*wrapKey* 및 *unwrapKey* 권한이 있어야 합니다.  
  
    다음 명령에 표시된 것처럼 `ServicePrincipalName` 매개 변수에 대해 [1단계: Azure AD 서비스 주체 설정](#step-1-set-up-an-azure-ad-service-principal)의 **앱(클라이언트) ID**를 사용합니다. `Set-AzKeyVaultAccessPolicy`는 성공적으로 실행되는 경우 출력 없이 자동으로 실행됩니다.  
  
    ```powershell  
    Set-AzKeyVaultAccessPolicy -VaultName 'ContosoEKMKeyVault' `  
      -ServicePrincipalName 9A57CBC5-4C4C-40E2-B517-EA677 `  
      -PermissionsToKeys get, list, wrapKey, unwrapKey  
    ```  
  
    `Get-AzKeyVault` cmdlet을 호출하여 권한을 확인합니다. `Access Policies` 아래의 문 출력에 이 키 자격 증명 모음에 대한 액세스 권한이 다른 테넌트로 나열되는 Azure AD 애플리케이션 이름이 표시되어야 합니다.  
  
1. 키 자격 증명 모음에서 비대칭 키를 생성합니다. 이렇게 하려면 기존 키를 가져오거나 새 키를 만드는 두 가지 방법 중 하나를 사용할 수 있습니다.  

     > [!NOTE]
     > SQL Server는 2048비트 RSA 키만 지원합니다.

### <a name="best-practices"></a>모범 사례

빠른 키 복구를 보장하고 Azure 외부의 데이터에 액세스하려면 다음 모범 사례를 권장합니다.

- 로컬 HSM(하드웨어 보안 모듈) 디바이스에서 암호화 키를 로컬로 만듭니다. SQL Server에서 지원하도록 비대칭 RSA 2048 키를 사용해야 합니다.
- Azure Key Vault에 암호화 키를 가져옵니다. 이 프로세스는 다음 섹션에 설명되어 있습니다.
- Azure Key Vault에서 키를 처음 사용하기 전에 Azure Key Vault 키 백업을 수행합니다. 자세한 내용은 [Backup-AzureKeyVaultKey](/sql/relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault) 명령을 참조하세요.
- 키를 변경할 때마다(예: ACL, 태그 또는 키 특성 추가) 다른 Azure Key Vault 키 백업을 수행해야 합니다.

  > [!NOTE]
  > 키 백업 작업은 장소에 상관없이 저장할 수 있는 파일을 반환하는 Azure Key Vault 키 작업입니다.

### <a name="types-of-keys"></a>키의 유형

SQL Server와 작동할 Azure Key Vault에서 두 가지 유형의 키를 생성할 수 있습니다. 두 유형은 모두 비대칭 2048비트 RSA 키입니다.  
  
- **소프트웨어 보호**: 소프트웨어에서 처리되고 안전하게 암호화됩니다. 소프트웨어 보호된 키에 대한 작업은 Azure Virtual Machines에서 발생합니다. 프로덕션 배포에 사용되지 않는 키에 이 유형을 사용하는 것이 좋습니다.  

- **HSM 보호**: 추가 보안을 위해 하드웨어 보안 모듈에서 생성하고 보호합니다. 비용은 키 버전당 약 USD 1입니다.  
  
    > [!IMPORTANT]
    > SQL Server 커넥터에는 문자 a-z, A-Z, 0-9 및 하이픈(-)만 사용하고 26자 제한이 있습니다.
    > Azure Key Vault에서 동일한 키 이름의 다른 키 버전은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터에서 작동하지 않습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 사용하는 Azure Key Vault 키를 회전하려면 [SQL Server 커넥터 유지 관리 및 문제 해결](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)의 “A. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터에 대한 유지 관리 지침” 섹션에서 키 롤오버 단계를 참조하세요.  

### <a name="import-an-existing-key"></a>기존 키 가져오기
  
기존 2048비트 RSA 소프트웨어 보호된 키가 있는 경우 키를 Azure Key Vault에 업로드할 수 있습니다. 예를 들어 `C:\\` 드라이브에 저장된 .PFX 파일(이름: *softkey.pfx*)이 있고 Azure Key Vault에 업로드하려는 경우에는 다음 명령을 실행하여 PFX 파일에 암호 `12987553`에 대한 `securepfxpwd` 변수를 설정합니다.  
  
``` powershell  
$securepfxpwd = ConvertTo-SecureString -String '12987553' `  
  -AsPlainText -Force  
```  

다음 명령을 실행하여 PFX 파일에서 키를 가져올 수 있습니다. 이렇게 하면 Key Vault 서비스에서 하드웨어(권장)로부터 키가 보호됩니다.  
  
``` powershell  
    Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' `  
      -Name 'ContosoFirstKey' -KeyFilePath 'c:\softkey.pfx' `  
      -KeyFilePassword $securepfxpwd $securepfxpwd  -Destination 'HSM'  
```  

> [!CAUTION]
> 비대칭 키를 가져오면 관리자가 키 에스크로 시스템에 키를 위탁할 수 있으므로 비대칭 키를 가져오는 것은 프로덕션 시나리오에 매우 좋습니다. 프라이빗 키는 자격 증명 모음을 벗어날 수 없으므로 비대칭 키를 자격 증명 모음에서 만든 경우에는 키를 위탁할 수 없습니다. 중요한 데이터를 보호하는 데 사용되는 키는 위탁해야 합니다. 비대칭 키가 손실되는 경우 데이터가 영구적으로 손실됩니다.  

### <a name="create-a-new-key"></a>새 키 만들기

또는 Azure Key Vault에 직접 새 암호화 키를 만들고 소프트웨어 보호 또는 HSM 보호를 설정할 수 있습니다.  이 예제에서는 `Add-AzureKeyVaultKey` cmdlet을 사용하여 소프트웨어 보호 키를 만들어 봅니다.  

``` powershell  
Add-AzureKeyVaultKey -VaultName 'ContosoEKMKeyVault' `  
  -Name 'ContosoRSAKey0' -Destination 'Software'  
```  
  
문은 다음을 반환합니다.  
  
```console
Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes  
Key        :  {"kid":"https:contosoekmkeyvault.azure.net/keys/  
                ContosoRSAKey0/<guid>","dty":"RSA:,"key_ops": ...  
VaultName  : contosodevkeyvault  
Name       : contosoRSAKey0  
Version    : <guid>  
Id         : https://contosoekmkeyvault.vault.azure.net:443/  
              keys/ContosoRSAKey0/<guid>  
```  

> [!IMPORTANT]
> 키 자격 증명 모음은 동일한 이름이 지정된 키의 여러 버전을 지원하지만 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터에서 사용할 키는 버전이 지정되거나 여기저기 사용해서는 안 됩니다. 관리자가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 암호화에 사용된 키를 다른 곳에 사용하려는 경우, 키 자격 증명 모음에서 다른 이름으로 새 키를 만들어 DEK를 암호화하는 데 사용해야 합니다.  

---

## <a name="step-3-install-the-ssnoversion-connector"></a>3단계: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터 설치

[Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/p/?LinkId=521700)에서 SQL Server 커넥터를 다운로드합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 컴퓨터의 관리자가 다운로드해야 합니다.  

> [!NOTE]
> - SQL Server 커넥터 버전 1.0.0.440 이하 버전은 대체되었으며 더 이상 프로덕션 환경에서 지원되지 않고 [SQL Server 커넥터 유지 관리 및 문제 해결](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md) 페이지의 [SQL Server 커넥터 업그레이드](sql-server-connector-maintenance-troubleshooting.md#upgrade-of--connector) 지침을 사용하지 않습니다.
> - 1\.0.3.0 버전부터 SQL Server 커넥터는 문제를 해결하기 위해 Windows 이벤트 로그에 관련 오류 메시지를 보고합니다.
> - 1\.0.4.0 버전부터 Azure 중국, Azure 독일, Azure Government 등 프라이빗 Azure 클라우드가 지원됩니다.
> - 1\.0.5.0 버전의 경우 지문 알고리즘 측면에서 호환성이 손상되는 변경이 있습니다. 1\.0.5.0으로 업그레이드한 후 데이터베이스 복원 실패가 발생할 수 있습니다. 자세한 내용은 [기술 자료 문서 447099](https://support.microsoft.com/help/4470999/db-backup-problems-to-sql-server-connector-for-azure-1-0-5-0)를 참조하세요.
> - **1.0.7.0 버전부터 SQL Server 커넥터는 메시지 필터링 및 네트워크 요청 다시 시도 논리를 지원합니다.**
  
  ![SQL Server 커넥터 설치 마법사 스크린샷](../../../relational-databases/security/encryption/media/ekm/ekm-connector-install.png)  
  
기본적으로 커넥터는 C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault에 설치됩니다. 이 위치는 설치 중 변경할 수 있습니다. 변경하는 경우 다음 섹션에서 스크립트를 조정합니다.  
  
커넥터에 대한 인터페이스가 없는데도 성공적으로 설치되는 경우에는 머신에 *Microsoft.AzureKeyVaultService.EKM.dll*이 설치되어 있기 때문입니다. 이 어셈블리는 `CREATE CRYPTOGRAPHIC PROVIDER` 문을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 등록해야 하는 암호화 EKM 공급자 DLL입니다.  
  
SQL Server 커넥터를 설치하면 원할 경우 SQL Server 암호화를 위한 샘플 스크립트를 다운로드할 수도 있습니다.  
  
SQL Server 커넥터에 대한 오류 코드 설명, 구성 설정 또는 유지 관리 작업을 보려면 다음을 참조하세요.  
  
- [A. SQL Server 커넥터에 대한 유지 관리 지침](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixA)  
- [C. SQL Server 커넥터에 대한 오류 코드 설명](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixC)  
  
## <a name="step-4-configure-ssnoversion"></a>4단계: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성  

이 섹션의 각 작업에 필요한 최소 권한 수준에 대한 정보를 보려면 [B. 질문과 대답](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixB)을 참조하세요.  
  
1. *sqlcmd.exe*를 실행하거나 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Studio를 엽니다.  
  
1. 다음 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 스크립트를 실행하여 EKM을 사용하도록 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 구성합니다.  
  
    ```sql  
    -- Enable advanced options.  
    USE master;  
    GO  

    EXEC sp_configure 'show advanced options', 1;  
    GO  
    RECONFIGURE;  
    GO  

    -- Enable EKM provider  
    EXEC sp_configure 'EKM provider enabled', 1;  
    GO  
    RECONFIGURE;  
    ```  
  
1. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터를 EKM 공급자로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 등록합니다.  
  
    Azure Key Vault에 대한 EKM 공급자인 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터를 사용하여 암호화 공급자를 만듭니다.
    이 예제에서는 공급자 이름이 `AzureKeyVault_EKM`입니다.  
  
    ```sql  
    CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM
    FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';  
    GO  
    ```  

    > [!NOTE]
    > 파일 경로 길이는 256자를 초과할 수 없습니다.  
  
1. 키 자격 증명 모음을 사용하기 위해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인에 대해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 자격 증명을 설정합니다.  
  
    키 자격 증명 모음에서 키를 사용하여 암호화를 수행할 각 로그인에 자격 증명을 추가해야 합니다. 여기에는 다음이 포함될 수 있습니다.  
  
    - 키 자격 증명 모음을 사용하여 암호화 시나리오를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]설정 및 관리하는 관리자 로그인[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
    - TDE 또는 기타 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 암호화 기능을 사용하도록 설정할 수 있는 다른 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인  
  
    자격 증명과 로그인은 일대일로 매핑됩니다. 즉 각 로그인에는 고유한 자격 증명이 있어야 합니다.  
  
    다음과 같은 방법으로 이 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 스크립트를 수정합니다.  
  
    - Azure Key Vault를 가리키도록 `IDENTITY` 인수(`ContosoEKMKeyVault`)를 편집합니다.
      - ‘전역 Azure’를 사용하는 경우 `IDENTITY` 인수를 [2단계: 키 자격 증명 모음 만들기](#step-2-create-a-key-vault)의 Azure Key Vault 이름으로 바꿉니다.
      - ‘프라이빗 Azure 클라우드’(예: Azure Government, Azure 중국 21Vianet 또는 Azure 독일)를 사용하는 경우 `IDENTITY` 인수를 [PowerShell을 사용하여 키 자격 증명 모음 및 키 만들기](#create-a-key-vault-and-key-by-using-powershell) 섹션의 3단계에 반환된 자격 증명 URI로 바꿉니다. 자격 증명 모음 URI에 “https://”를 포함하지 마세요.
    - `SECRET` 인수의 첫 번째 부분을 [1단계: Azure AD 서비스 주체 설정](#step-1-set-up-an-azure-ad-service-principal)의 Azure Active Directory 클라이언트 ID로 바꿉니다. 이 예제에서 **클라이언트 ID**는 `9A57CBC54C4C40E2B517EA677E0EFA00`입니다.  
  
      > [!IMPORTANT]
      > 앱(클라이언트) ID에서 하이픈을 제거해야 합니다.  
  
    - [1단계: Azure AD 서비스 주체 설정](#step-1-set-up-an-azure-ad-service-principal)의 **클라이언트 암호**를 사용하여 `SECRET` 인수의 두 번째 부분을 완성합니다.  이 예제에서 클라이언트 암호는 `08:k?[:XEZFxcwIPvVVZhTjHWXm7w1?m`입니다. `SECRET` 인수의 최종 문자열은 하이픈 없는 문자 및 숫자의 긴 시퀀스가 됩니다.  
  
    ```sql  
    USE master;  
    CREATE CREDENTIAL sysadmin_ekm_cred
        WITH IDENTITY = 'ContosoEKMKeyVault',                            -- for public Azure
        -- WITH IDENTITY = 'ContosoEKMKeyVault.vault.usgovcloudapi.net', -- for Azure Government
        -- WITH IDENTITY = 'ContosoEKMKeyVault.vault.azure.cn',          -- for Azure China 21Vianet
        -- WITH IDENTITY = 'ContosoEKMKeyVault.vault.microsoftazure.de', -- for Azure Germany
               --<----Application (Client) ID ---><--Azure AD app (Client) ID secret-->
        SECRET = '9A57CBC54C4C40E2B517EA677E0EFA0008:k?[:XEZFxcwIPvVVZhTjHWXm7w1?m'
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM;  
  
    -- Add the credential to the SQL Server administrator's domain login
    ALTER LOGIN [<domain>\<login>]  
    ADD CREDENTIAL sysadmin_ekm_cred;  
    ```  
  
    `CREATE CREDENTIAL` 인수에 대한 변수 사용과 클라이언트 ID에서 하이픈을 프로그래밍 방식으로 제거하는 예는 [CREATE CREDENTIAL&#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)을 참조하세요.  
  
1. SQL Server 인스턴스에서 Azure Key Vault 키를 엽니다.  

    [2단계: Key Vault 만들기](#step-2-create-a-key-vault)에서 설명한 대로 새 키를 만들었거나 비대칭 키를 가져온 경우 키를 열어야 합니다. 다음 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 스크립트에서 키 이름을 제공하여 키를 엽니다.  
  
    - `EKMSampleASYKey`를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 사용하려는 키 이름으로 바꿉니다.  
    - `ContosoRSAKey0`을 Azure Key Vault의 키 이름으로 바꿉니다.  
  
    ```sql  
    CREATE ASYMMETRIC KEY EKMSampleASYKey
    FROM PROVIDER [AzureKeyVault_EKM]  
    WITH PROVIDER_KEY_NAME = 'ContosoRSAKey0',  
    CREATION_DISPOSITION = OPEN_EXISTING;  
    ```  

1. 이전 단계에서 만든 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 비대칭 키를 사용하여 새 로그인을 만듭니다.

     ```sql  
    --Create a Login that will associate the asymmetric key to this login
    CREATE LOGIN TDE_Login
    FROM ASYMMETRIC KEY EKMSampleASYKey;
    ```  

1. SQL Server의 비대칭 키에서 새 로그인을 만듭니다. 4단계에서 자격 증명 매핑을 삭제합니다. 자격 증명을 새 로그인에 매핑할 수 있도록 SQL Server를 구성합니다.

     ```sql  
    --Now drop the credential mapping from the original association
    ALTER LOGIN [<domain>\<login>]
    DROP CREDENTIAL sysadmin_ekm_cred;
    ```

1. 새 로그인을 변경하고 EKM 자격 증명을 새 로그인에 매핑합니다.

     ```sql  
    --Now drop the credential mapping from the original association
    ALTER LOGIN TDE_Login
    ADD CREDENTIAL sysadmin_ekm_cred;
    ```  

1. Azure Key Vault 키를 사용하여 암호화되는 테스트 데이터베이스를 만듭니다.

     ```sql
    --Create a test database that will be encrypted with the Azure key vault key
    CREATE DATABASE TestTDE
    ```  

1. 비대칭 키(EKMSampleASYKey)를 사용하여 데이터베이스 암호화 키를 만듭니다.

    ```sql  
    --Create an ENCRYPTION KEY using the ASYMMETRIC KEY (EKMSampleASYKey)
    CREATE DATABASE ENCRYPTION KEY
    WITH ALGORITHM = AES_256
    ENCRYPTION BY SERVER ASYMMETRIC KEY EKMSampleASYKey;
    ```
  
1. 테스트 데이터베이스를 암호화합니다. 암호화를 설정하여 TDE를 사용하도록 설정합니다.

     ```sql  
    --Enable TDE by setting ENCRYPTION ON
    ALTER DATABASE TestTDE
    SET ENCRYPTION ON;  
     ```  

1. 테스트 개체를 정리합니다. 이 테스트 스크립트에서 만든 개체를 모두 삭제합니다.

    ```sql  
    -- CLEAN UP
    USE Master
    ALTER DATABASE [TestTDE] SET SINGLE_USER WITH ROLLBACK IMMEDIATE
    DROP DATABASE [TestTDE]

    ALTER LOGIN [TDE_Login] DROP CREDENTIAL [sysadmin_ekm_cred]
    DROP LOGIN [TDE_Login]

    DROP CREDENTIAL [sysadmin_ekm_cred]  

    USE MASTER
    DROP ASYMMETRIC KEY [EKMSampleASYKey]
    DROP CRYPTOGRAPHIC PROVIDER [AzureKeyVault_EKM]
    ```  

샘플 스크립트는 [SQL Server 투명한 데이터 암호화 및 Azure Key Vault를 사용한 확장 가능 키 관리](https://techcommunity.microsoft.com/t5/sql-server/intro-sql-server-transparent-data-encryption-and-extensible-key/ba-p/1427549) 블로그를 참조하세요.

## <a name="next-steps"></a>다음 단계  
  
이제 기본 구성을 완료했으므로 [SQL 암호화 기능을 통해 SQL Server 커넥터 사용](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)을 참조하세요.
  
## <a name="see-also"></a>참고 항목  

- [Azure Key Vault를 사용하여 확장 가능 키 관리](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)
- [SQL Server 커넥터 유지 관리 및 문제 해결](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)
