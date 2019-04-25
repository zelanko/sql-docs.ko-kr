---
title: SQL Server PowerShell 공급자 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
helpviewer_keywords:
- PowerShell [SQL Server], provider
- PowerShell [SQL Server], SQL Server PowerShell Provider
- Providers [PowerShell]
- SMO [SQL Server], PowerShell
- PowerShell [SQL Server], SMO
- SQL Server Management Objects, PowerShell
ms.assetid: b97acc43-fcd2-4ae5-b218-e183bab916f9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3e8fc0f770d8763ccb330b3c7588a97604d876e8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62762845"
---
# <a name="sql-server-powershell-provider"></a>SQL Server PowerShell Provider
  Windows PowerShell용 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 공급자는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 개체의 계층 구조를 파일 시스템 경로와 비슷한 경로에 표시합니다. 이 경로를 사용하여 개체를 찾은 다음 SMO( [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Object) 모델의 메서드를 사용하여 개체에 대해 동작을 수행할 수 있습니다.  
  
## <a name="benefits-of-the-sql-server-powershell-provider"></a>SQL Server PowerShell 공급자의 이점  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 공급자가 구현하는 경로에 따라 SQL Server 인스턴스의 모든 개체를 대화식으로 쉽게 검토할 수 있습니다. 파일 시스템 경로를 탐색하는 데 일반적으로 사용되는 명령과 비슷한 Windows PowerShell 별칭을 사용하여 경로를 탐색할 수 있습니다.  
  
## <a name="the-sql-server-powershell-hierarchy"></a>SQL Server PowerShell 계층 구조  
 데이터나 개체 모델을 계층 구조로 표현할 수 있는 제품은 Windows PowerShell 공급자를 사용하여 계층 구조를 표시합니다. Windows 파일 시스템에 사용되는 것과 유사한 드라이브 및 경로 구조를 사용하여 계층 구조를 표시합니다.  
  
 각 Windows PowerShell 공급자는 하나 이상의 드라이브를 구현합니다. 각 드라이브는 관련 개체 계층 구조의 루트 노드를 나타냅니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 공급자는 SQLSERVER: 드라이브를 구현합니다. 또한 공급자는 SQLSERVER: 드라이브에 대한 기본 폴더 집합을 정의합니다. 각 폴더 및 해당 하위 폴더는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 관리 개체 모델을 사용하여 액세스할 수 있는 개체 집합을 나타냅니다. 이러한 주 폴더 중 하나로 시작하는 경로의 하위 폴더에 포커스를 설정하면 관련 개체 모델의 메서드를 사용하여 이러한 노드가 나타내는 개체에 대해 동작을 수행할 수 있습니다. [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 공급자가 구현하는 Windows PowerShell 폴더는 다음 테이블에 나열되어 있습니다.  
  
|Folder|SQL Server 개체 모델 네임스페이스|개체|  
|------------|---------------------------------------|-------------|  
|SQLSERVER:\SQL|<xref:Microsoft.SqlServer.Management.Smo><br /><br /> <xref:Microsoft.SqlServer.Management.Smo.Agent><br /><br /> <xref:Microsoft.SqlServer.Management.Smo.Broker><br /><br /> <xref:Microsoft.SqlServer.Management.Smo.Mail>|테이블, 뷰 및 저장 프로시저와 같은 데이터베이스 개체입니다.|  
|SQLSERVER:\SQLPolicy|<xref:Microsoft.SqlServer.Management.Dmf><br /><br /> <xref:Microsoft.SqlServer.Management.Facets>|정책 및 패싯과 같은 정책 기반 관리 개체입니다.|  
|SQLSERVER:\SQLRegistration|<xref:Microsoft.SqlServer.Management.RegisteredServers><br /><br /> <xref:Microsoft.SqlServer.Management.Smo.RegSvrEnum>|서버 그룹 및 등록된 서버와 같은 등록된 서버 개체입니다.|  
|SQLSERVER:\Utility|<xref:Microsoft.SqlServer.Management.Utility>|[!INCLUDE[ssDE](../includes/ssde-md.md)]의 관리되는 인스턴스와 같은 유틸리티 개체입니다.|  
|SQLSERVER:\DAC|<xref:Microsoft.SqlServer.Management.DAC>|DAC 패키지와 같은 데이터 계층 애플리케이션 개체 및 DAC 배포와 같은 작업입니다.|  
|SQLSERVER:\DataCollection|<xref:Microsoft.SqlServer.Management.Collector>|컬렉션 집합 및 구성 저장소와 같은 데이터 수집기 개체입니다.|  
|SQLSERVER:\IntegrationServices|<xref:Microsoft.SqlServer.Management.IntegrationServices>|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 개체.|  
|SQLSERVER:\SQLAS|<xref:Microsoft.AnalysisServices>|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 개체|  
  
 예를 들어 SQLSERVER:\SQL 폴더를 사용하여 SMO 개체 모델에서 지원하는 개체를 표시할 수 있는 경로를 시작할 수 있습니다. SQLSERVER:\SQL 경로의 앞쪽 부분은 SQLSERVER:\SQL\\*ComputerName*\\*InstanceName*입니다. 인스턴스 이름 뒤에 오는 노드에는 개체 컬렉션(예: *데이터베이스* 또는 *뷰*)과 개체 이름(예: AdventureWorks2012)이 번갈아 사용됩니다. 스키마는 개체 클래스로 표현되지 않습니다. 스키마의 테이블 또는 뷰와 같은 최상위 수준 개체에 대한 노드를 지정할 때는 개체 이름을 *SchemaName.ObjectName*형식으로 지정해야 합니다.  
  
 다음은 로컬 컴퓨터의 기본 [!INCLUDE[ssDE](../includes/ssde-md.md)] 인스턴스에서 AdventureWorks2012 데이터베이스의 Purchasing 스키마에 있는 Vendor 테이블의 경로입니다.  
  
```  
SQLSERVER:\SQL\localhost\DEFAULT\Databases\AdventureWorks2012\Tables\Purchasing.Vendor  
```  
  
 SMO 개체 모델 계층 구조에 대한 자세한 내용은 [SMO Object Model Diagram](../relational-databases/server-management-objects-smo/smo-object-model-diagram.md)을 참조하십시오.  
  
 경로의 컬렉션 노드는 관련된 개체 모델의 컬렉션 클래스와 관련이 있습니다. 다음 테이블에 나와 있듯이 개체 이름 노드는 관련된 개체 모델의 개체 클래스와 관련이 있습니다.  
  
|경로|SMO 클래스|  
|----------|---------------|  
|SQLSERVER:\SQL\MyComputer\DEFAULT\Databases|<xref:Microsoft.SqlServer.Management.Smo.DatabaseCollection>|  
|SQLSERVER:\SQL\MyComputer\DEFAULT\Databases\AdventureWorks2012|<xref:Microsoft.SqlServer.Management.Smo.Database>|  
  
## <a name="sql-server-provider-tasks"></a>SQL Server 공급자 태스크  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|Windows PowerShell cmdlet을 사용하여 경로의 노드를 탐색하고 각 노드에서 해당 노드의 개체 목록을 가져오는 방법에 대해 설명합니다.|[SQL Server PowerShell 경로 탐색](navigate-sql-server-powershell-paths.md)|  
|SMO 메서드와 속성을 사용하여 경로의 노드에 표시되는 개체에 대해 보고하고 개체에 대한 작업을 수행하는 방법에 대해 설명합니다. 또한 노드에 대한 SMO 메서드 및 속성 목록을 가져오는 방법에 대해 설명합니다.|[SQL Server PowerShell 경로 작업](work-with-sql-server-powershell-paths.md)|  
|SMO URN(Uniform Resource Name)을 SQL Server 공급자 경로로 변환하는 방법에 대해 설명합니다.|[URN을 SQL Server 공급자 경로로 변환](../database-engine/convert-urns-to-sql-server-provider-paths.md)|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 공급자를 사용하여 SQL Server 인증 연결을 여는 방법에 대해 설명합니다. 기본적으로 공급자는 Windows PowerShell 세션을 실행하는 Windows 계정의 자격 증명을 사용하여 만든 Windows 인증 연결을 사용합니다.|[데이터베이스 엔진 PowerShell에서 인증 관리](manage-authentication-in-database-engine-powershell.md)|  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
