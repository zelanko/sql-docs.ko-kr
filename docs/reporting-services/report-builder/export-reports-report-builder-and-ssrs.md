---
title: 보고서 내보내기(보고서 작성기 및 SSRS) | Microsoft Docs
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
f1_keywords:
- "10437"
ms.assetid: a2bab8c1-505d-4da3-b1db-ea0ae13b2336
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5be30a3d5a7461c728bdcf67b5de07a18d929704
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53211259"
---
# <a name="export-reports-report-builder-and-ssrs"></a>보고서 내보내기(보고서 작성기 및 SSRS)

  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서를 PowerPoint, Image, PDF, [!INCLUDE[ofprword](../../includes/ofprword-md.md)], [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 등의 다른 파일 형식으로 내보낼 수도 있고, Atom 서비스 문서를 생성해 보고서를 내보내서 보고서에서 사용 가능한 Atom 규격 데이터 피드 목록을 표시할 수도 있습니다. 보고서 작성기, 보고서 디자이너([!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]) 또는 보고서 서버에서 보고서를 내보낼 수 있습니다.  
  
 보고서를 내보내면 다음을 수행할 수 있습니다.  
  
-   **다른 애플리케이션에서 보고서 데이터로 작업.** 예를 들어 보고서를 Excel로 내보낸 다음 Excel에서 해당 데이터를 사용하여 계속 작업할 수 있습니다.  
  
-   **다른 형식으로 보고서 인쇄.** 예를 들어 보고서를 PDF 파일 형식으로 내보낸 다음 인쇄할 수 있습니다.  
  
-   **다른 파일 유형으로 보고서 복사본 저장.** 예를 들어 보고서의 복사본을 만들어 Word로 내보낸 다음 저장할 수 있습니다.  
  
-   **애플리케이션에서 보고서 데이터를 데이터 피드로 사용.** 예를 들어 파워 피벗 또는 Power BI에서 사용할 수 있는 Atom 규격 데이터 피드를 생성한 다음 파워 피벗 또는 Power BI에서 이 데이터로 작업할 수 있습니다. 자세한 내용은 [보고서에서 데이터 피드 생성](../../reporting-services/report-builder/generate-data-feeds-from-a-report-report-builder-and-ssrs.md)을 참조하세요.  
  
-   보고서 서버에서 보고서를 렌더링하면 구독을 설정하려는 경우나 전자 메일을 통해 보고서를 배달하려는 경우 또는 보고서 서버에서 사용할 수 있도록 보고서를 저장하려는 경우에 도움이 됩니다. 자세한 내용은 [구독 및 배달&#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)을 참조하세요.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서는 보고서를 일반 파일 형식으로 내보낼 수 있도록 하는 다양한 렌더링 확장 프로그램을 제공합니다. 렌더링 확장 프로그램은 소프트 페이지 나누기를 사용하는 파일 형식(예: Word 또는 Excel), 하드 페이지 나누기를 사용하는 파일 형식(예: PDF 또는 TIFF) 또는 데이터만 있는 파일 형식(예: CSV 또는 Atom 호환 XML)을 지원합니다.  
  
 보고서를 다른 형식으로 내보낼 때 보고서 페이지 매김이 영향을 받을 수 있습니다. 보고서를 미리 볼 때는 소프트 페이지 나누기 규칙을 따르는 HTML 렌더링 확장 프로그램에 의해 렌더링된 보고서가 표시됩니다. 보고서를 Adobe Acrobat(PDF)과 같은 다른 파일 형식으로 내보낼 때는 실제 페이지 크기를 기준으로, 즉 하드 페이지 나누기 규칙에 따라 페이지 매김이 결정됩니다. 보고서에 추가한 논리적 페이지 나누기에 따라 페이지가 나뉠 수 있지만 페이지의 실제 길이는 어떤 종류의 렌더러를 사용하는가에 따라 달라집니다. 보고서 페이지 매김을 변경하려면 선택한 렌더링 확장 프로그램의 페이지 매김 동작에 대해 잘 알고 있어야 합니다. 해당 렌더링 확장 프로그램에 맞게 보고서 레이아웃 디자인을 조정해야 할 수도 있습니다. 자세한 내용은 [페이지 레이아웃 및 렌더링](../../reporting-services/report-design/page-layout-and-rendering-report-builder-and-ssrs.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]

## <a name="bkmk_export_from_rb"></a> 보고서 작성기에서 보고서를 내보내려면

1.  보고서를 실행하거나 미리 봅니다.  
  
2.  리본에서 **내보내기**를 클릭합니다.  
  
     ![보고서 작성기 내보내기](../../reporting-services/report-builder/media/ssrb-export.png "보고서 작성기 내보내기")  
  
3.  사용할 형식을 선택합니다.  
  
     **다른 이름으로 저장** 대화 상자가 열립니다. 기본적으로 파일 이름은 내보낸 보고서의 이름입니다. 필요한 경우 파일 이름을 변경할 수 있습니다.  
  
##  <a name="bkmk_export_from_rm"></a>[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 웹 포털에서 보고서를 내보내려면  
  
1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 웹 포털 **홈** 페이지에서 내보낼 보고서로 이동합니다.  
  
2.  보고서를 클릭하여 렌더링하고 미리 봅니다.  
  
3.  보고서 뷰어 도구 모음에서 **내보내기** 드롭다운 화살표를 클릭합니다.  
  
     ![Reporting Services 웹 포털 내보내기](../../reporting-services/report-builder/media/ssrsportal-export.png "Reporting Services 웹 포털 내보내기")  
  
4.  사용할 형식을 선택합니다.  
  
5.  **내보내기**를 클릭합니다. 파일을 열지 아니면 저장할지를 묻는 대화 상자가 나타납니다.  
  
6.  선택한 내보내기 형식으로 보고서를 보려면 **열기**를 클릭합니다.  
  
     \- 또는-  
  
     선택한 내보내기 형식으로 보고서를 즉시 저장하려면 **저장**을 클릭합니다.  
  
     선택한 형식에 연결되어 있는 애플리케이션을 사용하여 보고서가 표시 또는 저장됩니다. **저장**을 클릭하면 보고서를 저장할 위치를 묻는 메시지가 나타납니다.  
  
##  <a name="bkmk_export_from_sharepoint"></a> SharePoint 라이브러리에서 보고서를 내보내려면  
  
1.  보고서를 미리 봅니다.  
  
2.  도구 모음에서 **동작**을 클릭하고 **내보내기**를 가리킨 다음 사용할 형식을 선택합니다.  
  
     **파일 다운로드** 대화 상자가 열립니다.  
  
3.  선택한 내보내기 형식으로 보고서를 보려면 **열기**를 클릭합니다.  
  
     \- 또는-  
  
     선택한 내보내기 형식으로 보고서를 즉시 저장하려면 **저장**을 클릭합니다.  
  
     선택한 형식에 연결되어 있는 애플리케이션을 사용하여 보고서가 표시 또는 저장됩니다. **저장**을 클릭하면 보고서를 저장할 위치를 묻는 메시지가 나타납니다.  
  
     필요한 경우 내보낸 보고서의 파일 이름을 변경합니다.  
  
     **참고** 선택한 파일 형식에 연결된 프로그램이 없어서 지정된 형식으로 보고서를 열 수 없는 경우에는 내보낸 보고서를 저장하거나 보고서를 여는 데 필요한 프로그램을 온라인으로 찾으라는 메시지가 나타납니다.  
  
##  <a name="RendererTypes"></a> 렌더링 확장 프로그램 유형  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 렌더링 확장 프로그램에는 다음 세 가지 유형이 있습니다.  
  
-   **데이터 렌더링 확장 프로그램** 데이터 렌더링 확장 프로그램은 보고서에서 서식 및 레이아웃 정보를 모두 제거하고 데이터만 표시합니다. 이렇게 내보낸 파일은 Excel 같은 다른 파일 형식, 다른 데이터베이스, XML 데이터 메시지 또는 사용자 지정 애플리케이션으로 원시 보고서 데이터를 가져오는 데 사용할 수 있습니다. 데이터 렌더링 확장 프로그램은 페이지 나누기를 지원하지 않습니다.  
  
     지원되는 데이터 렌더링 확장 프로그램은 CSV, XML 및 Atom입니다.  
  
-   **소프트 페이지 나누기 렌더러 확장 프로그램** 소프트 페이지 나누기 렌더링 확장 프로그램에서는 보고서 레이아웃과 서식이 유지됩니다. 이렇게 내보낸 파일은 웹 페이지나 **ReportViewer** 컨트롤 같은 화면 중심의 보기 및 배달용으로 최적화됩니다.  
  
     지원되는 소프트 페이지 나누기 렌더링 확장 프로그램은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word 및 MHTML(웹 보관 파일)입니다.  
  
-   **하드 페이지 나누기 렌더링 확장 프로그램** 하드 페이지 나누기 렌더러 확장 프로그램에서는 보고서 레이아웃과 서식이 유지됩니다. 생성되는 파일은 인쇄 환경을 일정하게 유지하거나 온라인에서 책 형태로 보고서를 볼 수 있도록 최적화됩니다.  
  
     지원되는 하드 페이지 나누기 렌더링 확장 프로그램은 TIFF와 PDF입니다.  
  
##  <a name="ExportFormats"></a> 보고서를 보는 중에 내보낼 수 형식  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서는 다양한 형식으로 보고서를 렌더링하는 렌더링 확장 프로그램을 제공합니다. 선택한 파일 형식에 맞게 보고서 디자인을 최적화해야 합니다.  다음 표에는 사용자 인터페이스에서 내보낼 수 형식이 나와 있습니다.  URL에 액세스하여 내보내는 경우 또는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구독에서 내보내는 경우에는 추가 형식을 사용할 수 있습니다.  이 항목의 [보고서를 내보내는 다른 방법](#OtherWaysExportingReports)섹션을 참조하세요.  
  
|형식|렌더링 확장 프로그램 유형|설명|  
|------------|------------------------------|-----------------|  
|Acrobat(PDF) 파일|하드 페이지 나누기|PDF 렌더링 확장 프로그램은 Adobe Acrobat 및 PDF 1.3을 지원하는 타사 PDF 뷰어에서 열 수 있는 파일로 보고서를 렌더링합니다. PDF 1.3은 Adobe Acrobat 4.0 이상 버전과 호환되지만 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서는 Adobe Acrobat 6 이상 버전을 지원합니다. 이 렌더링 확장 프로그램으로 보고서를 렌더링하기 위해 Adobe 소프트웨어가 필요한 것은 아닙니다. 그러나 PDF 형식으로 보고서를 보거나 인쇄하기 위해서는 Adobe Acrobat과 같은 PDF 뷰어가 필요합니다.<br /><br /> 자세한 내용은 [PDF 파일로 내보내기](../../reporting-services/report-builder/exporting-to-a-pdf-file-report-builder-and-ssrs.md)를 참조하세요.|  
|Atom|data|Atom 렌더링 확장 프로그램은 보고서에서 Atom 규격 데이터 피드를 생성합니다. 데이터 피드는 Atom 규격 데이터 피드를 사용할 수 있는 파워 피벗 또는 Power BI와 같은 애플리케이션을 통해 읽을 수 있고 교환할 수 있습니다.<br /><br /> 이 확장 프로그램의 출력 형식은 보고서에서 사용할 수 있는 데이터 피드를 나열하는 Atom 서비스 문서입니다. 이 문서에서는 보고서의 각 데이터 영역에 대한 데이터 피드가 하나 이상 생성되는데, 데이터 영역의 유형과 데이터 영역에 표시되는 데이터에 따라 여러 개의 데이터 피드가 생성될 수 있습니다.<br /><br /> 자세한 내용은 [보고서에서 데이터 피드 생성](../../reporting-services/report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md)을 참조하세요.|  
|CSV|data|CSV(쉼표로 구분된 값) 렌더링 확장 프로그램은 보고서의 데이터를 결합하여 읽기 쉽고 많은 애플리케이션과 교환할 수 있는 표준화된 일반 텍스트 형식으로 렌더링합니다.<br /><br /> 자세한 내용은 [CSV 파일로 내보내기](../../reporting-services/report-builder/exporting-to-a-csv-file-report-builder-and-ssrs.md)를 참조하세요.|  
|EXCELOPENXML|소프트 페이지 나누기|보고서를 검토할 때 내보내기 메뉴에 "Excel"로 표시됩니다. Excel 렌더링 확장 프로그램은 보고서를 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2013과 호환되는 Excel 문서(.xlsx)로 렌더링합니다.  자세한 내용은 [Microsoft Excel로 내보내기](../../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md)를 참조하세요.|  
|PowerPoint|하드 페이지 나누기|PowerPoint 렌더링 확장 프로그램은 보고서를 PowerPoint 2013과 호환되는 PowerPoint 문서(.pptx)로 렌더링합니다.|  
|TIFF 파일|하드 페이지 나누기|이미지 렌더링 확장 프로그램은 보고서를 비트맵이나 메타파일로 렌더링합니다. 기본적으로 이미지 렌더링 확장 프로그램은 보고서를 여러 페이지로 볼 수 있도록 TIFF 파일로 만듭니다. 클라이언트가 이미지를 수신하면 이미지 뷰어에서 확인하거나 인쇄할 수 있습니다.<br /><br /> 이미지 렌더링 확장 프로그램은 [!INCLUDE[ndptecgdiplus](../../includes/ndptecgdiplus-md.md)]에서 지원하는 BMP, EMF, EMFPlus, GIF, JPEG, PNG 및 TIFF 형식으로 파일을 생성할 수 있습니다.<br /><br /> 자세한 내용은 [이미지 파일로 내보내기](../../reporting-services/report-builder/exporting-to-an-image-file-report-builder-and-ssrs.md)를 참조하세요.|  
|웹 보관 파일|소프트 페이지 나누기|HTML 렌더링 확장 프로그램은 보고서를 HTML 형식으로 렌더링합니다. 완전한 형식의 HTML 페이지 또는 HTML 조각을 만들어 다른 HTML 페이지에 포함시킬 수도 있습니다. 모든 HTML은 UTF-8 인코딩을 사용하여 만들어집니다.<br /><br /> HTML 렌더링 확장 프로그램은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 웹 포털에서 실행될 때를 포함하여 보고서 작성기에서 미리 보거나 브라우저에서 보는 보고서의 기본 렌더링 확장 프로그램입니다.<br /><br /> 자세한 내용은 [HTML로 렌더링](../../reporting-services/report-builder/rendering-to-html-report-builder-and-ssrs.md)을 참조하세요.|  
|WORDOPENXML|소프트 페이지 나누기|보고서를 볼 때 내보내기 메뉴에 "Word"로 표시됩니다. Word 렌더링 확장 프로그램은 보고서를 [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2013과 호환되는 Word 문서(.docx)로 렌더링합니다.  자세한 내용은 [Microsoft Word로 내보내기](../../reporting-services/report-builder/exporting-to-microsoft-word-report-builder-and-ssrs.md)를 참조하세요.|  
|XML|데이터|XML 렌더링 확장 프로그램은 보고서를 XML 형식으로 반환합니다. 보고서의 XML 스키마는 보고서마다 고유하며 데이터만 포함합니다. 레이아웃 정보는 렌더링되지 않으며 페이지 번호는 XML 렌더링 확장 프로그램을 통해 유지되지 않습니다. 이 확장 프로그램에서 생성된 XML은 데이터베이스로 가져오거나 XML 데이터 메시지로 사용하거나 사용자 지정 애플리케이션으로 전송할 수 있습니다.<br/><br/> 자세한 내용은 [XML로 내보내기](../../reporting-services/report-builder/exporting-to-xml-report-builder-and-ssrs.md)를 참조하세요.|  
  
##  <a name="GeneratingDataFeedsFromReport"></a> 보고서에서 데이터 피드 생성  
 보고서에서 데이터 피드를 생성하려면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 웹 포털에서 보고서를 실행한 다음 웹 포털 도구 모음에서 **데이터 피드 생성** 아이콘을 클릭합니다. 파일을 저장할지, 아니면 열지를 선택하라는 메시지가 나타납니다. **열기**를 선택하면 .atomsvc 파일 확장명과 연결된 애플리케이션에서 Atom 서비스 문서가 열리고, **저장**을 선택하면 문서가 .atomsvc 파일로 저장됩니다. 기본적으로 이 파일의 이름은 보고서의 이름입니다. 이 이름은 보다 의미 있는 이름으로 변경할 수 있습니다.  
  
 Atom 서비스 문서를 컴퓨터에 저장한 후 나중에 다른 사용자가 사용할 수 있도록 보고서 서버나 다른 서버에 업로드할 수 있습니다. 자세한 내용은 [보고서에서 데이터 피드 생성](../../reporting-services/report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md) 및 [보고서에서 데이터 피드 생성](../../reporting-services/report-builder/generate-data-feeds-from-a-report-report-builder-and-ssrs.md)을 참조하세요.  
  
##  <a name="Troubleshooting"></a> 내보낸 보고서의 문제 해결  
 보고서를 다른 형식으로 내보낸 후 보고서가 다르게 표시되거나 원하는 대로 동작하지 않는 경우가 있습니다. 이 문제는 렌더러에 몇 가지 규칙 및 제한 사항이 적용되기 때문일 수 있습니다. 보고서를 만들 때 이러한 제한 사항을 고려하면 대부분의 문제를 해결할 수 있습니다. 보고서에서 약간 다른 레이아웃을 사용하거나, 보고서 내의 항목을 주의해서 맞추거나, 보고서 바닥글을 한 줄 텍스트로 제한하는 등의 작업이 필요할 수 있습니다.  
  
 보고서에 아라비아 숫자가 포함된 유니코드 텍스트 또는 아랍어로 된 날짜가 포함되는 경우, 다음 형식으로 보고서를 내보내거나 보고서를 인쇄할 때 날짜와 숫자가 올바르게 렌더링되지 않습니다.  
  
-   PDF  
  
-   Word  
  
-   내보내기  
  
-   Image/TIFF  
  
 보고서를 HTML로 내보내는 경우, 날짜와 숫자가 올바르게 렌더링됩니다.  
  
 특정 렌더러에 대한 항목에서는 보고서 항목 및 데이터 영역이 렌더링되는 방식과 각 렌더러에 대한 제한 사항 및 이를 해결 방법에 대해 설명합니다.  
  
-   [CSV 파일로 내보내기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/exporting-to-a-csv-file-report-builder-and-ssrs.md)  
  
-   [Microsoft Excel로 내보내기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md)  
  
-   [Microsoft Word로 내보내기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/exporting-to-microsoft-word-report-builder-and-ssrs.md)  
  
-   [HTML로 렌더링&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/rendering-to-html-report-builder-and-ssrs.md)  
  
-   [PDF 파일로 내보내기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/exporting-to-a-pdf-file-report-builder-and-ssrs.md)  
  
-   [이미지 파일로 내보내기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/exporting-to-an-image-file-report-builder-and-ssrs.md)  
  
-   [XML로 내보내기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/exporting-to-xml-report-builder-and-ssrs.md)  
  
-   [보고서에서 데이터 피드 생성&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md)  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서는 다른 형식에서도 제대로 작동하는 보고서를 만드는 데 유용한 추가 기능을 제공합니다. 테이블릭스 데이터 영역(테이블, 행렬, 목록), 그룹 및 사각형에 페이지 나누기를 적용하면 보고서 페이지 매김을 보다 효율적으로 제어할 수 있습니다. 페이지 나누기로 구분된 보고서 페이지에는 각각 다른 페이지 이름을 적용하고 페이지 번호 매기기를 다시 설정할 수 있습니다. 식을 사용하면 보고서를 실행할 때 페이지 이름 및 페이지 번호를 동적으로 업데이트할 수 있습니다. 자세한 내용은 [Reporting Services의 페이지 매김](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)을 참조하세요.  
  
 또한 기본 제공 전역 변수인 RenderFormat을 사용하면 조건에 따라 렌더러마다 각기 다른 보고서 레이아웃을 적용할 수 있습니다. 자세한 내용은 [기본 제공 Globals 및 Users 참조](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)를 참조하세요.

##  <a name="OtherWaysExportingReports"></a> 보고서를 내보내는 다른 방법  
 보고서 내보내기는 보고서가 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 웹 포털이나 보고서 작성기에 열려 있을 때 사용자가 수행하는 요청 시 태스크입니다. 되풀이 일정에서 특정 파일 형식으로 공유 폴더에 보고서를 내보내려는 경우와 같이 내보내기 작업을 자동화하려면 보고서를 공유 폴더로 배달하는 구독을 만듭니다. 자세한 내용은 [File Share Delivery in Reporting Services](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md)을 참조하세요.  
  
 보고서 작성 도구에서 미리 보거나 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 웹 포털과 같은 브라우저 애플리케이션에서 여는 보고서는 항상 HTML로 먼저 렌더링됩니다. 다른 렌더링 확장 프로그램을 보고서를 표시하는 기본 프로그램으로 지정할 수 없습니다. 그러나 이후에 받은 편지함이나 공유 폴더로 배달할 때 사용할 렌더링 형식으로 보고서를 생성하는 구독을 만들 수 있습니다. 자세한 내용은 [기본 모드 보고서 서버 구독 만들기 및 관리](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md) 및 [데이터 기반 구독 만들기, 수정 및 삭제](../../reporting-services/subscriptions/create-modify-and-delete-data-driven-subscriptions.md)를 참조하세요.  
  
 렌더링 확장 프로그램을 URL 매개 변수로 지정하는 URL을 통해 보고서에 액세스한 후 보고서를 HTML로 먼저 렌더링하지 않고 지정된 형식으로 직접 렌더링할 수도 있습니다. 다음 예에서는 보고서를 Excel 형식으로 렌더링합니다.  
  
```  
https://<Report Server Name>/reportserver?/Sales/YearlySalesSummary&rs:Format=Excel&rs:Command=Render  
```  
  
 그리고 다음 예에서는 명명된 인스턴스에서 PowerPoint 보고서를 렌더링합니다.  
  
```  
https://<Report Server Name/ReportServer_THESQLINSTANCE/Pages/ReportViewer.aspx?%2freportfolder%2freport+name+with+spaces&rs:Format=pptx  
```  
  
 자세한 내용은 [Export a Report Using URL Access](../../reporting-services/export-a-report-using-url-access.md)를 참조하세요.  

## <a name="next-steps"></a>다음 단계

[페이지 나누기, 머리글, 열 및 행 제어&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/controlling-page-breaks-headings-columns-and-rows-report-builder-and-ssrs.md)   
[보고서 찾기, 보기 및 관리&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
[보고서 인쇄&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)   
[보고서 저장&#40;보고서 작성기&#41;](../../reporting-services/report-builder/saving-reports-report-builder.md)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)
