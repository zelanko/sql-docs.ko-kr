---
title: PDF 파일로 내보내기(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 10/21/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-builder
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f22497b7-f6c1-4c7b-b831-8c731e26ae37
caps.latest.revision: 13
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f609ff4110827d6165ede8cd39986d4e5dc77971
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33022960"
---
# <a name="exporting-to-a-pdf-file-report-builder-and-ssrs"></a>PDF 파일로 내보내기(보고서 작성기 및 SSRS)
  PDF 렌더링 확장 프로그램은 Adobe Acrobat 및 PDF 1.3을 지원하는 타사 PDF 뷰어에서 열 수 있는 파일로 페이지 매김 처리한 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 보고서를 렌더링합니다. PDF 1.3은 Adobe Acrobat 4.0 이상 버전과 호환되지만 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서는 Adobe Acrobat 11.0 이상 버전을 지원합니다. 이 렌더링 확장 프로그램으로 보고서를 렌더링하기 위해 Adobe 소프트웨어가 필요한 것은 아닙니다. 그러나 PDF 형식으로 보고서를 보거나 인쇄하기 위해서는 Adobe Acrobat과 같은 PDF 뷰어가 필요합니다.  
  
 PDF 렌더링 확장 프로그램에서는 ANSI 문자를 지원하며 한국어, 일본어, 중국어 번체, 중국어 간체, 키릴 자모, 히브리어 및 아랍어를 특정 제한과 함께 유니코드 문자로 변환할 수 있습니다. 제한 사항에 대한 자세한 내용은 [보고서 내보내기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)를 참조하세요.  
  
 PDF 렌더러는 물리적 페이지 렌더러이므로 페이지 매김 동작이 HTML 및 Excel 같은 다른 렌더러와는 차이가 있습니다. 이 항목에서는 PDF 렌더러 관련 정보를 제공하고 규칙의 예외를 설명합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="FontRequirements"></a> 글꼴 포함  
 가능한 경우 PDF 렌더링 확장 프로그램에는 보고서를 PDF 파일로 표시하는 데 필요한 각 하위 집합이 포함되어 있습니다. 보고서에 사용된 글꼴이 보고서 서버에 설치되어 있어야 합니다. 보고서 서버는 PDF 형식으로 보고서를 생성할 때 보고서에서 참조하는 글꼴로 저장된 정보를 사용하여 PDF 파일 내에 문자 매핑을 만듭니다. 렌더링된 글꼴이 보고서 서버에 설치되어 있지 않으면 결과 PDF 파일이 올바른 매핑을 포함하지 않을 수 있으며 화면에 올바르게 표시되지 않을 수 있습니다.  
  
 다음 조건을 만족할 경우 PDF 파일에 글꼴이 포함됩니다.  
  
-   글꼴 작성자가 글꼴 포함 권한을 허가한 경우. 설치된 글꼴에는 글꼴 작성자가 문서에 글꼴 포함을 허용했는지 여부를 나타내는 속성이 포함되어 있습니다. 속성 값이 EMBED_NOEMBEDDING이면 글꼴이 PDF 파일에 포함되지 않습니다. 자세한 내용은 msdn.microsoft.com의 "TTGetEmbeddingType"을 참조하십시오.  
  
-   글꼴이 트루타입인 경우  
  
-   보고서에 표시되는 항목이 글꼴을 참조하는 경우. 숨김 속성이 True로 설정된 항목이 글꼴을 참조하는 경우 렌더링된 데이터를 표시하는 데 글꼴이 필요하지 않으므로 파일에 포함되지 않습니다. 렌더링된 보고서 데이터를 표시하는 데 필요한 글꼴만 포함됩니다.  
  
 이러한 조건을 모두 만족하는 경우에만 PDF 파일에 글꼴이 포함됩니다. 이 조건 중 하나라도 만족하지 않으면 PDF 파일에 글꼴이 포함되지 않습니다.  
  
> [!NOTE]  
>  조건이 충족되는 경우에도 글꼴이 PDF 파일에 포함되지 않는 한 가지 상황이 있습니다. 사용된 글꼴이 표준 유형 1 글꼴 또는 기본 14 글꼴이라고 하는 PDF 사양 항목인 경우 글꼴이 ANSI 콘텐츠에 포함되지 않습니다.  
  
  
### <a name="fonts-on-the-client-computer"></a>클라이언트 컴퓨터의 글꼴  
 글꼴이 PDF 파일에 포함되면 컴퓨터(클라이언트 컴퓨터)에 해당 글꼴이 설치되어 있지 않아도 보고서가 제대로 표시됩니다.  
  
 글꼴이 PDF 파일에 포함되지 않으면 컴퓨터에 해당 글꼴이 설치되어 있어야 보고서가 제대로 표시됩니다. 클라이언트 컴퓨터에 글꼴이 설치되어 있지 않으면 PDF 파일에서 지원되지 않는 글자가 물음표(?)로 표시됩니다.  
  
### <a name="verifying-fonts-in-a-pdf-file"></a>PDF 파일의 글꼴 확인  
 PDF 출력 결과가 다르게 나타나는 현상은 주로 보고서에 사용된 글꼴이 라틴어 이외의 문자를 지원하지 않는데 라틴어 이외의 문자를 보고서에 추가한 경우 발생합니다. 보고서가 제대로 렌더링되는지 확인하려면 보고서 서버와 클라이언트 컴퓨터 모두에서 PDF 렌더링 출력을 테스트해야 합니다.  
  
 그래픽 디자인 인터페이스나 Microsoft Internet Explorer에서는 자동으로 글꼴이 대체되어 올바르게 표시되기 때문에 미리 보기나 HTML로 내보낸 결과만 믿어서는 안 됩니다. 서버에 유니코드 문자가 없으면 문자가 물음표(?)로 바뀌어 표시될 수 있습니다. 클라이언트에 글꼴이 없으면 문자가 사각형( )으로 바뀌어 표시될 수 있습니다.  
  
 PDF 파일에 포함된 글꼴은 파일에 저장된 Fonts 속성에 메타데이터로 포함됩니다.  
  
##  <a name="Metadata"></a> 메타데이터  
 PDF 렌더링 확장 프로그램에서는 보고서 레이아웃 이외에 다음과 같은 메타데이터를 PDF 문서 정보 사전에 기록합니다.  
  
|PDF 속성|정보 출처|  
|------------------|------------------|  
|**Title**|**Name** RDL 요소의 **Report** 특성|  
|**작성자**|**Author** RDL 요소|  
|**Subject**|**Description** RDL 요소|  
|**만든 이**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 제품 이름 및 버전|  
|**Producer**|렌더링 확장 프로그램 이름 및 버전|  
|**CreationDate**|PDF **datetime** 형식의 보고서 실행 시간|  
  
  
##  <a name="Interactivity"></a> 상호 작용  
 PDF에서는 일부 대화형 요소가 지원됩니다. 다음은 특정 동작에 대한 설명입니다.  
  
### <a name="show-and-hide"></a>표시 및 숨기기  
 동적 표시 및 숨기기 요소는 PDF에서 지원되지 않습니다. PDF 문서는 보고서에 포함된 모든 항목의 현재 상태와 일치하도록 렌더링됩니다. 예를 들어 보고서를 처음 실행할 때 항목이 표시된 상태이면 해당 항목이 렌더링됩니다. 설정/해제할 수 있는 이미지의 경우 보고서를 내보낼 당시 숨겨진 상태이면 해당 이미지가 렌더링되지 않습니다.  
  
### <a name="document-map"></a>문서 구조  
 보고서에 문서 구조 레이블이 있으면 PDF 파일에 문서 개요가 추가됩니다. 각 문서 구조 레이블은 보고서에 표시된 것과 같은 순서에 따라 문서 개요의 항목으로 표시됩니다. Acrobat에서는 문서 개요가 있는 페이지를 렌더링하는 경우에만 문서 개요에 대상 책갈피를 추가합니다.  
  
 한 페이지만 렌더링하는 경우에는 문서 개요가 추가되지 않습니다. 문서 구조는 보고서의 중첩 수준을 반영하는 계층 구조에 따라 배열됩니다. 문서 개요에 액세스하려면 Acrobat에서 책갈피 탭을 사용합니다. 문서 개요 내의 항목을 클릭하면 문서에서 책갈피 설정된 위치로 이동할 수 있습니다.  
  
### <a name="bookmarks"></a>책갈피  
 책갈피는 PDF 렌더링에 지원되지 않습니다.  
  
### <a name="drillthrough-links"></a>드릴스루 링크  
 드릴스루 링크는 PDF 렌더링에 지원되지 않습니다. 드릴스루 링크는 클릭 가능한 링크로 렌더링되지 않으며 드릴스루 보고서는 드릴스루 대상에 연결할 수 없습니다.  
  
### <a name="hyperlinks"></a>하이퍼링크  
 보고서의 하이퍼링크는 PDF 파일에서 클릭하여 연결할 수 있는 링크로 렌더링됩니다. 이를 클릭하면 Acrobat에서 클라이언트의 기본 브라우저가 열리고 하이퍼링크 URL로 이동합니다.  
  
  
##  <a name="Compression"></a> 압축  
 이미지 압축은 이미지의 원래 파일 형식을 기준으로 합니다. PDF 렌더링 확장 프로그램에서는 기본적으로 PDF 파일을 압축합니다.  
  
 PDF 파일에 포함된 이미지의 모든 압축을 가능한 한 계속 유지하기 위해 JPEG 이미지는 JPEG로 저장되고 다른 모든 이미지 형식은 BMP로 저장됩니다.  
  
> [!NOTE]  
>  PDF 파일은 PNG 포함 이미지를 지원하지 않습니다.  
  
  
##  <a name="DeviceInfo"></a> 장치 정보 설정  
 장치 정보 설정을 변경하여 이 렌더러의 기본 설정을 일부 변경할 수 있습니다. 자세한 내용은 [PDF Device Information Settings](../../reporting-services/pdf-device-information-settings.md)을 참조하세요.  
  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services의 페이지 매김&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [렌더링 동작&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [여러 보고서 렌더링 확장 프로그램의 대화형 기능&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [보고서 항목 렌더링&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [테이블, 행렬 및 목록&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
