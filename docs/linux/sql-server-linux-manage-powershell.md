---
title: 관리 SQL Server PowerShell 사용한 linux | Microsoft Docs
description: 이 문서에서는 PowerShell을 사용 하 여 Linux에서 SQL Server와 Windows에 대 한 개요를 제공 합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: a3492ce1-5d55-4505-983c-d6da8d1a94ad
ms.openlocfilehash: ea606c9380b9729f20857518eca7978b6f1c46e7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="use-powershell-on-windows-to-manage-sql-server-on-linux"></a>Windows PowerShell을 사용 하 여 Linux에서 SQL Server 관리

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 소개 [SQL Server PowerShell](https://msdn.microsoft.com/en-us/library/mt740629.aspx) 과정을 안내 하는 몇 가지 예 SQL Server 2017 Linux에서 함께 사용 하는 방법에 대 한 합니다. PowerShell SQL Server에 대 한 지원은 windows에서 현재 사용할 수 있는 Linux에서 원격 SQL Server 인스턴스에 연결할 수 있는 Windows 컴퓨터에 있는 경우에 사용할 수 있도록 합니다.

## <a name="install-the-newest-version-of-sql-powershell-on-windows"></a>Windows에서 최신 버전의 SQL PowerShell 설치

[SQL PowerShell](https://msdn.microsoft.com/en-us/library/mt740629.aspx) windows에 포함 된 [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md)합니다. SQL Server를 사용할 때는 가장 최신 버전의 SSMS 및 SQL PowerShell를 항상 사용 해야 합니다. 최신 버전의 SSMS 지속적으로 업데이트 되 고 최적화 된와 현재 SQL Server on 2017 Linux 합니다. 참조를 다운로드 하 여 최신 버전을 설치 하려면 [SQL Server Management Studio 다운로드](../ssms/download-sql-server-management-studio-ssms.md)합니다. 최신 상태로 유지, 최신 버전의 SSMS 묻는 메시지를 다운로드 하는 새 버전이 있는 경우.

## <a name="before-you-begin"></a>시작하기 전 주의 사항

읽기는 [알려진 문제](sql-server-linux-release-notes.md) for SQL Server 2017 Linux.

## <a name="launch-powershell-and-import-the-sqlserver-module"></a>PowerShell을 시작 하 고 가져올는 *sqlserver* 모듈

Windows에서 PowerShell을 시작 하 여 시작 하겠습니다. 열기는 *명령 프롬프트* 입력 하 여 Windows 컴퓨터에서 **PowerShell** 새 Windows PowerShell 세션을 시작 합니다.

```
PowerShell
```

라는 Windows PowerShell 모듈을 제공 하는 SQL Server **SqlServer** PowerShell 환경 또는 스크립트로 (SQL Server 공급자 및 cmdlet) SQL Server 구성 요소를 가져오는 데 사용할 수 있습니다.

복사 하 고 가져오려는 PowerShell 프롬프트에서 다음 명령을 붙여는 **SqlServer** 현재 PowerShell 세션에 모듈:

```powershell
Import-Module SqlServer
```

확인 하려면 PowerShell 프롬프트에서 다음 명령을 입력 된 **SqlServer** 모듈을 올바르게 가져왔는지를:

```powershell
Get-Module -Name SqlServer
```

PowerShell에는 다음 출력과 유사한 정보가 표시 되어야 합니다.

```
ModuleType Version    Name          ExportedCommands
---------- -------    ----          ----------------
Script     0.0        SqlServer
Manifest   20.0       SqlServer     {Add-SqlAvailabilityDatabase, Add-SqlAvailabilityGroupList...
```

## <a name="connect-to-sql-server-and-get-server-information"></a>SQL Server에 연결 하 고 서버 정보 가져오기

SQL Server 2017 Linux에서 인스턴스에 연결의 서버 속성을 표시 하 windows PowerShell을 사용 하겠습니다.

복사한 PowerShell 프롬프트에서 다음 명령을 붙여 넣습니다. 이러한 명령을 실행할 때 PowerShell 수행 합니다.
- 표시는 *Windows PowerShell 자격 증명 요청* 자격 증명을 묻는 대화 상자 (*SQL 사용자 이름* 및 *SQL 암호*) SQL Server 2017 연결할 Linux에서 인스턴스
- SQL Server 관리 개체 (SMO) 어셈블리를 로드 합니다.
- 인스턴스를 만들고는 [서버](https://msdn.microsoft.com/en-us/library/microsoft.sqlserver.management.smo.server.aspx) 개체
- 에 연결 된 **서버** 몇 가지 속성을 표시 하 고

대체 **\<your_server_instance\>** Linux에서 SQL Server 2017 인스턴스의 호스트 이름 또는 IP 주소입니다.

```powershell
# Prompt for credentials to login into SQL Server
$serverInstance = "<your_server_instance>"
$credential = Get-Credential

# Load the SMO assembly and create a Server object
[System.Reflection.Assembly]::LoadWithPartialName('Microsoft.SqlServer.SMO') | out-null
$server = New-Object ('Microsoft.SqlServer.Management.Smo.Server') $serverInstance

# Set credentials
$server.ConnectionContext.LoginSecure=$false
$server.ConnectionContext.set_Login($credential.UserName)
$server.ConnectionContext.set_SecurePassword($credential.Password)

# Connect to the Server and get a few properties
$server.Information | Select-Object Edition, HostPlatform, HostDistribution | Format-List
# done
```

PowerShell에는 다음 출력과 유사한 정보가 표시 되어야 합니다.

```
Edition          : Developer Edition (64-bit)
HostPlatform     : Linux
HostDistribution : Ubuntu
```
> [!NOTE]
> 이러한 값에 대해 아무 항목도 표시 하는 경우 대상 SQL Server 인스턴스에 대 한 연결 가장 실패할 수 있습니다. SQL Server Management Studio에서 연결 하려면 동일한 연결 정보를 사용할 수 있는지 확인 합니다. 그런 다음 [connection troubleshooting recommendations](sql-server-linux-troubleshooting-guide.md#connection)(연결 문제 해결 권장 사항)를 검토합니다.

## <a name="examine-sql-server-error-logs"></a>SQL Server 오류 로그를 검사 합니다.

이제 오류 로그를 검사 하는 Windows에서 PowerShell을 사용 하 여 Linux에서 SQL Server 2017 인스턴스에 연결 합니다. 또한 사용 합니다는 **Out-gridview** cmdlet에서 오류 정보를 표시할 그리드 뷰 디스플레이에 기록 합니다.

복사한 PowerShell 프롬프트에서 다음 명령을 붙여 넣습니다. 실행 하는 데 몇 분 정도 걸릴 수 있습니다. 이 명령은 다음을 수행 합니다.
- 표시는 *Windows PowerShell 자격 증명 요청* 자격 증명을 묻는 대화 상자 (*SQL 사용자 이름* 및 *SQL 암호*) SQL Server 2017 연결할 Linux에서 인스턴스
- 사용 하 여는 **Get SqlErrorLog** cmdlet의 SQL Server 2017 Linux 인스턴스에 연결 하 고 오류를 검색할 이후 로그 **어제**
- 출력을 파이프는 **Out-gridview** cmdlet

대체 **\<your_server_instance\>** Linux에서 SQL Server 2017 인스턴스의 호스트 이름 또는 IP 주소입니다.

```powershell
# Prompt for credentials to login into SQL Server
$serverInstance = "<your_server_instance>"
$credential = Get-Credential

# Retrieve error logs since yesterday
Get-SqlErrorLog -ServerInstance $serverInstance -Credential $credential -Since Yesterday | Out-GridView
# done
```
## <a name="see-also"></a>참고 항목
- [SQL Server PowerShell](../relational-databases/scripting/sql-server-powershell.md)
