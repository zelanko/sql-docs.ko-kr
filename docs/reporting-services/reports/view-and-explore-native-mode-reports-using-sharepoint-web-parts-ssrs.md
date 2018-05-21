---
title: SharePoint 웹 파트를 사용하여 기본 모드 보고서 보기 및 탐색(SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: reports
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: dee8ee42-156b-43b6-b202-02dfb9404284
caps.latest.revision: 9
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 1072350a30a5f28ac16cda48f72720a383012d02
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="view-and-explore-native-mode-reports-using-sharepoint-web-parts-ssrs"></a>SharePoint 웹 파트를 사용하여 기본 모드 보고서 보기 및 탐색(SSRS)

> [!IMPORTANT]  
>  SQL Server Reporting Services는 더 이상 기본 모드(RSWebParts.cab) 웹 파트를 사용하여 기본 모드 보고서 서버에서 SharePoint 사이트의 보고서 서버 내용에 액세스할 수 없습니다. 대신 [SharePoint 사이트의 보고서 뷰어 웹 파트](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md) 를 사용합니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 특정 버전의 보고서 서버 및 배포 모드에서 작동하는 다양한 웹 파트를 제공합니다.  
  
-   **기본 모드:** 기본 모드 보고서 서버에서 SharePoint 사이트의 보고서 서버 내용에 액세스하려면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에 포함되어 있는 SharePoint 2.0 웹 파트 보고서 탐색기 및 보고서 뷰어를 사용합니다. 2.0 웹 파트를 설치하고 사용하는 방법은 이 항목에 제공되어 있습니다.  
  
-   **SharePoint 모드:** SharePoint 모드에서 실행되는 보고서 서버에 액세스하려면 SharePoint 제품에 대해 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능으로 설치된 웹 파트를 사용합니다. 추가 기능 다운로드에 대한 자세한 내용은 [SharePoint 제품용 Reporting Services 추가 기능 검색 위치](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)를 참조하세요.  
  
> [!NOTE]  
>  기본 모드의 보고서 뷰어 웹 파트(SPViewer.dwp)는 SharePoint 제품용 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능으로 설치된 웹 파트(ReportViewer.dwp)와 다른 웹 파트입니다. 웹 파트는 스키마 및 구현이 서로 다르지만 이를 모두 동일한 SharePoint 팜에 설치할 수 있습니다. 추가 기능을 통해 설치되는 보고서 뷰어 웹 파트의 도구 모음에는 **동작** 메뉴가 있으므로 이러한 시각적 특징을 통해 두 웹 파트를 구분할 수 있습니다.  
  
 보고서 서버 모드에 대한 자세한 내용은 [Reporting Services 보고서 서버](../../reporting-services/report-server-sharepoint/reporting-services-report-server.md)를 참조하세요.  
  
 항목 내용  
  
-   [보고서 탐색기 및 보고서 뷰어 정보](#bkmk_aboutwebparts)  
  
-   [웹 파트 사용을 위한 요구 사항](#bkmk_requirements)  
  
-   [웹 파트 설치](#bkmk_installingwebparts)  
  
-   [웹 파트 추가 및 구성](#bkmk_configurewebparts)  
  
##  <a name="bkmk_aboutwebparts"></a> 보고서 탐색기 및 보고서 뷰어 정보  
 보고서 탐색기와 보고서 뷰어는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2000 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SP2(서비스 팩 2)에서 도입되어 현재 릴리스에서도 계속 사용할 수 있는 SharePoint 2.0 웹 파트입니다.  
  
 웹 파트를 사용하면 SharePoint 사이트에서 보고서를 보고 보고서 서버 폴더 계층을 탐색할 수 있습니다.  
  
 웹 파트는 사용자 지정할 수 없습니다. 웹 파트는 있는 그대로 사용하도록 제작되었으므로 확장하거나 수정하면 안 됩니다.  
  
-   **보고서 탐색기** (SPExplorer.dwp)는 보고서 서버 컴퓨터의 보고서 관리자에 연결합니다. 보고서 서버에서 사용 가능한 보고서를 찾아보고 개별 보고서를 구독할 수 있습니다. 보고서 작성기를 사용하며 충분한 사용 권한이 있으면 보고서 탐색기 웹 파트에서 보고서 작성기를 시작할 수 있습니다.  
  
     보고서 탐색기는 보고서 관리자의 페이지를 사용하여 폴더 내용을 표시합니다. 전체 보고서 서버 폴더 계층의 개별 항목 및 폴더에 대한 액세스는 보고서 서버의 역할 할당을 통해 제어됩니다. 보고서를 선택하면 해당 보고서가 새 브라우저 창에서 열립니다. 보고서 서버의 HTML 뷰어는 보고서를 표시하고 보고서 뷰어 웹 파트 대신 보고서 도구 모음을 제공합니다. 도구 모음 설정을 사용자 지정하려면 보고서 서버에서 URL 액세스 매개 변수를 지정해야 합니다. 자세한 내용은 [URL 액세스 매개 변수 참조](../../reporting-services/url-access-parameter-reference.md)를 참조하세요.  
  
-   **보고서 뷰어** (SPViewer.dwp)는 보고서를 표시하고 페이지 탐색, 내용 검색 또는 보고서 내보내기에 사용할 수 있는 도구 모음을 제공합니다. 보고서 뷰어 웹 파트를 웹 파트 페이지에 추가하여 해당 페이지에 항상 특정 보고서가 표시되도록 하거나 **보고서 탐색기에 연결하여** 해당 웹 파트를 통해 열리는 보고서를 표시할 수 있습니다.  
  
##  <a name="bkmk_requirements"></a> 웹 파트 사용을 위한 요구 사항  
 보고서 뷰어 웹 파트와 보고서 탐색기 웹 파트를 사용하기 위한 요구 사항은 다음과 같습니다.  
  
-   지원되는 SharePoint 제품 및 기술 버전에는  
  
    -   [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3.0 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007이 있습니다.  
  
    -   [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 및 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]입니다.  
  
-   기본 모드 보고서 서버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 이상 버전이어야 합니다.  
  
-   보고서 서버는 기본 모드로 실행되어야 합니다. 보고서 탐색기 및 보고서 뷰어 웹 파트를 사용하여 SharePoint 모드로 실행되는 보고서 서버에 연결하거나 이 서버의 보고서를 볼 수는 **없습니다** .  
  
-   보고서 관리자가 설치되어 있어야 합니다.  
  
 보고서 탐색기 웹 파트와 보고서 뷰어 웹 파트는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에 포함된 캐비닛 파일(.cab)을 통해 배포됩니다. 웹 파트 설치, 구성 및 사용 방법은 이 항목의 다음 섹션에 제공되어 있습니다.  
  
##  <a name="bkmk_installingwebparts"></a> 웹 파트 설치  
 웹 파트는 SharePoint 서버에 캐비닛 파일(.cab)로 전달됩니다. 명령줄에서 .cab 파일에 대해 SharePoint Stsadm.exe 도구를 실행하여 웹 파트를 설치합니다. 이 도구 및 웹 파트 배포에 대한 자세한 내용은 SharePoint 설명서를 참조하세요.  
  
#### <a name="install-web-parts-using-powershell"></a>Powershell을 사용하여 웹 파트 설치  
  
1.  **RSWebParts.cab** 를 SharePoint 서버의 폴더로 복사합니다. 이 파일을 SharePoint 서버에 있는 임의의 폴더로 복사한 다음 웹 파트를 설치한 후 삭제할 수 있습니다. 기본적으로 SQL Server 2014 Reporting Services 및 이전 버전에서는 다음 폴더에 RSWebParts.cab 파일을 설치합니다.  
  
    ```  
    C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Reporting Services\SharePoint  
    ```  
  
2.  SharePoint 제품이 설치된 컴퓨터에서 **관리 권한** 으로 **SharePoint 2010 관리 셸**을 엽니다.  
  
3.  다음 PowerShell 명령을 실행합니다.  
  
    ```  
    Install-SPWebPartPack -LiteralPath "C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Reporting Services\SharePoint\RSWebParts.cab" -GlobalInstall  
    ```  
  
4.  웹 파트가 배포되었음을 나타내는 다음과 비슷한 메시지가 표시됩니다.  
  
    > Name               SolutionId                                             Deployed  
  
    > ----                  ----------                                              -------\-  
  
    > rswebparts.cab    00000000-0000-0000-0000-000000000000     True  
  
     PowerShell 사용에 대한 자세한 내용은 [Install-SPWebPartPack(http://technet.microsoft.com/library/ff607840.aspx)](http://technet.microsoft.com/library/ff607840.aspx)을 참조합니다.  
  
#### <a name="install-web-parts-using-stsadmexe"></a>STSADM.exe를 사용하여 웹 파트 설치  
  
1.  이 문서의 PowerShell 세션에 설명된 대로 SharePoint 서버의 동일 위치에 **RSWebParts.cab** 파일을 복사합니다.  
  
2.  SharePoint 제품 또는 기술이 설치되어 있는 컴퓨터에서 관리 권한으로 명령 프롬프트 창을 열고 **Stsadm.exe** 도구가 있는 폴더로 이동합니다. [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 에 대한 기본 경로는 다음과 같습니다.  
  
    > C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\14\BIN.  
  
3.  다음 구문을 사용하여 .cab에 대해 Stsadm.exe를 실행합니다.  
  
    ```  
    STSADM.EXE -o addwppack -filename "C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Reporting Services\SharePoint\RSWebParts.cab" -globalinstall  
    ```  
  
4.  "작업이 완료 되었습니다." 메시지가 나타납니다.  
  
     `-globalinstall` 을 지정하면 웹 파트가 GAC(전역 어셈블리 캐시)에 추가됩니다. 이 단계는 웹 파트를 연결하려는 경우 필요합니다.  
  
##  <a name="bkmk_configurewebparts"></a> 웹 파트 추가 및 구성  
 웹 파트를 설치한 후 SharePoint 사이트에서 하나 이상의 웹 페이지에 웹 파트를 추가할 수 있습니다. 이때 웹 사이트를 만들고 내용을 추가할 수 있는 권한이 있어야 합니다.  
  
 다음 절차에서는 페이지에 두 웹 파트를 추가한 후 보고서 탐색기 및 보고서 뷰어를 함께 연결하여 보고서 탐색기에서 보고서를 클릭할 때 보고서가 보고서 뷰어 내에 표시됩니다.  
  
#### <a name="add-report-viewer"></a>보고서 뷰어 추가  
  
1.  사이트 동작에서 **페이지 편집**을 클릭합니다.  
  
2.  페이지의 한 영역에서 **웹 파트 추가**를 클릭합니다.  
  
3.  **웹 파트 추가** 대화 상자에서 아래쪽의 **기타** 범주로 스크롤합니다.  
  
4.  **보고서 뷰어**를 선택합니다.  
  
    > [!WARNING]  
    >  **SQL Server Reporting Services 보고서 뷰어** 를 선택하지 마세요. 이 웹 파트는 SharePoint 제품용 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능을 설치할 때 등록되며 SharePoint 모드에서 보고서 서버를 실행하기 위해 사용됩니다. 기본 모드 보고서 서버의 보고서를 보는 데에는 사용할 수 없습니다.  
  
5.  **추가**를 클릭합니다.  
  
6.  페이지가 편집 모드에 있는 동안 보고서 뷰어 웹 파트에서 **웹 파트 편집** 을 클릭합니다.  
  
7.  **보고서 관리자 URL**에 액세스할 기본 모드 보고서 서버에 연결된 보고서 관리자 인스턴스의 URL을 입력합니다. 기본적으로 보고서 관리자 URL의 구문은 **http://\<servername>/reports**입니다.  
  
8.  **보고서 경로**에 슬래시를 지정하고 그 뒤에 폴더 경로와 보고서 이름을 지정합니다. 이때 서버 이름이나 보고서 관리자 가상 디렉터리는 포함하지 **마세요** . 예를 들어 Adventure Works 폴더에 있는 'Company Sales' 보고서를 열려면 **/Adventure Works/Company Sales**를 지정합니다. 다음은 '제품' 보고서가 보고서 서버 루트 폴더인 **/Products**에 있는 또 다른 예입니다.  
  
9. **확인**을 클릭합니다.  
  
#### <a name="add-report-explorer-and-connect-to-report-viewer"></a>보고서 탐색기 추가 및 보고서 뷰어에 연결  
  
1.  페이지의 다른 영역에서 **웹 파트 추가** 를 클릭하고 miscellaneous 폴더에서 **보고서 탐색기** 를 클릭한 후 **추가**를 클릭합니다.  
  
2.  보고서 탐색기 웹 파트 상황별 메뉴에서 **웹 파트 편집**을 클릭합니다.  
  
3.  **보고서 관리자 URL**에 액세스할 기본 모드 보고서 서버에 연결된 보고서 관리자 인스턴스의 URL을 입력합니다.  
  
4.  필요에 따라 **시작 경로**를 설정합니다. 시작 경로는 보고서 서버 폴더 계층의 폴더입니다. 기본 페이지를 폴더 계층에서 보다 하위 수준에 속하는 폴더로 설정하려면 시작 경로를 지정합니다. 경로는 슬래시로 시작해야 합니다. 보고서 서버 폴더 계층의 루트 노드로 시작하지만 서버 이름이나 보고서 관리자 가상 디렉터리를 포함하지 않는 전체 경로를 지정해야 합니다. 예를 들어 루트 노드 바로 아래에 있는 Adventure Works라는 폴더를 열려면 시작 경로에 **/Adventure Works** 를 지정합니다.  
  
5.  **확인**을 클릭합니다.  
  
6.  보고서 탐색기에 보고서 서버의 보고서 항목 목록이 표시됩니다. 기본적으로 보고서 이름을 클릭하면 보고서가 새 창으로 열립니다. 보고서 탐색기에서 보고서 이름을 클릭할 때 보고서가 보고서 뷰어에 표시되도록 보고서 탐색기에서 보고서 뷰어로 연결하려는 경우 다음 단계를 수행합니다.  
  
    1.  보고서 탐색기 상황별 메뉴에서 **연결**을 클릭합니다.  
  
    2.  **보고서 표시 위치**를 클릭합니다.  
  
    3.  **보고서 뷰어**를 클릭합니다.  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
