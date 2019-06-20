---
title: SQL Server 2014 설치 빠른 시작 | Microsoft Docs
ms.custom: ''
ms.date: 05/25/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- quick start installation [SQL Server]
- installation [SQL Server]
- installing SQL Server, quick start installations
ms.assetid: 672afac9-364d-4946-ad5d-8a2d89cf8d81
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b06f5248152f8a11bf3e46d222df457f5442b6b4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62837789"
---
# <a name="quick-start-installation-of-sql-server-2014"></a>SQL Server 2014 빠른 시작 설치
    
## <a name="introduction"></a>소개  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설치 마법사는 Windows Installer를 기반으로 하며 다음 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 요소 설치에 대해 단일 기능 트리를 제공합니다.  
  
-   [!INCLUDE[ssDE](../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]  
  
-   [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]  
  
-   [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)]  
  
-   관리 도구  
  
-   연결 구성 요소  
  
 각 구성 요소를 개별적으로 설치하거나 위에 나열된 구성 요소 조합을 선택할 수 있습니다. 사용할 수 있는 버전과 구성 요소 중에서 최상의 수 있도록 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]를 참조 하세요 [버전 및 SQL Server 2014 구성 요소](../sql-server/editions-and-components-of-sql-server-2016.md)합니다.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 32비트 및 64비트 버전으로 제공됩니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설치 프로그램은 다음 설치 옵션을 지원합니다.  
  
-   **설치 마법사**  
  
     참조 [설치 마법사에서 SQL Server 2014 설치 &#40;설치&#41; ](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md) 설치 하는 방법에 대 한 절차 정보 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설치 마법사를 사용 하 여 합니다.  
  
-   **명령 프롬프트**  
  
     참조 [명령 프롬프트에서 SQL Server 2014 설치](../database-engine/install-windows/install-sql-server-from-the-command-prompt.md) 무인된 설치를 실행 하기 위한 예제 구문 및 설치 매개 변수에 대 한 합니다.  
  
-   **구성 파일**  
  
     참조 [SQL Server 2014 사용 하 여 설치 구성 파일을](../database-engine/install-windows/install-sql-server-using-a-configuration-file.md) 샘플 구문 및 설치 매개 변수에 대 한 구성 파일을 통해 설치 프로그램을 실행 합니다.  
  
-   **SysPrep**  
  
     참조 [SysPrep을 사용 하 여 SQL Server 2014 설치](../database-engine/install-windows/install-sql-server-using-sysprep.md) 설치 하는 방법에 대 한 절차 정보 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] SysPrep를 사용 하 여 합니다.  
  
-   **Server Core 설치**  
  
     참조 [Server Core에 SQL Server 2014 설치](../database-engine/install-windows/install-sql-server-on-server-core.md) 설치 하는 방법에 대 한 절차 정보 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Windows Server Core에 있습니다.  
  
-   **[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] BI 기능 설치**  
  
     참조 [SQL Server 2014 BI 기능 설치](../sql-server/install/install-sql-server-business-intelligence-features.md) 포함 하는 Microsoft BI 플랫폼의 일부인 기능을 설치 하는 방법에 대 한 내용은 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], 및 여러 클라이언트 응용 프로그램 분석 데이터를 사용 하 여 만들거나 사용 합니다.  
  
-   **장애 조치 클러스터 설치**  
  
     참조 [SQL Server 장애 조치 클러스터 설치](../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md) 설치 하는 방법에 대 한 절차 정보 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 장애 조치 클러스터입니다.  
  
 기본적으로 예제 데이터베이스와 예제 코드는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설치의 일부로 설치되지 않습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express Edition 이외의 버전을 위한 샘플 데이터베이스 및 샘플 코드를 설치하려면 [CodePlex 웹 사이트](https://go.microsoft.com/fwlink/?LinkId=87843)를 참조하세요. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 예제 데이터베이스 및 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]예제 코드에 대한 지원 정보를 확인하려면 [데이터베이스 및 예제 개요](https://go.microsoft.com/fwlink/?LinkId=110391)를 참조하십시오.  
  
## <a name="includessnoversionincludesssnoversion-mdmd-installation"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설치  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설치 마법사와 명령 프롬프트 중 어느 쪽을 사용하든 관계없이 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설치에는 다음 단계가 하나 이상 포함됩니다.  
  
-   설치 요구 사항, 시스템 구성 검사 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설치를 위한 보안 고려 사항을 검토합니다.  자세한 내용은 [Planning a SQL Server Installation](quick-start-installation-of-sql-server-2014.md#BKMK_BeforeYouInstall)을(를) 참조하세요.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설치 프로그램을 실행하여 기존 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]로 업그레이드할 수 있습니다. 자세한 내용은 [SQL Server 2014로 업그레이드](#BKMK_Upgrading)합니다.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설치 프로그램을 실행하여 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]의 새 인스턴스를 설치할 수 있습니다. 자세한 내용은 [SQL Server 2014 설치](#BKMK_Install)합니다.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설치 완료 후 다음 주요 단계는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 및 해당 구성 요소를 구성하는 것입니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 유틸리티를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 구성합니다. 자세한 내용은 [SQL Server 2014 구성](#BKMK_Configure)합니다.  
  
 다음 섹션에서는 이러한 태스크에 대한 자세한 설명을 찾을 수 있습니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
###  <a name="BKMK_BeforeYouInstall"></a> 계획을 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설치  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]를 설치하기 전에 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 설치하고 실행하기 위한 하드웨어 및 소프트웨어 설치 요구 사항, 네트워크 및 인터넷 고려 사항 및 보안 고려 사항을 검토합니다. 자세한 내용은 [SQL Server 설치 계획](../../2014/sql-server/install/planning-a-sql-server-installation.md) 및 다음 항목:  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|하드웨어 및 소프트웨어 요구 사항, 운영 체제 지원, 네트워크 및 인터넷 고려 사항, 하드 디스크 공간 요구 사항을 검토합니다.|[설치 필수 구성 요소](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설치를 위한 보안 고려 사항을 검토합니다.|[보안 고려 사항](../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)|  
|다른 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 버전에서 지원되는 기능의 세부 정보를 검토합니다.|[기능 및 버전](features-supported-by-the-editions-of-sql-server-2014.md)|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 사용할 수 있는 여러 버전과 구성 요소 중에서 가장 적합한 항목을 결정합니다.|[SQL Server 2014 버전 및 구성 요소](../sql-server/editions-and-components-of-sql-server-2016.md)|  
|하드웨어 구성을 검토하고 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 설치를 준비하는 방법을 알아 봅니다.|[장애 조치(Failover) 클러스터링을 설치하기 전에](../sql-server/failover-clusters/install/before-installing-failover-clustering.md)|  
  
###  <a name="BKMK_Upgrading"></a> 로 업그레이드 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 기존 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 또는 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 인스턴스를 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]로 업그레이드할 수 있습니다. 자세한 내용은 [SQL Server 2014로 업그레이드](../database-engine/install-windows/upgrade-sql-server.md)합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설치 프로그램을 실행하여 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]로 업그레이드하기 전에 업그레이드 프로세스에 대한 다음 항목을 검토하십시오.  
  
|Description|항목|  
|-----------------|-----------|  
|지원되는 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]로의 업그레이드 경로에 대해 설명합니다.|[지원 되는 업그레이드](../database-engine/install-windows/supported-version-and-edition-upgrades.md)|  
|[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 및 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 인스턴스를 분석하여 알려진 업그레이드 문제를 식별하는 도구인 업그레이드 관리자에 대해 설명합니다.|[업그레이드 관리자를 사용하여 업그레이드 준비](../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)|  
|여러 컴퓨터를 사용해 추적 데이터를 재생하여 중요한 작업을 효율적으로 시뮬레이션할 수 있는 도구인 Distributed Replay Utility에 대해 설명합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 업그레이드 이전 및 이후에 테스트 서버에서 재생을 수행하면 성능 차이를 측정하고 업그레이드와의 응용 프로그램 비호환성을 확인할 수 있습니다.|[Distributed Replay Utility를 사용하여 업그레이드 준비](../../2014/sql-server/install/use-the-distributed-replay-utility-to-prepare-for-upgrades.md)|  
|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]로 업그레이드한 후 응용 프로그램에 영향을 줄 수 있는 중요한 변경 내용을 보여 줍니다.|[이전 버전과의 호환성](backward-compatibility.md)|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 독립 실행형 인스턴스를 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]로 업그레이드하는 절차 항목입니다.|[업그레이드 하려면 SQL Server 2014 설치 마법사를 사용 하 여 &#40;설치&#41;](../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)|  
|특정 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 버전을 다른 버전으로 업그레이드하는 절차 항목입니다. 지원되는 버전 업그레이드 경로에 대한 자세한 내용은 [지원되는 버전 및 에디션 업그레이드](../database-engine/install-windows/supported-version-and-edition-upgrades.md)를 참조하세요.|[다른 버전의 SQL Server 2014로 업그레이드 &#40;설치&#41;](../database-engine/install-windows/upgrade-to-a-different-edition-of-sql-server-setup.md)|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 모든 장애 조치(failover) 클러스터 노드에서 [!INCLUDE[ssDE](../includes/ssde-md.md)] 및 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]를 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 또는 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]에서 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 장애 조치(failover) 클러스터로 개별 업그레이드하도록 지원합니다. 자세한 내용은 이 항목을 검토하십시오.|[SQL Server 장애 조치(Failover) 클러스터 업그레이드](../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md)|  
  
###  <a name="BKMK_Install"></a> 설치 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]의 다양한 설치 시나리오에 대한 정보는 다음 항목을 검토하십시오.  
  
|Description|항목|  
|-----------------|-----------|  
|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]의 다양한 구성 요소 설치에 대한 항목 및 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 설치에 대한 절차 항목 링크를 제공합니다.|[SQL Server 2014 설치](../database-engine/install-windows/install-sql-server.md)|  
|Windows Server Core에 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 를 설치하려면 이 항목을 검토합니다.|[Server Core에 SQL Server 2014 설치](../database-engine/install-windows/install-sql-server-on-server-core.md)|  
|기존 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 인스턴스에 개별 기능을 추가하려면 이 항목을 검토하십시오|[SQL server 2014 인스턴스에 기능 추가 &#40;설치&#41;](../database-engine/install-windows/add-features-to-an-instance-of-sql-server-setup.md)|  
|새 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 인스턴스를 만들려면 이 항목을 검토하십시오.|[새 SQL Server 장애 조치(failover) 클러스터 만들기&#40;설치 프로그램&#41;](../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)|  
|이 항목에서는 기존 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 인스턴스에서 노드를 관리합니다.|[SQL Server 장애 조치(Failover) 클러스터에서 노드 추가 또는 제거&#40;설치&#41;](../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)|  
|이 항목에서는 장애 조치(Failover) 클러스터에 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 클라이언트 도구를 설치합니다.|[SQL Server 장애 조치 클러스터에 클라이언트 도구 설치](../sql-server/failover-clusters/install/install-client-tools-on-a-sql-server-failover-cluster.md)|  
|SQL 검색 보고서 사용 방법을 검토하여 컴퓨터에 설치된 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 버전 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 기능을 확인합니다.|[SQL Server 설치 유효성 검사](../database-engine/install-windows/validate-a-sql-server-installation.md)|  
|설치 마법사, 명령 프롬프트, 구성 파일 사용 및 SysPrep 사용 등의 방법으로 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]를 설치하는 절차 항목에 대한 링크를 제공합니다.|[설치 방법 도움말 항목](../../2014/sql-server/install/installation-how-to-topics.md)|  
  
## <a name="related-content"></a>관련 내용  
 이 섹션에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 및 제거에 대해 설명합니다.  
  
###  <a name="BKMK_Configure"></a> 구성 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설치를 완료하면 그래픽 및 명령 프롬프트 유틸리티를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 추가로 구성할 수 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 처음 구성할 때는 다음 항목을 참조하십시오.  
  
|Description|항목|  
|-----------------|-----------|  
|이 항목에 있는 정보를 사용하여 방화벽의 포트 차단을 해제하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 또는 SharePoint용 PowerPivot에 대한 액세스를 허용하도록 결정할 수 있습니다. 이 항목에서 제공하는 단계를 수행하여 포트와 방화벽 설정을 모두 구성할 수 있습니다.|[Analysis Services 액세스를 허용하도록 Windows 방화벽 구성](../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|  
|이 항목에서는 방화벽 구성의 개요를 제공하고 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 관리자에게 유용한 정보를 요약하여 설명합니다.|[Configure the Windows Firewall to Allow SQL Server Access](../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|  
|이 항목에서는 다중 홈 환경에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 네트워크 연결을 제공하기 위해 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 와 고급 보안이 포함된 Windows 방화벽을 구성하는 방법에 대해 설명합니다.|[SQL Server 액세스를 허용하도록 다중 홈 컴퓨터 구성](../../2014/sql-server/install/configure-a-multi-homed-computer-for-sql-server-access.md)|  
  
###  <a name="BKMK_Uninstalling"></a> 제거 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 다음 항목에서는 독립 실행형 및 장애 조치(failover) 클러스터형 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스를 수동으로 제거하는 방법에 대해 설명합니다.  
  
|Description|항목|  
|-----------------|-----------|  
|이 항목에서는 독립 실행형 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스를 수동으로 제거하는 방법에 대해 설명합니다.|[SQL Server 2014 제거](../sql-server/install/uninstall-sql-server.md)|  
|이 항목에서는 장애 조치(failover) 클러스터 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스를 제거하는 방법에 대해 설명합니다.|[SQL Server 장애 조치(Failover) 클러스터 인스턴스 제거&#40;설치&#41;](../sql-server/failover-clusters/install/remove-a-sql-server-failover-cluster-instance-setup.md)|  
|이 항목에서는 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)]를 제거한 후 DQS([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]) 개체를 수동으로 제거하거나 DQS 서버만 제거하는 방법에 대해 자세히 설명합니다.|[Data Quality 서버 개체 제거](../../2014/sql-server/install/remove-data-quality-server-objects.md)|  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 2014 제품 사양](sql-server-2014-product-specifications.md)   
 [SQL Server 제품 설명서를 사용 하 여 시작](../2014-toc/books-online-for-sql-server-2014.md) [이전 버전과 호환성](backward-compatibility.md)  
  
  
