---
title: "Microsoft Naive Bayes 뷰어를 사용 하 여 모델 찾아보기 | Microsoft Docs"
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
- discrimination [Analysis Services]
- naive bayes model [Analysis Services]
- Bayesian classifiers
- mining model content, viewing
- predictive modeling [Analysis Services]
- Naive Bayes Viewer [Analysis Services]
- data mining [Analysis Services], predictive modeling
- Microsoft Naive Bayes Viewer
- histograms [Analysis Services]
- mining models [Analysis Services], predictive modeling
- dependencies [Analysis Services]
ms.assetid: 19743095-63c1-4486-8c1d-2efc143243be
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ec5fa6be2358366b181b0608025d3d3a4b94a321
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="browse-a-model-using-the-microsoft-naive-bayes-viewer"></a>Microsoft Naive Bayes 뷰어를 사용하여 모델 찾아보기
  [!INCLUDE[msCoName](../../includes/msconame-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Naive Bayes 뷰어는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes 알고리즘을 사용하여 작성된 마이닝 모델을 표시합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes 알고리즘은 예측 모델링 태스크에 매우 적응력이 뛰어난 분류 알고리즘입니다. 이 알고리즘에 대한 자세한 내용은 [Microsoft Naive Bayes Algorithm](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)를 참조하십시오.  
  
 Naive Bayes 모델의 주 목적 중 하나는 데이터 집합의 데이터를 빨리 탐색하는 방법을 제공하는 것이기 때문에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes 뷰어는 예측 가능한 특성과 입력 특성 간의 상호 작용을 표시하는 여러 가지 방법을 제공합니다.  
  
> [!NOTE]  
>  발견된 패턴 및 모델에 사용된 수식에 대한 자세한 정보를 보려는 경우 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 일반 콘텐츠 트리 뷰어로 전환할 수 있습니다. 자세한 내용은 [Microsoft 일반 콘텐츠 트리 뷰어를 사용하여 모델 찾아보기](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) 또는 [Microsoft 일반 콘텐츠 트리 뷰어&#40;데이터 마이닝&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c)를 참조하세요.  
  
##  <a name="BKMK_ViewerTabs"></a> 뷰어 탭  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 마이닝 모델을 찾으면 해당 모델의 적절한 뷰어에서 데이터 마이닝 디자이너의 **마이닝 모델 뷰어** 탭에 해당 모델이 표시됩니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes 뷰어는 데이터 탐색을 위해 다음과 같은 탭을 제공합니다.  
  
-   [종속성 네트워크](#BKMK_Dependency)  
  
-   [특성 프로필](#BKMK_Profiles)  
  
-   [특성 특징](#BKMK_Characteristics)  
  
-   [특성 판별](#BKMK_Discrimination)  
  
##  <a name="BKMK_Dependency"></a> 종속성 네트워크  
 **종속성 네트워크** 탭은 모델의 입력 특성과 예측 가능한 특성 간의 종속성을 표시합니다. 뷰어의 왼쪽에 있는 슬라이더는 종속성 수준에 연결된 필터 역할을 합니다. 슬라이더를 내리면 강력한 링크만 표시됩니다.  
  
 노드를 선택하면 뷰어는 해당 노드와 관련된 종속성을 강조 표시합니다. 예를 들어 예측 가능한 노드를 선택하면 뷰어는 예측 가능한 노드를 예측하는 데 도움을 주는 각 노드도 강조 표시합니다.  
  
 뷰어의 아래쪽에 있는 범례는 색 코드를 그래프에 있는 종속성 유형에 연결합니다. 예를 들어 예측 가능한 노드를 선택하면 예측 가능한 노드는 옥색으로 표시되며 선택한 노드를 예측하는 노드는 주황색으로 표시됩니다.  
  
 [맨 위로 이동](#BKMK_ViewerTabs)  
  
##  <a name="BKMK_Profiles"></a> 특성 프로필  
 **특성 프로필** 탭은 히스토그램을 표로 표시합니다. 이 표를 사용하여 **예측 가능** 상자에서 선택한 예측 가능한 특성을 모델의 다른 모든 특성과 비교할 수 있습니다. 이 탭에 있는 각 열은 예측 가능한 특성의 상태를 나타냅니다. 예측 가능한 특성에 많은 상태가 있으면 **히스토그램 막대**를 조절하여 히스토그램에 나타나는 상태 수를 변경할 수 있습니다. 선택한 수가 특성의 전체 상태 수보다 적으면 지원 순서대로 상태가 나열되고 나머지 상태는 회색의 단일 버킷으로 수집됩니다.  
  
 히스토그램의 색을 특성 상태에 연결하는 마이닝 범례를 표시하려면 **범례 표시** 확인란을 클릭합니다. 또한 마이닝 범례는 선택하는 각 특성 값 쌍에 대해 사례 배포를 표시합니다.  
  
 표 내용을 클립보드에 HTML 테이블로 복사하려면 **특성 프로필** 탭을 마우스 오른쪽 단추로 클릭하고 **복사**를 선택합니다.  
  
 [맨 위로 이동](#BKMK_ViewerTabs)  
  
##  <a name="BKMK_Characteristics"></a> 특성 특징  
 **특성 특징** 탭을 사용하려면 **특성** 목록에서 예측 가능한 특성을 선택하고 **값** 목록에서 선택한 특성의 상태를 선택합니다. 이러한 변수를 설정하면 **특성 특징** 탭에 선택한 특성의 선택한 사례와 연결된 특성의 상태가 표시됩니다. 특성은 중요도 순서로 정렬됩니다.  
  
 [맨 위로 이동](#BKMK_ViewerTabs)  
  
##  <a name="BKMK_Discrimination"></a> 특성 판별  
 **특성 판별** 탭을 사용하려면 **특성**, **값 1**및 **값 2** 목록에서 예측 가능한 특성과 두 가지 상태를 선택합니다. 그러면 **특성 판별** 탭에 있는 표의 열에 다음 정보가 표시됩니다.  
  
 **특성**  
 예측 가능한 특성의 한 가지 상태와 유사성이 큰 상태가 포함된 데이터 집합의 다른 특성을 나열합니다.  
  
 **값**  
 **특성** 열의 특성 값을 보여 줍니다.  
  
 **유사성 \<값 1 >**  
 특성 값이 **값 1**에 표시된 예측 가능한 특성 값과 얼마나 유사한지 나타내는 색이 지정된 막대를 표시합니다.  
  
 **유사성 \<값 2 >**  
 특성 값이 **값 2**에 표시된 예측 가능한 특성 값과 얼마나 유사한지 나타내는 색이 지정된 막대를 표시합니다.  
  
 [맨 위로 이동](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>관련 항목:  
 [Microsoft Naive Bayes Algorithm](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)   
 [마이닝 모델 뷰어 태스크 및 방법](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [데이터 마이닝 도구](../../analysis-services/data-mining/data-mining-tools.md)   
 [데이터 마이닝 모델 뷰어](../../analysis-services/data-mining/data-mining-model-viewers.md)  
  
  

