---
title: Always Encrypted용 열 마스터 키 만들기 및 저장
description: 키 저장소를 선택하고 SQL Server Always Encrypted용 열 마스터 키를 만드는 방법에 대해 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 10/31/2019
ms.prod: sql
ms.prod_service: security, sql-database"
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
ms.assetid: 856e8061-c604-4ce4-b89f-a11876dd6c88
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c9a0dfad97e37325c0990bb8c1786a63a5bf897a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479364"
---
# <a name="create-and-store-column-master-keys-for-always-encrypted"></a>Always Encrypted용 열 마스터 키 만들기 및 저장
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]

*열 마스터 키* 는 상시 암호화에서 열 암호화 키를 암호화하는 데 사용되는 키를 보호하는 키입니다. 열 마스터 키는 신뢰할 수 있는 키 저장소에 저장되어야 하며 데이터 암호화 또는 암호 해독이 필요한 애플리케이션, 그리고 상시 암호화 구성 및 상시 암호화 키 관리용 도구에 액세스할 수 있어야 합니다.

이 문서에서는 상시 암호화를 위한 키 저장소 선택 및 열 마스터 키 만들기에 대한 세부 정보를 제공합니다. 자세한 내용은 [상시 암호화를 위한 키 관리 개요](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)를 참조하세요.

## <a name="selecting-a-key-store-for-your-column-master-key"></a>열 마스터 키에 대한 키 저장소 선택

상시 암호화는 여러 키 저장소를 지원하여 상시 암호화 열 마스터 키를 저장할 수 있습니다. 지원되는 키 저장소는 사용 중인 드라이버 및 버전에 따라 달라집니다.

키 저장소는 크게 두 가지 범주( *로컬 키 저장소* 및 *중앙 집중식 키 저장소*)로 나뉩니다.

###  <a name="local-or-centralized-key-store"></a>로컬 또는 중앙 집중식 키 저장소

* **로컬 키 저장소** - 로컬 키 저장소가 포함된 컴퓨터의 애플리케이션에서만 사용할 수 있습니다. 즉, 키 저장소 및 키를 애플리케이션이 실행 중인 각 컴퓨터에 복제해야 합니다. 로컬 키 저장소의 예는 Windows 인증서 저장소입니다. 로컬 키 저장소를 사용할 경우 애플리케이션을 호스트하는 각 컴퓨터에 키 저장소가 있고, 애플리케이션에서 상시 암호화를 사용하여 보호된 데이터에 액세스할 때 필요한 열 마스터 키가 컴퓨터에 있는지 확인해야 합니다. 열 마스터 키를 처음 프로비전하거나 키를 변경(순환)하는 경우 애플리케이션을 호스트하는 모든 컴퓨터에 키가 배포되었는지 확인해야 합니다.

* **중앙 집중식 키 저장소** - 여러 컴퓨터의 애플리케이션에 제공합니다. 중앙 집중식 키 저장소의 예로는 [Azure 주요 자격 증명 모음](https://azure.microsoft.com/services/key-vault/)이 있습니다. 중앙 집중식 키 저장소는 여러 컴퓨터에서 열 마스터 키의 복사본을 여러 개 관리할 필요가 없으므로 일반적으로 키 관리가 더 쉬워집니다. 애플리케이션이 중앙 집중식 키 저장소에 연결하도록 구성되어 있어야 합니다.

### <a name="which-key-stores-are-supported-in-always-encrypted-enabled-client-drivers"></a>상시 암호화 지원 클라이언트 드라이버에서 지원하는 키 저장소

상시 암호화 지원 클라이언트 드라이버는 기본적으로 상시 암호화를 클라이언트 애플리케이션에 통합할 수 있는 SQL Server 클라이언트 드라이버입니다. 상시 암호화 지원 드라이버에는 인기 있는 키 저장소에 대한 기본 제공 공급자가 몇 가지 포함되어 있습니다. 일부 드라이버를 사용하면 사용자 지정 열 마스터 키 저장소 공급자를 구현 및 등록할 수 있으므로 지원하는 기본 제공 공급자가 없어도 모든 키 저장소를 사용할 수 있습니다. 기본 제공 공급자와 사용자 지정 공급자 중 사용할 공급자를 결정할 때는 기본 제공 공급자를 사용하는 것이 일반적으로 애플리케이션을 더 적게 변경한다는 사실을 고려하세요. 경우에 따라 데이터베이스 연결 문자열만 변경할 때도 있습니다.

사용 가능한 기본 제공 공급자는 선택된 드라이버, 드라이버 버전 및 운영 체제에 따라 달라집니다.  특정 드라이버에서 기본적으로 지원하는 키 저장소와 사용 중인 드라이버가 사용자 지정 키 저장소 공급자를 지원하는지 여부는 Always Encrypted 설명서에서 [Always Encrypted를 사용하여 애플리케이션 개발](always-encrypted-client-development.md)을 참조하세요.

### <a name="which-key-stores-are-supported-in-sql-tools"></a>SQL 도구에서 지원되는 키 저장소는 무엇입니까?
SQL Server Management Studio 및 SqlServer PowerShell 모듈은 CNG(Cryptography Next Generation) API 또는 CAPI(암호화 API)를 제공하는 Azure Key Vault, Windows 인증서 저장소 및 키 저장소에 저장된 열 마스터 키만 지원합니다. 

## <a name="creating-column-master-keys-in-windows-certificate-store"></a>Windows 인증서 저장소에서 열 마스터 키 만들기    

열 마스터 키는 Windows 인증서 저장소에 저장된 인증서일 수 있습니다. Always Encrypted 지원 드라이버에서는 만료 날짜 또는 인증 기관 체인을 확인하지 않습니다. 인증서는 단지 퍼블릭 키와 프라이빗 키로 구성된 키 쌍으로만 사용됩니다.

올바른 열 마스터 키가 되려면 인증서가 다음 조건을 만족해야 합니다.
* X.509 인증서여야 합니다.
* 두 인증서 저장 위치인 *로컬 컴퓨터* 또는 *현재 사용자* 중 하나에 저장되어야 합니다. 로컬 컴퓨터 인증서 저장소 위치에 인증서를 만들려면 대상 컴퓨터의 관리자여야 합니다.
* 프라이빗 키를 포함해야 합니다. 인증서의 권장되는 키 길이는 2048비트 이상입니다.
* 키 교환을 위해 만들어져야 합니다.


여러 가지 방법으로 올바른 열 마스터 키인 인증서를 만들 수 있지만 자체 서명된 인증서를 만드는 것이 가장 간단합니다.


### <a name="create-a-self-signed-certificate-using-powershell"></a>PowerShell을 사용하여 자체 서명된 인증서 만들기

[New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate) cmdlet을 사용하여 자체 서명된 인증서를 만듭니다. 다음 예제에서는 상시 암호화에 대한 열 마스터 키로 사용할 수 있는 인증서를 생성하는 방법을 보여 줍니다.

```
# New-SelfSignedCertificate is a Windows PowerShell cmdlet that creates a self-signed certificate. The below examples show how to generate a certificate that can be used as a column master key for Always Encrypted.
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation Cert:CurrentUser\My -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage KeyEncipherment -KeySpec KeyExchange -KeyLength 2048 

# To create a certificate in the local machine certificate store location you need to run the cmdlet as an administrator.
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation Cert:LocalMachine\My -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage KeyEncipherment -KeySpec KeyExchange -KeyLength 2048
```

### <a name="create-a-self-signed-certificate-using-sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio)를 사용하여 자체 서명된 인증서 만들기

자세한 내용은 [SQL Server Management Studio를 사용하여 Always Encrypted 키 프로비전](configure-always-encrypted-keys-using-ssms.md)을 참조하세요.
SSMS를 사용하고 Windows 인증서 저장소에 상시 암호화 키를 저장하는 단계별 자습서는 [상시 암호화 마법사 자습서(Windows 인증서 저장소)](/azure/azure-sql/database/always-encrypted-certificate-store-configure)를 참조하세요.


### <a name="making-certificates-available-to-applications-and-users"></a>애플리케이션 및 사용자가 인증서를 사용할 수 있도록 설정

열 마스터 키가 *로컬 컴퓨터* 인증서 저장소 위치에 저장된 인증서인 경우 프라이빗 키가 있는 인증서를 내보내고 암호화된 열에 저장된 데이터를 암호화 또는 암호 해독할 애플리케이션을 호스트하는 모든 컴퓨터 또는 상시 암호화 구성 및 상시 암호화 키 관리용 도구로 인증서를 가져와야 합니다. 또한 인증서를 열 마스터 키로 사용할 수 있도록 로컬 컴퓨터 인증서 저장소 위치에 저장된 인증서에 대해 읽기 권한을 각 사용자에게 부여해야 합니다.

열 마스터 키가 *현재 사용자* 인증서 저장소 위치에 저장된 인증서인 경우 프라이빗 키가 있는 인증서를 내보내고 암호화된 열에 저장된 데이터를 암호화 또는 암호 해독할 애플리케이션을 실행 중인 모든 사용자 계정의 현재 사용자 인증서 저장소 위치 또는 상시 암호화 구성 및 상시 암호화 키 관리용 도구(이러한 애플리케이션/도구가 포함된 모든 컴퓨터에서)로 인증서를 가져와야 합니다. 사용 권한 구성이 필요하지 않습니다. 사용자는 컴퓨터에 로그온한 다음 현재 사용자 인증서 저장소 위치에 있는 모든 인증서에 액세스할 수 있습니다.

#### <a name="using-powershell"></a>PowerShell 사용
[Import-PfxCertificate](/powershell/module/pkiclient/import-pfxcertificate) 및 [Export-PfxCertificate](/powershell/module/pkiclient/export-pfxcertificate) cmdlet을 사용하여 인증서를 가져오고 내보낼 수 있습니다.

#### <a name="using-microsoft-management-console"></a>Microsoft Management Console 사용 

사용자에게 로컬 컴퓨터 인증서 저장소 위치에 저장된 인증서에 대한 *읽기* 권한을 부여하려면 다음 단계를 따릅니다.

1.  명령 프롬프트를 열고 **mmc** 를 입력합니다.
2.  MMC 콘솔의 **파일** 메뉴에서 **스냅인 추가/제거** 를 클릭합니다.
3.  **스냅인 추가/제거** 대화 상자에서 **추가** 를 클릭합니다.
4.  **독립 실행형 스냅인 추가** 대화 상자에서 **인증서** 를 클릭하고 **추가** 를 클릭합니다.
5.  **인증서 스냅인** 대화 상자에서 **컴퓨터 계정** 을 클릭한 다음 **마침** 을 클릭합니다.
6.  **독립 실행형 스냅인 추가** 대화 상자에서 **닫기** 를 클릭합니다.
7.  **스냅인 추가/제거** 대화 상자에서 **확인** 을 클릭합니다.
8.  **인증서** 스냅인의 **인증서 &gt; 개인** 폴더에서 인증서를 찾은 다음 인증서를 마우스 오른쪽 단추로 클릭하고 **모든 태스크** 를 가리킨 다음 **프라이빗 키 관리** 를 클릭합니다.
9.  필요한 경우 **보안** 대화 상자에서 사용자 계정에 대한 읽기 권한을 추가합니다.

## <a name="creating-column-master-keys-in-azure-key-vault"></a>Azure 주요 자격 증명 모음에서 열 마스터 키 만들기

Azure 주요 자격 증명 모음은 암호화 키 및 암호를 보호하고 상시 암호화에 대한 열 마스터 키를 저장하는 편리한 옵션입니다(특히 애플리케이션이 Azure에서 호스트되는 경우). [Azure 주요 자격 증명 모음](/azure/key-vault/general/overview)에서 키를 만들려면 [Azure 구독](https://azure.microsoft.com/free/) 및 Azure 주요 자격 증명 모음이 필요합니다.

### <a name="using-powershell"></a>PowerShell 사용

다음 예제에서는 새 Azure 주요 자격 증명 모음 및 키를 만들고 원하는 사용자에게 권한을 부여합니다.

```
# Create a column master key in Azure Key Vault.
Connect-AzAccount
$SubscriptionId = "<Azure subscription ID>"
$resourceGroup = "<resource group name>"
$azureLocation = "<key vault location>"
$akvName = "<key vault name>"
$akvKeyName = "<column master key name>"
$azureCtx = Set-AzContext -SubscriptionId $SubscriptionId # Sets the context for the below cmdlets to the specified subscription.
New-AzResourceGroup -Name $resourceGroup -Location $azureLocation # Creates a new resource group - skip, if you desire group already exists.
New-AzKeyVault -VaultName $akvName -ResourceGroupName $resourceGroup -Location $azureLocation -SKU premium # Creates a new key vault - skip if your vault already exists.
Set-AzKeyVaultAccessPolicy -VaultName $akvName -ResourceGroupName $resourceGroup -PermissionsToKeys get, create, delete, list, update, import, backup, restore, wrapKey, unwrapKey, sign, verify -UserPrincipalName $azureCtx.Account
$akvKey = Add-AzKeyVaultKey -VaultName $akvName -Name $akvKeyName -Destination HSM
```

### <a name="using-sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio) 사용

SSMS를 사용하여 Azure Key Vault에서 열 마스터 키를 만드는 방법에 대한 자세한 내용은 [SQL Server Management Studio를 사용하여 Always Encrypted 키 프로비전](configure-always-encrypted-keys-using-ssms.md)을 참조하세요.
SSMS를 사용하고 Azure 주요 자격 증명 모음에 상시 암호화 키를 저장하는 단계별 자습서는 [상시 암호화 마법사 자습서(Azure 주요 자격 증명 모음)](/azure/azure-sql/database/always-encrypted-azure-key-vault-configure)를 참조하세요.

### <a name="making-azure-key-vault-keys-available-to-applications-and-users"></a>애플리케이션 및 사용자가 Azure 주요 자격 증명 모음을 사용할 수 있도록 설정

Azure Key Vault 키를 열 마스터 키로 사용하는 경우 애플리케이션에서 Azure를 인증해야 하며 애플리케이션 ID에는 주요 자격 증명 모음에 대한 *get*, *unwrapKey* 및 *verify* 권한이 있어야 합니다. 

Azure 주요 자격 증명 모음에 저장된 열 마스터 키를 사용하여 보호된 열 암호화 키를 프로비전하려면 *get*, *unwrapKey*, *wrapKey*, *sign* 및 *verify* 권한이 필요합니다. 또한 Azure 주요 자격 증명 모음에서 새 키를 생성하려면 *create* 권한이 필요하고, 주요 자격 증명 모음 콘텐츠를 나열하려면 *list* 권한이 필요합니다.

#### <a name="using-powershell"></a>PowerShell 사용

사용자와 애플리케이션이 Azure Key Vault의 실제 키에 액세스할 수 있게 하려면 자격 증명 모음 액세스 정책([Set-AzKeyVaultAccessPolicy](/powershell/module/az.keyvault/set-azkeyvaultaccesspolicy))을 설정해야 합니다.

```
$vaultName = "<vault name>"
$resourceGroupName = "<resource group name>"
$userPrincipalName = "<user to grant access to>"
$clientId = "<client Id>"

# grant users permissions to the keys:
Set-AzKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $resourceGroupName -PermissionsToKeys create,get,wrapKey,unwrapKey,sign,verify,list -UserPrincipalName $userPrincipalName
# grant applications permissions to the keys:
Set-AzKeyVaultAccessPolicy  -VaultName $vaultName  -ResourceGroupName $resourceGroupName -ServicePrincipalName $clientId -PermissionsToKeys get,wrapKey,unwrapKey,sign,verify,list
```

## <a name="creating-column-master-keys-in-hardware-security-modules-using-cng"></a>CNG를 사용하여 하드웨어 보안 모듈에서 열 마스터 키 만들기

상시 암호화를 위한 열 마스터 키를 CNG(Cryptography Next Generation) API를 구현하는 키 저장소에 저장할 수 있습니다. 일반적으로 이 유형의 저장소는 HSM(하드웨어 보안 모듈)입니다. HSM은 디지털 키를 보호 및 관리하고 암호화 처리를 제공하는 물리적 디바이스입니다. HSM은 일반적으로 컴퓨터(로컬 HSM) 또는 네트워크 서버에 직접 연결되는 플러그 인 카드 또는 외부 디바이스 형태입니다.

특정 컴퓨터의 애플리케이션에서 HSM을 사용할 수 있도록 하려면 CNG를 구현하는 KSP(키 스토리지 공급자)를 컴퓨터에서 설치 및 구성해야 합니다. 상시 암호화 클라이언트 드라이버(드라이버 내의 열 마스터 키 저장소 공급자)는 KSP를 사용하여 키 저장소에 저장된 열 마스터 키로 보호되는 열 암호화 키를 암호화 및 암호 해독합니다.

Windows에는 테스트 용도로 사용할 수 있는 Microsoft 소프트웨어 키 스토리지 공급 기업(소프트웨어 기반 KSP)이 있습니다. [CNG 키 스토리지 공급자](/windows/desktop/SecCertEnroll/cng-key-storage-providers)를 참조하세요.

### <a name="creating-column-master-keys-in-a-key-store-using-cngksp"></a>CNG/KSP를 사용하여 키 저장소에서 열 마스터 키 만들기

열 마스터 키는 RSA 알고리즘을 사용하는 비대칭 키(퍼블릭/프라이빗 키 쌍)여야 합니다. 권장되는 키 길이는 2048 이상입니다.

#### <a name="using-hsm-specific-tools"></a>HSM 관련 도구 사용
HSM에 대한 설명서를 참조하세요.

#### <a name="using-powershell"></a>PowerShell 사용

PowerShell의 CNG를 사용 중인 키 저장소에서 .NET API를 사용하여 키를 만들 수 있습니다.


```
$cngProviderName = "Microsoft Software Key Storage Provider" # If you have an HSM, you can use a KSP for your HSM instead of a Microsoft KSP
$cngAlgorithmName = "RSA"
$cngKeySize = 2048 # Recommended key size for Always Encrypted column master keys
$cngKeyName = "AlwaysEncryptedKey" # Name identifying your new key in the KSP
$cngProvider = New-Object System.Security.Cryptography.CngProvider($cngProviderName)
$cngKeyParams = New-Object System.Security.Cryptography.CngKeyCreationParameters
$cngKeyParams.provider = $cngProvider
$cngKeyParams.KeyCreationOptions = [System.Security.Cryptography.CngKeyCreationOptions]::OverwriteExistingKey
$keySizeProperty = New-Object System.Security.Cryptography.CngProperty("Length", [System.BitConverter]::GetBytes($cngKeySize), [System.Security.Cryptography.CngPropertyOptions]::None);
$cngKeyParams.Parameters.Add($keySizeProperty)
$cngAlgorithm = New-Object System.Security.Cryptography.CngAlgorithm($cngAlgorithmName)
$cngKey = [System.Security.Cryptography.CngKey]::Create($cngAlgorithm, $cngKeyName, $cngKeyParams)
```

#### <a name="using-sql-server-management-studio"></a>SQL Server Management Studio 사용

[SQL Server Management Studio를 사용하여 Always Encrypted 키 프로비전](configure-always-encrypted-keys-using-ssms.md)을 참조하세요.

### <a name="making-cng-keys-available-to-applications-and-users"></a>애플리케이션 및 사용자가 CNG 키를 사용할 수 있도록 설정

컴퓨터에서 KSP를 구성하고 애플리케이션 및 사용자에게 HSM 액세스 권한을 부여하는 방법은 HSM 및 KSP 설명서를 참조하세요.

## <a name="creating-column-master-keys-in-hardware-security-modules-using-capi"></a>CAPI를 사용하여 하드웨어 보안 모듈에서 열 마스터 키 만들기

상시 암호화를 위한 열 마스터 키를 CAPI(암호화 API)를 구현하는 키 저장소에 저장할 수 있습니다. 일반적으로 이러한 저장소는 HSM(하드웨어 보안 모듈)으로서, 디지털 키를 보호 및 관리하고 암호화 프로세스를 제공하는 물리적 디바이스입니다. HSM은 일반적으로 컴퓨터(로컬 HSM) 또는 네트워크 서버에 직접 연결되는 플러그 인 카드 또는 외부 디바이스 형태입니다.

특정 컴퓨터의 애플리케이션에서 HSM을 사용할 수 있도록 하려면 CAPI를 구현하는 CSP(Cryptography Service Provider)를 컴퓨터에서 설치 및 구성해야 합니다. 상시 암호화 클라이언트 드라이버(드라이버 내의 열 마스터 키 저장소 공급자)는 CSP를 사용하여 키 저장소에 저장된 열 마스터 키로 보호되는 열 암호화 키를 암호화 및 암호 해독합니다. 

> [!NOTE]
> CAPI는 사용되지 않는 레거시 API입니다. HSM에서 KSP를 사용할 수 있는 경우 CSP/CAPI 대신 사용해야 합니다.

CSP는 상시 암호화와 함께 사용하도록 RSA 알고리즘을 지원해야 합니다.

Windows에는 RSA를 지원하는 소프트웨어 기반(HSM에서 지원되지 않음) CSP인 Microsoft Enhanced RSA and AES Cryptographic Provider가 포함되어 있으며 테스트 용도로 사용할 수 있습니다.

### <a name="creating-column-master-keys-in-a-key-store-using-capicsp"></a>CAPI/CSP를 사용하여 키 저장소에서 열 마스터 키 만들기

열 마스터 키는 RSA 알고리즘을 사용하는 비대칭 키(퍼블릭/프라이빗 키 쌍)여야 합니다. 권장되는 키 길이는 2048 이상입니다.

#### <a name="using-hsm-specific-tools"></a>HSM 관련 도구 사용
HSM에 대한 설명서를 참조하세요.

#### <a name="using-sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio) 사용
[SQL Server Management Studio를 사용하여 Always Encrypted 키 프로비전](configure-always-encrypted-keys-using-ssms.md)을 참조하세요.

### <a name="making-cng-keys-available-to-applications-and-users"></a>애플리케이션 및 사용자가 CNG 키를 사용할 수 있도록 설정
컴퓨터에서 CSP를 구성하고 애플리케이션 및 사용자에게 HSM 액세스 권한을 부여하는 방법은 HSM 및 CSP 설명서를 참조하세요.
 
## <a name="next-steps"></a>다음 단계  
- [SQL Server Management Studio를 사용하여 Always Encrypted 키 프로비전](configure-always-encrypted-keys-using-ssms.md)
- [PowerShell을 사용하여 Always Encrypted 키 프로비저닝](configure-always-encrypted-keys-using-powershell.md)
  
## <a name="see-also"></a>참고 항목 
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted를 위한 키 관리 개요](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)