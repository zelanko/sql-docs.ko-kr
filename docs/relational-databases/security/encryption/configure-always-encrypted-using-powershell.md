---
title: PowerShell을 사용하여 상시 암호화 구성 | Microsoft 문서
ms.custom: ''
ms.date: 10/01/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
ms.assetid: 12f2bde5-e100-41fa-b474-2d2332fc7650
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5c90ea22849dd1d0437cdf058f639bbe546ccab9
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594412"
---
# <a name="configure-always-encrypted-using-powershell"></a>PowerShell을 사용하여 상시 암호화 구성
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

SqlServer PowerShell 모듈은 [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)를 구성하기 위한 cmdlet을 제공합니다.

## <a name="security-considerations-when-using-powershell-to-configure-always-encrypted"></a>PowerShell을 사용하여 Always Encrypted를 구성할 때의 보안 고려 사항

Always Encrypted의 주요 목표는 데이터베이스 시스템이 손상된 경우에도 암호화된 중요한 데이터를 안전하게 보호하는 것이므로 SQL Server 컴퓨터에서 키 또는 중요한 데이터를 처리하는 PowerShell 스크립트를 실행하면 기능의 이점이 감소하거나 무효화될 수 있습니다. 보안과 관련된 추가 권장 사항을 보려면 [키 관리에 대한 보안 고려 사항](overview-of-key-management-for-always-encrypted.md#security-considerations-for-key-management)을 참조하세요.

역할 구분이 있거나 없는 경우 모두 키 저장소에 실제 암호화 액세스 키에 대한 액세스 권한이 있는 사용자 및 데이터베이스에 대한 액세스 권한이 있는 사용자를 제어함으로써 PowerShell을 사용하여 Always Encrypted 키를 관리할 수 있습니다.

 추가 권장 사항을 보려면 [키 관리에 대한 보안 고려 사항](overview-of-key-management-for-always-encrypted.md#security-considerations-for-key-management)을 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항

SQL Server 인스턴스를 호스트하는 컴퓨터가 아닌 보안 컴퓨터에 [SqlServer 모듈](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/sqlserver) 을 설치합니다. PowerShell 갤러리에서 직접 모듈을 설치할 수 있습니다.  자세한 내용은 [다운로드](../../../ssms/download-sql-server-ps-module.md) 지침을 참조하세요.


## <a name="importsqlservermodule"></a> SqlServer 모듈 가져오기 

SqlServer 모듈을 로드하려면

1.  **Set-ExecutionPolicy** cmdlet을 사용하여 적절한 스크립트 실행 정책을 설정합니다.
2.  **Import-Module** cmdlet을 사용하여 SqlServer 모듈을 가져옵니다.

이 예제에서는 SqlServer 모듈을 로드합니다.

```
# Import the SQL Server Module.  
Import-Module "SqlServer" 
```

## <a name="connectingtodatabase"></a> 데이터베이스에 연결

상시 암호화 cmdlet 중 일부는 데이터베이스의 데이터 또는 메타데이터로 작업하므로 먼저 데이터베이스에 연결해야 합니다. SqlServer 모듈을 사용하여 상시 암호화를 구성할 때 데이터베이스에 연결하는 다음 두 가지 권장 방법이 있습니다. 
1. **Get-SqlDatabase** cmdlet을 사용하여 연결
2. SQL Server PowerShell 공급자를 사용하여 연결

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

### <a name="using-get-sqldatabase"></a>Get-SqlDatabase 사용
**Get-SqlDatabase** cmdlet을 사용하여 SQL Server 또는 Azure SQL Database의 데이터베이스에 연결할 수 있습니다. 이 cmdlet은 데이터베이스 개체를 반환합니다. 그러면 데이터베이스에 연결하는 cmdlet의 **InputObject** 매개 변수를 사용하여 이 개체를 전달할 수 있습니다. 

### <a name="using-sql-server-powershell"></a>SQL Server PowerShell 사용

```
# Import the SqlServer module
Import-Module "SqlServer"  

# Connect to your database
# Set the valid server name, database name and authentication keywords in the connection string
$serverName = "<Azure SQL server name>.database.windows.net"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Authentication = Active Directory Integrated"
$database = Get-SqlDatabase -ConnectionString $connStr

# List column master keys for the specified database.
Get-SqlColumnMasterKey -InputObject $database
```

또는 파이프를 사용할 수 있습니다.


```
$database | Get-SqlColumnMasterKey
```

### <a name="using-sql-server-powershell-provider"></a>SQL Server PowerShell 공급자 사용
[SQL Server PowerShell 공급자](../../../powershell/sql-server-powershell-provider.md)는 SQL Server 개체의 계층 구조를 파일 시스템 경로와 비슷한 경로로 표시합니다. SQL Server PowerShell에서 파일 시스템 경로를 탐색하는 데 일반적으로 사용되는 명령과 비슷한 Windows PowerShell 별칭을 사용하여 경로를 탐색할 수 있습니다. 대상 인스턴스와 데이터베이스로 이동하면 이후 cmdlet은 다음 예제와 같이 해당 데이터베이스를 대상으로 합니다. 

> [!NOTE]
> 이 데이터베이스 연결 방법은 SQL Server에서만 작동합니다(Azure SQL 데이터베이스에서는 지원되지 않음).

```
# Import the SqlServer module.
Import-Module "SqlServer"
# Navigate to the database in the remote instance.
cd SQLSERVER:\SQL\servercomputer\DEFAULT\Databases\yourdatabase
# List column master keys in the above database.
Get-SqlColumnMasterKey
```

 
또는 데이터베이스로 이동하는 대신 제네릭 **Path** 매개 변수를 사용하여 데이터베이스 경로를 지정할 수 있습니다.


```
# Import the SqlServer module.
Import-Module "SqlServer" 
# List column master keys for the specified database.
Get-SqlColumnMasterKey -Path SQLSERVER:\SQL\servercomputer\DEFAULT\Databases\yourdatabase
```
 
## <a name="always-encrypted-tasks-using-powershell"></a>PowerShell을 사용하는 상시 암호화 작업

- [PowerShell을 사용하여 Always Encrypted 키 프로비전](configure-always-encrypted-keys-using-powershell.md)
- [PowerShell을 사용하여 상시 암호화 키 순환](../../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-powershell.md)
- [PowerShell을 사용하여 Always Encrypted로 열 암호화, 다시 암호화 또는 암호 해독](configure-column-encryption-using-powershell.md)


##  <a name="aecmdletreference"></a> 상시 암호화 Cmdlet 참조

상시 암호화에 사용할 수 있는 PowerShell cmdlet은 다음과 같습니다.

|CMDLET |설명
|:---|:---
|**[Add-SqlAzureAuthenticationContext](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext)**   |Azure에 인증을 수행하고 인증 토큰을 획득합니다.
|**[Add-SqlColumnEncryptionKeyValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlcolumnencryptionkeyvalue)**   |데이터베이스의 기존 열 암호화 키 개체에 대한 새 암호화된 값을 추가합니다.
|**[Complete-SqlColumnMasterKeyRotation](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/complete-sqlcolumnmasterkeyrotation)**   |열 마스터 키 순환을 완료합니다.
|**[Get-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/get-sqlcolumnencryptionkey)** |데이터베이스에서 정의된 모든 열 암호화 키 개체를 반환하거나 지정된 이름을 가진 열 암호화 키 개체 하나를 반환합니다.
|**[Get-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/get-sqlcolumnmasterkey)** |데이터베이스에서 정의된 열 마스터 키 개체를 반환하거나 지정된 이름을 가진 열 마스터 키 개체 하나를 반환합니다.
|**[Invoke-SqlColumnMasterKeyRotation](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/invoke-sqlcolumnmasterkeyrotation)**   |열 마스터 키 순환을 시작합니다.
|**[New-SqlAzureKeyVaultColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlazurekeyvaultcolumnmasterkeysettings)**   |Azure 주요 자격 증명 모음에 저장된 비대칭 키를 설명하는 SqlColumnMasterKeySettings 개체를 만듭니다.
|**[New-SqlCngColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcngcolumnmasterkeysettings)**   |CNG(Cryptography Next Generation) API를 지원하는 키 저장소에 저장된 비대칭 키를 설명하는 SqlColumnMasterKeySettings 개체를 만듭니다.
|**[New-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkey)** |데이터베이스에 열 암호화 키 개체를 만듭니다.
|**[New-SqlColumnEncryptionKeyEncryptedValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkeyencryptedvalue)** |열 암호화 키의 암호화된 값을 생성합니다.
|**[New-SqlColumnEncryptionSettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionsettings)**   |CEK 및 암호화 유형을 포함하여 단일 열의 암호화에 대한 정보를 캡슐화하는 SqlColumnEncryptionSettings 개체를 만듭니다.
|**[New-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkey)** |데이터베이스에 열 마스터 키 개체를 만듭니다.
|**[New-SqlColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkeysettings)**|지정된 공급자 및 키 경로를 사용하여 열 마스터 키에 대한 SqlColumnMasterKeySettings 개체를 만듭니다.
|**[New-SqlCspColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcspcolumnmasterkeysettings)**   |CAPI(Cryptography API)를 지원하는 CSP(암호화 서비스 공급자)의 키 저장소에 저장된 비대칭 키를 설명하는 SqlColumnMasterKeySettings 개체를 만듭니다.
|**[Remove-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnencryptionkey)**   |데이터베이스에서 열 암호화 키 개체를 제거합니다.
|**[Remove-SqlColumnEncryptionKeyValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnencryptionkeyvalue)** |데이터베이스의 기존 열 암호화 키 개체에서 암호화된 값을 제거합니다.
|**[Remove-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnmasterkey)**   |데이터베이스에서 열 마스터 키 개체를 제거합니다.
|**[Set-SqlColumnEncryption](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/set-sqlcolumnencryption)**   |데이터베이스의 지정된 열을 암호화, 해독 또는 다시 암호화합니다.



## <a name="see-also"></a>참고 항목

- [항상 암호화](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted를 위한 키 관리 개요](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [SQL Server Management Studio를 사용하여 Always Encrypted 구성](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md)
- [Always Encrypted를 사용하여 애플리케이션 개발](always-encrypted-client-development.md)