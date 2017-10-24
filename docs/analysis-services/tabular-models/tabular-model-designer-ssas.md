---
title: "테이블 형식 모델 디자이너 | Microsoft Docs"
ms.date: 10/19/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ASVS.BIDTOOLSET.TOPLEVSEMMODUIENTRY.F1
ms.assetid: 45735c57-2a95-4e45-8994-7242df6c9c5f
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 685286966599c4dcd3dc2f7029413c77f3ff2689
ms.openlocfilehash: b660ee5e5923b47c45e3198297042607fa59f874
ms.contentlocale: ko-kr
ms.lasthandoff: 10/20/2017

---
# <a name="tabular-model-designer-ssas"></a>테이블 형식 모델 디자이너(SSAS)
테이블 형식 모델 디자이너는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 일부로 Microsoft [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에 통합되어 있으며, 전문적인 테이블 형식의 모델 솔루션을 개발하기 위한 추가 프로젝트 형식 템플릿이 함께 제공됩니다.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 는 무료 웹 다운로드로 설치됩니다. 자세한 내용은 [SSDT(SQL Server Data Tools) 다운로드](../../ssdt/download-sql-server-data-tools-ssdt.md)를 참조하세요.    
  
##  <a name="bkmk_benefits"></a> 이점  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]를 설치하면 테이블 형식의 모델을 만들기 위한 새 프로젝트 템플릿이 사용 가능한 프로젝트 형식에 추가됩니다. 이 템플릿 중 하나를 사용하여 테이블 형식의 새 모델 프로젝트를 만든 다음 테이블 형식 모델 디자이너 도구와 마법사를 사용하여 모델 제작을 시작할 수 있습니다.  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 환경에서는 전문적인 다차원 및 테이블 형식 모델 솔루션 제작을 위한 새로운 템플릿과 도구뿐만 아니라 디버깅 및 프로젝트 수명 주기 기능을 제공하여 조직에 맞는 가장 강력한 BI 솔루션을 개발할 수 있습니다. [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에 대한 자세한 내용은 [Visual Studio 시작](http://go.microsoft.com/fwlink/?LinkId=206389)을 참조하십시오.  
  
##  <a name="bkmk_proj_temp"></a>프로젝트 템플릿  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]를 설치하면 다음과 같은 테이블 형식 모델 프로젝트 템플릿이 비즈니스 인텔리전스 프로젝트 형식에 추가됩니다.  
  
 **Analysis Services 테이블 형식 프로젝트**  
 이 템플릿은 비어 있는 새 테이블 형식 모델 프로젝트를 만드는 데 사용할 수 있습니다. 호환성 수준은 프로젝트를 만들 때 지정됩니다.
  
 **서버에서 가져오기(테이블 형식)**  
 이 템플릿은 Analysis Services의 기존 테이블 형식 모델에서 메타데이터를 추출하여 새 테이블 형식 모델 프로젝트를 만드는 데 사용할 수 있습니다.  
  
 이전 모델에서는 오래된 호환성 수준이 사용됩니다. 모델 정의 가져온 후 호환성 수준 속성을 변경 하 여 업그레이드할 수 있습니다.  
  
 **다음에서 가져오기 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]**  
 이 템플릿은 [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] 파일에서 메타데이터와 데이터를 추출하여 새 테이블 형식 모델 프로젝트를 만드는 데 사용됩니다.  
  
##  <a name="bkmk_wind_men"></a> 창 및 메뉴  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 테이블 형식 모델 제작 환경에는 다음이 포함되어 있습니다.  
  
### <a name="designer-window"></a>디자이너 창  
 디자이너 창은 테이블 형식 모델 제작에 사용되며 모델에 대한 시각적 표현을 제공합니다. Model.bim 파일을 열면 디자이너 창에서 모델이 열립니다. 디자이너 창에서 다음과 같은 두 가지 다른 보기 모드를 사용하여 모델을 제작할 수 있습니다.  
  
 **데이터 뷰**  
 데이터 뷰는 테이블을 표 형식으로 표시합니다. 데이터 뷰에서만 각 테이블에 표시할 수 있는 측정값 표를 사용하여 측정값을 정의할 수도 있습니다.  
  
 **다이어그램 보기**  
 다이어그램 뷰는 테이블을 그래픽 형식의 관계도와 함께 표시합니다. 열, 측정값, 계층 및 KPI를 필터링할 수 있으며 정의된 큐브 뷰를 사용하여 모델을 표시하도록 선택할 수도 있습니다.  
  
 대부분의 모델 제작 태스크를 이 두 가지 뷰에서 수행할 수 있습니다.  
  
### <a name="view-code-window"></a>코드 창 보기  
 솔루션 탐색기에서 마우스 오른쪽 단추를 클릭하고 파일에 대해 **코드 보기** 를 선택하면 Model.bim 파일의 코드를 볼 수 있습니다. 호환성 수준 1200 이상에서 테이블 형식 모델에 대 한 모델 정의 JSON으로 표현 됩니다.  
  
 이 정의를 확인하려면 JSON 편집기를 제공하는 정식 버전 Visual Studio가 필요합니다. 상용 버전의 추가 기능이 필요하지 않으면 [무료 Visual Studio Community 버전](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) 을 다운로드하여 설치할 수 있습니다.  
  
### <a name="solution-explorer"></a>솔루션 탐색기  
 솔루션 탐색기 창은 활성 솔루션을 테이블 형식 모델 프로젝트 및 해당 프로젝트와 관련된 항목에 대한 논리적 컨테이너로 보여줍니다. 모델 프로젝트(.smproj)에는 참조 개체(비어 있음)와 Model.bim 파일만 포함됩니다. 이 뷰에서 프로젝트 항목을 열어 수정하고 다른 관리 태스크를 직접 수행할 수 있습니다.  
  
 테이블 형식 모델 솔루션에는 대개 하나의 프로젝트만 포함되지만 한 솔루션에 Integration Services 또는 Reporting Services 프로젝트 등의 다른 여러 프로젝트가 포함될 수도 있습니다. 테이블 형식 모델 프로젝트 파일과 형식이 다르고 빌드 동작 속성이 없음으로 설정되거나 출력 디렉터리로 복사 속성이 복사 안 함으로 설정된 파일은 개수와 관계없이 무제한 추가할 수 있습니다.  
  
 솔루션 탐색기를 보려면 **보기** 메뉴를 클릭한 다음 **솔루션 탐색기**를 클릭합니다.  

### <a name="tabular-model-explorer"></a>테이블 형식 모델 탐색기
  첫 번째의 2016 년 8 월 릴리스 (14.0.60812.0)에서 사용할 수 있는 [SQL Server Data Tools](https://msdn.microsoft.com/mt186501), 테이블 형식 모델 탐색기를 사용 하면 테이블 형식 모델에서 메타 데이터 개체를 이동할 수 있습니다.

 테이블 형식 모델 탐색기를 표시하려면 **보기** > **다른 창**을 클릭한 다음 **테이블 형식 모델 탐색기**를 클릭합니다.
   
  ![테이블 형식 모델 탐색기](../../analysis-services/tabular-models/media/tabular-model-explorer.png) 
  
 테이블 형식 모델 탐색기 유사한 테이블 형식 모델의 스키마는 트리 구조로 메타 데이터 개체를 구성 합니다. 데이터 원본, 큐브 뷰, 관계, 역할, 테이블 및 변환은 최상위 스키마 개체에 해당합니다. 특히 KPI 및 측정값과 같이 기술적으로 최상위 개체는 아니지만 모델에서 여러 테이블의 자식 개체인 예외 항목이 몇 가지 있습니다. 그러나 모든 KPI 및 측정값에 대한 최상위 컨테이너를 통합하면 특히 모델에 아주 많은 테이블을 포함한 경우 이러한 개체를 사용하여 쉽게 작업할 수 있습니다. 측정값은 해당 부모 테이블에도 나열되므로 실제 부모-자식 관계에 대해 명확하게 확인할 수 있습니다. 최상위 측정값 컨테이너에서 측정값을 선택하면 동일한 측정값이 테이블 하위의 자식 컬렉션에서도 선택됩니다. 그 반대의 경우도 마찬가지입니다.  
 
 테이블 형식 모델 탐색기에서 개체 노드는 Visual Studio의 모델, 테이블 및 열 메뉴 아래에서 숨겨져 있었던 적절한 메뉴 옵션에 연결됩니다. 개체를 마우스 오른쪽 단추로 클릭하여 개체 형식에 대한 옵션을 탐색할 수 있습니다. 일부 개체 노드 형식에는 상황에 맞는 메뉴가 있지만 추가 옵션 및 향상된 기능이 후속 릴리스에서 도입될 예정입니다. 

 테이블 형식 모델 탐색기는 또한 편리한 검색 기능을 제공합니다. 검색 상자에 이름을 일부만 입력해도 테이블 형식 모델 탐색기에서 일치하는 항목을 트리 보기로 보여 줍니다. 
  
### <a name="properties-window"></a>속성 창  
 속성 창은 선택된 개체의 속성을 나열합니다. 속성 창에서 다음과 같은 개체의 속성을 보고 편집할 수 있습니다.  
  
-   Model.bim  
  
-   테이블  
  
-   열  
  
-   이름  
  
 프로젝트 속성은 속성 창에 프로젝트 이름과 프로젝트 폴더만 표시합니다. 프로젝트에는 또한 모달 속성 대화 상자에서 설정할 수 있는 추가 배포 옵션 및 배포 서버 설정이 있습니다. 이 속성을 보려면 **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
 속성 창의 필드에는 클릭하면 열리는 컨트롤이 포함되어 있습니다. 편집 컨트롤 유형은 특정 속성에 따라 달라집니다. 컨트롤에는 편집 상자, 드롭다운 목록, 사용자 지정 대화 상자에 대한 링크 등이 있습니다. 흐리게 표시되는 속성은 읽기 전용입니다.  
  
 **속성** 창을 보려면 **보기** 메뉴를 클릭한 다음 **속성 창**을 클릭합니다.  
  
### <a name="error-list"></a>오류 목록  
 오류 목록 창에는 다음과 같은 모델 상태에 대한 메시지가 포함됩니다.  
  
-   최상의 권장 보안 방법에 대한 알림  
  
-   데이터 처리 요구 사항  
  
-   계산 열, 측정값 및 역할 행 필터에 대한 의미 체계 오류 정보. 계산 열에서 오류 메시지를 두 번 클릭하면 오류의 출처가 표시됩니다.  
  
-   DirectQuery 유효성 검사 오류  
  
 기본적으로 **오류 목록** 은 오류가 반환되어야만 표시됩니다. 그러나 **오류 목록** 창은 언제든지 확인할 수 있습니다. **오류 목록** 창을 보려면 **보기** 메뉴를 클릭한 다음 **오류 목록**을 클릭합니다.  
  
### <a name="output"></a>출력  
 빌드 및 배포 정보가 **출력** 창 및 모달 진행률 대화 상자에 표시됩니다. **출력** 창을 보려면 **보기** 메뉴를 클릭한 다음 출력을 클릭합니다.  
  
### <a name="menu-items"></a>메뉴 항목  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]를 설치하면 테이블 형식의 모델을 제작하는 데 사용되는 추가 메뉴 항목이 Visual Studio 메뉴 모음에 추가됩니다. **모델** 메뉴를 사용하여 데이터 가져오기 마법사를 시작하고, 기존 연결을 보고, 작업 영역 데이터를 처리하고, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel에서 모델 작업 영역을 찾아볼 수 있습니다. **테이블** 메뉴를 사용하여 테이블 간의 관계를 만들고 관리하고, 측정값을 만들고 관리하며, 데이터 테이블 설정을 지정하고, 계산 옵션을 지정하고, 기타 테이블 속성을 지정할 수 있습니다. **열** 메뉴를 사용하여 테이블에서 열을 추가 및 삭제하고, 열을 숨기거나 숨기기를 취소하고, 데이터 형식 및 필터와 같은 기타 열 속성을 지정할 수 있습니다. **빌드** 메뉴에서 테이블 형식 모델 솔루션을 빌드하고 배포할 수 있습니다. 복사/붙여넣기 기능은 **편집** 메뉴에 포함되어 있습니다.  
  
 이러한 새 메뉴 항목 외에도 도구 메뉴 항목의 Analysis Services 옵션에 추가 설정이 추가되어 있습니다.  
  
### <a name="toolbar"></a>도구 모음  
 Analysis Services 도구 모음을 통해 신속하고 간편하게 자주 사용하는 모델 작성 명령에 액세스할 수 있습니다.  
  
##  <a name="bkmk_vsint"></a>Visual Studio 통합  
 **소스 제어**  
 Analysis Services 프로젝트는 선택한 원본 제어 플러그 인과 통합됩니다. 원본 제어를 사용하도록 Visual Studio를 구성하면 솔루션 탐색기에서 체크 인/체크 아웃을 사용할 수 있습니다. Team Foundation Server를 사용하도록 구성하려면 [Team Foundation 버전 제어로 Visual Studio 구성](http://msdn.microsoft.com/library/ms253064.aspx)을 참조하십시오. 그 외 다양한 타사 원본 제어 플러그 인도 지원합니다.  
  
 **글꼴**  
 테이블 형식 모델은 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 환경의 글꼴을 사용하여 표시되는 글꼴을 제어합니다. 기본 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 글꼴을 사용하여 해당 언어의 유니코드 문자를 모두 표시할 수 없을 경우 이 글꼴을 변경해야 할 수 있습니다. 글꼴을 변경하려면 **도구** 메뉴를 클릭하고 **옵션**을 클릭한 다음 **글꼴 및 색**을 클릭합니다.  
  
 **바로 가기 키**  
 도구->옵션->키보드 대화 상자를 통해 Analysis Services 키보드 바로 가기를 구성하거나 다시 매핑할 수 있습니다. 빌드, 저장, 디버그, 새 프로젝트 등과 같은 전역 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 바로 가기가 테이블 형식 모델 디자이너 컨텍스트에서 지원됩니다. 그 외 테이블 형식 모델 디자이너용 바로 가기 키는 Analysis Services 컨텍스트에서 지원됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [테이블 형식 모델 프로젝트&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/tabular-model-projects-ssas-tabular.md)   
 [속성&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/properties-ssas-tabular.md)  
  
  

