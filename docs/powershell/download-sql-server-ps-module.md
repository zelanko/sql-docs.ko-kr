---
title: SQL Server PowerShell 모듈 다운로드 | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
keywords:
- sql server powershell 설치, sql server powershell 다운로드
ms.assetid: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f0f14a3cee050fff07c7fe5bc2467bcb8209a53c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62672572"
---
# <a name="install-sql-server-powershell-module"></a>SQL Server PowerShell 모듈 설치
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

이 문서에서는 **SqlServer** PowerShell 모듈 설치에 대한 지침을 제공합니다.
> [!NOTE]
> SQL Server PowerShell 모듈에는 다음 두 가지가 있습니다. 
> * **SQLPS**: 이 모듈은 SQL Server 설치(이전 버전과의 호환성을 위해)에 포함되어 있지만 더 이상 업데이트되지 않습니다. 최신 PowerShell 모듈은 **SqlServer** 모듈입니다.
> * **SqlServer**: 이 모듈에는 최신 SQL 기능을 지원하는 새 cmdlet이 포함되어 있습니다. 또한 이 모듈에는 **SQLPS**의 업데이트된 cmdlet 버전도 포함되어 있습니다. 

이전 버전의 **SqlServer** 모듈은 SSMS(SQL Server Management Studio)에 *포함되었습니다*(SSMS 16.x 버전만 해당). SSMS 17.0 이상이 포함된 PowerShell을 사용하려면 [PowerShell 갤러리](https://www.powershellgallery.com/packages/Sqlserver)에서 **SqlServer** 모듈을 설치해야 합니다.
**SqlServer** 모듈의 현재 버전은 21.1.18080입니다. 이는 Microsoft.SQLServer.SMO의 버전 v150을 기반으로 하며 다음 버전의 SQL Server를 지원합니다. Microsoft.SQLServer.SMO의 버전 v140을 기반으로 하는 모듈의 마지막 버전)은 21.0.17279입니다.

모듈의 시험판 버전은 더 자주 제공될 수 있습니다. 이러한 버전의 모듈을 가져오는 방법에 대해서는 이 페이지 하단의 섹션을 참조하세요.

PowerShell 갤러리에서 **SqlServer** 모듈을 설치하려면 [PowerShell](https://docs.microsoft.com/powershell/scripting/powershell-scripting) 세션을 시작하고 다음 명령을 사용합니다. 설치 시 문제가 발생할 경우 [Install-Module 설명서](https://docs.microsoft.com/powershell/gallery/psget/module/psget_install-module) 및 [Install-Module 참조](https://docs.microsoft.com/powershell/module/powershellget/Install-Module)를 참조하세요.

**SqlServer** 모듈을 설치하려면

```Install-Module -Name SqlServer```

컴퓨터에 이전 버전의 **SqlServer** 모듈이 있을 경우 `Update-Module`(이 문서의 뒷부분에서 설명)을 사용하거나 `-AllowClobber` 매개 변수를 제공할 수 있습니다.  

```Install-Module -Name SqlServer -AllowClobber```

PowerShell 세션을 관리자 권한으로 실행할 수 없는 경우 현재 사용자를 위해 설치할 수 있습니다.

```Install-Module -Name SqlServer -Scope CurrentUser```

업데이트된 버전의 **SqlServer** 모듈을 사용할 수 있는 경우 `Update-Module`을 사용하여 버전을 업데이트할 수 있습니다.

```Update-Module -Name SqlServer```

설치된 모듈 버전을 보려면

```Get-Module SqlServer -ListAvailable```

특정 버전의 모듈을 사용하려면 다음과 유사한 특정 버전 번호를 사용하여 가져올 수 있습니다.

```Import-Module SqlServer -Version 21.1.18080```

> [!NOTE]
> 모듈의 시험판(또는 “미리 보기”) 버전은 PowerShell 갤러리에서 사용할 수 있습니다. *-AllowPrerelease* 스위치를 전달하여 [PowerShellGet](https://www.powershellgallery.com/packages/PowerShellGet) 모듈의 일부인 업데이트된 *Find-Module* 및 *Install-Module* cmdlet을 사용하여 이러한 버전을 검색한 후 설치할 수 있습니다.
>
> 모듈의 시험판/미리 보기 버전을 확인하려면 다음 명령을 실행할 수 있습니다.
>
> ```Find-Module SqlServer -AllowPrerelease```
>
> 특정 시험판/미리 보기 버전의 모듈을 설치하려면 다음과 유사한 특정 버전 번호를 사용하여 설치할 수 있습니다.
>
> ```Install-Module SqlServer -RequiredVersion 21.1.18040-preview -AllowPrerelease```
> 

PowerShell 갤러리의 **SqlServer** 모듈 버전은 버전 관리를 지원하며 PowerShell 버전 5.0 이상이 필요합니다. 

* [PowerShell 갤러리의 SqlServer 모듈](https://www.powershellgallery.com/packages/Sqlserver) 
* [SqlServer cmdlet](https://docs.microsoft.com/powershell/module/sqlserver)
* [SQLPS cmdlet](https://docs.microsoft.com/powershell/module/sqlps)
