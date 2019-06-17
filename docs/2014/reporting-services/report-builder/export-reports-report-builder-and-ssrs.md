---
title: 내보내는 보고서 (보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10437"
ms.assetid: a2bab8c1-505d-4da3-b1db-ea0ae13b2336
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d8b4fe6e791f84f0949b0657b890c79db99dfbf9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107953"
---
# <a name="exporting-reports-report-builder-and-ssrs"></a>보고서 내보내기(보고서 작성기 및 SSRS)
  보고서를 실행한 후 Excel이나 PDF 같은 다른 형식으로 보고서를 내보내거나 보고서에서 사용할 수 있는 Atom 규격 데이터 피드를 나열하는 Atom 서비스 문서를 생성하여 보고서를 내보낼 수 있습니다.  
  
 보고서를 내보내면 다음을 수행할 수 있습니다.  
  
-   다른 애플리케이션에서 보고서 데이터로 작업. 예를 들어 보고서를 Excel로 내보낸 다음 Excel에서 해당 데이터를 사용하여 계속 작업할 수 있습니다.  
  
-   다른 형식으로 보고서 인쇄. 예를 들어 보고서를 PDF 파일 형식으로 내보낸 다음 인쇄할 수 있습니다.  
  
-   다른 파일 유형으로 보고서 복사본 저장. 예를 들어 보고서의 복사본을 만들어 Word로 내보낸 다음 저장할 수 있습니다.  
  
-   애플리케이션에서 보고서 데이터를 데이터 피드로 사용. 예를 들어 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 클라이언트에서 사용할 수 있는 Atom 규격 데이터 피드를 생성한 다음 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]에서 이 데이터로 작업할 수 있습니다.  
  
 내보내기 옵션은 보고서 관리자의 보고서 뷰어 도구 모음에서 사용할 수 있습니다. 이 도구 모음은 보고서 서버에서 보고서를 볼 때 모든 보고서의 맨 위에 나타나며 보고서를 미리 볼 때 보고서 작성기의 리본 메뉴에 표시됩니다. 데이터 피드 옵션은 보고서 관리자에서만 사용할 수 있습니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서는 보고서를 일반 파일 형식으로 내보낼 수 있도록 하는 다양한 렌더링 확장 프로그램을 제공합니다. 렌더링 확장 프로그램은 소프트 페이지 나누기를 사용하는 파일 형식(예: Word 또는 Excel), 하드 페이지 나누기를 사용하는 파일 형식(예: PDF 또는 TIFF) 또는 데이터만 있는 파일 형식(예: CSV 또는 Atom 호환 XML)을 지원합니다.  
  
 신속 하 게 시작 하려면 보고서를 내보내는 작업과 보고서에서 Atom 규격 데이터 피드 생성을 참조 하세요 [다른 파일 형식으로 보고서 내보내기 &#40;보고서 작성기 및 SSRS&#41; ](../export-a-report-as-another-file-type-report-builder-and-ssrs.md) 하 고 [에서 데이터 피드 생성을 보고서 &#40;보고서 작성기 및 SSRS&#41;](generate-data-feeds-from-a-report-report-builder-and-ssrs.md)합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="RendererTypes"></a> 렌더링 확장 프로그램 유형  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 렌더링 확장 프로그램에는 다음 세 가지 유형이 있습니다.  
  
-   **데이터 렌더링 확장 프로그램** 데이터 렌더링 확장 프로그램은 보고서에서 서식 및 레이아웃 정보를 모두 제거하고 데이터만 표시합니다. 이렇게 내보낸 파일은 Excel 같은 다른 파일 형식, 다른 데이터베이스, XML 데이터 메시지 또는 사용자 지정 애플리케이션으로 원시 보고서 데이터를 가져오는 데 사용할 수 있습니다. 데이터 렌더링 확장 프로그램은 페이지 나누기를 지원하지 않습니다.  
  
     다음 데이터 렌더링 확장 프로그램 지원 됩니다. CSV, XML 및 Atom입니다.  
  
-   **소프트 페이지 나누기 렌더러 확장 프로그램** 소프트 페이지 나누기 렌더링 확장 프로그램에서는 보고서 레이아웃과 서식이 유지됩니다. 이렇게 내보낸 파일은 웹 페이지나 **ReportViewer** 컨트롤 같은 화면 중심의 보기 및 배달용으로 최적화됩니다.  
  
     다음과 같은 소프트 페이지 나누기 렌더링 확장 프로그램 지원 됩니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word 및 웹 보관 파일 (MHTML).  
  
-   **하드 페이지 나누기 렌더링 확장 프로그램** 하드 페이지 나누기 렌더러 확장 프로그램에서는 보고서 레이아웃과 서식이 유지됩니다. 생성되는 파일은 인쇄 환경을 일정하게 유지하거나 온라인에서 책 형태로 보고서를 볼 수 있도록 최적화됩니다.  
  
     다음 하드 페이지 나누기 렌더링 확장 프로그램 지원 됩니다. TIFF와 PDF입니다.  
  
##  <a name="ExportFormats"></a> 내보내기 형식  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서는 다양한 형식으로 보고서를 렌더링하는 렌더링 확장 프로그램을 제공합니다. 이 기능을 사용하려는 경우 선택한 파일 형식에 맞게 보고서 디자인을 최적화해야 합니다. 각 렌더링 확장 프로그램에 대한 항목에서는 보고서가 이러한 형식으로 렌더링되는 방식에 대한 자세한 정보를 제공합니다.  
  
 다음 표에서는 사용 가능한 형식을 보여 줍니다.  
  
|형식|렌더링 확장 프로그램 유형|Description|  
|------------|------------------------------|-----------------|  
|CSV|data|CSV(쉼표로 구분된 값) 렌더링 확장 프로그램은 보고서의 데이터를 결합하여 읽기 쉽고 많은 애플리케이션과 교환할 수 있는 표준화된 일반 텍스트 형식으로 렌더링합니다.<br /><br /> 자세한 내용은 [CSV 파일로 내보내기&#40;보고서 작성기 및 SSRS&#41;](exporting-to-a-csv-file-report-builder-and-ssrs.md)를 참조하세요.|  
|내보내기|소프트 페이지 나누기|Excel 렌더링 확장 프로그램은 Word, Excel 및 PowerPoint용 Microsoft Office 호환 기능 팩이 설치된 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2003뿐만 아니라 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2007-2010과도 호환되는 Excel 문서로 보고서를 렌더링합니다 보고서를 Excel 워크시트로 내보내면 일부 레이아웃과 원래 디자인 요소가 유지되지 않을 수 있습니다. 보고서를 Excel로 내보낼 때 워크시트 탭 이름을 지정할 수 있도록 하는 속성을 보고서 및 보고서 내의 그룹에 설정할 수 있습니다. 이 렌더러에 의해 생성되는 파일의 확장명은 xlsx입니다.<br /><br /> 자세한 내용은 [Microsoft Excel로 내보내기&#40;보고서 작성기 및 SSRS&#41;](exporting-to-microsoft-excel-report-builder-and-ssrs.md)를 참조하세요.<br /><br /> 참고: 네이티브 형식으로 렌더링 하는 Excel 2003 렌더링 확장 프로그램 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2003은 일부 보고 시나리오에서 사용할 수 있습니다.|  
|Word|소프트 페이지 나누기|Word 렌더링 확장 프로그램은 Word, Excel 및 PowerPoint용 [!INCLUDE[ofprword](../../includes/ofprword-md.md)] Office 호환 기능 팩이 설치된 [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2003뿐만 아니라 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 2007-2010과도 호환되는 Word 문서로 보고서를 렌더링합니다. 보고서를 Word 문서로 내보낸 후에는 보고서의 내용을 변경하고 우편물 레이블, 구매 주문서 또는 편지 양식과 같은 문서 스타일의 보고서를 디자인할 수 있습니다. 이 렌더러에 의해 생성되는 파일의 확장명은 docx입니다.<br /><br /> 자세한 내용은 [Microsoft Word로 내보내기&#40;보고서 작성기 및 SSRS&#41;](exporting-to-microsoft-word-report-builder-and-ssrs.md)를 참조하세요.<br /><br /> 참고: 네이티브 형식으로 렌더링 하는 Word 2003 렌더링 확장 프로그램 [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2003은 일부 보고 시나리오에서 사용할 수 있습니다.|  
|웹 보관 파일|소프트 페이지 나누기|HTML 렌더링 확장 프로그램은 보고서를 HTML 형식으로 렌더링합니다. 완전한 형식의 HTML 페이지 또는 HTML 조각을 만들어 다른 HTML 페이지에 포함시킬 수도 있습니다. 모든 HTML은 UTF-8 인코딩을 사용하여 만들어집니다.<br /><br /> HTML 렌더링 확장 프로그램은 보고서 관리자에서 실행될 때를 포함하여 보고서 작성기에서 미리 보거나 브라우저에서 여는 보고서의 기본 렌더링 확장 프로그램입니다.<br /><br /> 자세한 내용은 [HTML로 렌더링&#40;보고서 작성기 및 SSRS&#41;](rendering-to-html-report-builder-and-ssrs.md)을 참조하세요.|  
|Acrobat(PDF) 파일|하드 페이지 나누기|PDF 렌더링 확장 프로그램은 Adobe Acrobat 및 PDF 1.3을 지원하는 타사 PDF 뷰어에서 열 수 있는 파일로 보고서를 렌더링합니다. PDF 1.3은 Adobe Acrobat 4.0 이상 버전과 호환되지만 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서는 Adobe Acrobat 6 이상 버전을 지원합니다. 이 렌더링 확장 프로그램으로 보고서를 렌더링하기 위해 Adobe 소프트웨어가 필요한 것은 아닙니다. 그러나 PDF 형식으로 보고서를 보거나 인쇄하기 위해서는 Adobe Acrobat과 같은 PDF 뷰어가 필요합니다.<br /><br /> 자세한 내용은 [PDF 파일로 내보내기&#40;보고서 작성기 및 SSRS&#41;](exporting-to-a-pdf-file-report-builder-and-ssrs.md)를 참조하세요.|  
|TIFF 파일|하드 페이지 나누기|이미지 렌더링 확장 프로그램은 보고서를 비트맵이나 메타파일로 렌더링합니다. 기본적으로 이미지 렌더링 확장 프로그램은 보고서를 여러 페이지로 볼 수 있도록 TIFF 파일로 만듭니다. 클라이언트가 이미지를 수신하면 이미지 뷰어에서 확인하거나 인쇄할 수 있습니다.<br /><br /> 이미지 렌더링 확장 프로그램에서 지 원하는 형식으로 파일을 생성할 수 [!INCLUDE[ndptecgdiplus](../../includes/ndptecgdiplus-md.md)]: BMP, EMF, EMFPlus, GIF, JPEG, PNG 및 TIFF입니다.<br /><br /> 자세한 내용은 [이미지 파일로 내보내기&#40;보고서 작성기 및 SSRS&#41;](exporting-to-an-image-file-report-builder-and-ssrs.md)를 참조하세요.|  
|XML|데이터|XML 렌더링 확장 프로그램은 보고서를 XML 형식으로 반환합니다. 보고서의 XML 스키마는 보고서마다 고유하며 데이터만 포함합니다. 레이아웃 정보는 렌더링되지 않으며 페이지 번호는 XML 렌더링 확장 프로그램을 통해 유지되지 않습니다. 이 확장 프로그램에서 생성된 XML은 데이터베이스로 가져오거나 XML 데이터 메시지로 사용하거나 사용자 지정 애플리케이션으로 전송할 수 있습니다.<br /><br /> 자세한 내용은 [XML로 내보내기&#40;보고서 작성기 및 SSRS&#41;](exporting-to-xml-report-builder-and-ssrs.md)를 참조하세요.|  
|Atom|data|Atom 렌더링 확장 프로그램은 보고서에서 Atom 규격 데이터 피드를 생성합니다. 데이터 피드는 Atom 규격 데이터 피드를 사용할 수 있는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 클라이언트와 같은 응용 프로그램을 통해 읽을 수 있고 교환할 수 있습니다.<br /><br /> 이 확장 프로그램의 출력 형식은 보고서에서 사용할 수 있는 데이터 피드를 나열하는 Atom 서비스 문서입니다. 이 문서에서는 보고서의 각 데이터 영역에 대한 데이터 피드가 하나 이상 생성되는데, 데이터 영역의 유형과 데이터 영역에 표시되는 데이터에 따라 여러 개의 데이터 피드가 생성될 수 있습니다.<br /><br /> 자세한 내용은 [보고서에서 데이터 피드 생성&#40;보고서 작성기 및 SSRS&#41;](generating-data-feeds-from-reports-report-builder-and-ssrs.md)을 참조하세요.|  
  
##  <a name="ExportingReport"></a> 보고서 내보내기  
 보고서를 내보내려면 보고서 관리자나 보고서 작성기에서 보고서를 실행한 다음 내보내기 드롭다운 목록에서 형식을 선택합니다. 파일을 저장할지, 아니면 열지를 선택하라는 메시지가 나타납니다. **열기**를 선택하면 선택한 렌더링 형식에 연결된 응용 프로그램에 보고서가 열립니다. 예를 들어 **Excel** 을 선택하면 보고서가 Excel에 열리고, **저장**을 선택하면 보고서가 저장됩니다. 예를 들어 Excel로 내보내는 경우 보고서가 .xls 파일로 저장됩니다. 로컬 컴퓨터에 정의된 파일 연결에 따라 특정 렌더링 형식에 사용되는 애플리케이션이 결정됩니다. 자세한 내용은 [다른 파일 형식으로 보고서 내보내기 &#40;보고서 작성기 및 SSRS&#41;](../export-a-report-as-another-file-type-report-builder-and-ssrs.md)합니다.  
  
 보고서 서버에서는 현재 사용자 세션의 상태 그대로 보고서를 내보냅니다. 보고서를 연 상태에서 다른 사용자가 보고서의 업데이트된 버전을 게시하거나 보고서에 표시되는 데이터가 변경되더라도 내보낸 보고서는 업데이트되지 않습니다.  
  
 보고서를 다른 형식으로 내보낼 때 보고서 페이지 매김이 영향을 받을 수 있습니다. 보고서를 미리 볼 때는 소프트 페이지 나누기 규칙을 따르는 HTML 렌더링 확장 프로그램에 의해 렌더링된 보고서가 표시됩니다. 보고서를 Adobe Acrobat(PDF)과 같은 다른 파일 형식으로 내보낼 때는 실제 페이지 크기를 기준으로, 즉 하드 페이지 나누기 규칙에 따라 페이지 매김이 결정됩니다. 보고서에 추가한 논리적 페이지 나누기에 따라 페이지가 나뉠 수 있지만 페이지의 실제 길이는 어떤 종류의 렌더러를 사용하는가에 따라 달라집니다. 보고서 페이지 매김을 변경하려면 선택한 렌더링 확장 프로그램의 페이지 매김 동작에 대해 잘 알고 있어야 합니다. 해당 렌더링 확장 프로그램에 맞게 보고서 레이아웃 디자인을 조정해야 할 수도 있습니다. 자세한 내용은 [페이지 레이아웃 및 렌더링&#40;보고서 작성기 및 SSRS&#41;](../report-design/page-layout-and-rendering-report-builder-and-ssrs.md)을 참조하세요.  
  
##  <a name="GeneratingDataFeedsFromReport"></a> 보고서에서 데이터 피드 생성  
 보고서에서 데이터 피드를 생성하려면 보고서 관리자에서 보고서를 실행한 다음 보고서 관리자 도구 모음에서 **데이터 피드 생성** 아이콘을 클릭합니다. 파일을 저장할지, 아니면 열지를 선택하라는 메시지가 나타납니다. **열기**를 선택하면 .atomsvc 파일 확장명과 연결된 응용 프로그램에서 Atom 서비스 문서가 열리고, **저장**을 선택하면 문서가 .atomsvc 파일로 저장됩니다. 기본적으로 이 파일의 이름은 보고서의 이름입니다. 이 이름은 보다 의미 있는 이름으로 변경할 수 있습니다.  
  
 Atom 서비스 문서를 컴퓨터에 저장한 후 나중에 다른 사용자가 사용할 수 있도록 보고서 서버나 다른 서버에 업로드할 수 있습니다. 자세한 내용은 [보고서에서 데이터 피드 생성&#40;보고서 작성기 및 SSRS&#41;](generating-data-feeds-from-reports-report-builder-and-ssrs.md) 및 [보고서에서 데이터 피드 생성&#40;보고서 작성기 및 SSRS&#41;](generate-data-feeds-from-a-report-report-builder-and-ssrs.md)을 참조하세요.  
  
##  <a name="Troubleshooting"></a> 내보낸 보고서의 문제 해결  
 보고서를 다른 형식으로 내보낸 후 보고서가 다르게 표시되거나 원하는 대로 동작하지 않는 경우가 있습니다. 이 문제는 렌더러에 몇 가지 규칙 및 제한 사항이 적용되기 때문일 수 있습니다. 보고서를 만들 때 이러한 제한 사항을 고려하면 대부분의 문제를 해결할 수 있습니다. 보고서에서 약간 다른 레이아웃을 사용하거나, 보고서 내의 항목을 주의해서 맞추거나, 보고서 바닥글을 한 줄 텍스트로 제한하는 등의 작업이 필요할 수 있습니다.  
  
 보고서에 아라비아 숫자가 포함된 유니코드 텍스트 또는 아랍어로 된 날짜가 포함되는 경우, 다음 형식으로 보고서를 내보내거나 보고서를 인쇄할 때 날짜와 숫자가 올바르게 렌더링되지 않습니다.  
  
-   PDF  
  
-   Word  
  
-   내보내기  
  
-   Image/TIFF  
  
 보고서를 HTML로 내보내는 경우, 날짜와 숫자가 올바르게 렌더링됩니다.  
  
 특정 렌더러에 대한 항목에서는 보고서 항목 및 데이터 영역이 렌더링되는 방식과 각 렌더러에 대한 제한 사항 및 이를 해결 방법에 대해 설명합니다.  
  
-   [CSV 파일로 내보내기&#40;보고서 작성기 및 SSRS&#41;](exporting-to-a-csv-file-report-builder-and-ssrs.md)  
  
-   [Microsoft Excel로 내보내기&#40;보고서 작성기 및 SSRS&#41;](exporting-to-microsoft-excel-report-builder-and-ssrs.md)  
  
-   [Microsoft Word로 내보내기&#40;보고서 작성기 및 SSRS&#41;](exporting-to-microsoft-word-report-builder-and-ssrs.md)  
  
-   [HTML로 렌더링&#40;보고서 작성기 및 SSRS&#41;](rendering-to-html-report-builder-and-ssrs.md)  
  
-   [PDF 파일로 내보내기&#40;보고서 작성기 및 SSRS&#41;](exporting-to-a-pdf-file-report-builder-and-ssrs.md)  
  
-   [이미지 파일로 내보내기&#40;보고서 작성기 및 SSRS&#41;](exporting-to-an-image-file-report-builder-and-ssrs.md)  
  
-   [XML로 내보내기&#40;보고서 작성기 및 SSRS&#41;](exporting-to-xml-report-builder-and-ssrs.md)  
  
-   [보고서에서 데이터 피드 생성&#40;보고서 작성기 및 SSRS&#41;](generating-data-feeds-from-reports-report-builder-and-ssrs.md)  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서는 다른 형식에서도 제대로 작동하는 보고서를 만드는 데 유용한 추가 기능을 제공합니다. 테이블릭스 데이터 영역(테이블, 행렬, 목록), 그룹 및 사각형에 페이지 나누기를 적용하면 보고서 페이지 매김을 보다 효율적으로 제어할 수 있습니다. 페이지 나누기로 구분된 보고서 페이지에는 각각 다른 페이지 이름을 적용하고 페이지 번호 매기기를 다시 설정할 수 있습니다. 식을 사용하면 보고서를 실행할 때 페이지 이름 및 페이지 번호를 동적으로 업데이트할 수 있습니다. 자세한 내용은 [Reporting Services의 페이지 매김&#40;보고서 작성기 및 SSRS&#41;](../report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)을 참조하세요.  
  
 또한 기본 제공 전역 변수인 RenderFormat을 사용하면 조건에 따라 렌더러마다 각기 다른 보고서 레이아웃을 적용할 수 있습니다. 자세한 내용은 [기본 제공 Globals 및 Users 참조&#40;보고서 작성기 및 SSRS&#41;](../report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)를 참조하세요.  
  
##  <a name="OtherWaysExportingReports"></a> 보고서를 내보내는 다른 방법  
 보고서 내보내기는 보고서가 보고서 관리자나 보고서 작성기에 열려 있을 때 사용자가 수행하는 요청 시 태스크입니다. 되풀이 일정에서 특정 파일 형식으로 공유 폴더에 보고서를 내보내려는 경우와 같이 내보내기 작업을 자동화하려면 보고서를 공유 폴더로 배달하는 구독을 만듭니다. 자세한 내용은 [File Share Delivery in Reporting Services](../subscriptions/file-share-delivery-in-reporting-services.md)을 참조하세요.  
  
 보고서 작성 도구에서 미리 보거나 보고서 관리자와 같은 브라우저 애플리케이션에서 여는 보고서는 항상 HTML로 먼저 렌더링됩니다. 다른 렌더링 확장 프로그램을 보고서를 표시하는 기본 프로그램으로 지정할 수 없습니다. 그러나 이후에 받은 편지함이나 공유 폴더로 배달할 때 사용할 렌더링 형식으로 보고서를 생성하는 구독을 만들 수 있습니다. 자세한 내용은 참조 하세요. [Create, Modify, and 표준 구독 삭제 &#40;기본 모드의 Reporting Services&#41; ](../subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md) 및 [만들기, 수정 및 데이터 기반 구독 삭제](../subscriptions/data-driven-subscriptions.md).  
  
 렌더링 확장 프로그램을 URL 매개 변수로 지정하는 URL을 통해 보고서에 액세스한 후 보고서를 HTML로 먼저 렌더링하지 않고 지정된 형식으로 직접 렌더링할 수도 있습니다. 다음 예에서는 보고서를 Excel 형식으로 렌더링합니다.  
  
```  
http://<Server Name>/reportserver?/Sales/YearlySalesSummary&rs:Format=Excel&rs:Command=Render  
```  
  
 자세한 내용은 [Export a Report Using URL Access](../export-a-report-using-url-access.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [페이지 나누기, 머리글, 열 및 행 제어&#40;보고서 작성기 및 SSRS&#41;](../report-design/controlling-page-breaks-headings-columns-and-rows-report-builder-and-ssrs.md)   
 [보고서 찾기, 보기 및 관리&#40;보고서 작성기 및 SSRS&#41;](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [보고서 인쇄&#40;보고서 작성기 및 SSRS&#41;](print-reports-report-builder-and-ssrs.md)   
 [보고서 저장&#40;보고서 작성기&#41;](saving-reports-report-builder.md)  
  
  
