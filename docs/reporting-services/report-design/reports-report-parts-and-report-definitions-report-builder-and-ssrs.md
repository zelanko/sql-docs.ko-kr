---
title: "보고서 파트를 보고서 및 보고서 정의 (보고서 작성기 및 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- report definitions
- reports
ms.assetid: 2d746550-f8cc-4e97-8a06-d0f03cffc18d
caps.latest.revision: 26
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 1ad3eee80539ea31af3ccf9e117b2f39b4921846
ms.contentlocale: ko-kr
ms.lasthandoff: 09/21/2017

---
# <a name="reports-report-parts-and-report-definitions-report-builder-and-ssrs"></a>보고서, 보고서 파트 및 보고서 정의(보고서 작성기 및 SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 다양한 용어를 사용하여 사용자에게 표시되는 초기 정의, 게시된 보고서 및 표시된 보고서를 비롯한 여러 상태의 페이지가 매겨진 보고서를 설명합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-definition-rdl-files"></a>보고서 정의 파일(.rdl)  
 보고서 정의는 보고서 작성기나 보고서 디자이너에서 만든 파일입니다. 이 파일은 데이터 원본 연결에 대한 완전한 설명, 데이터 검색에 사용되는 쿼리, 식, 매개 변수, 이미지, 입력란, 테이블 및 보고서에 포함할 수 있는 기타 디자인 타임 요소를 제공합니다. 보고서 정의는 복잡할 수도 있지만 기본적으로 쿼리 및 기타 보고서 내용, 보고서 속성 및 보고서 레이아웃을 지정합니다.  
  
 보고서 정의는 런타임에 처리된 보고서로 렌더링됩니다. 이 시점에서 데이터가 데이터 원본에서 검색되고 보고서 정의의 명령에 따라 형식이 지정됩니다. 보고서 정의는 컴퓨터에서 직접 실행하고 로컬에 저장할 수 있으며 보고서 서버에 게시하여 다른 사람이 실행하도록 할 수도 있습니다.  
  
 보고서 정의는 RDL(Report Definition Language)이라는 XML 문법에 맞는 XML로 작성됩니다. RDL은 보고서에서 가정할 수 있는 모든 변형을 포함하는 XML 요소를 기술합니다.  
  
## <a name="client-report-definition-rdlc-files"></a>클라이언트 보고서 정의 파일(.rdlc)  
 Visual Studio 보고서 디자이너는 ReportViewer 컨트롤에 사용할 클라이언트 보고서 정의 파일(.rdlc)을 생성합니다. .rdlc 파일을 .rdl 파일로 변환하여 Reporting Services 보고서 디자이너에 사용할 수 있습니다.  
  
## <a name="report-part-rsc-files"></a>보고서 파트 파일(.rsc)  
 보고서 파트는 보고서 서버에 저장된 자체 포함된 보고서 항목으로 다른 보고서에 포함될 수 있습니다. 보고서 작성기를 사용하여 보고서 파트 갤러리에서 보고서에 추가할 파트를 찾아 선택합니다. 보고서 디자이너 또는 보고서 작성기를 사용하여 보고서 파트 갤러리에 사용할 보고서 파트를 저장합니다.  
  
 보고서 파트 정의는 보고서 정의 파일의 XML 조각입니다. 보고서 정의를 만든 다음 보고서의 보고서 항목을 선택하여 별도의 보고서 파트로 게시하는 방법으로 보고서 파트를 만들 수 있습니다. 보고서 파트에는 데이터 영역, 사각형과 이에 포함된 항목 및 이미지가 포함됩니다. 보고서 파트를 종속 데이터 집합 및 공유 데이터 원본 참조와 함께 저장하여 다른 보고서에서 다시 사용할 수 있습니다.  
  
 자세한 내용은 [보고서 파트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md) 및 [보고서 디자이너의 보고서 파트&#40;SSRS&#41;](../../reporting-services/report-design/report-parts-in-report-designer-ssrs.md)를 참조하세요.  
  
## <a name="published-reports"></a>게시된 보고서  
 .rdl 파일을 만든 후에는 로컬에 저장하거나 보고서 서버의 내 보고서 폴더와 같은 개인 폴더에 저장할 수 있습니다. 다른 사용자가 볼 수 있도록 보고서를 설정하려면 보고서 작성기에서 보고서 서버의 공용 폴더로 저장하거나, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 웹 포털을 통해 업로드하거나, 보고서 디자이너에서 보고서 프로젝트 솔루션을 배포하여 게시합니다. 게시된 보고서는 보고서 서버 데이터베이스에 저장되고 보고서 서버 또는 SharePoint 사이트에서 관리됩니다.  
  
 게시된 보고서는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 역할 기반 보안 모델을 사용하여 역할 할당을 통해 보안이 유지됩니다. 게시된 보고서는 URL, SharePoint 웹 파트 또는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 웹 포털을 통해 액세스하거나 보고서 작성기에서 해당 보고서를 찾아서 열 수 있습니다.  
  
### <a name="report-snapshots"></a>보고서 스냅숏  
 보고서는 보고서를 처음 실행했을 때의 레이아웃 정보와 데이터가 모두 포함된 스냅숏으로 게시할 수도 있습니다. 보고서 스냅숏은 특정 렌더링 형식으로 저장되지 않으며 사용자나 응용 프로그램이 보고서 스냅숏을 요청할 때만 HTML과 같은 최종 보기 형식으로 렌더링됩니다. 자세한 내용은 참조 [보고서 찾기 및 보기에서 보고서 관리자 &#40; 보고서 작성기 및 SSRS &#41; ](/sql-docs/docs/reporting-services/report-builder/finding-and-viewing-reports-with-a-browser-report-builder-and-ssrs).  
  
## <a name="rendered-reports"></a>렌더링된 보고서  
 렌더링된 보고서는 데이터와 레이아웃 정보가 HTML과 같은 적합한 표시 형식으로 포함되어 있는 완전히 처리된 보고서입니다. 출력 형식으로 렌더링되지 않은 보고서는 볼 수 없습니다. 다음 중 하나를 수행하여 보고서를 렌더링할 수 있습니다.  
  
-   보고서 작성기 또는 보고서 디자이너에서 보고서를 만들거나 열고 실행합니다.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 웹 포털에서 보고서를 찾아 실행합니다.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버와 통합된 SharePoint 사이트에서 보고서를 찾고 실행합니다.  
  
-   사용자가 지정한 출력 형식으로 전자 메일 받은 편지함이나 파일 공유 위치로 배달되는 보고서를 구독합니다.  
  
 사용자가 지정한 출력 형식으로 전자 메일 받은 편지함이나 파일 공유 위치로 배달되는 보고서를 구독합니다. 보고서의 기본 렌더링 형식은 HTML 4.0입니다. 보고서는 HTML 외에도 Excel, Word, XML, PDF, TIFF 및 CSV를 비롯한 다양한 출력 형식으로 렌더링할 수 있습니다. 게시된 보고서와 마찬가지로 렌더링된 보고서는 편집하거나 보고서 서버에 다시 저장할 수 없습니다. 자세한 내용은 [보고서 내보내기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [보고서 제작 개념&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-authoring-concepts-report-builder-and-ssrs.md)   
 [SQL Server 2016의 보고서 작성기](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)   
 [보고서 찾기, 보기 및 관리&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [보고서 내보내기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)  
  
  
