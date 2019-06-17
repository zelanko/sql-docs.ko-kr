---
title: PowerShell Core를 사용 하 여 Linux에서 SQL Server 관리 | Microsoft Docs
description: 이 문서에서는 Linux의 SQL Server를 사용 하 여 PowerShell Core를 사용 하는 개요를 제공 합니다.
ms.date: 04/22/2019
ms.reviewer: jroth
ms.prod: sql
ms.technology: linux
ms.topic: conceptual
author: SQLvariant
ms.author: aanelson
manager: craigg
ms.openlocfilehash: 242e3ab70d41df4d774400034f361b31289d97c9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66713148"
---
# <a name="manage-sql-server-on-linux-with-powershell-core"></a>PowerShell Core를 사용 하 여 Linux에서 SQL Server 관리

이 문서에서는 소개 [SQL Server PowerShell](../powershell/sql-server-powershell.md) macOS 및 Linux에서 PowerShell Core (PS 코어)를 사용 하 여 사용 하는 방법에 대 한 예제 가지 안내 단계적으로 안내 합니다. PowerShell Core는 오픈 소스 프로젝트인 [GitHub](https://github.com/powershell/powershell)합니다.

## <a name="cross-platform-editor-options"></a>플랫폼 간 편집기 옵션

일반 터미널에서 PowerShell Core 아래 단계의 모든 작업은 또는 VS Code 또는 Azure Data Studio 내에서 터미널에서 실행할 수 있습니다.  VS Code 및 Azure Data Studio macOS 및 Linux에서 사용할 수 있습니다.  Azure Data Studio에 대 한 자세한 내용은 참조 하세요. [이 빠른 시작](https://docs.microsoft.com/sql/azure-data-studio/quickstart-sql-server)합니다.  사용 하 여 고려해 야 할 수도 있습니다는 [PowerShell 확장](https://docs.microsoft.com/sql/azure-data-studio/powershell-extension) 에 대 한 합니다.

## <a name="installing-powershell-core"></a>PowerShell Core 설치

지원 되는 및 실험에 대 한 다양 한 플랫폼에서 PowerShell Core 설치에 대 한 자세한 내용은 다음 문서를 참조 합니다.

- [Windows에서 PowerShell Core 설치](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-windows?view=powershell-6)
- [Linux에서 PowerShell Core 설치](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-linux?view=powershell-6)
- [MacOS에서 PowerShell Core 설치](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-macos?view=powershell-6)
- [ARM에서 PowerShell Core 설치](https://docs.microsoft.com/powershell/scripting/install/powershell-core-on-arm?view=powershell-6)

## <a name="install-the-sqlserver-module"></a>SqlServer 모듈 설치

합니다 `SqlServer` 모듈에서 유지 관리 되는 [PowerShell 갤러리](https://www.powershellgallery.com/packages/SqlServer/)합니다. SQL Server에서 작업할 때 SqlServer PowerShell 모듈의 최신 버전 항상 사용 해야 합니다.

SqlServer 모듈을 설치 하려면 PowerShell Core 세션을 열고 다음 코드를 실행 합니다.

```powerhsell
Install-Module -Name SqlServer
```

PowerShell 갤러리의 SqlServer 모듈을 설치 하는 방법에 대 한 자세한 내용은 참조 [페이지](../powershell/download-sql-server-ps-module.md)합니다.

## <a name="using-the-sqlserver-module"></a>SqlServer 모듈을 사용 하 여

PowerShell Core를 실행 하 여 시작 해 보겠습니다.  MacOS 또는 Linux에서 열려 있는 경우는 *터미널 세션* 입력 하 여 컴퓨터에 **pwsh** 새 PowerShell Core 세션을 시작 합니다.  Windows를 사용 하 여 <kbd>Win</kbd>+<kbd>R</kbd>, 및 형식 `pwsh` 새 PowerShell Core 세션을 시작 하려면.

```
pwsh
```

SQL Server 라는 PowerShell 모듈을 제공 **SqlServer**합니다. 사용할 수는 **SqlServer** 모듈을 PowerShell 환경 또는 스크립트로 SQL Server 구성 (SQL Server 공급자 및 cmdlet)를 가져옵니다.

복사 하 고 가져오는 PowerShell 프롬프트에서 다음 명령을 붙여 합니다 **SqlServer** 현재 PowerShell 세션에 모듈:

```powershell
Import-Module SqlServer
```

확인 하려면 PowerShell 프롬프트에서 다음 명령을 입력 합니다 **SqlServer** 모듈을 제대로 가져온:

```powershell
Get-Module -Name SqlServer
```

PowerShell은 다음 출력과 유사한 정보가 표시 되어야 합니다.

```
ModuleType Version    Name          ExportedCommands
---------- -------    ----          ----------------
Script     21.1.18102 SqlServer     {Add-SqlAvailabilityDatabase, Add-SqlAvailabilityGroupList...
```

## <a name="connect-to-sql-server-and-get-server-information"></a>SQL Server에 연결 하 고 서버 정보 가져오기

다음 단계를 PowerShell Core를 사용 하 여 Linux에서 SQL Server 인스턴스에 연결할를 몇 개의 서버 속성을 표시 합니다.

복사 하 고 PowerShell 프롬프트에서 다음 명령을 붙여 넣습니다. 이러한 명령은 실행 하면 PowerShell 됩니다.
- 호스트 이름 또는 인스턴스의 IP 주소를 묻는 대화 상자를 표시 합니다.
- 표시 된 *PowerShell 자격 증명 요청* 자격 증명을 묻는 대화 상자에서. 사용할 수 있습니다 하 *SQL 사용자 이름* 및 *SQL 암호* Linux에서 SQL Server 인스턴스에 연결 하려면
- 사용 하 여는 **Get-SqlInstance** cmdlet에 연결 하는 **Server** 몇 가지 속성을 표시 하 고

필요에 따라 바꿀 수 있습니다만 `$serverInstance` IP 주소 또는 SQL Server 인스턴스의 호스트 이름을 사용 하 여 변수입니다.

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Connect to the Server and return a few properties
Get-SqlInstance -ServerInstance $serverInstance -Credential $credential
# done
```

PowerShell은 다음 출력과 유사한 정보가 표시 되어야 합니다.

```
Instance Name                   Version    ProductLevel UpdateLevel  HostPlatform HostDistribution
-------------                   -------    ------------ -----------  ------------ ----------------
your_server_instance            14.0.3048  RTM          CU13         Linux        Ubuntu
```

> [!NOTE]
> 아무 것도 이러한 값에 대 한 표시를 하는 경우 대상 SQL Server 인스턴스에 대 한 연결 가능성이 실패 했습니다. SQL Server Management Studio에서 연결 하려면 동일한 연결 정보를 사용할 수 있습니다 있는지 확인 합니다. 그런 다음 [connection troubleshooting recommendations](sql-server-linux-troubleshooting-guide.md#connection)(연결 문제 해결 권장 사항)를 검토합니다.

## <a name="using-the-sql-server-powershell-provider"></a>SQL Server PowerShell 공급자 사용

SQL Server 인스턴스에 연결 하기 위한 다른 옵션은 사용 하 여 [SQL Server PowerShell 공급자](https://docs.microsoft.com/sql/powershell/sql-server-powershell-provider)합니다.  공급자를 사용 하는 명령줄에만 개체 탐색기에서 트리 구조를 탐색 된 것 처럼 유사한 SQL Server 인스턴스를 이동할 수 있습니다.  기본적으로이 공급자는 이름이 PSDrive로 제시 `SQLSERVER:\` 연결 및 도메인 계정이 액세스할 수 있는 SQL Server 인스턴스를 이동 하는 데 사용할 수 있는 합니다.  참조 [구성 단계](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-auth-overview#configuration-steps) Linux의 SQL Server에 대 한 Active Directory authentication 설정 하는 방법에 대 한 정보에 대 한 합니다.

또한 SQL Server PowerShell 공급자를 사용 하 여 SQL 인증을 사용할 수 있습니다. 이 위해 사용 하 여는 `New-PSDrive` cmdlet는 새 PSDrive를 만들고 연결 하는 적절 한 자격 증명을 사용 합니다.

아래이 예제에서는 SQL 인증을 사용 하는 새 PSDrive를 만드는 방법의 예가 표시 됩니다.

```powershell
# NOTE: We are reusing the values saved in the $credential variable from the above example.

New-PSDrive -Name SQLonDocker -PSProvider SqlServer -Root 'SQLSERVER:\SQL\localhost,10002\Default\' -Credential $credential
```

드라이브를 실행 하 여 만들어졌는지 확인할 수 있습니다는 `Get-PSDrive` cmdlet.

```powershell
Get-PSDrive
```

사용자는 새 PSDrive를 만든 후에 탐색 하기 시작할 수 있습니다.

```powershell
dir SQLonDocker:\Databases
```

출력 모양을 다음과 같습니다.  이 출력은 데이터베이스 노드를 표시 하는 SSMS를 확인할 수 있습니다.  시스템 데이터베이스가 아닌 제외한 사용자 데이터베이스를 표시합니다.

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

인스턴스에서 모든 데이터베이스를 참조 해야 할 경우 한 가지 방법은 사용 하 여 `Get-SqlDatabase` cmdlet.

## <a name="get-databases"></a>데이터베이스 가져오기

알아야 하는 중요 한 cmdlet은는 `Get-SqlDatabase`합니다.  데이터베이스 또는 데이터베이스 내의 개체를 포함 하는 여러 가지 작업에는 `Get-SqlDatabase` cmdlet을 사용할 수 있습니다.  둘 다에 대 한 값을 제공 하는 경우는 `-ServerInstance` 및 `-Database` 매개 변수를 해당 데이터베이스 개체만 검색 됩니다.  그러나 지정 하는 경우는 `-ServerInstance` 매개 변수를 해당 인스턴스에서 모든 데이터베이스의 전체 목록이 반환 됩니다.

```powershell
# NOTE: We are reusing the values saved in the $credential variable from the above example.

# Connect to the Instance and retrieve all databases
Get-SqlDatabase -ServerInstance ServerB -Credential $credential
```

위의 Get-sqldatabase 명령에 의해 반환 될 수 있습니다의 예제는 다음과 같습니다.

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

## <a name="examine-sql-server-error-logs"></a>SQL Server 오류 로그를 검사 합니다.

다음 단계를 Linux에서 SQL Server 인스턴스에서 로그 연결 오류를 검사 하려면 PowerShell Core를 사용 합니다.

복사 하 고 PowerShell 프롬프트에서 다음 명령을 붙여 넣습니다. 이러한 실행 하려면 몇 분 정도 걸릴 수 있습니다. 이 명령은 다음 단계를 수행합니다.
- 호스트 이름 또는 인스턴스의 IP 주소를 묻는 대화 상자를 표시 합니다.
- 표시 된 *PowerShell 자격 증명 요청* 자격 증명을 묻는 대화 상자. 사용할 수 있습니다 하 *SQL 사용자 이름* 및 *SQL 암호* Linux에서 SQL Server 인스턴스에 연결 하려면
- 사용 된 **Get SqlErrorLog** cmdlet은 Linux에서 SQL Server 인스턴스에 연결 하 고 오류를 검색 이후 로그 **어제**

필요에 따라 바꿀 수 있습니다는 `$serverInstance` IP 주소 또는 SQL Server 인스턴스의 호스트 이름을 사용 하 여 변수입니다.

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Retrieve error logs since yesterday
Get-SqlErrorLog -ServerInstance $serverInstance -Credential $credential -Since Yesterday
# done
```

## <a name="explore-cmdlets-currently-available-in-ps-core"></a>PS Core에서 현재 사용할 수 있는 cmdlet 탐색
SqlServer 모듈에는 현재 Windows PowerShell에서 사용할 수 있는 106 cmdlet에, 하는 동안는 106의 유일한 59 PSCore에서 사용할 수 있습니다. 현재 사용할 수 있는 59 cmdlet의 전체 목록은 아래 포함 되어 있습니다.  SqlServer 모듈의 모든 cmdlet의 심층적인 설명서, 참조는 SqlServer [cmdlet 참조](https://docs.microsoft.com/powershell/module/sqlserver/)합니다.

다음 명령을 모두 표시 됩니다 사용할 수 있는 cmdlet 사용 하는 PowerShell의 버전입니다.

```powershell
Get-Command -Module SqlServer -CommandType Cmdlet |
SORT -Property Noun |
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
- Convert-UrnToPath

## <a name="see-also"></a>참고자료
- [SQL Server PowerShell](../relational-databases/scripting/sql-server-powershell.md)
