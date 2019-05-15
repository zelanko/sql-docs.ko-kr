---
title: HTML 뷰어 및 보고서 도구 모음 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- HTML Viewer [Reporting Services]
- report toolbar [Reporting Services]
ms.assetid: cd86b319-babd-45af-a6a4-f659fdcc40c3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 948abaaae630de34f4340370fd2f6f0f4e0a1d34
ms.sourcegitcommit: e4794943ea6d2580174d42275185e58166984f8c
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65503071"
---
# <a name="html-viewer-and-the-report-toolbar"></a>HTML 뷰어 및 보고서 도구 모음
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 는 보고서 서버의 요청에 따라 보고서를 표시하는 데 사용되는 HTML 뷰어를 제공합니다. HTML 뷰어는 HTML 형식의 보고서를 표시하는 프레임워크, 즉 보고서 도구 모음, 매개 변수 섹션, 자격 증명 섹션 및 문서 구조를 제공합니다. HTML 뷰어의 보고서 도구 모음에는 보고서를 HTML이 아닌 다른 형식으로 표시할 수 있도록 하는 내보내기 옵션을 비롯하여 보고서 작업에 사용할 수 있는 다양한 기능이 있습니다. 매개 변수 섹션과 문서 구조는 매개 변수 및 문서 구조 컨트롤을 사용하도록 구성된 보고서를 열 경우에만 표시됩니다.  
  
 보고서 도구 모음을 수정할 수는 없지만 보고서 URL의 매개 변수를 구성하여 보고서에서 보고서 도구 모음을 숨길 수 있습니다. 보고서 도구 모음을 숨기는 방법은 [URL 액세스 매개 변수 참조](../reporting-services/url-access-parameter-reference.md)를 참조하세요.  
  
## <a name="report-toolbar"></a>보고서 도구 모음  
 보고서 도구 모음은 HTML 렌더링 확장 프로그램에서 렌더링된 보고서에 대해 페이지 탐색, 확대/축소, 새로 고침, 검색, 내보내기, 인쇄 및 데이터 피드 기능을 제공합니다.  
  
 인쇄 기능은 선택 사항입니다. 인쇄 기능을 사용할 수 있는 경우 프린터 아이콘이 보고서 도구 모음에 표시됩니다. 인쇄 기능을 처음 사용하는 경우 프린터 아이콘을 클릭하면 반드시 설치해야 하는 ActiveX 컨트롤이 다운로드됩니다. 컨트롤이 설치된 후에 프린터 아이콘을 클릭하면 컴퓨터에 구성된 프린터 중에서 선택할 수 있는 프린터 대화 상자가 열립니다. 인쇄 기능 사용 가능 여부는 서버 설정 및 브라우저 설정에 따라 결정됩니다. 자세한 내용은 [인쇄 컨트롤을 사용하여 브라우저에서 보고서 인쇄&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-builder/print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md) 및 [Reporting Services에 대한 클라이언트 쪽 인쇄 기능 설정 및 해제](../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)를 참조하세요.  
  
 보고서 도구 모음은 다음 그림과 같습니다. 그러나 실제 보고서 도구 모음은 사용할 수 있는 보고서 기능이나 렌더링 옵션에 따라 다를 수 있습니다.  
  
 ![Report toolbar](../reporting-services/media/ssrs-htmlviewer-toolbar.png "Report toolbar")  
  
 다음 표에서는 일반적으로 사용되는 보고서 도구 모음 기능을 설명합니다. 각 기능은 해당 기능을 액세스하는 데 사용하는 컨트롤로 구분됩니다.  
  
|아이콘 또는 컨트롤||수행할 작업|  
|------------------------------|-|--------|  
|![페이지 이동 컨트롤](../reporting-services/media/htmlviewer-pagenav.gif "페이지 이동 컨트롤")|**페이지 이동 컨트롤**|보고서의 첫 번째 또는 마지막 페이지를 열고, 페이지 단위로 스크롤하고, 특정 페이지를 엽니다. 특정 페이지를 보려면 페이지 번호를 입력한 다음 Enter 키를 누릅니다.|  
|![페이지 표시 컨트롤](../reporting-services/media/htmlviewer-pagesize.gif "페이지 표시 컨트롤")|**페이지 표시 컨트롤**|보고서 페이지의 크기를 확대하거나 축소합니다. 비율에 따라 보고서 페이지 크기를 조정할 수 있을 뿐만 아니라 **페이지 너비** 를 선택하여 페이지의 가로 길이를 브라우저 창에 맞추거나 **전체 페이지** 를 선택하여 페이지의 세로 길이를 브라우저 창에 맞출 수도 있습니다. **확대/축소** 옵션은 [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Explorer 5.5 이상에서 지원됩니다.|  
|![검색 필드](../reporting-services/media/htmlviewer-search.gif "검색 필드")|**검색 필드**|찾을 단어나 구(최대 256자까지 입력 가능)를 입력하여 보고서 내용을 검색합니다. 검색은 대/소문자를 구분하며 현재 선택한 페이지나 섹션에서 시작됩니다. 표시 가능한 내용만 검색 작업에 포함됩니다. 같은 값을 계속 검색하려면 **다음**을 클릭합니다.|  
|![내보내기 형식](../reporting-services/media/htmlviewer-export.GIF "내보내기 형식")|**내보내기 형식**|새 브라우저 창을 열고 보고서를 선택한 형식으로 렌더링합니다. 사용할 수 있는 형식은 보고서 서버에 설치되어 있는 렌더링 확장 프로그램에 따라 다릅니다. 인쇄할 경우에는 TIFF 형식을 권장합니다. 선택한 형식으로 보고서를 표시하려면 **내보내기** 를 클릭합니다.|  
|![문서 구조 아이콘](../reporting-services/media/htmlviewer-docmap.GIF "문서 구조 아이콘")|**문서 구조 아이콘**|문서 구조를 포함하는 보고서에서 문서 구조 창을 표시하거나 숨깁니다. 문서 구조는 웹 사이트의 탐색 창과 유사한 보고서 탐색 컨트롤입니다. 문서 구조의 항목을 클릭하여 특정 그룹, 페이지 또는 하위 보고서로 이동할 수 있습니다.|  
|![프린터 아이콘](../reporting-services/media/printer-icon.gif "프린터 아이콘")|**프린터 아이콘**|인쇄 옵션을 지정하고 보고서를 인쇄할 수 있도록 인쇄 대화 상자를 엽니다. 인쇄 기능을 처음 사용하는 경우 이 아이콘을 클릭하면 인쇄 컨트롤을 다운로드하라는 메시지가 표시됩니다.|  
||**표시 및 숨기기 아이콘**|매개 변수가 포함된 보고서에서 매개 변수 값 필드와 **보고서 보기** 단추를 표시하거나 숨깁니다.|  
|![보고서 도구 모음의 브라우저 새로 고침 단추](../reporting-services/media/htmlviewer-refresh.GIF "보고서 도구 모음의 브라우저 새로 고침 단추")|**보고서 새로 고침 아이콘**|보고서를 새로 고칩니다. 활성화된 보고서의 데이터를 새로 고칩니다. 캐시된 보고서는 저장된 위치에서 다시 로드됩니다.|  
|![htmlviewer_datafeed](../reporting-services/media/htmlviewer-datafeed.gif "htmlviewer_datafeed")|**데이터 피드 아이콘**|보고서에서 생성된 데이터 피드를 나타냅니다.|  
|![ssrs_powerbi_button_reportwviewer](../reporting-services/media/ssrs-powerbi-button-reportwviewer.png "ssrs_powerbi_button_reportwviewer")|**Power BI 대시보드에 고정**|지원 보고서 항목을 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]에 고정합니다. 단추가 표시되지 않는 경우 보고서 서버가 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]에 통합되지 않은 것입니다.  자세한 내용은 [Power BI 보고서 서버 통합&#40;구성 관리자&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)과 통합해야 합니다.|  
  
### <a name="about-export-formats"></a>내보내기 형식 정보  
 보고서 도구 모음에서 보고서를 다양한 형식으로 볼 수 있습니다. 사용할 수 있는 형식은 보고서 서버에 설치되어 있는 렌더링 확장 프로그램에 따라 다릅니다. 다른 형식을 선택하면 별도의 브라우저 창이 열려 선택한 내보내기 형식과 연결된 뷰어를 사용하여 보고서를 표시합니다. 선택한 형식에 사용할 수 있는 뷰어가 없는 경우 다른 형식을 선택할 수 있습니다.  
  
 기본 보고서 서버 설치에는 다음과 같은 내보내기 형식이 포함되어 있습니다. 실제로 사용할 수 있는 내보내기 형식 목록은 여기에 나열된 것과 다를 수 있습니다.  
  
|내보내기 형식|설명|  
|-------------------|-----------------|  
|XML|보고서를 XML 구문으로 표시합니다. XML로 표시된 보고서는 새 브라우저 창에서 열립니다.|  
|CSV|보고서를 쉼표로 분리된 형식으로 표시합니다. 보고서가 CSV 파일 형식과 연결된 애플리케이션에서 열립니다.|  
|PDF|클라이언트 쪽 PDF 뷰어를 사용하여 보고서를 봅니다. 이 형식을 사용하려면 타사의 PDF Viewer(예: Adobe Acrobat Reader)가 있어야 합니다.|  
|MHTML|보고서와 함께 이미지와 연결된 내용을 유지하는 MIME로 인코딩된 HTML 형식으로 보고서를 봅니다.|  
|내보내기|[!INCLUDE[msCoName](../includes/msconame-md.md)] Excel에서 보고서(.xlsx 파일)를 봅니다.|  
|PowerPoint|[!INCLUDE[msCoName](../includes/msconame-md.md)] PowerPoint에서 보고서(.pptx 파일)를 봅니다.|  
|TIFF 파일|기본 TIFF 뷰어로 보고서를 봅니다. 일부 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 클라이언트의 경우 이 뷰어는 Windows 사진 및 팩스 뷰어입니다. 페이지 단위의 레이아웃으로 보고서를 보려면 이 형식을 선택합니다.|  
|Word|[!INCLUDE[msCoName](../includes/msconame-md.md)] Word에서 보고서(.docx 파일)를 봅니다.|  
  
## <a name="parameters"></a>매개 변수  
 매개 변수는 특정 데이터를 선택하는 데 사용되는 값입니다. 특히, 보고서에서 데이터를 선택하는 쿼리를 완성하거나 결과 집합을 필터링하는 데 사용됩니다. 보고서에서 일반적으로 사용하는 매개 변수에는 날짜, 이름, ID 등이 들어 있습니다. 매개 변수 값을 지정하면 보고서에는 해당 값과 일치하는 데이터만 포함됩니다(예: 직원 ID 매개 변수를 기준으로 한 직원 데이터). 매개 변수는 보고서의 필드에 해당합니다. 매개 변수를 지정한 후 데이터를 가져오려면 **보고서 보기** 를 클릭합니다.  
  
 보고서를 만든 사람이 각 보고서에 맞는 매개 변수 값을 정의합니다. 보고서 관리자도 매개 변수 값을 설정할 수 있습니다. 보고서에 맞는 매개 변수 값을 확인하려면 보고서를 디자인한 사람이나 관리자에게 문의하십시오.  
  
## <a name="credentials"></a>자격 증명  
 자격 증명은 데이터 원본에 액세스할 수 있는 사용자 이름과 암호 값입니다. 자격 증명을 지정한 후 데이터를 가져오려면 **보고서 보기** 를 클릭합니다. 로그온이 필요한 보고서의 경우 각 사용자에게 표시되는 데이터가 다를 수 있습니다. 따라서 두 사용자가 같은 보고서를 실행해도 다른 결과를 얻을 수 있습니다. 또한 일부 보고서에는 숨겨진 영역이 있는데 사용자 로그온 자격 증명이나 보고서 자체의 선택 사항에 따라 표시 여부가 결정됩니다. 보고서의 숨겨진 영역은 검색 작업에서 제외되므로 보고서의 모든 부분을 볼 수 있는 경우와는 검색 결과가 다를 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [보고서 찾기, 보기 및 관리&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [보고서 내보내기&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)  
  
  
