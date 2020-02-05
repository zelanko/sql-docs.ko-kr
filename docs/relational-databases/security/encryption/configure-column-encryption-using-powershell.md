---
title: PowerShell로 Always Encrypted를 사용하여 열 암호화 구성 | Microsoft Docs
ms.custom: ''
ms.date: 10/31/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
ms.assetid: 074c012b-cf14-4230-bf0d-55e23d24f9c8
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cc6f86a091f96f3d38bc4db7a5d5d2fde5462dce
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "73594383"
---
# <a name="configure-column-encryption-using-always-encrypted-with-powershell"></a>PowerShell로 Always Encrypted를 사용하여 열 암호화 구성
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

이 문서에서는 [SqlServer](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/set-sqlcolumnencryption) PowerShell 모듈의 *Set-SqlColumnEncryption* cmdlet을 사용하여 데이터베이스 열에 대한 대상 상시 암호화 구성을 설정하는 단계를 제공합니다. **Set-SqlColumnEncryption** cmdlet은 대상 데이터베이스의 스키마와 선택한 열에 저장된 데이터를 둘 다 수정합니다. 열에 지정된 대상 암호화 설정과 현재 암호화 구성에 따라 열에 저장된 데이터를 암호화, 다시 암호화 또는 암호 해독할 수 있습니다.

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

> [!NOTE]
> [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)]를 사용하고 SQL Server 인스턴스가 보안 Enclave로 구성된 경우 데이터베이스 외부로 데이터를 이동하지 않고도 바로 암호화 작업을 실행할 수 있습니다. [보안 enclave를 사용한 Always Encrypted를 이용하여 내부 열 암호화 구성](always-encrypted-enclaves-configure-encryption.md)을 참조하세요. PowerShell은 내부 암호화를 지원하지 않습니다.

::: moniker-end
SqlServer PowerShell 모듈의 Always Encrypted 지원에 대한 자세한 내용은 [PowerShell을 사용하여 Always Encrypted 구성](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)을 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항

대상 암호화 구성을 설정하려면 다음을 확인해야 합니다.
- 열 암호화 키가 데이터베이스에 구성되어 있어야 합니다(열을 암호화 또는 다시 암호화하는 경우). 자세한 내용은 [PowerShell을 사용하여 Always Encrypted 키 구성](../../../relational-databases/security/encryption/configure-always-encrypted-keys-using-powershell.md)을 참조하세요.
- PowerShell cmdlet을 실행하는 컴퓨터에서 암호화, 다시 암호화 또는 암호 해독하려는 각 열에 대한 열 마스터 키에 액세스할 수 있어야 합니다. 

## <a name="performance-and-availability-considerations"></a>성능 및 가용성 고려 사항

데이터베이스에 대해 지정된 대상 암호화 설정을 적용하기 위해 **Set-SqlColumnEncryption** cmdlet은 대상 테이블이 포함된 열에서 모든 데이터를 투명하게 다운로드하고, 데이터를 임시 테이블 집합에 다시 업로드하며(대상 암호화 설정 사용), 마지막으로 원래 테이블을 새 버전의 테이블로 바꿉니다. 기본 .NET Framework Data Provider for SQL Server는 다운로드 및/또는 업로드 시 대상 열의 현재 암호화 구성과 대상 열의 지정된 대상 암호화 설정에 따라 데이터를 암호화 및/또는 암호 해독합니다. 영향을 받는 테이블의 데이터 크기 및 네트워크 대역폭에 따라 데이터를 이동하는 데 오래 걸릴 수 있습니다.

**Set-SqlColumnEncryption** cmdlet은 대상 암호화 구성을 설정하는 두 가지 접근 방식(온라인 및 오프라인)을 지원합니다.

오프라인 접근 방식을 사용하는 경우 대상 테이블(및 대상 테이블과 관련된 모든 테이블, 예: 대상 테이블과 외래 키 관계가 있는 모든 테이블)을 사용하여 전체 작업 기간 동안 트랜잭션을 작성할 수 없습니다. 외래 키 제약 조건의 의미 체계(**CHECK** 또는 **NOCHECK**)는 오프라인 방법을 사용하는 경우 항상 유지됩니다.

온라인 접근 방식(SqlServer PowerShell 모듈 버전 21.x 이상 필요)을 사용하는 경우, 데이터를 복사 및 암호화, 암호 해독 또는 다시 암호화하는 작업이 증분적으로 수행됩니다. 애플리케이션이 마지막 반복을 제외하고 전체 데이터 이동 작업에서 대상 테이블에서 데이터를 읽고 쓸 수 있으며, 해당 기간은 사용자가 정의할 수 있는 **MaxDownTimeInSeconds** 매개 변수에 의해 제한됩니다. 데이터가 복사되는 동안 애플리케이션에서 적용할 수 있는 변경 내용을 검색하고 처리하기 위해 이 cmdlet은 대상 데이터베이스에서 [변경 내용 추적](../../track-changes/enable-and-disable-change-tracking-sql-server.md)을 지원합니다. 따라서 온라인 접근 방식은 오프라인 접근 방식보다 서버 쪽의 리소스를 더 많이 사용할 가능성이 높습니다. 온라인 접근 방식에서는 특히 쓰기 작업이 많은 워크로드가 데이터베이스에 대해 실행되는 경우 작업이 훨씬 오래 걸릴 수도 있습니다. 온라인 접근 방식은 한 번에 하나의 테이블을 암호화하는 데 사용될 수 있으며, 테이블에는 기본 키가 있어야 합니다. 기본적으로 외래 키 제약 조건은 애플리케이션에 대한 영향을 최소화하기 위해 **NOCHECK** 옵션으로 다시 만들어집니다. **KeepCheckForeignKeyConstraints** 옵션을 지정하여 외래 키 제약 조건의 의미 체계 유지를 적용할 수 있습니다. 

다음은 오프라인 접근 방식과 온라인 접근 방식을 선택하는 방법에 대한 지침입니다.

오프라인 접근 방식 사용:
- 작업 기간을 최소화하기 위해 
- 여러 테이블의 열을 동시에 암호화/암호 해독/다시 암호화하기 위해
- 대상 테이블에 기본 키가 없는 경우

온라인 접근 방식 사용:
- 애플리케이션에 대한 데이터베이스의 가동 중지 시간/사용 불가를 최소화합니다.

## <a name="security-considerations"></a>보안 고려사항

데이터베이스 열에 대한 암호화를 구성하는 데 사용되는 **Set-SqlColumnEncryption** cmdlet은 상시 암호화 키와 데이터베이스 열에 저장된 데이터를 둘 다 처리합니다. 따라서 보안 컴퓨터에서 cmdlet을 실행하는 것이 중요합니다. 데이터베이스가 SQL Server에 있는 경우 SQL Server 인스턴스를 호스트하는 컴퓨터 이외의 다른 컴퓨터에서 cmdlet을 실행합니다. 상시 암호화의 주요 목표는 데이터베이스 시스템이 손상된 경우에도 암호화된 중요한 데이터를 안전하게 보호하는 것이므로 SQL Server 컴퓨터에서 키 및/또는 중요한 데이터를 처리하는 PowerShell 스크립트를 실행하면 기능의 이점이 감소하거나 무효화될 수 있습니다.

Task  |아티클  |일반 텍스트 키/키 저장소 액세스  |데이터베이스 액세스   
---|---|---|---
1단계. PowerShell 환경을 시작하고 SqlServer 모듈을 가져옵니다. | [SqlServer 모듈 가져오기](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#importsqlservermodule) | 예 | 예
2단계. 서버 및 데이터베이스에 연결 | [데이터베이스에 연결](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase) | 예 | yes
3단계. 열 마스터 키(순환할 열 암호화 키 보호)가 Azure 주요 자격 증명 모음에 저장된 경우 Azure에 인증 | [Add-SqlAzureAuthenticationContext](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext) | yes | 예
4단계. 암호화, 다시 암호화 또는 암호 해독하려는 각 데이터베이스 열에 대해 하나씩 SqlColumnEncryptionSettings 개체 배열을 생성합니다. SqlColumnMasterKeySettings는 PowerShell의 메모리에 있는 개체입니다. 열에 대한 대상 암호화 체계를 지정합니다. | [New-SqlColumnEncryptionSettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionsettings) | 예 | 예
5단계. 이전 단계에서 만든 SqlColumnMasterKeySettings 개체 배열에 지정된 원하는 암호화 구성을 설정합니다. 열에 지정된 대상 설정과 현재 암호화 구성에 따라 열이 암호화, 다시 암호화 또는 암호 해독됩니다.| [Set-SqlColumnEncryption](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/set-sqlcolumnencryption)<br><br>**참고:** 이 단계는 시간이 오래 걸릴 수 있습니다. 선택한 접근 방식(온라인 또는 오프라인)에 따라 애플리케이션에서 전체 작업이나 일부 작업 중에 테이블에 액세스할 수 없게 됩니다. | yes | yes

## <a name="encrypt-columns-using-offline-approach---example"></a>오프라인 접근 방식을 사용한 열 암호화 - 예제

아래 예제에서는 두 열에 대한 대상 암호화 구성을 설정하는 방법을 보여 줍니다. 열이 암호화되어 있지 않으면 암호화됩니다. 열이 다른 키 및/또는 다른 암호화 유형을 사용하여 이미 암호화되어 있으면 암호가 해독된 다음 지정된 대상 키/유형으로 다시 암호화됩니다.


```PowerShell
# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
# Change the authentication method in the connection string, if needed.
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$database = Get-SqlDatabase -ConnectionString $connStr

# Encrypt the selected columns (or re-encrypt, if they are already encrypted using keys/encrypt types, different than the specified keys/types.
$ces = @()
$ces += New-SqlColumnEncryptionSettings -ColumnName "dbo.Patients.SSN" -EncryptionType "Deterministic" -EncryptionKey "CEK1"
$ces += New-SqlColumnEncryptionSettings -ColumnName "dbo.Patients.BirthDate" -EncryptionType "Randomized" -EncryptionKey "CEK1"
Set-SqlColumnEncryption -InputObject $database -ColumnEncryptionSettings $ces -LogFileDirectory .
```
 
## <a name="encrypt-columns-using-online-approach---example"></a>온라인 접근 방식을 사용한 열 암호화 - 예제

아래 예제에서는 온라인 접근 방식을 사용하여 두 열에 대한 대상 암호화 구성을 설정하는 방법을 보여 줍니다. 열이 암호화되어 있지 않으면 암호화됩니다. 열이 다른 키 및/또는 다른 암호화 유형을 사용하여 이미 암호화되어 있으면 암호가 해독된 다음 지정된 대상 키/유형으로 다시 암호화됩니다.

```PowerShell
# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
# Change the authentication method in the connection string, if needed.
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$database = Get-SqlDatabase -ConnectionString $connStr

# Encrypt the selected columns (or re-encrypt, if they are already encrypted using keys/encrypt types, different than the specified keys/types.
$ces = @()
$ces += New-SqlColumnEncryptionSettings -ColumnName "dbo.Patients.SSN" -EncryptionType "Deterministic" -EncryptionKey "CEK1"
$ces += New-SqlColumnEncryptionSettings -ColumnName "dbo.Patients.BirthDate" -EncryptionType "Randomized" -EncryptionKey "CEK1"
Set-SqlColumnEncryption -InputObject $database -ColumnEncryptionSettings $ces -UseOnlineApproach -MaxDowntimeInSeconds 180 -LogFileDirectory .
```
## <a name="decrypt-columns---example"></a>열 암호 해독 - 예제

다음 예제에서는 데이터베이스에서 현재 암호화된 모든 열의 암호를 해독하는 방법을 보여 줍니다.


```PowerShell
# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
# Change the authentication method in the connection string, if needed.
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$database = Get-SqlDatabase -ConnectionString $connStr

# Find all encrypted columns, and create a SqlColumnEncryptionSetting object for each column.
$ces = @()
$tables = $database.Tables
for($i=0; $i -lt $tables.Count; $i++){
    $columns = $tables[$i].Columns
    for($j=0; $j -lt $columns.Count; $j++) {
        if($columns[$j].isEncrypted) {
            $threeColPartName = $tables[$i].Schema + "." + $tables[$i].Name + "." + $columns[$j].Name 
            $ces += New-SqlColumnEncryptionSettings -ColumnName $threeColPartName -EncryptionType "Plaintext" 
        }
    }
}

# Decrypt all columns.
Set-SqlColumnEncryption -ColumnEncryptionSettings $ces -InputObject $database -LogFileDirectory .
```
 
## <a name="next-steps"></a>다음 단계
- [Always Encrypted를 사용하여 애플리케이션 개발](always-encrypted-client-development.md)

## <a name="see-also"></a>참고 항목  
 - [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
 - [Always Encrypted를 위한 키 관리 개요](overview-of-key-management-for-always-encrypted.md) 
 - [PowerShell을 사용하여 Always Encrypted 구성](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)
 - [Always Encrypted 마법사를 사용하여 열 암호화 구성](always-encrypted-wizard.md)
 - [DAC 패키지로 Always Encrypted를 사용하여 열 암호화 구성](configure-always-encrypted-using-dacpac.md)


