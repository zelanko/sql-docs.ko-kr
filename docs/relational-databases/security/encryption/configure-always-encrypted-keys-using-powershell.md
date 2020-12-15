---
title: PowerShell을 사용하여 Always Encrypted 키 프로비전 | Microsoft Docs
description: SqlServer PowerShell 모듈을 사용하여 Always Encrypted에 대한 키를 프로비전하여 암호화 키와 데이터베이스에 대한 제어 액세스를 제공하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
ms.assetid: 3bdf8629-738c-489f-959b-2f5afdaf7d61
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b9b9cbe8eb0a443471f261a59aadcaa5b48fc835
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97405923"
---
# <a name="provision-always-encrypted-keys-using-powershell"></a>PowerShell을 사용하여 Always Encrypted 키 프로비전
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]

    
이 문서에서는 [SqlServer PowerShell 모듈](../../../powershell/sql-server-powershell-provider.md)을 사용하여 상시 암호화 키를 프로비전하는 단계를 제공합니다. [역할 구분이 있거나 없는 경우](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md#KeyManagementRoles)모두 키 저장소에 실제 암호화 액세스 키에 대한 액세스 권한이 있는 사용자 및 데이터베이스에 대한 액세스 권한이 있는 사용자를 제어함으로써 PowerShell을 사용하여 상시 암호화 키를 프로비전할 수 있습니다. 

몇 가지 높은 수준의 모범 사례 권장 사항을 비롯한 Always Encrypted 키 관리에 대한 개요는 [Always Encrypted를 위한 키 관리 개요](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)를 참조하세요.
상시 암호화에 SqlServer PowerShell 모듈을 사용 시작하는 방법은 [PowerShell을 사용하여 상시 암호화 구성](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)을 참조하세요.


## <a name="key-provisioning-without-role-separation"></a><a name="KeyProvisionWithoutRoles"></a> 역할 구분 없이 키 프로비전

이 섹션에서는 보안 관리자 및 DBA 간에 역할 구분을 지원하지 않는 키 프로비전 방법에 대해 설명합니다. 아래 단계의 일부에서는 물리적 키에 대한 작업과 키 메타데이터에 대한 작업을 조합합니다. 따라서 이 키 프로비전 방법은 데이터베이스가 클라우드에 호스트되고 중요한 데이터에 액세스하지 못하도록 클라우드 관리자(온-프레미스 DBA는 아님) 제한을 주된 목표로 하는 경우 또는 DevOps 모델을 사용하는 조직에 권장됩니다. 잠재적인 악의적 사용자가 DBA에 포함되거나 DBA가 중요한 데이터에 액세스하면 안 되는 경우에는 권장되지 않습니다.

일반 텍스트 키 또는 키 저장소에 대한 액세스가 관여된 모든 단계(아래 표의 **일반 텍스트 키/키 저장소 액세스** 열에서 식별됨)를 실행하기 전에 데이터베이스를 호스트하는 컴퓨터와 다른 보안 컴퓨터에서 PowerShell 환경이 실행하는지 확인합니다. 자세한 내용은 [키 관리에 대한 보안 고려 사항](overview-of-key-management-for-always-encrypted.md#security-considerations-for-key-management)을 참조하세요.


Task  |아티클  |일반 텍스트 키/키 저장소 액세스  |데이터베이스 액세스   
---------|---------|---------|---------
1단계. 키 저장소에 열 마스터 키를 만듭니다.<br><br>**참고:** SqlServer PowerShell 모듈은 이 단계를 지원하지 않습니다. 명령줄에서 이 태스크를 수행하려면 선택한 키 저장소에 관련된 도구를 사용합니다. |[Always Encrypted를 위한 열 마스터 키 만들기 및 저장](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md) | 예 | 예     
2단계.  PowerShell 환경을 시작하고 SqlServer PowerShell 모듈을 가져옵니다.  |   [PowerShell을 사용하여 Always Encrypted 구성](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)   |    예    | 예         
3단계.  서버 및 데이터베이스에 연결합니다.     |     [데이터베이스에 연결](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase)    |    예     | 예         
4단계.  열 마스터 키의 위치에 대한 정보가 포함된 *SqlColumnMasterKeySettings* 개체를 만듭니다. SqlColumnMasterKeySettings는 PowerShell의 메모리에 있는 개체입니다. 키 저장소에 관련된 cmdlet을 사용합니다.   |     [New-SqlAzureKeyVaultColumnMasterKeySettings](/powershell/sqlserver/sqlserver/vlatest/new-sqlazurekeyvaultcolumnmasterkeysettings)<br><br>[New-SqlCertificateStoreColumnMasterKeySettings](/powershell/sqlserver/sqlserver/vlatest/new-sqlcertificatestorecolumnmasterkeysettings)<br><br>[New-SqlCngColumnMasterKeySettings](/powershell/sqlserver/sqlserver/vlatest/new-sqlcngcolumnmasterkeysettings)<br><br>[New-SqlCspColumnMasterKeySettings](/powershell/sqlserver/sqlserver/vlatest/new-sqlcspcolumnmasterkeysettings)        |   예      | 예         
5단계.  데이터베이스에 열 마스터 키에 대한 메타데이터를 만듭니다.      |    [New-SqlColumnMasterKey](/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkey)<br><br>**참고:** 내부적으로 cmdlet은 [CREATE COLUMN MASTER KEY(Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) 문을 실행하여 키 메타데이터를 만듭니다.|    예     |    예
6단계.  열 마스터 키가 Azure 주요 자격 증명 모음에 저장된 경우 Azure에 인증합니다. | [Add-SqlAzureAuthenticationContext](/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext)    |  예   | 예         
7단계.  새 열 암호화 키를 생성하고 열 마스터 키로 암호화하고 데이터베이스에 열 암호화 키 메타데이터를 만듭니다.     |    [New-SqlColumnEncryptionKey](/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkey)<br><br>**참고:** 내부적으로 열 암호화 키를 생성하고 암호화하는 cmdlet 변형을 사용합니다.<br><br>**참고:** 내부적으로 cmdlet은 [CREATE COLUMN ENCRYPTION KEY(Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md) 문을 실행하여 키 메타데이터를 만듭니다.  | 예 | 예
  

## <a name="windows-certificate-store-without-role-separation-example"></a>역할 구분이 없는 Windows 인증서 저장소(예)

이 스크립트는 Windows 인증서 스토리지의 인증서인 열 마스터 키 생성, 열 암호화 키 생성 및 암호화, SQL Server 데이터베이스에 키 메타데이터 생성 등에 관한 엔드투엔드 예제입니다. 


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

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlCertificateStoreColumnMasterKeySettings -CertificateStoreLocation "CurrentUser" -Thumbprint $cert.Thumbprint

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings


# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName  -InputObject $database -ColumnMasterKey $cmkName
```

## <a name="azure-key-vault-without-role-separation-example"></a>역할 구분이 없는 Azure 주요 자격 증명 모음(예제)

이 스크립트는 Azure 주요 자격 증명 모음 프로비전 및 구성, 자격 증명 모음에 열 마스터 키 생성, 열 암호화 키 생성 및 암호화, Azure SQL 데이터베이스에 키 메타데이터 생성에 대한 엔드투엔드 예제입니다.


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

# Connect to your database (Azure SQL database).
Import-Module "SqlServer"
$serverName = "<Azure SQL server name>.database.windows.net"
$databaseName = "<database name>"
# Change the authentication method in the connection string, if needed.
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Authentication = Active Directory Integrated"
$database = Get-SqlDatabase -ConnectionString $connStr

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlAzureKeyVaultColumnMasterKeySettings -KeyURL $akvKey.ID

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Authenticate to Azure
Add-SqlAzureAuthenticationContext -Interactive

# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName
```

## <a name="cngksp-without-role-separation-example"></a>역할 구분이 없는 CNG/KSP(예제)

아래 스크립트는 CNG(Cryptography Next Generation) API를 구현하는 키 스토리지에 열 마스터 키 생성, 열 암호화 키 생성 및 암호화, SQL Server 데이터베이스에 키 메타데이터 생성에 대한 엔드투엔드 예제입니다.

이 예제는 Microsoft 소프트웨어 키 스토리지 공급자를 사용하는 키 스토리지를 활용합니다. 하드웨어 보안 모듈 등의 다른 저장소를 사용하도록 예제를 수정할 수 있습니다. 그러려면 디바이스에 대한 CNG를 구현하는 KSP(키 저장소 공급자)가 머신에 설치되어 있고 적절하게 작동해야 합니다. `Microsoft Software Key Storage Provider`를 장치의 KSP 이름으로 바꾸어야 합니다.


```powershell
# Create a column master key in a key store that has a CNG provider, a.k.a key store provider (KSP).
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

# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
# Change the authentication method in the connection string, if needed.
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$database = Get-SqlDatabase -ConnectionString $connStr

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlCngColumnMasterKeySettings -CngProviderName $cngProviderName -KeyName $cngKeyName

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName
```

## <a name="key-provisioning-with-role-separation"></a><a name="KeyProvisionWithRoles"></a> 역할 구분이 있는 키 프로비전

이 섹션에서는 보안 관리자가 데이터베이스에 대한 액세스 권한이 없고, 데이터베이스 관리자가 키 저장소 또는 일반 텍스트 키에 대한 액세스 권한이 없는 암호화를 구성하는 단계를 제공합니다.


### <a name="security-administrator"></a>보안 관리자

일반 텍스트 키 또는 키 저장소에 대한 액세스가 관여된 단계(아래 표의 **일반 텍스트 키/키 저장소 액세스** 열에서 식별됨)를 실행하기 전에 다음을 확인합니다.
1.  PowerShell 환경이 데이터베이스를 호스트하는 컴퓨터와 다른 보안 컴퓨터에서 실행됩니다.
2.  조직의 DBA가 역할 구분 목적을 벗어나는 컴퓨터에 대한 액세스 권한이 없습니다.

자세한 내용은 [키 관리에 대한 보안 고려 사항](overview-of-key-management-for-always-encrypted.md#security-considerations-for-key-management)을 참조하세요.


Task  |아티클  |일반 텍스트 키/키 저장소 액세스  |데이터베이스 액세스  
---------|---------|---------|---------
1단계. 키 저장소에 열 마스터 키를 만듭니다.<br><br>**참고:** SqlServer 모듈은 이 단계를 지원하지 않습니다. 명령줄에서 이 태스크를 수행하려면 키 저장소의 유형에 관련된 도구를 사용해야 합니다.     | [Always Encrypted를 위한 열 마스터 키 만들기 및 저장](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)  |    예    | 예 
2단계.  PowerShell 세션을 시작하고 SqlServer 모듈을 가져옵니다.      |     [SqlServer 모듈 가져오기](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#importsqlservermodule)     | 예 | 예         
3단계.  열 마스터 키의 위치에 대한 정보가 포함된 *SqlColumnMasterKeySettings* 개체를 만듭니다. *SqlColumnMasterKeySettings* 는 PowerShell의 메모리에 존재하는 개체입니다. 키 저장소에 관련된 cmdlet을 사용합니다. |      [New-SqlAzureKeyVaultColumnMasterKeySettings](/powershell/sqlserver/sqlserver/vlatest/new-sqlazurekeyvaultcolumnmasterkeysettings)<br><br>[New-SqlCertificateStoreColumnMasterKeySettings](/powershell/sqlserver/sqlserver/vlatest/new-sqlcertificatestorecolumnmasterkeysettings)<br><br>[New-SqlCngColumnMasterKeySettings](/powershell/sqlserver/sqlserver/vlatest/new-sqlcngcolumnmasterkeysettings)<br><br>[New-SqlCspColumnMasterKeySettings](/powershell/sqlserver/sqlserver/vlatest/new-sqlcspcolumnmasterkeysettings)   | 예         | 예         
4단계.  열 마스터 키가 Azure 주요 자격 증명 모음에 저장된 경우 Azure에 인증 |    [Add-SqlAzureAuthenticationContext](/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext)    |예|예         
5단계.  열 암호화 키를 생성하고 열 마스터 키로 암호화하여 열 암호화 키의 암호화된 값을 생성합니다.     |   [New-SqlColumnEncryptionKeyEncryptedValue](/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkeyencryptedvalue)     |    예    | 예        
6단계.  열 마스터 키의 위치(열 마스터 키의 공급자 이름 및 키 경로)와 열 암호화 키의 암호화된 값을 DBA에 제공합니다.  | 아래 예제를 참조하세요.        |   예      | 예         

### <a name="dba"></a>DBA 

DBA는 보안 관리자(위의 6단계)에게 받은 정보를 사용하여 데이터베이스에서 상시 암호화 키 메타데이터를 관리합니다.

Task  |아티클  |일반 텍스트 키 액세스  |데이터베이스 액세스   
---------|---------|---------|---------
1단계.  보안 관리자로부터 열 마스터 키의 위치와 열 암호화 키의 암호화된 값을 얻습니다. |아래 예제를 참조하세요. | 예 | 예
2단계.  PowerShell 환경을 시작하고 SqlServer 모듈을 가져옵니다.  | [PowerShell을 사용하여 Always Encrypted 구성](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)  | 예 | 예
3단계.  서버 및 데이터베이스에 연결합니다. | [데이터베이스에 연결](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase) | 예 | 예
4단계.  열 마스터 키의 위치에 대한 정보가 포함된 SqlColumnMasterKeySettings 개체를 만듭니다. SqlColumnMasterKeySettings는 메모리에 존재하는 개체입니다. | New-SqlColumnMasterKeySettings | 예 | 예
5단계. 데이터베이스에 열 마스터 키에 대한 메타데이터를 만듭니다. | [New-SqlColumnMasterKey](/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkey)<br>**참고:** 내부적으로 cmdlet은 [CREATE COLUMN MASTER KEY(Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) 문을 실행하여 열 마스터 키 메타데이터를 만듭니다. | 예 | 예
6단계. 데이터베이스에 열 암호화 키 메타데이터를 만듭니다. | New-SqlColumnEncryptionKey<br>**참고:** DBA는 열 암호화 키 메타데이터만 만드는 cmdlet의 변형을 사용합니다.<br>내부적으로 cmdlet은 [CREATE COLUMN ENCRYPTION KEY(Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md) 문을 실행하여 열 암호화 키 메타데이터를 만듭니다. | 예 | 예
  
## <a name="windows-certificate-store-with-role-separation-example"></a>역할 구분이 있는 Windows 인증서 저장소(예제)

### <a name="security-administrator"></a>보안 관리자


```powershell
# Create a column master key in Windows Certificate Store.
$storeLocation = "CurrentUser"
$certPath = "Cert:" + $storeLocation + "\My"
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation $certPath -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage DataEncipherment -KeySpec KeyExchange

# Import the SqlServer module
Import-Module "SqlServer"

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlCertificateStoreColumnMasterKeySettings -CertificateStoreLocation "CurrentUser" -Thumbprint $cert.Thumbprint

# Generate a column encryption key, encrypt it with the column master key to produce an encrypted value of the column encryption key.
$encryptedValue = New-SqlColumnEncryptionKeyEncryptedValue -TargetColumnMasterKeySettings $cmkSettings

# Share the location of the column master key and an encrypted value of the column encryption key with a DBA, via a CSV file on a share drive
$keyDataFile = "Z:\keydata.txt"
"KeyStoreProviderName, KeyPath, EncryptedValue" > $keyDataFile
$cmkSettings.KeyStoreProviderName + ", " + $cmkSettings.KeyPath + ", " + $encryptedValue >> $keyDataFile

# Read the key data back to verify
$keyData = Import-Csv $keyDataFile
$keyData.KeyStoreProviderName
$keyData.KeyPath
$keyData.EncryptedValue 
```

### <a name="dba"></a>DBA

```powershell
# Obtain the location of the column master key and the encrypted value of the column encryption key from your Security Administrator, via a CSV file on a share drive.
$keyDataFile = "Z:\keydata.txt"
$keyData = Import-Csv $keyDataFile

# Import the SqlServer module
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$database = Get-SqlDatabase -ConnectionString $connStr

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlColumnMasterKeySettings -KeyStoreProviderName $keyData.KeyStoreProviderName -KeyPath $keyData.KeyPath

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Generate a  column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName -EncryptedValue $keyData.EncryptedValue
```  
 
## <a name="next-steps"></a>다음 단계    
- [PowerShell로 Always Encrypted를 사용하여 열 암호화 구성](configure-column-encryption-using-powershell.md)  
- [PowerShell을 사용하여 Always Encrypted 키 순환](../../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-powershell.md)
- [Always Encrypted를 사용하여 애플리케이션 개발](always-encrypted-client-development.md)

## <a name="see-also"></a>참고 항목    
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)    
- [Always Encrypted를 위한 키 관리 개요](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [Always Encrypted를 위한 열 마스터 키 만들기 및 저장](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)
- [PowerShell을 사용하여 Always Encrypted 구성](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)
- [SQL Server Management Studio를 사용하여 Always Encrypted 키 프로비전](configure-always-encrypted-keys-using-ssms.md)
- [CREATE COLUMN MASTER KEY(Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)
- [CREATE COLUMN MASTER KEY(Transact-SQL)](../../../t-sql/statements/drop-column-master-key-transact-sql.md)
- [CREATE COLUMN ENCRYPTION KEY(Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md)
- [ALTER COLUMN ENCRYPTION KEY(Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md)
- [DROP COLUMN ENCRYPTION KEY(Transact-SQL)](../../../t-sql/statements/drop-column-encryption-key-transact-sql.md) 
- [sys.column_master_keys(Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
- [sys.column_encryption_keys(Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)