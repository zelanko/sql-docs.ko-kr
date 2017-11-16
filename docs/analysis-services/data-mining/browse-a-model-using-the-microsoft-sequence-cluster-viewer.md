---
title: "Microsoft 시퀀스 클러스터 뷰어를 사용 하 여 모델 찾아보기 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Sequence Cluster Viewer
- clusters [Analysis Services]
- data mining [Analysis Services], sequences
- discrimination [Analysis Services]
- mining model content, viewing
- mining models [Analysis Services], sequences
- Microsoft Sequence Cluster Viewer
- sequence [Analysis Services]
- transitions [Analysis Services]
ms.assetid: 3ada00aa-da9e-488a-9f53-c3e188f81f84
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 87f8b6d83647639e8c2a807add3df680ff47b6b9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="browse-a-model-using-the-microsoft-sequence-cluster-viewer"></a>Microsoft 시퀀스 클러스터 뷰어를 사용하여 모델 찾아보기
  [!INCLUDE[msCoName](../../includes/msconame-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 시퀀스 클러스터 뷰어는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시퀀스 클러스터링 알고리즘을 사용하여 작성된 마이닝 모델을 표시합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시퀀스 클러스터링 알고리즘은 경로, 즉 *시퀀스*를 따라 연결할 수 있는 이벤트가 포함된 데이터 탐색 시 사용되는 시퀀스 분석 알고리즘입니다. 이 알고리즘에 대한 자세한 내용은 [Microsoft 시퀀스 클러스터링 알고리즘](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)을 참조하세요.  
  
> [!NOTE]  
>  발견된 패턴 및 모델에 사용된 수식에 대한 자세한 정보를 보려면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 일반 콘텐츠 트리 뷰어를 사용하십시오. 자세한 내용은 [Microsoft 일반 콘텐츠 트리 뷰어를 사용하여 모델 찾아보기](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) 또는 [Microsoft 일반 콘텐츠 트리 뷰어&#40;데이터 마이닝&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시퀀스 클러스터 뷰어는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 클러스터 뷰어와 유사한 기능 및 옵션을 제공합니다. 자세한 내용은 [Microsoft 클러스터 뷰어를 사용하여 모델 찾아보기](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)를 참조하세요.  
  
##  <a name="BKMK_ViewerTabs"></a> 뷰어 탭  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 마이닝 모델을 찾으면 해당 모델의 적절한 뷰어에서 데이터 마이닝 디자이너의 **마이닝 모델 뷰어** 탭에 해당 모델이 표시됩니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시퀀스 클러스터 뷰어는 시퀀스 클러스터링 마이닝 모델 탐색 시 사용할 수 있는 다음과 같은 탭을 제공합니다.  
  
-   [클러스터 다이어그램](#BKMK_Diagram)  
  
-   [클러스터 프로필](#BKMK_Profile)  
  
-   [클러스터 특징](#BKMK_Characteristics)  
  
-   [클러스터 판별](#BKMK_Discrimination)  
  
-   [클러스터 전환](#BKMK_Transitions)  
  
###  <a name="BKMK_Diagram"></a> 클러스터 다이어그램  
 **시퀀스 클러스터 뷰어의** 클러스터 다이어그램 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 탭은 마이닝 모델에 있는 모든 클러스터를 표시합니다. 두 클러스터를 연결하는 선의 음영은 클러스터의 유사성 정도를 나타냅니다. 음영이 옅거나 없으면 두 클러스터가 그다지 유사하지 않은 것입니다. 선이 어두울수록 링크의 유사성은 더 강해집니다. 클러스터의 오른쪽에 있는 슬라이더를 조정하여 뷰어에 표시되는 선의 개수를 조정할 수 있습니다. 슬라이더를 내리면 강력한 링크만 표시됩니다.  
  
 기본적으로 음영은 클러스터의 채우기를 나타냅니다. **음영****변수** 및 **상태** 옵션을 사용하여 음영이 나타내는 특성 및 상태 쌍을 선택할 수 있습니다. 음영이 어두울수록 특정 상태에 대한 특성 분포는 증가합니다. 음영이 밝을수록 분포는 감소합니다.  
  
 클러스터의 이름을 바꾸려면 해당 노드를 마우스 오른쪽 단추로 클릭한 다음 **클러스터 이름 바꾸기**를 선택합니다. 새 이름은 서버에 저장됩니다.  
  
 다이어그램에서 표시되는 섹션을 클립보드로 복사하려면 **그래프 뷰 복사**를 클릭합니다. 전체 다이어그램을 복사하려면 **전체 그래프 복사**를 클릭합니다. 또한 **확대** 와 **축소**를 사용하여 확대 및 축소할 수 있으며 **창에 맞게 다이어그램 크기 조정**을 사용하여 다이어그램을 화면에 맞출 수 있습니다.  
  
 [맨 위로 이동](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Profile"></a> 클러스터 프로필  
 **클러스터 프로필** 탭을 사용하여 모델의 알고리즘에서 만드는 클러스터를 전체적으로 볼 수 있습니다. 표에서 **채우기** 열 뒤에 있는 각 열은 해당 모델에 의해 검색된 클러스터를 나타냅니다. \<특성 > 행 여러 클러스터에 있는 데이터의 다른 시퀀스를 나타내며 및 \<특성 > 행은 클러스터에 포함 된 모든 항목 및 전체 분포에 설명 합니다.  
  
 **히스토그램 막대** 옵션은 히스토그램에 표시되는 막대의 수를 제어합니다. 선택한 것보다 더 많은 막대가 있는 경우 중요성이 가장 높은 막대가 유지되고 나머지 막대는 모두 회색 버킷으로 그룹화됩니다.  
  
 클러스터의 기본 이름을 좀 더 구체적인 이름으로 변경할 수 있습니다. 클러스터의 열 제목을 마우스 오른쪽 단추로 클릭하고 **클러스터 이름 바꾸기**를 선택하여 클러스터의 이름을 바꿉니다. **열 숨기기**를 선택하여 클러스터를 숨길 수 있으며 열을 마우스로 끌어 뷰어에서 열을 다시 정렬할 수도 있습니다.  
  
 클러스터를 더 크고 자세하게 보여 주는 창을 열려면 **상태** 열의 셀이나 뷰어의 히스토그램을 두 번 클릭합니다.  
  
 [맨 위로 이동](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Characteristics"></a> 클러스터 특징  
 **클러스터 특징** 탭을 사용하려면 **클러스터** 목록에서 클러스터를 선택합니다. 클러스터를 선택한 다음 해당 클러스터를 구성하는 특징을 확인할 수 있습니다. 클러스터에 포함된 특성은 **변수** 열에 나열되어 있으며 나열된 특성의 상태는 **값** 열에 나열되어 있습니다. 특성 상태는 클러스터에서 나타날 확률이 높은 순서에 따라 중요도 순으로 나열됩니다. 이러한 확률은 **확률** 열에 표시되어 있습니다.  
  
 [맨 위로 이동](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Discrimination"></a> 클러스터 판별  
 **클러스터 판별** 탭을 사용하여 두 클러스터의 특성을 비교하고 시퀀스의 항목이 다른 클러스터에 비해 특정 클러스터와 유사한 정도를 확인할 수 있습니다. **클러스터 1** 및 **클러스터 2** 목록을 사용하여 비교할 클러스터를 선택합니다. 뷰어는 클러스터 간의 가장 중요한 차이점을 확인하여 해당 차이점과 연결된 특성 상태를 중요도 순으로 표시합니다. 특성의 오른쪽에 있는 막대는 상태가 유사한 클러스터를 보여 주며 막대의 크기는 상태가 클러스터와 유사한 정도를 보여 줍니다.  
  
 [맨 위로 이동](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Transitions"></a> 클러스터 전환  
 **클러스터 전환** 탭에서 클러스터를 선택하면 선택한 클러스터의 시퀀스 상태 전환을 검색할 수 있습니다. 뷰어에서 각 노드는 시퀀스 열의 상태를 나타냅니다. 화살표는 두 상태 간의 전환 및 이 전환과 관련된 확률을 나타냅니다. 전환이 원래 노드로 돌아가면 화살표가 다시 원래 노드를 가리킬 수 있습니다.  
  
 점에서 시작하는 화살표는 노드가 시퀀스의 시작일 확률을 나타냅니다. null을 발생시키는 끝 가장자리는 노드가 시퀀스의 끝일 확률을 나타냅니다.  
  
 탭 왼쪽에 있는 슬라이더를 사용하여 노드 가장자리를 필터링할 수 있습니다.  
  
 [맨 위로 이동](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>관련 항목:  
 [마이닝 모델 뷰어 태스크 및 방법](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [마이닝 모델 뷰어 태스크 및 방법](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Microsoft Sequence Clustering Algorithm](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)   
 [데이터 마이닝 도구](../../analysis-services/data-mining/data-mining-tools.md)   
 [데이터 마이닝 모델 뷰어](../../analysis-services/data-mining/data-mining-model-viewers.md)   
 [Microsoft 클러스터 뷰어를 사용하여 모델 찾아보기](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)  
  
  

