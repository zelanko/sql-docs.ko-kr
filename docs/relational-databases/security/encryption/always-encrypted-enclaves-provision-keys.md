---
description: Enclave 사용 키 프로비전
title: Enclave 사용 키 프로비전 | Microsoft Docs
ms.custom: ''
ms.date: 10/01/2019
ms.prod: sql
ms.reviewer: vanto
ms.prod_service: database-engine, sql-database
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 13e6fd165c65aa8aeaed4394ec91a17c82b72097
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482240"
---
# <a name="provision-enclave-enabled-keys"></a>Enclave 사용 키 프로비전
[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

이 문서에서는 [보안 enclave를 사용한 Always Encrypted](always-encrypted-enclaves.md)에 사용되는 서버 쪽 보안 enclave 내에서 계산을 지원하는 enclave 사용 키를 프로비전하는 방법을 설명합니다. 

Enclave 사용 키를 프로비전할 때 [Always Encrypted 키 관리에](overview-of-key-management-for-always-encrypted.md)를 위한 일반적인 지침 및 프로세스가 적용됩니다. 이 문서에서는 보안 enclave를 사용한 Always Encrypted와 관련된 세부 정보를 설명합니다.

SQL Server Management Studio 또는 PowerShell을 사용하여 enclave 사용 열 마스터 키를 프로비전하려면 새 키가 enclave 계산을 지원해야 합니다. 그러면 도구(SSMS 또는 PowerShell)에서 데이터베이스의 열 마스터 키 메타데이터에 `ENCLAVE_COMPUTATIONS`를 설정하는 `CREATE COLUMN MASTER KEY` 문을 생성합니다. 자세한 내용은 [CREATE COLUMN MASTER KEY(Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)를 참조하세요. 

또한 이 도구는 열 마스터 키를 사용하여 열 마스터 속성에 디지털 서명하고 데이터베이스 메타데이터에 서명을 저장합니다. 이 서명은 `ENCLAVE_COMPUTATIONS` 설정을 사용한 악의적인 변조를 방지합니다. SQL 클라이언트 드라이버는 Enclave 사용을 허용하기 전에 서명을 확인합니다. 이를 통해 보안 관리자는 Enclave 내에서 계산될 수 있는 열 데이터를 제어할 수 있습니다.

`ENCLAVE_COMPUTATIONS`는 변경할 수 없습니다. 즉, 메타데이터에서 열 마스터 키를 정의한 후에는 변경할 수 없습니다. 지정된 열 마스터 키가 암호화하는 열 암호화 키를 사용하여 enclave 계산을 사용하도록 설정하려면 열 마스터 키를 순환하여 enclave 사용 열 마스터 키로 바꾸어야 합니다. [Enclave 사용 키 순환](always-encrypted-enclaves-rotate-keys.md)을 참조하세요.

> [!NOTE]
> 현재, SSMS와 PowerShell 모두 Azure Key Vault 또는 Windows 인증서 저장소에 저장된 enclave 사용 열 마스터 키를 지원합니다. 하드웨어 보안 모듈(CNG 또는 CAPI 사용)은 지원되지 않습니다.

Enclave 사용 열 암호화 키를 만들려면 enclave 사용 열 마스터 키를 선택하여 새 키를 암호화해야 합니다. 

다음 섹션에서는 SSMS 및 PowerShell을 사용하여 enclave 사용 키를 프로비전하는 방법을 자세히 알아봅니다.

## <a name="provision-enclave-enabled-keys-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 enclave 사용 키 프로비전
SQL Server Management Studio 18.3 이상에서는 다음을 프로비전할 수 있습니다.
- **새 열 마스터 키** 대화 상자를 사용하는 enclave 사용 열 마스터 키.
- **새 열 암호화 키** 대화 상자를 사용하는 enclave 사용 열 암호화 키.

> [!NOTE]
> [Always Encrypted 마법사](always-encrypted-wizard.md)는 현재 enclave 사용 키 생성을 지원하지 않습니다. 그러나 위의 대화 상자를 먼저 사용하여 enclave 사용 키를 만든 다음 마법사를 실행할 때 암호화하려는 열에 대해 기존의 enclave 사용 열 암호화를 선택할 수 있습니다.

### <a name="provision-enclave-enabled-column-master-keys-with-the-new-column-master-key-dialog"></a>새 열 마스터 키 대화 상자를 사용하는 enclave 사용 열 마스터 키 프로비전
Enclave 사용 열 마스터 키를 프로비전하려면 [새 열 마스터 키 대화 상자를 사용하여 열 마스터 키 프로비전](configure-always-encrypted-keys-using-ssms.md#provision-column-master-keys-with-the-new-column-master-key-dialog)의 단계를 수행합니다. **Enclave 계산 허용**을 선택해야 합니다. 아래 스크린샷을 참조하세요.

![Enclave 계산 허용](./media/always-encrypted-enclaves/allow-enclave-computations.png)

> [!NOTE]
> **Enclave 계산 허용** 확인란은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 올바르게 초기화된 보안 enclave가 포함된 경우에만 나타납니다. 자세한 내용은 [Always Encrypted에 대한 enclave 유형 구성](../../../database-engine/configure-windows/configure-column-encryption-enclave-type.md)을 참조하세요.

> [!TIP]
> 열 마스터 키가 enclave를 사용하도록 설정되어 있는지 확인하려면 개체 탐색기에서 해당 키를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. 키가 enclave를 사용하도록 설정된 경우 키 속성을 보여주는 창에 **Enclave 계산: 허용**이 표시됩니다. 또는 [sys.column_master_keys(Transact-SQL)](../../system-catalog-views/sys-column-master-keys-transact-sql.md) 보기를 사용할 수 있습니다.

### <a name="provision-enclave-enabled-column-encryption-keys-with-the-new-column-encryption-key-dialog"></a>새 열 암호화 키 대화 상자를 사용하는 enclave 사용 열 암호화 키 프로비전
Enclave 사용 열 암호화 키를 프로비전하려면 [새 열 암호화 키 대화 상자를 사용하여 열 암호화 키 프로비전](configure-always-encrypted-keys-using-ssms.md#provision-column-encryption-keys-with-the-new-column-encryption-key-dialog)의 단계를 수행합니다. 열 마스터 키를 선택하는 경우 enclave를 사용하도록 설정되어 있는지 확인합니다.

> [!TIP]
> 열 암호화 키가 enclave를 사용하도록 설정되어 있는지 확인하려면 개체 탐색기에서 해당 키를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. 키가 enclave를 사용하도록 설정된 경우 키 속성을 보여주는 창에 **Enclave 계산: 허용**이 표시됩니다.

## <a name="provision-enclave-enabled-keys-using-powershell"></a>PowerShell을 사용하여 Enclave 사용 키 프로비저닝
PowerShell을 사용하여 enclave 사용 키를 프로비전하려면 SqlServer Powershell 모듈 버전 21.1.18179 이상이 필요합니다.

일반적으로 [PowerShell을 사용하여 Always Encrypted 키 프로비전](configure-always-encrypted-keys-using-powershell.md)에 설명된 Always Encrypted에 대한 PowerShell 키 프로비저닝 워크플로(역할 구분 사용 및 사용 안 함)가 enclave 사용 키에도 적용됩니다. 이 섹션에서는 enclave 사용 키와 관련된 세부 정보를 설명합니다.

SqlServer PowerShell 모듈은 프로비저닝 프로세스 도중 enclave 사용 열 마스터 키를 지정할 수 있도록 [**New-SqlCertificateStoreColumnMasterKeySettings**](https://docs.microsoft.com/powershell/module/sqlserver/new-sqlcertificatestorecolumnmasterkeysettings) 및 [**New-SqlAzureKeyVaultColumnMasterKeySettings**](https://docs.microsoft.com/powershell/module/sqlserver/new-sqlazurekeyvaultcolumnmasterkeysettings) cmdlet을 `-AllowEnclaveComputations` 매개 변수로 확장합니다. 각 cmdlet은 Azure Key Vault 또는 Windows 인증서 저장소에 저장된 열 마스터 키의 속성을 포함 하는 로컬 개체를 만듭니다. 지정된 경우 `-AllowEnclaveComputations` 속성은 키를 로컬 개체에서 enclave 사용으로 표시합니다. 또한 cmdlet이 참조되는 열 마스터 키(Azure Key Vault 또는 Windows 인증서 저장소)에 액세스하여 키의 속성에 디지털 서명합니다. 새 enclave 사용 열 마스터 키에 대한 설정 개체를 만들면 [**New-SqlColumnMasterKey**](https://docs.microsoft.com/powershell/module/sqlserver/new-sqlcolumnmasterkey) cmdlet의 후속 호출에서 이를 사용하여 데이터베이스에서 새 키를 설명하는 메타데이터 개체를 만들 수 있습니다.

Enclave 사용 열 암호화 키를 프로비전하는 것은 enclave를 사용하지 않는 열 암호화 키를 프로비전하는 것과 다르지 않습니다. 새 열 암호화 키를 암호화하는 데 사용되는 열 마스터 키가 enclave를 사용하도록 설정되어 있는지 확인만 하면 됩니다.

> [!NOTE]
> SqlServer PowerShell 모듈은 하드웨어 보안 모듈(CNG 또는 CAPI 사용)에 저장된 enclave 사용 키의 프로비저닝을 현재 지원하지 않습니다.

### <a name="example---provision-enclave-enabled-keys-using-windows-certificate-store"></a>예 - Windows 인증서 저장소를 사용하여 enclave 사용 키 프로 비전
아래 엔드투엔드 예제에서는 Windows 인증서 저장소에 열 마스터 키를 저장하여 enclave 사용 키를 프로비전하는 방법을 보여줍니다. 이 스크립트는 [역할 구분이 없는 Windows 인증서 저장소(예)](configure-always-encrypted-keys-using-powershell.md#windows-certificate-store-without-role-separation-example)의 예제를 기반으로 합니다. 유의할 점은 [**New-SqlCertificateStoreColumnMasterKeySettings**](https://docs.microsoft.com/powershell/module/sqlserver/new-sqlcertificatestorecolumnmasterkeysettings) cmdlet에서 `-AllowEnclaveComputations` 매개 변수를 사용한다는 것이 두 예제의 워크플로에서 유일한 차이점입니다.

```powershell
# Create a column master key in Windows Certificate Store.
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation Cert:CurrentUser\My -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage DataEncipherment -KeySpec KeyExchange

# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
# Change the authentication method in the connection string, if needed.
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$database = Get-SqlDatabase -ConnectionString $connStr

# Create a SqlColumnMasterKeySettings object for your column master key
# using the -AllowEnclaveComputations parameter.
$cmkSettings = New-SqlCertificateStoreColumnMasterKeySettings -CertificateStoreLocation "CurrentUser" -Thumbprint $cert.Thumbprint -AllowEnclaveComputations

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName  -InputObject $database -ColumnMasterKey $cmkName
```

### <a name="example---provision-enclave-enabled-keys-using-azure-key-vault"></a>예제 - Azure Key Vault를 사용하여 enclave 사용 키 프로비전
아래 엔드투엔드 예제에서는 Azure Key Vault에 열 마스터 키를 저장하여 enclave 사용 키를 프로비전하는 방법을 보여줍니다. 이 스크립트는 [역할 구분이 없는 Azure Key Vault(예)](configure-always-encrypted-keys-using-powershell.md#azure-key-vault-without-role-separation-example)의 예제를 기반으로 합니다. Enclave를 사용하지 않는 키와 비교하여 enclave 사용 키에 대한 워크플로에서 두 가지 차이점을 확인하는 것이 중요합니다. 
- 아래 스크립트에서 [**New-SqlCertificateStoreColumnMasterKeySettings**](https://docs.microsoft.com/powershell/module/sqlserver/new-sqlcertificatestorecolumnmasterkeysettings)는 `-AllowEnclaveComputations` 매개 변수를 사용하여 새 열 마스터 키를 enclave 사용으로 지정합니다. 
- 아래 스크립트는 [**New-SqlAzureKeyVaultColumnMasterKeySettings**](https://docs.microsoft.com/powershell/module/sqlserver/new-sqlazurekeyvaultcolumnmasterkeysettings) cmdlet을 호출하기 전에 [**Add-SqlAzureAuthenticationContext**](https://docs.microsoft.com/powershell/module/sqlserver/add-sqlazureauthenticationcontext) cmdlet을 호출하여 Azure에 로그인합니다. `-AllowEnclaveComputations` 매개 변수는 **New-SqlAzureKeyVaultColumnMasterKeySettings**에서 Azure Key Vault를 호출하여 열 마스터 키의 속성에 서명하므로 먼저 Azure에로그인해야 합니다.

```powershell
# Create a column master key in Azure Key Vault.
Import-Module Az
Connect-AzAccount
$SubscriptionId = "<Azure SubscriptionId>"
$resourceGroup = "<resource group name>"
$azureLocation = "<datacenter location>"
$akvName = "<key vault name>"
$akvKeyName = "<key name>"
$azureCtx = Set-AzConteXt -SubscriptionId $SubscriptionId # Sets the context for the below cmdlets to the specified subscription.
New-AzResourceGroup -Name $resourceGroup -Location $azureLocation # Creates a new resource group - skip, if your desired group already exists.
New-AzKeyVault -VaultName $akvName -ResourceGroupName $resourceGroup -Location $azureLocation # Creates a new key vault - skip if your vault already exists.
Set-AzKeyVaultAccessPolicy -VaultName $akvName -ResourceGroupName $resourceGroup -PermissionsToKeys get, create, delete, list, wrapKey,unwrapKey, sign, verify -UserPrincipalName $azureCtx.Account
$akvKey = Add-AzureKeyVaultKey -VaultName $akvName -Name $akvKeyName -Destination "Software"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
# Change the authentication method in the connection string, if needed.
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$database = Get-SqlDatabase -ConnectionString $connStr

# Authenticate to Azure - it is required before calling the next cmdlet.
Add-SqlAzureAuthenticationContext -Interactive

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlAzureKeyVaultColumnMasterKeySettings -KeyURL $akvKey.ID -AllowEnclaveComputations

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName
```

## <a name="next-steps"></a>다음 단계
- [보안 Enclave를 사용한 Always Encrypted를 사용하여 열 쿼리](always-encrypted-enclaves-query-columns.md)
- [보안 enclave를 사용한 Always Encrypted를 이용하여 내부 열 암호화 구성](always-encrypted-enclaves-configure-encryption.md)
- [기존 암호화된 열에 관해 보안 Enclave를 사용한 Always Encrypted 사용](always-encrypted-enclaves-enable-for-encrypted-columns.md)
- [보안 enclave를 사용한 Always Encrypted를 이용하여 애플리케이션 개발](always-encrypted-enclaves-client-development.md) 

## <a name="see-also"></a>참고 항목  
- [자습서: SSMS를 사용하여 보안 Enclave를 사용한 Always Encrypted 시작](../tutorial-getting-started-with-always-encrypted-enclaves.md)
- [보안 Enclave를 사용한 Always Encrypted 키 관리](always-encrypted-enclaves-manage-keys.md)
- [CREATE COLUMN MASTER KEY(Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) 
