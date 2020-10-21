---
title: SQL Server PowerShell 모듈 다운로드
description: SqlServer PowerShell 모듈을 설치하는 방법을 알아봅니다. 이 모듈은 최신 SQL 기능을 지원하는 cmdlet을 제공하며 SQLPS 모듈에 업데이트된 버전의 cmdlet도 포함합니다.
ms.prod: sql
ms.technology: sql-server-powershell
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: matteot, drskwier
ms.custom: ''
ms.date: 10/14/2020
ms.openlocfilehash: 21730bf32e66c5954b2447037286dfdc10717e9c
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081542"
---
# <a name="install-the-sql-server-powershell-module"></a>SQL Server PowerShell 모듈 설치

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

이 문서에서는 **SqlServer** PowerShell 모듈 설치에 대한 지침을 제공합니다.

## <a name="powershell-modules-for-sql-server"></a>SQL Server용 PowerShell 모듈

SQL Server PowerShell 모듈에는 다음 두 가지가 있습니다.

- **SqlServer**: SqlServer 모듈에는 최신 SQL 기능을 지원하는 새 cmdlet이 포함되어 있습니다. 또한 이 모듈에는 **SQLPS**의 업데이트된 cmdlet 버전도 포함되어 있습니다. SqlServer 모듈을 다운로드하려면 [PowerShell 갤러리의 SqlServer 모듈](https://www.powershellgallery.com/packages/Sqlserver)로 이동합니다.

- **SQLPS**: SQLPS는 PowerShell 하위 시스템을 사용하여 에이전트 작업 단계에서 에이전트 작업을 실행하기 위해 [SQL 에이전트](sql-server-powershell.md#sql-server-agent)에서 사용하는 모듈입니다.

> [!NOTE]
> PowerShell 갤러리의 **SqlServer** 모듈 버전은 버전 관리를 지원하며 PowerShell 버전 5.0 이상이 필요합니다.

도움말 항목:

- [SqlServer](/powershell/module/sqlserver) cmdlet.
- [SQLPS](/powershell/module/sqlps) cmdlet.

## <a name="sql-server-management-studio"></a>SQL Server Management Studio

[SSMS(SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md)도 PowerShell 모듈을 설치하지 않습니다. SSMS에서 PowerShell을 사용하려면 [PowerShell 갤러리](https://www.powershellgallery.com/packages/Sqlserver)에서 **SqlServer** 모듈을 설치합니다.

> [!NOTE]
> SSMS 16.x를 사용하는 경우 이전 버전의 **SqlServer** 모듈이 SSMS(SQL Server Management Studio)에 포함되어 있습니다.

## <a name="azure-data-studio"></a>Azure Data Studio

[Azure Data Studio](../azure-data-studio/download-azure-data-studio.md)도 PowerShell 모듈을 설치하지 않습니다. Azure Data Studio에서 PowerShell을 사용하려면 [PowerShell 갤러리](https://www.powershellgallery.com/packages/Sqlserver)에서 **SqlServer** 모듈을 설치합니다.

Azure Data Studio에서 풍부한 PowerShell 편집기 지원을 제공하는 [PowerShell 확장](../azure-data-studio/extensions/powershell-extension.md)을 사용할 수 있습니다.

## <a name="installing-or-updating-the-sqlserver-module"></a>SqlServer 모듈 설치 또는 업데이트

PowerShell 갤러리에서 **SqlServer** 모듈을 설치하려면 관리자로 [PowerShell](/powershell/scripting/overview) 세션을 시작합니다. 또한 통합 터미널의 PowerShell 세션에서 관리자로 Azure Data Studio를 시작하고 다음 명령을 실행할 수 있습니다.

*Install-Module SQLServer -Scope CurrentUser*를 사용하여 상승된 권한을 실행할 수도 있습니다. 이 cmdlet은 해당 환경에서 관리자가 아닌 사용자에게 유용합니다. 그러나 범위가 현재 사용자로 제한되기 때문에 동일한 컴퓨터의 다른 사용자가 이 모듈을 사용할 수 없습니다.

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

설치 시 문제가 발생할 경우 [Install-Module 설명서](https://www.powershellgallery.com/packages/PowerShellGet/2.2.1) 및 [Install-Module 참조](/powershell/module/powershellget/Install-Module)를 참조하세요.

## <a name="using-a-specific-version-of-the-sqlserver-module"></a>특정 버전의 SqlServer 모듈 사용

특정 버전의 모듈을 사용하려면 다음 명령과 비슷한 특정 버전 번호를 사용하여 가져옵니다.

```powershell
Import-Module SqlServer -Version 21.1.18218
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
Install-Module SqlServer -RequiredVersion 21.1.18218-preview -AllowPrerelease
```

## <a name="sql-server-powershell-on-linux"></a>Linux의 SQL Server PowerShell

Linux에서 SQL Server PowerShell을 설치하는 방법을 알아보려면 [PowerShell Core를 사용하여 SQL Server on Linux 관리](../linux/sql-server-linux-manage-powershell-core.md)를 참조하세요.

## <a name="other-modules"></a>기타 모듈

- [Az.Sql](https://www.powershellgallery.com/packages/Az.Sql/) - Windows PowerShell 및 PowerShell Core의 Azure Resource Manager를 위한 SQL 서비스 cmdlet입니다.

- [SqlServerDsc](https://www.powershellgallery.com/packages/SqlServerDsc/) - Microsoft SQL Server의 배포 및 구성을 위한 DSC 리소스가 포함된 모듈입니다.

## <a name="cmdlet-reference"></a>Cmdlet 참조

- [SqlServer cmdlet](https://docs.microsoft.com/powershell/module/sqlserver)
- [SQLPS cmdlet](https://docs.microsoft.com/powershell/module/sqlps)

## <a name="next-steps"></a>다음 단계

- [SQL Server PowerShell](sql-server-powershell.md)
- [SQL Server PowerShell cmdlet](https://docs.microsoft.com/powershell/module/sqlserver)
- [Azure Data Studio와 함께 PowerShell 사용](../azure-data-studio/extensions/powershell-extension.md)