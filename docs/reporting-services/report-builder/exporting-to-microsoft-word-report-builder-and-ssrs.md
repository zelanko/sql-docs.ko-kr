---
title: Microsoft Word로 내보내기(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-builder
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 0cd8ae26-4682-4473-8f15-af084951defd
caps.latest.revision: 23
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 73c41c24d4572c6bc91ec0a8728be590344787df
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33022320"
---
# <a name="exporting-to-microsoft-word-report-builder-and-ssrs"></a>Microsoft Word로 내보내기(보고서 작성기 및 SSRS)

  Word 렌더링 확장 프로그램은 페이지가 매겨진 보고서를  [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 형식(.docx)으로 렌더링합니다. 형식은 Office Open XML입니다.  
  
 이 렌더러에 의해 생성된 파일의 콘텐츠 형식은 **application/vnd.openxmlformats-officedocument.wordprocessingml.document** 이고 파일 확장명은 .docx입니다.  
  
 Word로 내보내는 방법에 대한 자세한 내용은 [보고서 내보내기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)를 참조하세요.  
  
 보고서를 Word 문서로 내보낸 후에는 보고서의 내용을 변경하고 우편물 레이블, 구매 주문서 또는 편지 양식과 같은 문서 스타일의 보고서를 디자인할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="ReportItemsWord"></a> Word의 보고서 항목  
 Word로 내보낸 보고서는 보고서 본문을 나타내는 중첩된 표로 표시됩니다. 테이블릭스 데이터 영역은 보고서에 있는 데이터 영역의 구조를 반영하는 중첩된 표로 렌더링됩니다. 입력란과 사각형은 각각 표 안에 셀로 렌더링됩니다. 입력란 값은 셀 안에 표시됩니다.  
  
 이미지, 차트, 데이터 막대, 스파크라인, 맵, 지표 및 계기는 각각 표 셀 안에 정적 이미지로 렌더링됩니다. 이러한 보고서 항목의 하이퍼링크와 드릴스루 링크는 렌더링되지만, 차트 내에서 클릭할 수 있는 영역과 지도는 렌더링되지 않습니다.  
  
 회보 스타일 열 보고서는 Word에서 렌더링되지 않습니다. 보고서 본문 및 페이지의 배경 이미지와 색은 렌더링되지 않습니다.  
  
##  <a name="Pagination"></a> 페이지 매김  
 Word에서 보고서를 열면 페이지 크기를 기준으로 하여 전체 보고서의 페이지가 다시 매겨집니다. 페이지를 다시 매기는 과정에서 의도하지 않았던 자리에 페이지 나누기가 삽입될 수도 있고, 경우에 따라서는 내보낸 보고서에 페이지 나누기가 두 번 연속으로 삽입되거나 빈 페이지가 추가될 수도 있습니다. 페이지 여백을 조정하여 Word의 페이지 매김을 변경할 수도 있습니다.  
  
 이 렌더러에서는 논리적 페이지 나누기만 지원합니다.  
  
### <a name="page-sizing"></a>페이지 크기 조정  
 보고서가 렌더링될 때 Word 페이지 높이 및 너비는 페이지 크기 높이와 너비, 왼쪽과 오른쪽 페이지 여백, 위쪽과 아래쪽 페이지 여백과 같은 RDL 속성으로 설정됩니다.  
  
### <a name="page-width"></a>페이지 너비  
 Word에서 지원하는 페이지 너비는 최대 55.87cm입니다. 보고서가 55.87cm보다 더 넓더라도 렌더러를 통해 보고서가 렌더링되지만 Word의 인쇄 모양 보기나 읽기 모드 보기에서는 보고서 내용이 표시되지 않습니다. 데이터를 보려면 기본 보기나 웹 모양 보기로 전환해야 합니다. Word의 이러한 보기에서는 공백의 크기를 줄여 보고서 내용을 더 많이 표시할 수 있습니다.  
  
 렌더링된 보고서는 내용을 표시하기 위해 필요한 경우 너비가 22인치까지 늘어납니다. 보고서의 최소 너비는 속성 창의 RDL Width 속성을 기준으로 합니다.  
  
##  <a name="DocumentProperties"></a> 문서 속성  
 Word 렌더러는 DOCX 파일에 다음과 같은 메타데이터를 기록합니다.  
  
|보고서 요소 속성|Description|  
|-------------------------------|-----------------|  
|Report Title(보고서 제목)|Title|  
|Report.Author|작성자|  
|Report.Description|주석|  
  
##  <a name="ReportHeadersFooters"></a> 페이지 머리글 및 바닥글  
 페이지 머리글 및 바닥글은 Word에서 머리글 및 바닥글 영역으로 렌더링됩니다. 보고서 페이지 번호나 보고서 페이지의 총 수를 나타내는 식이 페이지 머리글이나 바닥글에 있으면 렌더링된 보고서에 정확한 페이지를 표시할 수 있도록 해당 페이지 번호나 식이 Word 필드로 변환됩니다. 보고서에 머리글 또는 바닥글 높이가 설정되어 있더라도 이 설정은 Word에서 지원되지 않습니다. PrintOnFirstPage 속성은 일부 환경에서 보고서의 첫 번째 페이지에 페이지 머리글 및 페이지 바닥글을 인쇄할지 여부를 지정할 수 있습니다. 렌더링된 보고서에 여러 페이지가 있고 각 페이지에 단일 섹션만 포함되는 경우 PrintOnFirstPage를 False로 설정할 수 있으며 이렇게 하면 텍스트가 첫 번째 페이지에 표시되지 않습니다. 그렇지 않은 경우 텍스트는 PrintOnFirstPage 속성의 값에 상관없이 인쇄됩니다.  
  
 Word 렌더러는 보고서가 Word로 내보낼 때 페이지 머리글 및 바닥글의 모든 식에 대해 구문 분석을 시도합니다. 여러 형식의 식은 성공적으로 구문 분석되며 예상 값은 모든 보고서 페이지의 머리글 및 바닥글에 나타납니다.  
  
 그러나 페이지 머리글 및 페이지 바닥글이 보고서의 다른 페이지에 있는 다른 값을 확인하는 복합 식을 포함한 경우 동일한 값이 모든 보고서 페이지에 표시됩니다. 다음 두 식의 페이지 번호는 내보낸 보고서에서 증가하지 않습니다. 페이지 번호는 모든 보고서 페이지에서 동일한 값으로 변환됩니다.  
  
-   `="Page: " + Globals!PageNumber.ToString + " of " + Globals!TotalPages.ToString`  
  
-   `=Avg(Fields!YTDPurchase.Value, "Sales") & " Page Number " & Globals!PageNumber`  
  
 이는 Word 렌더러가 **PageNumber** 및 **TotalPages** 등의 페이지 매김과 관련된 필드에 대해 보고서를 구문 분석하며, 함수를 호출하는 것이 아니라 단순 참조만 처리하기 때문입니다. 이 경우 식에서는 **ToString** 함수를 호출합니다. 다음 두 식은 동일하며, 보고서를 보고서 작성기 또는 보고서 디자이너에서 미리 보거나 게시된 보고서를 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 웹 포털 또는 SharePoint 라이브러리에서 렌더링할 때 두 식 모두 올바르게 렌더링됩니다. 그러나 Word 렌더러는 두 번째 식만 올바르게 구문 분석하여 올바른 페이지 번호를 렌더링합니다.  
  
-   **복합 식:**  식은 `="Average Sales " & Avg(Fields!YTDPurchase.Value, "Sales") & " Page Number " & Globals!PageNumber`  
  
-   **텍스트 실행을 사용하는 식:** 텍스트, **평균 판매**와 식,  `=Avg(Fields!YTDPurchase.Value, "Sales)`및 텍스트, **페이지 번호**와 식 `=Globals!PageNumber`  
  
 이러한 문제를 방지하려면 머리글 및 바닥글에서 식을 사용할 때 하나의 복합 식 대신 여러 텍스트를 사용해 실행하세요. 다음은 이와 동등한 두 가지 식입니다. 첫 번째 식은 복합식이고 두 번째 식은 텍스트 실행을 사용합니다. Word 렌더러는 두 번째 식만 성공적으로 구문 분석합니다.  
  
##  <a name="Interactivity"></a> 상호 작용  
 Word에서는 일부 대화형 요소가 지원됩니다. 다음은 특정 동작에 대한 설명입니다.  
  
### <a name="show-and-hide"></a>표시 및 숨기기  
 Word 렌더러에서는 렌더링되는 보고서 항목의 상태에 따라 보고서 항목을 렌더링합니다. 보고서 항목이 숨김 상태이면 해당 보고서 항목이 Word 문서에 렌더링되지 않습니다. 보고서 항목이 표시됨 상태이면 해당 보고서 항목이 Word 문서에 렌더링됩니다. 보고서 항목의 상태를 전환하는 기능은 Word에서 지원되지 않습니다.  
  
### <a name="document-map"></a>문서 구조  
 보고서에 문서 구조 레이블이 있으면 해당 레이블이 관련 보고서 항목 및 그룹의 Word TOC(목차) 레이블로 렌더링됩니다. 문서 구조 레이블은 TOC 레이블의 레이블 텍스트로 사용됩니다. 대상 링크는 레이블이 설정되어 있는 항목 근처에 배치됩니다. Word 문서에서 TOC가 자동으로 만들어지지는 않지만 보고서에 렌더링된 문서 구조 레이블을 사용하여 TOC를 직접 작성할 수 있습니다.  
  
### <a name="hyperlink-and-drillthrough-links"></a>하이퍼링크 및 드릴스루 링크  
 입력란 및 이미지 보고서 항목에 대한 하이퍼링크와 드릴스루 링크는 Word 문서에서 하이퍼링크로 렌더링됩니다. 하이퍼링크를 클릭하면 기본 웹 브라우저가 열리고 지정된 URL로 이동합니다. 드릴스루 하이퍼링크를 클릭하면 원본 보고서 서버에 액세스할 수 있습니다.  
  
### <a name="interactive-sorting"></a>대화형 정렬  
 보고서 내용은 보고서 데이터 영역 내에 현재 정렬되어 있는 방식을 기준으로 렌더링됩니다. Word에서는 대화형 정렬을 지원하지 않습니다. 보고서를 렌더링한 다음 Word 내에서 표 정렬을 적용할 수 있습니다.  
  
### <a name="bookmarks"></a>책갈피  
 보고서의 책갈피는 Word 책갈피로 렌더링됩니다. 책갈피 링크는 문서 내에서 책갈피 레이블로 연결되는 하이퍼링크로 렌더링됩니다. 책갈피 레이블은 길이가 40자 미만이어야 합니다. 밑줄(_) 이외의 특수 문자는 책갈피 레이블에 사용할 수 없습니다. 지원되지 않는 특수 문자는 책갈피 레이블 이름에서 제거되며, 이름이 40자보다 길면 이름의 뒷부분이 잘립니다. 보고서에 중복된 책갈피 이름이 있으면 Word에서 책갈피가 렌더링되지 않습니다.  
  
##  <a name="WordStyleRendering"></a> Word 스타일 렌더링  
 다음은 Word에서 스타일이 렌더링되는 방식에 대한 간략한 설명입니다.  
  
### <a name="color-palette"></a>색상표  
 보고서에서 렌더링한 색은 Word 문서에서도 렌더링됩니다.  
  
### <a name="border"></a>테두리  
 페이지 테두리를 제외한 보고서 항목의 테두리는 Word 표 셀 테두리로 렌더링됩니다.  
  
##  <a name="SquigglyLines"></a> 내보낸 보고서의 구불구불한 선  
 보고서를 내보내고 Word에서 보는 경우 보고서 데이터 또는 상수에 빨간색이나 녹색의 구불구불한 선으로 밑줄이 표시될 수 있습니다. 빨간색의 구불구불한 선은 맞춤법 오류를 나타내고, 녹색의 구불구불한 선은 문법 오류를 나타냅니다. 이 문제는 Word에서 지정된 편집 언어의 교정(맞춤법 및 문법)을 따르지 않는 단어가 보고서에 포함되어 있는 경우 발생합니다. 예를 들어 보고서가 스페인어 버전의 Word에서 렌더링되는 경우 영어 보고서 열 제목에는 빨간색의 구불구불한 선으로 밑줄이 표시될 가능성이 높습니다. 일반적으로 보고서에는 완전한 문장이나 단락보다는 짧은 텍스트만 포함되기 때문에 감지된 문법 오류보다는 감지된 맞춤법 오류가 보고서에 보다 일반적으로 나타납니다.  
  
 보고서에 구불구불한 선이 있으면 보고서에 오류가 있음을 의미하지만 실제로는 오류가 없을 가능성이 높습니다. 보고서의 교정 언어를 변경하여 구불구불한 선을 제거할 수 있습니다. 교정 언어를 변경하려면 보고서의 내용을 선택한 다음 내용에 적합한 언어를 지정합니다. 내용을 전부 선택하거나 일부만 선택할 수 있습니다. Word에서 **교정 언어 설정** 언어 옵션은 **검토** 탭의 **언어** 영역에 있습니다. 내용을 업데이트한 후에는 문서를 다시 저장해야 합니다.  
  
 Office 프로그램의 언어 버전에 따라 선택한 언어의 교정 도구(예: 사전)가 프로그램과 함께 포함되거나 구입한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office 언어 팩에서 제공됩니다.  
  
 다음 항목에서는 Office 및 Word 옵션 설정에 대한 추가 정보를 제공합니다.  
  
-   Word의 **Microsoft Office 언어 기본 설정** 또는 **Word 옵션** 대화 상자에서 편집 언어를 변경합니다. 자세한 내용은 [편집, 표시 또는 도움말 언어 기본 설정 지정](http://office.microsoft.com/word-help/enable-the-use-of-other-languages-in-your-office-programs-HA010354783.aspx?CTT=1)을 참조하세요.  
  
-   Office 언어 팩을 추가한 다음 편집 언어를 변경합니다. 자세한 내용은 [편집, 표시 또는 도움말 언어 기본 설정 지정](http://office.microsoft.com/word-help/enable-the-use-of-other-languages-in-your-office-programs-HA010354783.aspx?CTT=1) 및 [Office 언어 옵션](http://office.microsoft.com/language/)을 참조하세요.  
  
> [!NOTE]  
>  Word의 **Microsoft Office 언어 기본 설정** 또는 **Word 옵션** 대화 상자에서 편집 언어를 변경하는 경우 변경된 편집 언어가 모든 Office 프로그램에 적용됩니다.  
  
##  <a name="WordLimitations"></a> Word 제한 사항  
 다음은 [!INCLUDE[ofprword](../../includes/ofprword-md.md)]에서 적용되는 제한 사항입니다.  
  
-   Word 표에서는 최대 63개의 열을 지원합니다. 보고서에 포함된 열이 63개보다 많은 경우 이 보고서를 렌더링하면 Word에서 표가 분할됩니다. 63개를 초과하는 열은 보고서 본문에 표시된 63개의 열 옆에 배치됩니다. 따라서 보고서 열이 줄을 맞춰 제대로 정렬되지 않을 수 있습니다.  
  
-   Word에서는 페이지 너비의 경우 최대 55.87cm까지, 높이의 경우 최대 55.87cm까지 지원합니다. 보고서 내용의 너비가 55.87cm보다 넓으면 인쇄 모양 보기에서 일부 데이터가 표시되지 않을 수 있습니다.  
  
-   페이지 머리글 및 바닥글 높이 설정은 Word에서 무시됩니다.  
  
-   보고서를 내보내면 Word에서 보고서의 페이지가 다시 매겨집니다. 그 과정에서 렌더링된 보고서에 페이지 나누기가 추가로 삽입될 수 있습니다.  
  
-   테이블릭스(테이블, 행렬 또는 목록)의 정적 머리글 행에 대한 RepeatOnNewPage 속성을 **True**로 설정하더라도 Word에서는 머리글 행이 여러 페이지에 걸쳐 반복되지 않습니다. 보고서에 명시적 페이지 나누기를 정의하여 머리글 행이 새 페이지에도 표시되게 할 수 있습니다. 그러나 Word로 내보내 렌더링한 보고서에는 Word 자체의 고유한 페이지 매김 방식이 적용되므로 그 결과가 예상과 다를 수 있으며 머리글 행이 반복되지 않을 수 있습니다. 정적 머리글 행은 열 머리글을 포함하는 행입니다.  
  
-   입력란에 줄 바꿈하지 않는 공백이 포함되어 있으면 입력란의 크기가 늘어납니다.  
  
-   텍스트를 Word로 내보내면 특정 글꼴로 글꼴 장식이 되어 있는 텍스트로 인해 렌더링된 보고서에 예기치 않은 문자가 생기거나 문자가 누락될 수 있습니다.  
  
##  <a name="WordBenefits"></a> Word 렌더러 사용 이점  
 [!INCLUDE[ofprword](../../includes/ofprword-md.md)] .docx 파일의 새로운 기능을 내보낸 보고서에서 사용할 수 있을 뿐만 아니라 보고서를 *.docx 파일로 내보낼 경우 크기를 줄일 수 있습니다. Word 렌더러를 사용하여 내보낸 보고서는 일반적으로 동일한 보고서를 Word 2003 렌더러를 사용하여 내보낼 때보다 매우 작습니다.  
  
## <a name="backward-compatibility-of-exported-reports"></a>내보낸 보고서의 이전 버전 호환성  
 Word 호환성 모드를 선택하고 호환성 옵션을 설정할 수 있습니다. Word 렌더러에서는 호환성 모드가 설정된 상태로 문서를 만듭니다. 호환성 모드를 해제한 상태로 문서를 다시 저장하면 문서의 레이아웃에 영향을 줄 수 있습니다.  
  
 호환성 모드를 해제하고 보고서를 다시 저장할 경우 보고서 레이아웃이 예기치 않게 변경될 수 있습니다.  
  
##  <a name="AvailabilityWord"></a> Word 2003 렌더러  
  
> [!IMPORTANT]  
>  [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2003(.doc) 렌더링 확장 프로그램은 더 이상 사용되지 않습니다. 자세한 내용은 [SQL Server 2016의 SQL Server Reporting Services에서 지원되지 않는 기능](~/reporting-services/deprecated-features-in-sql-server-reporting-services-ssrs.md)을 참조하세요.  
  
 Word 렌더러는 Word, Excel 및 PowerPoint용 [!INCLUDE[ofprword](../../includes/ofprword-md.md)] Office 호환 기능 팩이 설치된 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 2003과도 호환됩니다. 자세한 내용은 [Word, Excel 및 PowerPoint용 Microsoft Office 호환 기능 팩](http://go.microsoft.com/fwlink/?LinkID=205622)을 참조하세요.  
  
 [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2003과 호환되는 이전 버전의 Word 렌더링 확장 프로그램은 Word 2003으로 이름이 변경되었습니다. 기본적으로 Word 렌더링 확장 프로그램만 사용할 수 있습니다. Word 2003 렌더링 확장 프로그램을 사용할 수 있도록 하려면 Reporting Services 구성 파일을 업데이트해야 합니다. Word 2003 렌더러를 통해 생성되는 파일의 콘텐츠 형식은 **application/vnd.ms-word** 이고 파일 이름 확장명은 .doc입니다.  
  
 SQL Server Reporting Services에서 기본 Word 렌더러는 [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 형식(.docx)으로 렌더링하는 버전입니다. 이 옵션은 **웹 포털 및 SharePoint의** 내보내기 **메뉴에 나열되는** Word [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 옵션입니다. [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2003과만 호환되는 이전 버전은 이제 이름이 Word 2003으로 지정되며 이 이름으로 메뉴에 나열됩니다. **Word 2003** 메뉴 옵션은 기본적으로 표시되지 않지만 관리자가 RSReportServer 구성 파일을 업데이트하여 표시할 수 있습니다. Word 2003 렌더러를 사용하여 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서 보고서를 내보내려면 RSReportDesigner 구성 파일을 업데이트합니다. 하지만 일부 경우에는 Word 2003 렌더러를 표시할 수 없습니다. RSReportServer 구성 파일이 보고서 서버에 존재하기 때문에 구성 파일을 읽으려면 보고서를 내보내는 위치의 도구 또는 제품이 보고서 서버에 연결되어 있어야 합니다. 연결되어 있지 않거나 로컬 모드에 있는 도구 또는 제품을 사용할 경우 Word 2003 렌더러가 표시되도록 해도 효과가 없습니다. **Word 2003** 메뉴 옵션은 사용할 수 없는 상태로 유지됩니다. RSReportDesigner 구성 파일에서 Word 2003 렌더러를 표시하도록 설정하면 **보고서 미리 보기에서** Word 2003 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 메뉴 옵션을 항상 사용할 수 있습니다.  
  
 다음과 같은 시나리오에서는 **Word 2003의** 메뉴 옵션이 표시되지 않습니다.  
  
-   보고서 작성기가 연결되지 않은 모드이고 보고서 작성기에서 보고서를 미리 보는 경우.  
  
-   보고서 뷰어 웹 파트가 로컬 모드이고 SharePoint 팜이 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버와 통합되지 않은 경우. 자세한 내용은 [보고서 뷰어의 로컬 모드와 보고서 뷰어의 연결 모드 보고서&#40;SharePoint 모드의 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/local-mode-vs-connected-mode-reports-in-the-report-viewer.md)  
  
 **Word 2003** 렌더러가 표시되도록 구성된 경우 다음과 같은 시나리오에서 **Word** 및 **Word 2003** 메뉴 옵션을 사용할 수 있습니다.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Reporting Services가 기본 모드로 설치된 경우의 웹 포털  
  
-   Reporting Services가 SharePoint 통합 모드로 설치된 경우의 SharePoint 사이트  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 및 보고서 미리 보기  
  
-   보고서 작성기가 보고서 서버에 연결된 경우.  
  
-   보고서 뷰어 웹 파트가 원격 모드인 경우  
  
 다음 XML에서는 RSReportServer 및 RSReportDesigner 구성 파일의 두 Word 렌더링 확장 프로그램에 대한 요소를 보여 줍니다.  
  
 `<Extension Name="WORDOPENXML" Type="Microsoft.ReportingServices.Rendering.WordRenderer.WordOpenXmlRenderer.WordOpenXmlDocumentRenderer,Microsoft.ReportingServices.WordRendering"/>`  
  
 `<Extension Name="WORD" Type="Microsoft.ReportingServices.Rendering.WordRenderer.WordDocumentRenderer,Microsoft.ReportingServices.WordRendering" Visible="false"/>`  
  
 WORDOPENXML 확장은 [!INCLUDE[ofprword](../../includes/ofprword-md.md)] .docx 파일에 대한 Word 렌더러를 정의합니다. WORD 확장은 [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2003 버전을 정의합니다. `Visible = “false”` 는 Word 2003 렌더러가 숨겨져 있음을 나타냅니다. 자세한 내용은 [RsReportServer.config 구성 파일](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) 및 [RSReportDesigner 구성 파일](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)을 참조하세요.  
  
### <a name="differences-between-the-word-and-word-2003-renderers"></a>Word와 Word 2003 렌더러의 차이점  
 Word 또는 Word 2003 렌더러를 사용하여 렌더링된 보고서는 대개 시각적으로는 구분되지 않습니다. 그러나 Word 형식과 Word 2003 형식에는 약간의 차이점이 있습니다.  
  
##  <a name="DeviceInfo"></a> 장치 정보 설정  
 장치 정보 설정을 변경하여 이 렌더러의 일부 기본 설정을 변경할 수 있습니다. 예를 들어 하이퍼링크 및 드릴스루 링크를 생략할 수 있고 렌더링 시 항목의 원래 상태와 상관없이 설정/해제 전환이 가능한 모든 항목을 확장할 수 있습니다. 자세한 내용은 [Word Device Information Settings](../../reporting-services/word-device-information-settings.md)을 참조하세요.  

## <a name="next-steps"></a>다음 단계

[Reporting Services의 페이지 매김](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
[렌더링 동작](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
[여러 보고서 렌더링 확장 프로그램의 대화형 기능](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
[보고서 항목 렌더링](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
[테이블, 행렬 및 목록](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
