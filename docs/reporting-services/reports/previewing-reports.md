---
title: "보고서 미리 보기 | Microsoft Docs"
ms.custom: 
ms.date: 05/05/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Report Designer [Reporting Services], previewing reports
- previewing reports [Reporting Services]
- printing previews
- test servers [Reporting Services]
ms.assetid: 85117f6c-828e-45c9-810f-e700d9bfba67
caps.latest.revision: "44"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: c4d8cd078dd674ddb0d8bbf1db5a28f794e093df
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="previewing-reports"></a>보고서 미리 보기
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서를 디자인할 때 프로덕션 환경에 게시하기 전에 보고서를 미리 볼 수 있습니다. 이 작업은 보고서 디자이너에서 미리 보기 모드로 전환하거나, 보고서 디자이너에서 미리 보기 창을 사용하거나, 테스트 환경의 보고서 서버에 보고서를 게시하여 수행할 수 있습니다.  
  
> [!NOTE]  
>  보고서를 미리 보면 보고서의 데이터가 로컬 컴퓨터의 파일에 캐시됩니다. 동일한 쿼리, 매개 변수 및 자격 증명을 사용하여 동일한 보고서를 다시 미리 보면 보고서 디자이너는 쿼리를 다시 실행하지 않고 캐시된 복사본을 검색합니다. 데이터 파일은 보고서 정의 파일과 같은 디렉터리에 *\<reportname>*.rdl.data로 저장됩니다. 이 파일은 보고서 디자이너를 닫아도 삭제되지 않습니다.  
  
## <a name="preview-mode"></a>미리 보기 모드  
 ![ssrs_ssdt_preview](../../reporting-services/media/ssrs-ssdt-preview.png "ssrs_ssdt_preview")를 클릭하여 보고서 디자이너에서 보고서를 미리 볼 수 있습니다. 이때 보고서는 로컬로 실행되며 보고서 서버에 제공되는 동일한 보고서 처리 및 렌더링 기능을 사용합니다. 표시되는 보고서는 대화형 이미지이므로 매개 변수를 선택하고, 링크를 클릭하고, 문서 구조를 보고, 보고서의 숨겨진 영역을 확대 및 축소할 수 있습니다. 또한 설치된 렌더링 형식으로 보고서를 내보낼 수 있습니다.  
  
## <a name="standalone-preview"></a>독립 실행형 미리 보기  
 디버그 구성 등에서 보고서 프로젝트를 실행하여 사용자가 작성하는 사용자 지정 어셈블리를 디버깅하여 보고서를 미리 볼 수도 있습니다. 보고서는 기본 브라우저에서 열립니다. 프로젝트를 실행하는 방법에는 세 가지가 있습니다.  
  
-   **디버그** 메뉴에서 **디버깅 시작** 을 클릭합니다.  
  
-   [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 표준 도구 모음 ![ssrs_ssdt_startdebug](../../reporting-services/reports/media/ssrs-ssdt-startdebug.png "ssrs_ssdt_startdebug")에서 **시작** 단추를 클릭합니다.  
  
-   **F5**키를 누릅니다.  
  
 보고서를 작성은 하지만 배포하지 않는 프로젝트 구성을 사용하면 현재 구성의 **StartItem** 속성에 지정된 보고서는 별도의 미리 보기 창에 열립니다. 미리 보기 창에서 보고서는 미리 보기 모드와 동일한 방식으로 표시되고 동일한 기능을 제공합니다.  
  
> [!NOTE]  
>  보고서를 디버깅하려면 먼저 시작 항목을 설정해야 합니다. 예를 들어 디버그 모드를 실행하는 경우 브라우저에서 기본 보고서 서버 페이지가 열리고 보고서가 미리 보기 모드로 열리지 않습니다. 시작 항목을 설정하려면 솔루션 탐색기에서 보고서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭한 다음 **StartItem**에서 표시할 보고서의 이름을 선택합니다.  
  
 프로젝트의 시작 항목이 아닌 특정 보고서를 미리 보려면 보고서를 작성하지만 배포하지 않는 구성(예: DebugLocal 구성)을 선택하고 보고서를 마우스 오른쪽 단추로 클릭한 다음 **실행**을 클릭합니다. 보고서를 배포하지 않는 구성을 선택해야 합니다. 그렇지 않으면 보고서는 로컬 컴퓨터의 미리 보기 창에 표시되지 않고 보고서 서버에 게시됩니다.  
  
## <a name="publishing-to-a-test-server"></a>테스트 서버에 게시  
 보고서를 테스트 서버에 게시하여 테스트하고 보고서를 찾아 미리 볼 수도 있습니다. 테스트 서버와 프로덕션 서버에 보고서를 게시하는 방법은 동일합니다. 보고서 게시에 대한 자세한 내용은 [보고서 서버에 보고서 게시](../../reporting-services/reports/publishing-reports-to-a-report-server.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [보고서 인쇄&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)   
 [보고서 인쇄&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/print-a-report-report-builder-and-ssrs.md)   
 [보고서 게시](http://msdn.microsoft.com/library/ef5a514e-e818-4041-a8b0-15835f9a046b)   
 [보고서에서 사용자 지정 어셈블리 사용](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
