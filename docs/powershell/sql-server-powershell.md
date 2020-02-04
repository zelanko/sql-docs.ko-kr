---
title: SQL Server PowerShell | Microsoft 문서
ms.custom: ''
ms.date: 08/04/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: 89b70725-bbe7-4ffe-a27d-2a40005a97e7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7a2725586a094aed0cb7d933553bc3fc389adfdf
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67912210"
---
# <a name="sql-server-powershell"></a>SQL Server PowerShell
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

**[SQL Server PowerShell 설치](download-sql-server-ps-module.md)**

> [!NOTE]
> SQL Server PowerShell 모듈은 **SqlServer**와 **SQLPS**의 두 가지가 있습니다. **SQLPS** 모듈은 (이전 버전과의 호환성을 위해) SQL Server 설치에 포함되어 있지만 더 이상 업데이트되지는 않습니다. 최신 PowerShell 모듈은 **SqlServer** 모듈입니다. **SqlServer** 모듈은 **SQLPS**에 업데이트된 버전의 cmdlet이 포함되어 있으며, 최신 SQL 기능을 지원하는 새로운 cmdlet도 포함되어 있습니다.  
> 이전 버전의 **SqlServer** 모듈은 SSMS(SQL Server Management Studio)에 *포함되었습니다*(SSMS 16.x 버전만 해당). SSMS 17.0 이상이 포함된 PowerShell을 사용하려면 PowerShell 갤러리에서 **SqlServer** 모듈을 설치해야 합니다.
> **SqlServer** 모듈을 설치하려면 [SQL Server PowerShell 설치](download-sql-server-ps-module.md)를 참조하세요.

**모듈이 SQLPS에서 SqlServer로 변경된 이유는 무엇인가요?**

SQL PowerShell 업데이트를 제공하기 위해 SQL PowerShell 모듈의 ID와 *SQLPS.exe*라고 하는 래퍼를 변경해야 했습니다. 이러한 변경으로 인해 이제 **SqlServer** 모듈과 **SQLPS** 모듈이라는 두 가지 SQL PowerShell 모듈이 있습니다.  

**SQLPS 모듈을 가져오는 PowerShell 스크립트를 업데이트하세요.**

`Import-Module -Name SQLPS`를 실행하는 PowerShell 스크립트가 있다면 새로운 공급자 기능과 새로운 cmdlet을 활용하는 것이 좋으며 이를 `Import-Module -Name SqlServer`로 변경해야 합니다. 새 모듈은 `%ProgramFiles%\WindowsPowerShell\Modules\SqlServer` 폴더에 설치됩니다. 따라서 $env:PSModulePath 변수를 업데이트할 필요가 없습니다. **SqlServer**라는 타사 또는 커뮤니티 버전의 모듈을 사용하는 스크립트가 있다면 Prefix 매개 변수를 사용하여 이름 충돌을 방지하세요.

SQL Server 에이전트에서 사용하는 모듈에 대한 변경 사항은 없습니다. 따라서 PowerShell 형식의 작업 단계에서는 SQLPS 모듈을 사용합니다. 자세한 내용은 [SQL Server 에이전트에서 PowerShell을 실행하는 방법](run-windows-powershell-steps-in-sql-server-agent.md)을 참조하세요.


## <a name="sql-server-powershell-components"></a>SQL Server PowerShell 구성 요소  
**SqlServer** 모듈은 두 개의 Windows PowerShell 스냅인을 로드합니다.  
  
-   파일 시스템 경로와 유사한 간단한 탐색 메커니즘을 제공하는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 공급자. 드라이브가 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 관리 개체 모델과 연결되고 노드가 개체 모델 클래스를 기반으로 하는 파일 시스템 경로와 비슷한 경로를 작성할 수 있습니다. 그런 다음 명령 프롬프트 창에서 폴더를 탐색하는 것과 비슷한 방법으로 **cd** 및 **dir** 과 같은 친숙한 명령을 사용하여 경로를 탐색할 수 있습니다. **ren** 또는 **del**과 같은 다른 명령을 사용하여 경로의 노드에 동작을 수행할 수 있습니다.  
  
-   **또는 XQuery 문이 포함된**sqlcmd[!INCLUDE[tsql](../includes/tsql-md.md)] 스크립트 실행과 같은 동작을 지원하는 cmdlet 집합.  
  
  
## <a name="sql-server-versions"></a>SQL Server 버전  
SQL PowerShell cmdlet을 사용하여 Azure SQL Database, Azure SQL Data Warehouse 및 모든 [지원되는 SQL Server 제품](https://support.microsoft.com/lifecycle/search/1044)의 인스턴스를 관리할 수 있습니다.  


## <a name="sql-server-identifiers-that-contain-characters-not-supported-in-powershell-paths"></a>PowerShell 경로에서 지원되지 않는 문자가 포함된 SQL Server 식별자  
 
**Encode-Sqlname** 및 **Decode-Sqlname** cmdlet을 사용하면 PowerShell 경로에서 지원되지 않는 문자가 포함된 SQL Server 식별자를 지정할 수 있습니다. 자세한 내용은 [SQL Server Identifiers in PowerShell](sql-server-identifiers-in-powershell.md)을(를) 참조하세요.  
  
**Convert-UrnToPath** cmdlet을 사용하면 [!INCLUDE[ssDE](../includes/ssde-md.md)] 개체의 URN을 SQL Server PowerShell 공급자의 경로로 변환할 수 있습니다. 자세한 내용은 [Convert URNs to SQL Server Provider Paths](https://docs.microsoft.com/powershell/module/sqlserver/Convert-UrnToPath)을(를) 참조하세요.  
  
## <a name="query-expressions-and-unique-resource-names"></a>쿼리 식 및 Unique Resource Names  

쿼리 식은 개체 모델 계층 구조에 있는 하나 이상의 개체를 열거하는 조건 집합을 지정하기 위해 XPath와 유사한 구문을 사용하는 문자열입니다. URN(Unique Resource Name)은 단일 개체를 고유하게 식별하는 특정 유형의 쿼리 식 문자열입니다. 자세한 내용은 [Query Expressions and Uniform Resource Names](query-expressions-and-uniform-resource-names.md)을(를) 참조하세요.       


## <a name="cmdlet-reference"></a>Cmdlet 참조
* [SqlServer cmdlet](https://docs.microsoft.com/powershell/module/sqlserver)
* [SQLPS cmdlet](https://docs.microsoft.com/powershell/module/sqlps)
