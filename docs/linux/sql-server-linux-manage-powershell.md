---
title: PowerShell 사용 하 여 Linux에서 SQL Server 관리 | Microsoft Docs
description: 이 문서에서는 Linux의 SQL Server를 사용 하 여 Windows에서 PowerShell을 사용 하는 개요를 제공 합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: a3492ce1-5d55-4505-983c-d6da8d1a94ad
ms.openlocfilehash: 73d9780e2980eeecf49cf420901e7e6f1dc4a669
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65089381"
---
# <a name="use-powershell-on-windows-to-manage-sql-server-on-linux"></a>Linux의 SQL Server를 관리 하는 Windows에서 PowerShell을 사용 하 여

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 소개 [SQL Server PowerShell](../powershell/sql-server-powershell.md) Linux의 SQL Server와 함께 사용 하는 방법에 몇 가지 예가 단계적으로 안내 합니다. Windows, MacOS 및 Linux에서 SQL Server에 대 한 PowerShell 지원을 현재 사용할 수 있는 경우 이 문서는 Windows 컴퓨터를 사용 하 여 Linux에서 원격 SQL Server 인스턴스에 연결할 안내 합니다.

## <a name="install-the-newest-version-of-sql-powershell-on-windows"></a>Windows에서 SQL PowerShell의 최신 버전을 설치 합니다.

[SQL PowerShell](../powershell/download-sql-server-ps-module.md) Windows에 PowerShell 갤러리에 유지 됩니다. SQL Server에서 작업할 때 SqlServer PowerShell 모듈의 최신 버전 항상 사용 해야 합니다.

## <a name="before-you-begin"></a>시작하기 전 주의 사항

읽기를 [알려진 문제](sql-server-linux-release-notes.md) Linux의 SQL Server에 대 한 합니다.

## <a name="launch-powershell-and-import-the-sqlserver-module"></a>PowerShell을 시작 하 고 가져올는 *sqlserver* 모듈

Windows에서 PowerShell을 시작 하 여 시작 해 보겠습니다. 사용 하 여 <kbd>Win</kbd>+<kbd>R</kbd>입력 하 여 Windows 컴퓨터에 **PowerShell** 새 Windows PowerShell 세션을 시작 합니다.

```
PowerShell
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

Linux의 SQL Server 인스턴스에 연결의 서버 속성을 표시 하에서 Windows PowerShell을 사용 하겠습니다.

복사 하 고 PowerShell 프롬프트에서 다음 명령을 붙여 넣습니다. 이러한 명령은 실행 하면 PowerShell 됩니다.
- 호스트 이름 또는 인스턴스의 IP 주소를 묻는 대화 상자를 표시 합니다.
- 표시 된 *Windows PowerShell 자격 증명 요청* 자격 증명을 묻는 대화 상자에서. 사용할 수 있습니다 하 *SQL 사용자 이름* 및 *SQL 암호* Linux에서 SQL Server 인스턴스에 연결 하려면
- 사용 하 여는 **Get-SqlInstance** cmdlet에 연결 하는 **Server** 몇 가지 속성을 표시 하 고

필요에 따라 바꿀 수 있습니다만 `$serverInstance` IP 주소 또는 SQL Server 인스턴스의 호스트 이름을 사용 하 여 변수입니다.

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Connect to the Server and get a few properties
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

SQL Server 인스턴스에 연결 하기 위한 다른 옵션은 사용 하 여 [SQL Server PowerShell 공급자](https://docs.microsoft.com/sql/powershell/sql-server-powershell-provider)합니다.  이 공급자를 사용 하는 명령줄에만 개체 탐색기에서 트리 구조를 탐색 된 것 처럼 유사한 SQL Server 인스턴스를 이동할 수 있습니다.  기본적으로이 공급자는 이름이 PSDrive로 제시 `SQLSERVER:\` 연결 및 도메인 계정이 액세스할 수 있는 SQL Server 인스턴스를 이동 하는 데 사용할 수 있는 합니다.  참조 [구성 단계](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-auth-overview#configuration-steps) Linux의 SQL Server에 대 한 Active Directory authentication 설정 하는 방법에 대 한 정보에 대 한 합니다.

또한 SQL Server PowerShell 공급자를 사용 하 여 SQL 인증을 사용할 수 있습니다. 이 위해 사용 하 여는 `New-PSDrive` cmdlet는 새 PSDrive를 만들고 연결 하기 위해 적절 한 자격 증명을 제공 합니다.

아래이 예제에서는 SQL 인증을 사용 하는 새 PSDrive를 만드는 방법의 예로 표시 됩니다.

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

출력 모양을 다음과 같습니다.  데이터베이스 노드를 표시 하는 SSMS는 비슷합니다 출력을 확인할 수 있습니다.  시스템 데이터베이스가 아닌 제외한 사용자 데이터베이스를 표시합니다.

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

인스턴스에서 모든 데이터베이스를 참조 해야 할 경우 한 가지 방법은 사용 하 여 [Get-sqldatabase](https://docs.microsoft.com/powershell/module/sqlserver/Get-SqlDatabase) cmdlet.

## <a name="examine-sql-server-error-logs"></a>SQL Server 오류 로그를 검사 합니다.

다음 단계를 사용 하면 Windows에서 PowerShell을 사용 하는 로그는 Linux에서 SQL Server 인스턴스에 연결 하는 오류를 검사 합니다. 사용 합니다 **Out-gridview** 표 보기에서에서 로그 오류에서 정보를 표시 하는 cmdlet입니다.

복사 하 고 PowerShell 프롬프트에서 다음 명령을 붙여 넣습니다. 이러한 실행 하려면 몇 분 정도 걸릴 수 있습니다. 이 명령은 다음을 수행 합니다.
- 호스트 이름 또는 인스턴스의 IP 주소를 묻는 대화 상자를 표시 합니다.
- 표시 된 *Windows PowerShell 자격 증명 요청* 자격 증명을 묻는 대화 상자에서. 사용할 수 있습니다 하 *SQL 사용자 이름* 및 *SQL 암호* Linux에서 SQL Server 인스턴스에 연결 하려면
- 사용 된 **Get SqlErrorLog** cmdlet은 Linux에서 SQL Server 인스턴스에 연결 하 고 오류를 검색 이후 로그 **어제**
- 출력을 파이프 합니다 **Out-gridview** cmdlet

필요에 따라 바꿀 수 있습니다는 `$serverInstance` IP 주소 또는 SQL Server 인스턴스의 호스트 이름을 사용 하 여 변수입니다.

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Retrieve error logs since yesterday
Get-SqlErrorLog -ServerInstance $serverInstance -Credential $credential -Since Yesterday | Out-GridView
# done
```
## <a name="see-also"></a>참고자료
- [SQL Server PowerShell](../relational-databases/scripting/sql-server-powershell.md)
- [SqlServer cmdlet](https://docs.microsoft.com/powershell/module/sqlserver)
