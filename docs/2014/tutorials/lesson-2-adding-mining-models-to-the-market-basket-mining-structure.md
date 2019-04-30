---
title: '2단원: Market Basket 마이닝 구조에 마이닝 모델 추가 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d96a7a7d-35d7-4b34-abb5-f0822c256253
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b9573d9359983e33cf23533787c26039572710ea
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63204725"
---
# <a name="lesson-2-adding-mining-models-to-the-market-basket-mining-structure"></a>2단원: Market Basket 마이닝 구조에 마이닝 모델 추가
  이 단원에서는 두 개의 마이닝 모델 추가에서 만든 Market Basket 마이닝 구조를 [1 단원: Market Basket 마이닝 구조 만들기](../../2014/tutorials/lesson-1-creating-the-market-basket-mining-structure.md)합니다. 이러한 마이닝 모델을 사용하여 예측을 만들 수 있습니다.  
  
 고객이 동시에 구입하는 경향이 있는 제품 유형을 예측하기 위해 [Microsoft Association Algorithm](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md) 및 *MINIMUM_PROBABILTY* 매개 변수에 대한 서로 다른 두 값을 사용하여 두 개의 마이닝 모델을 만듭니다.  
  
 *MINIMUM_PROBABILTY* 는 규칙에 있어야 할 최소 확률을 지정하여 마이닝 모델이 포함할 규칙 수를 결정하는 데 도움이 되는 [!INCLUDE[msCoName](../includes/msconame-md.md)] 연결 알고리즘 매개 변수입니다. 예를 들어 이 값을 0.4로 설정하면 규칙에서 설명하는 제품 조합의 발생 확률이 40% 이상인 경우에만 규칙을 생성할 수 있도록 지정합니다.  
  
 *MINIMUM_PROBABILTY* 매개 변수 변경의 결과는 이후 단원에서 볼 수 있습니다.  
  
## <a name="alter-mining-structure-statement"></a>ALTER MINING STRUCTURE 문  
 마이닝 구조에 중첩된 테이블이 포함 된 마이닝 모델을 추가 하려면 사용 합니다 [ALTER MINING STRUCTURE &#40;DMX&#41; ](/sql/dmx/alter-mining-structure-dmx?view=sql-server-2016) 문입니다. 이 문의 코드는 다음 부분으로 나눌 수 있습니다.  
  
-   마이닝 구조 식별  
  
-   마이닝 모델 이름 지정  
  
-   키 열 정의  
  
-   입력 및 예측 가능한 열 정의  
  
-   중첩 테이블 열 정의  
  
-   알고리즘 및 매개 변수 변경 내용 식별  
  
 다음은 구조에 중첩 테이블 열을 포함하는 마이닝 모델을 추가하는 `ALTER MINING STRUCTURE` 문의 일반적인 예입니다.  
  
```  
ALTER MINING STRUCTURE [<Mining Structure Name>]  
ADD MINING MODEL [<Mining Model Name>]  
(  
    [<key column>],  
    <mining model column> <usage>,  
    <table columns>  
    (  [<nested key column>],  
       <nested mining model columns> )  
) USING <algorithm>( <algorithm parameters> )  
```  
  
 코드의 첫 번째 줄에서는 마이닝 모델을 추가할 기존 마이닝 구조를 식별합니다.  
  
```  
ALTER MINING STRUCTURE [<mining structure name>]  
```  
  
 코드의 다음 줄에서는 마이닝 구조에 추가할 마이닝 모델의 이름을 지정합니다.  
  
```  
ADD MINING MODEL [<mining model name>]  
```  
  
 개체의 확장 DMX (Data Mining) 이름을 지정 하는 방법에 대 한 내용은 [식별자 &#40;DMX&#41;](/sql/dmx/identifiers-dmx)합니다.  
  
 코드의 다음 줄에서는 마이닝 모델에서 사용할 마이닝 구조의 열을 정의합니다.  
  
```  
[<key column>],  
<mining model columns> <usage>,  
```  
  
 마이닝 구조에 이미 있는 열만 사용할 수 있습니다.  
  
 마이닝 모델 열 목록의 첫 번째 열은 마이닝 구조의 키 열이어야 합니다. 그러나 입력 필요가 없습니다 `KEY` 후 키 열 사용법을 지정 합니다. 이는 마이닝 구조를 만들 때 해당 열을 키로 이미 정의했기 때문입니다.  
  
 나머지 줄에서는 새 마이닝 모델에서의 열 사용법을 지정합니다. 다음 구문을 사용하여 마이닝 모델의 열이 예측에 사용되도록 지정할 수 있습니다.  
  
```  
<column name> PREDICT,  
```  
  
 사용법을 지정하지 않는 경우 목록에 데이터 마이닝 구조 열을 포함할 필요가 없습니다. 참조된 데이터 마이닝 구조에 사용되는 모든 열은 해당 구조를 기반으로 하는 마이닝 모델에서 자동으로 사용할 수 있게 됩니다. 그러나 사용자가 사용법을 지정하지 않는 한 모델에서는 학습에 해당 열을 사용하지 않습니다.  
  
 코드의 마지막 줄에서는 마이닝 모델 생성에 사용할 알고리즘 및 알고리즘 매개 변수를 정의합니다.  
  
```  
) USING <algorithm>( <algorithm parameters> )  
```  
  
## <a name="lesson-tasks"></a>단원 태스크  
 이 단원에서는 다음 태스크를 수행합니다.  
  
-   기본 확률을 사용하여 구조에 연결 마이닝 모델 추가  
  
-   수정된 확률을 사용하여 구조에 연결 마이닝 모델 추가  
  
## <a name="adding-an-association-mining-model-to-the-structure-using-the-default-minimumprobability"></a>MINIMUM_PROBABILITY의 기본값을 사용하여 구조에 연결 마이닝 모델 추가  
 Market Basket 마이닝 구조에 새 마이닝 모델을 기반으로 추가 하는 첫 번째 작업은 [!INCLUDE[msCoName](../includes/msconame-md.md)] 에 대 한 기본값을 사용 하는 연결 알고리즘 *MINIMUM_PROBABILITY*합니다.  
  
#### <a name="to-add-an-association-mining-model"></a>연결 마이닝 모델을 추가하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]인스턴스를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 가리킨 다음 **DMX**를 클릭합니다.  
  
     비어 있는 새 쿼리가 포함된 쿼리 편집기가 열립니다.  
  
    > [!NOTE]  
    >  특정 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스에 대해 DMX 쿼리를 만들려면 인스턴스 대신 데이터베이스를 마우스 오른쪽 단추로 클릭하십시오.  
  
2.  `ALTER MINING STRUCTURE` 문의 일반적인 예를 빈 쿼리에 복사합니다.  
  
3.  다음 내용을  
  
    ```  
    <mining structure name>   
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    [Market Basket]  
    ```  
  
4.  다음 내용을  
  
    ```  
    <mining model name>   
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    [Default Association]  
    ```  
  
5.  다음 내용을  
  
    ```  
    [<key column>],  
    <mining model columns>,  
    <table columns>  
    (  [<nested key column>],  
       <nested mining model columns> )  
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    OrderNumber,  
        [Products] PREDICT (  
            [Model]  
        )  
    ```  
  
     이 경우 `[Products]` 테이블을 예측 가능한 열로 지정했습니다.`.` 또한 `[Model]` 열은 중첩 테이블의 키 열이므로 중첩 테이블 열 목록에 포함되었습니다.  
  
    > [!NOTE]  
    >  중첩 키는 사례 키와 다릅니다. 사례 키는 사례의 고유 식별자인 반면 중첩 키는 모델링할 특성입니다.  
  
6.  다음 내용을  
  
    ```  
    USING <algorithm>( <algorithm parameters> )  
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    Using Microsoft_Association_Rules  
    ```  
  
     이제 결과 문이 다음과 같아야 합니다.  
  
    ```  
    ALTER MINING STRUCTURE [Market Basket]  
    ADD MINING MODEL [Default Association]  
    (  
        OrderNumber,  
        [Products] PREDICT (  
            [Model]  
        )  
    )  
    Using Microsoft_Association_Rules  
    ```  
  
7.  **파일** 메뉴에서 **다른 이름으로 DMXQuery1.dmx 저장**을 클릭합니다.  
  
8.  에 **다른 이름으로 저장** 대화 상자에서 적절 한 폴더로 이동 하 고 파일 이름을 `Default_Association_Model.dmx`입니다.  
  
9. 도구 모음에서 **실행** 단추를 클릭합니다.  
  
## <a name="adding-an-association-mining-model-to-the-structure-changing-the-default-minimumprobability"></a>MINIMUM_PROBABILITY의 기본값을 변경하여 구조에 연결 마이닝 모델 추가  
 다음 태스크는 [!INCLUDE[msCoName](../includes/msconame-md.md)] 연결 알고리즘을 기반으로 Market Basket 마이닝 구조에 새 마이닝 모델을 추가하고 MINIMUM_PROBABILITY의 기본값을 0.01로 변경하는 것입니다. 매개 변수를 변경하면 [!INCLUDE[msCoName](../includes/msconame-md.md)] 연결 알고리즘에서 더 많은 규칙을 만듭니다.  
  
#### <a name="to-add-an-association-mining-model"></a>연결 마이닝 모델을 추가하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]인스턴스를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 가리킨 다음 **DMX**를 클릭합니다.  
  
     비어 있는 새 쿼리가 포함된 쿼리 편집기가 열립니다.  
  
2.  `ALTER MINING STRUCTURE` 문의 일반적인 예를 빈 쿼리에 복사합니다.  
  
3.  다음 내용을  
  
    ```  
    <mining structure name>   
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    Market Basket  
    ```  
  
4.  다음 내용을  
  
    ```  
    <mining model name>   
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    [Modified Association]  
    ```  
  
5.  다음 내용을  
  
    ```  
    <mining model columns>,  
    <table columns>  
    (  [<nested key column>],  
       <nested mining model columns> )  
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    OrderNumber,  
    [Products] PREDICT (  
            [Model]  
        )  
    ```  
  
     이 경우 `[Products]` 테이블을 예측 가능한 열로 지정했습니다. 또한 `[MODEL]` 열은 중첩 테이블의 키 열이므로 목록에 포함되었습니다.  
  
6.  다음 내용을  
  
    ```  
    USING <algorithm>( <algorithm parameters> )  
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    USING Microsoft_Association_Rules (Minimum_Probability = 0.1)  
    ```  
  
     이제 결과 문이 다음과 같아야 합니다.  
  
    ```  
    ALTER MINING STRUCTURE [Market Basket]  
    ADD MINING MODEL [Modified Assocation]  
    (  
        OrderNumber,  
        [Products] PREDICT (  
            [Model]  
        )  
    )  
    USING Microsoft_Association_Rules (Minimum_Probability = 0.1)  
    ```  
  
7.  **파일** 메뉴에서 **다른 이름으로 DMXQuery1.dmx 저장**을 클릭합니다.  
  
8.  에 **다른 이름으로 저장** 대화 상자에서 적절 한 폴더로 이동 하 고 파일 이름을 `Modified Association_Model.dmx`입니다.  
  
9. 도구 모음에서 **실행** 단추를 클릭합니다.  
  
 다음 단원에서는 Market Basket 마이닝 구조를 연결된 해당 마이닝 모델과 함께 처리합니다.  
  
## <a name="next-lesson"></a>다음 단원  
 [3단원: Market Basket 마이닝 구조 처리](../../2014/tutorials/lesson-3-processing-the-market-basket-mining-structure.md)  
  
  
