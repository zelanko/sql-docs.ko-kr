---
title: SharePoint를 사용 하 여 SQL Server BI 기능 설치 (PowerPivot 및 Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3166107c-30c2-468e-bb1b-bb42b79b37c3
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 954f60e49f5bc94881fcdf66b7a381385fb40416
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68890140"
---
# <a name="install-sql-server-bi-features-with-sharepoint-powerpivot-and-reporting-services"></a>SharePoint와 함께 SQL Server BI 기능 설치(PowerPivot 및 Reporting Services)
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]는 Microsoft SharePoint 팜과 통합되어 SharePoint의 BI(비즈니스 인텔리전스) 기능을 사용할 수 있습니다. 해당하는 기능은 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]입니다. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]는 SharePoint 팜의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 액세스에 사용 됩니다. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]은 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel에서 만들어지고 SharePoint 라이브러리에서 액세스되는 통합 문서를 위한 데이터 엔진입니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서를 SharePoint에 저장한 다음에는 이를 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 보고서에 대한 데이터 원본으로 사용할 수 있습니다.  
  
 SharePoint 2010에 필요한 설치 및 구성 단계 중 일부는 SharePoint 2013에 필요한 단계와 다릅니다. 이 단원의 항목 중 일부는 SharePoint의 두 버전에 모두에 적용됩니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 &#124; SharePoint 2010|  
  
 ![참고](../../../2014/reporting-services/media/rs-fyinote.png "참고") 현재 릴리스 정보는 [SQL server 2014 릴리스 정보](https://go.microsoft.com/fwlink/?LinkID=296445)를 참조 하세요.  
  
##  <a name="bkmk_top"></a> 항목 내용  
  
-   [SQL Server BI 시나리오 및 SharePoint 2013](#bkmk_bi_scenarios)  
  
-   [설치 개요](#bkmk_install_sharepoint2013_overview)  
  
## <a name="in-this-section"></a>섹션 내용  
 이 항목의 정보 외에 다음과 같은 관련 항목이 이 섹션에 포함되어 있습니다.  
  
 [SharePoint의 SQL Server BI 기능에 대한 배포 토폴로지](deployment-topologies-for-sql-server-bi-features-in-sharepoint.md)  
  
 [SharePoint 2010 팜에서 SQL Server BI 기능을 사용하기 위한 지침](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
 [SharePoint와 함께 BI 기능을 설치하기 위한 검사 목록](../../../2014/sql-server/install/checklists-for-installing-bi-features-with-sharepoint.md)  
  
 [Sharepoint 모드 설치 &#40;Reporting Services sharepoint 2010 및 sharepoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)  
  
 [SharePoint 2013용 PowerPivot 설치](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode)  
  
 [SharePoint 2010용 PowerPivot 설치](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
##  <a name="bkmk_bi_scenarios"></a>SQL Server BI 시나리오 및 SharePoint 2013  
 이 섹션에는 설치 및 구성할 때 선택할 수 있는 여러 수준의 BI 기능이 요약되어 있습니다.  
  
 SharePoint 2013의 Excel Services에는 브라우저에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서와 상호 작용할 수 있도록 데이터 모델 기능이 포함되어 있습니다. 기본 데이터 모델 기능의 경우 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 추가 기능을 팜에 배포할 필요가 없습니다. SharePoint 모드의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버를 설치하고 Excel Services **데이터 모델** 설정 내에 서버를 등록해야 합니다.  
  
 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 추가 기능을 배포하면 추가 기능 및 SharePoint 팜의 기능을 사용할 수 있습니다. 추가 기능에는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 갤러리, 데이터 새로 고침 예약 및 PowerPivot 관리 대시보드가 있습니다. 추가 정보는 테이블을 참조하세요.  
  
||Level|기능|설치 또는 구성|  
|-|-----------|--------------|--------------------------|  
|1|SharePoint 전용|기본 Excel Services 기능|SharePoint Server 2013에 포함된 Excel Services 및 기타 서비스입니다.|  
|**2**|SharePoint와 SharePoint 모드의 Analysis Services|브라우저의 대화형 PowerPivot 통합 문서|SharePoint 모드의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 를 설치합니다.<br /><br /> Excel Services에 Analysis Services 서버를 등록합니다.|  
|**3**|SharePoint와 SharePoint 모드의 Reporting Services|파워 뷰|SharePoint 모드의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 설치합니다.<br /><br /> SharePoint [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 용 추가 기능 **(rssharepoint.msi)** 을 설치 합니다. 자세한 내용은 [sharepoint &#40;SharePoint 2010 및&#41; sharepoint 2013 용 Reporting Services 추가 기능 설치 또는 제거](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md) 를 참조 하세요.|  
|**4**|모든 PowerPivot 기능|팜 외부로부터 통합 문서를 데이터 원본으로 액세스합니다.<br /><br /> 데이터 새로 고침을 예약합니다.<br /><br /> PowerPivot 갤러리입니다.<br /><br /> 관리 대시보드입니다.<br /><br /> BISM 링크 파일 콘텐츠 형식입니다.|SharePoint용 PowerPivot 2013 추가 기능 **(Sppowerpivot .msi)** 을 배포 합니다. 자세한 내용은 다음 항목을 참조하세요.<br /><br /> [SharePoint용 PowerPivot 추가 기능 &#40;SharePoint 2013 설치 또는 제거&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013)<br /><br /> **spPowerPivot.msi**를 다운로드하는 방법에 대한 자세한 내용은 [SQL Server 2014 SharePoint용 PowerPivot 다운로드](https://go.microsoft.com/fwlink/?LinkID=296473)를 참조하세요.|  
  
 기능을 사용 하도록 설정 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 하는 방법에 대 한 자세한 내용은 [SharePoint 2013에 대 한 SQL Server BI 롤업 스토리](https://blogs.msdn.com/b/analysisservices/archive/2012/07/27/introducing-the-bi-light-up-story-for-sharepoint-2013.aspx) ()https://blogs.msdn.com/b/analysisservices/archive/2012/07/27/introducing-the-bi-light-up-story-for-sharepoint-2013.aspx) 를 참조 하세요.  
  
##  <a name="bkmk_install_sharepoint2013_overview"></a>설치 개요  
 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 둘 다 사용하려는 경우 SQL Server 설치 마법사를 두 번 실행하세요. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]및 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 는 SQL Server 설치 마법사의 **설치 역할** 페이지에서 별도로 선택할 수 있습니다.  
  
 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]는 SharePoint 2010과 SharePoint 2013을 모두 지원하지만 SharePoint 버전에 따라 서로 다른 아키텍처 및 설치 프로세스를 사용합니다.  
  
 다음은 단일 서버에 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] BI 기능을 배포하는 설치 단계를 요약한 것입니다.  
  
 **[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013**  
  
 **SharePoint 2013**의 경우 SharePoint 제품이 설치되지 않은 서버에 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 을 설치할 수 있습니다. SharePoint 2013에 사용되는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 아키텍처는 SharePoint 팜 **외부** 에서 실행되며 SharePoint 설치가 포함된 서버 또는 SharePoint 설치가 포함되지 않은 서버에 설치될 수 있습니다.  
  
1.  SharePoint Server 2013을 설치하고 Excel Services를 설치합니다.  
  
2.  SharePoint 모드에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]를 설치하고 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 SharePoint 팜 및 서비스 계정에 서버 관리자 권한을 부여합니다.  
  
     SharePoint의 두 버전에 대해 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 설치 프로세스는 SQL Server 설치 마법사에서 **SharePoint용 SQL Server PowerPivot** 의 설정 역할을 선택하거나 SQL Server 명령 프롬프트 설치를 사용하여 시작됩니다.  
  
     ![설치 역할](../../../2014/sql-server/install/media/gmni-setupui-featurerole-sql2012sp1.gif "설치 역할")  
  
3.  SharePoint 2013의 경우 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 기능 및 환경을 확장할 수 있습니다. **spPowerPivot.msi** 를 다운로드 및 실행하여 서버 쪽 데이터 새로 고침 처리, 협업 및 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서에 대한 관리 지원을 추가합니다. 자세한 내용은 [Microsoft® SharePoint용 Microsoft SQL Server 2014 PowerPivot](https://go.microsoft.com/fwlink/?LinkID=324854)을 참조하세요.  
  
     SharePoint 팜의 각 서버에서 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 설치 패키지 **spPowerPivot.msi** 를 실행하여 올바른 버전의 데이터 공급자가 설치되어 있는지 확인합니다.  
  
4.  SharePoint 2013용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 을 구성하려면 **SharePoint 2013용 PowerPivot 구성** 도구를 사용합니다.  
  
     SQL Server 설치 마법사는 두 개의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 구성 도구를 설치합니다. 구성 도구 중 하나는 SharePoint 2013을 지원하고 다른 하나는 SharePoint 2010을 지원합니다.  
  
     ![두 개의 파워 피벗 구성 도구](https://docs.microsoft.com/analysis-services/analysis-services/media/as-powerpivot-configtools-bothicons.gif "두 개의 파워 피벗 구성 도구")  
  
5.  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스를 사용하도록 SharePoint Server 2013의 Excel Services를 구성합니다. 자세한 내용은 [SharePoint용 PowerPivot 2013 설치](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode)에서 "기본 Analysis Services SharePoint 통합 구성" 섹션을 참조 하 고 [Excel Services 데이터 모델 설정 관리 (SharePoint Server 2013)](https://technet.microsoft.com/library/jj219780.aspx) (https://technet.microsoft.com/library/jj219780.aspx) )를 참조 하십시오.  
  
6.  자세한 내용은 [PowerPivot for SharePoint 2013 Installation](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode)을 참조하세요.  
  
 **[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010**  
  
 SharePoint 2010의 경우 SharePoint 2010을 이미 설치했거나 설치하려는 서버에서 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 설치를 실행해야 합니다. SharePoint 2010용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 아키텍처는 팜 **내부** 에서 실행되며 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 이 설치된 서버에 SharePoint가 있어야 합니다.  
  
1.  SharePoint 모드에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]를 설치하고 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 SharePoint 팜 및 서비스 계정에 서버 관리자 권한을 부여합니다.  
  
     SharePoint 2010 배포는 spPowerPivot.msi를 지원하지 않으며 SharePoint 2010에는 .msi가 필요하지 **않습니다** .  
  
     SharePoint의 두 버전에 대해 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 설치 프로세스는 SQL Server 설치 마법사에서 **SharePoint용 SQL Server PowerPivot** 의 설정 역할을 선택하거나 SQL Server 명령 프롬프트 설치를 사용하여 시작됩니다.  
  
2.  SQL Server 설치 마법사는 두 개의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 구성 도구를 설치합니다. 구성 도구 중 하나는 SharePoint 2013을 지원하고 다른 하나는 SharePoint 2010을 지원합니다.  
  
     SharePoint 2010용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 을 구성하려면 **PowerPivot 구성 도구** 를 사용합니다.  
  
3.  자세한 내용은 [PowerPivot for SharePoint 2010 Installation](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)을 참조하세요.  
  
 **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]**  
  
1.  SharePoint 모드의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치는 이전 릴리스와 달라지지 않았습니다.  
  
     SharePoint 2010 및 SharePoint 2013의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치 단계는 매우 유사합니다. SharePoint 버전에 관한 중요 참고 사항은 다음과 같습니다.  
  
    -   지원되는 다음 항목의 조합을 참조하세요.  
  
        -   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 버전입니다.  
  
        -   SharePoint 제품용 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능  
  
        -   SharePoint 제품의 버전  
  
         [지원 되는 SharePoint 및 Reporting Services 서버와 추가 기능 조합 &#40;SQL Server 2014&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
    -   SharePoint 2010의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에는 SharePoint 2010 SP2(서비스 팩 2)가 필요합니다.  
  
    1.  SharePoint 모드의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 설치합니다. [Sharepoint 모드 설치 &#40;sharepoint 2010 및 sharepoint 2013&#41; 을 Reporting Services](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md) 하 고 sharepoint [2010 용 sharepoint 모드 Reporting Services 설치](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)합니다.  
  
    2.  SharePoint 제품용 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능(rsSharePoint.msi)을 설치합니다. [Sharepoint &#40;SharePoint 2010 및&#41;sharepoint 2013 용 Reporting Services 추가 기능 설치 또는 제거](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)를 참조 하세요. Sharepoint 용 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능에 대 한 최신 버전은 [sharepoint 제품용 Reporting Services 추가 기능을 찾을 수 있는 위치](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)를 참조 하세요.  
  
    3.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 서비스와 하나 이상의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션을 구성합니다. 자세한 내용은 [sharepoint 2013에 대 한 Reporting Services Sharepoint 모드 설치](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md)에서 "Reporting Services 서비스 응용 프로그램 만들기" 섹션을 참조 하세요.  
  
##  <a name="bkm_database_attach"></a>데이터베이스 연결 업그레이드 및 SharePoint 2013 개요  
 SharePoint 2013에서는 전체 업그레이드를 지원하지 않습니다. 그러나 **데이터베이스 연결 업그레이드는 지원**됩니다.  
  
 기존 PowerPivot 설치가 SharePoint 2010에 통합되어 있는 경우에는 SharePoint 서버를 전체 업그레이드할 수 없습니다.  그러나 SharePoint 데이터베이스 연결 업그레이드 일부로 다음 단계를 수행할 수 있습니다.  
  
1.  새로 SharePoint Server 2013 팜을 설치합니다.  
  
2.  SharePoint 데이터베이스 연결 업그레이드를 완료하고 PowerPivot 관련 콘텐츠 데이터베이스를 SharePoint 2013 팜으로 마이그레이션합니다.  
  
3.  SharePoint 모드에서 SQL Server Analysis Services 인스턴스를 설치하고 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 SharePoint 팜 및 서비스 계정에 서버 관리자 권한을 부여합니다.  
  
4.  SharePoint 2013용 PowerPivot 설치 패키지 **spPowerPivot.msi** 를 SharePoint 팜의 각 서버에 설치합니다.  
  
5.  SharePoint 2013 중앙 관리에서 3단계에서 만든 SharePoint 모드로 실행하는 Analysis Services 서버를 사용하도록 Excel Services를 구성합니다.  
  
     새로 고침 일정을 마이그레이션하려면 PowerPivot 서비스 애플리케이션을 구성합니다.  
  
> [!NOTE]  
>  PowerPivot 및 SharePoint 데이터베이스 연결 업그레이드에 대한 자세한 내용은 다음을 참조하십시오.  
  
-   [SharePoint 2013으로 PowerPivot 마이그레이션](https://docs.microsoft.com/analysis-services/instances/install-windows/migrate-power-pivot-to-sharepoint-2013)  
  
-   [SharePoint 2013으로 업그레이드 프로세스의 개요](https://go.microsoft.com/fwlink/p/?LinkId=256688).  
  
-   [SharePoint 2013으로 업그레이드하기 전에 정리 준비](https://go.microsoft.com/fwlink/p/?LinkId=256689).  
  
-   [SharePoint 2010에서 SharePoint 2013으로 데이터베이스 업그레이드](https://go.microsoft.com/fwlink/p/?LinkId=256690).  
  
## <a name="see-also"></a>관련 항목  
 [SharePoint 제품용 Reporting Services 추가 기능 검색 위치](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)   
 [지원 되는 SharePoint 및 Reporting Services 서버와 추가 기능 조합 &#40;SQL Server 2014&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)   
 [Sharepoint &#40;sharepoint 2010 및 sharepoint 2013 용 Reporting Services 추가 기능 설치 또는 제거&#41;](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
