---
title: SQL Server PowerShell
description: PowerShell 공급자 및 cmdlet을 포함하는 두 개의 SQL Server PowerShell 모듈 SqlServer 및 SQLPS에 대해 알아봅니다.
ms.prod: sql
ms.technology: scripting
ms.topic: conceptual
ms.assetid: 89b70725-bbe7-4ffe-a27d-2a40005a97e7
author: markingmyname
ms.author: maghan
ms.reviewer: matteot
ms.custom: ''
ms.date: 06/11/2020
ms.openlocfilehash: f08c2917e225bf96422e7ea27aae9baab31390fd
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86921537"
---
# <a name="sql-server-powershell"></a>SQL Server PowerShell

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

**[SQL Server PowerShell 설치](download-sql-server-ps-module.md)**

SQL Server PowerShell 모듈은 **SqlServer**와 **SQLPS**의 두 가지가 있습니다. **SQLPS** 모듈은 (이전 버전과의 호환성을 위해) SQL Server 설치에 포함되어 있지만 더 이상 업데이트되지는 않습니다. 최신 PowerShell 모듈은 **SqlServer** 모듈입니다. **SqlServer** 모듈은 **SQLPS**에 업데이트된 버전의 cmdlet이 포함되어 있으며, 최신 SQL 기능을 지원하는 새로운 cmdlet도 포함되어 있습니다.  

이전 버전의 **SqlServer** 모듈은 SSMS(SQL Server Management Studio)에 포함되었습니다(SSMS 16.x 버전만 해당).

SSMS 17.0 이상이 포함된 PowerShell을 사용하려면 PowerShell 갤러리에서 **SqlServer** 모듈을 설치해야 합니다.

**SqlServer** 모듈을 설치하려면 [SQL Server PowerShell 설치](download-sql-server-ps-module.md)를 참조하세요.

**모듈이 SQLPS에서 SqlServer로 변경된 이유는 무엇인가요?**

SQL PowerShell 업데이트를 제공하기 위해 SQL PowerShell 모듈의 ID와 *SQLPS.exe*라는 래퍼를 변경해야 했습니다. 이러한 변경으로 인해 이제 **SqlServer** 모듈과 **SQLPS** 모듈이라는 두 가지 SQL PowerShell 모듈이 있습니다.  

**SQLPS 모듈을 가져오는 경우 PowerShell 스크립트를 업데이트하세요.**

`Import-Module -Name SQLPS`를 실행하는 PowerShell 스크립트가 있다면 새로운 공급자 기능과 새로운 cmdlet을 활용하는 것이 좋으며 이를 `Import-Module -Name SqlServer`로 변경해야 합니다. 새 모듈은 `%ProgramFiles%\WindowsPowerShell\Modules\SqlServer` 폴더에 설치됩니다. 따라서 $env:PSModulePath 변수를 업데이트할 필요가 없습니다. **SqlServer**라는 타사 또는 커뮤니티 버전의 모듈을 사용하는 스크립트가 있다면 Prefix 매개 변수를 사용하여 이름 충돌을 방지하세요.

SQLPS 모듈이 동일한 컴퓨터에 설치되어 있는 경우 Side-by-Side 문제를 방지하려면 *Import-Module SQLServer*를 사용하여 스크립트를 시작하는 것이 좋습니다.

이 섹션은 SQL 에이전트가 아닌 PowerShell에서 실행되는 스크립트에 적용됩니다. 새 모듈은 [#NOSQLPS](#sql-server-agent)를 사용하는 SQL 에이전트 작업 단계에서 사용할 수 있습니다.

## <a name="sql-server-powershell-components"></a>SQL Server PowerShell 구성 요소

**SqlServer** 모듈은 다음과 함께 제공됩니다.

- 파일 시스템 경로와 유사한 간단한 탐색 메커니즘을 제공하는 [PowerShell 공급자](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_providers). 드라이브가 SQL Server 관리 개체 모델과 연결되고 노드가 개체 모델 클래스를 기반으로 하는 파일 시스템 경로와 비슷한 경로를 작성할 수 있습니다. 그런 다음 명령 프롬프트 창에서 폴더를 탐색하는 것과 비슷한 방법으로 **cd** 및 **dir** 과 같은 친숙한 명령을 사용하여 경로를 탐색할 수 있습니다. **ren** 또는 **del**과 같은 다른 명령을 사용하여 경로의 노드에 동작을 수행할 수 있습니다.

- Transact-SQL 또는 XQuery 문이 포함된 **sqlcmd** 스크립트 실행과 같은 동작을 지원하는 cmdlet 집합.  

- AS 공급자 및 cmdlet(이전에는 별도로 설치됨).

## <a name="sql-server-versions"></a>SQL Server 버전

SQL PowerShell cmdlet을 사용하여 Azure SQL Database, Azure SQL Data Warehouse 및 모든 [지원되는 SQL Server 제품](https://support.microsoft.com/lifecycle/search/1044)의 인스턴스를 관리할 수 있습니다.

## <a name="sql-server-identifiers-that-contain-characters-not-supported-in-powershell-paths"></a>PowerShell 경로에서 지원되지 않는 문자가 포함된 SQL Server 식별자

**Encode-Sqlname** 및 **Decode-Sqlname** cmdlet을 사용하면 PowerShell 경로에서 지원되지 않는 문자가 포함된 SQL Server 식별자를 지정할 수 있습니다. 자세한 내용은 [SQL Server Identifiers in PowerShell](sql-server-identifiers-in-powershell.md)을(를) 참조하세요.

**Convert-UrnToPath** cmdlet을 사용하면 데이터베이스 엔진 개체의 URN을 SQL Server PowerShell 공급자의 경로로 변환할 수 있습니다. 자세한 내용은 [Convert URNs to SQL Server Provider Paths](https://docs.microsoft.com/powershell/module/sqlserver/Convert-UrnToPath)을(를) 참조하세요.
  
## <a name="query-expressions-and-unique-resource-names"></a>쿼리 식 및 Unique Resource Names  

쿼리 식은 개체 모델 계층 구조에 있는 하나 이상의 개체를 열거하는 조건 집합을 지정하기 위해 XPath와 유사한 구문을 사용하는 문자열입니다. URN(Unique Resource Name)은 단일 개체를 고유하게 식별하는 특정 유형의 쿼리 식 문자열입니다. 자세한 내용은 [Query Expressions and Uniform Resource Names](query-expressions-and-uniform-resource-names.md)을(를) 참조하세요.

## <a name="sql-server-agent"></a>SQL Server 에이전트

SQL Server 에이전트에서 사용하는 모듈에 대한 변경 사항은 없습니다. 따라서 PowerShell 유형 작업 단계를 포함하는 SQL Server 에이전트 작업은 SQLPS 모듈을 사용합니다. 자세한 내용은 [SQL Server 에이전트에서 PowerShell을 실행하는 방법](run-windows-powershell-steps-in-sql-server-agent.md)을 참조하세요. 그러나 SQL Server 2019부터 SQLPS를 사용하지 않도록 설정할 수 있습니다. 이렇게 하려면 PowerShell 유형 작업 단계의 첫 번째 줄에 `#NOSQLPS`를 추가할 수 있습니다. 그러면 SQL 에이전트가 SQLPS 모듈을 자동으로 로드하지 않습니다. 이렇게 하면 SQL 에이전트 작업이 컴퓨터에 설치된 PowerShell 버전을 실행하므로 원하는 다른 PowerShell 모듈을 사용할 수 있습니다.

SQL 에이전트 작업 단계에서 **SqlServer** 모듈을 사용하려는 경우 스크립트의 처음 두 줄에 다음 코드를 배치할 수 있습니다.

```powershell
#NOSQLPS
Import-Module -Name SqlServer
```

## <a name="cmdlet-reference"></a>Cmdlet 참조

- [SqlServer cmdlet](https://docs.microsoft.com/powershell/module/sqlserver)
- [SQLPS cmdlet](https://docs.microsoft.com/powershell/module/sqlps)

## <a name="next-steps"></a>다음 단계

[SQL Server PowerShell 모듈 다운로드](download-sql-server-ps-module.md)
