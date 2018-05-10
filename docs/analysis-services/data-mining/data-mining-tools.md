---
title: 데이터 마이닝 도구 | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 26e3d36a68197607d788ca1170a2fd509698221d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="data-mining-tools"></a>데이터 마이닝 도구
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에는 데이터 마이닝 솔루션을 만드는 데 사용할 수 있는 다음 도구가 있습니다.  
  
-   **** 의 데이터 마이닝 마법사 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 는 관계형 데이터 원본이나 큐브의 다차원 데이터를 사용하여 마이닝 구조와 마이닝 모델을 쉽게 만들 수 있도록 합니다.  
  
     이 마법사에서 사용할 데이터를 선택한 다음 클러스터링, 신경망 또는 시계열 모델링과 같은 특정 데이터 마이닝 기술을 적용할 수 있습니다.  
  
-   **모델 뷰어** 는 마이닝 모델이 만들어진 후 마이닝 모델을 탐색하기 위해 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 및 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 제공됩니다.  각 알고리즘에 맞게 조정된 뷰어를 사용하여 모델을 찾아보거나 모델 콘텐츠 뷰어를 사용하여 세부적으로 분석할 수 있습니다.  
  
-   **예측 쿼리 작성기** 는 예측 쿼리를 쉽게 만들 수 있도록 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 및 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서 제공됩니다. 홀드아웃 데이터 집합 또는 외부 데이터에 대해 모델의 정확도를 테스트하거나 교차 유효성 검사를 사용하여 데이터 집합의 품질을 평가할 수도 있습니다.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에 배포된 기존 데이터 마이닝 솔루션을 관리하는 인터페이스입니다. 구조와 모델을 다시 처리하여 구조와 모델의 데이터를 업데이트할 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 데이터를 정리하고, 예측 생성, 모델 업데이트 등의 태스크를 자동화하고, 텍스트 마이닝 솔루션을 만드는 데 사용할 수 있는 도구가 있습니다.  
  
 다음 섹션에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 데이터 마이닝 도구에 대한 추가 정보를 제공합니다.  
  
## <a name="data-mining-wizard"></a>데이터 마이닝 마법사  
 데이터 마이닝 마법사를 사용하여 데이터 마이닝 솔루션 생성을 시작할 수 있습니다. 이 마법사는 빠르고 쉬우며 데이터 마이닝 구조 및 초기 관련 마이닝 모델을 만드는 과정을 안내하고 알고리즘 유형 및 데이터 원본 선택 태스크와 분석에 사용되는 사례 데이터 정의 태스크를 포함합니다.  
  
 **자세한 내용:** [데이터 마이닝 마법사&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/data-mining-wizard-analysis-services-data-mining.md)  
  
## <a name="data-mining-designer"></a>데이터 마이닝 디자이너  
 데이터 마이닝 마법사를 사용하여 마이닝 구조와 마이닝 모델을 만든 후 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 데이터 마이닝 디자이너를 사용하여 기존 모델과 구조로 작업할 수 있습니다.  
  
 디자이너에는 다음 태스크를 위한 도구가 포함되어 있습니다.  
  
-   마이닝 구조의 속성을 수정하고, 열을 추가하고 열 별칭을 만들고, 범주화 방법이나 값의 예상 분포를 변경합니다.  
  
-   기존 구조에 새 모델을 추가하고, 모델을 복사하고, 모델 속성이나 메타데이터를 변경하고, 마이닝 모델에 대한 필터를 정의합니다.  
  
-   모델 내의 패턴과 규칙을 찾아보고, 연결 또는 의사 결정 트리를 탐색하고, 자세한 통계를 얻습니다.  
  
     데이터를 분석하고 데이터 마이닝으로 드러난 패턴을 탐색하는 데 도움을 주기 위해 사용자 지정 뷰어가 모델의 각기 다른 각 시간에 대해 제공됩니다.  
  
-   리프트 차트를 만들거나 모델의 수익 곡선을 분석하여 모델의 유효성을 검사합니다. 분류 행렬을 사용하여 모델을 비교하거나 교차 유효성 검사를 사용하여 데이터 집합과 해당 모델의 유효성을 검사합니다.  
  
-   기존 마이닝 모델에 대해 예측 및 내용 쿼리를 만듭니다. 외부 데이터의 전체 테이블에 대한 예측을 생성하기 위해 쿼리를 설정하거나 일회용 쿼리를 작성합니다.  
  
## <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 마이닝 모델을 만들어 서버에 배포한 후 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 데이터 마이닝 개체를 호스팅하는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 관리할 수 있습니다. 또한 모델 탐색, 새 데이터 처리, 예측 생성 등의 모델을 사용하는 태스크를 계속 수행할 수도 있습니다.  
  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 에는 DMX(Data Mining Extensions) 쿼리를 디자인하고 실행하거나 XMLA를 사용하여 데이터 마이닝 개체로 작업하는 데 사용할 수 있는 쿼리 편집기도 포함되어 있습니다.  
  
## <a name="integration-services-data-mining-tasks-and-transformations"></a>Integration Services 데이터 마이닝 태스크 및 변환  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 데이터 마이닝을 지원하는 많은 구성 요소가 있습니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 의 일부 도구는 예측, 모델 작성, 처리 등의 일반적인 데이터 마이닝 태스크를 쉽게 자동화할 수 있도록 설계되었습니다. 예를 들어:  
  
-   데이터 집합이 새 고객으로 업데이트될 때마다 모델을 자동으로 업데이트하는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 만듭니다.  
  
-   사례 레코드의 사용자 지정 구분 또는 사용자 지정 샘플링을 수행합니다.  
  
-   매개 변수에서 전달된 모델을 자동으로 생성합니다.  
  
 그러나 다른 프로세스에 대한 입력으로 패키지 워크플로에서 데이터 마이닝을 사용할 수도 있습니다. 예를 들어:  
  
-   모델에서 생성된 확률 값을 사용하여 텍스트 마이닝 또는 다른 분류 태스크에 대한 점수에 가중치를 부여합니다.  
  
-   이전 데이터를 기반으로 자동으로 예측을 생성하고 해당 값을 사용하여 새 데이터의 유효성을 평가합니다.  
  
-   로지스틱 회귀를 사용하여 위험을 기준으로 들어오는 고객을 구분합니다.  
  
 **자세한 내용:** [데이터 마이닝 솔루션 관련 프로젝트](../../analysis-services/data-mining/related-projects-for-data-mining-solutions.md)  
  
## <a name="see-also"></a>관련 항목:  
 [Data Mining Extensions & #40; DMX & #41; 참조](../../dmx/data-mining-extensions-dmx-reference.md)   
 [마이닝 모델 태스크 및 방법](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [마이닝 모델 뷰어 태스크 및 방법](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [데이터 마이닝 솔루션](../../analysis-services/data-mining/data-mining-solutions.md)  
  
  
