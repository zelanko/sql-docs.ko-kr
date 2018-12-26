---
title: 만들기 또는 데이터 피드 라이브러리 (SharePoint 용 파워 피벗)를 사용자 지정 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 71c051d64a40f38a6514301ca3353e7627c67aaf
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34021257"
---
# <a name="create-or-customize-a-data-feed-library-power-pivot-for-sharepoint"></a>데이터 피드 라이브러리 만들기 또는 사용자 지정(SharePoint용 Power Pivot)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  *데이터 피드 라이브러리* 는 Atom 데이터 서비스 문서(.atomsvc)를 등록 및 공유할 수 있도록 해 주는 특수 용도의 SharePoint 라이브러리입니다. 이러한 문서는 Atom 데이터 피드 형식을 지원하는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서나 기타 클라이언트 애플리케이션에 XML 데이터 피드를 제공합니다. 데이터 피드 라이브러리는 다음과 같은 기능을 제공하므로 다른 SharePoint 라이브러리와 다릅니다.  
  
-   특정 피드에 대한 HTTP 연결을 지정하는 데 사용되는 *데이터 서비스 문서*만들기 또는 편집  
  
-   중앙 위치에서 데이터 서비스 문서 공유 및 관리  
  
-   동일한 라이브러리에 저장 된 다른 문서에서 서비스 문서를 쉽게 구분할 수 있도록 아이콘을 사용 하 여 데이터 서비스 문서를 시각적으로 식별: ![GMNI_IconDataFeed](../../analysis-services/power-pivot-sharepoint/media/gmni-icondatafeed.gif "GMNI_IconDataFeed")  
  
 데이터 피드 라이브러리에는 항상 데이터 서비스 문서(.atomsvc) 파일이 포함되어 있고 데이터 피드 자체는 포함되어 있지 않습니다. 정적 XML 데이터로 구성되는 데이터 피드와 달리 데이터 서비스 문서는 반복 가능한 가져오기 작업에 재사용 가능한 연결 정보를 제공하여 요청에 따라 피드를 생성하는 서비스 또는 애플리케이션에 대한 URL을 지정합니다.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
 [필수 구성 요소](#prereq)  
  
 [새 데이터 피드 라이브러리 만들기](#createlib)  
  
 [라이브러리에 데이터 피드 콘텐츠 형식 추가](#addtolib)  
  
##  <a name="prereq"></a> 필수 구성 요소  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 기능 통합을 활성화해야 합니다. 데이터 피드 라이브러리 템플릿 유형을 사용할 수 없는 경우 이 사전 요구 사항이 충족되지 않았을 수 있습니다. 자세한 내용은 [중앙 관리에서 사이트 모음에 대해 파워 피벗 기능 통합 활성화](../../analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca.md)을(를) 참조하세요.  
  
 라이브러리를 만들려면 사이트 소유자여야 합니다.  
  
##  <a name="createlib"></a> 새 데이터 피드 라이브러리 만들기  
 데이터 피드 라이브러리 만들기는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서에 대해 데이터 피드를 사용하도록 설정하는 첫 번째 단계입니다. 데이터 피드 라이브러리는 데이터 서비스 문서에 대한 애플리케이션 및 관리 페이지를 제공하므로, 새 문서를 만들려면 이 라이브러리가 있어야 합니다.  
  
 데이터 피드 라이브러리는 데이터 서비스 문서의 속성과 동작을 정의하는 미리 구성된 *데이터 서비스 문서 콘텐츠 형식* 과 기본 제공 템플릿을 기반으로 합니다.  
  
1.  페이지 왼쪽 위 모퉁이에 있는 **사이트 작업** 을 클릭합니다.  
  
2.  **기타 옵션...** 을 클릭합니다.  
  
3.  라이브러리에서 **데이터 피드 라이브러리**를 클릭합니다.  
  
4.  이름, 설명, 시작 및 버전 기본 설정을 입력합니다. 사용자가 이 라이브러리를 데이터 서비스 문서에 대한 저장소로 식별하는 데 도움이 되는 설명 정보를 포함합니다.  
  
5.  **만들기**를 클릭합니다.  
  
 데이터 피드 라이브러리에 대한 링크가 현재 사이트의 탐색 빠른 실행 창에 표시됩니다.  
  
 라이브러리를 만든 후 해당 라이브러리를 사용하여 데이터 서비스 문서를 만들 수 있습니다. 자세한 내용은 [데이터 피드 사용&#40;SharePoint용 파워 피벗&#41;](../../analysis-services/power-pivot-sharepoint/use-data-feeds-power-pivot-for-sharepoint.md)을(를) 참조하세요.  
  
##  <a name="addtolib"></a> 라이브러리에 데이터 피드 콘텐츠 형식 추가  
 전용 데이터 피드 라이브러리를 만들지 않지만 SharePoint 사이트에서 데이터 서비스 문서를 만들고 관리하려는 경우 데이터 서비스 문서(.atomsvc) 파일을 공유하는 데 사용할 라이브러리에 대한 데이터 서비스 문서 콘텐츠 형식을 수동으로 추가하여 구성할 수 있습니다.  
  
 콘텐츠 형식을 추가하고 구성하려면 최소한 목록 관리 권한이 있어야 합니다. 이 권한은 디자인 권한 수준 이상에 포함되어 있습니다.  
  
 데이터 피드 등록 문서를 만들거나 편집하려는 라이브러리마다 다음 단계를 반복해야 합니다.  
  
#### <a name="step-1-enable-content-type-management"></a>1단계: 콘텐츠 형식 관리 사용  
  
1.  여러 콘텐츠 형식을 사용할 문서 라이브러리를 엽니다.  
  
2.  SharePoint 리본의 라이브러리 도구에서 **라이브러리**를 클릭합니다.  
  
3.  **설정**을 클릭합니다.  
  
4.  **라이브러리 설정**을 클릭합니다.  
  
5.  일반 설정에서 **고급 설정**을 클릭합니다.  
  
6.  콘텐츠 형식의 "콘텐츠 형식 관리를 허용하시겠습니까?" 섹션에서 **예**를 클릭합니다.  
  
7.  **확인**을 클릭합니다.  
  
#### <a name="step-2-add-the-data-service-document-content-type"></a>2단계: 데이터 서비스 문서 콘텐츠 형식 추가  
  
1.  콘텐츠 형식 섹션에서 **기존 사이트 콘텐츠 형식에서 추가**를 클릭합니다. 이 페이지가 표시되지 않는 경우 사이트로 돌아가서 라이브러리 도구에서 **라이브러리** 를 클릭한 다음 **라이브러리 설정**을 클릭합니다.  
  
2.  콘텐츠 형식에서 **기존 사이트 콘텐츠 형식에서 추가**를 클릭합니다.  
  
3.  사이트 콘텐츠 형식 선택에서 **비즈니스 인텔리전스**를 선택합니다.  
  
4.  사용 가능한 사이트 콘텐츠 형식에서 **데이터 서비스 문서**를 클릭한 다음 **추가** 를 클릭하여 선택한 콘텐츠 형식을 목록을 추가할 콘텐츠 형식으로 이동합니다.  
  
5.  **확인**을 클릭합니다.  
  
#### <a name="step-3-verify-data-service-document-configuration"></a>3단계: 데이터 서비스 문서 구성 확인  
  
1.  사이트 홈 페이지를 엽니다.  
  
2.  라이브러리를 엽니다.  
  
3.  SharePoint 리본에서 **문서**를 클릭합니다.  
  
4.  새 문서에서 아래쪽 화살표를 클릭하고 **데이터 서비스 문서**를 선택합니다. 새 데이터 서비스 문서 페이지가 표시됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 피드 사용&#40;SharePoint용 파워 피벗&#41;](../../analysis-services/power-pivot-sharepoint/use-data-feeds-power-pivot-for-sharepoint.md)   
 [파워 피벗 데이터 피드 라이브러리 삭제](../../analysis-services/power-pivot-sharepoint/delete-a-power-pivot-data-feed-library.md)   
 [중앙 관리에서 파워 피벗 서버 관리 및 구성](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [Power Pivot 데이터 피드](../../analysis-services/power-pivot-sharepoint/power-pivot-data-feeds.md)  
  
  
