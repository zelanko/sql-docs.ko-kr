---
title: Microsoft 신경망 뷰어를 사용 하 여 모델 찾아보기 | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ba0f41f182eaa2d96ce771373b8abba4d863d619
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="browse-a-model-using-the-microsoft-neural-network-viewer"></a>Microsoft 신경망 뷰어를 사용하여 모델 찾아보기
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 신경망 뷰어는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 신경망 알고리즘을 사용하여 작성된 마이닝 모델을 표시합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 신경망 알고리즘은 개방형 분석 및 탐색에 유용하고 여러 입력 및 출력을 분석할 수 있는 분류 및 회귀 마이닝 모델을 만듭니다. 이 알고리즘에 대한 자세한 내용은 [Microsoft Neural Network Algorithm](../../analysis-services/data-mining/microsoft-neural-network-algorithm.md)를 참조하십시오.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 신경망 뷰어를 사용하여 모델을 탐색할 때는 일반적으로 대상 특성 및 상태를 선택한 다음 뷰어를 사용하여 입력 특성이 출력에 영향을 주는 방식을 확인합니다.  
  
 예를 들어 잠재 고객 클래스에 대해 다음과 같은 사실을 알고 있다고 가정해 봅니다.  
  
-   중년(40~50세)  
  
-   주택 소유  
  
-   집에 두 아이도 함께 살고 있음  
  
 고객이 구매할 가능성과 이러한 특성 간에 어떻게 상관 관계를 지정할 수 있습니까?  
  
 구매 행동을 대상 결과로 사용하여 신경망 모델을 작성함으로써 높은 수입과 같은 고객 특성에 대한 여러 조합을 탐색하고 어떤 조합이 구매 행동에 가장 영향을 많이 주는지 확인할 수 있습니다. 예를 들어 결정 요소가 고객의 통근 거리라는 사실을 발견할 수 있습니다.  
  
 발견된 각 패턴을 나타내는 수식과 같은 자세한 정보를 보려는 경우 뷰로 전환하고 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 일반 콘텐츠 트리 뷰어를 사용할 수 있습니다. 자세한 내용은 [Microsoft 일반 콘텐츠 트리 뷰어를 사용하여 모델 찾아보기](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) 또는 [Microsoft 일반 콘텐츠 트리 뷰어&#40;데이터 마이닝&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c)를 참조하세요.  
  
##  <a name="BKMK_ViewerTabs"></a> 뷰어 탭  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 마이닝 모델을 찾으면 해당 모델의 적절한 뷰어에서 데이터 마이닝 디자이너의 **마이닝 모델 뷰어** 탭에 해당 모델이 표시됩니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 신경망 뷰어는 신경망 마이닝 모델 탐색 시 사용할 수 있는 다음과 같은 탭을 제공합니다.  
  
-   [입력](#BKMK_Inputs)  
  
-   [출력](#BKMK_Outputs)  
  
-   [변수](#BKMK_Characteristics)  
  
###  <a name="BKMK_Inputs"></a> 입력  
 **입력** 탭을 사용하여 모델에서 입력으로 사용한 특성 및 특성 값을 선택합니다. 뷰어를 열면 기본적으로 모든 특성이 포함되어 있습니다. 이 기본 뷰에서 모델은 표시할 가장 중요한 특성 값을 선택합니다.  
  
 입력 특성을 선택하려면 **입력** 표의 **특성** 열 내부를 클릭하고 드롭다운 목록에서 특성을 선택합니다. 모델에 있는 특성만 목록에 포함됩니다.  
  
 **값** 열에 첫 번째 고유 값이 표시됩니다. 기본값을 클릭하면 관련 특성의 모든 가능한 상태가 포함된 목록이 표시됩니다. 조사할 상태를 선택할 수 있으며 원하는 만큼 특성을 선택할 수 있습니다.  
  
 [맨 위로 이동](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Outputs"></a> 출력  
 **출력** 탭을 사용하여 조사할 결과 특성을 선택합니다. 비교할 두 결과 상태를 선택할 수 있습니다. 열은 모델을 작성할 때 예측 가능한 특성으로 정의되었다고 가정합니다.  
  
 **출력 특성** 목록을 사용하여 특성을 선택할 수 있습니다. 그런 다음 **값 1** 목록과 **값 2** 목록에서 해당 특성과 연결된 두 개의 상태를 선택할 수 있습니다. 출력 특성의 이러한 두 가지 상태는 **변수** 창에서 비교됩니다.  
  
 [맨 위로 이동](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Characteristics"></a> 변수  
 **변수** 탭의 표에는 **특성**, **값**, **[값 1]과(와)의 유사성**및 **[값 2]과(와)의 유사성**열이 있습니다. 기본적으로 열은 **[값 1]과(와)의 유사성**수준에 따라 정렬됩니다. 열 제목을 클릭하면 선택한 열의 정렬 순서가 변경됩니다.  
  
 특성의 오른쪽에 있는 막대는 지정된 입력 특성 상태가 유사한 출력 특성 상태를 보여 줍니다. 막대의 크기는 출력 상태와 입력 상태의 유사한 정도를 보여 줍니다.  
  
 [맨 위로 이동](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>관련 항목:  
 [Microsoft 신경망 알고리즘](../../analysis-services/data-mining/microsoft-neural-network-algorithm.md)   
 [마이닝 모델 뷰어 태스크 및 방법](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [마이닝 모델 뷰어 태스크 및 방법](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [데이터 마이닝 도구](../../analysis-services/data-mining/data-mining-tools.md)   
 [데이터 마이닝 모델 뷰어](../../analysis-services/data-mining/data-mining-model-viewers.md)  
  
  
