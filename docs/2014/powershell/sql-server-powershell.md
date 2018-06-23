---
title: SQL Server PowerShell | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 89b70725-bbe7-4ffe-a27d-2a40005a97e7
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: e66e94d1b49ecb275ba1422a6c7ee16c1eddc3f0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36187008"
---
# <a name="sql-server-powershell"></a>SQL Server PowerShell
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 는 관리자와 개발자가 서버 관리 및 응용 프로그램 배포를 자동화할 수 있는 강력한 스크립팅 셸인 Windows PowerShell을 지원합니다. Windows PowerShell 언어는 [!INCLUDE[tsql](../includes/tsql-md.md)] 스크립트보다 더 복잡한 논리를 지원하므로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 관리자가 강력한 관리 스크립트를 작성할 수 있습니다. 또한 Windows PowerShell 스크립트를 사용하여 다른 [!INCLUDE[msCoName](../includes/msconame-md.md)] 서버 제품을 관리할 수도 있습니다. 이는 관리자에게 서버 전체에 대한 공용 스크립팅 언어를 제공합니다.  
  
## <a name="sql-server-powershell-components"></a>SQL Server PowerShell 구성 요소  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 요소를 Windows PowerShell 2.0 환경 또는 스크립트로 가져오는 데 사용되는 `sqlps`라는 Windows PowerShell 모듈을 제공합니다. `sqlps` 모듈은 다음을 구현하는 두 개의 Windows PowerShell 스냅인을 로드합니다.  
  
-   파일 시스템 경로와 유사한 간단한 탐색 메커니즘을 제공하는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 공급자. 드라이브가 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 관리 개체 모델과 연결되고 노드가 개체 모델 클래스를 기반으로 하는 파일 시스템 경로와 비슷한 경로를 작성할 수 있습니다. 그런 다음 명령 프롬프트 창에서 폴더를 탐색하는 것과 비슷한 방법으로 **cd** 및 **dir** 과 같은 친숙한 명령을 사용하여 경로를 탐색할 수 있습니다. **ren** 또는 **del**과 같은 다른 명령을 사용하여 경로의 노드에 동작을 수행할 수 있습니다.  
  
-   Windows PowerShell 스크립트에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 동작을 지정하는 데 사용되는 명령인 cmdlet 집합. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] cmdlet은 **sqlcmd** 또는 XQuery 문이 포함된 [!INCLUDE[tsql](../includes/tsql-md.md)] 스크립트 실행과 같은 동작을 지원합니다.  
  
 Windows PowerShell에 대한 자세한 내용은 [Windows PowerShell 시작 가이드](http://msdn.microsoft.com/library/hh857337.aspx)를 참조하십시오.  
  
## <a name="sql-server-versions"></a>SQL Server 버전  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] PowerShell 구성 요소는 [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)] 이상의 인스턴스를 관리하는 데 사용할 수 있습니다. [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 인스턴스는 SP2 이상을 실행하고 [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)] 인스턴스는 SP4 이상을 실행하고 있어야 합니다. [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] PowerShell 구성 요소를 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]와 함께 사용할 경우에는 해당 버전에서 사용 가능한 기능만 사용할 수 있습니다.  
  
## <a name="sql-server-powershell-tasks"></a>SQL Server PowerShell 태스크  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|실행에 대 한 기본 메커니즘을 설명는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 세션 및 부하를 열려면 PowerShell 구성 요소는 `sqlps` 모듈입니다. `sqlps` 모듈은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 공급자 및 cmdlet와 공급자 및 cmdlet에 사용되는 SMO(SQL Server 관리 개체) 어셈블리에서 로드됩니다.|[SQLPS 모듈 가져오기](../database-engine/import-the-sqlps-module.md)|  
|공급자나 cmdlet 없이 SMO 어셈블리만 로드하는 방법을 설명합니다.|[Windows PowerShell에서 SMO 어셈블리 로드](load-the-smo-assemblies-in-windows-powershell.md)|  
|**개체 탐색기**에서 노드를 마우스 오른쪽 단추로 클릭하여 Windows PowerShell 세션을 실행하는 방법을 설명합니다. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] Windows PowerShell 세션을 시작, 로드는 `sqlps` 모듈, 선택한 개체에 SQL Server 공급자 경로 가져오거나 설정 합니다.|[SQL Server Management Studio에서 Windows PowerShell 실행](run-windows-powershell-from-sql-server-management-studio.md)|  
|Windows PowerShell 스크립트를 실행하는 SQL Server 에이전트 작업 단계를 만드는 방법을 설명합니다. 그런 다음 특정 시간에 또는 이벤트에 응답하여 실행하도록 작업을 예약할 수 있습니다.|[SQL Server 에이전트에서 Windows PowerShell 작업 단계 실행] (run-windows-powershell-steps-in-sql-server-agent.md
)|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 공급자를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 개체의 계층 구조를 탐색하는 방법을 설명합니다.|[SQL Server PowerShell 공급자](sql-server-powershell-provider.md)|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 스크립트 실행과 같은 [!INCLUDE[ssDE](../includes/ssde-md.md)] 동작을 지정하는 [!INCLUDE[tsql](../includes/tsql-md.md)] cmdlet을 사용하는 방법을 설명합니다.|[데이터베이스 엔진 cmdlet 사용](../database-engine/use-the-database-engine-cmdlets.md)|  
|Windows PowerShell에서 지원되지 않는 문자가 포함된 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구분 식별자를 지정하는 방법을 설명합니다.|[PowerShell의 SQL Server 식별자](sql-server-identifiers-in-powershell.md)|  
|SQL Server 인증 연결을 만드는 방법을 설명합니다. 기본적으로 SQL Server PowerShell 구성 요소는 Windows PowerShell을 실행하는 프로세스의 Windows 자격 증명을 사용하는 Windows 인증 연결을 사용합니다.|[데이터베이스 엔진 PowerShell에서 인증 관리](manage-authentication-in-database-engine-powershell.md)|  
|SQL Server PowerShell 공급자가 구현한 변수를 사용하여 Windows PowerShell 탭 완성 기능을 사용할 때 나열되는 개체 수를 제어하는 방법을 설명합니다. 이 기능은 많은 수의 개체가 포함된 데이터베이스에서 작업하는 경우에 특히 유용합니다.|[탭 완성 기능 관리&#40;SQL Server PowerShell&#41;](manage-tab-completion-sql-server-powershell.md)|  
|Windows PowerShell 환경에서 Get-Help를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 요소에 대한 정보를 가져오는 방법을 설명합니다.|[Get Help SQL Server PowerShell](../database-engine/get-help-sql-server-powershell.md)|  
  
  