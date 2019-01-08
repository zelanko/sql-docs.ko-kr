---
title: 보고서 미리 보기
author: markingmyname
ms.author: maghan
manager: kfile
ms.reviewer: ''
ms.prod: reporting-services-2014, sql-server-2014
ms.prod_service: reporting-services-native, reporting-services-sharepoint
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: 7746263fc015f7cf1d398c821ce94e49c134ba0f
ms.sourcegitcommit: 2f5773f4bc02bfff4f2924226ac5651eb0c00924
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/18/2018
ms.locfileid: "53553235"
---
# <a name="preview-reports-in-sql-server-reporting-services-ssrs"></a>SQL Server Reporting Services (SSRS)에서 보고서 미리 보기

  보고서를 디자인할 때 프로덕션 환경에 게시하기 전에 보고서를 미리 볼 수 있습니다. 이 작업은 보고서 디자이너에서 미리 보기 모드로 전환하거나, 보고서 디자이너에서 미리 보기 창을 사용하거나, 테스트 환경의 보고서 서버에 보고서를 게시하여 수행할 수 있습니다.  
  
> [!NOTE]  
> 보고서를 미리 보면 보고서의 데이터가 로컬 컴퓨터의 파일에 캐시됩니다. 동일한 쿼리, 매개 변수 및 자격 증명을 사용하여 동일한 보고서를 다시 미리 보면 보고서 디자이너는 쿼리를 다시 실행하지 않고 캐시된 복사본을 검색합니다. 데이터 파일은 보고서 정의 파일과 같은 디렉터리에 *\<reportname>*.rdl.data로 저장됩니다. 이 파일은 보고서 디자이너를 닫아도 삭제되지 않습니다.  
  
## <a name="preview-mode"></a>미리 보기 모드

 클릭 하 여 보고서 디자이너에서 보고서를 미리 볼 수 있습니다 **미리 보기**합니다. 이때 보고서는 로컬로 실행되며 보고서 서버에 제공되는 동일한 보고서 처리 및 렌더링 기능을 사용합니다. 표시되는 보고서는 대화형 이미지이므로 매개 변수를 선택하고, 링크를 클릭하고, 문서 구조를 보고, 보고서의 숨겨진 영역을 확대 및 축소할 수 있습니다. 또한 설치된 렌더링 형식으로 보고서를 내보낼 수 있습니다.  
  
## <a name="standalone-preview"></a>독립 실행형 미리 보기

 디버그 구성 등에서 보고서 프로젝트를 실행하여 사용자가 작성하는 사용자 지정 어셈블리를 디버깅하여 보고서를 미리 볼 수도 있습니다. 프로젝트를 실행하는 방법에는 세 가지가 있습니다.  
  
- 클릭 하 여 **시작** 에 **디버그** 메뉴.  
  
- 클릭 하 여 합니다 **시작** 단추를 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 표준 도구 모음입니다.  
  
- F5 키를 누릅니다.  
  
 보고서를 작성은 하지만 배포하지 않는 프로젝트 구성을 사용하면 현재 구성의 `StartItem` 속성에 지정된 보고서는 별도의 미리 보기 창에 열립니다. 미리 보기 창에서 보고서는 미리 보기 모드와 동일한 방식으로 표시되고 동일한 기능을 제공합니다.  
  
> [!NOTE]  
> 보고서를 디버깅하려면 먼저 시작 항목을 설정해야 합니다. 시작 항목을 설정 하려면 솔루션 탐색기에서 보고서 프로젝트를 마우스 오른쪽 단추로 클릭 **속성**를 선택한 다음 `StartItem`를 표시할 보고서의 이름을 선택 합니다.  
  
 프로젝트의 시작 항목이 아닌 특정 보고서를 미리 보려면 보고서를 작성하지만 배포하지 않는 구성(예: DebugLocal 구성)을 선택하고 보고서를 마우스 오른쪽 단추로 클릭한 다음 **실행**을 클릭합니다. 보고서를 배포하지 않는 구성을 선택해야 합니다. 그렇지 않으면 보고서는 로컬 컴퓨터의 미리 보기 창에 표시되지 않고 보고서 서버에 게시됩니다.  
  
## <a name="print-preview"></a>인쇄 미리 보기

 미리 보기 모드 또는 미리 보기 창에서 보고서를 처음으로 보면 해당 보고서가 HTML 렌더링 확장 프로그램에서 생성된 보고서와 유사하게 표시됩니다. 미리 보기는 HTML 형식은 아니지만 보고서의 레이아웃 및 페이지 매기기는 HTML 출력과 유사합니다.  
  
 인쇄 미리 보기 모드로 전환하여 인쇄될 보고서를 표시할 수 있습니다. 미리 보기 도구 모음에서 **인쇄 미리 보기** 단추를 클릭합니다. 보고서는 실제 인쇄된 페이지처럼 표시되며 이미지 및 PDF 렌더링 확장 프로그램에서 생성된 출력과도 유사합니다. 인쇄 미리 보기는 이미지나 PDF 파일 형식은 아니지만 보고서의 레이아웃 및 페이지 매기기는 해당 형식의 출력과 유사합니다.  
  
## <a name="publish-to-a-test-server"></a>테스트 서버에 게시

 테스트 서버에 게시하여 보고서를 테스트할 수도 있습니다. 테스트 서버와 프로덕션 서버에 보고서를 게시하는 방법은 동일합니다. 보고서 게시에 대한 자세한 내용은 [보고서 서버에 보고서 게시](publishing-reports-to-a-report-server.md)를 참조하세요.  
  
## <a name="next-steps"></a>다음 단계

 - [보고서 인쇄&#40;보고서 작성기 및 SSRS&#41;](../report-builder/print-reports-report-builder-and-ssrs.md)
 - [보고서 인쇄&#40;보고서 작성기 및 SSRS&#41;](../report-builder/print-a-report-report-builder-and-ssrs.md)
 - [보고서 게시](../publish-reports.md)
 - [보고서에서 사용자 지정 어셈블리 사용](../custom-assemblies/using-custom-assemblies-with-reports.md)