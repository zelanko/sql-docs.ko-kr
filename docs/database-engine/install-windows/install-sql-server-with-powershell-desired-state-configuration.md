---
title: '설치: PowerShell Desired State Configuration'
description: PowerShell DSC를 사용하여 SQL Server를 설치하고 Windows Server 2016에서 SQL Server 2017 독립 실행형 인스턴스의 초기 설정에 대해 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.devlang: PowerShell
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
author: randomnote1
ms.author: dareist
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 5a9770cd648fe804ee973878adee27b2d55080d0
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2020
ms.locfileid: "91671066"
---
# <a name="install-sql-server-with-powershell-desired-state-configuration"></a>PowerShell Desired State Configuration을 사용하여 SQL Server 설치

SQL Server 설치 인터페이스를 통해 별생각 없이 같은 단추를 선택하고 같은 정보를 입력하면서 사용해 본적이 있나요? 설치가 완료되었지만 **sysadmin** 역할에서 DBA 그룹을 지정하는 것을 잊었습니다. 그러면 다음과 같은 작업을 수행해야 합니다.
* 단일 사용자 모드로 전환합니다.
* 적절한 사용자 또는 그룹을 추가합니다.
* 다중 사용자 모드에서 SQL Server를 백업합니다.
* 테스트. 

설상가상으로, 이로 인해 전체 설치에 대한 신뢰가 흔들린다는 것입니다. "내가 또 무엇을 빠뜨렸을까?" 직접 요청할 수 있습니다.

[PowerShell DSC(Desired State Configuration)](/powershell/scripting/dsc/overview/overview)에 대해 읽어 보세요. DSC를 사용하면 수백, 수천 대의 서버에서 재사용할 수있는 하나의 구성 템플릿을 빌드할 수 있습니다. 빌드에 따라 몇 가지 설정 매개 변수를 조정해야 할수도 있습니다. 하지만 모든 표준 설정을 그대로 유지할 수 있으므로 중요한 문제는 아닙니다. 이는 중요한 매개 변수를 입력하는 것을 잊지 않게 해줍니다.

이 문서에서는 **SqlServerDsc** DSC 리소스를 사용하여 Windows Server 2016에서 SQL Server 2017의 독립 실행형 인스턴스의 초기 설정을 살펴보겠습니다. DSC에 대한 사전 지식은 DSC가 어떻게 작동하는지 탐색하지 않기 때문에 유용합니다.

이 연습에서는 다음 항목이 필요합니다.

- Windows Server 2016을 실행하는 머신입니다.
- SQL Server 2017 설치 미디어.
- **SqlServerDsc** DSC 리소스.

## <a name="prerequisites"></a>사전 요구 사항

대부분의 경우 DSC는 필수 구성 요소 요구 사항을 처리하는 데 사용됩니다. 그러나 이 데모에서는 수동으로 필수 구성 요소를 처리합니다.

## <a name="install-the-sqlserverdsc-dsc-resource"></a>SqlServerDsc DSC 리소스 설치

[Install-Module](/powershell/module/powershellget/Install-Module?view=powershell-5.1) cmdlet을 사용하여 [PowerShell 갤러리](https://www.powershellgallery.com/)에서 [SqlServerDsc](https://www.powershellgallery.com/packages/SqlServerDsc) DSC 리소스를 다운로드합니다. 

> [!NOTE]
> 모듈을 설치하려면 PowerShell이 **관리자 권한으로** 실행되고 있는지 확인하세요.

```PowerShell
Install-Module -Name SqlServerDsc
```

### <a name="get-the-sql-server-2017-installation-media"></a>SQL Server 2017 설치 미디어 가져오기
서버에 SQL Server 2017 설치 미디어를 다운로드합니다. Visual Studio 구독에서 SQL Server 2017 Enterprise를 다운로드하고 ISO를 `C:\en_sql_server_2017_enterprise_x64_dvd_11293666.iso`로 복사했습니다.

이제 ISO를 디렉터리로 추출해야 합니다.

```PowerShell
New-Item -Path C:\SQL2017 -ItemType Directory
$mountResult = Mount-DiskImage -ImagePath 'C:\en_sql_server_2017_enterprise_x64_dvd_11293666.iso' -PassThru
$volumeInfo = $mountResult | Get-Volume
$driveInfo = Get-PSDrive -Name $volumeInfo.DriveLetter
Copy-Item -Path ( Join-Path -Path $driveInfo.Root -ChildPath '*' ) -Destination C:\SQL2017\ -Recurse
Dismount-DiskImage -ImagePath 'C:\en_sql_server_2017_enterprise_x64_dvd_11293666.iso'
```

## <a name="create-the-configuration"></a>구성 만들기

### <a name="configuration"></a>구성

[MOF(Managed Object Format)](/windows/desktop/WmiSdk/managed-object-format--mof-) 문서를 생성하기 위해 호출될 구성 함수를 만듭니다.

```PowerShell
Configuration SQLInstall
{...}
```

### <a name="modules"></a>모듈

모듈을 현재 세션으로 가져옵니다. 이러한 모듈은 구성 문서에서 MOF 문서를 빌드하는 방법을 알려줍니다. 또한 DSC 엔진에 MOF 문서를 적용하는 방법을 알려줍니다.

```PowerShell
Import-DscResource -ModuleName SqlServerDsc
```

### <a name="resources"></a>리소스

#### <a name="net-framework"></a>.NET Framework

SQL Server는 .NET Framework를 사용합니다. 따라서 SQL Server를 설치하기 전에 설치되어 있는지 확인해야 합니다. **WindowsFeature** 리소스는 **Net-Framework-45-Core** Windows 기능을 설치하는 데 사용됩니다.

```PowerShell
WindowsFeature 'NetFramework45'
{
     Name = 'Net-Framework-45-Core'
     Ensure = 'Present'
}
```

#### <a name="sqlsetup"></a>SqlSetup

**SqlSetup** 리소스는 SQL Server 설치 방법을 DSC에 알려주는 데 사용됩니다. 기본 설치에 필요한 매개 변수는 다음과 같습니다.

- **InstanceName**. 인스턴스의 이름입니다. 기본 인스턴스의 경우 **MSSQLSERVER**를 사용합니다.
- **기능**. 설치할 기능입니다. 이 예제에서는 **SQLEngine** 기능만 설치합니다.
- **SourcePath**. SQL 설치 미디어의 경로입니다. 이 예제에서는 `C:\SQL2017`에서 SQL 설치 미디어에 저장하겠습니다. 네트워크 공유는 서버에서 사용되는 공간을 최소화할 수 있습니다.
- **SQLSysAdminAccounts**. **sysadmin** 역할의 구성원이 될 사용자 또는 그룹입니다. 이 예제에서는 로컬 관리자 그룹 **sysadmin** 액세스 권한을 부여하겠습니다. 

> [!NOTE]
> 높은 수준의 보안 환경에서는 이 구성을 권장하지 않습니다.

**SqlSetup**에서 사용할 수 있는 매개 변수의 전체 목록과 설명은 [SqlServerDsc GitHub 리포지토리](https://github.com/PowerShell/SqlServerDsc/tree/master#sqlsetup)에서 확인할 수 있습니다.

**SqlSetup** 리소스는 SQL Server만 설치하고 적용된 설정은 유지 관리하지 **않습니다**. 설치 시 **SQLSysAdminAccounts**가 지정된 경우를 예로 들 수 있습니다. 관리자는 **sysadmin** 역할에 로그인을 추가하거나 로그인을 제거할 수 있습니다. 그러나 **SqlSetup** 리소스는 영향을 받지 않습니다. DSC에서 **sysadmin** 역할의 멤버 자격을 적용하려면 [SqlServerRole](https://github.com/PowerShell/SqlServerDsc/tree/master#sqlserverrole) 리소스를 사용합니다.

#### <a name="finish-configuration"></a>구성 완료

```PowerShell
Configuration SQLInstall
{
     Import-DscResource -ModuleName SqlServerDsc

     node localhost
     {
          WindowsFeature 'NetFramework45'
          {
               Name   = 'NET-Framework-45-Core'
               Ensure = 'Present'
          }

          SqlSetup 'InstallDefaultInstance'
          {
               InstanceName        = 'MSSQLSERVER'
               Features            = 'SQLENGINE'
               SourcePath          = 'C:\SQL2017'
               SQLSysAdminAccounts = @('Administrators')
               DependsOn           = '[WindowsFeature]NetFramework45'
          }
     }
}
```

## <a name="build-and-deploy"></a>빌드 및 배포

### <a name="compile-the-configuration"></a>구성 컴파일

구성 스크립트를 도트 소싱합니다.

```PowerShell
. .\SQLInstallConfiguration.ps1
```

구성 함수를 실행합니다.

```PowerShell
SQLInstall
```

**SQLInstall**라는 디렉터리는 작업 디렉터리에서 만들어집니다. **localhost.mof**라는 파일이 포함되어 있습니다. 컴파일된 DSC 구성을 보여주는 MOF의 콘텐츠를 검토합니다.

### <a name="deploy-the-configuration"></a>구성 배포

SQL Server의 DSC 배포를 시작하려면 **Start-DscConfiguration** cmdlet을 호출합니다. 다음 매개 변수가 cmdlet에 제공됩니다.

- **경로**. 배포할 MOF 문서가 포함된 폴더의 경로입니다. 예제는 `C:\SQLInstall`입니다.
- **대기**. 구성 작업이 완료될 때까지 기다립니다.
- **Force**. 모든 기존 DSC 구성을 재정의합니다.
- **Verbose**. 자세한 정보 출력을 표시합니다. 이는 문제 해결을 위해 처음으로 구성을 푸시할 때 유용합니다.

```PowerShell
Start-DscConfiguration -Path C:\SQLInstall -Wait -Force -Verbose
```

구성이 적용되면 자세한 정보 출력이 현재 상황을 보여줍니다. 오류(빨간색 텍스트)가 throw되지 않는 한 **Operation 'Invoke CimMethod' complete**가 화면에 나타나면 SQL Server 를 설치해야 합니다.

## <a name="validate-installation"></a>설치 유효성 검사

### <a name="dsc"></a>DSC

[Test-DscConfiguration](/powershell/module/psdesiredstateconfiguration/test-dscconfiguration) cmdlet은 서버의 현재 상태가 원하는 상태를 충족하는지 확인할 수 있습니다. 이 경우 SQL Server 설치입니다. **Test-DscConfiguration**의 결과는 **True**이어야 합니다.

```PowerShell
PS C:\> Test-DscConfiguration
True
```

### <a name="services"></a>Services

서비스 목록은 이제 SQL Server 서비스를 반환합니다.

```PowerShell
PS C:\> Get-Service -Name *SQL*
Status  Name           DisplayName
------  ----           -----------
Running MSSQLSERVER    SQL Server (MSSQLSERVER)
Stopped SQLBrowser     SQL Server Browser
Running SQLSERVERAGENT SQL Server Agent (MSSQLSERVER)
Running SQLTELEMETRY   SQL Server CEIP service (MSSQLSERVER)
Running SQLWriter      SQL Server VSS Writer
```

### <a name="sql-server"></a>SQL Server

```PowerShell
PS C:\> & sqlcmd -S $env:COMPUTERNAME
1> SELECT @@SERVERNAME
2> GO
1> quit
```

## <a name="see-also"></a>참고 항목

[Windows PowerShell Desired State Configuration 개요](/powershell/scripting/dsc/overview/overview)

[명령 프롬프트에서 SQL Server 설치](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)

[구성 파일을 사용하여 SQL Server 설치](../../database-engine/install-windows/install-sql-server-using-a-configuration-file.md)