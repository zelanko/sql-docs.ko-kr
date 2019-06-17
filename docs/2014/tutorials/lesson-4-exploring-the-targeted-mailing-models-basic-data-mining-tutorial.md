---
title: '4단원: (기본 데이터 마이닝 자습서) 타겟된 메일링 모델 탐색 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1e00c5b9-a9f8-4503-99ee-377c9cc02d7f
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 97db61dc3b9adf2e345957c8e08aa752e51286e0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63312145"
---
# <a name="lesson-4-exploring-the-targeted-mailing-models-basic-data-mining-tutorial"></a>4단원: (기본 데이터 마이닝 자습서) 타겟된 메일링 모델 탐색
  프로젝트의 모델이 처리되면 이러한 모델을 탐색하여 관심 있는 추세를 찾아볼 수 있습니다. 숫자만 보는 경우 패턴이 복잡하고 어려울 수 있기 때문에 SQL Server 데이터 마이닝은 데이터를 조사하고 알고리즘이 데이터 내에서 발견한 규칙과 관계를 이해하는 데 도움을 주는 몇 가지 시각적 도구를 제공합니다. 또한 다양한 정확도 테스트를 사용하여 데이터 세트의 유효성을 검사하거나 모델을 배포하기 전에 성능이 가장 뛰어난 모델을 찾을 수 있습니다.  
  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 를 사용하여 모델을 탐색하는 경우 만들어진 각 모델은 데이터 마이닝 디자이너의 **마이닝 모델 뷰어** 탭에 나열됩니다. 뷰어를 사용하여 모델을 탐색할 수 있습니다. 이러한 뷰는 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서도 사용할 수 있습니다.  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 모델을 작성하는 데 사용하는 각 알고리즘에 따라 다른 유형의 결과가 반환됩니다. 따라서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 는 각 유형의 시스템 학습 모델에 대한 사용자 지정 뷰어를 제공합니다.  
  
 세부 사항을 보려는 경우 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 는 **일반 콘텐츠 트리 뷰어**라는 HTML 뷰어도 제공합니다. 이 뷰어에는 모델 데이터와 발견된 모든 패턴에 대한 자세한 정보가 절반 정도는 표 형식으로 표시됩니다. 자세한 내용은 [Microsoft 일반 콘텐츠 트리 뷰어를 사용하여 모델 찾아보기](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)를 참조하세요.  
  
 이 단원에서는 세 모델에서 결과를 확인합니다. 각 모델 형식은 다른 알고리즘을 기반으로 하며 데이터에 대한 다른 관점을 제공합니다.  
  
-   의사 결정 트리 모델은 자전거 구매에 영향을 주는 요소에 대해 알려줍니다.  
  
-   클러스터링 모델은 자전거 구매 동작 및 기타 선택한 특성을 포함하는 특성별로 고객을 그룹화합니다.  
  
-   Naive Bayes 모델을 통해 다른 특성 간 관계를 탐색할 수 있습니다.  
  
 각 마이닝 모델 뷰어에 대해 자세히 알아보려면 다음 항목을 참조하십시오.  
  
-   [의사 결정 트리 모델 탐색 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
-   [클러스터링 모델 탐색 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
-   [Naive Bayes 모델 탐색 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
 수식, 데이터 값 등을 추출하기 위해 세 모델을 모두 **일반 콘텐츠 트리 뷰어**를 사용하여 볼 수 있습니다.  
  
## <a name="first-task-in-lesson"></a>단원의 첫 번째 태스크  
 [의사 결정 트리 모델 탐색 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
## <a name="previous-lesson"></a>이전 단원  
 [3단원: 모델 추가 및 처리](../../2014/tutorials/lesson-3-adding-and-processing-models.md)  
  
## <a name="next-lesson"></a>다음 단원  
 [5단원: 모델을 테스트 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-5-testing-models-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>관련 항목  
 [마이닝 모델 뷰어 태스크 및 방법](../../2014/analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [데이터 마이닝 모델 뷰어](../../2014/analysis-services/data-mining/data-mining-model-viewers.md)  
  
  
