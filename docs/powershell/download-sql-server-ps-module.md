---
title: SQL Server PowerShell 모듈 다운로드
ms.prod: sql
ms.technology: scripting
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: carlrab
ms.custom: ''
ms.date: 01/23/2020
ms.openlocfilehash: 99976a12ae76254da5b50c5467df9d9e42fdbbce
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "76920353"
---
# <a name="install-the-sql-server-powershell-module"></a>SQL Server PowerShell 모듈 설치

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

이 문서에서는 **SqlServer** PowerShell 모듈 설치에 대한 지침을 제공합니다.

## <a name="powershell-modules-for-sql-server"></a>SQL Server용 PowerShell 모듈

SQL Server PowerShell 모듈에는 다음 두 가지가 있습니다.

- **SqlServer**: SqlServer 모듈에는 최신 SQL 기능을 지원하는 새 cmdlet이 포함되어 있습니다. 또한 이 모듈에는 **SQLPS**의 업데이트된 cmdlet 버전도 포함되어 있습니다. SqlServer 모듈을 다운로드하려면 [PowerShell 갤러리의 SqlServer 모듈](https://www.powershellgallery.com/packages/Sqlserver)로 이동합니다.
- **SQLPS**: SQLPS 모듈은 이전 버전과의 호환성을 위해 SQL Server 설치에 포함되어 있지만 더 이상 업데이트되지는 않습니다. 최신 PowerShell 모듈은 **SqlServer** 모듈입니다.

> [!NOTE]
> PowerShell 갤러리의 **SqlServer** 모듈 버전은 버전 관리를 지원하며 PowerShell 버전 5.0 이상이 필요합니다.

도움말 항목:

- [SqlServer](https://docs.microsoft.com/powershell/module/sqlserver) cmdlet.
- [SQLPS](https://docs.microsoft.com/powershell/module/sqlps) cmdlet.

## <a name="sql-server-management-studio"></a>SQL Server Management Studio

SSMS(SQL Server Management Studio) 버전 17.0부터는 PowerShell 모듈을 설치하지 않습니다. SSMS에서 PowerShell을 사용하려면 [PowerShell 갤러리](https://www.powershellgallery.com/packages/Sqlserver)에서 **SqlServer** 모듈을 설치합니다.

> [!NOTE]
> SSMS 버전 16.x를 사용하는 경우 이전 버전의 **SqlServer** 모듈이 SSMS(SQL Server Management Studio)에 포함되어 있습니다.

## <a name="azure-data-studio"></a>Azure Data Studio

Azure Data Studio도 PowerShell 모듈을 설치하지 않습니다. Azure Data Studio에서 PowerShell을 사용하려면 [PowerShell 갤러리](https://www.powershellgallery.com/packages/Sqlserver)에서 **SqlServer** 모듈을 설치합니다.

Azure Data Studio에서 풍부한 PowerShell 편집기 지원을 제공하는 [PowerShell 확장](../azure-data-studio/powershell-extension.md)을 사용할 수 있습니다.

## <a name="installing-or-updating-the-sqlserver-module"></a>SqlServer 모듈 설치 또는 업데이트

PowerShell 갤러리에서 **SqlServer** 모듈을 설치하려면 관리자로 [PowerShell](https://docs.microsoft.com/powershell/scripting/powershell-scripting) 세션을 시작합니다. 또한 관리자로 Azure Data Studio를 시작하고 통합 터미널의 PowerShell 세션에서 다음 명령을 실행합니다.

### <a name="install-the-sqlserver-module"></a>SqlServer 모듈 설치

PowerShell 세션에서 다음 명령을 실행하여 모든 사용자에 대해 SqlServer 모듈을 설치합니다.

```powershell
Install-Module -Name SqlServer
```

### <a name="to-view-the-versions-of-the-sqlserver-module-installed"></a>설치된 SqlServer 모듈의 버전을 보려면

다음 명령을 실행하여 설치된 SqlServer 모듈의 버전을 확인합니다.

```powershell
Get-Module SqlServer -ListAvailable
```

### <a name="install-for-the-current-user-rather-than-as-an-administrator"></a>관리자가 아닌 현재 사용자에 대해 설치

관리자로 PowerShell 세션을 실행할 수 없는 경우 다음 명령을 사용하여 현재 사용자에 대해 설치합니다.

```powershell
Install-Module -Name SqlServer -Scope CurrentUser
```

### <a name="to-overwrite-a-previous-version-of-the-sqlserver-module"></a>이전 버전의 SqlServer 모듈을 덮어쓰려면

`Install-Module` 명령을 사용하여 이전 버전을 덮어쓸 수도 있습니다.

```powershell
Install-Module -Name SqlServer -AllowClobber
```

> [!Note]
> PowerShell은 항상 설치된 최신 모듈을 사용합니다.

### <a name="update-the-installed-version-of-the-sqlserver-module"></a>설치된 SqlServer 모듈 버전 업데이트

**SqlServer** 모듈의 업데이트된 버전을 사용할 수 있는 경우 다음 명령을 사용하여 최신 버전을 설치할 수 있습니다.

```powershell
Install-Module -Name SqlServer -AllowClobber
```

`Update-Module` 명령을 사용하여 최신 버전의 SQLServer PowerShell 모듈을 설치할 수 있지만 이전 버전은 제거되지 않습니다. 최신 버전을 실험해 볼 수 있도록 최신 버전을 설치하지만 이전 모듈도 여전히 설치되어 있습니다.

이전 모듈 버전을 유지하지 않으려면 `Uninstall-Module` 명령을 사용하여 이전 버전을 제거할 수 있습니다.

둘 이상의 버전이 설치된 경우 다음 명령을 사용하여 나열할 수 있습니다.

```powershell
Get-Module SqlServer -ListAvailable
```

다음 명령을 사용하여 이전 버전을 제거할 수 있습니다.

```powershell
Uninstall-module -Name SQLServer -RequiredVersion "<version number>" -AllowClobber
```

### <a name="troubleshooting"></a>문제 해결

설치 시 문제가 발생할 경우 [Install-Module 설명서](https://www.powershellgallery.com/packages/PowerShellGet/2.2.1) 및 [Install-Module 참조](https://docs.microsoft.com/powershell/module/powershellget/Install-Module)를 참조하세요.

## <a name="using-a-specific-version-of-the-sqlserver-module"></a>특정 버전의 SqlServer 모듈 사용

특정 버전의 모듈을 사용하려면 다음 명령과 비슷한 특정 버전 번호를 사용하여 가져옵니다.

```powershell
Import-Module SqlServer -Version 21.1.18080
```

## <a name="pre-release-versions-of-the-sqlserver-module"></a>SqlServer 모듈의 시험판 버전

SqlServer 모듈의 시험판(또는 "미리 보기") 버전은 PowerShell 갤러리에서 사용할 수 있습니다.

> [!IMPORTANT]
> *-AllowPrerelease* 스위치를 전달하여 [PowerShellGet](https://www.powershellgallery.com/packages/PowerShellGet) 모듈의 일부인 업데이트된 *Find-Module* 및 *Install-Module* cmdlet을 사용하여 이러한 버전을 검색한 후 설치할 수 있습니다. 이러한 cmdlet을 사용하려면 PowerShellGet 모듈을 설치한 다음 새 세션을 엽니다.

### <a name="to-discover-pre-release-versions-of-the-sqlserver-module"></a>SqlServer 모듈의 시험판 버전을 검색하려면

SqlServer 모듈의 시험판(미리 보기) 버전을 검색하려면 다음 명령을 실행합니다.

```powershell
Find-Module SqlServer -AllowPrerelease
```

### <a name="to-install-a-specific-pre-release-version-of-the-sqlserver-module"></a>SqlServer 모듈의 특정 시험판 버전을 설치하려면

모듈의 특정 시험판 버전을 설치하려면 특정 버전 번호를 사용하여 설치합니다.

다음 명령을 사용할 수 있습니다.

```powershell
Install-Module SqlServer -RequiredVersion 21.1.18040-preview -AllowPrerelease
```

## <a name="sql-server-powershell-on-linux"></a>Linux의 SQL Server PowerShell

Linux에서 SQL Server PowerShell을 설치하는 방법을 알아보려면 [PowerShell Core를 사용하여 SQL Server on Linux 관리](../linux/sql-server-linux-manage-powershell-core.md)를 참조하세요.
