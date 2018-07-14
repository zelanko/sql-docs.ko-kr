---
title: SharePoint (PowerPivot 및 Reporting Services)를 사용 하 여 SQL Server BI 기능 설치 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3166107c-30c2-468e-bb1b-bb42b79b37c3
caps.latest.revision: 20
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 85ded5847bbb2bc1c32336e999b3579925a4e930
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37325543"
---
# <a name="install-sql-server-bi-features-with-sharepoint-powerpivot-and-reporting-services"></a>SharePoint와 함께 SQL Server BI 기능 설치(PowerPivot 및 Reporting Services)
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint의 BI (비즈니스 인텔리전스) 기능을 사용 하도록 설정 하려면 Microsoft SharePoint 팜과 통합 될 수 있습니다. 이러한 기능에 포함 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]합니다. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] SharePoint 팜에 대 한 데이터 액세스 합니다. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]은 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel에서 만들어지고 SharePoint 라이브러리에서 액세스되는 통합 문서를 위한 데이터 엔진입니다. 저장 한 후에 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서를 SharePoint에 사용할 수 것에 대 한 데이터 소스로 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 보고서입니다.  
  
 SharePoint 2010에 필요한 설치 및 구성 단계 중 일부는 SharePoint 2013에 필요한 단계와 다릅니다. 이 단원의 항목 중 일부는 SharePoint의 두 버전에 모두에 적용됩니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 &#124; SharePoint 2010|  
  
 ![참고](../../../2014/reporting-services/media/rs-fyinote.png "참고") 현재 릴리스 정보를 참조 하세요. [SQL server 2014 릴리스 정보](http://go.microsoft.com/fwlink/?LinkID=296445)합니다.  
  
##  <a name="bkmk_top"></a> 항목 내용  
  
-   [SQL Server BI 시나리오 및 SharePoint 2013](#bkmk_bi_scenarios)  
  
-   [설치 개요](#bkmk_install_sharepoint2013_overview)  
  
## <a name="in-this-section"></a>섹션 내용  
 이 항목의 정보 외에 다음과 같은 관련 항목이 이 섹션에 포함되어 있습니다.  
  
 [SharePoint의 SQL Server BI 기능에 대한 배포 토폴로지](deployment-topologies-for-sql-server-bi-features-in-sharepoint.md)  
  
 [SharePoint 2010 팜에서 SQL Server BI 기능을 사용하기 위한 지침](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
 [SharePoint와 함께 BI 기능을 설치하기 위한 검사 목록](../../../2014/sql-server/install/checklists-for-installing-bi-features-with-sharepoint.md)  
  
 [Reporting Services SharePoint 모드 설치 &#40;SharePoint 2010 및 SharePoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)  
  
 [SharePoint 2013용 PowerPivot 설치](../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
 [SharePoint 2010용 PowerPivot 설치](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
##  <a name="bkmk_bi_scenarios"></a> SQL Server BI 시나리오 및 SharePoint 2013  
 이 섹션에는 설치 및 구성할 때 선택할 수 있는 여러 수준의 BI 기능이 요약되어 있습니다.  
  
 SharePoint 2013의 Excel Services에는 브라우저에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서와 상호 작용할 수 있도록 데이터 모델 기능이 포함되어 있습니다. 기본 데이터 모델 기능에 대 한 필요가 없습니다를 배포 하는 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 추가 기능에 팜에 합니다. SharePoint 모드의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버를 설치하고 Excel Services **데이터 모델** 설정 내에 서버를 등록해야 합니다.  
  
 배포는 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 추가 기능에서 추가 기능 및 SharePoint 팜의 기능을 사용 하도록 설정 합니다. 추가 기능에는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 갤러리, 데이터 새로 고침 예약 및 PowerPivot 관리 대시보드. 추가 정보는 테이블을 참조하세요.  
  
||Level|기능|설치 또는 구성|  
|-|-----------|--------------|--------------------------|  
|1|SharePoint 전용|기본 Excel Services 기능|SharePoint Server 2013에 포함된 Excel Services 및 기타 서비스입니다.|  
|**2**|SharePoint와 SharePoint 모드의 Analysis Services|브라우저의 대화형 PowerPivot 통합 문서|SharePoint 모드의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 를 설치합니다.<br /><br /> Excel Services에 Analysis Services 서버를 등록합니다.|  
|**3**|SharePoint와 SharePoint 모드의 Reporting Services|파워 뷰|SharePoint 모드의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 설치합니다.<br /><br /> 설치 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 애드인 **(기능 rsSharePoint.msi)** SharePoint에 대 한 합니다. 자세한 내용은 [설치 또는 SharePoint 용 Reporting Services 추가 기능에 제거 &#40;SharePoint 2010 및 SharePoint 2013&#41;](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)|  
|**4**|모든 PowerPivot 기능|팜 외부로부터 통합 문서를 데이터 원본으로 액세스합니다.<br /><br /> 데이터 새로 고침을 예약합니다.<br /><br /> PowerPivot 갤러리입니다.<br /><br /> 관리 대시보드입니다.<br /><br /> BISM 링크 파일 콘텐츠 형식입니다.|PowerPivot for SharePoint 2013 추가 기능에서 배포할 **(spPowerPivot.msi)** 합니다. 자세한 내용은 다음 항목을 참조하세요.<br /><br /> [설치 하거나 SharePoint 추가 기능에 대 한 PowerPivot을 제거할 &#40;SharePoint 2013&#41;](../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)<br /><br /> **spPowerPivot.msi**를 다운로드하는 방법에 대한 자세한 내용은 [SQL Server 2014 SharePoint용 PowerPivot 다운로드](http://go.microsoft.com/fwlink/?LinkID=296473)를 참조하세요.|  
  
 사용 하도록 설정 하는 자세한 방법은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 기능을 참조 하세요 [The SQL Server BI 스토리 SharePoint 2013 용](http://blogs.msdn.com/b/analysisservices/archive/2012/07/27/introducing-the-bi-light-up-story-for-sharepoint-2013.aspx) (http://blogs.msdn.com/b/analysisservices/archive/2012/07/27/introducing-the-bi-light-up-story-for-sharepoint-2013.aspx)합니다.  
  
##  <a name="bkmk_install_sharepoint2013_overview"></a> 설치 개요  
 둘 다 사용 하려는 경우 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 고 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], SQL Server 설치 마법사를 두 번 실행 합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 및 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 별도 선택 항목에는 **설치 역할** SQL Server 설치 마법사의 페이지입니다.  
  
 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] SharePoint 2010과 SharePoint 2013을 모두 지원합니다. 하지만 SharePoint 버전에 따라 다른 아키텍처 및 설치 프로세스를 사용 합니다.  
  
 다음은 단일 서버에 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] BI 기능을 배포하는 설치 단계를 요약한 것입니다.  
  
 **[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013**  
  
 에 대 한 **SharePoint 2013**는 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] SharePoint 제품이 설치 되지 않은 서버에 설치할 수 있습니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] SharePoint 2013의 경우 사용 되는 아키텍처 실행 **외부** SharePoint 팜 및 하거나 SharePoint 설치를 포함 하는 서버에 설치할 수 있습니다 또는 수 포함 되지 않은 서버를 설치는 SharePoint 설치 합니다.  
  
1.  SharePoint Server 2013을 설치하고 Excel Services를 설치합니다.  
  
2.  SharePoint 모드에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]를 설치하고 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 SharePoint 팜 및 서비스 계정에 서버 관리자 권한을 부여합니다.  
  
     두 SharePoint 버전 모두에 대 한 합니다 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 설치 역할을 선택 하 여 설치 프로세스가 시작 됩니다 **SQL Server PowerPivot for SharePoint** SQL Server 설치 마법사를 사용 하 여 SQL Server 명령 프롬프트에서 설치 합니다.  
  
     ![설치 역할](../../../2014/sql-server/install/media/gmni-setupui-featurerole-sql2012sp1.gif "설치 역할")  
  
3.  SharePoint 2013 용 확장할 수 있습니다는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 기능 및 환경을 합니다. 다운로드 및 실행 **spPowerPivot.msi** 에 대 한 서버 쪽 데이터 새로 고침 처리, 공동 작업 및 관리 지원을 추가할 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서. 자세한 내용은 [Microsoft® SharePoint용 Microsoft SQL Server 2014 PowerPivot](http://go.microsoft.com/fwlink/?LinkID=324854)을 참조하세요.  
  
     실행 합니다 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 설치 패키지 **spPowerPivot.msi** 데이터의 올바른 버전을 확인 하려면 SharePoint 팜의 각 서버에서 공급자가 설치 됩니다.  
  
4.  구성 하려면 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 사용 하 여 SharePoint 2013 용 **SharePoint 용 PowerPivot 2013 구성** 도구입니다.  
  
     SQL Server 설치 마법사가 두 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 구성 도구입니다. 구성 도구 중 하나는 SharePoint 2013을 지원하고 다른 하나는 SharePoint 2010을 지원합니다.  
  
     ![두 개의 파워 피벗 구성 도구](../../../2014/analysis-services/media/as-powerpivot-configtools-bothicons.gif "두 개의 파워 피벗 구성 도구")  
  
5.  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스를 사용하도록 SharePoint Server 2013의 Excel Services를 구성합니다. 자세한 내용은 "Basic Analysis Services SharePoint 통합 구성" 섹션을 참조 [PowerPivot for SharePoint 2013 Installation](../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)그리고 [관리 Excel Services 데이터 모델 설정 (SharePoint Server 2013)](http://technet.microsoft.com/library/jj219780.aspx) (http://technet.microsoft.com/library/jj219780.aspx)합니다.  
  
6.  자세한 내용은 [SharePoint 용 PowerPivot 2013 설치](../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)합니다.  
  
 **[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010**  
  
 SharePoint 2010의 경우 SharePoint 2010을 이미 설치했거나 설치하려는 서버에서 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 설치를 실행해야 합니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] SharePoint 2010 용 아키텍처 실행 **내** 팜의 서버에 SharePoint가 있어야 하 고는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] SharePoint가 설치에 대 한 합니다.  
  
1.  SharePoint 모드에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]를 설치하고 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 SharePoint 팜 및 서비스 계정에 서버 관리자 권한을 부여합니다.  
  
     SharePoint 2010 배포는 spPowerPivot.msi를 지원하지 않으며 SharePoint 2010에는 .msi가 필요하지 **않습니다** .  
  
     두 SharePoint 버전 모두에 대 한 합니다 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 설치 역할을 선택 하 여 설치 프로세스가 시작 됩니다 **SQL Server PowerPivot for SharePoint** SQL Server 설치 마법사를 사용 하 여 SQL Server 명령 프롬프트에서 설치 합니다.  
  
2.  SQL Server 설치 마법사가 두 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 구성 도구입니다. 구성 도구 중 하나는 SharePoint 2013을 지원하고 다른 하나는 SharePoint 2010을 지원합니다.  
  
     구성 하려면 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] SharePoint 2010을 사용 합니다 **PowerPivot 구성 도구** 합니다.  
  
3.  자세한 내용은 [PowerPivot for SharePoint 2010 Installation](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)을 참조하세요.  
  
 **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]**  SharePoint 2010 및 2013  
  
1.  에 대 한 설치 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드를 이전 릴리스로부터 변경 되지 않습니다.  
  
     [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 2010 및 SharePoint 2013에 대 한 설치 단계는 매우 유사 합니다. SharePoint 버전에 관한 중요 참고 사항은 다음과 같습니다.  
  
    -   지원되는 다음 항목의 조합을 참조하세요.  
  
        -   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 버전입니다.  
  
        -   SharePoint 제품용 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능  
  
        -   SharePoint 제품의 버전  
  
         [지원 되는 SharePoint와 Reporting Services 서버 및 추가 기능의 조합 &#40;SQL Server 2014&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
    -   SharePoint 2010의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에는 SharePoint 2010 SP2(서비스 팩 2)가 필요합니다.  
  
    1.  SharePoint 모드의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 설치합니다. [Reporting Services SharePoint 모드 설치 &#40;SharePoint 2010 및 SharePoint 2013&#41; ](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md) 하 고 [Reporting Services SharePoint 2010 용 SharePoint 모드 설치](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)합니다.  
  
    2.  SharePoint 제품용 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능(rsSharePoint.msi)을 설치합니다. 참조 [설치 추가 또는 제거는 Reporting Services-SharePoint 용 &#40;SharePoint 2010 및 SharePoint 2013&#41;](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)합니다. 최신 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 제품용 추가 참조 하십시오 [SharePoint 제품용 Reporting Services 추가 기능 검색 위치](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)합니다.  
  
    3.  구성 된 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 서비스와 하나 이상의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램입니다. 자세한 내용은 "Reporting Services 서비스 응용 프로그램 만들기" 섹션을 참조 [Reporting Services SharePoint 모드 설치 SharePoint 2013 용](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md)합니다.  
  
##  <a name="bkm_database_attach"></a> 데이터베이스 연결 개요 업그레이드 및 SharePoint 2013  
 SharePoint 2013에서는 전체 업그레이드를 지원하지 않습니다. 그러나 **데이터베이스 연결 업그레이드는 지원**됩니다.  
  
 기존 PowerPivot 설치가 SharePoint 2010에 통합되어 있는 경우에는 SharePoint 서버를 전체 업그레이드할 수 없습니다.  그러나 SharePoint 데이터베이스 연결 업그레이드 일부로 다음 단계를 수행할 수 있습니다.  
  
1.  새로 SharePoint Server 2013 팜을 설치합니다.  
  
2.  SharePoint 데이터베이스 연결 업그레이드를 완료하고 PowerPivot 관련 콘텐츠 데이터베이스를 SharePoint 2013 팜으로 마이그레이션합니다.  
  
3.  SharePoint 모드에서 SQL Server Analysis Services의 인스턴스를 설치 하 고 SharePoint 팜 및 서비스 계정에서 서버 관리자 권한을 부여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]합니다.  
  
4.  SharePoint 2013용 PowerPivot 설치 패키지 **spPowerPivot.msi** 를 SharePoint 팜의 각 서버에 설치합니다.  
  
5.  SharePoint 2013 중앙 관리에서 3단계에서 만든 SharePoint 모드로 실행하는 Analysis Services 서버를 사용하도록 Excel Services를 구성합니다.  
  
     새로 고침 일정을 마이그레이션하려면 PowerPivot 서비스 응용 프로그램을 구성합니다.  
  
> [!NOTE]  
>  PowerPivot 및 SharePoint 데이터베이스 연결 업그레이드에 대한 자세한 내용은 다음을 참조하십시오.  
  
-   [SharePoint 2013으로 PowerPivot 마이그레이션](../../analysis-services/instances/install-windows/migrate-power-pivot-to-sharepoint-2013.md)  
  
-   [SharePoint 2013으로 업그레이드 프로세스의 개요](http://go.microsoft.com/fwlink/p/?LinkId=256688).  
  
-   [SharePoint 2013으로 업그레이드하기 전에 정리 준비](http://go.microsoft.com/fwlink/p/?LinkId=256689).  
  
-   [SharePoint 2010에서 SharePoint 2013으로 데이터베이스 업그레이드](http://go.microsoft.com/fwlink/p/?LinkId=256690).  
  
## <a name="see-also"></a>관련 항목  
 [SharePoint 제품용 Reporting Services 추가 기능 검색 위치](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)   
 [지원 되는 SharePoint와 Reporting Services 서버 및 추가 기능의 조합 &#40;SQL Server 2014&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)   
 [설치 또는 제거는 Reporting Services 추가-SharePoint 용 &#40;SharePoint 2010 및 SharePoint 2013&#41;](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
