---
title: '1 단원: 새 테이블 형식 모델 프로젝트 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0d2eb34d-78c8-41ff-b92d-49b62c16b2ac
author: minewiskan
ms.author: owend
ms.openlocfilehash: f21d1805eda75bfa0008214e2f46f54b67ab48f5
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84543602"
---
# <a name="lesson-1-create-a-new-tabular-model-project"></a>1단원: 새 테이블 형식 모델 프로젝트 만들기
  이 단원에서는 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 새로운 빈 테이블 형식 모델 프로젝트를 만듭니다. 새 프로젝트를 만든 후 테이블 가져오기 마법사를 사용하여 데이터를 추가할 수 있습니다. 이 단원에서는 새 프로젝트를 만들 뿐 아니라 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]의 테이블 형식 모델 제작 환경에 대해서도 간단히 소개합니다.  
  
 다양한 유형의 테이블 형식 모델 프로젝트에 대한 자세한 내용은 [테이블 형식 모델 프로젝트&#40;SSAS 테이블 형식&#41;](tabular-models/tabular-model-projects-ssas-tabular.md)를 참조하세요. 테이블 형식 모델 제작 환경에 대 한 자세한 내용은 [테이블 형식 모델 디자이너 &#40;SSAS 테이블 형식&#41;](tabular-model-designer-ssas-tabular.md)을 참조 하세요.  
  
 이 단원을 완료하기 위한 예상 시간: **10분**  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 항목은 테이블 형식 모델 제작 자습서의 첫 번째 단원입니다. 이 섹션을 완료하려면 SQL Server 인스턴스에 AdventureWorksDW 데이터베이스가 설치되어 있어야 합니다. 자세한 내용은 [테이블 형식 모델링&#40;Adventure Works 자습서&#41;](tabular-modeling-adventure-works-tutorial.md)을 참조하세요.  
  
## <a name="create-a-new-tabular-model-project"></a>새 테이블 형식 모델 프로젝트 만들기  
  
#### <a name="to-create-a-new-tabular-model-project"></a>새 테이블 형식 모델 프로젝트를 만들려면  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]의 **파일** 메뉴에서 **새로 만들기**를 클릭한 다음 **프로젝트**를 클릭합니다.  
  
2.  **새 프로젝트** 대화 상자의 **설치 된 템플릿**에서 **비즈니스 인텔리전스**를 클릭 한 다음 **Analysis Services**를 클릭 하 고 **테이블 형식 프로젝트 Analysis Services**를 클릭 합니다.  
  
3.  **이름**에를 입력 `AW Internet Sales Tabular Model` 하 고 프로젝트 파일의 위치를 지정 합니다.  
  
     기본적으로 **솔루션 이름**은 프로젝트 이름과 같게 되지만 다른 솔루션 이름을 입력할 수 있습니다.  
  
4.  **확인**을 클릭합니다.  
  
## <a name="understanding-the-sql-server-data-tools-tabular-model-authoring-environment"></a>SQL Server Data Tools 테이블 형식 모델 제작 환경 이해  
 새 테이블 형식 모델 프로젝트를 만들었으므로 이제 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] (Visual Studio 2010 이상)에서 테이블 형식 모델 제작 환경을 살펴보겠습니다.  
  
 프로젝트를 만들면 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 열립니다. 모델 디자이너에 빈 모델이 표시되고 **솔루션 탐색기** 창에서 **Model.bim** 파일이 선택됩니다. 데이터를 추가하면 테이블과 열이 디자이너에 표시됩니다. 디자이너 (model.bim 탭이 있는 빈 창)가 표시 되지 않으면 **솔루션 탐색기**의에서 `AW Internet Sales Tabular Model` **model.bim** 파일을 두 번 클릭 합니다.  
  
 **속성** 창에서 기본 프로젝트 속성을 볼 수 있습니다. **솔루션 탐색기**에서를 클릭 `AW Internet Sales Tabular Model` 합니다. **속성** 창의 **프로젝트 파일**에 **AW Internet Sales Tabular Model.smproj**가 표시됩니다. 이 이름은 프로젝트 파일 이름이며 프로젝트 파일 위치는 **프로젝트 폴더**에서 확인할 수 있습니다.  
  
 **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 한 `AW Internet Sales Tabular Model` 다음 **속성**을 클릭 합니다. **AW Internet Sales Tabular Model 속성 페이지** 대화 상자가 나타납니다. 다음은 고급 프로젝트 속성입니다. 나중에 모델을 배포할 준비가 되었을 때 이러한 속성 중 일부를 설정합니다.  
  
 이제 모델 속성을 살펴보겠습니다. **솔루션 탐색기**에서 **Model.bim**을 클릭합니다. **속성** 창에 모델 속성이 표시되며 이 중 **DirectQuery 모드** 속성이 가장 중요한 속성입니다. 이 속성은 모델이 메모리 내 모드(Off) 또는 DirectQuery 모드(On)로 배포되는지를 지정합니다. 이 자습서에서는 메모리 내 모드에서 모델을 제작하고 배포합니다.  
  
 새 모델을 만들 때 특정 모델 속성은 데이터 모델링 설정에 따라 자동으로 설정됩니다. 데이터 모델링 설정은 도구\옵션 대화 상자에서 지정할 수 있습니다. 데이터 Backup, 작업 영역 보존 및 작업 영역 서버 속성은 작업 영역 데이터베이스가 백업되고 메모리 내 보존되며 빌드되는 방식과 위치를 지정합니다. 필요한 경우 나중에 이러한 설정을 변경할 수 있지만 지금은 이러한 속성을 그대로 둡니다.  
  
 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]를 설치할 때 몇 가지 새 메뉴 항목이 Visual Studio 환경에 추가되었습니다. 테이블 형식 모델 작성과 관련 된 새 메뉴 항목을 살펴보겠습니다. **모델** 메뉴를 클릭합니다. 이 메뉴에서는 테이블 가져오기 마법사를 시작하고, 기존 연결을 보거나 편집하고, 작업 영역 데이터를 새로 고치고, Excel에서 분석 기능을 사용하여 [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel에서 모델을 검색하고, 큐브 뷰와 역할을 만들고, 모델 뷰를 선택하고, 계산 옵션을 설정할 수 있습니다.  
  
 **테이블** 메뉴를 클릭합니다. 이 메뉴에서 테이블 간 관계를 만들거나 관리하고, 날짜 테이블 설정을 만들고 관리하고 지정하고, 파티션을 만들고, 테이블 속성을 편집할 수 있습니다.  
  
 **열** 메뉴를 클릭합니다. 이 메뉴에서 테이블에 열을 추가 및 삭제하고, 열을 고정하고, 정렬 순서를 지정할 수 있습니다. 자동 합계 기능을 사용하여 선택한 열에 대한 표준 집계 측정값을 만들 수도 있습니다. 다른 도구 모음 단추를 사용하면 자주 사용하는 기능과 명령에 빠르게 액세스할 수 있습니다.  
  
 테이블 형식 모델 제작과 관련된 다양한 기능의 위치와 대화 상자를 살펴보십시오. 일부 항목은 아직 활성화되어 있지 않지만 테이블 형식 모델 제작 환경을 파악하는 데 도움이 될 것입니다.  
  
## <a name="next-steps"></a>다음 단계  
 이 자습서를 계속하려면 다음 단원인 [2단원: 데이터 추가](lesson-2-add-data.md)로 이동하세요.  
  
  
