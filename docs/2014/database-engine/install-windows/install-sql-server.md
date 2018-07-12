---
title: SQL Server 2014 설치 | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- installing SQL Server, preparing to install
- installation [SQL Server]
ms.assetid: 0300e777-d56b-4d10-9c33-c9ebd2489ee5
caps.latest.revision: 40
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7f03f01be41395cea94acdc40acd582a6fb78772
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37157014"
---
# <a name="install-sql-server-2014"></a>SQL Server 2014 설치
## <a name="-download-sql-server-2014-express-httpwwwhanselmancomblogdownloadsqlserverexpressaspx"></a>[ SQL Server 2014 Express 다운로드 ](http://www.hanselman.com/blog/DownloadSQLServerExpress.aspx)
  **준 [Scott hanselman이](http://www.hanselman.com/) 한곳에서 설치 관리자 패키지 링크를 모두 수집 하기 위한!**
  
 이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치를 위해 필요한 여러 설치 옵션에 대한 개요를 제공합니다. 다양 한에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치할 수 있는 구성 요소 및 설치 프로세스를 참조 하세요 [SQL Server 2014 설치](installation-for-sql-server.md)합니다.  
> **참고:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 32 비트 및 64 비트 버전에서 사용할 수 있습니다. 64비트 및 32비트 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 설치 마법사나 명령 프롬프트를 통해 설치됩니다. 에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소를 참조 하세요 [버전 및 SQL Server 2014 구성 요소](../../sql-server/editions-and-components-of-sql-server-2016.md) 하 고 [SQL Server 2014 버전에서 지 원하는 기능](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)합니다.  
  
 기본적으로 예제 데이터베이스와 예제 코드는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치의 일부로 설치되지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express Edition 이외의 버전을 위한 샘플 데이터베이스 및 샘플 코드를 설치하려면 [CodePlex 웹 사이트](http://go.microsoft.com/fwlink/?LinkId=87843)를 참조하세요. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 예제 데이터베이스 및 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]예제 코드에 대한 지원 정보를 확인하려면 [데이터베이스 및 예제 개요](http://go.microsoft.com/fwlink/?LinkId=110391)를 참조하십시오.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하기 전에 설치 요구 사항, 시스템 구성 검사 및 보안 고려 사항을 검토합니다. 자세한 내용은 [Planning a SQL Server Installation](../../sql-server/install/planning-a-sql-server-installation.md)을(를) 참조하세요. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 여러 설치 시나리오에 대한 정보는 다음 섹션의 항목을 참조하십시오.  
  
  
## <a name="install-includesscurrentincludessscurrent-mdmd-components"></a>설치 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 구성 요소  
  
|항목|Description|  
|-----------|-----------------|  
|[SQL Server 데이터베이스 엔진 정보](../sql-server-database-engine-overview.md)|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]을 설치 및 구성하는 방법에 대해 설명합니다.|  
|[SQL Server 복제 설치](install-sql-server-replication.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제를 설치 및 구성하는 방법에 대해 설명합니다.|  
|[Distributed Replay 설치](../../tools/distributed-replay/install-distributed-replay-overview.md)|Distributed Replay 기능 설치와 관련된 항목들을 나열합니다.|  
|[SQL Server 관리 도구 설치](../../sql-server/install/install-sql-server-management-tools.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리 도구를 설치 및 구성하는 방법에 대해 설명합니다.|  
|[SQL Server PowerShell 설치](install-sql-server-powershell.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 구성 요소 설치에 대한 고려 사항을 설명합니다.|  
  
## <a name="how-to-install-includesscurrentincludessscurrent-mdmd"></a>설치 하는 방법 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
|Title|Description|  
|-----------|-----------------|  
|[설치 방법 도움말 항목](../../sql-server/install/installation-how-to-topics.md)|설치 마법사, 명령 프롬프트, 구성 파일 사용 및 SysPrep 사용 등의 방법으로 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]를 설치하는 절차 항목에 대한 링크를 제공합니다.|  
|[Server Core에 SQL Server 2014 설치](install-sql-server-on-server-core.md)|Windows Server Core에 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 설치하려면 이 항목을 검토합니다.|  
|[SQL Server 설치 유효성 검사](validate-a-sql-server-installation.md)|SQL 검색 보고서 사용 방법을 검토하여 컴퓨터에 설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 버전 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능을 확인합니다.|  
|[시스템 구성 검사기의 검사 매개 변수](check-parameters-for-the-system-configuration-checker.md)|SCC(시스템 구성 검사기)의 기능에 대해 설명합니다.|  
  
## <a name="configuration"></a>Configuration  
  
|항목|Description|  
|-----------|-----------------|  
|[SQL Server 액세스를 허용하도록 Windows 방화벽 구성](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|이 항목에서는 방화벽 구성 및 Windows 방화벽 구성 방법에 대한 개요를 제공합니다.|  
|[SQL Server 액세스를 허용하도록 다중 홈 컴퓨터 구성](../../sql-server/install/configure-a-multi-homed-computer-for-sql-server-access.md)|이 항목에서는 다중 홈 환경에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 네트워크 연결을 제공하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 고급 보안이 포함된 Windows 방화벽을 구성하는 방법에 대해 설명합니다.|  
|[Analysis Services 액세스를 허용하도록 Windows 방화벽 구성](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|이 항목에서 제공하는 단계를 따라 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 또는 SharePoint용 PowerPivot에 액세스할 수 있도록 포트 및 방화벽 설정 모두를 구성할 수 있습니다.|  
  
## <a name="related-sections"></a>관련 섹션  
 [SQL Server 2014 BI 기능 설치](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] BI 플랫폼에 속하는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 기능에는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] 및 분석 데이터를 만들거나 사용하는 데 사용되는 일부 클라이언트 응용 프로그램이 포함됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 설명서 중 이 섹션에서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치 방법에 대해 설명합니다.  
  
 [SQL Server 장애 조치(Failover) 클러스터 설치](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 설명서 중 이 섹션에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터를 설치 및 구성하는 방법에 대해 설명합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 설치 계획](../../sql-server/install/planning-a-sql-server-installation.md)   
 [SQL Server 2014로 업그레이드](upgrade-sql-server.md)   
 [SQL Server 2014 제거](../../sql-server/install/uninstall-sql-server.md)   
 [고가용성 솔루션&#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)  
  
  
