---
title: SharePoint 사이트의 보고서 뷰어 웹 파트 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SharePoint integration [Reporting Services], viewing reports
- Web Parts [Reporting Services]
- SharePoint integration [Reporting Services], Web Parts
- Report Viewer Web Part [Reporting Services]
ms.assetid: b6341a73-172f-4632-a9e9-cc79fed3f36b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ba8b23c800718d289b2a7a633d5244261b5ab8a8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66103047"
---
# <a name="report-viewer-web-part-on-a-sharepoint-site"></a>SharePoint 사이트의 보고서 뷰어 웹 파트
  보고서 뷰어 웹 파트는 SharePoint 제품용 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 추가 기능에 의해 설치되는 사용자 지정 웹 파트입니다. 웹 파트를 사용하여 SharePoint 통합 모드로 실행되도록 구성된 보고서 서버에서 보고서를 보고 탐색하며 인쇄하고 내보낼 수 있습니다. 보고서 뷰어 웹 파트는 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보고서 서버에서 처리하는 보고서 정의 파일(.rdl)과 연결됩니다. 다른 소프트웨어 제품에서 만든 다른 보고서 문서와 함께 이 웹 파트를 사용할 수 없습니다.  
  
 웹 파트를 설치하려면 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 추가 기능 설치 프로그램을 실행해야 합니다. 웹 파트를 독립적으로 설치하거나 제거하지 마십시오. 웹 파트는 추가 기능의 일부이며 추가 기능 설치 패키지를 통해서만 설치할 수 있습니다. 보고서 뷰어 웹 파트의 파일 이름은 ReportViewer.dwp입니다. 이 파일은 Program Files\Common Files\Microsoft Shared\web server extensions\12\template\features\reportserver 폴더에 있으며 다른 폴더로 이동하면 안 됩니다.  
  
 웹 파트를 사용하려면 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 추가 기능을 설치 및 구성하고 보고서 서버를 SharePoint 통합용으로 구성해야 합니다. 또한 뷰어에 표시할 보고서가 있어야 합니다. 라이브러리, 라이브러리 폴더, 보고서 기록에 있는 보고서나 라이브러리 웹 파트에서 보고서 뷰어 웹 파트로 링크된 보고서만 열 수 있습니다. 사용자 지정 목록의 항목에 대한 첨부 파일로 저장된 보고서는 열 수 없습니다.  
  
 보고서 뷰어 웹 파트의 속성을 설정하여 도구 모음과 보기 영역의 모양을 제어하고 웹 파트를 특정 보고서에 연결할 수 있습니다. 보고서 뷰어에는 명시적으로 링크된 보고서가 표시되거나 열린 .rdl 파일이 표시됩니다.  
  
 보고서 뷰어 인스턴스 하나에 여러 개의 보고서를 연결할 수는 없지만 보고서를 그룹화하려는 경우 여러 개의 보고서 뷰어 웹 파트 인스턴스를 한 페이지에 포함하는 웹 파트 페이지나 대시보드를 만들 수 있습니다.  
  
 웹 파트에는 보기 영역, 도구 모음, 자격 증명과 매개 변수 설정을 위한 축소 가능한 영역 및 속성이 포함되어 있습니다. 다음 그림에서는 Company Sales 예제 보고서가 표시된 웹 파트와 도구 모음에서 선택할 수 있는 내보내기 옵션을 보여 줍니다.  
  
 ![보고서 뷰어 웹 파트](media/rs-sharepointrvwebpart.gif "보고서 뷰어 웹 파트")  
  
## <a name="web-part-components"></a>웹 파트 구성 요소  
 보기 영역에는 보고서가 HTML로 표시됩니다. 웹 파트 구성 방법에 따라 보기 영역이 최대화되어 보고서가 전체 페이지 모드로 표시되거나 인접한 창 및 도구 모음과 사용 가능한 공간이 공유될 수 있습니다.  
  
 도구 모음에서는 페이지 탐색, 검색 및 확대/축소 기능을 제공하며 다른 애플리케이션 형식으로 보고서를 볼 수 있도록 내보내기 기능도 제공합니다. 또한 HTML 보고서로 페이지가 매겨진 인쇄 결과물을 생성하고 페이지 레이아웃 및 여백 설정을 변경하는 기능이 포함된 선택적 인쇄 기능을 제공합니다. **보고서 작성기로 열기, 구독**, **내보내기**및 **인쇄** 는 도구 모음의 **동작** 메뉴에 제공됩니다. 페이지 탐색 및 확대/축소 컨트롤은 도구 모음에 바로 제공됩니다.  
  
> [!NOTE]  
>  해당 코드를 작성하지 않으면 도구 모음을 사용자 지정할 수 없지만 속성을 설정하여 컨트롤을 모두 또는 일부 숨길 수 있습니다.  
  
### <a name="export-action-on-the-report-toolbar"></a>보고서 도구 모음의 내보내기 동작  
 **동작** 메뉴의 **내보내기** 명령은 보고서 서버에 배포된 렌더링 확장 프로그램과 연결된 응용 프로그램 형식을 표시합니다. 특정 형식을 사용할 수 있는지 확인하려면 보고서 서버에서 렌더링 확장 프로그램을 추가 또는 제거하거나 구성 설정을 수정하여 목록에서 특정 내보내기 형식을 제거해 봅니다. 보고서 서버에서 구성 설정을 지정하여 사용 가능한 형식을 제어할 수도 있습니다. 해당 렌더링 확장 프로그램의 구성 설정을 추가 및 수정하여 특정 형식의 기본 동작을 수정할 수 있습니다.  
  
### <a name="print-action-on-the-report-toolbar"></a>보고서 도구 모음의 인쇄 동작  
 **동작** 메뉴의 **인쇄** 는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]를 통해 제공되는 사용자 지정 인쇄 기능입니다. **인쇄**를 클릭하면 ActiveX 클라이언트 쪽 인쇄 컨트롤이 클라이언트 컴퓨터에 다운로드됩니다. 대부분의 경우 **인쇄** 를 클릭하는 사용자에게는 로컬 컴퓨터에 대한 관리자 권한이 있어야 합니다. 관리자 권한이 있는 사용자만 ActiveX 컨트롤을 다운로드할 수 있도록 제한하는 것이 일반적입니다. 클라이언트 쪽 인쇄 컨트롤이 다운로드를 사용할지 여부를 SharePoint 중앙 관리를 사용할 수 있습니다.  
  
### <a name="find-action-on-the-report-toolbar"></a>보고서 도구 모음의 찾기 동작  
 **동작** 메뉴의 **찾기** 는 보고서에서 대상 위치로 이동하는 방법을 제공합니다. 찾을 단어나 구를 입력하여 보고서 내용을 검색할 수 있습니다. 검색 단어는 최대 256자까지 입력할 수 있습니다. 검색 중 보고서에서 일치하는 값을 찾으면 해당 값이 포함된 보고서 부분으로 포커스가 이동합니다.  
  
 검색할 값을 입력할 때는 보고서에 표시되는 대로 값을 입력합니다. 문장의 모든 단어가 보고서에 있는 경우가 아니면 "이달의 평균 수익은 얼마입니까" 등의 질문을 사용하지 마십시오.  
  
 한 번에 하나의 용어나 값만 검색할 수 있습니다. 검색 연산자(예: `AND` 또는 `OR`)나 기호 및 와일드카드는 사용할 수 없습니다. 데이터의 교집합 영역(예: 특정 제품에 대한 특정 월의 순매출 검색)은 검색할 수 없습니다. 이러한 종류의 분석을 수행하려면 보고서 작성기를 사용하여 클릭 광고 보고서를 만듭니다.  
  
 보고서 데이터에 대한 액세스를 제한하는 데이터베이스 및 모델 보안 설정이 검색 작업에 적용됩니다. 모델을 데이터 원본으로 사용하는 클릭 광고 보고서에서 값을 검색 중이며 모델의 일부에 액세스할 수 없는 경우 해당 모델 부분이 나타내는 데이터는 검색에서 제외됩니다.  
  
### <a name="panes-for-specifying-credentials-and-parameters"></a>자격 증명 및 매개 변수 지정 창  
 **자격 증명** 및 **매개 변수** 는 보기 영역 옆에 나타나는 창입니다. **자격 증명** 은 데이터 원본에 대한 액세스 권한이 있는 계정과 암호를 요청하는 메시지를 사용자에게 표시하도록 보고서에 대한 데이터 원본 연결을 구성한 경우 나타납니다. **매개 변수** 는 보고서에 정의된 매개 변수에 대한 사용자 입력을 보고서에서 사용하는 경우 나타납니다.  
  
### <a name="setting-properties-on-the-report-viewer-web-part"></a>보고서 뷰어 웹 파트에 속성 설정  
 웹 파트의 속성에는 보고서 뷰어와 관련된 사용자 지정 속성과 모든 웹 파트에 설정할 수 있는 일반 속성이 포함됩니다. 자세한 내용은 [보고서 뷰어 웹 파트 구성](../../2014/reporting-services/customize-the-report-viewer-web-part.md)을 참조하세요.  
  
 기본적으로 보고서는 전체 페이지 모드로 열립니다. 전체 페이지 모드에서는 페이지 탐색, 검색 및 기타 기능을 제공하는 도구 모음이 표시됩니다. 웹 파트를 사용자 지정하여 모양이나 기본 동작을 변경할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [설치 또는 제거는 Reporting Services 추가-SharePoint 용 &#40;SharePoint 2010 및 SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
 [웹 페이지에 보고서 뷰어 웹 파트 추가&#40;SharePoint 통합 모드의 Reporting Services&#41;](report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)  
  
  
