---
title: PowerShell을 사용하여 SQL Server on Linux 관리
description: 이 문서에서는 SQL Server on Linux와 함께 Windows의 PowerShell을 사용하는 방법을 간략히 설명합니다.
author: VanMSFT
ms.author: vanto
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: a3492ce1-5d55-4505-983c-d6da8d1a94ad
ms.openlocfilehash: 52db0986bb6af34e1dc034d95146a96d3fdcf246
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68000124"
---
# <a name="use-powershell-on-windows-to-manage-sql-server-on-linux"></a>Windows의 PowerShell을 사용하여 SQL Server on Linux 관리

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 [SQL Server PowerShell](../powershell/sql-server-powershell.md)을 소개하고 SQL Server on Linux에서 사용하는 방법에 관한 몇 가지 예제를 안내합니다. SQL Server에 대한 PowerShell 지원은 현재 Windows, MacOS 및 Linux에서 사용할 수 있습니다. 이 문서에서는 Windows 머신을 사용하여 Linux의 원격 SQL Server 인스턴스에 연결하는 과정을 안내합니다.

## <a name="install-the-newest-version-of-sql-powershell-on-windows"></a>Windows에 최신 버전의 SQL PowerShell 설치

Windows의 [SQL PowerShell](../powershell/download-sql-server-ps-module.md)은 PowerShell 갤러리에서 유지 관리됩니다. SQL Server를 사용하는 경우 항상 최신 버전의 SqlServer PowerShell 모듈을 사용해야 합니다.

## <a name="before-you-begin"></a>시작하기 전 주의 사항

SQL Server on Linux의 [알려진 문제](sql-server-linux-release-notes.md)를 확인합니다.

## <a name="launch-powershell-and-import-the-sqlserver-module"></a>PowerShell을 시작하고 *sqlserver* 모듈을 가져옵니다.

먼저 Windows에서 PowerShell을 시작하겠습니다. Windows 컴퓨터에서 <kbd>Win</kbd>+<kbd>R</kbd>을 사용하고 **PowerShell**을 입력하여 새 Windows PowerShell 세션을 시작합니다.

```
PowerShell
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

Windows에서 PowerShell을 사용하여 Linux의 SQL Server 인스턴스에 연결하고 몇 가지 서버 속성을 표시하겠습니다.

다음 명령을 복사하여 PowerShell 프롬프트에 붙여넣습니다. 이러한 명령을 실행하면 PowerShell에서 다음을 수행합니다.
- 인스턴스의 호스트 이름 또는 IP 주소를 입력하라는 대화 상자를 표시합니다.
- 자격 증명을 묻는 ‘Windows PowerShell 자격 증명 요청’ 대화 상자를 표시합니다.  ‘SQL 사용자 이름’ 및 ‘SQL 암호’를 사용하여 Linux의 SQL Server 인스턴스에 연결할 수 있습니다.  
- **Get-SqlInstance** cmdlet을 사용하여 **서버**에 연결하고 몇 가지 속성을 표시합니다.

필요에 따라 `$serverInstance` 변수를 해당 SQL Server 인스턴스의 IP 주소나 호스트 이름으로 바꿀 수 있습니다.

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Connect to the Server and get a few properties
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

SQL Server 인스턴스에 연결하는 또 다른 옵션은 [SQL Server PowerShell 공급자](https://docs.microsoft.com/sql/powershell/sql-server-powershell-provider)를 사용하는 것입니다.  이 공급자를 사용하면 개체 탐색기에서 트리 구조를 탐색하는 것처럼 SQL Server 인스턴스를 명령줄에서 탐색할 수 있습니다.  기본적으로 이 공급자는 도메인 계정이 액세스할 수 SQL Server 인스턴스를 연결 및 탐색하는 데 사용할 수 있는 `SQLSERVER:\`라는 PSDrive로 표시됩니다.  SQL Server on Linux의 Active Directory 인증을 설정하는 방법에 대한 자세한 내용은 [구성 단계](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-auth-overview#configuration-steps)를 참조하세요.

SQL Server PowerShell 공급자를 통해 SQL 인증을 사용할 수도 있습니다. 이렇게 하려면 `New-PSDrive` cmdlet을 사용하여 새 PSDrive을 만들고 연결하는 데 사용할 적절한 자격 증명을 제공합니다.

아래 예제에서는 SQL 인증을 사용하여 새 PSDrive를 만드는 방법의 한 가지 예를 보여 줍니다.

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

인스턴스의 모든 데이터베이스를 확인해야 하는 경우 한 가지 옵션은 [Get-SqlDatabase](https://docs.microsoft.com/powershell/module/sqlserver/Get-SqlDatabase) cmdlet을 사용하는 것입니다.

## <a name="examine-sql-server-error-logs"></a>SQL Server 오류 로그 검사

다음 단계에서는 Windows의 PowerShell을 사용하여 Linux의 SQL Server 인스턴스에서 오류 로그 연결을 검사합니다. 또한 **Out-GridView** cmdlet을 사용하여 그리드 보기 표시에 오류 로그의 정보를 표시합니다.

다음 명령을 복사하여 PowerShell 프롬프트에 붙여넣습니다. 명령을 실행하는 데 몇 분 정도 걸릴 수 있습니다. 이 명령은 다음 작업을 수행합니다.
- 인스턴스의 호스트 이름 또는 IP 주소를 입력하라는 대화 상자를 표시합니다.
- 자격 증명을 묻는 ‘Windows PowerShell 자격 증명 요청’ 대화 상자를 표시합니다.  ‘SQL 사용자 이름’ 및 ‘SQL 암호’를 사용하여 Linux의 SQL Server 인스턴스에 연결할 수 있습니다.  
- **Get-SqlErrorLog** cmdlet을 사용하여 Linux의 SQL Server 인스턴스에 연결하고 **Yesterday** 이후의 오류 로그를 검색합니다.
- 출력을 **Out-GridView** cmdlet으로 파이프합니다.

필요에 따라 `$serverInstance` 변수를 SQL Server 인스턴스의 IP 주소나 호스트 이름으로 바꿀 수 있습니다.

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Retrieve error logs since yesterday
Get-SqlErrorLog -ServerInstance $serverInstance -Credential $credential -Since Yesterday | Out-GridView
# done
```
## <a name="see-also"></a>관련 항목:
- [SQL Server PowerShell](../relational-databases/scripting/sql-server-powershell.md)
- [SqlServer cmdlet](https://docs.microsoft.com/powershell/module/sqlserver)
