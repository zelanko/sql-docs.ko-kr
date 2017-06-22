---
title: "여러 보고서 렌더링 확장 프로그램의 대화형 기능-| Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f0bd1c4c-e8b5-467f-b5a1-541f19c7e3e2
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 9a422c1619ae284ec49643465bd8b84efda1910b
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="interactive-functionality---different-report-rendering-extensions"></a>여러 보고서 렌더링 확장 프로그램의 대화형 기능-
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 런타임 시 페이지를 매긴 보고서와 상호 작용하기 위한 기능을 제공합니다. 모든 보고서 렌더링 형식에 대화형 기능을 전부 사용할 수 있는 것은 아닙니다. 다음 표에는 각 대화형 기능이 특정 형식에서 어떻게 작동하는지 이해하는 데 도움이 되는 정보가 나와 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="interactive-features-in-different-output-formats"></a>여러 출력 형식에서의 대화형 기능  
 XML, CSV 또는 이미지 형식으로 렌더링되는 페이지를 매긴 보고서는 대화형 기능을 지원하지 않습니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 웹 포털, SharePoint 웹 파트 또는 브라우저에 표시되는 보고서는 HTML로 렌더링됩니다. HTML과 Windows Forms은 모든 대화형 기능을 완벽하게 지원하는 유일한 보고서 출력 형식입니다. MHTML과 같은 대체 HTML 형식은 많은 대화형 기능을 지원합니다. MHTML에 대한 예외가 있는 경우 다음 표에서 설명합니다.  
  
### <a name="document-maps"></a>문서 구조  
  
|내보내기 옵션|지원 정보|  
|-------------------|-------------------------|  
|미리 보기/보고서 뷰어, HTML|대화형 문서 구조는 보고서의 다양한 섹션으로 이동하는 데 사용할 수 있는 계층적 링크가 포함된 탐색 창을 제공합니다.|  
|PDF|PDF는 문서 구조를 책갈피 창으로 렌더링합니다. 문서 구조의 모든 항목이 위에서부터 차례로 창에 나열됩니다. 여기에는 링크의 계층 구조가 포함됩니다. 페이지 범위를 지정한 경우 렌더링된 책갈피만 계층 구조에 포함됩니다.|  
|Excel|Excel은 문서 구조를 통합 문서의 첫째 워크시트로 렌더링합니다. 여기에는 링크의 계층 구조가 포함됩니다. 문서 구조의 링크를 클릭하면 그에 해당하는 워크시트의 적절한 대상 셀이 열립니다.|  
|Word|Word에서는 문서 구조를 목차 레이블로 렌더링합니다.|  
|기타(예: TIFF, XML 및 CSV)|MHTML, XML, CSV 또는 이미지에서는 사용할 수 없습니다.|  
  
### <a name="drillthrough-links-to-other-reports"></a>다른 보고서에 대한 드릴스루 링크  
  
|내보내기 옵션|지원 정보|  
|-------------------|-------------------------|  
|미리 보기/보고서 뷰어, HTML|보고서의 데이터 값을 클릭하여 다른 보고서의 관련 데이터를 볼 수 있습니다.|  
|PDF|PDF에는 드릴스루 링크를 사용할 수 없습니다. 다른 페이지에 링크되는 PDF 보고서에 대해서는 하이퍼링크를 사용하십시오.|  
|Excel|드릴스루 링크는 Excel에서 렌더링됩니다.<br /><br /> 해당 링크는 드릴스루 링크가 참조하는 보고서를 가리키는 하이퍼링크가 됩니다. 링크를 클릭하면 브라우저 창에 보고서가 열립니다.|  
|Word|드릴스루 링크는 Word에서 렌더링됩니다.<br /><br /> 해당 링크는 드릴스루 링크가 참조하는 보고서를 가리키는 하이퍼링크가 됩니다. 링크를 클릭하면 브라우저 창에 보고서가 열립니다.|  
|기타|XML, CSV 또는 이미지에서는 사용할 수 없습니다.|  
  
### <a name="toggle-items-within-a-report"></a>보고서 내의 설정/해제 항목  
  
|내보내기 옵션|지원 정보|  
|-------------------|-------------------------|  
|미리 보기/보고서 뷰어, HTML|확장 및 축소 아이콘을 클릭하여 보고서의 섹션을 볼 수 있습니다.|  
|PDF|보고서 서버에서는 보고서의 현재 표시 또는 숨김 상태를 PDF로 내보냅니다. 대화형 설정/해제는 지원되지 않습니다.|  
|Excel|설정/해제할 수 있는 항목과 드릴다운 링크는 Excel에서 축소 가능한 윤곽선으로 렌더링됩니다. 보고서의 섹션을 확장하고 축소할 수 있습니다. Excel 관련 제한 사항에 대한 자세한 내용은 [Microsoft Excel로 내보내기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md)를 참조하세요.|  
|Word|보고서 서버에서는 보고서의 현재 표시 또는 숨김 상태를 PDF로 내보냅니다. 대화형 설정/해제는 지원되지 않습니다.|  
|기타|MHTML, XML 또는 CSV에서는 사용할 수 없습니다. 이미지 형식으로 내보내는 경우 보고서 서버에서는 보고서의 현재 표시 또는 숨김 상태를 PDF로 내보냅니다. 대화형 설정/해제는 지원되지 않습니다.|  
  
### <a name="interactive-sorting"></a>대화형 정렬  
  
|내보내기 옵션|지원 정보|  
|-------------------|-------------------------|  
|미리 보기/보고서 뷰어, HTML|테이블 형식 보고서의 경우 열에 있는 정렬 화살표를 클릭하여 데이터 정렬 방법을 변경할 수 있습니다.|  
|PDF|PDF에서는 사용할 수 없습니다.|  
|Excel|Excel에서는 사용할 수 없습니다.|  
|Word|Word에서는 사용할 수 없습니다.|  
|기타|MHTML, XML, CSV 또는 이미지에서는 사용할 수 없습니다.|  
  
### <a name="hyperlinks-to-external-web-content-or-images"></a>외부 웹 콘텐츠 또는 이미지에 대한 하이퍼링크  
  
|내보내기 옵션|지원 정보|  
|-------------------|-------------------------|  
|미리 보기/보고서 뷰어, HTML|링크를 클릭하여 새 브라우저 창에서 외부 웹 페이지를 열 수 있습니다.|  
|PDF|하이퍼링크는 PDF 렌더링 확장 프로그램에서 렌더링됩니다. 사용자가 하이퍼링크를 클릭하면 링크된 페이지가 브라우저에 열립니다.|  
|Excel|하이퍼링크는 Excel에서 렌더링됩니다.|  
|Word|하이퍼링크는 Word에서 렌더링됩니다.|  
|기타|MHTML, XML, CSV 또는 이미지에서는 하이퍼링크를 사용할 수 없습니다.<br /><br /> MHTML 및 이미지의 경우 외부 이미지는 정적 그림으로 렌더링됩니다.|  
  
### <a name="bookmark-or-anchor"></a>책갈피 또는 앵커  
  
|내보내기 옵션|지원 정보|  
|-------------------|-------------------------|  
|미리 보기/보고서 뷰어, HTML|링크를 클릭하여 같은 보고서 내의 다른 섹션으로 이동할 수 있습니다.|  
|PDF|PDF에서는 사용할 수 없습니다.|  
|Excel|책갈피는 Excel로 렌더링됩니다.<br /><br /> 책갈피는 보고서 항목의 이름을 가리키는 하이퍼링크가 됩니다.|  
|Word|책갈피는 Word에서 렌더링됩니다.<br /><br /> 책갈피는 책갈피로 연결된 보고서 항목을 가리키는 하이퍼링크가 됩니다. 보고서를 내보낼 때는 책갈피나 앵커의 이름 중 처음 40자만 변환되므로 중복된 책갈피 또는 앵커 이름이 생성될 수 있습니다. 공백은 밑줄(_)로 변환됩니다.|  
|기타|XML, CSV 또는 이미지에서는 사용할 수 없습니다.|  
  
### <a name="prompted-parameters-obtained-at-run-time"></a>런타임에 가져오는 메시지 표시 매개 변수  
  
|내보내기 옵션|지원 정보|  
|-------------------|-------------------------|  
|미리 보기/보고서 뷰어, HTML|매개 변수 입력 영역은 보고서의 맨 위에 나타납니다. 이 영역은 보고서를 브라우저에 표시하는 데 사용되는 HTML 뷰어의 일부분입니다.|  
|PDF|보고서 서버에서는 보고서에 현재 사용되고 있는 매개 변수 값을 사용하여 보고서를 PDF로 내보냅니다.|  
|Excel|보고서 서버에서는 보고서에 현재 사용되고 있는 매개 변수 값을 사용하여 보고서를 Excel로 내보냅니다.|  
|Word|보고서 서버에서는 보고서에 현재 사용되고 있는 매개 변수 값을 사용하여 보고서를 Word로 내보냅니다.|  
|기타|보고서 서버에서는 보고서에 현재 사용되고 있는 매개 변수 값을 사용하여 보고서를 다른 형식으로 내보냅니다.|  
  
### <a name="filters-applied-at-run-time"></a>런타임에 적용되는 필터  
  
|내보내기 옵션|지원 정보|  
|-------------------|-------------------------|  
|미리 보기/보고서 뷰어, HTML|필터링된 데이터는 런타임에 사용자에게 표시됩니다.|  
|PDF|보고서 서버에서는 현재 보고서의 필터링된 데이터를 사용하여 보고서를 PDF로 내보냅니다.|  
|Excel|보고서 서버에서는 현재 보고서의 필터링된 데이터를 사용하여 보고서를 Excel로 내보냅니다.|  
|Word|보고서 서버에서는 현재 보고서의 필터링된 데이터를 사용하여 보고서를 Word로 내보냅니다.|  
|기타|보고서 서버에서는 현재 보고서의 필터링된 데이터를 사용하여 보고서를 다른 형식으로 내보냅니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [보고서 내보내기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [대화형 정렬, 문서 구조 및 링크&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
    
 [테이블, 행렬 및 목록&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  

