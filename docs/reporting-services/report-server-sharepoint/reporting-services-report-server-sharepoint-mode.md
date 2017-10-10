---
title: "Reporting Services 보고서 서버 (SharePoint 모드) | Microsoft Docs"
ms.custom: 
ms.date: 09/26/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: a8cd1bd00ec92535fff73c5eaa4ff9bbe9274ef2
ms.contentlocale: ko-kr
ms.lasthandoff: 10/06/2017

---

# <a name="reporting-services-report-server-sharepoint-mode"></a>Reporting Services 보고서 서버(SharePoint 모드)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  Reporting Services 보고서 서버에 대 한 구성 **SharePoint 모드** SharePoint 제품 배포 내에서 실행할 수 있습니다. SharePoint 모드의 보고서 서버에서는 보고서 및 기타 [!INCLUDE[ssRSnfoversion_md](../../includes/ssrsnoversion-md.md)] 콘텐츠 형식에 SharePoint의 공동 작업 및 관리 기능을 사용할 수 있습니다. SharePoint 모드는 SharePoint 웹 프런트 엔드에 Reporting Services 추가 기능에 SharePoint 제품에 대 한 적절 한 버전을 설치 해야 합니다.  
  
> [!NOTE]
> SQL Server 2016 후 SharePoint와 reporting Services 통합을 사용할 수 없습니다.

 설치 및 구성하는 방법은 다음 항목을 참조하세요.  
  
-   [SharePoint 2010 용 Reporting Services SharePoint 모드 설치](http://msdn.microsoft.com/47efa72e-1735-4387-8485-f8994fb08c8c)합니다.  
  
-   [팜에 추가 보고서 서버 추가](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)합니다.  
  
## <a name="feature-summary"></a>기능 요약

 SharePoint 통합 모드에서 실행되도록 보고서 서버를 구성하면 이 모드에서 보고서 서버를 배포할 때만 사용 가능한 다음 추가 기능이 제공됩니다.  
  
-   경고를 포함한 SharePoint 문서 관리 및 공동 작업 기능을 사용할 수 있습니다. SharePoint 사이트는 단일 위치에서 모든 보고서 항목에 대해 액세스 및 관리 작업을 수행할 수 있는 통합 포털을 제공합니다.  
  
-   SharePoint 권한 및 인증 공급자를 사용하여 보고서, 모델 및 기타 항목에 대한 액세스를 제어할 수 있습니다.  
  
-   SharePoint 배포 토폴로지를 사용하여 인터넷 연결을 통해 보고서를 방화벽 외부에 배포할 수 있습니다. 보고서 서버는 인터넷 액세스가 가능하도록 구성된 대규모 SharePoint 배포 컨텍스트에서 보고서 및 데이터 처리 서비스를 제공합니다.  
  
-   SharePoint 사이트의 사용자 지정 응용 프로그램 페이지에서 보고서, 모델, 데이터 원본, 일정 및 보고서 기록을 관리할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 다른 도구와 같은 방식으로 SharePoint 사이트에서 속성을 설정하고 일정 및 구독을 정의하며 보고서 기록을 생성 및 관리할 수 있습니다.  
  
-   보고서, 보고서 모델, 리소스 및 공유 데이터 원본 파일을 Office SharePoint Server의 보고서 센터를 비롯한 SharePoint 라이브러리에 게시하거나 업로드할 수 있습니다.  
  
     보고서 디자이너, 모델 디자이너 및 보고서 작성기를 사용하여 SharePoint 라이브러리에 직접 게시할 보고서 및 데이터 원본을 만들 수 있습니다. 또한 SharePoint 사이트에서 업로드 동작을 사용하여 SharePoint 라이브러리에 보고서 정의 및 보고서 모델을 추가할 수 있습니다.  
  
     보고서 서버에서는 사용하는 서버 모드에 관계없이 동일한 방법으로 보고서 정의를 처리하므로 보고서 데이터 및 레이아웃은 서버 모드의 영향을 받지 않습니다. 기본 모드 보고서 서버에서 실행할 수 있는 모든 보고서는 SharePoint 통합 모드로 구성된 보고서 서버에서 실행될 수 있습니다.  
  
-   새 SharePoint 배달 확장 프로그램을 사용하여 보고서를 구독하고 SharePoint 라이브러리에 배달할 수 있습니다. 전자 메일을 통해 보고서를 배달하거나 공유 폴더로 보고서를 배달할 수도 있습니다. 보고서 배달에는 보고서 서버 배달 확장 프로그램이 사용됩니다. 런타임에 쿼리된 구독자 데이터를 사용하여 대규모 보고서 배포용 데이터 기반 구독을 만들 수 있습니다.  
  
-   보고서 뷰어 웹 파트를 SharePoint 웹 응용 프로그램 내에서 보고서를 보려면 SharePoint 페이지에 추가할 수 있습니다. 웹 파트 포함 페이지 탐색, 검색, 인쇄 및 내보내기 기능.  
  
-   새 SOAP 끝점에 대해 프로그래밍하여 SharePoint 사이트와 통합되는 사용자 지정 응용 프로그램을 만들 수 있습니다. 업데이트된 WMI(Windows Management Instrumentation) 공급자를 사용하여 SharePoint 통합 모드에서 실행되는 보고서 서버 인스턴스를 프로그래밍 방식으로 구성할 수도 있습니다.  
  
-   연결된 모드의 Microsoft Access 서비스 보고  
  
-   AAM 영역, 인터넷 연결 배포 및 SharePoint 목록에 대한 SharePoint 사용자 토큰.  
  
## <a name="connected-mode-and-local-mode"></a>연결 된 모드 및 로컬 모드

 SQL Server 2008 R2 릴리스에는 SharePoint 2010 제품용 Microsoft SQL Server 2008 R2 이상 Reporting Services 추가 기능이 설치되어 있는 SharePoint 2010 서버에서 보고서를 볼 수 있도록 *로컬 모드* 라는 새로운 모드가 도입되었습니다.  
  
-   *로컬 모드*: 로컬 모드에서는 보고서를 로컬로 Reporting Services 보고서 서버와 통합 하지 않고도 SharePoint 문서 라이브러리에서 렌더링할 수 있습니다. Reporting Services 추가 기능에 SharePoint 제품에 대 한 필요 하지만 Reporting Services 보고서 서버는 없습니다. 추가 기능은 SharePoint 2010 제품 준비 도구를 비롯한 여러 가지 방법으로 설치할 수 있습니다. 로컬 모드에 대 한 자세한 내용은 참조 하십시오. [로컬 모드 보고서 뷰어에 보고서 연결 된 모드와](../../reporting-services/report-server-sharepoint/local-mode-vs-connected-mode-reports-in-the-report-viewer.md) 및 [SharePoint 제품용 Reporting Services 추가 기능을 찾을 수 있는 위치](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)합니다.  
  
-   *연결 된 모드*: 연결 된 모드 Reporting Services 보고서 서버를 SharePoint 중앙 관리를 사용 하 여 SharePoint 팜에 통합 하 여 사용할 수 있습니다. 보고서 서버와의 통합을 통해 완전한 보고가 가능해질 뿐만 아니라 SharePoint 2010의 공동 작업 기능과 구독, 스냅숏 및 서버 기반 처리와 같은 보고서 서버의 서버 기반 기능도 사용할 수 있습니다.  
  
## <a name="unsupported-sharepoint-features"></a>지원 되지 않는 sharePoint 기능

 일부 SharePoint 기능은 통합 작업에서 사용할 수 없습니다. 다음은 Reporting Services와 직접 통합 되지 않는 SharePoint 기능 목록입니다.  
  
-   Secure Store Service.  
  
-   문서 라이브러리의 Reporting Services 파일에 대해서는 SharePoint Outlook 일정 통합이나 SharePoint 일정을 사용할 수 없습니다.  
  
-   SharePoint Business Data 카탈로그.  
  
-   SharePoint 개인 설정 Reporting Services 페이지에서 지원 되지 않습니다. SharePoint 웹 응용 프로그램에서 익명 액세스를 사용할 수 있는 경우에는 보고서 서버 통합이 지원되지 않습니다.  
  
-   SQL Server Reporting Services는 SharePoint 문서 라이브러리 버전 제어를 지원하지 **않습니다** . “문서 버전 기록”을 사용하도록 구성된 문서 라이브러리에 보고서 항목을 저장한 경우 Reporting Services 기능은 제대로 작동하지 않으며 ULS 로그에 오류가 생성됩니다. 다음은 ULS 로그에 있는 오류의 예입니다.  
  
    -   “…보고서와 연결된 데이터 원본을 사용할 수 없습니다”.  
  
     문서 라이브러리 버전 기록은 “라이브러리 설정”의 ”버전 관리 설정” 페이지에 구성됩니다.  
  
## <a name="supported-combinations-of-the-sharepoint-add-in-and-report-server"></a>지원 되는 SharePoint 추가 기능 및 보고서 서버는 조합

 보고서 서버, SharePoint용 Reporting Services 추가 기능 및 SharePoint 제품의 모든 조합에서 모든 기능이 지원되는 것은 아닙니다. 자세한 내용은 참조 [조합의 SharePoint 및 Reporting Services 서버 및 추가 기능을 지원 합니다.](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
> [!NOTE]  
>  해당 버전의 SharePoint 제품에 올바른 버전의 Reporting Services 추가 기능을 사용해야 합니다.  
  
## <a name="components-that-provide-integration"></a>통합 기능을 제공 하는 구성 요소

 설치 된 여러 서버를 단일 배포로 결합 하려면 통합 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SharePoint 제품의 인스턴스와 Reporting Services  
  
 통합을 통해 제공 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 SharePoint 제품용 Reporting Services add-in 합니다. Reporting Services 추가 기능을 다운로드 하 고 다음 적절 한 버전의 SharePoint 실행 중인 서버에 설치할 수 있는 무료 배포 가능 구성 됩니다.  
  
> [!TIP]  
>  보고서 서버, SharePoint용 Reporting Services 추가 기능 및 SharePoint 제품의 모든 조합에서 모든 기능이 지원되는 것은 아닙니다. 자세한 내용은 참조 하십시오 [지원 되는 SharePoint 및 Reporting Services 서버 및 추가 기능에서 조합은](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)합니다.  
  
-   SharePoint에서 Reporting Services 추가 기능을 제공 ReportServer 프록시 끝점, 보고서 뷰어 웹 파트 및 응용 프로그램 페이지 보기, 저장 및 SharePoint 사이트 또는 팜에서 보고서 서버 내용을 관리할 수 있도록 합니다.  
  
-   Reporting Services에서 업데이트 된 프로그램 파일, SOAP 끝점, 및 사용자 지정 보안 및 배달 확장 프로그램을 제공합니다. 보고서 서버는 SharePoint 사이트를 통해 보고서 액세스와 배달만 전적으로 지원하는 SharePoint 통합 모드에서 실행되도록 구성해야 합니다.  
  
 SharePoint에서 Reporting Services 추가 기능을 설치 하 고 통합을 위해 두 서버를 구성 후 업로드 또는 보고서 서버 콘텐츠 형식을 SharePoint 라이브러리에 게시 하 고 확인 및 SharePoint 사이트에서 해당 문서를 관리 합니다. 보고서 서버 콘텐츠를 게시 또는 업로드 하는 것이 중요 한; 웹 파트와 페이지 보고서 정의 (.rdl)을 선택 하 고 보고서 모델 (.smdl) 공유 데이터 원본 (.rsds) SharePoint 사이트에서 사용할 수 있습니다.  
  
##  <a name="language-considerations"></a>언어 관련 고려 사항

 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 및 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 제품은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 보고서 서버를 SharePoint 제품 배포 내에서 실행되도록 구성하는 경우 여러 언어가 혼합되어 나타날 수 있습니다. 사용자 인터페이스, 설명서 및 메시지는 다음 언어로 표시됩니다.  
  
-   모든 응용 프로그램 페이지, 도구, 오류, 경고 및 Reporting Services에서 생성 된 메시지 중 하나에서 Reporting Services 인스턴스에 의해 사용 되는 언어로 표시 됩니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 언어입니다.  
  
-   응용 프로그램 페이지를 SharePoint 사이트, 보고서 뷰어 웹 파트 및 보고서 작성기에서 열고는 Reporting Services 추가 기능에 대해 지원 되는 언어 중 하나에 표시 됩니다. 지원 되는 언어 목록을 보려면로 이동 [SQL Server 다운로드](http://msdn.microsoft.com/sql/downloads/) 다운로드 페이지에는 SQL Server 2016 Reporting Services 추가 기능을 찾습니다.  
  
-   SharePoint 사이트, SharePoint 중앙 관리, 온라인 도움말 및 메시지는 Office Server 제품에서 지원되는 언어로 제공됩니다.  
  
 SharePoint 제품 또는 기술과의 언어는 보고서 서버 언어와 다른 경우 Reporting Services는 가장 일치 하는 같은 언어군에서 언어를 사용 하려고 합니다. 근접하게 일치하는 대체 언어가 없는 경우 보고서 서버에서는 영어를 사용합니다.  
  
## <a name="related-tasks"></a>관련 작업

 다음 표에서 Reporting Services SharePoint 모드 보고서 서버와 관련 된 작업 요약:  
  
|**태스크**|**링크**|  
|--------------|--------------|  
|설치 및 SharePoint 모드의 Reporting Services를 구성 하는 자세한 단계입니다.|[SharePoint 2010 용 Reporting Services SharePoint 모드 설치](http://msdn.microsoft.com/47efa72e-1735-4387-8485-f8994fb08c8c) 및 [팜에 추가 보고서 서버 추가](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)합니다.|  
|Reporting Services SharePoint 배포 하 여 확장 보고서 서버를 추가 합니다.|[팜에 추가 보고서 서버 추가](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md) 및 [SharePoint의 SQL Server BI 기능의 배포 토폴로지](http://msdn.microsoft.com/library/39f76bc7-94e6-4dbc-bfa5-d56f4430bb26)합니다.|  
|추가 SharePoint 웹 프런트 엔드에 Reporting Services 구성 요소를 설치한 보기 및 보고서 항목에 대 한 추가 합니다.|[팜에 추가 Reporting Services 웹 프런트 엔드 추가](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)|  
|SharePoint 내에서 보고서 서버에 대 한 전자 메일을 구성 합니다.|[Reporting Services 서비스 응용 프로그램에 대 한 전자 메일 구성](../install-windows/configure-e-mail-for-a-reporting-services-service-application.md)|
|TechNet Wiki에 있는 이 릴리스에 대한 최신 정보|[SQL Server 2012 Reporting Services 팁, 요령 및 문제 해결](http://go.microsoft.com/fwlink/?LinkId=221297)합니다.|  

## <a name="next-steps"></a>다음 단계

[설치 또는 SharePoint 용 Reporting Services에 대 한 개의 sdd 제거](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
[보고서 뷰어 웹 파트는 SharePoint 사이트에서](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
[퀴즈: SharePoint 통합을 위한 SSRS 2012 구성](http://go.microsoft.com/fwlink/?LinkId=306443)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
