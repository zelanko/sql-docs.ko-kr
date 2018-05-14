---
title: PowerShell을 사용하여 Always Encrypted 키 순환 | Microsoft 문서
ms.custom: ''
ms.date: 05/17/2017
ms.prod: sql
ms.prod_service: security, sql-database"
ms.reviewer: ''
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5117b4fd-c8d3-48d5-87c9-756800769f31
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 0b16ad6c18bec1954d9c52ada5fd22202e3ff9da
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="rotate-always-encrypted-keys-using-powershell"></a>PowerShell을 사용하여 상시 암호화 키 순환
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

이 문서에서는 SqlServer PowerShell 모듈을 사용하여 상시 암호화 키를 순환하는 단계를 제공합니다. 상시 암호화에 SqlServer PowerShell 모듈을 사용 시작하는 방법은 [PowerShell을 사용하여 상시 암호화 구성](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)을 참조하세요.

상시 암호화 키 순환은 기존 키를 새 키로 교체하는 프로세스입니다. 키가 손상된 경우 또는 암호화 키를 정기적으로 순환하도록 요구하는 조직의 정책이나 규정 준수 규칙을 준수하기 위해 키를 순환해야 할 수 있습니다. 

상시 암호화는 두 가지 유형의 키를 사용하므로 열 마스터 키 순환과 열 암호화 키 순환이라는 두 개의 상위 수준 키 순환 워크플로가 있습니다.

* **열 암호화 키 순환** - 현재 키로 암호화된 데이터의 암호를 해독하고 새 열 암호화 키를 사용하여 데이터를 다시 암호화합니다. 열 암호화 키를 순환하려면 키와 데이터베이스 둘 다에 액세스해야 하므로 열 암호화 키 순환은 역할이 구분되지 않는 경우에만 수행할 수 있습니다.
* **열 마스터 키 순환** - 현재 열 마스터 키로 보호된 열 암호화 키의 암호를 해독하고 새 열 마스터 키를 사용하여 다시 암호화한 다음 두 유형의 키에 대한 메타데이터를 모두 업데이트합니다. 열 마스터 키 순환은 역할 구분에 관계없이 완료할 수 있습니다(SqlServer PowerShell 모듈 사용 시).


## <a name="column-master-key-rotation-without-role-separation"></a>역할 구분을 사용하지 않는 열 마스터 키 순환
이 섹션에서 설명하는 열 마스터 키 순환 방법은 보안 관리자와 DBA 간의 역할 구분을 지원하지 않습니다. 아래 단계 중 일부에서는 물리적 키에 대한 작업을 키 메타데이터에 대한 작업과 결합하므로, 이 워크플로는 DevOps 모델을 사용하는 조직이나 데이터베이스가 클라우드에서 호스트되고 클라우드 관리자(온-프레미스 DBA 아님)가 중요한 데이터에 액세스할 수 없도록 제한하는 것이 주요 목표인 경우에 권장됩니다. 잠재적인 악의적 사용자가 DBA에 포함되거나 또는 DBA가 중요한 데이터에 쉽게 액세스해서는 안 될 경우에는 권장되지 않습니다.  


| 태스크 | 아티클 | 일반 텍스트 키/키 저장소 액세스| 데이터베이스 액세스
|:---|:---|:---|:---
|1단계. 키 저장소에 새 열 마스터 키를 만듭니다.<br><br>**참고:** SqlServer PowerShell 모듈은 이 단계를 지원하지 않습니다. 명령줄에서 이 작업을 수행하려면 키 저장소와 관련된 도구를 사용해야 합니다. | 열 마스터 키 만들기 및 저장(상시 암호화)| 예 | 아니오
|2단계. PowerShell 환경을 시작하고 SqlServer 모듈을 가져옵니다. | [SqlServer 모듈 가져오기](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#importsqlservermodule) | 아니오 | 아니오
|3단계. 서버 및 데이터베이스에 연결합니다. | [데이터베이스에 연결](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase) | 아니오 | 예
|4단계. 새 열 마스터 키의 위치에 대한 정보가 포함된 SqlColumnMasterKeySettings 개체를 만듭니다. SqlColumnMasterKeySettings는 PowerShell의 메모리에 있는 개체입니다. 개체를 만들려면 키 저장소에 관련된 cmdlet을 사용해야 합니다. |[New-SqlAzureKeyVaultColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlazurekeyvaultcolumnmasterkeysettings)<br><br>[New-SqlCertificateStoreColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcertificatestorecolumnmasterkeysettings)<br><br>[New-SqlCngColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcngcolumnmasterkeysettings)<br><br>[New-SqlCspColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcspcolumnmasterkeysettings)<br> | 아니오 | 아니오
|5단계. 데이터베이스에 새 열 마스터 키에 대한 메타데이터를 만듭니다. | [New-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkey)<br><br>**참고:** 내부적으로 이 cmdlet은 [CREATE COLUMN MASTER KEY(TRANSACT-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) 문을 실행하여 키 메타데이터를 만듭니다. | 아니오 | 예
|6단계. 현재 열 마스터 키 또는 새 열 마스터 키가 Azure 주요 자격 증명 모음에 저장된 경우 Azure에 인증합니다. | [Add-SqlAzureAuthenticationContext](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext) | 예 | 아니오
|7단계. 이전 열 마스터 키로 현재 보호된 열 암호화 키를 각각 새 열 마스터 키로 암호화하여 순환을 시작합니다. 이 단계를 수행하면 영향을 받는 각 열 암호화 키(순환되는 이전 열 마스터 키와 연결됨)가 이전 열 마스터 키와 새 열 마스터 키 둘 다로 암호화되며 데이터베이스 메타데이터에 두 개의 암호화된 값이 포함됩니다.| [Invoke-SqlColumnMasterKeyRotation](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/invoke-sqlcolumnmasterkeyrotation) | 예 | 예
|8단계. 데이터베이스의 암호화된 열을 쿼리하며 이전 열 마스터 키로 보호된 모든 응용 프로그램의 관리자와 협력하여 응용 프로그램이 새 열 마스터 키에 액세스할 수 있도록 합니다.| [열 마스터 키 만들기 및 저장(Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md) | 예 | 아니오
|9단계. 순환을 완료합니다.<br><br>**참고:** 이 단계를 실행하기 전에 암호화된 열을 쿼리하며 이전 열 마스터 키로 보호된 모든 응용 프로그램이 새 열 마스터 키를 사용하도록 구성되었는지 확인합니다. 이 단계를 중간에 수행하면 해당 응용 프로그램 중 일부가 데이터 암호를 해독하지 못할 수 있습니다. 이전 열 마스터 키로 만든 데이터베이스에서 암호화된 값을 제거하여 순환을 완료합니다. 이렇게 하면 이전 열 마스터 키와 이 키가 보호하는 열 암호화 키 간의 연결이 제거됩니다. |[Complete-SqlColumnMasterKeyRotation](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/complete-sqlcolumnmasterkeyrotation)| 아니오 | 예
|10단계. 이전 열 마스터 키에서 메타데이터를 제거합니다. |[Remove-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnmasterkey)| 아니오 | 예

> [!NOTE]
> 순환 후에 이전 열 마스터 키를 영구적으로 삭제하지 않는 것이 좋습니다. 대신, 이전 열 마스터 키를 현재 키 저장소에 유지하거나 다른 안전한 장소에 보관해야 합니다. 백업 파일에서 새 열 마스터 키가 구성되기 *전의* 시점으로 데이터베이스를 복원하는 경우 데이터에 액세스하려면 이전 키가 필요합니다.

### <a name="rotating-a-column-master-key-without-role-separation-windows-certificate-example"></a>역할 구분을 사용하지 않는 열 마스터 키 순환(Windows 인증서 예제)

아래 스크립트는 기존 열 마스터 키(CMK1)를 새 열 마스터 키(CMK2)로 대체하는 종단 간 예제입니다.

```
# Create a new column master key in Windows Certificate Store.
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation Cert:CurrentUser\My -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage KeyEncipherment -KeySpec KeyExchange -KeyLength 2048

# Import the SqlServer module
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$connection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$connection.ConnectionString = $connStr
$connection.Connect()
$server = New-Object Microsoft.SqlServer.Management.Smo.Server($connection)
$database = $server.Databases[$databaseName]

# Create a SqlColumnMasterKeySettings object for your new column master key. 
$newCmkSettings = New-SqlCertificateStoreColumnMasterKeySettings -CertificateStoreLocation "CurrentUser" -Thumbprint $cert.Thumbprint

# Create metadata for your new column master key in the database.
$newCmkName = "CMK2"
New-SqlColumnMasterKey -Name $newCmkName -InputObject $database -ColumnMasterKeySettings $newCmkSettings

# Initiate the rotation from the current column master key to the new column master key.
$oldCmkName = "CMK1"
Invoke-SqlColumnMasterKeyRotation -SourceColumnMasterKeyName $oldCmkName -TargetColumnMasterKeyName $newCmkName -InputObject $database

# Complete the rotation of the old column master key.
Complete-SqlColumnMasterKeyRotation -SourceColumnMasterKeyName $oldCmkName  -InputObject $database

# Remove the old column master key metadata.
Remove-SqlColumnMasterKey -Name $oldCmkName -InputObject $database
```

## <a name="column-master-key-rotation-with-role-separation"></a>역할 구분을 사용하는 열 마스터 키 순환

이 섹션에서 설명하는 열 마스터 키 순환 워크플로는 보안 관리자와 DBA를 구분합니다.

> [!IMPORTANT]
> 아래 표에서 *일반 텍스트 키/키 저장소 액세스*=**예** 인 단계(일반 텍스트 키 또는 키 저장소에 액세스하는 단계)를 실행하기 전에 데이터베이스를 호스트하는 컴퓨터와 다른 보안 컴퓨터에서 PowerShell 환경이 실행하는지 확인합니다. 자세한 내용은 [키 관리에 대한 보안 고려 사항](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md#SecurityForKeyManagement)을 참조하세요.


### <a name="part-1-dba"></a>1부: DBA

DBA가 순환할 열 마스터 키 및 현재 열 마스터 키와 연결된 영향을 받는 열 암호화 키에 대한 메타데이터를 검색합니다. DBA는 이 모든 정보를 보안 관리자와 공유합니다.


| 태스크 | 아티클 | 일반 텍스트 키/키 저장소 액세스| 데이터베이스 액세스
|:---|:---|:---|:---
|1단계. PowerShell 환경을 시작하고 SqlServer 모듈을 가져옵니다. | [SqlServer 모듈 가져오기](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#importsqlservermodule) | 아니오 | InclusionThresholdSetting
|2단계. 서버 및 데이터베이스에 연결합니다. | [데이터베이스에 연결](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase) | 아니오 | 예
|3단계. 이전 열 마스터 키에 대한 메타데이터를 검색합니다.| [Get-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/get-sqlcolumnmasterkey) | 아니오 | 예
|4단계. 암호화된 값을 포함하여 이전 열 마스터 키로 보호된 열 암호화 키에 대한 메타데이터를 검색합니다. | [Get-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/get-sqlcolumnencryptionkey) | 아니오 | 예
|5단계. 열 마스터 키의 위치(열 마스터 키의 공급자 이름 및 키 경로)와 이전 열 마스터 키로 보호된 해당 열 암호화 키의 암호화된 값을 공유합니다.| 다음 예를 참조하십시오. | 아니오 | 아니오

### <a name="part-2-security-administrator"></a>2부: 보안 관리자

보안 관리자가 새 열 마스터 키를 생성하고, 영향을 받는 열 암호화 키를 새 열 마스터 키로 다시 암호화한 다음 새 열 마스터 키에 대한 정보 및 영향을 받는 열 암호화 키에 대해 새로 암호화된 값 집합을 DBA와 공유합니다.

| 태스크 | 아티클 | 일반 텍스트 키/키 저장소 액세스| 데이터베이스 액세스
|:---|:---|:---|:---
|1단계. 이전 열 마스터 키의 위치와 이전 열 마스터 키로 보호된 해당 열 암호화 키의 암호화된 값을 DBA로부터 얻습니다.|해당 사항 없음<br>다음 예를 참조하십시오.|아니오| 아니오
|2단계. 키 저장소에 새 열 마스터 키를 만듭니다.<br><br>**참고:** SqlServer 모듈은 이 단계를 지원하지 않습니다. 명령줄에서 이 태스크를 수행하려면 키 저장소의 유형에 관련된 도구를 사용해야 합니다.|[열 마스터 키 만들기 및 저장(Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)| 예 | 아니오
|3단계. PowerShell 환경을 시작하고 SqlServer 모듈을 가져옵니다. | [SqlServer 모듈 가져오기](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#importsqlservermodule) | 아니오 | 아니오
|4단계. **이전** 열 마스터 키의 위치에 대한 정보가 포함된 SqlColumnMasterKeySettings 개체를 만듭니다. SqlColumnMasterKeySettings는 PowerShell의 메모리에 있는 개체입니다. |New-SqlColumnMasterKeySettings| 아니오 | 아니오
|5단계. **새** 열 마스터 키의 위치에 대한 정보가 포함된 SqlColumnMasterKeySettings 개체를 만듭니다. SqlColumnMasterKeySettings는 PowerShell의 메모리에 있는 개체입니다. 개체를 만들려면 키 저장소에 관련된 cmdlet을 사용해야 합니다. | [New-SqlAzureKeyVaultColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlazurekeyvaultcolumnmasterkeysettings)<br><br>[New-SqlCertificateStoreColumnMasterKeySettings](https://msdn.microsoft.com/library/mt759816.aspx)<br><br>[New-SqlCngColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcngcolumnmasterkeysettings)<br><br>[New-SqlCspColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcspcolumnmasterkeysettings)| 아니오 | 아니오
|6단계. 이전(현재) 열 마스터 키 또는 새 열 마스터 키가 Azure 주요 자격 증명 모음에 저장된 경우 Azure에 인증합니다. | [Add-SqlAzureAuthenticationContext](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext) | 예 | 아니오
|7단계. 이전 열 마스터 키로 현재 보호된 열 암호화 키의 값을 각각 새 열 마스터 키로 다시 암호화합니다. | [New-SqlColumnEncryptionKeyEncryptedValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkeyencryptedvalue)<br><br>**참고:** 이 cmdlet을 호출할 때 다시 암호화할 열 암호화 키의 값과 함께 이전 열 마스터 키와 새 열 마스터 키 둘 다의 SqlColumnMasterKeySettings 개체를 전달합니다.|예|아니오
|8단계. 열 마스터 키의 위치(열 마스터 키의 공급자 이름 및 키 경로)와 열 암호화 키의 새로 암호화된 값 집합을 DBA와 공유합니다.| 다음 예를 참조하십시오. | 아니오 | 아니오

> [!NOTE]
> 순환 후에 이전 열 마스터 키를 영구적으로 삭제하지 않는 것이 좋습니다. 대신, 이전 열 마스터 키를 현재 키 저장소에 유지하거나 다른 안전한 장소에 보관해야 합니다. 백업 파일에서 새 열 마스터 키가 구성되기 *전의* 시점으로 데이터베이스를 복원하는 경우 데이터에 액세스하려면 이전 키가 필요합니다.


### <a name="part-3-dba"></a>3부: DBA

DBA가 새 열 마스터 키에 대한 메타데이터를 만들고 영향을 받는 열 암호화 키를 업데이트하여 새로 암호화된 값 집합을 추가합니다. 이 단계에서 DBA는 암호화 열을 쿼리하는 응용 프로그램의 관리자와도 협력합니다. 관리자는 응용 프로그램이 새 열 마스터 키에 액세스할 수 있는지 확인합니다. 모든 응용 프로그램이 새 열 마스터 키를 사용하도록 설정되면 DBA가 이전 암호화된 값 집합과 이전 열 마스터 키 메타데이터를 제거합니다.

| 태스크 | 아티클 | 일반 텍스트 키/키 저장소 액세스| 데이터베이스 액세스
|:---|:---|:---|:---
|1단계. 새 열 마스터 키의 위치와 이전 열 마스터 키로 보호된 해당 열 암호화 키의 새로 암호화된 값 집합을 보안 관리자로부터 얻습니다.| 다음 예를 참조하십시오. | 아니오 | 아니오
|2단계. PowerShell 환경을 시작하고 SqlServer 모듈을 가져옵니다. | [SqlServer 모듈 가져오기](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#importsqlservermodule) | 아니오 | 아니오
|3단계. 서버 및 데이터베이스에 연결합니다. | [데이터베이스에 연결](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase) | 아니오 | 예
|4단계. 새 열 마스터 키의 위치에 대한 정보가 포함된 SqlColumnMasterKeySettings 개체를 만듭니다. SqlColumnMasterKeySettings는 PowerShell의 메모리에 있는 개체입니다. |New-SqlColumnMasterKeySettings| 아니오| 아니오
|5단계. 데이터베이스에 새 열 마스터 키에 대한 메타데이터를 만듭니다.|[New-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkey)<br><br>**참고:** 내부적으로 이 cmdlet은 [CREATE COLUMN MASTER KEY(TRANSACT-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) 문을 실행하여 키 메타데이터를 만듭니다. | 아니오 | 예
|6단계. 이전 열 마스터 키로 보호된 열 암호화 키에 대한 메타데이터를 검색합니다.| [Get-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/get-sqlcolumnencryptionkey)| 아니오 | 예
|7단계. 새 열 마스터 키를 사용하여 생성된 새 암호화된 값을 영향을 받는 각 열 암호화 키에 대한 메타데이터에 추가합니다.|[Add-SqlColumnEncryptionKeyValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlcolumnencryptionkeyvalue)|아니오|예
|8단계. 데이터베이스의 암호화된 열을 쿼리하며 이전 열 마스터 키로 보호된 모든 응용 프로그램의 관리자와 협력하여 응용 프로그램이 새 열 마스터 키에 액세스할 수 있도록 합니다.|[열 마스터 키 만들기 및 저장(Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)| 아니오|아니오
|9단계. 이전 열 마스터 키와 연결된 암호화된 값을 데이터베이스에서 제거하여 순환을 완료합니다.<br><br>**참고:** 이 단계를 실행하기 전에 암호화된 열을 쿼리하며 이전 열 마스터 키로 보호된 모든 응용 프로그램이 새 열 마스터 키를 사용하도록 구성되었는지 확인합니다. 이 단계를 중간에 수행하면 해당 응용 프로그램 중 일부가 데이터 암호를 해독하지 못할 수 있습니다.<br><br>이 단계에서는 이전 열 마스터 키와 이 키가 보호하는 열 암호화 키 간의 연결을 제거합니다. | [Complete-SqlColumnMasterKeyRotation](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/complete-sqlcolumnmasterkeyrotation)<br><br>또는 [Remove-SqlColumnEncryptionKeyValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnencryptionkeyvalue)를 사용할 수 있습니다. | 아니오|예
|10단계. 이전 열 마스터 키 메타데이터를 데이터베이스에서 제거합니다.| [Remove-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnmasterkey)| 아니오|예

### <a name="rotating-a-column-master-key-with-role-separation-windows-certificate-example"></a>역할 구분을 사용하는 열 마스터 키 순환(Windows 인증서 예제)

아래 스크립트는 Windows 인증서 저장소의 인증서인 새 열 마스터 키를 생성하고 기존(현재) 열 마스터 키를 순환하여 새 열 마스터 키로 대체하는 종단 간 예제입니다. 스크립트에서는 대상 데이터베이스에 일부 열 암호화 키를 암호화하는 열 마스터 키 CMK1(순환됨)이 들어 있다고 가정합니다.

1부: DBA

```
# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$connection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$connection.ConnectionString = $connStr
$connection.Connect()
$server = New-Object Microsoft.SqlServer.Management.Smo.Server($connection)
$database = $server.Databases[$databaseName]

# Retrieve the data about the old column master key, which needs to be rotated.
$oldCmkName = "CMK1"
$oldCmk = Get-SqlColumnMasterKey -Name $oldCmkName -InputObject $database


# Share the location of the old column master key with a Security Administrator, via a CSV file on a share drive.
$oldCmkDataFile = "Z:\oldcmkdata.txt"
"KeyStoreProviderName, KeyPath" > $oldCmkDataFile
$oldCmk.KeyStoreProviderName +", " + $oldCmk.KeyPath >> $oldCmkDataFile


# Find column encryption keys associated with the old column master key and provide the encrypted values of column encryption keys to the Security Administrator, via a CSV file on a share drive.
$ceks = Get-SqlColumnEncryptionKey -InputObject $database
$oldCekValuesFile = "Z:\oldcekvalues.txt"
"CEKName, CEKEncryptedValue" > $oldCekValuesFile 
for($i=0; $i -lt $ceks.Length; $i++){
    if($ceks[$i].ColumnEncryptionKeyValues.Length -eq 2) {
        # This column encryption has 2 encrypted values - let's check, if it is associated with the old column master key.
        if($ceks[$i].ColumnEncryptionKeyValues[0].ColumnMasterKeyName -eq $oldCmkName -or $ceks[$i].ColumnEncryptionKeyValues[1].ColumnMasterKeyName -eq $oldCmkName) {
            Write-Host $ceks[$i].Name "already has 2 encrypted values and therefore" $oldCmkName + "cannot be rotated"
            exit 1
        }
    }
    if($ceks[$i].ColumnEncryptionKeyValues[0].ColumnMasterKeyName -eq $oldCmkName) {# This column encryption key has 1 encrypted value that was produced using the old column master key
        # Save the name and the encrypted value of the column encryption key in the file.
        $encryptedValue =  "0x" + -join ($ceks[$i].ColumnEncryptionKeyValues[0].EncryptedValue |  foreach {$_.ToString("X2") } )
        $ceks[$i].Name + "," + $encryptedValue >> $oldCekValuesFile
    }
} 
```


2부: 보안 관리자

```
# Obtain the location of the old column master key and the encrypted values of the corresponding column encryption keys, from your DBA, via a CSV file on a share drive.
$oldCmkDataFile = "Z:\oldcmkdata.txt"
$oldCmkData = Import-Csv $oldCmkDataFile
$oldCekValuesFile = "Z:\oldcekvalues.txt"
$oldCekValues = @(Import-Csv $oldCekValuesFile)

# Create a new column master key in Windows Certificate Store.
$storeLocation = "CurrentUser"
$certPath = "Cert:\" + $storeLocation + "\My"
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation $certPath -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage DataEncipherment -KeySpec KeyExchange

# Import the SqlServer module.
Import-Module "SqlServer"

# Create a SqlColumnMasterKeySettings object for your old column master key. 
$oldCmkSettings = New-SqlColumnMasterKeySettings -KeyStoreProviderName $oldCmkData.KeyStoreProviderName -KeyPath $oldCmkData.KeyPath

# Create a SqlColumnMasterKeySettings object for your new column master key. 
$newCmkSettings = New-SqlCertificateStoreColumnMasterKeySettings -CertificateStoreLocation $storeLocation -Thumbprint $cert.Thumbprint


# Prepare a CSV file, you will use to share the encrypted values of column encryption keys, produced using the new column master key.
$newCekValuesFile = "Z:\newcekvalues.txt"
"CEKName, CEKEncryptedValue" > $newCekValuesFile

# Re-encrypt each value with the new column master key and save the new encrypted value in the file.
for($i=0; $i -lt $oldCekValues.Count; $i++){
    # Re-encrypt each value with the new CMK
    $newValue = New-SqlColumnEncryptionKeyEncryptedValue -TargetColumnMasterKeySettings $newCmkSettings -ColumnMasterKeySettings $oldCmkSettings -EncryptedValue $oldCekValues[$i].CEKEncryptedValue
    $oldCekValues[$i].CEKName + ", " + $newValue >> $newCekValuesFile
}

# Share the new column master key data with your DBA, via a CSV file.
$newCmkDataFile = $home + "\newcmkdata.txt"
"KeyStoreProviderName, KeyPath" > $newCmkDataFile
$newCmkSettings.KeyStoreProviderName +", " + $newCmkSettings.KeyPath >> $newCmkDataFile
```


3부: DBA

```
# Obtain the location of the new column master key and the new encrypted values of the corresponding column encryption keys, from your Security Administrator, via a CSV file on a share drive.
$newCmkDataFile = "Z:\newcmkdata.txt"
$newCmkData = Import-Csv $newCmkDataFile
$newCekValuesFile = "Z:\newcekvalues.txt"
$newCekValues = @(Import-Csv $newCekValuesFile)

# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$connection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$connection.ConnectionString = $connStr
$connection.Connect()
$server = New-Object Microsoft.SqlServer.Management.Smo.Server($connection)
$database = $server.Databases[$databaseName]

# Create a SqlColumnMasterKeySettings object for your new column master key. 
$newCmkSettings = New-SqlColumnMasterKeySettings -KeyStoreProviderName $newCmkData.KeyStoreProviderName -KeyPath $newCmkData.KeyPath
# Create metadata for the new column master key in the database.
$newCmkName = "CMK2"
New-SqlColumnMasterKey -Name $newCmkName -InputObject $database -ColumnMasterKeySettings $newCmkSettings


# Get all CEK objects
$oldCmkName = "CMK1"
$ceks = Get-SqlColumnEncryptionKey -InputObject $database
for($i=0; $i -lt $ceks.Length; $i++){
    if($ceks[$i].ColumnEncryptionKeyValues.Length -eq 2) {# This column encryption key has 2 encrypted values. Let's check, if it is associated with the old CMK.
        if($ceks[$i].ColumnEncryptionKeyValues[0].ColumnMasterKeyName -eq $oldCmkName -or $ceks[$i].ColumnEncryptionKeyValues[1].ColumnMasterKeyName -eq $oldCmkName) {
            Write-Host $ceks[$i].Name "already has 2 encrypted values and therefore" $oldCmkName + "cannot be rotated"
            exit 1
        }
    }
    if($ceks[$i].ColumnEncryptionKeyValues[0].ColumnMasterKeyName -eq $oldCmkName) {
        # Find the corresponding new encrypted value, received from the Security Administrator.
        $newValueRow = ($newCekValues| Where-Object {$_.CEKName -eq $ceks[$i].Name }[0])
        # Update the column encryption key metadata object by adding the new encrypted value
        Add-SqlColumnEncryptionKeyValue -ColumnMasterKeyName $newCmkName -Name $ceks[$i].Name -EncryptedValue $newValueRow.CEKEncryptedValue -InputObject $database 
    }
}

# Complete the rotation of the current column master key.
Complete-SqlColumnMasterKeyRotation -SourceColumnMasterKeyName $oldCmkName  -InputObject $database

# Remove the old column master key.
Remove-SqlColumnMasterKey -Name $oldCmkName -InputObject $database
```


## <a name="rotating-a-column-encryption-key"></a>열 암호화 키 순환

열 암호화 키를 순환하려면 모든 열에서 순환할 키로 암호화된 데이터의 암호를 해독하고 새 열 암호화 키를 사용하여 데이터를 다시 암호화해야 합니다. 이 순환 워크플로에서는 키와 데이터베이스 둘 다에 액세스해야 하므로 역할 구분을 사용하여 수행할 수 없습니다. 순환할 키로 암호화된 열을 포함하는 테이블이 크면 열 암호화 키를 순환하는 데 시간이 오래 걸릴 수 있습니다. 따라서 조직에서 열 암호화 키 순환을 계획할 때는 주의해야 합니다.

오프라인 또는 온라인 접근 방식을 사용하여 열 암호화 키를 회전할 수 있습니다. 오프라인 방식은 더 빠를 수 있지만 응용 프로그램이 영향을 받는 테이블에 쓸 수 없습니다. 온라인 방식은 시간이 더 오래 걸릴 수 있지만 영향을 받는 테이블을 응용 프로그램에 사용할 수 없는 시간 간격을 제한할 수 있습니다. 자세한 내용은 [PowerShell을 사용하여 열 암호화 구성](../../../relational-databases/security/encryption/configure-column-encryption-using-powershell.md) 및 [Set-SqlColumnEncryption](https://msdn.microsoft.com/library/mt759790.aspx) 을 참조하세요.

| 태스크 | 아티클 | 일반 텍스트 키/키 저장소 액세스| 데이터베이스 액세스
|:---|:---|:---|:---
|1단계. PowerShell 환경을 시작하고 SqlServer 모듈을 가져옵니다. | [SqlServer 모듈 가져오기](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#importsqlservermodule) | 아니오 | 아니오
|2단계. 서버 및 데이터베이스에 연결합니다. | [데이터베이스에 연결](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase) | 아니오 | 예
|3단계. 열 마스터 키(순환할 열 암호화 키 보호)가 Azure 주요 자격 증명 모음에 저장된 경우 Azure에 인증합니다. | [Add-SqlAzureAuthenticationContext](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext) | 예 | 아니오
|4단계. 새 열 암호화 키를 생성하고 열 마스터 키로 암호화하고 데이터베이스에 열 암호화 키 메타데이터를 만듭니다.  | [New-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkey)<br><br>**참고:** 내부적으로 열 암호화 키를 생성하고 암호화하는 cmdlet 변형을 사용합니다.<br>내부적으로 이 cmdlet은 [CREATE COLUMN ENCRYPTION KEY(Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md) 문을 실행하여 키 메타데이터를 만듭니다. | 예 | 예
|5단계. 이전 열 암호화 키로 암호화된 열을 모두 찾습니다. | [SMO(SQL Server 관리 개체) 프로그래밍 가이드](../../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md) | 아니오 | 예
|6단계. 영향을 받는 각 열에 대한 *SqlColumnEncryptionSettings* 개체를 만듭니다.  SqlColumnMasterKeySettings는 PowerShell의 메모리에 있는 개체입니다. 열에 대한 대상 암호화 체계를 지정합니다. 이 경우 개체는 영향을 받는 열을 새 열 암호화 키로 암호화하도록 지정해야 합니다. | [New-SqlColumnEncryptionSettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkeysettings) | 아니오 | 아니오
|7단계. 5단계에서 확인된 열을 새 열 암호화 키로 다시 암호화합니다. | [Set-SqlColumnEncryption](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/set-sqlcolumnencryption)<br><br>**참고:** 이 단계는 시간이 오래 걸릴 수 있습니다. 선택한 접근 방식(온라인 또는 오프라인)에 따라 응용 프로그램이 전체 작업 또는 그 일부를 통해 테이블에 액세스할 수 없게 됩니다. | 예 | 예
|8단계. 이전 열 암호화 키에 대한 메타데이터를 제거합니다. | [Remove-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnencryptionkey) | 아니오 | 예

### <a name="example---rotating-a-column-encryption-key"></a>예제 - 열 암호화 키 순환

아래 스크립트는 열 암호화 키 순환을 보여 줍니다.  스크립트에서는 대상 데이터베이스에 CEK1(순환됨)이라는 열 암호화 키로 암호화된 일부 열이 있다고 가정합니다. 이 키는 CMK1이라는 열 마스터 키를 사용하여 보호됩니다(열 마스터 키는 Azure 주요 자격 증명 모음에 저장되지 않음).


```
# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$connection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$connection.ConnectionString = $connStr
$connection.Connect()
$server = New-Object Microsoft.SqlServer.Management.Smo.Server($connection)
$database = $server.Databases[$databaseName]

# Generate a new column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cmkName = "CMK1"
$newCekName = "CEK2"
New-SqlColumnEncryptionKey -Name $newCekName -InputObject $database -ColumnMasterKey $cmkName 


# Find all columns encrypted with the old column encryption key, and create a SqlColumnEncryptionSetting object for each column.
$ces = @()
$oldCekName = "CEK1"
$tables = $database.Tables
for($i=0; $i -lt $tables.Count; $i++){
    $columns = $tables[$i].Columns
    for($j=0; $j -lt $columns.Count; $j++) {
        if($columns[$j].isEncrypted -and $columns[$j].ColumnEncryptionKeyName -eq $oldCekName) {
            $threeColPartName = $tables[$i].Schema + "." + $tables[$i].Name + "." + $columns[$j].Name 
            $ces += New-SqlColumnEncryptionSettings -ColumnName $threeColPartName -EncryptionType $columns[$j].EncryptionType -EncryptionKey $newCekName
        }
     }
}

# Re-encrypt all columns, currently encrypted with the old column encryption key, using the new column encryption key.
Set-SqlColumnEncryption -ColumnEncryptionSettings $ces -InputObject $database -UseOnlineApproach -MaxDowntimeInSeconds 120 -LogFileDirectory .

# Remove the old column encryption key metadata.
Remove-SqlColumnEncryptionKey -Name $oldCekName -InputObject $database
```


  
## <a name="next-steps"></a>Next Steps  
    
- [.NET Framework Data Provider for SQL Server와 Always Encrypted를 사용하여 응용 프로그램 개발](../../../relational-databases/security/encryption/always-encrypted-client-development.md)
  
## <a name="additional-resources"></a>추가 리소스  

- [Always Encrypted를 위한 키 관리 개요](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [PowerShell을 사용하여 Always Encrypted 구성](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)    
- [Always Encrypted(데이터베이스 엔진)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted 블로그](https://blogs.msdn.microsoft.com/sqlsecurity/tag/always-encrypted/)

