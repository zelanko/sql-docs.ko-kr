---
title: Windows PowerShell에서 SMO 어셈블리 로드 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: 8ca42b69-da5a-47f4-9085-34e443f0e389
author: stevestein
ms.author: sstein
ms.openlocfilehash: dc5d5f1a11603dac8e3d4aa075ccceb784d8ae15
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84960423"
---
# <a name="load-the-smo-assemblies-in-windows-powershell"></a>Windows PowerShell에서 SMO 어셈블리 로드
  이 항목에서는 SQL Server PowerShell 공급자를 사용하지 않는 Windows PowerShell 스크립트에서 SMO(SQL Server Management Object) 어셈블리를 로드하는 방법을 설명합니다.  
  
## <a name="before-you-begin"></a>시작하기 전에  
 SMO 어셈블리를 로드하는 기본 메커니즘은 `sqlps` 모듈을 로드하는 것입니다. 모듈에 포함된 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 공급자는 SMO 어셈블리를 자동으로 로드하며 PowerShell 스크립트에서 SMO 개체의 유용성을 확장하는 기능도 구현합니다.  
  
 SMO 어셈블리를 직접 로드해야 할 수 있는 두 가지 경우가 있습니다.  
  
-   스크립트에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 스냅인의 cmdlet 또는 공급자를 참조하는 첫 번째 명령 전에 SMO 개체를 참조하는 경우  
  
-   공급자 또는 cmdlet을 사용하지 않는 C# 또는 Visual Basic과 같은 다른 언어에서 SMO 코드를 이식하려는 경우  
  
## <a name="example-loading-the-sql-server-management-objects"></a>예제: SQL Server 관리 개체 로드  
 다음 코드는 SMO 어셈블리를 로드합니다.  
  
```powershell
# Loads the SQL Server Management Objects (SMO)  
  
$ErrorActionPreference = "Stop"  
  
$sqlpsreg = "HKLM:\SOFTWARE\Microsoft\PowerShell\1\ShellIds\Microsoft.SqlServer.Management.PowerShell.sqlps"  
  
if (Get-ChildItem $sqlpsreg -ErrorAction "SilentlyContinue")  
{  
    throw "SQL Server Provider for Windows PowerShell is not installed."  
}  
else  
{  
    $item = Get-ItemProperty $sqlpsreg  
    $sqlpsPath = [System.IO.Path]::GetDirectoryName($item.Path)  
}  
  
$assemblylist =   
"Microsoft.SqlServer.Management.Common",  
"Microsoft.SqlServer.Smo",  
"Microsoft.SqlServer.Dmf ",  
"Microsoft.SqlServer.Instapi ",  
"Microsoft.SqlServer.SqlWmiManagement ",  
"Microsoft.SqlServer.ConnectionInfo ",  
"Microsoft.SqlServer.SmoExtended ",  
"Microsoft.SqlServer.SqlTDiagM ",  
"Microsoft.SqlServer.SString ",  
"Microsoft.SqlServer.Management.RegisteredServers ",  
"Microsoft.SqlServer.Management.Sdk.Sfc ",  
"Microsoft.SqlServer.SqlEnum ",  
"Microsoft.SqlServer.RegSvrEnum ",  
"Microsoft.SqlServer.WmiEnum ",  
"Microsoft.SqlServer.ServiceBrokerEnum ",  
"Microsoft.SqlServer.ConnectionInfoExtended ",  
"Microsoft.SqlServer.Management.Collector ",  
"Microsoft.SqlServer.Management.CollectorEnum",  
"Microsoft.SqlServer.Management.Dac",  
"Microsoft.SqlServer.Management.DacEnum",  
"Microsoft.SqlServer.Management.Utility"  
  
foreach ($asm in $assemblylist)  
{  
    $asm = [Reflection.Assembly]::LoadWithPartialName($asm)  
}  
  
Push-Location  
cd $sqlpsPath  
Update-FormatData -PrependPath SQLProvider.Format.ps1xml
Pop-Location  
```  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server PowerShell](sql-server-powershell.md)  
