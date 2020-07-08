---
title: PowerShell Core를 사용하여 SQL Server on Linux 관리
description: 이 문서에서는 SQL Server on Linux와 함께 PowerShell Core를 사용하는 방법을 간략히 설명합니다.
ms.date: 04/22/2019
ms.prod: sql
ms.technology: linux
ms.topic: conceptual
author: SQLvariant
ms.author: aanelson
ms.reviewer: vanto
ms.openlocfilehash: 3f70d69e58d513abcba8f27bbda53ab09d5e00ab
ms.sourcegitcommit: 19ff45e8a2f4193fe8827f39258d8040a88befc7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2020
ms.locfileid: "83807654"
---
# <a name="manage-sql-server-on-linux-with-powershell-core"></a>PowerShell Core를 사용하여 SQL Server on Linux 관리

이 문서에서는 [SQL Server PowerShell](../powershell/sql-server-powershell.md)을 소개하고 macOS 및 Linux에서 PowerShell Core(PS Core)와 함께 사용하는 방법에 관한 몇 가지 예를 안내합니다. PowerShell Core는 현재 [GitHub](https://github.com/powershell/powershell)에 게시된 오픈 소스 프로젝트입니다.

## <a name="cross-platform-editor-options"></a>플랫폼 간 편집기 옵션

아래 PowerShell Core의 모든 단계는 일반 터미널에서 수행하거나 VS Code 또는 Azure Data Studio 내의 터미널에서 실행할 수 있습니다.  VS Code와 Azure Data Studio는 모두 macOS 및 Linux에서 사용할 수 있습니다.  Azure Data Studio에 대한 자세한 내용은 [이 빠른 시작](https://docs.microsoft.com/sql/azure-data-studio/quickstart-sql-server)을 참조하세요.  [PowerShell 확장](https://docs.microsoft.com/sql/azure-data-studio/powershell-extension)을 사용할 수도 있습니다.

## <a name="installing-powershell-core"></a>PowerShell Core 설치

지원되는 다양한 실험적 플랫폼에서 PowerShell Core를 설치하는 방법에 관한 자세한 내용은 다음 문서를 참조하세요.

- [Windows에서 PowerShell Core 설치](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-windows?view=powershell-6)
- [Linux에서 PowerShell Core 설치](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-linux?view=powershell-6)
- [macOS에서 PowerShell Core 설치](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-macos?view=powershell-6)
- [ARM에서 PowerShell Core 설치](https://docs.microsoft.com/powershell/scripting/install/powershell-core-on-arm?view=powershell-6)

## <a name="install-the-sqlserver-module"></a>SqlServer 모듈 설치

`SqlServer` 모듈은 [PowerShell 갤러리](https://www.powershellgallery.com/packages/SqlServer/)에서 유지 관리됩니다. SQL Server를 사용하는 경우 항상 최신 버전의 SqlServer PowerShell 모듈을 사용해야 합니다.

SqlServer 모듈을 설치하려면 PowerShell Core 세션을 열고 다음 코드를 실행합니다.

```powerhsell
Install-Module -Name SqlServer
```

PowerShell 갤러리에서 SqlServer 모듈을 설치하는 방법에 관한 자세한 내용은 이 [페이지](../powershell/download-sql-server-ps-module.md)를 참조하세요.

## <a name="using-the-sqlserver-module"></a>SqlServer 모듈 사용

먼저 PowerShell Core를 시작합니다.  macOS 또는 Linux를 사용하는 경우 컴퓨터에서 ‘터미널 세션’  을 열고 **pwsh**를 입력하여 새 PowerShell Core 세션을 시작합니다.  Windows에서는 <kbd>Win</kbd>+<kbd>R</kbd>을 사용하고 `pwsh`를 입력하여 새 PowerShell Core 세션을 시작합니다.

```
pwsh
```

SQL Server는 **SqlServer**라는 PowerShell 모듈을 제공합니다. **SqlServer** 모듈을 사용하여 SQL Server 구성 요소(SQL Server 공급자 및 cmdlet)를 PowerShell 환경 또는 스크립트로 가져올 수 있습니다.

다음 명령을 복사하고 PowerShell 프롬프트에 붙여넣어 **SqlServer** 모듈을 현재 PowerShell 세션으로 가져옵니다.

```powershell
Import-Module SqlServer
```

PowerShell 프롬프트에 다음 명령을 입력하여 **SqlServer** 모듈을 올바르게 가져왔는지 확인합니다.

```powershell
Get-Module -Name SqlServer
```

PowerShell에서 다음 출력과 유사한 정보가 표시되어야 합니다.

```
ModuleType Version    Name          ExportedCommands
---------- -------    ----          ----------------
Script     21.1.18102 SqlServer     {Add-SqlAvailabilityDatabase, Add-SqlAvailabilityGroupList...
```

## <a name="connect-to-sql-server-and-get-server-information"></a>SQL Server에 연결 및 서버 정보 가져오기

다음 단계에는 PowerShell Core를 사용하여 Linux의 SQL Server 인스턴스에 연결하고 몇 가지 서버 속성을 표시합니다.

다음 명령을 복사하여 PowerShell 프롬프트에 붙여넣습니다. 이러한 명령을 실행하면 PowerShell에서 다음을 수행합니다.
- 인스턴스의 호스트 이름 또는 IP 주소를 입력하라는 대화 상자를 표시합니다.
- 자격 증명을 묻는 ‘PowerShell 자격 증명 요청’  대화 상자를 표시합니다. ‘SQL 사용자 이름’ 및 ‘SQL 암호’를 사용하여 Linux의 SQL Server 인스턴스에 연결할 수 있습니다.  
- **Get-SqlInstance** cmdlet을 사용하여 **서버**에 연결하고 몇 가지 속성을 표시합니다.

필요에 따라 `$serverInstance` 변수를 해당 SQL Server 인스턴스의 IP 주소나 호스트 이름으로 바꿀 수 있습니다.

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Connect to the Server and return a few properties
Get-SqlInstance -ServerInstance $serverInstance -Credential $credential
# done
```

PowerShell에서 다음 출력과 유사한 정보가 표시되어야 합니다.

```
Instance Name                   Version    ProductLevel UpdateLevel  HostPlatform HostDistribution
-------------                   -------    ------------ -----------  ------------ ----------------
your_server_instance            14.0.3048  RTM          CU13         Linux        Ubuntu
```

> [!NOTE]
> 이러한 값 중 아무것도 표시되지 않으면 대상 SQL Server 인스턴스에 연결되지 않았을 수 있습니다. 동일한 연결 정보를 사용하여 SQL Server Management Studio에서 연결할 수 있는지 확인합니다. 그런 다음 [connection troubleshooting recommendations](sql-server-linux-troubleshooting-guide.md#connection)(연결 문제 해결 권장 사항)를 검토합니다.

## <a name="using-the-sql-server-powershell-provider"></a>SQL Server PowerShell 공급자 사용

SQL Server 인스턴스에 연결하는 또 다른 옵션은 [SQL Server PowerShell 공급자](https://docs.microsoft.com/sql/powershell/sql-server-powershell-provider)를 사용하는 것입니다.  공급자를 사용하면 개체 탐색기에서 트리 구조를 탐색할 때처럼 SQL Server 인스턴스를 명령줄에서 탐색할 수 있습니다.  기본적으로 이 공급자는 도메인 계정이 액세스할 수 SQL Server 인스턴스를 연결 및 탐색하는 데 사용할 수 있는 `SQLSERVER:\`라는 PSDrive로 표시됩니다.  SQL Server on Linux의 Active Directory 인증을 설정하는 방법에 대한 자세한 내용은 [구성 단계](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-auth-overview#configuration-steps)를 참조하세요.

SQL Server PowerShell 공급자를 통해 SQL 인증을 사용할 수도 있습니다. 이렇게 하려면 `New-PSDrive` cmdlet을 사용하여 새 PSDrive을 만들고 연결할 적절한 자격 증명을 제공합니다.

아래 예제에서는 SQL 인증을 사용하여 새 PSDrive를 만드는 방법의 예를 보여 줍니다.

```powershell
# NOTE: We are reusing the values saved in the $credential variable from the above example.

New-PSDrive -Name SQLonDocker -PSProvider SqlServer -Root 'SQLSERVER:\SQL\localhost,10002\Default\' -Credential $credential
```

`Get-PSDrive` cmdlet을 실행하여 드라이브가 생성되었는지 확인할 수 있습니다.

```powershell
Get-PSDrive
```

새 PSDrive를 만들었으면 드라이브 탐색을 시작할 수 있습니다.

```powershell
dir SQLonDocker:\Databases
```

출력은 다음과 같습니다.  이 출력은 SSMS가 데이터베이스 노드에 표시하는 내용과 유사합니다.  즉, 시스템 데이터베이스가 아니라 사용자 데이터베이스를 표시합니다.

```powershell
Name                 Status           Size     Space  Recovery Compat. Owner
                                            Available  Model     Level
----                 ------           ---- ---------- -------- ------- -----
AdventureWorks2016   Normal      209.63 MB    1.31 MB Simple       130 sa
AdventureWorksDW2012 Normal      167.00 MB   32.47 MB Simple       110 sa
AdventureWorksDW2014 Normal      188.00 MB   78.10 MB Simple       120 sa
AdventureWorksDW2016 Normal      172.00 MB   74.76 MB Simple       130 sa
AdventureWorksDW2017 Normal      208.00 MB   40.57 MB Simple       140 sa
```

인스턴스의 모든 데이터베이스를 확인해야 하는 경우 `Get-SqlDatabase` cmdlet을 사용할 수 있습니다.

## <a name="get-databases"></a>데이터베이스 가져오기

알아야 하는 중요한 cmdlet은 `Get-SqlDatabase`입니다.  데이터베이스 또는 데이터베이스 내의 개체를 사용하는 많은 작업에서 `Get-SqlDatabase` cmdlet을 사용할 수 있습니다.  `-ServerInstance` 및 `-Database` 매개 변수의 값을 둘 다 제공하는 경우 해당 데이터베이스 개체 하나만 검색됩니다.  그러나 `-ServerInstance` 매개 변수만 지정하면 해당 인스턴스에 있는 모든 데이터베이스의 전체 목록이 반환됩니다.

```powershell
# NOTE: We are reusing the values saved in the $credential variable from the above example.

# Connect to the Instance and retrieve all databases
Get-SqlDatabase -ServerInstance ServerB -Credential $credential
```

위의 Get-SqlDatabase 명령에서 반환될 수 있는 항목의 샘플은 다음과 같습니다.

```powershell
Name                 Status           Size     Space  Recovery Compat. Owner
                                            Available  Model     Level
----                 ------           ---- ---------- -------- ------- -----
AdventureWorks2016   Normal      209.63 MB    1.31 MB Simple       130 sa
AdventureWorksDW2012 Normal      167.00 MB   32.47 MB Simple       110 sa
AdventureWorksDW2014 Normal      188.00 MB   78.10 MB Simple       120 sa
AdventureWorksDW2016 Normal      172.00 MB   74.88 MB Simple       130 sa
AdventureWorksDW2017 Normal      208.00 MB   40.63 MB Simple       140 sa
master               Normal        6.00 MB  600.00 KB Simple       140 sa
model                Normal       16.00 MB    5.70 MB Full         140 sa
msdb                 Normal       15.50 MB    1.14 MB Simple       140 sa
tempdb               Normal       16.00 MB    5.49 MB Simple       140 sa

```

## <a name="examine-sql-server-error-logs"></a>SQL Server 오류 로그 검사

다음 단계에서는 PowerShell Core를 사용하여 Linux의 SQL Server 인스턴스에서 오류 로그 연결을 검사합니다.

다음 명령을 복사하여 PowerShell 프롬프트에 붙여넣습니다. 명령을 실행하는 데 몇 분 정도 걸릴 수 있습니다. 이러한 명령은 다음 단계를 수행합니다.
- 인스턴스의 호스트 이름 또는 IP 주소를 입력하라는 대화 상자를 표시합니다.
- 자격 증명을 묻는 ‘PowerShell 자격 증명 요청’  대화 상자를 표시합니다. ‘SQL 사용자 이름’ 및 ‘SQL 암호’를 사용하여 Linux의 SQL Server 인스턴스에 연결할 수 있습니다.  
- **Get-SqlErrorLog** cmdlet을 사용하여 Linux의 SQL Server 인스턴스에 연결하고 **Yesterday** 이후의 오류 로그를 검색합니다.

필요에 따라 `$serverInstance` 변수를 SQL Server 인스턴스의 IP 주소나 호스트 이름으로 바꿀 수 있습니다.

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Retrieve error logs since yesterday
Get-SqlErrorLog -ServerInstance $serverInstance -Credential $credential -Since Yesterday
# done
```

## <a name="explore-cmdlets-currently-available-in-ps-core"></a>현재 PS Core에서 사용할 수 있는 cmdlet 살펴보기
SqlServer 모듈에는 현재 Windows PowerShell에서 사용할 수 있는 109개 cmdlet이 있지만 PSCore에서는 109개 중 62개만 사용할 수 있습니다. 현재 사용할 수 있는 62개 cmdlet의 전체 목록은 아래와 같습니다.  Sqlserver 모듈의 모든 cmdlet에 대한 자세한 설명서는 SqlServer [cmdlet reference](https://docs.microsoft.com/powershell/module/sqlserver/)(cmdlet 참조)를 참조하세요.

다음 명령을 실행하면 사용 중인 PowerShell 버전에서 사용할 수 있는 모든 cmdlet이 표시됩니다.

```powershell
Get-Command -Module SqlServer -CommandType Cmdlet |
Sort-Object -Property Noun |
SELECT Name
```

- ConvertFrom-EncodedSqlName
- ConvertTo-EncodedSqlName
- Get-SqlAgent
- Get-SqlAgentJob
- Get-SqlAgentJobHistory
- Get-SqlAgentJobSchedule
- Get-SqlAgentJobStep
- Get-SqlAgentSchedule
- Invoke-SqlAssessment
- Get-SqlAssessmentItem
- Remove-SqlAvailabilityDatabase
- Resume-SqlAvailabilityDatabase
- Add-SqlAvailabilityDatabase
- Suspend-SqlAvailabilityDatabase
- New-SqlAvailabilityGroup
- Set-SqlAvailabilityGroup
- Remove-SqlAvailabilityGroup
- Switch-SqlAvailabilityGroup
- Join-SqlAvailabilityGroup
- Revoke-SqlAvailabilityGroupCreateAnyDatabase
- Grant-SqlAvailabilityGroupCreateAnyDatabase
- New-SqlAvailabilityGroupListener
- Set-SqlAvailabilityGroupListener
- Add-SqlAvailabilityGroupListenerStaticIp
- Set-SqlAvailabilityReplica
- Remove-SqlAvailabilityReplica
- New-SqlAvailabilityReplica
- Set-SqlAvailabilityReplicaRoleToSecondary
- New-SqlBackupEncryptionOption
- Get-SqlBackupHistory
- Invoke-Sqlcmd
- New-SqlCngColumnMasterKeySettings
- Remove-SqlColumnEncryptionKey
- Get-SqlColumnEncryptionKey
- Remove-SqlColumnEncryptionKeyValue
- Add-SqlColumnEncryptionKeyValue
- Get-SqlColumnMasterKey
- Remove-SqlColumnMasterKey
- New-SqlColumnMasterKey
- Get-SqlCredential
- Set-SqlCredential
- New-SqlCredential
- Remove-SqlCredential
- New-SqlCspColumnMasterKeySettings
- Get-SqlDatabase
- Restore-SqlDatabase
- Backup-SqlDatabase
- Set-SqlErrorLog
- Get-SqlErrorLog
- New-SqlHADREndpoint
- Set-SqlHADREndpoint
- Get-SqlInstance
- Add-SqlLogin
- Remove-SqlLogin
- Get-SqlLogin
- Set-SqlSmartAdmin
- Get-SqlSmartAdmin
- Read-SqlTableData
- Write-SqlTableData
- Read-SqlViewData
- Read-SqlXEvent
- Convert-UrnToPath

## <a name="see-also"></a>참고 항목
- [SQL Server PowerShell](../relational-databases/scripting/sql-server-powershell.md)
