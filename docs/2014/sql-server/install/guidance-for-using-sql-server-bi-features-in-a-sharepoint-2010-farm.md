---
title: SharePoint 2010 팜에서 SQL Server BI 기능 사용에 대 한 지침 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 5f9a94c4-854b-4577-a8b1-7142f19904e3
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 08323d12fb787ea3989555070632d9716ad41152
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952265"
---
# <a name="guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm"></a>SharePoint 2010 팜에서 SQL Server BI 기능을 사용하기 위한 지침
  이 항목에서는 사용 중인 소프트웨어의 버전에 따라 사용 가능한 기능을 요약하여 보여 줍니다. 또한 특정 SQL Server 기능을 사용하는 데 필요한 SharePoint 2010 설치 요구 사항에 대해서도 설명합니다. SharePoint 2013 관련 정보는 [sharepoint의 SQL SERVER BI 기능에 대 한 배포 토폴로지](deployment-topologies-for-sql-server-bi-features-in-sharepoint.md)를 참조 하세요.  
  
 항목 내용  
  
-   [일반 SharePoint 2010 요구 사항](#bkmk_generalsharepoint)  
  
-   [SharePoint 2010 SP1 (서비스 팩 1)](#bkmk_sp1)  
  
-   [SharePoint 버전 및 BI 기능 지원](#bkmk_vers)  
  
-   [SharePoint 2010 제품 준비 도구](#bkmk_prereq)  
  
-   [SharePoint 설치를 실행 하기 위한 요구 사항 및 제안 사항](#bkmk_install)  
  
##  <a name="bkmk_generalsharepoint"></a>일반 SharePoint 2010 요구 사항  
  
-   SharePoint 2010 제품은 64비트 전용입니다. 이전 SharePoint 버전인 32비트 버전이 설치되어 있고 SharePoint 통합 모드로 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]가 설치된 경우 SharePoint 2010으로 업그레이드할 수 없습니다. 자세한 내용은 SharePoint 설명서를 검토하십시오.  
  
-   Reporting Services에는 SharePoint 제품용 추가 기능이 포함되어 있습니다. 해당 추가 기능 및 보고서 서버에 대해 지원되는 구성은 여기에 표시된 것보다 더 세분되어 있습니다. 자세한 내용은 [지원 되는 SharePoint 및 Reporting Services 서버 조합 및 &#40;SQL Server 2014&#41;의 추가 기능](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)을 참조 하세요.  
  
-   SharePoint 개발자 도구는 SharePoint 독립 실행형 구성만 지원합니다.  자세한 내용은 SharePoint 설명서: [Sharepoint 솔루션 개발을 위한 요구 사항](https://msdn.microsoft.com/library/ee231582.aspx)을 참조 하세요.  
  
##  <a name="bkmk_vers"></a>SharePoint 버전 및 BI 기능 지원  
 일부 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Business Intelligence 기능은 SharePoint 제품의 특정 버전에서만 지원됩니다.  
  
|지원되는 기능|SharePoint 제품|  
|------------------------|------------------------|  
|[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]는 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Enterprise Edition 용 추가 기능 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기능입니다.<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 경고<br /><br /> [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 을 참조하세요.|[!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Enterprise Edition|  
|일반 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 보기 및 SharePoint와 기능 통합|[!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Standard 및 Enterprise Editions<br /><br /> [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 을 참조하세요.|  
  
 자세한 내용은 [SQL Server 2012 버전에서 지 원하는 기능](https://go.microsoft.com/fwlink/?linkid=232473)을 참조 하세요.  
  
##  <a name="bkmk_sp1"></a>SharePoint 2010 SP1 (서비스 팩 1)  
 SharePoint 2010 설치를 SharePoint 2010 SP1(서비스 팩 1)로 업데이트하는 것이 좋습니다. SharePoint SP1은 다음과 같은 경우 필요합니다.  
  
-   SharePoint 콘텐츠 데이터베이스 또는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 카탈로그 데이터베이스용 데이터베이스 엔진의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 버전을 사용하려고 합니다.  
  
-   [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 및 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 구성 도구를 사용하려고 합니다.  
  
 S p 1을 실행 하는 SharePoint 설치에는 s p 1이 필요 합니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]는 이전 릴리스에서 더 이상 사용 되지 않는 데이터베이스 엔진 기능 **sp_dboption**[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 릴리스에서 더 이상 사용 되지 않습니다. 자세한 내용은 [SQL Server 2014에서](../../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md) 지원 되지 않는 데이터베이스 엔진 기능을 참조 하세요.  
  
### <a name="sharepoint-2010-sp1-installation-guidance"></a>SharePoint 2010 SP1 설치 지침  
 [SharePoint Server 2010](https://go.microsoft.com/fwlink/?LinkID=219697) s p 1을 다운로드 하 여 팜의 모든 서버에 적용 합니다.  
  
> [!NOTE]  
>  기존 팜에서는 SharePoint SP1 업그레이드를 완료 하려면 다음 **추가** 단계 중 하나를 사용 해야 합니다. 자세한 내용은 [Office 2010 sp1 및 sharepoint 2010](https://support.microsoft.com/kb/2532126) s p 1을 설치할 때의 알려진 문제 및 [sharepoint Server 2010](https://support.microsoft.com/kb/2460045)s p 1에 대 한 설명을 참조 하세요.  
  
-   **SharePoint 제품 구성 마법사:** 마법사를 실행 하 여 SP1 업그레이드 및 구성을 완료 합니다.  
  
-   **Psconfig.exe를 사용 하 여 업그레이드를 완료 합니다.** 명령 `psconfig -upgrade`를 실행 하 여 SP1 업그레이드를 완료 합니다.  
  
 자세한 내용은 [(Sharepoint Server 2010)](https://technet.microsoft.com/library/cc263093.aspx) 의 "업그레이드" 섹션 및 [리소스 센터: Sharepoint 2010 제품용 업데이트](https://technet.microsoft.com/sharepoint/ff800847.aspx) 를 참조 하세요.  
  
## <a name="sharepoint-installation-with-sql-server-bi-features"></a>SQL Server BI 기능을 사용한 SharePoint 설치  
  
###  <a name="bkmk_prereq"></a>SharePoint 2010 제품 준비 도구  
 SharePoint 제품 준비 도구는 운영 체제의 서버 역할을 사용하도록 설정하고 SharePoint 설치에 필요한 기타 필수 구성 요소 소프트웨어를 설치합니다. 다음 표에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]용으로 서버를 구성하는 추가 단계를 보여 줍니다.  
  
|구성 요소|작업|  
|---------------|------------|  
|Reporting Services 추가 기능|SharePoint 2010 제품 준비 도구는 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 버전의 Reporting Services 추가 기능을 설치합니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 기능에 필요한 최신 버전의 추가 기능이 포함됩니다. 추가 기능은 MSDN에서 다운로드하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사를 사용하여 설치할 수 있습니다. 최신 버전의 추가 기능과이를 설치 하는 방법에 대 한 자세한 내용은 [Sharepoint 제품용 Reporting Services 추가](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md) 기능을 찾을 수 있는 위치 및 sharepoint [ &#40;&#41;Sharepoint 2010 및 sharepoint 2013 용 Reporting Services 추가 기능 설치 또는 제거](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)를 참조 하십시오.|  
|Analysis Services OLE DB 공급자(MSOLAP)|SharePoint 2010은 Excel Services 배포의 일환으로 SQL Server 2008 버전의 OLE DB 공급자를 설치합니다. 이 버전은 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 액세스를 지원하지 않습니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 연결을 지원하는 SharePoint 서버에는 더 높은 버전의 공급자를 설치해야 합니다. 자세한 내용은 [SharePoint 서버에 Analysis Services OLE DB Provider 설치](../../../2014/sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md) 를 참조 하세요.|  
|ADO.NET Services|SharePoint 2010의 필수 구성 요소 목록에는 ADO.NET Services가 포함되지만 필수 구성 요소 설치 관리자 프로그램이 이 서비스를 설치하지는 않습니다. ADO.NET Services를 추가하려면 수동으로 설치해야 합니다. SharePoint 목록을 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서 또는 Reporting Services 보고서에 대한 데이터 피드로 사용하려면 ADO.NET Services를 설치해야 합니다. 지침은 [ADO.NET 설치 Data Services를 참조 하 여 SharePoint 목록의 데이터 피드 내보내기를 지원](../../../2014/sql-server/install/install-ado-net-data-services-to-support-data-feed-exports-of-sharepoint-lists.md)합니다.|  
  
###  <a name="bkmk_install"></a>SharePoint 설치를 실행 하기 위한 요구 사항 및 제안 사항  
 설치하는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 기능과 이 기능의 설치 순서에 따라 SharePoint와의 통합 수준이 결정됩니다. 예를 들어 기본 제공 데이터베이스를 사용하는 SharePoint 서버에서 Reporting Services를 통한 일정 수준의 기능 통합이 가능하기는 하지만, 일부 BI 기능에 필요한 인프라는 팜 설치를 통해서만 제공되기 때문에 대부분의 기능 통합 시나리오에서는 SharePoint 팜 설치가 필요합니다.  
  
 SharePoint 팜은 단일 서버일 수도 있고 다중 서버일 수도 있습니다. 팜은 Windows 토큰 서비스에 대한 클레임과 같은 추가 인프라가 존재한다는 점에서 독립 실행형 설치와 다릅니다.  
  
 팜은 SharePoint 설치 프로그램에서 **서버 팜** 옵션을 선택 하면 사용 하도록 설정 됩니다. SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 또는 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]를 사용하려면 팜 설치가 필요합니다. 독립 실행형 SharePoint 설치도 지원되며 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 개발 환경에서는 이 설치가 일반적입니다. 하지만 프로덕션 환경에서는 SharePoint 팜 설치가 권장됩니다.  
  
 ![GMNI_SetupUI_SharePoint2010InstallType](../../../2014/sql-server/install/media/gmni-setupui-sharepoint2010installtype.gif "GMNI_SetupUI_SharePoint2010InstallType")  
  
 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 또는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 공유 서비스에도 전체 서버 설치가 필요합니다.  
  
 ![GMNI_SetupUI_SharePoint2010ServerType](../../../2014/sql-server/install/media/gmni-setupui-sharepoint2010servertype.gif "GMNI_SetupUI_SharePoint2010ServerType")  
  
 설치 마법사의 마지막 페이지에서는 팜을 구성하고 선택적으로 기본 웹 애플리케이션 및 루트 사이트 모음을 구성할 수 있습니다. 대부분의 설치 사용자는 이 설치 경로를 따릅니다. 여기에서 팜을 구성하지 않는 경우 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 구성 도구의 팜 구성 옵션을 사용하여 팜을 구성할 수 있습니다.  
  
 이전 릴리스에서는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 설치의 경우 팜을 구성되지 않은 상태로 두도록 권장되었습니다. 그 이유는 SQL Server 설치 옵션을 사용하여 사용 준비가 완료된 상태로 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]를 설치하는 경우 필요한 단계가 줄어들기 때문입니다. 이번 릴리스에서는 더 이상 이러한 사항을 고려할 필요가 없습니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 구성 도구를 사용하여 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 설치에 권장되는 설정을 사용하도록 기존 팜을 조정할 수 있습니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 기존 SharePoint 팜에 설치할 수 있습니다. 임의의 순서로 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 또는 SharePoint를 설치할 수 있지만 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 구성은 순서에 따라 달라집니다. 자세한 내용은 [팜에 &#40;&#41; 추가 보고서 서버를 추가 하](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md) 고 [sharepoint 2010에 대 한 sharepoint 모드 Reporting Services 설치](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md) 를 참조 하세요.  
  
 ![GMNI_SetupUI_DoNotConfigureMOSS](../../../2014/sql-server/install/media/gmni-setupui-donotconfiguremoss.gif "GMNI_SetupUI_DoNotConfigureMOSS")  
  
## <a name="see-also"></a>관련 항목  
 [SharePoint Server 2010  설치 및 배포](https://technet.microsoft.com/sharepoint/ee518643.aspx)  
 [3 계층 팜을 위한 다중 서버 (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?linkID=219834)  
  
  
