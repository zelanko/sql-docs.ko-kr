---
title: 시계열에 대 한 수식을 보려면 모델 (데이터 마이닝) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0aaa1be07dcd5857585e7db3dbd4a78a44d41ff3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62659733"
---
# <a name="view-the-formula-for-a-time-series-model-data-mining"></a>시계열 모델에 대한 수식 보기(데이터 마이닝)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 마이닝을 사용하여 시계열 모델을 만든 경우 모든 상수를 읽을 수 있는 형식으로 제공하는 **Microsoft 시계열 뷰어** 의 [마이닝 범례](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-time-series-viewer.md)를 사용하면 모델에 대한 회귀 수식을 가장 쉽게 확인할 수 있습니다.  
  
### <a name="to-view-the-artxp-regression-formula-for-a-time-series-model"></a>시계열 모델의 ARTXP 회귀 수식을 보려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 보려는 시계열 모델을 선택하고 **찾아보기**를 클릭합니다.  
  
     -- 또는 --  
  
     [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 시계열 모델을 선택한 다음 **마이닝 모델 뷰어** 탭을 클릭합니다.  
  
2.  **모델** 탭을 클릭합니다.  
  
3.  모델에 여러 개의 트리가 있는 경우 **트리** 드롭다운 목록에서 단일 트리를 선택합니다.  
  
    > [!NOTE]  
    >  데이터 계열이 둘 이상인 경우 모델에는 항상 여러 개의 트리가 있습니다. 그러나 **시계열 뷰어** 에 표시되는 트리 수는 [Microsoft 일반 콘텐츠 트리 뷰어](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c)에 표시되는 트리 수와 같지 않습니다. 시계열 뷰어에서는 각 데이터 계열의 ARIMA 및 ARTXP 정보를 단일 표현으로 조합하기 때문입니다.  
  
4.  트리의 리프 노드를 클릭합니다.  
  
     **데이터 계열** 이라는 레이블이 붙는 노드는 항상 리프 노드이며 수식을 포함할 수 있습니다. **(All)** 노드에 자식 노드가 없는 경우 이 노드도 수식을 포함할 수 있습니다.  
  
5.  **마이닝 범례** 를 사용할 수 없는 경우 노드를 마우스 오른쪽 단추로 클릭하고 **범례 표시**를 선택합니다.  
  
     ARTXP 수식은 **마이닝 범례**의 첫 번째 부분에 **트리 노드 수식**으로 표시됩니다.  
  
     ![범례에는 시계열 수식 보기](../../analysis-services/data-mining/media/ssdm-timeserieslegend.png "범례에는 시계열 수식 보기")  
  
### <a name="to-view-the-arima-formula-for-a-time-series-model"></a>시계열 모델의 ARIMA 수식을 보려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 보려는 시계열 모델을 선택하고 **찾아보기**를 클릭합니다.  
  
     -- 또는 --  
  
     [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 시계열 모델을 선택한 다음 **마이닝 모델 뷰어** 탭을 클릭합니다.  
  
2.  **모델** 탭을 클릭합니다.  
  
3.  모델에 여러 개의 트리가 있는 경우 **트리** 드롭다운 목록에서 단일 트리를 선택합니다.  
  
    > [!NOTE]  
    >  데이터 계열이 둘 이상인 경우 모델에는 항상 여러 개의 트리가 있습니다.  
  
4.  트리의 노드를 클릭합니다.  
  
     ARIMA 수식은 **마이닝 범례**의 두 번째 부분에 **ARIMA 수식**으로 표시됩니다.  
  
5.  **마이닝 범례** 를 사용할 수 없는 경우 노드를 마우스 오른쪽 단추로 클릭하고 **범례 표시**를 선택합니다.  
  
### <a name="to-get-the-coefficients-and-terms-for-the-equation"></a>수식에 대한 계수 및 조건을 가져오려면  
  
1.  모델 콘텐츠에서 **내용 쿼리** 를 만들어 시계열 모델에 대한 회귀 수식의 조건 및 계수를 가져올 수도 있습니다.  
  
     자세한 내용은 [시간 시계열 모델 쿼리 예제](../../analysis-services/data-mining/time-series-model-query-examples.md)를 참조하세요.  
  
2.  또한 [Microsoft 일반 콘텐츠 트리 뷰어](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c)를 사용하여 시계열 모델을 찾아보고 조건 및 계수를 찾을 수 있습니다.  
  
     자세한 내용은 [시계열 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)를 참조하세요.  
  
    > [!NOTE]  
    >  ARIMA와 ARTXP 모델을 모두 사용하는 혼합 모델의 콘텐츠를 찾아보면 두 모델은 모델을 나타내는 루트 노드에서 결합된 별도의 트리에 있습니다. ARIMA 및 ARTXP 모델은 편의상 하나의 뷰어에 표시되지만 구조는 결합하거나 비교할 수 없는 수식과 마찬가지로 매우 다릅니다. ARTXP 트리는 의사 결정 트리와 더 유사한 반면 ARIMA 트리는 일련의 이동 평균을 나타냅니다.  
  
## <a name="see-also"></a>관련 항목  
 [마이닝 모델 뷰어 태스크 및 방법](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Microsoft 시계열 뷰어를 사용하여 모델 찾아보기](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-time-series-viewer.md)  
  
  
