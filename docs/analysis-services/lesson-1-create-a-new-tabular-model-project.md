---
title: '1 단원: 새 테이블 형식 모델 프로젝트 만들기 | Microsoft Docs'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f17f0c36b129d3c2699be714390c2cb1eb8efdd1
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="lesson-1-create-a-new-tabular-model-project"></a>1단원: 새 테이블 형식 모델 프로젝트를 만들기
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

이 단원에서는 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 새로운 빈 테이블 형식 모델 프로젝트를 만듭니다. 새 프로젝트를 만든 후 테이블 가져오기 마법사를 사용하여 데이터를 추가할 수 있습니다. 이 단원에서는 테이블 형식 모델 제작 환경 SSDT에에 대 한 간략 한 소개를 제공 합니다.  
  
이 단원에 소요되는 예상 시간: **10분**  
  
## <a name="prerequisites"></a>필수 구성 요소  
이 항목은 테이블 형식 모델 제작 자습서의 첫 번째 단원입니다. 이 단원을 완료 하려면 AdventureWorksDW 예제 데이터베이스는 SQL Server 인스턴스에 설치 되어 있어야 합니다. 자세한 내용은 참고 [테이블 형식 모델링 &#40;Adventure Works 자습서&#41;](../analysis-services/tabular-modeling-adventure-works-tutorial.md)합니다.  
  
## <a name="create-a-new-tabular-model-project"></a>새 테이블 형식 모델 프로젝트 만들기  
  
#### <a name="to-create-a-new-tabular-model-project"></a>새 테이블 형식 모델 프로젝트를 만들려면  
  
1.  SSDT에서는는 **파일** 메뉴를 클릭 **새로** > **프로젝트**합니다.  
  
2.  에 **새 프로젝트** 대화 상자에서 **설치 됨** > **Business Intelligence** > **Analysis Services**, 클릭 하 고 **Analysis Services 테이블 형식 프로젝트**합니다.  
  
3.  **이름**, 형식 **AW Internet Sales**, 프로젝트 파일의 위치를 지정 합니다.  
  
    **솔루션 이름** 은 기본적으로 프로젝트 이름과 동일하지만 다른 솔루션 이름을 입력할 수 있습니다.  
  
4.  **확인**을 클릭합니다.  
  
5.  에 **테이블 형식 모델 디자이너** 대화 상자에서 **통합된 작업 영역**합니다.  
  
    작업 영역 모델 제작 중 프로젝트와 이름이 같은 테이블 형식 모델 데이터베이스를 호스트 합니다. 통합된 작업 영역 이면 SSDT는 사용할 기본 제공 된 인스턴스를 모델 제작에 대 한 별도 Analysis Services 서버 인스턴스를 설치할 필요가 없습니다. 자세한 내용은 참고 [작업 영역 데이터베이스](../analysis-services/tabular-models/workspace-database-ssas-tabular.md)합니다.
      
6.  **호환성 수준**에서 **SQL Server 2016(1200)** 이 선택되어 있는지 확인한 다음 **확인**을 클릭합니다.   
 
    ![as-tabular-lesson1-tmd](../analysis-services/media/as-tabular-lesson1-tmd.png)
      
    호환성 수준 목록 상자에서 SQL Server 2016 RTM (1200) 표시 되지 않는, 사용 중인 경우 하지 SQL Server Data Tools의 최신 버전입니다. 최신 버전을 다운로드하려면 [SQL Server Data Tools 설치](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)를 참조하세요.  

    최신 버전의 SSDT 사용 하는 SQL Server 2017 선택할 수도 있습니다 (1400). 그러나 전체 단원 13으로: 배포, SQL Server 2017 또는 Azure 서버를 배포 하려면 필요 합니다.
      
    이전 호환성 수준 선택 하려는 경우 이전 버전의 SQL Server를 실행 하는 다른 Analysis Services 인스턴스에 배포 하는 완료 된 테이블 형식 모델에만 권장 됩니다. 통합된 작업 영역 이전 호환성 수준에 대 한 지원 되지 않습니다. 자세한 내용은 [호환성 수준](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)을참조하세요.   
  
## <a name="understanding-the-ssdt-tabular-model-authoring-environment"></a>SSDT 테이블 형식 모델 제작 환경 이해  
새 테이블 형식 모델 프로젝트를 만들었으므로 이제 제작 환경 SSDT에서 테이블 형식 모델을 탐색할 잠시 하겠습니다.  
  
프로젝트를 만든 후 SSDT에서 열립니다. 오른쪽에서에서 **테이블 형식 모델 탐색기**, 모델에 있는 개체의 트리 보기에 표시 됩니다. 데이터를 가져온 아직 하지 않은 이후 폴더는 비어 있게 됩니다. 메뉴 모음과 비슷한 작업을 수행 하는 개체 폴더를 마우스 오른쪽 단추로 클릭 수 있습니다. 이 자습서를 실행할 때는 모델 프로젝트에서 서로 다른 개체를 탐색 하는 테이블 형식 모델 탐색기를 사용 합니다.

![as-tabular-lesson1-tme](../analysis-services/media/as-tabular-lesson1-tme.png)

클릭는 **솔루션 탐색기** 탭 합니다. 확인할 수 있습니다 프로그램 **Model.bim** 파일입니다. 디자이너 창의 왼쪽 (Model.bim 탭 된 빈 창)에 표시 되지 않는 경우 **솔루션 탐색기**아래 **AW Internet Sales 프로젝트**, 두 번 클릭은 **Model.bim** 파일입니다. Model.bim 파일 모든 모델 프로젝트에 대 한 메타 데이터를 포함합니다. 

![as-tabular-lesson1-se](../analysis-services/media/as-tabular-lesson1-se.png)
  
모델 속성에 살펴보겠습니다. 클릭 **Model.bim**합니다. 에 **속성** 창 표시는 [모델 속성](../analysis-services/tabular-models/model-properties-ssas-tabular.md)되며이 중 가장 중요 한는 **DirectQuery 모드** 속성입니다. 이 속성은 모델이 메모리 내 모드(해제)로 배포되는지 아니면 DirectQuery 모드(설정)로 배포되는지를 지정합니다. 이 자습서에서는 메모리 내 모드에서 모델을 제작하고 배포합니다.

![as-tabular-lesson1-properties](../analysis-services/media/as-tabular-lesson1-properties.png)
  
특정 모델 속성에 지정할 수 있는 데이터 모델링 설정에 따라 자동으로 설정 됩니다는 새 모델을 만들 때의 **도구** > **옵션** 대화 상자. 데이터 백업, 작업 영역 보존 및 작업 영역 서버 속성은 작업 영역 데이터베이스(모델 제작 데이터베이스)가 백업되고 메모리에 보관되고 작성되는 방법을 지정합니다. 필요하면 나중에 이러한 설정을 변경할 수 있지만 지금은 있는 그대로 둡니다.  

**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **AW Internet Sales** (프로젝트)를 클릭 하 고 **속성**합니다. **AW Internet Sales 속성 페이지** 대화 상자가 나타납니다. 이 고급 [프로젝트 속성](../analysis-services/tabular-models/project-properties-ssas-tabular.md)합니다. 나중에 모델을 배포할 준비가 되었을 때 이러한 속성 중 일부를 설정합니다.  
  
SSDT를 설치할 때 몇 가지 새 메뉴 항목이 Visual Studio 환경에 추가 되었습니다. 테이블 형식 모델 제작과 관련 된에서 살펴보겠습니다. **모델** 메뉴를 클릭합니다. 여기에서 있습니다 수 테이블 가져오기 마법사를 시작, 보고 및 편집 기존 연결, 작업 영역 데이터를 새로 고칠는 Excel에서에서 분석 기능을 사용 하 여 Excel에서 모델 찾아보기, 큐브 뷰 및 역할을 만들, 모델 뷰를 선택 하 고 계산 옵션을 설정 합니다.  
  
**테이블** 메뉴를 클릭합니다. 이 메뉴에서 테이블 간 관계를 만들거나 관리하고, 날짜 테이블 설정을 만들고 관리하고 지정하고, 파티션을 만들고, 테이블 속성을 편집할 수 있습니다.  
  
**열** 메뉴를 클릭합니다. 이 메뉴에서 테이블에 열을 추가 및 삭제하고, 열을 고정하고, 정렬 순서를 지정할 수 있습니다. 자동 합계 기능을 사용하여 선택한 열에 대한 표준 집계 측정값을 만들 수도 있습니다. 다른 도구 모음 단추를 사용하면 자주 사용하는 기능과 명령에 빠르게 액세스할 수 있습니다.  
  
테이블 형식 모델 제작과 관련된 다양한 기능의 위치와 대화 상자를 살펴보십시오. 일부 항목은 아직 활성화되어 있지 않지만 테이블 형식 모델 제작 환경을 파악하는 데 도움이 될 것입니다.  


## <a name="additional-resources"></a>추가 리소스
다양 한 유형의 테이블 형식 모델 프로젝트에 대 한 자세한 참조 [테이블 형식 모델 프로젝트](../analysis-services/tabular-models/tabular-model-projects-ssas-tabular.md)합니다. 테이블 형식 모델 제작 환경에 대 한 자세한 참조 [테이블 형식 모델 디자이너 ](../analysis-services/tabular-models/tabular-model-designer-ssas.md)합니다.  
  

## <a name="whats-next"></a>다음 단계
다음 단원으로 이동: [2 단원: 데이터 추가](../analysis-services/lesson-2-add-data.md)합니다.

  
  
  
