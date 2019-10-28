---
title: 보안 Enclave를 사용한 Always Encrypted 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 27f78de54735559365f771aaee3669b8f08856c7
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72902994"
---
# <a name="configure-always-encrypted-with-secure-enclaves"></a>보안 Enclave를 사용한 Always Encrypted 구성

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[보안 Enclave를 사용한 Always Encrypted](always-encrypted-enclaves.md)는 기존 [Always Encrypted](always-encrypted-database-engine.md) 기능을 확장하여 데이터 기밀성을 유지하면서 중요한 데이터에 대해 보다 풍부한 기능을 사용하도록 설정합니다.

보안 enclave를 사용한 Always Encrypted를 설정하려면 다음 워크플로를 사용합니다.

1. HGS(호스트 보호 서비스) 증명을 구성합니다.
2. SQL Server 컴퓨터에 [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)]를 설치합니다.
3. 클라이언트/개발 컴퓨터에 도구를 설치합니다.
4. SQL Server 인스턴스에서 Enclave 형식을 구성합니다.
5. Enclave 사용 키를 프로비전합니다.
6. 중요한 데이터가 포함된 열을 암호화합니다.

> [!NOTE]
> 테스트 환경을 설정하고 SSMS에서 보안 enclave를 사용하여 Always Encrypted 기능을 사용하는 방법에 대한 단계별 자습서는 [자습서: SSMS를 사용하여 보안 enclave로 Always Encrypted 시작](../tutorial-getting-started-with-always-encrypted-enclaves.md)을 참조하세요.

## <a name="configure-your-environment"></a>환경 구성

Always Encrypted에서 보안 enclave를 사용하려면 사용자 환경에 Windows Server 2019 Preview, SSMS(SQL Server Management Studio) 18.0, .NET Framework 및 기타 여러 구성 요소가 필요합니다. 다음 섹션에서는 세부 정보와 필수 구성 요소를 다운로드하기 위한 링크를 제공합니다.

### <a name="sql-server-computer-requirements"></a>SQL Server 컴퓨터 요구 사항

SQL Server를 실행하는 컴퓨터에는 다음 운영 체제 및 SQL Server 버전이 필요합니다.

*SQL Server*:

- [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] 이상

*Windows*:

- Windows 10 Enterprise, 버전 1809
- Windows Server DataCenter(반기 채널), 버전 1809
- Windows Server 2019 DataCenter

> [!IMPORTANT]
> SQL Server 컴퓨터는 HGS로 증명된 보호된 호스트로 구성되어야 합니다. TPM 증명은 프로덕션 환경을 위한 권장되는 Enclave 증명 방법으로, 가상 머신이 아닌 물리적 컴퓨터에서 SQL Server를 실행해야 합니다. 가상 머신은 사전 프로덕션 환경에만 적합합니다.

### <a name="hgs-computer-requirements"></a>HGS 컴퓨터 요구 사항

단일 HGS 컴퓨터만으로 테스트 및 프로토타입 생성에 충분합니다. 프로덕션 환경에서는 컴퓨터 3대로 구성된 Windows 장애 조치(Failover) 클러스터를 사용하는 것이 좋습니다.

Windows HGS(호스트 보호 서비스)는 SQL Server와 동일한 컴퓨터가 아닌 별도 HGS 컴퓨터에 설치해야 합니다. HGS 컴퓨터 요구 사항 및 설정에 대한 자세한 내용은 [SQL Server에서 Always Encrypted의 호스트 보호 서비스 설정](https://docs.microsoft.com/windows-server/security/set-up-hgs-for-always-encrypted-in-sql-server)을 참조하세요.


### <a name="determine-your-attestation-service-url"></a>증명 서비스 URL 확인

증명 서비스 URL을 확인하려면 다음과 같이 도구 및 애플리케이션을 구성해야 합니다.

1. 관리자 권한으로 SQL Server 컴퓨터에 로그인합니다.
2. 관리자 권한으로 PowerShell을 실행합니다.
3. [Get-HGSClientConfiguration](https://docs.microsoft.com/powershell/module/hgsclient/get-hgsclientconfiguration)을 실행합니다.
4. AttestationServerURL 속성을 기록해 둔 후 저장합니다. `https://x.x.x.x/Attestation`과 같아야 합니다.

### <a name="install-tools"></a>도구 설치

클라이언트/개발 컴퓨터에 다음 도구를 설치합니다.

1. [.NET Framework 4.7.2](https://www.microsoft.com/net/download/dotnet-framework-runtime).
2. [SSMS 18.0 이상](../../../ssms/download-sql-server-management-studio-ssms.md)
3. [SQL Server PowerShell 모듈](../../../powershell/download-sql-server-ps-module.md) 버전 21.1 이상
4. [Visual Studio(2017 이상 권장)](https://visualstudio.microsoft.com/downloads/)
5. [.NET Framework 4.7.2용 개발자 팩](https://www.microsoft.com/net/download/visual-studio-sdks)
6. [Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider NuGet 패키지](https://www.nuget.org/packages/Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider), 버전 2.2.0 이상
7. [Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders NuGet 패키지](https://www.nuget.org/packages?q=Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders)

Visual Studio 프로젝트에서 NuGet 패키지를 사용하면 Always Encrypted를 보안 enclave와 함께 사용하여 애플리케이션을 개발할 수 있습니다. 첫 번째 패키지는 Azure Key Vault에 열 마스터 키를 저장하는 경우에만 필요합니다. 자세한 내용은 [애플리케이션 개발](#develop-applications-issuing-rich-queries-in-visual-studio)을 참조하세요.

### <a name="configure-a-secure-enclave"></a>보안 Enclave 구성

클라이언트/개발 컴퓨터에서 다음을 수행합니다.

1. SSMS를 열고 AD(Active Directory) 관리자 권한으로 SQL Server 인스턴스에 연결합니다.
2. 보안 Enclave를 사용한 Always Encrypted가 인스턴스에서 지원되는지 확인하려면 다음 쿼리를 실행합니다.

   ```sql
   SELECT [name], [value], [value_in_use] FROM sys.configurations
   WHERE [name] = 'column encryption enclave type';
   ```

    쿼리는 다음과 같은 행을 반환해야 합니다.  

    | NAME                           | value | value_in_use |
    | ------------------------------ | ----- | -------------|
    | 열 암호화 Enclave 형식 | 0     | 0            |

3. 보안 Enclave 형식을 VBS Enclave로 구성합니다.

   ```sql
   EXEC sys.sp_configure 'column encryption enclave type', 1;
   RECONFIGURE;
   ```

4. 이전 변경 내용을 적용하려면 SQL Server 인스턴스를 다시 시작합니다. 개체 탐색기에서 인스턴스를 마우스 오른쪽 단추로 클릭하고 다시 시작을 선택하여 SSMS에서 해당 인스턴스를 다시 시작합니다. 인스턴스가 다시 시작되면 다시 연결합니다.

5. 이제 다음 쿼리를 실행하여 보안 Enclave가 로드되는지 확인합니다.

   ```sql
   SELECT [name], [value], [value_in_use] FROM sys.configurations
   WHERE [name] = 'column encryption enclave type';
   ```   

    쿼리는 다음과 같은 행을 반환해야 합니다.  

    | NAME                           | value | value_in_use |
    | ------------------------------ | ----- | -------------- |
    | 열 암호화 Enclave 형식 | 1     | 1              |

6. 암호화된 열에 대해 리치 계산을 사용하도록 설정하려면 다음 쿼리를 실행합니다.

   ```sql
   DBCC traceon(127,-1);
   ```

    > [!NOTE]
    > 리치 계산은 [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)]에서 기본적으로 사용되지 않도록 설정됩니다. SQL Server 인스턴스를 다시 시작한 후에 매번 위의 문을 사용하여 리치 계산을 사용하도록 설정해야 합니다.

## <a name="provision-enclave-enabled-keys"></a>Enclave 사용 키 프로비전

enclave 사용 키를 도입해도 [Always Encrypted의 키 프로비저닝 및 키 관리 워크플로](overview-of-key-management-for-always-encrypted.md)는 기본적으로 변경되지 않습니다. 열 마스터 키 프로비저닝 워크플로만 변경되었습니다. 이제 키를 enclave 사용 키로 표시할 수 있습니다. 기본적으로 열 마스터 키는 enclave 사용 키가 아닙니다. 새 열 마스터 키를 enclave 사용 키로 설정하면(SSMS 또는 PowerShell 사용) 다음 동작이 발생합니다.

- 데이터베이스의 열 마스터 키 메타데이터에 있는 `ENCLAVE_COMPUTATIONS` 속성이 설정됩니다.
- 열 마스터 키 속성 값(`ENCLAVE_COMPUTATIONS` 설정 포함)이 디지털 서명됩니다. 이 도구는 실제 열 마스터 키를 사용하여 생성된 서명을 메타데이터에 추가합니다. 이 서명은 `ENCLAVE_COMPUTATIONS` 설정을 사용한 악의적인 변조를 방지합니다. SQL 클라이언트 드라이버는 Enclave 사용을 허용하기 전에 서명을 확인합니다. 이를 통해 보안 관리자는 Enclave 내에서 계산될 수 있는 열 데이터를 제어할 수 있습니다.

열 마스터 키의 `ENCLAVE_COMPUTATIONS` 속성은 변경할 수 없습니다. 키가 프로비저닝된 후에는 키를 변경할 수 없습니다. 하지만 열 마스터 키를 원래 키와는 다른 `ENCLAVE_COMPUTATIONS` 속성 값을 가진 새 키로 바꿀 수 있습니다. 열 마스터 키를 바꾸려면 [열 마스터 키를 순환](#make-columns-enclave-enabled-by-rotating-their-column-master-key)합니다. `ENCLAVE_COMPUTATIONS` 속성에 대한 자세한 내용은 [CREATE COLUMN MASTER KEY](../../../t-sql/statements/create-column-master-key-transact-sql.md)를 참조하세요.

Enclave 사용 열 암호화 키를 프로비전하려면 열 암호화 키를 암호화하는 열 마스터 키가 Enclave 사용 키인지 확인해야 합니다.

현재 Enclave 사용 키 프로비전에는 다음과 같은 제한 사항이 적용됩니다.

- enclave 사용 열 마스터 키는 [Windows 인증서 저장소](/windows/desktop/seccrypto/managing-certificates-with-certificate-stores) 또는 [Azure Key Vault](/azure/key-vault/key-vault-whatis/)에 저장해야 합니다. 지금은 enclave 사용 열 마스터 키를 다른 유형의 키 저장소(예: 하드웨어 보안 모듈 또는 사용자 지정 키 저장소)에 저장할 수 없습니다.

### <a name="provision-enclave-enabled-keys-using-sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio)를 사용하여 Enclave 사용 키 프로비저닝

다음 단계는 Enclave 사용 키를 만듭니다(SSMS 18.0 이상 필요).

1. SSMS를 사용하여 데이터베이스에 연결합니다.
2. **개체 탐색기**에서 데이터베이스를 확장하고 **보안** > **Always Encrypted 키**로 이동합니다.
3. 새 Enclave 사용 열 마스터 키를 프로비전합니다.

    1. **Always Encrypted 키**를 마우스 오른쪽 단추로 클릭하고 **새 열 마스터 키...** 를 선택합니다.
    2. 열 마스터 키 이름을 선택합니다.
    3. **Windows 인증서 저장소(현재 사용자 또는 로컬 컴퓨터)** 또는 **Azure Key Vault**를 선택해야 합니다.
    4. **Enclave 계산 허용**을 선택합니다.
    5. Azure Key Vault를 선택한 경우 Azure에 로그인하고 Key Vault를 선택합니다. Always Encrypted용 Key Vault를 만드는 방법에 대한 자세한 내용은 [Azure Portal에서 Key Vault 관리](https://blogs.technet.microsoft.com/kv/2016/09/12/manage-your-key-vaults-from-new-azure-portal/)를 참조하세요.
    6. 키가 이미 있는 경우 선택하고, 없는 경우 양식의 지침에 따라 새 키를 만듭니다.
    7. **확인**을 클릭합니다.

        ![Enclave 계산 허용](./media/always-encrypted-enclaves/allow-enclave-computations.png)

4. 새 Enclave 사용 열 암호화 키를 만듭니다.

    1. **Always Encrypted 키**를 마우스 오른쪽 단추로 클릭하고 **새 열 암호화 키**를 선택합니다.
    2. 새 열 암호화 키의 이름을 입력합니다.
    3. **열 마스터 키** 드롭다운에서 이전 단계에서 만든 열 마스터 키를 선택합니다.
    4. **확인**을 클릭합니다.

### <a name="provision-enclave-enabled-keys-using-powershell"></a>PowerShell을 사용하여 Enclave 사용 키 프로비저닝

다음 섹션에서는 Enclave 사용 키를 프로비전하기 위한 샘플 PowerShell 스크립트를 제공합니다. 보안 Enclave를 사용한 Always Encrypted 관련(신규) 단계는 강조 표시됩니다. PowerShell을 사용한 키 프로비전에 대한 자세한 내용은(보안 Enclave를 사용한 Always Encrypted에만 국한되지 않는) [PowerShell을 사용하여 Always Encrypted 키 구성](configure-always-encrypted-keys-using-powershell.md)을 참조하세요.

#### <a name="provisioning-enclave-enabled-keys---windows-certificate-store"></a>Enclave 사용 키 프로비저닝 - Windows 인증서 저장소

클라이언트/개발 컴퓨터에서 Windows PowerShell ISE를 열고 다음 스크립트를 실행합니다.

유의해야 할 중요한 사항은 [**New-SqlCertificateStoreColumnMasterKeySettings**](https://docs.microsoft.com/powershell/module/sqlserver/new-sqlcertificatestorecolumnmasterkeysettings) cmdlet에서 `-AllowEnclaveComputations` 매개 변수를 사용해야 한다는 것입니다.

```powershell
# Create a column master key in Windows Certificate Store.
$cert = New-SelfSignedCertificate -Subject "\<Subject Name\>" -CertStoreLocation Cert:CurrentUser\\My -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage DataEncipherment -KeySpec KeyExchange

# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database. Provide the server/db name. Modify the connection string, if needed.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Data Source = " + $serverName + "; Initial Catalog = " + $databaseName + "; Integrated Security = true"
$database = Get-SqlDatabase -ConnectionString $connStr

# Create a SqlColumnMasterKeySettings object for your column master key
# using the -AllowEnclaveComputations parameter.
$cmkSettings = New-SqlCertificateStoreColumnMasterKeySettings -CertificateStoreLocation "CurrentUser" -Thumbprint $cert.Thumbprint -AllowEnclaveComputations

# Create column master key metadata in the database.
$cmkName = "<column master key name in the database>"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database.
$cekName = "<column encryption key name in the database>"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName
```

#### <a name="provisioning-enclave-enabled-keys---azure-key-vault"></a>enclave 사용 키 프로비저닝 - Azure Key Vault

클라이언트/개발 컴퓨터에서 Windows PowerShell ISE를 열고 다음 스크립트를 실행합니다.

**1단계: Azure Key Vault에서 열 마스터 키 프로비전**

이 작업은 Azure Portal을 사용하여 수행할 수도 있습니다. 자세한 내용은 [Azure Portal에서 Key Vault 관리](https://blogs.technet.microsoft.com/kv/2016/09/12/manage-your-key-vaults-from-new-azure-portal/)를 참조하세요.


```powershell
Import-Module Az
Connect-AzAccount

# User values
$SubscriptionId = "<Azure SubscriptionId>"
$resourceGroup = "<resource group name>"
$azureLocation = "<datacenter location>"
$akvName = "<key vault name>"
$akvKeyName = "<key name>"

# Set the context to the specified subscription.
$azureCtx = Set-AzContext -SubscriptionId $SubscriptionId

# Create a new resource group - skip, if your desired group already exists.
New-AzResourceGroup -Name $resourceGroup -Location $azureLocation

# Create a new key vault - skip if your vault already exists.
New-AzKeyVault -VaultName $akvName -ResourceGroupName $resourceGroup -Location $azureLocation

# Grant yourself permissions needed to create and use the column master key.
Set-AzKeyVaultAccessPolicy -VaultName $akvName -ResourceGroupName $resourceGroup -PermissionsToKeys get, create, list, update, wrapKey,unwrapKey, sign, verify -UserPrincipalName $azureCtx.Account

# Create a column master key in Azure Key Vault.
$akvKey = Add-AzureKeyVaultKey -VaultName $akvName -Name $akvKeyName -Destination "Software"
```

**2단계: 데이터베이스에서 열 마스터 키 메타데이터 만들기, 열 암호화 키 만들기 및 데이터베이스에 열 암호화 키 메타데이터 만들기**


```powershell
# Import the SqlServer module.
Import-Module "SqlServer" -Version

# Connect to your database. Provide the server and db name. If needed, modify the connection string.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Data Source = " + $serverName + "; Initial Catalog = " + $databaseName + "; Integrated Security = true"
$database = Get-SqlDatabase -ConnectionString $connStr

# Authenticate to Azure before calling New-SqlAzureKeyVaultColumnMasterKeySettings,
# because -AllowEnclaveComputations causes a call to Azure Key Vault
# to generate the signature of the column master key.
Add-SqlAzureAuthenticationContext -Interactive

# Create a SqlColumnMasterKeySettings object for your column master key.
$cmkSettings = New-SqlAzureKeyVaultColumnMasterKeySettings -KeyURL $akvKey.ID -AllowEnclaveComputations

# Create column master key metadata in the database.
$cmkName = "<column master key name in the database>"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database.
$cekName = "<column encryption key name in the database>"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName
```

## <a name="identify-enclave-enabled-keys-and-columns"></a>enclave 사용 키 및 열 식별

데이터베이스에 구성된 열 마스터 키를 나열하려면 SSMS 등에서 [sys.column_master_keys](../../system-catalog-views/sys-column-master-keys-transact-sql.md) 카탈로그 뷰를 쿼리합니다. 새로운 **allow_enclave_computations** 열에는 열 마스터 키가 enclave 사용 키인지 여부가 표시됩니다.

```sql
SELECT name, allow_enclave_computations
FROM sys.column_master_keys;
```

열 암호화 키가 enclave 사용 열 암호화 키로 암호화된 경우에는 enclave 사용 키입니다. enclave 사용 열 암호화 키를 반환하기 위해 다음 쿼리는 [sys.column_master_keys](../../system-catalog-views/sys-column-master-keys-transact-sql.md), [sys.column_encryption_key_values](../../system-catalog-views/sys-column-encryption-key-values-transact-sql.md) 및 [sys.column_encryption_keys](../../system-catalog-views/sys-column-encryption-keys-transact-sql.md)를 조인합니다.

```sql
SELECT cek.name AS [cek_name]
, cmk.name AS [cmk_name]
, cmk.allow_enclave_computations
FROM sys.column_master_keys cmk
JOIN sys.column_encryption_key_values cekv
   ON cmk.column_master_key_id = cekv.column_master_key_id
JOIN sys.column_encryption_keys cek
   ON cekv.column_encryption_key_id = cek.column_encryption_key_id;
```

enclave 사용 키로 암호화된 열은 enclave 사용 열입니다. enclave 사용 열을 확인하려면 다음 쿼리를 사용합니다.

```sql
SELECT c.name AS column_name
, cek.name AS cek_name
, cmk.name AS [cmk_name]
, cmk.allow_enclave_computations
from sys.columns c
JOIN sys.column_encryption_keys cek 
ON c.column_encryption_key_id = cek.column_encryption_key_id 
JOIN sys.column_encryption_key_values cekv 
ON cekv.column_encryption_key_id = cek.column_encryption_key_id 
JOIN sys.column_master_keys cmk 
ON cmk.column_master_key_id = cekv.column_master_key_id;
```

## <a name="manage-collations"></a>데이터 정렬 관리

Always Encrypted는 데이터 정렬을 제한합니다. 결정적 암호화를 사용하여 암호화된 문자열 열에는 BIN2 이외의 데이터 정렬을 사용할 수 없습니다. 이 제한 사항은 Enclave 사용 문자열 열에도 적용됩니다.

BIN2 이외의 데이터 정렬은 임의 암호화 및 Enclave 사용 열 암호화 키로 암호화된 문자열 열에서 허용됩니다. 그러나 이러한 열에 사용할 수 있는 유일한 새 기능은 바로 암호화입니다. 리치 계산(패턴 일치, 비교 연산)을 사용하도록 설정하려면 암호화된 열에 BIN2 데이터 정렬이 필요합니다.

아래 표에서는 암호화 유형 및 데이터 정렬 순서에 따라 Enclave 사용 문자열 열에 대한 기능을 요약해서 설명합니다.

| **데이터 정렬 순서** | **결정적 암호화** | **임의 암호화**                 |
| ------------------------ | ---------------------------- | ----------------------------------------- |
| **BIN2 이외**             | 지원되지 않음                | 바로 암호화                       |
| **BIN2**                 | 같음 비교          | 바로 암호화 및 리치 계산 |

### <a name="determining-and-changing-collations"></a>데이터 정렬 설정 및 변경

SQL Server에서 데이터 정렬은 서버, 데이터베이스 또는 열 수준에서 설정할 수 있습니다. 현재 데이터 정렬을 확인하고 서버, 데이터베이스 또는 열 수준에서 데이터 정렬을 변경하는 방법에 대한 일반 지침은 [데이터 정렬 및 유니코드 지원](../../collations/collation-and-unicode-support.md)을 참조하세요.

### <a name="special-considerations-for-non-unicode-string-columns"></a>비유니코드 문자열 열에 대한 특수 고려 사항

SQL 클라이언트 드라이버의 제한 사항(Always Encrypted와 관련되지 않음)으로 인해 다음과 같은 추가 제한 사항이 비유니코드(ASCII) 문자열 열에 적용됩니다. 비유니코드(char, varchar) 문자열 열의 데이터베이스 데이터 정렬을 덮어쓴 경우 열 데이터 정렬이 데이터베이스 데이터 정렬과 동일한 코드 페이지를 사용하는지 확인해야 합니다.
데이터 정렬과 해당 코드 페이지 식별자를 나열하려면 다음 쿼리를 사용합니다.

```sql
SELECT [Name]
   , [Description]
   , [CodePage] = COLLATIONPROPERTY([Name], 'CodePage')
FROM ::fn_helpcollations();
```

예를 들어 `Chinese_Traditional_Stroke_Order_100_CI_AI_WS` 및 `Chinese_Traditional_Stroke_Order_100_BIN2`는 코드 페이지가 같지만(950) `Chinese_Traditional_Stroke_Order_100_CI_AI_WS` 및 `Latin1_General_100_BIN2`는 코드 페이지가 서로 다릅니다(950 및 1252). UNICODE(`nchar`, `nvarchar`) 문자열 열에는 위 제한이 적용되지 않습니다. 새로 만드는 암호화된 열에 UNICODE 데이터 형식을 설정하거나, 기존 열을 암호화하기 전에 형식을 UNICODE 형식으로 변경하는 것이 좋습니다.

## <a name="create-a-new-table-with-enclave-enabled-columns"></a>enclave 사용 열을 사용하여 새 테이블 만들기

[CREATE TABLE(Transact-SQL)](../../../t-sql/statements/create-table-transact-sql.md) 문을 사용하여 암호화된 열로 새 테이블을 만들 수 있습니다. 보안 enclave를 사용한 Always Encrypted는 이 문의 구문을 변경하지 않습니다.

1. SSMS를 사용하여 데이터베이스에 연결하고 쿼리 창을 엽니다.

     > [!NOTE]
     > 이 작업을 위해 연결 문자열에서 Always Encrypted를 사용하도록 설정할 필요는 없습니다.

2. 쿼리 창에서 암호화할 각 열의 [열 정의](../../../t-sql/statements/alter-table-column-definition-transact-sql.md)에 `ENCRYPTED WITH` 절을 지정하고 `CREATE TABLE` 문을 실행하여 새 테이블을 만듭니다. 열을 Enclave 사용 열로 지정하려면 Enclave 사용 열 암호화 키를 지정해야 합니다. 데이터베이스의 기본 데이터 정렬이 BIN2 데이터 정렬이 아닌 경우 문자열 열에 대해 BIN2 데이터 정렬을 지정해야 할 수도 있습니다. 자세한 내용은 데이터 정렬 설정 섹션을 참조하세요.

### <a name="example-of-creating-a-new-table-with-enclave-enabled-columns"></a>enclave 사용 열을 사용하여 새 테이블을 만드는 예제

아래 문은 2개의 암호화 열인 SSN 및 Salary를 사용하여 새 테이블을 만듭니다. CEK1을 Enclave 사용 열 암호화 키로 가정하면 열이 임의 암호화를 사용하므로 SQL Server 엔진은 두 열의 바로 암호화 및 리치 계산을 둘 다 지원합니다. 이 문은 UNICODE SSN 열에 대해 Latin1 \_General\_BIN2 데이터 정렬을 설정합니다. 이 설정은 기본 데이터베이스 데이터 정렬이 BIN2 Latin1 이외의 데이터 정렬이라고 가정할 때 필요합니다.

```sql
CREATE TABLE [dbo].[Employees]
(
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [SSN] [char](11) COLLATE Latin1_General_BIN2 ENCRYPTED WITH (
        COLUMN_ENCRYPTION_KEY = [CEK1],
        ENCRYPTION_TYPE = Randomized,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [Salary] [money] ENCRYPTED WITH (
        COLUMN_ENCRYPTION_KEY = [CEK1],
        ENCRYPTION_TYPE = Randomized,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
    CONSTRAINT [PK_dbo.Employees] PRIMARY KEY CLUSTERED (
[EmployeeID] ASC
)
) ON [PRIMARY];
GO
```

## <a name="add-a-new-enclave-enabled-column-to-an-existing-table"></a>기존 테이블에 새 enclave 사용 열 추가

[ALTER TABLE (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md) / ADD문을 사용하여 기존 테이블에 암호화된 새 열을 추가할 수 있습니다. 보안 enclave를 사용한 Always Encrypted는 이 문의 구문을 변경하지 않습니다.

1. SSMS를 사용하여 데이터베이스에 연결하고 쿼리 창을 엽니다.

   이 작업을 위해 연결 문자열에서 Always Encrypted를 사용하도록 설정할 필요는 없습니다.

2. 쿼리 창에서 [열 정의](../../../t-sql/statements/alter-table-column-definition-transact-sql.md)에 ENCRYPTED WITH 절을 지정하고 Enclave 사용 열 암호화 키를 사용하여 ADD 절을 통해 ALTER TABLE 문을 실행합니다. 새 열이 문자열 열이고 데이터베이스의 기본 데이터 정렬이 BIN2 데이터 정렬이 아닌 경우 BIN2 데이터 정렬을 지정해야 할 수도 있습니다. 자세한 내용은 데이터 정렬 설정 섹션을 참조하세요.

### <a name="example-of-adding-a-new-enclave-enabled-column-to-an-existing-table"></a>기존 테이블에 새 enclave 사용 열을 추가하는 예제

CEK1이 Enclave 사용 열 암호화 키라는 전제 하에, 아래 문은 리치 쿼리와 바로 암호화(열이 임의 암호화를 사용하므로)를 둘 다 지원하는 BirthDate라는 암호화된 새 열을 추가합니다.

```sql
ALTER TABLE [dbo].[Employees]
ADD [BirthDate] [Date] ENCRYPTED WITH (
COLUMN_ENCRYPTION_KEY = [CEK1],
ENCRYPTION_TYPE = Randomized,
ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NULL;
```


## <a name="prepare-an-ssms-query-window-with-always-encrypted-enabled"></a>Always Encrypted를 사용하는 SSMS 쿼리 창 준비

Enclave 계산을 사용하도록 설정하는 데 필요한 연결 매개 변수를 추가하려면

1. SSMS를 엽니다.
2. 서버에 연결 대화 상자에서 서버 이름과 데이터베이스 이름을 지정한 후 **옵션**을 클릭합니다. **Always Encrypted** 탭으로 이동한 후 **Always Encrypted 사용**을 선택하고 Enclave 증명 URL을 지정합니다.
    
    ![열 암호화 설정](./media/always-encrypted-enclaves/column-encryption-setting.png)

3. 연결을 클릭합니다.
4. 새 쿼리 창을 엽니다.

또는 쿼리 창이 이미 열려 있는 경우 다음 방법에 따라 Always Encrypted를 사용하도록 해당 데이터베이스 연결을 업데이트할 수 있습니다.

1. 기존 조회 창에서 아무 위치나 마우스 오른쪽 단추로 클릭합니다.
2. 연결 \> 연결 변경을 선택합니다.
3. **옵션**을 클릭합니다. **Always Encrypted** 탭으로 이동한 후 **Always Encrypted 사용**을 선택하고 Enclave 증명 URL을 지정합니다.
4. 연결을 클릭합니다.

## <a name="work-with-encrypted-columns"></a>암호화된 열 사용

### <a name="encrypt-an-existing-plaintext-column-in-place"></a>기존 일반 텍스트 열 바로 암호화

Enclave 사용 열 암호화 키를 사용할 경우 [ALTER TABLE (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md) / ALTER COLUMN 문을 사용하여 기존 일반 텍스트 열을 바로 암호화할 수 있습니다.

enclave 사용 키가 아닌 키를 사용하여 열을 암호화하려면 SSMS의 Always Encrypted 마법사 또는 SqlServer PowerShell 모듈의 Set-SqlColumnEncryption cmdlet과 같은 클라이언트 쪽 도구를 사용해야 합니다. 자세한 내용은 다음을 참조하세요.

- [Always Encrypted 마법사](always-encrypted-wizard.md)
- [PowerShell을 사용하여 열 암호화 구성](configure-column-encryption-using-powershell.md)


#### <a name="prerequisites-for-encrypting-an-existing-plaintext-column-in-place"></a>기존 일반 텍스트 열을 바로 암호화하기 위한 필수 조건

- 기존 열이 암호화되지 않았습니다.
- Enclave 사용 키를 프로비전했습니다.
- 열 마스터 키에 액세스할 수 있습니다.

#### <a name="steps-for-encrypting-existing-plaintext-column-in-place"></a>기존 일반 텍스트 열을 바로 암호화하는 단계

1. 데이터베이스 연결에서 Always Encrypted 및 Enclave 계산을 사용하도록 설정하여 SSMS 쿼리 창을 준비합니다. 자세한 내용은 [Always Encrypted가 사용되는 SSMS 쿼리 창 준비](#prepare-an-ssms-query-window-with-always-encrypted-enabled)를 참조하세요.
2. 쿼리 창에서 ENCRYPTED WITH 절에 Enclave 사용 열 암호화 키를 지정하여 ALTER COLUMN 절을 통해 ALTER TABLE 문을 실행합니다. 열이 문자열 열(예: char, varchar, nchar, nvarchar)인 경우에도 데이터 정렬을 BIN2 데이터 정렬로 변경해야 할 수 있습니다. 자세한 내용은 데이터 정렬 설정 섹션을 참조하세요.
    
    > [!NOTE]
    > 열 마스터 키가 Azure Key Vault에 저장된 경우 Azure에 로그인하라는 메시지가 표시될 수 있습니다.

3. 테이블에 액세스하는 모든 일괄 처리 및 저장 프로시저의 계획 캐시를 지워 매개 변수 암호화 정보를 새로 고칩니다. 
 
    ```sql
    ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
    ```
    > [!NOTE]
    > 영향을 받는 쿼리 계획을 캐시에서 제거하지 않으면 암호화 후 첫 번째 쿼리 실행이 실패할 수 있습니다.

    > [!NOTE]
    > 쿼리 성능이 일시적으로 저하될 수 있으므로 `ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE` 또는 `DBCC FREEPROCCACHE`를 사용하여 계획 캐시를 신중하게 지웁니다. 캐시를 지울 때 나타나는 부정적인 영향을 최소화하기 위해 영향을 받는 쿼리 계획만 선택적으로 제거할 수 있습니다.

4.  [sp_refresh_parameter_encryption](../../system-stored-procedures/sp-refresh-parameter-encryption-transact-sql.md)을 호출하여 [sys.parameters](../..//system-catalog-views/sys-parameters-transact-sql.md)에 보관되었으며 열 암호화로 인해 무효화되었을 수 있는 각 모듈(저장 프로시저, 함수, 뷰, 트리거)의 매개 변수 메타데이터를 업데이트합니다.

#### <a name="example-of-encrypting-existing-plaintext-column-in-place"></a>기존 일반 텍스트 열을 바로 암호화하는 예제

아래 예제에서는 다음을 가정합니다.

- CEK1은 Enclave 사용 열 암호화 키입니다.

- SSN 열은 일반 텍스트이며 현재 Latin1, BIN2 이외의 데이터 정렬(예: Latin1\_General\_CI\_AI\_KS\_WS)을 사용하고 있습니다.

이 문은 임의 암호화 및 Enclave 사용 열 암호화 키를 사용하여 SSN 열을 암호화합니다. 또한 기본 데이터베이스 데이터 정렬을 해당(동일한 코드 페이지) BIN2 데이터 정렬로 덮어씁니다.

이 작업은 온라인으로 수행됩니다(ONLINE = ON). 또한 테이블 스키마 변경의 영향을 받는 쿼리 계획을 다시 만드는 **ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE** 호출도 확인합니다.

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char] COLLATE Latin1_General_BIN2
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
WITH
(ONLINE = ON);
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

### <a name="make-an-existing-encrypted-column-enclave-enabled"></a>기존의 암호화된 열을 enclave 사용 열로 지정

enclave 사용 열이 아닌 기존 열에서 enclave 기능을 사용하도록 설정하는 여러 가지 방법이 있습니다. 어떤 방법을 선택하는지는 다음과 같은 몇 가지 요인에 따라 다릅니다.

- **범위/세분성:** 열 하위 집합 또는 지정된 열 마스터 키로 보호되는 모든 열의 enclave 기능을 사용하도록 설정하고 싶나요?
- **데이터 크기:** enclave 사용 열로 지정하려는 열이 포함된 테이블의 크기는 얼마나 되나요?
- 열의 암호화 유형을 변경하고 싶나요? 임의 암호화만 리치 계산(패턴 일치, 비교 연산자)을 지원한다는 점에 유의합니다. 결정적 암호화를 사용하여 열을 암호화한 경우에도, enclave의 전체 기능을 활용하려면 임의 암호화로 다시 암호화해야 합니다.

다음은 기존 열에 Enclave를 사용하도록 설정하는 세 가지 방법입니다.

#### <a name="option-1-rotate-the-column-master-key-to-replace-it-with-an-enclave-enabled-column-master-key"></a>옵션 1: 열 마스터 키를 순환하여 enclave 사용 열 마스터 키로 바꿉니다.
  
- 장점:
  - 데이터를 다시 암호화하지 않으므로 일반적으로 가장 빠른 방법입니다. 리치 계산을 사용하도록 설정해야 하는 모든 열이 이미 결정적 암호화를 사용하고 있으므로 다시 암호화할 필요가 없는 경우, 많은 양의 데이터를 포함하는 열에 권장되는 방법입니다.
  - 여러 열의 Enclave 기능을 대규모로 사용하도록 설정할 수 있습니다. 이 방식은 원래의 열 마스터 키와 관련된 모든 열 암호화 키 및 암호화된 모든 열을 Enclave 사용 방식으로 지정하기 때문입니다.
  
- 단점:
  - 암호화 유형을 결정적 암호화에서 임의 암호화로 변경할 수 없으므로, 결정적 암호화된 열을 바로 암호화할 수는 있지만 리치 계산을 사용할 수 없습니다.
  - 지정된 열 마스터 키와 연결된 일부 열만 선택적으로 변환할 수 없습니다.
  - 키 관리 오버헤드가 발생하므로 새 열 마스터 키를 만들고 영향을 받는 열을 쿼리하는 애플리케이션에서 사용하도록 해야 합니다.  

#### <a name="option-2-this-approach-involves-two-steps-1-rotating-the-column-master-key-as-in-option-1-and-2-re-encrypting-a-subset-of-deterministically-encrypted-columns-using-randomized-encryption-to-enable-rich-computations-for-those-columns"></a>옵션 2: 이 방법은 두 단계로 이루어집니다. 1) 열 마스터 키 순환(옵션 1과 같음) 및 2) 임의 암호화를 사용하여 확실히 암호화된 열의 하위 집합을 다시 암호화하여 해당 열에 대한 리치 계산을 사용하도록 설정합니다.
  
- 장점:
  - 데이터를 바로 암호화하므로, 대량의 데이터를 포함하는 열을 확실히 암호화하기 위해 리치 쿼리를 사용하도록 설정하는 데 권장되는 방법입니다. 1단계를 완료하면 결정적 암호화를 사용하는 열을 바로 암호화할 수 있으므로 2단계는 바로 수행할 수 있습니다.
  - 여러 열의 Enclave 기능을 대규모로 사용하도록 설정할 수 있습니다.
  
- 단점:
  - 지정된 열 마스터 키와 연결된 일부 열만 선택적으로 변환할 수 없습니다.
  - 키 관리 오버헤드가 발생하므로 새 열 마스터 키를 만들고 영향을 받는 열을 쿼리하는 애플리케이션에서 사용하도록 해야 합니다.

#### <a name="option-3-re-encrypting-selected-columns-with-a-new-enclave-enabled-column-encryption-key-and-randomized-encryption-if-needed-on-the-client-side"></a>옵션 3: 클라이언트 쪽에서 새 enclave 사용 열 암호화 키 및 임의 암호화(필요한 경우)를 사용하여 선택한 열을 다시 암호화합니다.
  
- 장점 - 이 방법에는 다음이 적용됩니다.
  - 하나의 열 또는 소규모 열 하위 집합에 대해 Enclave 기능을 선택적으로 사용하도록 설정할 수 있습니다.
  - 명확하게 암호화된 열의 리치 계산을 한 단계로 사용하도록 설정할 수 있습니다.
  - 새 열 마스터 키를 만들 필요가 없으므로 애플리케이션에 미치는 영향이 더 적습니다.
  
- 단점:
  - 다시 암호화하기 위해 열을 포함하는 테이블의 전체 내용을 데이터베이스 외부로 이동해야 하므로 소규모 테이블에만 권장됩니다.

자세한 내용은 다음 섹션을 참조하십시오.
  - [열 마스터 키를 순환하여 열을 Enclave 사용 열로 지정](#make-columns-enclave-enabled-by-rotating-their-column-master-key)
  - [열 바로 다시 암호화](#re-encrypt-columns-in-place)
  - [클라이언트 쪽에서 열 다시 암호화](#re-encrypt-columns-on-the-client-side)

### <a name="make-columns-enclave-enabled-by-rotating-their-column-master-key"></a>열 마스터 키를 순환하여 열을 enclave 사용 열로 지정

열 마스터 키 순환은 기존 열 마스터 키를 새 열 마스터 키로 대체하는 프로세스입니다. 이 방식에서는 이전 열 마스터 키와 관련된 열 암호화 키를 새 열 마스터 키로 다시 암호화합니다. 이 워크플로는 Always Encrypted의 초기 릴리스 이래로, 규정 준수 또는 보안상의 이유(기존 열 마스터 키가 손상된 경우)로 열 마스터 키 대체를 지원하기 위해 사용되었습니다.

Enclave를 사용한 Always Encrypted는 열 마스터 키 순환 워크플로를 사용하는 새로운 이유가 되고 있습니다. 이전 열 마스터 키가 enclave 사용 키가 아니고, 새 열 마스터 키가 enclave 사용 키라고 가정하면 순환 프로세스는 결과적으로 열 마스터 키와 관련된 모든 열 암호화 키를 enclave 사용 키로 만듭니다. 열 마스터 키 순환은 데이터를 다시 암호화하지 않으므로 기존 열에서 enclave 기능을 사용하도록 설정하는 권장 프로세스입니다.

열 마스터 키를 순환해도 영향을 받는 열의 암호화 유형은 변경되지 않습니다. 따라서 확실히 암호화된 열의 바로 암호화만 잠금 해제할 수 있습니다. 결정적 암호화를 사용하여 열의 리치 계산을 잠금 해제하려면, 열 마스터 키를 순환한 후 다시 암호화해야 합니다(바로).

또한 리치 계산을 잠금 해제하기 위해 임의 암호화를 사용하여 문자열 열의 데이터 정렬을 BIN2 데이터 정렬로 변경해야 할 수도 있습니다. 자세한 내용은 데이터 정렬 설정 섹션을 참조하세요.

열 마스터 키 순환 프로세스는 관련 키가 Enclave 사용 키인지에 관계없이 동일합니다. 열 마스터 키를 순환하는 방법에 대한 자세한 내용은 다음 문서에 나와 있습니다.

- [SSMS를 사용하여 열 마스터 키 순환](configure-always-encrypted-using-sql-server-management-studio.md)
- [PowerShell을 사용하여 열 마스터 키 순환](rotate-always-encrypted-keys-using-powershell.md)하기

사용자 편의를 위해 열 마스터 키 순환을 위한 샘플 PowerShell 스크립트가 아래에 제공됩니다.

#### <a name="prerequisites-of-rotating-the-column-master-key-for-enclave-enabled-columns"></a>enclave 사용 열에 대해 열 마스터 키를 순환하기 위한 필수 조건

- 새 Enclave 사용 열 마스터 키를 프로비전했습니다.
- 이전 및 새 열 마스터 키에 액세스할 수 있습니다.
- 이전 열 마스터 키로 보호되는 모든 문자열 열은 BIN2 데이터 정렬을 사용합니다.

> [!NOTE]
> 또는 열 마스터 키 순환 후 문자열 열의 데이터 정렬을 변경할 수 있습니다.

#### <a name="steps-for-rotating-the-column-master-key-for-enclave-enabled-columns"></a>enclave 사용 열에 대해 열 마스터 키를 순환하는 단계

Windows PowerShell ISE에 다음 스크립트를 붙여넣고 \<자리 표시자\>를 고유한 값으로 바꿉니다.

```powershell
# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database. Modify server/db name or/and the connection string, if needed.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Data Source = " + $serverName + "; Initial Catalog = " +
$databaseName + "; Integrated Security = true"
$database = Get-SqlDatabase -ConnectionString $connStr

# Set the names of the old/current column master key and the new/target enclave-enabled column master key. (Change the names, if needed).
$oldCmkName = "<old column master key name>"
$newCmkName = "<new column master key name>"

# Authenticate to Azure. Needed only of either column master key is stored in Azure Key Vault.
Add-SqlAzureAuthenticationContext -Interactive

# Initiate the rotation from the current column master key to the new column master key.
Invoke-SqlColumnMasterKeyRotation -SourceColumnMasterKeyName $oldCmkName
-TargetColumnMasterKeyName $newCmkName -InputObject $database

# Complete the rotation of the old column master key.
Complete-SqlColumnMasterKeyRotation -SourceColumnMasterKeyName
$oldCmkName -InputObject $database

# Remove the old column master key metadata.
Remove-SqlColumnMasterKey -Name $oldCmkName -InputObject $database
```


### <a name="re-encrypt-columns-in-place"></a>열 바로 다시 암호화

열을 Enclave 사용 열로 지정한 후에 다음 작업을 바로 수행할 수 있습니다(Enclave 내부에서 데이터베이스 외부로 데이터를 이동할 필요 없음).

- 열 암호화 키 순환(새 키로 대체). 경우에 따라 주기적인 키 순환을 요구하는 준수 규정을 충족하기 위해 또는 보안상의 이유로(열 암호화 키가 손상된 경우) 필요합니다.
- 암호화 유형을 결정적 암호화에서 임의 암호화로 변경(예를 들어 열의 리치 계산을 잠금 해제하기 위해)

#### <a name="prerequisites-for-re-encrypting-columns-in-place"></a>열을 바로 다시 암호화하기 위한 필수 조건

- Enclave 사용 열 암호화 키를 사용하여 열을 암호화했습니다.
- 새 Enclave 사용 열 암호화 키를 프로비전했습니다(현재 Enclave 사용 열 암호화 키를 대체하려는 경우 열 보호).
- 열 마스터 키에 액세스할 수 있습니다.

#### <a name="steps-for-re-encrypting-columns-in-place"></a>열을 바로 다시 암호화하는 단계

1. 데이터베이스 연결에서 Always Encrypted 및 Enclave 계산을 사용하도록 설정하여 SSMS 쿼리 창을 준비합니다. 자세한 내용은 [Always Encrypted가 사용되는 SSMS 쿼리 창 준비](#prepare-an-ssms-query-window-with-always-encrypted-enabled)를 참조하세요.

2. 쿼리 창에서 ENCRYPTED WITH 절에 다음을 지정하여 ALTER COLUMN 절을 통해 [ALTER TABLE (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md) 문을 실행합니다.
    
    1. 현재 키를 순환하는 경우 새 enclave 사용 열 암호화 키의 이름. 열 암호화 키를 변경하지 않는 경우 현재 키의 이름을 지정해야 합니다.
    
    2. 암호화 유형을 변경하는 경우 새 암호화 유형. 암호화 유형을 변경하지 않는 경우 현재 암호화 유형을 지정해야 합니다.
        
       다시 암호화하려는 열이 기본 데이터베이스 데이터 정렬과는 다른 데이터 정렬(BIN2)을 사용하는 경우 COLLATE 구를 포함하고 열 정의에 현재 열 데이터 정렬을 지정해야 합니다(데이터 정렬을 동일하게 유지).
        
       > [!NOTE]
       > 열 마스터 키가 Azure Key Vault에 저장된 경우 Azure에 로그인하라는 메시지가 표시될 수 있습니다.

3. 테이블에 액세스하는 모든 일괄 처리 및 저장 프로시저의 계획 캐시를 지워 매개 변수 암호화 정보를 새로 고칩니다. 
 
    ```sql
    ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
    ```
    > [!NOTE]
    > 영향을 받는 쿼리 계획을 캐시에서 제거하지 않으면 암호화 후 첫 번째 쿼리 실행이 실패할 수 있습니다.

    > [!NOTE]
    > 쿼리 성능이 일시적으로 저하될 수 있으므로 ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE 또는 DBCC FREEPROCCACHE를 사용하여 계획 캐시를 신중하게 지웁니다. 캐시를 지울 때 나타나는 부정적인 영향을 최소화하기 위해 영향을 받는 쿼리 계획만 선택적으로 제거할 수 있습니다.

4.  [sp_refresh_parameter_encryption](../../system-stored-procedures/sp-refresh-parameter-encryption-transact-sql.md)을 호출하여 [sys.parameters](../..//system-catalog-views/sys-parameters-transact-sql.md)에 보관되었으며 열 다시 암호화로 인해 무효화되었을 수 있는 각 모듈(저장 프로시저, 함수, 뷰, 트리거)의 매개 변수 메타데이터를 업데이트합니다.

#### <a name="examples-of-re-encrypting-columns-in-place"></a>열을 바로 다시 암호화하는 예제

현재, CEK1이라는 Enclave 사용 열 암호화 키 및 결정적 암호화를 사용하여 SSN 열을 암호화하며 열 수준에서 설정된 현재 데이터 정렬이 Latin1\_General\_BIN2인 경우 아래 문은 임의 암호화 및 동일한 키를 사용하여 열을 다시 암호화합니다.

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) COLLATE Latin1_General_BIN2
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1]
, ENCRYPTION_TYPE = Randomized
, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL;
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

현재 CEK1이라는 enclave 사용 열 암호화 키와 결정적 암호화를 사용하여 SSN 열이 암호화되었으며 기본 데이터베이스 데이터 정렬이 BIN2 데이터 정렬이고 열 수준에서 설정되지 않았다고 가정할 경우, 아래 문은 CEK2라는 새 enclave 사용 키로 열을 다시 암호화합니다(암호화 유형을 변경하지 않음).

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) 
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK2]
, ENCRYPTION\_TYPE = Deterministic
, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL;
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

현재 CEK1이라는 enclave 사용 열 암호화 키와 결정적 암호화를 사용하여 SSN 열이 암호화되었으며 기본 데이터베이스 데이터 정렬이 BIN2 데이터 정렬이고 열 수준에서 설정되지 않았다고 가정할 경우, 아래 문은 새 enclave 사용 키와 임의 암호화로 열을 다시 암호화합니다. 또한 이 작업은 온라인 모드에서 수행됩니다.

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) 
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1]
, ENCRYPTION_TYPE = Randomized
, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL 
WITH (ONLINE = ON);
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

### <a name="re-encrypt-columns-on-the-client-side"></a>클라이언트 쪽에서 열 다시 암호화

열을 다시 암호화(및 암호화 또는 암호 해독)하는 레거시 방법은 Always Encrypted 마법사 또는 PowerShell과 같은 클라이언트 쪽 도구를 사용합니다. 일반적으로 이 방법은 다시 암호화하려는 열을 포함하는 테이블이 작고, 새 enclave 사용 키로 열을 다시 암호화한 후 암호화 유형을 결정적에서 임의로 변경하려는 경우를 제외하고는 권장되지 않습니다.

임의 암호화를 사용하여 열을 다시 암호화하는 경우, 리치 계산을 활용하기 위해 다시 암호화 이전 또는 이후에 해당 데이터 정렬을 BIN2 데이터 정렬로 변경해야 할 수도 있습니다. 자세한 내용은 데이터 정렬 설정 섹션을 참조하세요.

자세한 내용은 다음을 참조하세요.

  - SSMS를 사용하여 열 암호화 키 순환: <https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-wizard>
  - PowerShell을 사용하여 열 암호화 키 순환: <https://docs.microsoft.com/sql/relational-databases/security/encryption/configure-column-encryption-using-powershell>

### <a name="decrypt-a-column-in-place"></a>열 바로 암호 해독

Enclave 사용 열 암호화 키로 열을 암호화할 경우 ALTER TABLE 문을 사용하여 바로 암호 해독(일반 텍스트 열로 변환)할 수 있습니다. 또한 이 작업은 온라인 모드에서 수행됩니다.

#### <a name="prerequisites-for-decrypting-a-column-in-place"></a>열을 바로 암호 해독하기 위한 필수 조건

- Enclave 사용 열 암호화 키를 사용하여 열을 암호화했습니다.
- 열 마스터 키에 액세스할 수 있습니다.

#### <a name="steps-for-decrypting-a-column-in-place"></a>열을 바로 암호 해독하는 단계

1. 데이터베이스 연결에서 Always Encrypted 및 Enclave 계산을 사용하도록 설정하여 SSMS 쿼리 창을 준비합니다. 자세한 내용은 [Always Encrypted가 사용되는 SSMS 쿼리 창 준비](#prepare-an-ssms-query-window-with-always-encrypted-enabled)를 참조하세요.

2. 쿼리 창에서 ENCRYPTED WITH 절을 사용하지 **않고** 원하는 열 구성을 지정하여 ALTER COLUMN 절을 통해 [ALTER TABLE (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md) 문을 실행합니다.
    
    > [!NOTE]
    > 열 마스터 키가 Azure Key Vault에 저장된 경우 Azure에 로그인하라는 메시지가 표시될 수 있습니다.

3. 테이블에 액세스하는 모든 일괄 처리 및 저장 프로시저의 계획 캐시를 지워 매개 변수 암호화 정보를 새로 고칩니다. 

    ```sql
    ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
    ```

    > [!NOTE]
    > 영향을 받는 쿼리 계획을 캐시에서 제거하지 않으면 암호화 후 첫 번째 쿼리 실행이 실패할 수 있습니다.

    > [!NOTE]
    > 쿼리 성능이 일시적으로 저하될 수 있으므로 ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE 또는 DBCC FREEPROCCACHE를 사용하여 계획 캐시를 신중하게 지웁니다. 캐시를 지울 때 나타나는 부정적인 영향을 최소화하기 위해 영향을 받는 쿼리 계획만 선택적으로 제거할 수 있습니다.

4. [sp_refresh_parameter_encryption](../../system-stored-procedures/sp-refresh-parameter-encryption-transact-sql.md)을 호출하여 [sys.parameters](../..//system-catalog-views/sys-parameters-transact-sql.md)에 보관되었으며 열 암호 해독으로 인해 무효화되었을 수 있는 각 모듈(저장 프로시저, 함수, 뷰, 트리거)의 매개 변수 메타데이터를 업데이트합니다.

#### <a name="example-for-decrypting-a-column-in-place"></a>열을 바로 암호 해독하는 예제

SSN 열이 암호화되고 열 수준에서 설정된 현재 데이터 정렬이 Latin1\_General\_BIN2라고 가정할 경우 아래 명령문은 열을 암호 해독합니다(데이터 정렬을 변경하지 않고 유지하면 동일한 명령문에서 데이터 정렬을 BIN2 이외의 데이터 정렬로 변경하도록 선택할 수도 있습니다).

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) COLLATE Latin1_General_BIN2
WITH (ONLINE = ON);
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

## <a name="issue-rich-queries-against-encrypted-columns-using-ssms"></a>SSMS를 사용하여 암호화된 열에 대해 풍부한 쿼리 실행

Enclave 사용 열에 리치 쿼리를 사용하는 가장 빠른 방법은 SSMS 쿼리 창에서 Always Encrypted에 대한 매개 변수화를 설정하는 것입니다. SSMS의 이 유용한 기능에 대한 자세한 내용은 다음을 참조하세요.

- [Always Encrypted에 대한 매개 변수화 - SSMS를 사용하여 암호화된 열에 삽입, 업데이트 및 필터링](https://blogs.msdn.microsoft.com/sqlsecurity/2016/12/13/parameterization-for-always-encrypted-using-ssms-to-insert-into-update-and-filter-by-encrypted-columns/)
- [암호화된 열 쿼리](configure-always-encrypted-using-sql-server-management-studio.md#querying-encrypted-columns)

### <a name="prerequisites-for-issuing-rich-queries-against-encrypted-columns-using-ssms"></a>SSMS를 사용하여 암호화된 열에 대해 풍부한 쿼리를 실행하기 위한 필수 조건

- 쿼리할 열은 Enclave 사용 열입니다.
- 열 마스터 키에 액세스할 수 있습니다.

### <a name="steps-for-issuing-rich-queries-against-encrypted-columns-using-ssms"></a>SSMS를 사용하여 암호화된 열에 대해 풍부한 쿼리를 실행하는 단계

1. 데이터베이스 연결에서 Always Encrypted 및 Enclave 계산을 사용하도록 설정하여 SSMS 쿼리 창을 준비합니다. 자세한 내용은 [Always Encrypted가 사용되는 SSMS 쿼리 창 준비](#prepare-an-ssms-query-window-with-always-encrypted-enabled)를 참조하세요.

2. Always Encrypted에 대해 매개 변수화 사용

    1. SSMS의 주 메뉴에서 **쿼리**를 선택합니다.
    2. **쿼리 옵션...** 을 선택합니다.
    3. **실행** > **고급**으로 이동합니다.
    4. Always Encrypted에 대해 매개 변수화 사용을 선택하거나 선택 취소합니다.
    5. 확인을 클릭합니다.

3. 암호화된 열에 리치 계산을 사용하여 쿼리를 작성하고 실행합니다. 쿼리에서 암호화된 열을 대상으로 하는 각 값에 대해 Transact-SQL 변수를 선언해야 합니다. 변수는 인라인 초기화를 사용해야 합니다(SET 문을 통해 설정할 수 없음).

    > [!NOTE]
    > 열 마스터 키가 Azure Key Vault에 저장된 경우 Azure에 로그인하라는 메시지가 표시될 수 있습니다.

### <a name="example-of-rich-queries-against-encrypted-columns"></a>암호화된 열에 대한 풍부한 쿼리 예제

이 예제에서는 데이터베이스가 다음 문을 사용하여 만든 테이블을 포함한다고 가정합니다.

```sql
CREATE TABLE [dbo].[Employees]
(
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [SSN] [char](11) COLLATE Latin1_General_BIN2 ENCRYPTED WITH (
        COLUMN_ENCRYPTION_KEY = [CEK1],
        ENCRYPTION_TYPE = Randomized,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [Salary] [money] ENCRYPTED WITH (
        COLUMN_ENCRYPTION_KEY = [CEK1],
        ENCRYPTION_TYPE = Randomized,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
    CONSTRAINT [PK_dbo.Employees] PRIMARY KEY CLUSTERED (
[EmployeeID] ASC
)
) ON [PRIMARY];
GO
```

CEK1은 Enclave 사용 열 암호화 키입니다.

해당 테이블에 대해 매개 변수화 지침을 준수하는 쿼리 예제는 다음과 같습니다.

```sql
DECLARE @SSNPattern [char](11) = '%1111%'
DECLARE @MinSalary [money] = 1000
SELECT *
FROM [dbo].[Employees]
WHERE SSN LIKE @SSNPattern
    AND [Salary] >= @MinSalary;
GO;
```

## <a name="create-and-use-indexes-on-enclave-enabled-columns-using-randomized-encryption"></a>임의 암호화를 사용하는 enclave 사용 열에 인덱스 만들기 및 사용

임의 암호화를 사용하는 enclave 사용 열의 인덱스는 암호화된 인덱스 키 값을 저장하는 동시에 일반 텍스트를 기준으로 값이 정렬되기 때문에, SQL Server 엔진은 다음을 포함하여 인덱스를 만들거나 업데이트해야 하는 모든 작업에 enclave를 사용해야 합니다.

- 인덱스 만들기 또는 다시 작성
- 인덱스의 인덱스 키 삽입 및/또는 제거를 트리거하는 테이블의 행 삽입, 업데이트 또는 삭제(인덱싱된/암호화된 열 포함)
- 인덱스 무결성 검사가 필요한 DBCC 명령(예: [DBCC CHECKDB(Transact-SQL)](../../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) 또는 [DBCC CHECKTABLE(Transact-SQL)](../../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)) 실행
- SQL Server에서 인덱스 변경 내용을 취소해야 하는 경우 데이터베이스 복구(예: SQL Server에서 오류가 발생하고 다시 시작된 후)(자세한 내용은 아래 참조)

위의 모든 작업을 수행하려면 인덱스 키의 암호를 해독할 수 있도록 인덱싱된 열의 열 암호화 키가 enclave에 있어야 합니다. 일반적으로 enclave는 다음 두 가지 방법 중 하나로 열 암호화 키를 가져올 수 있습니다.
- 클라이언트 애플리케이션에서 직접
- 열 암호화 키 캐시에서

### <a name="invoke-indexing-operations-with-column-encryption-keys-provided-directly-by-the-client"></a>클라이언트에서 직접 제공하는 열 암호화 키를 사용하여 인덱싱 작업 호출

인덱싱 작업을 호출하는 이 방법이 성공하려면 인덱스 작업을 트리거하는 쿼리를 실행하는 애플리케이션이 다음 조건을 충족해야 합니다.

- 데이터베이스 연결에서 Always Encrypted 및 enclave 계산을 모두 사용하는 데이터베이스에 연결합니다.
- 애플리케이션이 인덱싱된 열의 열 암호화 키를 보호하는 열 마스터 키에 액세스할 수 있어야 합니다.

SQL Server 엔진이 애플리케이션 쿼리를 구문 분석하고 쿼리를 실행하기 위해 암호화된 열의 인덱스를 업데이트해야 한다고 결정하면, 보안 채널을 통해 필요한 CEK를 enclave에 제공하도록 클라이언트 드라이버에 지시합니다. 인덱싱 작업을 포함하지 않는 쿼리 처리를 위해 enclave에 열 암호화 키를 제공하는 데 사용되는 것과 동일한 메커니즘입니다.

이 방법은 연결에 대해 Always Encrypted 및 enclave 계산을 사용하는 데이터베이스에 이미 연결되고 쿼리 처리에 enclave를 사용하는 애플리케이션에서 암호화된 열 인덱스의 현재 상태가 투명하도록 유지하는 데 유용합니다. 열에 인덱스를 만든 후, 앱 내부 드라이버가 인덱싱 작업을 위해 열 암호화 키를 enclave에 투명하게 제공합니다. 인덱스를 만드는 경우 애플리케이션이 열 암호화 키를 enclave로 보내야 하는 쿼리 수가 늘어날 수 있습니다.

이 방법을 사용하는 단계별 지침은 [자습서: 임의 암호화를 사용하는 Enclave 사용 열에 인덱스 만들기 및 사용](../tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md)을 참조하세요.

### <a name="invoke-indexing-operations-using-cached-column-encryption-keys"></a>캐시된 열 암호화 키를 사용하여 인덱싱 작업 호출

enclave 계산이 필요한 쿼리 처리를 위해 클라이언트 애플리케이션이 열 암호화 키를 enclave로 보내면 enclave는 enclave 내부에 있고 외부에서 액세스할 수 없는 내부 캐시에 열 암호화 키를 캐시합니다.

같거나 다른 사용자가 사용하는 같거나 다른 클라이언트 애플리케이션이 필요한 열 암호화를 직접 제공하지 않고 인덱스 작업을 트리거하면 enclave는 캐시에서 열 암호화 키를 조회합니다. 그 결과, 클라이언트 애플리케이션이 키를 제공하지 않았지만 인덱스 작업이 성공합니다.

인덱싱 작업을 호출하는 이 방법이 성공하려면 애플리케이션이 연결에 대해 Always Encrypted를 사용하지 않는 데이터베이스에 연결되어야 하고, enclave 내부 캐시에서 필요한 열 암호화 키를 사용할 수 있어야 합니다.

작업을 호출하는 이 방법은 인덱스와 관련이 없는 다른 작업에는 열 암호화 키가 필요 없는 쿼리에 대해서만 지원됩니다. 예를 들어 INSERT 문을 사용하여 암호화된 열을 포함하는 테이블에 행을 삽입하는 애플리케이션은 연결 문자열에서 Always Encrypted를 사용하는 데이터베이스에 연결되어야 하며, 암호화된 열에 인덱스가 있는지 여부와 관계없이 키에 액세스할 수 있어야 합니다.

이 방법은 다음과 같은 경우에 유용합니다.

- 일반 텍스트로 키와 데이터에 액세스할 수 없는 애플리케이션 및 사용자에게 임의 암호화를 사용한 enclave 사용 열 인덱스의 현재 상태가 투명하도록 유지합니다. 암호화된 열에 인덱스를 만들어도 기존 쿼리가 중단되지 않도록 합니다. 즉, 애플리케이션이 키에 액세스하지 않고도 암호화된 열을 포함하는 테이블에 대해 쿼리를 실행하는 경우 DBA가 인덱스를 만든 후에도 키에 액세스하지 않고 애플리케이션에서 계속 실행할 수 있습니다. 예를 들어 DBA가 암호화된 열에 인덱스를 만들기 전에 이전 예제에서 사용된 **Employees** 테이블에 대해 아래 쿼리를 실행하는 애플리케이션이 있다고 가정해 보세요. 

   ```sql
   DELETE FROM [dbo].[Employees] WHERE [EmployeeID] = 1;
   GO
   ```

   애플리케이션이 Always Encrypted 및 enclave 계산을 사용하지 않는 연결을 통해 쿼리를 제출하는 경우, 암호화된 열의 계산을 트리거하지 않으므로 쿼리가 성공합니다. DBA가 암호화된 열에 인덱스를 만든 후에는 쿼리로 인해 enclave에 열 암호화 키가 필요한 인덱스에서 인덱스 키 제거가 트리거됩니다. 그러나 데이터 소유자가 enclave에 열 암호화 키를 제공한 경우 애플리케이션이 동일한 연결을 통해 이 쿼리를 계속 실행할 수 있습니다.

- DBA가 중요한 데이터에 액세스하지 않고도 암호화된 열에 인덱스를 만들고 변경할 수 있기 때문에 인덱스를 관리할 때 역할을 구분합니다. 

이 방법을 사용하는 단계별 지침은 [자습서: 임의 암호화를 사용하는 Enclave 사용 열에 인덱스 만들기 및 사용](../tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md)을 참조하세요.

## <a name="develop-applications-issuing-rich-queries-in-visual-studio"></a>Visual Studio에서 리치 쿼리를 실행하는 애플리케이션 개발

### <a name="set-up-your-visual-studio-project"></a>Visual Studio 프로젝트 설정

.NET Framework 애플리케이션에서 보안 Enclave를 사용한 Always Encrypted를 사용하려면 .NET Framework 4.7.2에서 애플리케이션을 빌드하고 [Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders NuGet](https://www.nuget.org/packages/Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders)에 통합해야 합니다. 또한 열 마스터 키를 Azure Key Vault에 저장하는 경우에도 애플리케이션을 [Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider NuGet](https://www.nuget.org/packages/Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider) 버전 2.2.0 이상에 통합해야 합니다. 

1. Visual Studio를 엽니다.
2. 새 Visual C\# 프로젝트를 만들거나 기존 프로젝트를 엽니다.
3. 프로젝트가 .NET Framework 4.7.2 이상을 대상으로 하는지 확인합니다. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 속성을 선택한 후 대상 프레임워크를 .NET Framework 4.7.2로 설정합니다.

4. **도구** (주 메뉴) > **NuGet 패키지 관리자** > **패키지 관리자 콘솔**로 이동하여 다음 NuGet 패키지를 설치합니다. 패키지 관리자 콘솔에서 다음 코드를 실행합니다.

   ```powershell
   Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders -IncludePrerelease
   ```

5. 열 마스터 키를 저장하는 데 Azure Key Vault를 사용하는 경우 **도구** (주 메뉴) > **NuGet 패키지 관리자** > **패키지 관리자 콘솔**로 이동하여 다음 NuGet 패키지를 설치합니다. 패키지 관리자 콘솔에서 다음 코드를 실행합니다.

   ```powershell
   Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider -IncludePrerelease -Version 2.2.0
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```

6. 프로젝트를 선택하고 설치를 클릭합니다.
7. 프로젝트에서 구성 파일(예: App.config 또는 Web.config)을 엽니다.
8. \<구성\> 섹션을 찾아 \<configsections\> 섹션을 추가하거나 업데이트합니다.

   1\. \<구성\> 섹션에 \<configsections\> 섹션이 포함되어 있지 **않으면** \<구성\> 바로 아래 있는 다음 콘텐츠를 추가합니다.
   
      ```xml
      <configSections>
         <section name="SqlColumnEncryptionEnclaveProviders" type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
      </configSections>
      ```
   2\. \<구성\> 섹션에 이미 \<configsections\> 섹션이 있는 경우 \<configsections\> 내에 다음 줄을 추가합니다.

   ```xml
   <section name="SqlColumnEncryptionEnclaveProviders"  type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data,  Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" /\>
   ```

9. 구성 섹션 내의 \<configSections\> 아래에서 VBS Enclave를 증명하고 상호 작용하는 데 사용할 Enclave 공급자를 지정하는 다음 섹션을 추가합니다.

   ```xml
   <SqlColumnEncryptionEnclaveProviders>
       <providers>
           <add name="VBS"  type="Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders.VirtualizationBasedSecurityEnclaveProvider,  Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders,    Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91"/>
       </providers>
   </SqlColumnEncryptionEnclaveProviders>
   ```

다음은 간단한 콘솔 애플리케이션에 대한 app.config 파일의 전체 예제입니다.
```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <configSections>
    <section name="SqlColumnEncryptionEnclaveProviders" type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
  </configSections>
  <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.7.2" />
    </startup>

  <SqlColumnEncryptionEnclaveProviders>
    <providers>
      <add name="VBS" type="Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders.HostGuardianServiceEnclaveProvider, Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" />
    </providers>
  </SqlColumnEncryptionEnclaveProviders>
</configuration>
```
### <a name="develop-and-test-your-app"></a>앱 개발 및 테스트

Always Encrypted 및 enclave 계산을 사용하려면 애플리케이션이 연결 문자열`Column Encryption Setting = Enabled; Enclave Attestation Url=https://x.x.x.x/Attestation`(여기서 xxxx는 ip, 도메인 등일 수 있음)에 다음 두 개의 키워드를 사용해서 데이터베이스에 연결해야 합니다.

또한 애플리케이션은 Always Encrypted를 사용하여 애플리케이션에 적용되는 일반 지침을 준수해야 합니다. 예를 들어, 애플리케이션은 애플리케이션 쿼리에서 참조되는 데이터베이스 열과 관련된 열 마스터 키에 액세스할 수 있어야 합니다.

Always Encrypted를 사용하여 .NET Framework 애플리케이션을 개발하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.

- [.NET Framework 데이터 공급자와 Always Encrypted를 사용하여 개발](develop-using-always-encrypted-with-net-framework-data-provider.md)
- [Always Encrypted: SQL Database의 중요한 데이터 보호 및 Azure Key Vault에 암호화 키 저장](https://docs.microsoft.com/azure/sql-database/sql-database-always-encrypted)

#### <a name="example-of-simple-application"></a>간단한 애플리케이션 예제

아래 코드는 다음 스키마를 사용하여 테이블에 대해 LIKE 쿼리를 실행하는 C\# 콘솔 앱의 간단한 예제입니다.

```sql
CREATE TABLE [dbo].[Employees]
(
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [SSN] [char](11) ENCRYPTED WITH (
        COLUMN_ENCRYPTION_KEY = [CEK1],
        ENCRYPTION_TYPE = Randomized,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [Salary] [money] ENCRYPTED WITH (
        COLUMN_ENCRYPTION_KEY = [CEK1],
        ENCRYPTION_TYPE = Randomized,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
    CONSTRAINT [PK_dbo.Employees] PRIMARY KEY CLUSTERED (
[EmployeeID] ASC
)
) ON [PRIMARY];
GO
```

CEK1은 Enclave 사용 열 암호화 키로 간주됩니다.

```cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Data.SqlClient;
using System.Data;
namespace ConsoleApp1
{
   class Program
   {
      static void Main(string\[\] args)
   {

   string connectionString = "Data Source = myserver; Initial Catalog = ContosoHR; Column Encryption Setting = Enabled;Enclave Attestation Url = https://10.193.16.185/Attestation/attestationservice.svc/signingCertificates; Integrated Security = true";

using (SqlConnection connection = new SqlConnection(connectionString))
{
   connection.Open();
   
   SqlCommand cmd = connection.CreateCommand();
   cmd.CommandText = @"SELECT [SSN], [FirstName], [LastName], [Salary] FROM [dbo].[Employees] WHERE [SSN] LIKE @SSNPattern AND [Salary] > @MinSalary;";
   
   SqlParameter paramSSNPattern = cmd.CreateParameter();
   
   paramSSNPattern.ParameterName = @"@SSNPattern";
   paramSSNPattern.DbType = DbType.AnsiStringFixedLength;
   paramSSNPattern.Direction = ParameterDirection.Input;
   paramSSNPattern.Value = "%1111";
   paramSSNPattern.Size = 11;
   
   cmd.Parameters.Add(paramSSNPattern);
   
   SqlParameter MinSalary = cmd.CreateParameter();
   
   MinSalary.ParameterName = @"@MinSalary";
   MinSalary.DbType = DbType.Currency;
   MinSalary.Direction = ParameterDirection.Input;
   MinSalary.Value = 900;
   
   cmd.Parameters.Add(MinSalary);
   cmd.ExecuteNonQuery();
   
   SqlDataReader reader = cmd.ExecuteReader();
   while (reader.Read())
   
   {
     Console.WriteLine(reader);
     Console.WriteLine(reader\[0\] + ", " + reader\[1\] + ", " + reader\[2\] + ", " + reader\[3\]);
   }

   Console.ReadKey();

   }
  }
 }
}
```
