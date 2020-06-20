---
title: 기능 선택 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- feature selection, Setup
helpviewer_keywords:
- SQL Server Installation Wizard, Components to Install page
- Components to Install page [SQL Server Installation Wizard]
ms.assetid: 73182088-153b-4634-a060-d14d1fd23b70
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: ec5bf4706f349a4e0aabb254b4ac74f9d396128d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065403"
---
# <a name="feature-selection"></a>기능 선택
  **** 설치 마법사의 기능 선택 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 페이지에 있는 확인란을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치의 구성 요소를 선택할 수 있습니다.  
  
## <a name="installing-ssnoversion-features"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능 설치  
 **기능 선택** 페이지에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능은 **기능 인스턴스** 와 **공유 기능**이라는 2개의 주 섹션으로 나뉩니다.  
  
 **인스턴스 기능** 은 구성 요소의 복사본을 여러 개(인스턴스마다 하나씩) 갖도록 각 인스턴스에 대해 한 번씩 설치되는 구성 요소입니다. 각 인스턴스는 패치 수준이 다른 별개의 버전일 수 있습니다. 패치를 설치할 때 서비스 팩인지, 핫픽스인지 아니면 누적 업데이트인지에 관계없이 지정된 컴퓨터의 한 인스턴스에 대해서만 파일이 업데이트됩니다. 이미 업데이트되지 않은 공유 기능도 업데이트됩니다.  
  
 **공유 기능** 은 지정된 컴퓨터의 모든 인스턴에서 공통된 기능입니다. 이러한 각 공유 기능은 나란히 설치 가능한 지원되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전(서비스 팩, 누적 업데이트 및 핫픽스)과 호환됩니다.  
  
> [!NOTE]  
>  ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치 (Failover) 클러스터:** [!INCLUDE[ssDE](../../includes/ssde-md.md)] 및 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 구성 요소는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 장애 조치 (failover) 클러스터링을 지 원하는 유일한 기능입니다. 장애 조치(failover) 클러스터 노드에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 또는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]와 같은 다른 구성 요소를 설치할 수 있지만 이러한 구성 요소는 클러스터에서 인식되지 않으며 장애 조치(failover) 클러스터 노드가 오프라인 상태가 되어도 해당 서비스는 장애 조치(failover)되지 않습니다. 자세한 내용은 [AlwaysOn 장애 조치(failover) 클러스터 인스턴스&#40;SQL Server&#41;](../failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)를 참조하세요.  
  
### <a name="instance-features"></a>인스턴스 기능  
 각 구성 요소 그룹을 선택하면 해당 설명이 **설명** 창에 나타납니다. 확인란을 자유롭게 조합하여 선택할 수 있습니다. 작업을 계속하려면 항목을 선택해야 합니다.  
  
|기능|Description|  
|--------------|-----------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 서비스|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 데이터 저장, 처리 및 보안 유지를 위한 핵심 서비스인, 복제 기능, 전체 텍스트 검색 기능 및 관계형 데이터와 XML 데이터 관리 도구 및 [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] DQS () 서버가 포함 되어 있습니다. 다음은 데이터베이스 엔진의 기능입니다.<br /><br /> [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 데이터 저장, 처리 및 보안 유지를 위한 핵심 서비스입니다.<br /><br /> 복제: 선택 사항: 복제는 한 데이터베이스에서 다른 데이터베이스로 데이터와 데이터베이스 개체를 복사 및 배포한 후 데이터베이스 간에 동기화를 수행하여 일관성을 유지하는 일련의 기술입니다.<br /><br /> 전체 텍스트 검색: 선택 사항: 전체 텍스트 검색은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블의 일반 문자 기반 데이터에 대해 전체 텍스트 쿼리를 실행하는 기능을 제공합니다.<br /><br /> [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]: 선택 사항: [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS)는 데이터 원본에서 일관성 없고 올바르지 않은 데이터를 검색 하는 데 사용할 수 있는 데이터 정리 솔루션으로, 컴퓨터 기반 및 대화형 방법을 제공 하 여 데이터를 정리 합니다. DQS 서버를 설치하려면 이 확인란을 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치가 완료된 후 DQSInstaller.exe 파일을 실행하여 DQS 서버 설치를 *완료* 해야 합니다. SQL server의 기본 인스턴스를 설치한 경우이 파일은 C:\Program files \MSSQL12.에서 사용할 수 있습니다. \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] MSSQLSERVER\MSSQL\Binn.<br /><br /> <br /><br /> ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치 (Failover) 클러스터:** 복제 및 전체 텍스트 검색 구성 요소가 필요 하며, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 엔진 서비스를 선택 하면 장애 조치 (failover) 클러스터링 설치를 위해 설치 프로그램에서 자동으로 선택 됩니다.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에는 OLAP(온라인 분석 처리) 및 데이터 마이닝 애플리케이션을 생성하고 관리하기 위한 도구가 포함되어 있습니다.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-네이티브|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 네이티브 모드에는 테이블 형식, 행렬, 그래픽 및 자유 형식 보고서를 생성, 관리 및 배포하기 위한 서버/클라이언트 구성 요소가 포함되어 있습니다. 또한[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 보고서 애플리케이션을 개발하는 데 사용할 수 있는 확장 가능 플랫폼입니다.|  
  
> [!IMPORTANT]
>  1.  설치 프로그램은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 스케일 아웃 배포 시 여러 노드에 대해 로드 균형 조정이나 단일 URL 주소 지정을 구성하지 않습니다. 스케일 아웃 배포를 완료하려면 Windows Server, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Application Center 또는 타사 클러스터 관리 소프트웨어를 사용해야 합니다. 웹 팜 배포를 설정 하는 방법에 대 한 자세한 내용은 [스케일 아웃 배포에 대 한 Reporting Services 구성](https://go.microsoft.com/fwlink/?LinkId=199448) ()을 참조 하세요 https://go.microsoft.com/fwlink/?LinkId=199448) .  
> 2.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 요소의 브라우저 요구 사항은 [Reporting Services 및 파워 뷰 브라우저 지원 계획&#40;Reporting Services 2014&#41;](../../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md)을 참조하세요.  
> 3.  64비트 플랫폼 및 64비트 서버의 32비트 하위 시스템(WOW64)에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 함께 작동하도록 구성할 수 없습니다.  
  
### <a name="shared-features"></a>공유 기능  
 단일 컴퓨터에 있는 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 공유하는 기능은 단일 디렉터리에 설치됩니다. 이름은 다음과 같습니다.  
  
|기능|Description|  
|-------------|-----------------|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] - SharePoint|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]SharePoint 모드는 전자 메일, 여러 파일 형식 및 대화형 웹 기반 대형에 대 한 보고서를 만들고 관리 하 고 제공 하는 서버 기반 응용 프로그램입니다. SharePoint 모드에서는 보고서 보기 및 보고서 관리 환경을 SharePoint 제품과 통합합니다. 자세한 내용은 [Reporting Services 보고서 서버&#40;SharePoint 모드&#41;](../../../2014/reporting-services/reporting-services-report-server-sharepoint-mode.md)를 참조하세요.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능(SharePoint 제품용)|SharePoint 제품용 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능에는 SharePoint 모드에서 SharePoint 제품을 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버와 통합하는 관리 및 사용자 인터페이스 구성 요소가 포함되어 있습니다. 자세한 내용은 [SharePoint 제품용 Reporting Services 추가 기능을 찾을 수 있는 위치](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)를 참조 하세요.|  
|Data Quality 클라이언트|Data Quality 클라이언트는 DQS 서버에 연결하는 독립 실행형 애플리케이션으로, 데이터 정리 및 데이터 일치 작업을 수행하고 DQS에서 관리 태스크를 수행하기 위한 직관적인 그래픽 사용자 인터페이스를 제공합니다.|  
|클라이언트 도구 연결|클라이언트 도구에는 DB-Library, OLAP용 OLEDB, ODBC, ADODB 및 ADOMD+용 네트워크 라이브러리를 비롯한 클라이언트와 서버 간 통신용 구성 요소가 포함됩니다.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 데이터 이동, 복사 및 변환을 위한 그래픽 도구 및 프로그래밍 가능 개체 집합입니다.|  
|클라이언트 도구 이전 버전과의 호환성|클라이언트 도구 이전 버전과의 호환성에는 다음과 같은 구성 요소가 포함됩니다.<br /><br /> SQL-DMO(SQL Distributed Management Objects). 자세한 내용은 [SQL Server 2014에서 지원되지 않는 SQL Server 기능](../../../2014/getting-started/discontinued-sql-server-features-in-sql-server-2014.md)을 참조하세요.<br /><br /> DSO(의사 결정 지원 개체). 자세한 내용은 [SQL Server 2014에서 Analysis Services 기능의 주요 변경](../../../2014/analysis-services/breaking-changes-to-analysis-services-features-in-sql-server-2014.md)을 참조하세요.|  
|클라이언트 도구 SDK|프로그래머용 리소스가 들어 있는 소프트웨어 개발 키트를 포함합니다.|  
|설명서 구성 요소|설명서 구성 요소는 도움말 내용을 보고 관리하는 데 사용할 수 있는 구성 요소를 포함합니다.|  
|관리 도구 -  기본|**관리 도구-기본:** 여기에는 다음이 포함 됩니다.<br /><br /> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)][!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] , **sqlcmd** 유틸리티 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 공급자에 대 한 지원<br /><br /> **관리 도구-전체:** 여기에는 기본 버전의 구성 요소 외에도 다음과 같은 구성 요소가 포함 됩니다.<br /><br /> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 및 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 대한 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 지원<br /><br /> [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]<br /><br /> Database Engine Tuning Advisor<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]유틸리티 관리|  
|Distributed  Replay  Controller|Distributed Replay Controller는 Distributed Replay Client의 동작을 조정합니다. 각 Distributed Replay 환경에는 컨트롤러 인스턴스가 하나만 있을 수 있습니다. 자세한 내용은 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)을 참조하세요.|  
|Distributed  Replay  Client|여러 Distributed Replay Client가 함께 작동하여 SQL Server 인스턴스에 대해 작업을 시뮬레이션합니다. 각 Distributed Replay 환경에 하나 이상의 클라이언트가 있을 수 있습니다. 자세한 내용은 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)을 참조하세요.|  
|SQL  클라이언트 연결 SDK|데이터베이스 애플리케이션 개발을 위한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client(ODBC/OLE DB) SDK를 포함합니다.|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]는 정확도 향상과 감사를 위해 조직 전체에 분산된 개별 시스템의 데이터를 하나의 마스터 데이터 원본으로 통합하는 플랫폼입니다. [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 옵션은 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)], 어셈블리, Windows PowerShell 스냅인, 웹 애플리케이션과 서비스의 폴더 및 파일을 설치합니다.|  
  
 기본적으로 공유 구성 요소는 %Program Files%Microsoft SQL Server\\에 설치됩니다. 설치 경로를 변경하려면 **찾아보기** 단추를 클릭하십시오. 한 공유 구성 요소의 설치 경로를 변경하면 다른 공유 구성 요소의 설치 경로도 변경됩니다. 후속 설치의 경우 원본 설치와 동일한 위치에 공유 구성 요소가 설치됩니다.  
  
 **인스턴스 루트 디렉터리** -기본적으로 인스턴스 루트 디렉터리는 C:\Program files입니다 \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \\ . 기본 루트 디렉터리가 아닌 디렉터리를 지정하려면 **찾아보기** 단추를 클릭하거나 경로 이름을 제공합니다.  
  
 x64 기반 운영 체제에서는 64비트 구성 요소가 설치될 위치와 32비트 구성 요소가 WOW64 하위 시스템에 설치될 위치를 지정할 수 있습니다.  
  
## <a name="disk-space-requirements"></a>디스크 공간 요구 사항  
 디스크 공간 요약 페이지를 사용하여 설치하도록 선택한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능에 필요한 디스크 공간을 계산할 수 있습니다.  
  
### <a name="options"></a>옵션  
 필요한 디스크 공간이 너무 많은 경우 다음 옵션을 고려하십시오.  
  
-   설치 디렉터리를 디스크 공간이 더 많은 드라이브로 변경합니다.  
  
-   설치할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능을 변경합니다.  
  
-   다른 파일 또는 애플리케이션을 이동하여 지정된 드라이브의 빈 공간을 늘립니다.  
  
## <a name="installing-adventureworks-sample-databases"></a>AdventureWorks 예제 데이터베이스 설치  
 기본적으로 예제 데이터베이스와 예제 코드는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치의 일부로 설치되지 않습니다. 예제 데이터베이스 및 예제 코드를 설치 하는 방법에 대 한 자세한 내용은 [Microsoft SQL Server 커뮤니티 프로젝트 & 샘플](https://go.microsoft.com/fwlink/?LinkId=87843) ()을 참조 하세요 https://go.microsoft.com/fwlink/?LinkId=87843) .  
  
 예제에 대한 추가 정보는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]을 설치한 후에 확인할 수 있습니다. **시작** 메뉴에서 **모든 프로그램**, **[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** , **설명서 및 자습서**를 차례로 클릭 한 다음 ** [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 샘플 개요**를 클릭 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 2014 버전 및 구성 요소](../editions-and-components-of-sql-server-2016.md)  
  
  
