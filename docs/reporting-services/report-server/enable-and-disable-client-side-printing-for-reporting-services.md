---
title: Reporting Services에 대한 클라이언트 쪽 인쇄 기능 설정 및 해제 | Microsoft Docs
ms.custom: ''
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-server
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- pdf
- viewer
- reportviewer
- toolbar
ms.assetid: 0e709c96-7517-4547-8ef6-5632f8118524
caps.latest.revision: 14
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 54ed6dbd9c8f8a39be49ad9c979431e8666783df
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33028160"
---
# <a name="enable-and-disable-client-side-printing-for-reporting-services"></a>Reporting Services에 대한 클라이언트 쪽 인쇄 기능 설정 및 해제

  보고서 뷰어 도구 모음의 인쇄 단추는 브라우저에 표시된 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서의 클라이언트 쪽 인쇄에 대해 PDF(Portable Document Format) 형식을 사용합니다. 새 원격 인쇄 환경은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에 포함된 PDF 렌더링 확장을 사용하여 보고서를 PDF 형식으로 렌더링합니다. 보고서의 .PDF 형식을 다운로드하거나 .PDF 파일을 볼 수 있는 응용 프로그램이 설치된 경우 인쇄 버튼을 클릭하여 .PDF 파일의 페이지 크기, 방향 및 미리 보기 등과 같은 페이지의 일반적인 구성 항목에 대한 인쇄 대화 상자를 표시할 수 있습니다. 클라이언트 쪽 인쇄 기능은 기본적으로 설정되어 있지만 이 기능을 사용하지 않으려면 해제할 수 있습니다.  
  
 이전 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서는 보고서 서버에서 클라이언트 컴퓨터에 다운로드해야 하는 ActiveX 컨트롤을 사용했습니다. 보고서 서버를 SQL Server 2016으로 업그레이드하는 경우 인쇄 컨트롤이 보고서 서버 또는 클라이언트 컴퓨터에서 제거되지 않습니다.  

##  <a name="bkmk_clientside_printexpereince"></a> 인쇄 환경  
 보고서 뷰어 도구 모음에서 인쇄 ![htmlviewer_print](../../reporting-services/report-server/media/htmlviewer-print.png "htmlviewer_print") 단추를 클릭할 때 환경은 클라이언트 컴퓨터에 설치된 .PDF 보기 응용 프로그램 및 사용 중인 브라우저에 따라 달라집니다.   클라이언트 컴퓨터에 따라 PDF 파일을 다운로드하거나 대화 상자에서 인쇄 옵션을 구성하거나 두 가지를 모두 수행할 수 있습니다.  
  
 ![보고서 도구 모음](../../reporting-services/media/ssrs-htmlviewer-toolbar.png "보고서 도구 모음")  
  
|||  
|-|-|  
|첫 번째 대화 상자는 모든 브라우저에 대해 동일하며 방향과 같은 기본적인 레이아웃 속성을 변경할 수 있습니다. **인쇄**를 클릭할 때 환경은 사용 중인 브라우저에 따라 약간 다릅니다.|![ssrs_pdfprint_chrome1](../../reporting-services/report-server/media/ssrs-pdfprint-chrome1.png "ssrs_pdfprint_chrome1")|  
|Chrome에서는 자세한 브라우저 인쇄 대화 상자가 열립니다.   인쇄 구성을 변경하고, 인쇄하고, 운영 체제 인쇄 대화 상자를 열 수 있습니다.|![ssrs_pdfprint_chrome2](../../reporting-services/report-server/media/ssrs-pdfprint-chrome2.png "ssrs_pdfprint_chrome2") ![ssrs_pdfprint_chrome3.png](../../reporting-services/report-server/media/ssrs-pdfprint-chrome3-png.png "ssrs_pdfprint_chrome3.png")|  
|PDF 판독기 응용 프로그램이 설치된 경우 인쇄 버튼을 클릭하면 PDF 파일의 미리 보기 창이 열리며 해당 파일을 저장하거나 인쇄할 수 있습니다.||  
|PDF 판독기 응용 프로그램이 설치되지 않은 경우 두 가지 사용자 환경이 있습니다.<br /><br /> 보고서가 자동으로 렌더링되며 브라우저 다운로드 프로세스를 사용하여 PDF 파일을 다운로드합니다.   **참고:** 보고서가 복잡할수록 **인쇄** 를 클릭한 후 브라우저 다운로드 알림이 표시될 때까지 지연 시간이 더 길어집니다. 또한 **보고서의 PDF를 보려면 여기를 클릭하세요.** 를 클릭하여 다운로드를 강제로 다시 실행할 수 있습니다.<br /><br /> **보고서의 PDF를 보려면 여기를 클릭하세요.** 를 클릭하여 PDF 다운로드를 강제로 다시 실행합니다.|![ssrs_pdfprint_firefox2](../../reporting-services/report-server/media/ssrs-pdfprint-firefox2.png "ssrs_pdfprint_firefox2")|  
  
##  <a name="bkmk_troubleshoot_clientsideprinting"></a> 클라이언트 쪽 인쇄 문제 해결  
 보고서 뷰어 도구 모음의 인쇄 버튼이 비활성화된 경우 다음을 확인합니다.  
  
-   [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 보고서 서버에 대한 클라이언트 쪽 인쇄 기능이 비활성화되었습니다. 이 항목에서  [클라이언트 쪽 인쇄 사용 및 사용 안 함](#bkmk_enable) 섹션을 참조하세요.  
  
-   [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] PDF 렌더링 확장이 사용하지 않도록 설정되었습니다. `<Extension Name="PDF"` rsreportserver.config **파일의** 섹션을 검토합니다.  
  
-   이전 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] HTML4 렌더링 엔진을 사용하는 비교 가능 모드에서 보고서를 보고 있습니다. PDF 인쇄 환경을 사용하려면 HTML 5 렌더링 엔진이 필요합니다.  도구 모음의 **미리 보기 사용** 버튼을 클릭합니다.  
  
     ![ssrs_html5_switch2html5](../../reporting-services/report-server/media/ssrs-html5-switch2html5.png "ssrs_html5_switch2html5")  
  
##  <a name="bkmk_enable"></a> 클라이언트 쪽 인쇄 사용 및 사용 안 함  
 보고서 서버 관리자는 보고서 서버 시스템 속성인 **EnableClientPrinting** 을 **false**로 설정하여 원격 인쇄 기능을 해제할 수 있습니다. 이렇게 하면 해당 서버에서 관리하는 모든 보고서에 대한 클라이언트 쪽 인쇄 기능이 해제됩니다. 기본적으로 **EnableClientPrinting** 은 **true**로 설정되어 있습니다. 다음과 같은 방법으로 클라이언트 쪽 인쇄 기능을 해제할 수 있습니다.  
  
-   **기본 모드 보고서 서버**:  
  
    1.  관리자 권한으로 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 를 시작합니다.  
  
    2.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 보고서 서버 인스턴스에 연결합니다.  
  
    3.  보고서 서버 노드를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다. **속성** 옵션이 해제되어 있으면 관리자 권한으로 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 를 실행했는지 확인합니다.  
  
    4.  **고급**을 클릭합니다.  
  
    5.  **EnableClientPrinting**을 선택합니다.  
  
    6.  True 또는 False로 설정한 다음 **확인**을 클릭합니다.  
  
         ![ssrs_ssmsproperties_clientprinting](../../reporting-services/report-server/media/ssrs-ssmsproperties-clientprinting.png "ssrs_ssmsproperties_clientprinting")  
  
-   **SharePoint 모드 보고서 서버**:  
  
    1.  SharePoint 중앙 관리에서 **응용 프로그램 관리**를 클릭합니다.  
  
    2.  **서비스 응용 프로그램 관리**를 클릭합니다.  
  
    3.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램의 이름을 클릭하고 SharePoint 리본 메뉴에서 **관리** 를 클릭합니다.  
  
    4.  **시스템 설정**을 클릭합니다.  
  
    5.  **클라이언트 인쇄 사용**을 선택합니다. **클라이언트 인쇄 사용** 옵션은 페이지 아래쪽에 있습니다.  
  
    6.  **확인**을 클릭합니다.  
  
-   보고서 서버 시스템 속성 **EnableClientPrinting** 을 **false.** 로 설정하는 스크립트나 코드를 작성합니다.  
  
 다음 예제 스크립트에서는 클라이언트 쪽 인쇄 기능을 해제하는 한 가지 방법을 보여 줍니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 속성을 **EnableClientPrinting** 로 설정하려면 다음 **False**를 클릭하여 다운로드를 강제로 다시 실행할 수 있습니다. 코드를 실행한 후에는 IIS를 다시 시작합니다.  
  
### <a name="sample-script"></a>예제 스크립트  
  
```  
Imports System  
Imports System.Web.Services.Protocols  
Class Sample  
   Public Shared Sub Main()  
Dim rs As New ReportingService()  
      rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
        Dim props(0) As [Property]  
        Dim setProp As New [Property]  
        setProp.Name = "EnableClientPrinting"  
        setProp.Value = “False”   
        props(0) = setProp  
        Try  
            rs.SetSystemProperties(props)  
        Catch ex As System.Web.Services.Protocols.SoapException  
            Console.Write(ex.Detail.InnerXml)  
        Catch e as Exception  
            Console.Write(e.Message)  
        End Try  
    End Sub 'Main  
End Class 'Sample  
```

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
