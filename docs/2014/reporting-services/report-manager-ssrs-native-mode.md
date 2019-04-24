---
title: 보고서 관리자 (SSRS 기본 모드) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], managing
- Report Manager [Reporting Services], about Report Manager
- customizing Report Manager
- Report Manager [Reporting Services], customizing
- report servers [Reporting Services], administering
- browsing reports [Reporting Services]
- administering reports
- Report Manager [Reporting Services]
- components [Reporting Services], Report Manager
ms.assetid: 80949f9d-58f5-48e3-9342-9e9bf4e57896
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 31e64dfe871fa38daee266814006468a8ea32e65
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59940669"
---
# <a name="report-manager--ssrs-native-mode"></a>보고서 관리자(SSRS 기본 모드)
  보고서 관리자는 HTTP 연결을 통해 원격 위치의 단일 보고서 서버 인스턴스를 관리하는 데 사용되는 웹 기반 보고서 액세스 및 관리 도구입니다. 또한 보고서 관리자를 보고서 뷰어로 사용하고 탐색 기능도 활용할 수 있습니다. 항목 내용  
  
-   [보고서 관리자란?](#bkmk_whatis_report_manager)  
  
-   [시작 및 보고서 관리자를 사용 하 여](#bkmk_start_report_manager)  
  
-   [아이콘 설명](#bkmk_icon_descriptions)  
  
##  <a name="bkmk_whatis_report_manager"></a> 보고서 관리자란?  
 보고서 관리자를 사용하여 다음 태스크를 수행할 수 있습니다.  
  
-   보고서 보기, 검색, 인쇄 및 구독  
  
-   서버의 항목을 체계적으로 구성하도록 폴더 계층 구조 생성, 보안 설정 및 유지 관리  
  
-   항목 및 작업에 대한 액세스 권한을 결정하는 역할 기반 보안 구성  
  
-   보고서 실행 속성, 보고서 기록 및 보고서 매개 변수 구성  
  
-    [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터 원본 또는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 관계형 데이터 원본의 데이터에 연결하고 데이터를 검색하는 보고서 모델 만들기  
  
-   모델의 특정 엔터티에 대한 액세스를 허용하도록 모델 항목 보안 설정 또는 미리 정의된 클릭 광고 보고서에 엔터티 매핑  
  
-   일정 및 데이터 원본 연결을 편리하게 관리하기 위해 공유 일정 및 공유 데이터 원본 만들기  
  
-   대규모 받는 사람 목록에 보고서를 전달하는 데이터 기반 구독 만들기  
  
-   기존 보고서를 다른 방식으로 다시 사용하고 용도를 변경하기 위해 링크된 보고서 만들기  
  
-   보고서 서버에서 저장하고 실행할 수 있는 보고서를 만들기 위해 보고서 작성기 시작  
  
 보고서 관리자를 사용하여 보고서 서버 폴더를 찾아보거나 특정 보고서를 검색할 수 있습니다. 보고서, 해당 일반 속성 및 보고서 기록에 캡처된 보고서의 지난 복사본을 볼 수 있습니다. 권한에 따라 보고서를 구독하여 전자 메일 받은 편지함 또는 파일 시스템의 공유 폴더로 배달되도록 할 수도 있습니다.  
  
> [!NOTE]  
>  지원 되는 브라우저 및 버전에 대 한 내용은 참조 하세요 [Reporting Services 및 파워 뷰 브라우저 지원 계획 &#40;Reporting Services 2014&#41;](../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md)합니다.  
  
 보고서 관리자는 기본 모드로 실행되는 보고서 서버에만 사용되며 SharePoint 통합 모드용으로 구성된 보고서 서버에 대해서는 지원되지 않습니다.  
  
 일부 보고서 관리자 기능은 지정된 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]버전에서만 사용할 수 있습니다. 자세한 내용은 [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)을 참조하세요.  
  
 새로 설치하는 경우 로컬 관리자에게만 내용 및 설정을 사용할 수 있는 권한이 부여됩니다. 다른 사용자에게 사용 권한을 부여하려면 로컬 관리자가 보고서 서버에 대한 액세스 권한을 제공하는 역할 할당을 만들어야 합니다. 사용자가 이후에 액세스할 수 있는 애플리케이션 페이지 및 태스크는 해당 사용자에 대한 역할 할당에 따라 달라집니다. 자세한 내용은 [사용자에게 보고서 서버에 대한 액세스 권한 부여&#40;보고서 관리자&#41;](security/grant-user-access-to-a-report-server.md)를 참조하세요.  
  
 [!INCLUDE[wiprlhlong](../includes/wiprlhlong-md.md)] 또는 Windows Server 2008을 사용하는 경우 로컬 관리용으로 보고서 관리자를 구성해야 합니다. 자세한 내용은 [로컬 관리에 대해 기본 모드 보고서 서버 구성&#40;SSRS&#41;](report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)을 참조하세요.  
  
##  <a name="bkmk_start_report_manager"></a> 시작 및 보고서 관리자를 사용 하 여  
 보고서 관리자는 브라우저 창의 주소 표시줄에 보고서 관리자 URL을 입력하면 열리는 웹 애플리케이션입니다. 보고서 서버에 대해 가지고 있는 권한에 따라 보고서 관리자를 시작할 때 표시되는 페이지, 링크 및 옵션이 달라집니다. 특정 태스크를 수행하기 위해서는 해당 태스크를 포함하는 역할이 할당되어야 합니다. 모든 권한이 있는 역할이 할당된 사용자는 보고서 서버를 관리하는 데 사용할 수 있는 애플리케이션의 모든 메뉴와 페이지에 액세스할 수 있습니다. 그러나 보고서를 보고 실행할 수 있는 권한이 있는 역할이 할당된 사용자는 이러한 작업을 지원하는 메뉴와 페이지만 볼 수 있습니다. 각 사용자는 각 보고서 서버에 대해 다른 역할을 할당 받을 수 있으며, 단일 보고서 서버에 저장된 여러 보고서 및 폴더에 대해서도 각기 다른 역할을 할당 받을 수 있습니다.  
  
 역할에 대해 자세히 알아보려면 [기본 모드 보고서 서버에 대한 사용 권한 부여](security/granting-permissions-on-a-native-mode-report-server.md)를 참조하십시오.  
  
> [!NOTE]  
>  Windows Vista 또는 Windows Server 2008을 사용하는 경우 보고서 관리자에서 로컬 보고서 서버 인스턴스를 관리하려면 먼저 로컬 관리용으로 보고서 서버를 구성해야 합니다. 서버를 구성 하는 방법에 지침은 [로컬 관리를 위한 기본 모드 보고서 서버 구성 &#40;SSRS&#41;](report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)합니다.  
  
## <a name="start-report-manager"></a>보고서 관리자 시작  
  
#### <a name="to-start-report-manager-from-a-browser"></a>브라우저에서 보고서 관리자를 시작하려면  
  
1.  [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Explorer 7.0 이상을 엽니다.  
  
2.  웹 브라우저의 주소 표시줄에 보고서 관리자 URL을 입력합니다.  
  
    -   기본적으로 URL은 `http://[ComputerName]/reports`입니다.  
  
    -   특정 포트를 사용하도록 보고서 서버를 구성할 수 있습니다. 예를 들어 `http:// [ComputerName]:80/reports` 또는 `http:// [ComputerName]:8080/reports`입니다.  
  
## <a name="configuring-report-manager"></a>보고서 관리자 구성  
 보고서 관리자 구성은 애플리케이션 URL을 정의하는 작업으로 구성됩니다. 별도의 컴퓨터에서 배포가 실행 중인 보고서 관리자를 포함하는 경우에는 추가 구성이 필요합니다.  
  
 보고서 관리자의 사용자 지정 범위는 상당히 제한되어 있습니다. 예를 들면 사이트 설정 페이지에서 애플리케이션 제목을 수정할 수 있습니다. 웹 개발자인 경우 보고서 관리자에 사용되는 스타일 정보가 들어 있는 스타일시트를 수정할 수 있습니다. 보고서 관리자는 사용자 지정을 지원하도록 특수하게 디자인되지 않았으므로 수정한 사항을 철저히 테스트해야 합니다. 보고서 관리자로 원하는 작업을 수행할 수 없으면 사용자 지정 보고서 뷰어를 개발하거나 SharePoint 사이트에서 보고서를 찾고 확인할 수 있도록 SharePoint 웹 파트를 구성할 수 있습니다. 자세한 내용은 [보고서 관리자 구성&#40;기본 모드&#41;](report-server/configure-web-portal.md)을 참조하세요.  
  
##  <a name="bkmk_icon_descriptions"></a> 아이콘 설명  
 다음 표에서는 보고서 관리자에 사용되는 아이콘에 대해 설명합니다. 보고서 도구 모음에 표시 되는 아이콘에 대 한 자세한 내용은 참조 하세요. [HTML 뷰어 및 보고서 도구 모음](html-viewer-and-the-report-toolbar.md)합니다.  
  
|아이콘|Description|작업|  
|----------|-----------------|------------|  
|![보고서 아이콘](media/hlp-16doc.gif "보고서 아이콘")|보고서|보고서 아이콘 또는 이름을 클릭하여 보고서를 엽니다. 보고서가 별도의 창으로 열립니다.|  
|![모델 아이콘](media/model-icon.gif "모델 아이콘")|보고서 모델|모델 속성 페이지를 열려면 보고서 모델 아이콘을 클릭합니다.|  
|![링크된 보고서 아이콘](media/hlp-16linked.gif "링크된 보고서 아이콘")|링크된 보고서|보고서 아이콘 또는 이름을 클릭하여 링크된 보고서를 엽니다. 보고서가 별도의 창으로 열립니다.|  
|![폴더 아이콘](media/hlp-16folder.gif "폴더 아이콘")|Folder|폴더 아이콘 또는 이름을 클릭하여 폴더를 엽니다.|  
|![구독 아이콘](media/hlp-16subscription.gif "구독 아이콘")|구독|구독 아이콘 또는 설명을 클릭하여 구독을 편집합니다.|  
|![데이터 기반 구독 아이콘](media/hlp-16subscriptiondd.gif "데이터 기반 구독 아이콘")|데이터 기반 구독|데이터 기반 구독 아이콘 또는 설명을 클릭하여 구독을 편집합니다.|  
|![일반 리소스 아이콘](media/hlp-16file.gif "일반 리소스 아이콘")|리소스|리소스 아이콘 또는 이름을 클릭하여 리소스를 엽니다. 리소스가 별도의 창으로 열립니다.|  
|![공유 데이터 원본 아이콘](media/hlp-16datasource.png "공유 데이터 원본 아이콘")|공유 데이터 원본 항목|공유 데이터 원본 아이콘을 클릭하여 데이터 원본의 속성 페이지, 보고서 목록 및 구독 목록을 엽니다.|  
|![속성 페이지 아이콘](media/hlp-16prop.gif "속성 페이지 아이콘")|속성 페이지|속성 아이콘을 클릭하여 속성 및 보안을 설정할 수 있는 추가 페이지에 액세스합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [URL 구성&#40;SSRS 구성 관리자&#41;](install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [Reporting Services 및 파워 뷰 브라우저 지원 계획 &#40;Reporting Services 2014&#41;](../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md)   
 [보고서 작성기 &#40;SSRS&#41;](tools/report-builder-authoring-environment-ssrs.md)   
 [Reporting Services 도구](tools/reporting-services-tools.md)   
 [보고서 서버 콘텐츠 관리&#40;SSRS 기본 모드&#41;](report-server/report-server-content-management-ssrs-native-mode.md)   
 [SharePoint 웹 파트를 사용 하 여 기본 모드 보고서 보기 및 탐색 &#40;SSRS&#41;](reports/view-and-explore-native-mode-reports-using-sharepoint-web-parts-ssrs.md)   
 [보고서 관리자 F1 도움말](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
