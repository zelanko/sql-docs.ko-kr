---
title: 시계열 모델에 대 한 수식 보기 (데이터 마이닝) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], how-to topics
- ARTXP
- time series algorithms [Analysis Services]
- ARIMA
- time series [Analysis Services]
- Time Series Viewer [Analysis Services]
ms.assetid: 825ef719-2f44-4979-be01-5a81f54e1a53
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 43382b5dd8a20de1454bfc3d6a16aa68c99e34a5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66082595"
---
# <a name="view-the-formula-for-a-time-series-model-data-mining"></a>시계열 모델에 대한 수식 보기(데이터 마이닝)
  시계열 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 뷰어 Indata 마이닝 디자이너는 시계열 모델에 사용 되는 회귀 수식의 세부 정보를 보는 가장 쉬운 방법을 제공 합니다.  
  
 모델 콘텐츠를 쿼리하여 시계열 모델의 회귀 수식을 추출할 수 있습니다. 그러나 complete ARTXP 또는 ARIMA 수식을 보려면 모든 상수를 읽을 수 있는 형식으로 제공 하는 [Microsoft 시계열 뷰어](browse-a-model-using-the-microsoft-time-series-viewer.md)의 **마이닝 범례** 를 사용 하는 것이 좋습니다.  
  
 혼합 모델을 만들 경우 ARIMA 및 ARTXP 분석이 개별 트리에 만들어지고 모델을 나타내는 루트 노드에서 조인됩니다. ARIMA 트리와 ARTXP 트리는 구조가 아주 다릅니다. 예를 들어 ARTXP 트리는 실제로 의사 결정 트리와 같은 트리 구조인 반면에 ARIMA 트리는 이동 평균의 계열을 나타냅니다. 따라서 이러한 두 표현은 편의상 한 모델로 제공되지만 두 개의 독립적인 모델로 처리해야 합니다. 수식도 완전히 다르며 조합하거나 비교할 수 없습니다.  
  
 [Microsoft 일반 콘텐츠 트리 뷰어](../microsoft-generic-content-tree-viewer-data-mining.md)를 사용 하 여 시계열 모델을 볼 수도 있습니다. 시계열 모델의 내용에 대 한 자세한 내용은 [Analysis Services 데이터 마이닝&#41;&#40;시계열 모델에 대 한 마이닝 모델 콘텐츠 ](mining-model-content-for-time-series-models-analysis-services-data-mining.md)를 참조 하세요.  
  
### <a name="to-view-the-artxp-regression-formula-for-a-time-series-model"></a>시계열 모델의 ARTXP 회귀 수식을 보려면  
  
1.  
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 보려는 시계열 모델을 선택하고 **찾아보기**를 클릭합니다.  
  
     -- 또는 --  
  
     
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 시계열 모델을 선택한 다음 **마이닝 모델 뷰어** 탭을 클릭합니다.  
  
2.  
  **모델** 탭을 클릭합니다.  
  
3.  모델에 여러 개의 트리가 있는 경우 **트리** 드롭다운 목록에서 단일 트리를 선택합니다.  
  
    > [!NOTE]  
    >  데이터 계열이 둘 이상인 경우 모델에는 항상 여러 개의 트리가 있습니다. 그러나 **시계열 뷰어** 에 표시되는 트리 수는 [Microsoft 일반 콘텐츠 트리 뷰어](../microsoft-generic-content-tree-viewer-data-mining.md)에 표시되는 트리 수와 같지 않습니다. 시계열 뷰어에서는 각 데이터 계열의 ARIMA 및 ARTXP 정보를 단일 표현으로 조합하기 때문입니다.  
  
4.  트리의 리프 노드를 클릭합니다.  
  
     
  **데이터 계열** 이라는 레이블이 붙는 노드는 항상 리프 노드이며 수식을 포함할 수 있습니다. 
  **(All)** 노드에 자식 노드가 없는 경우 이 노드도 수식을 포함할 수 있습니다.  
  
5.  
  **마이닝 범례** 를 사용할 수 없는 경우 노드를 마우스 오른쪽 단추로 클릭하고 **범례 표시**를 선택합니다.  
  
     ARTXP 수식은 **마이닝 범례**의 첫 번째 부분에 **트리 노드 수식**으로 표시됩니다.  
  
### <a name="to-view-the-arima-formula-for-a-time-series-model"></a>시계열 모델의 ARIMA 수식을 보려면  
  
1.  
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 보려는 시계열 모델을 선택하고 **찾아보기**를 클릭합니다.  
  
     -- 또는 --  
  
     
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 시계열 모델을 선택한 다음 **마이닝 모델 뷰어** 탭을 클릭합니다.  
  
2.  
  **모델** 탭을 클릭합니다.  
  
3.  모델에 여러 개의 트리가 있는 경우 **트리** 드롭다운 목록에서 단일 트리를 선택합니다.  
  
    > [!NOTE]  
    >  데이터 계열이 둘 이상인 경우 모델에는 항상 여러 개의 트리가 있습니다.  
  
4.  트리의 노드를 클릭합니다.  
  
     ARIMA 수식은 **마이닝 범례**의 두 번째 부분에 **ARIMA 수식**으로 표시됩니다.  
  
5.  
  **마이닝 범례** 를 사용할 수 없는 경우 노드를 마우스 오른쪽 단추로 클릭하고 **범례 표시**를 선택합니다.  
  
## <a name="see-also"></a>참고 항목  
 [마이닝 모델 뷰어 태스크 및 방법](mining-model-viewer-tasks-and-how-tos.md)   
 [Microsoft 시계열 뷰어를 사용 하 여 모델 찾아보기](browse-a-model-using-the-microsoft-time-series-viewer.md)   
 [시계열 모델 쿼리 예제](time-series-model-query-examples.md)  
  
  
