---
title: SQL Server PowerShell 도움말 보기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Help [PowerShell]
- Help [SQL Server], PowerShell
- PowerShell [SQL Server], help
ms.assetid: 968c316d-db83-4c24-8ea6-9f18736842f7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 705512f54feae3bf60317c18b8c260ef484abebc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72797879"
---
# <a name="get-help-sql-server-powershell"></a>Get Help SQL Server PowerShell
  Windows PowerShell의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 공급자 및 cmdlet 사용에 대한 정보를 얻을 수 있는 몇 가지 도움말이 있습니다. 여기서는 Windows PowerShell 환경에서 사용 가능한 도움말에 대해 알아봅니다.  
  
## <a name="before-you-begin"></a>시작하기 전에  
 Windows PowerShell에 대한 자세한 내용은 [Windows PowerShell 시작 가이드](https://technet.microsoft.com/library/hh857337.aspx)를 참조하십시오.  
  
 
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] cmdlet 및 공급자에 대한 개요는 [SQL Server PowerShell](../powershell/sql-server-powershell.md)을 참조하세요.  
  
### <a name="help-in-the-windows-powershell-environment"></a>Windows PowerShell 환경의 도움말  
 Windows PowerShell 환경에서 **Get-Help** cmdlet을 사용하여 도움말을 볼 수 있습니다. **Get-help** 는 windows powershell에서 제공 되는 다양 한 cmdlet 및 공급자와 windows powershell 언어에 대 한 기본적인 도움말을 제공 합니다.  
  
 
  **Get-Help**를 사용할 수 있는 방법은 [Get-Help: 도움말 보기](https://go.microsoft.com/fwlink/?LinkId=102136)를 참조하세요.  
  
### <a name="sql-server-powershell-provider-help"></a>SQL Server PowerShell 공급자 도움말  
 
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 공급자는 SQLSERVER 가상 드라이브에서 여러 폴더(예: SQLSERVER:\SQL 및 SQLSERVER:\DAC 폴더)를 구현합니다. 각 폴더는 SQL Server 관리 효율성 개체 모델 중 하나에 연결됩니다. SQL Server 경로에 각 노드에 연결된 메서드 및 속성을 나열할 수 있지만 PowerShell 환경에서 해당 메서드와 속성에 대한 도움말을 볼 수 없습니다. 연결된 프로그래밍 참조에 대한 링크를 제공하는 폴더 테이블은 [SQL Server PowerShell Provider](../powershell/sql-server-powershell-provider.md)를 참조하십시오.  
  
### <a name="invoke-sqlcmd-help"></a>Invoke-Sqlcmd 도움말  
 
  **Invoke-Sqlcmd** cmdlet은 **sqlcmd** 유틸리티를 통해 실행할 수 있는 모든 쿼리 또는 스크립트 파일을 입력으로 사용합니다. 
  **Get-Help** 를 사용하면 **Invoke-Sqlcmd** 및 해당 매개 변수에 대한 정보는 확인할 수 있지만, **Get-Help** 를 통해 **sqlcmd** 쿼리에 대한 정보를 확인할 수는 없습니다.  
  
 
  *-Query* 또는 *-QueryFromFile* 입력에는 다음이 포함될 수 있습니다.  
  
-   **sqlcmd** 변수 및 명령. 이러한 변수 및 명령에 대한 자세한 내용은 [sqlcmd Utility](../tools/sqlcmd-utility.md)의 주의 섹션을 참조하십시오.  
  
-   [!INCLUDE[tsql](../includes/tsql-md.md)]할당문. 
  [!INCLUDE[tsql](../includes/tsql-md.md)] 언어에 대한 자세한 내용은 [Transact-SQL 참조&#40;데이터베이스 엔진&#41;](/sql/t-sql/language-reference)를 참조하세요.  
  
-   XQuery 문. 
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 지원하는 XQuery 언어에 대한 자세한 내용은 [XQuery 언어 참조&#40;SQL Server&#41;](/sql/xquery/xquery-language-reference-sql-server)를 참조하세요.  
  
## <a name="get-help-for-a-sql-server-cmdlet"></a>SQL Server cmdlet에 대한 도움말 보기  
 **cmdlet에 대한 도움말을 보려면**  
  
-   cmdlet의 이름과 반환할 도움말의 수준을 지정하여 Get-Help를 실행합니다.  
  
### <a name="example-cmdlet-get-help"></a>예: Get-Help cmdlet  
 다음 예에서는 **Invoke-Sqlcmd**에 대한 다양한 수준의 도움말을 반환합니다.  
  
```powershell
## Get the basic help.  
Get-Help Invoke-Sqlcmd  
  
## Get the full help.  
Get-Help Invoke-Sqlcmd -Full  
  
## Get the parameter descriptions.  
Get-Help Invoke-Sqlcmd -Parameter *  
  
## Get the code examples.  
Get-Help Invoke-Sqlcmd -Examples  
  
## Get the syntax diagram.  
Get-Help Invoke-Sqlcmd -Syntax  
```  
  
## <a name="get-a-list-of-providers"></a>공급자 목록 가져오기  

### <a name="to-get-a-list-of-active-providers"></a>활성 공급자 목록을 가져오려면
  
1.  공급자 범주를 지정하여 Get-Help를 실행합니다.  
  
 Windows PowerShell에서 공급자 도움말을 보는 방법은 [드라이브 및 공급자(Drives and Providers)](https://go.microsoft.com/fwlink/?LinkId=102137)를 참조하십시오.  
  
### <a name="example-get-a-list-of-providers"></a>예: 공급자 목록 가져오기  
 다음 코드는 Windows PowerShell 세션에서 현재 사용 가능한 공급자의 목록을 반환합니다.  
  
```powershell
Get-Help -Category provider  
```  
  
## <a name="get-help-about-the-sql-server-provider"></a>SQL Server 공급자에 대한 도움말 가져오기  
 **공급자에 대 한 도움말을 보려면**  
  
1.  이름을 SQLServer로 지정하여 Get-Help를 실행합니다.  
  
### <a name="example-get-sql-server-provider-help"></a>예: SQL Server 공급자 도움말 가져오기  
 이 예에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 공급자에 대한 기본 정보를 반환합니다.  
  
```powershell
Get-Help SQLServer  
```  
  
## <a name="list-methods-and-properties"></a>메서드 및 속성 나열  
 **SQL Server 공급자 경로에서 노드에 대 한 메서드와 속성을 나열 하려면**  
  
1.  CD 명령으로 SQL Server 경로의 노드로 이동하거나 해당 위치로 설정된 변수를 만듭니다.  
  
2.  -Type 매개 변수를 메서드 또는 속성으로 설정 하 여 **Get Member** cmdlet을 실행 합니다.  
  
### <a name="examples-listing-methods-and-properties"></a>예: 메서드 및 속성 나열  
 이 예에서는 Databases 노드에 지원되는 메서드를 나열합니다.  
  
```powershell
Set-Location SQL:\MyComputer\DEFAULT\Databases  
Get-Item . | Get-Member -Type Methods  
```  
  
 이 예에서는 SMO Table 개체에 설정된 변수의 속성을 나열합니다.  
  
```powershell
$MyVar = New-Object Microsoft.SqlServer.Management.SMO.Table  
$MyVar | Get-Member -Type Properties  
```  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server PowerShell 공급자](../powershell/sql-server-powershell-provider.md)   
 [데이터베이스 엔진 cmdlet 사용](../../2014/database-engine/use-the-database-engine-cmdlets.md)  
