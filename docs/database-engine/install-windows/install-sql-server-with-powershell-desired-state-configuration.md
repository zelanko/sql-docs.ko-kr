---
title: PowerShell Desired State Configuration을 사용하여 SQL Server 설치 | Microsoft Docs
description: PowerShell Desired State Configuration(DSC)을 사용하여 SQL Server 설치하는 방법에 대해 알아보세요.
ms.custom: ''
ms.date: 10/26/2018
ms.devlang: PowerShell
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
author: randomnote1
ms.author: dareist
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 16d425d8eb66a950f432fa3ef9c68a8e68a78d22
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50148485"
---
# <a name="install-sql-server-with-powershell-desired-state-configuration"></a>PowerShell Desired State Configuration을 사용하여 SQL Server 설치

SQL Server 설치 인터페이스를 통해 별생각 없이 이전과 같은 단추를 클릭하고 이전과 같은 정보를 입력하면서 얼마나 많이 클릭했습니까? 그런 후 설치가 완료되면 "sysadmin 역할에서 DBA 그룹을 지정하는 것을 잊었음"을 깨닫게 됩니다. 이제는 단일 사용자 모드에서 적절한 사용자 또는 그룹을 추가하고, 다중 사용자 모드에서 SQL을 백업하고 테스트하는 데 소중한 시간을 할애해야 합니다. 설상가상으로, 이로 인해 전체 설치에 대한 신뢰가 흔들린다는 것입니다. "내가 또 무엇을 빠뜨렸을까?" 이러한 상황은 저도 여러 번 겪어봤습니다.

이제 [PowerShell Desired State Configuration(DSC)](https://docs.microsoft.com/powershell/dsc/overview)가 있습니다. DSC를 사용하면 수십만 대의 서버에서 재사용할 수있는 하나의 구성 템플릿을 구축할 수 있습니다. 빌드에 따라 몇 가지 설정 매개 변수를 조정해야 할 수도 있지만 모든 표준 설정을 그대로 유지할 수 있으므로 큰 문제는 아닙니다. 이것의 장점은 밤 늦게까지 아이를 돌보느라 중요한 매개 변수를 입력하는 것을 잊을 가능성이 없다는 것입니다.

이 문서에서는 SqlServerDsc DSC 리소스를 사용하여 Windows Server 2016에서 SQL Server 2017의 독립 실행형 인스턴스의 초기 설정을 살펴보겠습니다. DSC가 작동하는 방식은 살펴보지 않을 것이기 때문에 DSC에 대한 약간의 사전 지식이 도움이 될 것입니다.

이 연습에서는 다음 항목이 필요합니다.

- Windows Server 2016을 실행하는 가상 머신
- SQL Server 2017 설치 미디어
- SqlServerDsc DSC 리소스(버전 10.0.0.0는 이 문서의 작성 당시 버전임)

## <a name="prerequisites"></a>사전 요구 사항

대부분의 경우 DSC는 사전 요구 사항을 처리하는 데 사용됩니다. 그러나 이 데모에서는 전제 조건을 직접 처리할 것입니다.

## <a name="install-the-sqlserverdsc-dsc-resource"></a>SqlServerDsc DSC 리소스 설치

[SqlServerDsc](https://www.powershellgallery.com/packages/SqlServerDsc) DSC 리소스는 [Install-Module](https://docs.microsoft.com/powershell/module/powershellget/Install-Module?view=powershell-5.1) cmdlet을 사용하여 [PowerShell 갤러리](https://www.powershellgallery.com/)에서 다운로드할 수 있습니다. _참고: 모듈을 설치하려면 PowerShell이 "관리자 권한으로" 실행되고 있는지 확인하세요._

```PowerShell
Install-Module -Name SqlServerDsc
```

SQL Server 2017 설치 미디어를 입수하여 SQL Server 2017 설치 미디어를 서버에 다운로드합니다. 저는 Visual Studio 구독에서 SQL Server 2017 Enterprise를 다운로드하고 ISO를 "C:\en_sql_server_2017_enterprise_x64_dvd_11293666.iso"로 복사했습니다.

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

### <a name="configuration"></a>Configuration

[MOF(Managed Object Format)](https://docs.microsoft.com/windows/desktop/WmiSdk/managed-object-format--mof-) 문서를 생성하기 위해 호출될 구성 함수를 만듭니다.

```PowerShell
Configuration SQLInstall
{...}
```

### <a name="modules"></a>모듈

모듈을 현재 세션으로 가져옵니다. 이 모듈은 MOF 문서를 작성하는 방법을 구성 문서에 알려주고 MOF 문서를 서버에 적용하는 방법을 DSC 엔진에 알려줍니다.

```PowerShell
Import-DscResource -ModuleName SqlServerDsc
```

### <a name="resources"></a>리소스

#### <a name="net-framework"></a>.NET Framework

SQL Server는 .NET Framework에서 작동하므로 SQL Server를 설치하기 전에 .NET Framework를 설치해야 합니다. WindowsFeature 리소스는 Net-Framework-45-Core Windows 기능을 설치하는 데 활용됩니다.

```PowerShell
WindowsFeature 'NetFramework45'
{
     Name = 'Net-Framework-45-Core'
     Ensure = 'Present'
}
```

#### <a name="sqlsetup"></a>SqlSetup

SqlSetup 리소스는 SQL Server 설치 방법을 DSC에 알려주는 데 사용됩니다. 기본 설치에 필요한 매개 변수는 다음과 같습니다.

- **InstanceName**: 인스턴스의 이름입니다. 기본 인스턴스의 경우 MSSQLSERVER를 활용합니다.
- **Features**: 설치할 기능입니다. 이 예제에서는 SQLEngine 기능만 설치합니다.
- **SourcePath**: SQL 설치 미디어의 경로입니다. 이 예제에서는 "C:\SQL2017"에서 SQL 설치 미디어에 저장하겠습니다. 네트워크 공유를 활용하여 서버에서 사용되는 공간을 최소화할 수 있습니다.
- **SQLSysAdminAccounts**: sysadmin 역할의 구성원이 될 사용자 또는 그룹입니다. 이 예제에서는 로컬 관리자 그룹 sysadmin 액세스를 부여하겠습니다. _참고: 이 구성은 높은 보안 환경에서 권장되지 않습니다._

SqlSetup에서 사용할 수 있는 매개 변수의 전체 목록과 설명은 [SqlServerDsc GitHub 리포지토리](https://github.com/PowerShell/SqlServerDsc/tree/master#sqlsetup)에서 확인할 수 있습니다.

SqlSetup 리소스는 SQL만 설치하고 적용된 설정을 유지 관리하지 않기 때문에 적합하지 않습니다. 예를 들어, 설치 시 SQLSysAdminAccounts가 지정되면 관리자는 sysadmin 역할에 대한 로그인을 추가 또는 제거할 수 있지만 SqlSetup 리소스는 이에 관여하지 않습니다. DSC가 sysadmin 역할의 구성원 자격을 적용하려는 경우 [SqlServerRole](https://github.com/PowerShell/SqlServerDsc/tree/master#sqlserverrole) 리소스를 활용해야 합니다.

#### <a name="complete-configuration"></a>구성 완료

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

"SQLInstall"이라는 작업 디렉터리에 디렉터리가 만들어지며 "localhost.mof"라는 파일 호출이 포함됩니다. MOF의 콘텐츠를 검토하면 컴파일된 DSC 구성이 표시됩니다.

### <a name="deploy-the-configuration"></a>구성 배포

SQL Server의 DSC 배포를 시작하려면 Start-DscConfiguration cmdlet을 호출합니다. cmdlet에 제공된 매개 변수는 다음과 같습니다.

- **Path**: 배포할 MOF 문서에 포함된 폴더의 경로입니다. (예: "C:\SQLInstall")
- **Wait**: 구성 작업이 완료될 때까지 기다립니다.
- **Force**: 모든 기존 DSC 구성을 재정의합니다.
- **Verbose**: 자세한 정보 출력을 표시합니다. 문제 해결을 위해 처음으로 구성을 푸시할 때 유용합니다.

```PowerShell
Start-DscConfiguration -Path C:\SQLInstall -Wait -Force -Verbose
```

구성이 적용될 때 Verbose 출력은 현재 상황을 보여주고 어떤 상황인지를 따뜻하고 포근한 느낌으로 제공합니다. 오류(빨간색 텍스트)가 throw되지 않는 한 "Operation 'Invoke CimMethod' complete."가 화면에 표시되면 SQL이 설치된 것입니다.

## <a name="validate-installation"></a>설치 유효성 검사

### <a name="dsc"></a>DSC

[Test-DscConfiguration](https://docs.microsoft.com/powershell/module/psdesiredstateconfiguration/test-dscconfiguration) cmdlet을 활용하여 서버의 현재 상태(SQL가 설치된 경우)가 원하는 상태를 충족하는지 확인할 수 있습니다. Test-DscConfiguration의 결과는 "True"이어야 합니다.

```PowerShell
PS C:\> Test-DscConfiguration
True
```

### <a name="services"></a>서비스

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

## <a name="see-also"></a>관련 항목:

[Windows PowerShell Desired State Configuration 개요](https://docs.microsoft.com/powershell/dsc/overview)

[명령 프롬프트에서 SQL Server 설치](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)

[구성 파일을 사용하여 SQL Server 설치](../../database-engine/install-windows/install-sql-server-using-a-configuration-file.md)
