---
title: Reporting Services 보고서 서버(SharePoint 모드) | Microsoft Docs
ms.prod: sql-server-2014
ms.technology:
- reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 06/13/2017
ms.openlocfilehash: 246b0be389857e002e5c9e30cb899826234a58b7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63273834"
---
# <a name="reporting-services-report-server-sharepoint-mode"></a>Reporting Services 보고서 서버(SharePoint 모드)

**SharePoint 모드**에 대해 구성된 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보고서 서버는 SharePoint 제품 배포 내에서 실행할 수 있습니다. SharePoint 모드의 보고서 서버에서는 보고서 및 기타 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 콘텐츠 형식에 SharePoint의 협업 및 관리 기능을 사용할 수 있습니다. SharePoint 모드를 사용하려면 SharePoint 제품에 대한 적절한 버전의 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 추가 기능을 SharePoint 웹 프런트 엔드에 설치해야 합니다.  
  
설치 및 구성하는 방법은 다음 항목을 참조하세요.  
  
- [SharePoint 2013 용 Reporting Services SharePoint 모드 설치](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md)  
  
- [SharePoint 2010용 Reporting Services SharePoint 모드 설치](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)  
  
- [팜에 추가 보고서 서버 추가 &#40;SSRS 스케일 아웃&#41;](install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)합니다.  
  
 이 릴리스의 새로운 기능에 대 한 내용은의 'SharePoint' 섹션을 참조 하세요 [새로운 &#40;Reporting Services&#41;](../../2014/reporting-services/what-s-new-reporting-services.md)합니다.  
  
 **항목 내용**  
  
-   [기능 요약](#bkmk_featuresum)  
  
-   [연결된 모드 및 로컬 모드](#bkmk_connectedandlocal)  
  
-   [지원되지 않는 SharePoint 기능](#bkmk_unsupportedsharepoint)  
  
-   [지원되는 SharePoint 추가 기능과 보고서 서버의 조합](#bkmk_supportedcombinations)  
  
-   [통합을 제공하는 구성 요소](#bkmk_components)  
  
-   [언어 관련 고려 사항](#bkmk_language)  
  
-   [관련 작업](#bkmk_relatedtasks)  
  
##  <a name="bkmk_featuresum"></a> 기능 요약

 SharePoint 통합 모드에서 실행되도록 보고서 서버를 구성하면 이 모드에서 보고서 서버를 배포할 때만 사용 가능한 다음 추가 기능이 제공됩니다.  
  
-   경고를 포함한 SharePoint 문서 관리 및 협업 기능을 사용할 수 있습니다. SharePoint 사이트는 단일 위치에서 모든 보고서 항목에 대해 액세스 및 관리 작업을 수행할 수 있는 통합 포털을 제공합니다.  
  
-   SharePoint 권한 및 인증 공급자를 사용하여 보고서, 모델 및 기타 항목에 대한 액세스를 제어할 수 있습니다.  
  
-   SharePoint 배포 토폴로지를 사용하여 인터넷 연결을 통해 보고서를 방화벽 외부에 배포할 수 있습니다. 보고서 서버는 인터넷 액세스가 가능하도록 구성된 대규모 SharePoint 배포 컨텍스트에서 보고서 및 데이터 처리 서비스를 제공합니다.  
  
-   SharePoint 사이트의 사용자 지정 애플리케이션 페이지에서 보고서, 모델, 데이터 원본, 일정 및 보고서 기록을 관리할 수 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 다른 도구와 같은 방식으로 SharePoint 사이트에서 속성을 설정하고 일정 및 구독을 정의하며 보고서 기록을 생성 및 관리할 수 있습니다.  
  
-   보고서, 보고서 모델, 리소스 및 공유 데이터 원본 파일을 Office SharePoint Server의 보고서 센터를 비롯한 SharePoint 라이브러리에 게시하거나 업로드할 수 있습니다.  
  
     보고서 디자이너, 모델 디자이너 및 보고서 작성기를 사용하여 SharePoint 라이브러리에 직접 게시할 보고서 및 데이터 원본을 만들 수 있습니다. 또한 SharePoint 사이트에서 업로드 동작을 사용하여 SharePoint 라이브러리에 보고서 정의 및 보고서 모델을 추가할 수 있습니다.  
  
     보고서 서버에서는 사용하는 서버 모드에 관계없이 동일한 방법으로 보고서 정의를 처리하므로 보고서 데이터 및 레이아웃은 서버 모드의 영향을 받지 않습니다. 기본 모드 보고서 서버에서 실행할 수 있는 모든 보고서는 SharePoint 통합 모드로 구성된 보고서 서버에서 실행될 수 있습니다.  
  
-   새 SharePoint 배달 확장 프로그램을 사용하여 보고서를 구독하고 SharePoint 라이브러리에 배달할 수 있습니다. 전자 메일을 통해 보고서를 배달하거나 공유 폴더로 보고서를 배달할 수도 있습니다. 보고서 배달에는 보고서 서버 배달 확장 프로그램이 사용됩니다. 런타임에 쿼리된 구독자 데이터를 사용하여 대규모 보고서 배포용 데이터 기반 구독을 만들 수 있습니다.  
  
-   SharePoint 페이지에 추가할 수 있는 보고서 뷰어 웹 파트를 통해 SharePoint 웹 애플리케이션 내에서 보고서를 볼 수 있습니다. 웹 파트에는 페이지 탐색, 검색, 인쇄 및 내보내기 기능이 포함되어 있습니다.  
  
-   새 SOAP 엔드포인트에 대해 프로그래밍하여 SharePoint 사이트와 통합되는 사용자 지정 애플리케이션을 만들 수 있습니다. 업데이트된 WMI(Windows Management Instrumentation) 공급자를 사용하여 SharePoint 통합 모드에서 실행되는 보고서 서버 인스턴스를 프로그래밍 방식으로 구성할 수도 있습니다.  
  
-   연결된 모드의 Microsoft Access 서비스 보고  
  
-   AAM 영역, 인터넷 연결 배포 및 SharePoint 목록에 대한 SharePoint 사용자 토큰.  
  
##  <a name="bkmk_connectedandlocal"></a> 연결된 모드 및 로컬 모드

 SQL Server 2008 R2 릴리스에는 SharePoint 2010 제품용 Microsoft SQL Server 2008 R2 이상 Reporting Services 추가 기능이 설치되어 있는 SharePoint 2010 서버에서 보고서를 볼 수 있도록 *로컬 모드* 라는 새로운 모드가 도입되었습니다.  
  
-   *로컬 모드*: 로컬 모드에서는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보고서 서버와 통합하지 않고도 SharePoint 문서 라이브러리에서 로컬로 보고서를 렌더링할 수 있습니다. SharePoint 제품용 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 추가 기능은 필요하지만 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보고서 서버는 아닙니다. 추가 기능은 SharePoint 2010 제품 준비 도구를 비롯한 여러 가지 방법으로 설치할 수 있습니다. 로컬 모드에 대한 자세한 내용은 [보고서 뷰어의 로컬 모드와 연결 모드 보고서를 보고서 뷰어에서 &#40;SharePoint 모드의 Reporting Services&#41; ](../../2014/reporting-services/local-vs-connected-mode-report-viewer-reporting-services-sharepoint-mode.md) 하 고 [SharePoint 제품용 Reporting Services 추가 기능 검색 위치](install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)합니다.  
  
-   *연결 된 모드*: 통합 하 여 연결 된 모드는 지원 되는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 중앙 관리를 사용 하 여 SharePoint 팜에 보고서 서버. 보고서 서버와의 통합을 사용 하면 전체 종단 간 보고, SharePoint 2010의 공동 작업 기능을 포함 하는 보고서 서버는 서버 기반 기능도 제공: 구독, 스냅숏 및 서버 기반 기능도 사용할 수 있습니다.  
  
##  <a name="bkmk_unsupportedsharepoint"></a> 지원되지 않는 SharePoint 기능

 일부 SharePoint 기능은 통합 작업에서 사용할 수 없습니다. 다음은 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 에 직접 통합되지 않는 SharePoint 기능 목록입니다.  
  
-   Secure Store Service.  
  
-   문서 라이브러리의 Reporting Services 파일에 대해서는 SharePoint Outlook 일정 통합이나 SharePoint 일정을 사용할 수 없습니다.  
  
-   SharePoint Business Data 카탈로그.  
  
-   SharePoint 개인 설정도 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 페이지에서 지원되지 않습니다. SharePoint 웹 애플리케이션에서 익명 액세스를 사용할 수 있는 경우에는 보고서 서버 통합이 지원되지 않습니다.  
  
-   SQL Server Reporting Services는 SharePoint 문서 라이브러리 버전 제어를 지원하지 **않습니다** . “문서 버전 기록”을 사용하도록 구성된 문서 라이브러리에 보고서 항목을 저장한 경우 Reporting Services 기능은 제대로 작동하지 않으며 ULS 로그에 오류가 생성됩니다. 다음은 ULS 로그에 있는 오류의 예입니다.  
  
    -   “...보고서와 연결된 데이터 원본을 사용할 수 없습니다”.  
  
     문서 라이브러리 버전 기록은 “라이브러리 설정”의 ”버전 관리 설정” 페이지에 구성됩니다.  
  
##  <a name="bkmk_supportedcombinations"></a> 지원되는 SharePoint 추가 기능과 보고서 서버의 조합

 보고서 서버, SharePoint용 Reporting Services 추가 기능 및 SharePoint 제품의 모든 조합에서 모든 기능이 지원되는 것은 아닙니다. 자세한 내용은 [지원 되는 SharePoint 및 Reporting Services 서버 및 추가 &#40;SQL Server 2014&#41;](install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
> [!NOTE]  
>  해당 버전의 SharePoint 제품에 올바른 버전의 Reporting Services 추가 기능을 사용해야 합니다.  
  
##  <a name="bkmk_components"></a> 통합을 제공하는 구성 요소

 여러 서버를 단일 배포로 결합하려면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 설치를 SharePoint 제품의 인스턴스와 통합해야 합니다.  
  
 통합은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 및 SharePoint 제품용 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 추가 기능을 통해 제공됩니다. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 추가 기능은 다운로드한 다음 적절한 버전의 SharePoint를 실행하는 서버에 설치할 수 있는 무료 배포 가능 구성 요소입니다.  
  
> [!TIP]  
>  보고서 서버, SharePoint용 Reporting Services 추가 기능 및 SharePoint 제품의 모든 조합에서 모든 기능이 지원되는 것은 아닙니다. 자세한 내용은 참조 하십시오 [지원 되는 SharePoint 및 Reporting Services 서버 및 추가 &#40;SQL Server 2014&#41;](install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)합니다.  
  
-   SharePoint에서 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 추가 기능은 SharePoint 사이트 또는 팜에서 보고서 서버 내용을 확인, 저장 및 관리할 수 있도록 ReportServer 프록시 엔드포인트, 보고서 뷰어 웹 파트 및 애플리케이션 페이지를 제공합니다.  
  
-   [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 에서는 업데이트된 프로그램 파일, SOAP 엔드포인트, 사용자 지정 보안 및 배달 확장 프로그램을 제공합니다. 보고서 서버는 SharePoint 사이트를 통해 보고서 액세스와 배달만 전적으로 지원하는 SharePoint 통합 모드에서 실행되도록 구성해야 합니다.  
  
 SharePoint에 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 추가 기능을 설치하고 통합을 위해 두 서버를 구성하면 SharePoint 라이브러리에 보고서 서버 콘텐츠 형식을 업로드 또는 게시한 다음 SharePoint 사이트에서 해당 문서를 보고 관리할 수 있습니다. 보고서 서버 내용을 업로드하거나 게시하는 것이 중요한 첫 번째 단계입니다. 웹 파트와 페이지는 SharePoint 사이트에서 보고서 정의(.rdl), 보고서 모델(.smdl) 및 공유 데이터 원본(.rsds)을 선택하면 사용할 수 있게 됩니다.  
  
##  <a name="bkmk_language"></a> 언어 관련 고려 사항

 [!INCLUDE[SPF2010](../includes/spf2010-md.md)] 및 [!INCLUDE[SPS2010](../includes/sps2010-md.md)] 제품은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
 보고서 서버를 SharePoint 제품 배포 내에서 실행되도록 구성하는 경우 여러 언어가 혼합되어 나타날 수 있습니다. 사용자 인터페이스, 설명서 및 메시지는 다음 언어로 표시됩니다.  
  
-   [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]의 모든 응용 프로그램 페이지, 도구, 오류, 경고 및 메시지는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 언어 중 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 사용되는 언어로 표시됩니다.  
  
-   SharePoint 사이트, 보고서 뷰어 웹 파트 및 보고서 작성기에서 애플리케이션 페이지를 열면 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 추가 기능에 대해 지원되는 언어 중 하나로 표시됩니다. 지원되는 언어 목록을 보려면 [SQL Server 다운로드](https://msdn.microsoft.com/sql/downloads/)로 이동하여 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 추가 기능 다운로드 페이지를 찾으세요.  
  
-   SharePoint 사이트, SharePoint 중앙 관리, 온라인 도움말 및 메시지는 Office Server 제품에서 지원되는 언어로 제공됩니다.  
  
 SharePoint 제품 또는 기술의 언어가 보고서 서버 언어와 다르면 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 는 같은 언어군에서 가장 일치하는 언어를 사용합니다. 근접하게 일치하는 대체 언어가 없는 경우 보고서 서버에서는 영어를 사용합니다.  
  
##  <a name="bkmk_relatedtasks"></a> 관련 작업

 다음 표에서는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 모드 보고서 서버와 관련된 태스크를 요약해서 보여 줍니다.  
  
|**태스크**|**링크**|  
|--------------|--------------|  
|SharePoint 모드에서 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 설치 및 구성을 위한 세부 단계|[Reporting Services SharePoint 2010 용 SharePoint 모드 설치](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md) 하 고 [팜에 추가 보고서 서버 추가 &#40;SSRS 확장&#41;](install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)합니다.|  
|보고서 서버를 추가하여 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 배포를 확대합니다.|[팜에 추가 보고서 서버 추가 &#40;SSRS 스케일 아웃&#41; ](install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md) 하 고 [SharePoint의 SQL Server BI 기능에 대 한 배포 토폴로지](../sql-server/install/deployment-topologies-for-sql-server-bi-features-in-sharepoint.md) 합니다.|  
|보기용으로 설치된 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 구성 요소 및 보고서 항목이 포함된 추가 SharePoint 웹 프런트 엔드를 추가합니다.|[팜에 추가 Reporting Services 웹 프런트 엔드 추가](install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 데이터 경고 및 구독 기능에 대한 전자 메일을 구성합니다.|[Reporting Services 서비스 애플리케이션에 대한 메일 구성&#40;SharePoint 2010 및 SharePoint 2013&#41;](install-windows/configure-e-mail-for-a-reporting-services-service-application.md)|  
|TechNet Wiki에 있는 이 릴리스에 대한 최신 정보|[SQL Server 2012 Reporting Services 팁, 요령 및 문제 해결](https://go.microsoft.com/fwlink/?LinkId=221297)(영문)|  
  
## <a name="see-also"></a>관련 항목  
 [설치 또는 제거는 Reporting Services 추가-SharePoint 용 &#40;SharePoint 2010 및 SharePoint 2013&#41; ](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md) [하드웨어 및 소프트웨어 요구 사항 SharePoint 모드의 Reporting Services](../../2014/sql-server/install/hardware-and-software-requirements-for-reporting-services-in-sharepoint-mode.md) [SharePoint 사이트의 보고서 뷰어 웹 파트](../../2014/reporting-services/report-viewer-web-part-on-a-sharepoint-site.md)