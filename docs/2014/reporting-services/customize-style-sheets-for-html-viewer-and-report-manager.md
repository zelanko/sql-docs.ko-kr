---
title: HTML 뷰어 및 보고서 관리자 스타일 시트 사용자 지정 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- style sheets [Reporting Services]
ms.assetid: df805cff-b1de-4062-b2ac-423f37390fbd
caps.latest.revision: 18
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 6baf2dbbb100711b9665d5d705bce6399e3c754b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37192933"
---
# <a name="customize-style-sheets-for-html-viewer-and-report-manager"></a>HTML 뷰어 및 보고서 관리자에 대한 스타일시트 사용자 지정
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 기본 연계 스타일 시트 파일 (.css) 스타일을 정의 하는 제공 된 **보고서** HTML 뷰어 및 보고서 관리자 도구 모음입니다. 웹 개발자나 CSS 스타일시트 파일을 만드는 전문가인 경우 기본 스타일을 수정하여 도구 모음이나 보고서 관리자의 색, 글꼴 및 레이아웃을 변경할 수 있습니다. 단, 이로 인해 발생하는 모든 문제에 대한 책임은 자신에게 있습니다. 이 릴리스에서는 기본 스타일시트나 스타일시트 수정 지침을 다루지 않습니다.  
  
 스타일시트를 잘못 수정하면 보고서를 열 때 오류가 발생할 수 있습니다. 스타일시트를 수정하는 방법을 모르는 경우 기본 스타일시트를 사용해야 합니다. 스타일시트를 사용자 지정하려는 경우 수정하기 전에 모든 기본 .css 파일의 백업을 만드십시오.  
  
 스타일시트를 수정해도 보고서 서버에서 실행되는 게시된 보고서의 모양에는 영향을 주지 않습니다. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서 보고서는 스타일시트를 참조하지 않습니다. 보고서 서버에서 자동으로 생성하는 임시 보고서는 보고서 서버 프로그램 파일에 포함 리소스로 저장되어 있는 스타일 정보를 사용합니다. 보고서 디자이너에서 만드는 보고서는 보고서 정의에서 지정하는 글꼴, 색 및 레이아웃을 사용합니다. 스타일은 나머지 레이아웃과 인라인으로 만들어집니다.  
  
> [!NOTE]  
>  미리 정의된 보고서 스타일을 사용하려는 경우 보고서 마법사를 사용하여 보고서를 만듭니다. 보고서 마법사는 서로 다른 색 조합과 글꼴을 사용하도록 스타일이 지정된 보고서를 만드는 데 사용할 수 있는 다양한 테마를 제공합니다. 보고서의 테마를 정의하는 스타일 템플릿은 수정할 수 있습니다.  
  
## <a name="reporting-services-style-sheets"></a>Reporting Services 스타일시트  
 다음 표에서 설명에 사용 되는 스타일 시트 (.css) 파일을 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 설치 합니다.  
  
|스타일시트|Description|  
|-----------------|-----------------|  
|Htmlviewer.css|HTML 뷰어의 **보고서** 도구 모음에 대한 사용자 지정 스타일을 만드는 데 템플릿으로 사용할 수 있는 예제 스타일시트를 제공합니다.<br /><br /> HTML 뷰어에서 사용하는 기본 스타일은 보고서 서버로 컴파일됩니다. Htmlviewer.css 파일은 뷰어가 사용하는 스타일 예제를 제공합니다.|  
|ReportingServices.css|보고서 관리자의 스타일을 정의합니다.|  
  
> [!NOTE]  
>  Sql.css와 Mailto.css 스타일시트는 보고서 관리자 온라인 설명서에서 사용되므로 수정해서는 안 됩니다. 다른 스타일시트는 SharePoint 웹 파트에서 열리는 보고서와 보고서 관리자에 대한 스타일을 정의합니다. 이러한 스타일시트에는 Rswebparts.css, Sp_full.css 및 Sp_small.css 등이 있습니다. SharePoint 스타일 시트는 수정하지 않는 것이 좋습니다. 웹 파트를 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [보기 및 탐색 기본 모드 보고서를 사용 하 여 SharePoint 웹 파트 &#40;SSRS&#41;](reports/view-and-explore-native-mode-reports-using-sharepoint-web-parts-ssrs.md)합니다.  
  
## <a name="configuring-reporting-services-to-use-a-custom-style-sheet"></a>사용자 지정 스타일시트를 사용하도록 Reporting Services 구성  
 스타일시트는 유효한 CSS 스타일시트 파일(.css)이어야 하며 Styles 폴더에 있어야 합니다. 기본적으로 Styles 폴더에 위치한 \< *드라이브*>: \Program Files\Microsoft SQL Server\MSSQL. *n*\Reporting Services\ReportServer\Styles 합니다.  
  
 런타임에 HTML 뷰어의 사용자 지정 스타일시트를 사용하려면 다음 방법 중에서 선택합니다.  
  
-   <`HTMLViewerStyleSheet`> 설정을 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 구성 파일에 추가합니다.  
  
-   보고서 URL의 스타일시트를 지정합니다.  
  
### <a name="modifying-the-rsreportserverconfig-file"></a>RSReportServer.config 파일 수정  
 RSReportServer.config 파일을 수정하여 HTML 뷰어의 사용자 지정 스타일시트를 지정할 수 있습니다. <`HTMLViewerStyleSheet`> 설정은 기본적으로 파일에 포함되어 있지 않습니다. 따라서 RSReportServer.config 파일의 <`Configuration`> 선택 사항에 직접 입력한 다음 사용하려는 스타일시트를 지정해야 합니다. 스타일시트를 지정할 때 .css 파일 확장명은 포함하지 마십시오.  
  
 다음 예에서는 스타일시트를 지정하는 방법을 보여 줍니다.  
  
```  
<Configuration>  
...  
          <HTMLViewerStyleSheet>MyStyleSheet</HTMLViewerStyleSheet>  
...  
</Configuration>  
```  
  
### <a name="specifying-a-style-sheet-on-a-report-url"></a>보고서 URL의 스타일시트 지정  
 `rc:StyleSheet` URL 액세스 매개 변수를 사용하여 보고서 URL에 대한 사용자 지정 스타일시트를 지정할 수 있습니다. URL 액세스 매개 변수를 지정 하는 방법에 대 한 자세한 내용은 참조 하세요. [URL Access Parameter Reference](url-access-parameter-reference.md)합니다.  
  
 다음 예에서는 사용자 지정 스타일을 추가하는 방법을 보여 줍니다.  
  
```  
http://localhost/reportserver?/AdventureWorksSampleReports/Product+Line+Sales&rs:Command=Render&rc:Stylesheet=MyStyleSheet  
```  
  
## <a name="see-also"></a>관련 항목  
 [보고서 관리자 &#40;SSRS 기본 모드&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [HTML 뷰어 및 보고서 도구 모음](html-viewer-and-the-report-toolbar.md)   
 [RSReportServer 구성 파일](report-server/rsreportserver-config-configuration-file.md)  
  
  
