---
title: SQL Server PowerShell 모듈 다운로드 | Microsoft Docs
ms.custom: ''
ms.date: 01/05/2018
ms.prod: sql
ms.prod_service: powershell
ms.component: powershell
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords:
- sql server powershell 설치, sql server powershell 다운로드
ms.assetid: ''
caps.latest.revision: 113
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6790f25062e7d3bfaaae970f1ce4a42135c8ce6e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="install-sql-server-powershell-module"></a>SQL Server PowerShell 모듈 설치
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

이 문서에서는 **SqlServer** PowerShell 모듈 설치에 대한 지침을 제공합니다.

> [!NOTE]
> SQL Server PowerShell 모듈은 **SqlServer**와 **SQLPS**의 두 가지가 있습니다. **SQLPS** 모듈은 (이전 버전과의 호환성을 위해) SQL Server 설치에 포함되어 있지만 더 이상 업데이트되지는 않습니다. 최신 PowerShell 모듈은 **SqlServer** 모듈입니다. **SqlServer** 모듈은 **SQLPS**에 업데이트된 버전의 cmdlet이 포함되어 있으며, 최신 SQL 기능을 지원하는 새로운 cmdlet도 포함되어 있습니다. 이전 버전의 **SqlServer** 모듈은 SSMS(SQL Server Management Studio)에 *포함되었습니다*(SSMS 16.x 버전만 해당). SSMS 17.0 이상이 포함된 PowerShell을 사용하려면 PowerShell 갤러리에서 **SqlServer** 모듈을 설치해야 합니다.

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

```Import-Module SqlServer -Version 21.0.17178```


PowerShell 갤러리의 **SqlServer** 모듈 버전은 버전 관리를 지원하며 PowerShell 버전 5.0 이상이 필요합니다. 

* [PowerShell 갤러리의 SqlServer 모듈](https://www.powershellgallery.com/packages/Sqlserver) 
* [SqlServer cmdlet](https://docs.microsoft.com/powershell/module/sqlserver)
* [SQLPS cmdlet](https://docs.microsoft.com/powershell/module/sqlps)
