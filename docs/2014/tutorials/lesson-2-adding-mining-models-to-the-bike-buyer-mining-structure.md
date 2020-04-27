---
title: '2 단원: 자전거 구매자 마이닝 구조에 마이닝 모델 추가 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 03fe44c5-6452-4ed0-95f6-9682670c0f52
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: de65fb7a85154f607cd8f266faec4621cdc41476
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63131740"
---
# <a name="lesson-2-adding-mining-models-to-the-bike-buyer-mining-structure"></a>2단원: Bike Buyer 마이닝 구조에 마이닝 모델 추가
  이 단원에서는 [1 단원: 자전거 구매자 마이닝 구조 만들기](../../2014/tutorials/lesson-1-creating-the-bike-buyer-mining-structure.md)에서 만든 자전거 구매자 마이닝 구조에 두 개의 마이닝 모델을 추가 합니다. 이러한 마이닝 모델을 추가하면 한 모델을 사용하여 데이터를 탐색하고 다른 모델을 사용하여 예측을 만들 수 있습니다.  
  
 잠재적 고객이 해당 특성으로 분류 될 수 있는 방법을 살펴보려면 [Microsoft 클러스터링 알고리즘](../../2014/analysis-services/data-mining/microsoft-clustering-algorithm.md)을 기반으로 하는 마이닝 모델을 만듭니다. 이후 단원에서는 이 알고리즘에서 비슷한 특징을 공유하는 고객 집단을 찾는 방법을 알아 봅니다. 예를 들어 여러 특정 고객이 서로 근처에 살고 자전거로 출퇴근하며 비슷한 학력을 갖는 경향이 있음을 알게 될 수 있습니다. 이러한 집단을 사용하여 고객 간의 상호 연관성을 보다 잘 파악할 수 있으며 이러한 정보를 사용하여 특정 고객을 대상으로 하는 마케팅 전략을 세울 수 있습니다.  
  
 잠재 고객이 자전거를 구입할 가능성이 있는지 여부를 예측 하기 위해 [Microsoft 의사 결정 트리 알고리즘](../../2014/analysis-services/data-mining/microsoft-decision-trees-algorithm.md)을 기반으로 마이닝 모델을 만듭니다. 이 알고리즘에서는 각 잠재 고객과 관련된 정보를 조사하여 해당 고객이 자전거를 구입할 지 여부를 예측하는 데 유용한 특징을 찾아냅니다. 그런 다음 이전 자전거 구매자의 특징 값과 새 잠재 고객의 특징 값을 비교하여 새 잠재 고객이 자전거를 구입할 가능성이 있는지 여부를 확인합니다.  
  
## <a name="alter-mining-structure-statement"></a>ALTER MINING STRUCTURE 문  
 마이닝 구조에 마이닝 모델을 추가 하려면 [ALTER 마이닝 structure &#40;DMX&#41;](/sql/dmx/alter-mining-structure-dmx?view=sql-server-2016) 문을 사용 합니다. 이 문의 코드는 다음 부분으로 나눌 수 있습니다.  
  
-   마이닝 구조 식별  
  
-   마이닝 모델 이름 지정  
  
-   키 열 정의  
  
-   입력 및 예측 가능한 열 정의  
  
-   알고리즘 및 매개 변수 변경 내용 식별  
  
 다음은 ALTER MINING MODEL 문의 일반적인 예입니다.  
  
```  
ALTER MINING STRUCTURE [<mining structure name>]  
ADD MINING MODEL [<mining model name>]  
(  
    [<key column>],  
    <mining model columns>,  
) USING <algorithm name>( <algorithm parameters> )  
WITH FILTER (<expression>)  
```  
  
 코드의 첫 번째 줄에서는 마이닝 모델을 추가할 기존 마이닝 구조를 식별합니다.  
  
```  
ALTER MINING STRUCTURE [<mining structure name>]  
```  
  
 코드의 다음 줄에서는 마이닝 구조에 추가할 마이닝 모델의 이름을 지정합니다.  
  
```  
ADD MINING MODEL [<mining model name>]  
```  
  
 DMX에서 개체의 이름을 지정 하는 방법에 대 한 자세한 내용은 [id &#40;dmx&#41;](/sql/dmx/identifiers-dmx)를 참조 하세요.  
  
 코드의 다음 줄에서는 마이닝 모델에서 사용할 마이닝 구조의 열을 정의합니다.  
  
```  
[<key column>],  
<mining model columns>  
```  
  
 마이닝 구조에 이미 있는 열만 사용할 수 있으며 목록의 첫 번째 열은 마이닝 구조의 키 열이어야 합니다.  
  
 코드의 다음 줄에서는 마이닝 모델을 생성하는 마이닝 알고리즘과 알고리즘에 설정할 수 있는 알고리즘 매개 변수를 정의합니다.  
  
```  
) USING <algorithm name>( <algorithm parameters> )  
```  
  
 조정할 수 있는 알고리즘 매개 변수에 대 한 자세한 내용은 [Microsoft 의사 결정 트리 알고리즘](../../2014/analysis-services/data-mining/microsoft-decision-trees-algorithm.md) 및 [microsoft 클러스터링 알고리즘](../../2014/analysis-services/data-mining/microsoft-clustering-algorithm.md)을 참조 하세요.  
  
 다음 구문을 사용하여 마이닝 모델의 열이 예측에 사용되도록 지정할 수 있습니다.  
  
```  
<mining model column> PREDICT  
```  
  
 선택 사항인 코드의 마지막 줄에서는 모델을 학습하고 테스트할 때 적용되는 필터를 정의합니다. 마이닝 모델에 필터를 적용 하는 방법에 대 한 자세한 내용은 [마이닝 모델에 대 한 필터 &#40;Analysis Services 데이터 마이닝&#41;](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)를 참조 하세요.  
  
## <a name="lesson-tasks"></a>단원 태스크  
 이 단원에서는 다음 태스크를 수행합니다.  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] 의사 결정 트리 알고리즘을 사용하여 Bike Buyer 구조에 의사 결정 트리 마이닝 모델 추가  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] 클러스터링 알고리즘을 사용하여 Bike Buyer 구조에 클러스터링 마이닝 모델 추가  
  
-   모든 경우에 대한 결과를 보기 위해 두 모델에 아직 필터를 추가하지 않습니다.  
  
## <a name="adding-a-decision-tree-mining-model-to-the-structure"></a>구조에 의사 결정 트리 마이닝 모델 추가  
 첫 번째 단계는 [!INCLUDE[msCoName](../includes/msconame-md.md)] 의사 결정 트리 알고리즘을 기반으로 마이닝 모델을 추가하는 것입니다.  
  
#### <a name="to-add-a-decision-tree-mining-model"></a>의사 결정 트리 마이닝 모델을 추가하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]의 인스턴스를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 가리킨 다음 **DMX** 를 클릭하여 쿼리 편집기와 비어 있는 새 쿼리를 엽니다.  
  
2.  ALTER MINING STRUCTURE 문의 일반적인 예를 빈 쿼리에 복사합니다.  
  
3.  다음 내용을  
  
    ```  
    <mining structure name>   
    ```  
  
     다음으로 바꿉니다.  
  
    ```  
    [Bike Buyer]  
    ```  
  
4.  다음 내용을  
  
    ```  
    <mining model name>   
    ```  
  
     다음으로 바꿉니다.  
  
    ```  
    Decision Tree  
    ```  
  
5.  다음 내용을  
  
    ```  
    <mining model columns>,  
    ```  
  
     다음으로 바꿉니다.  
  
    ```  
    (  
       CustomerKey,  
       [Age],  
       [Bike Buyer] PREDICT,  
       [Commute Distance],  
       [Education],  
       [Gender],  
       [House Owner Flag],  
       [Marital Status],  
       [Number Cars Owned],  
       [Number Children At Home],  
       [Occupation],  
       [Region],  
       [Total Children],  
       [Yearly Income]  
    ```  
  
     이 경우 `[Bike Buyer]` 열을 PREDICT 열로 지정했습니다.  
  
6.  다음 내용을  
  
    ```  
    USING <algorithm name>( <algorithm parameters> )   
    ```  
  
     다음으로 바꿉니다.  
  
    ```  
    Using Microsoft_Decision_Trees  
    WITH DRILLTHROUGH  
    ```  
  
     WITH DRILLTHROUGH 문을 사용하면 마이닝 모델을 작성하는 데 사용된 사례를 탐색할 수 있습니다.  
  
     이제 결과 문이 다음과 같아야 합니다.  
  
    ```  
    ALTER MINING STRUCTURE [Bike Buyer]  
    ADD MINING MODEL [Decision Tree]  
    (  
       CustomerKey,  
       [Age],  
       [Bike Buyer] PREDICT,  
       [Commute Distance],  
       [Education],  
       [Gender],  
       [House Owner Flag],  
       [Marital Status],  
       [Number Cars Owned],  
       [Number Children At Home],  
       [Occupation],  
       [Region],  
       [Total Children],  
       [Yearly Income]  
    ) USING Microsoft_Decision_Trees  
    WITH DRILLTHROUGH  
    ```  
  
7.  **파일** 메뉴에서 **다른 이름으로 DMXQuery1.dmx 저장**을 클릭합니다.  
  
8.  다른 이름 **으로 저장** 대화 상자에서 해당 폴더로 이동한 다음 파일 `DT_Model.dmx`이름을로 합니다.  
  
9. 도구 모음에서 **실행** 단추를 클릭합니다.  
  
## <a name="adding-a-clustering-mining-model-to-the-structure"></a>구조에 클러스터링 마이닝 모델 추가  
 이제 [!INCLUDE[msCoName](../includes/msconame-md.md)] 클러스터링 알고리즘을 기반으로 Bike Buyer 마이닝 구조에 마이닝 모델을 추가할 수 있습니다. 클러스터링 마이닝 모델은 마이닝 구조에 정의된 모든 열을 사용하기 때문에 바로 가기를 사용하여 마이닝 열 정의를 생략하여 구조에 모델을 추가할 수 있습니다.  
  
#### <a name="to-add-a-clustering-mining-model"></a>클러스터링 마이닝 모델을 추가하려면  
  
1.  **개체 탐색기**에서 인스턴스 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]를 마우스 오른쪽 단추로 클릭 하 고 **새 쿼리**를 가리킨 다음 **DMX** 를 클릭 하 여 쿼리 편집기 열기와 비어 있는 새 쿼리를 엽니다.  
  
2.  ALTER MINING STRUCTURE 문의 일반적인 예를 빈 쿼리에 복사합니다.  
  
3.  다음 내용을  
  
    ```  
    <mining structure name>   
    ```  
  
     다음으로 바꿉니다.  
  
    ```  
    [Bike Buyer]  
    ```  
  
4.  다음 내용을  
  
    ```  
    <mining model>   
    ```  
  
     다음으로 바꿉니다.  
  
    ```  
    Clustering Model  
    ```  
  
5.  다음 내용을 삭제합니다.  
  
    ```  
    (  
        [<key column>],  
        <mining model columns>,  
    )  
    ```  
  
6.  다음 내용을  
  
    ```  
    USING <algorithm name>( <algorithm parameters> )  
    ```  
  
     다음으로 바꿉니다.  
  
    ```  
    USING Microsoft_Clustering  
    ```  
  
     이제 전체 문이 다음과 같아야 합니다.  
  
    ```  
    ALTER MINING STRUCTURE [Bike Buyer]  
    ADD MINING MODEL [Clustering]  
    USING Microsoft_Clustering   
    ```  
  
7.  **파일** 메뉴에서 **다른 이름으로 DMXQuery1.dmx 저장**을 클릭합니다.  
  
8.  다른 이름 **으로 저장** 대화 상자에서 해당 폴더로 이동한 다음 파일 `Clustering_Model.dmx`이름을로 합니다.  
  
9. 도구 모음에서 **실행** 단추를 클릭합니다.  
  
 다음 단원에서는 모델과 마이닝 구조를 처리합니다.  
  
## <a name="next-lesson"></a>다음 단원  
 [3단원: Bike Buyer 마이닝 구조 처리](../../2014/tutorials/lesson-3-processing-the-bike-buyer-mining-structure.md)  
  
  
