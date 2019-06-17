---
title: '4단원: Bike Buyer 마이닝 모델 찾아보기 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 8de3c500-f881-42da-a096-b6c03300d58d
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 709df371d840d4b24e420b4fcd08750fd31e8075
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63070895"
---
# <a name="lesson-4-browsing-the-bike-buyer-mining-models"></a>4단원: Bike Buyer 마이닝 모델 찾아보기
  이 단원에서는 사용할지 합니다 [SELECT (DMX)](/sql/dmx/select-dmx) 문을에서는 의사 결정 트리 및 클러스터링 마이닝 모델에서 만든 [단원 2: 예측 마이닝 구조에 마이닝 모델 추가](../../2014/tutorials/lesson-2-adding-mining-models-to-the-bike-buyer-mining-structure.md)합니다.  
  
 마이닝 모델에 포함된 열은 마이닝 구조에서 정의한 열이 아니라 알고리즘에서 찾은 경향 및 패턴을 설명하는 특정 열 집합입니다. 이러한 마이닝 모델 열에 설명 되어는 [DMSCHEMA_MINING_MODEL_CONTENT 행 집합](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset) 스키마 행 집합입니다. 예를 들어 내용 스키마 행 집합의 MODEL_NAME 열에는 마이닝 모델의 이름이 포함되어 있습니다. 클러스터링 마이닝 모델의 경우 NODE_CAPTION 열에는 각 클러스터의 이름이 포함되어 있으며 NODE_DESCRIPTION 열에는 각 클러스터의 특징에 대한 설명이 포함되어 있습니다. SELECT를 사용 하 여 이러한 열을 찾아보면 \<모델 >. DMX에서 콘텐츠 문입니다. 이 문을 사용하여 마이닝 모델 생성에 사용된 데이터도 탐색할 수 있습니다. 이 문을 사용하려면 마이닝 구조에 드릴스루를 설정해야 합니다. 문에 대 한 자세한 내용은 참조 하세요. [선택에서 &#60;모델&#62;합니다. 경우 &#40;DMX&#41;](/sql/dmx/select-from-model-content-dmx)합니다.  
  
 또한 SELECT DISTINCT 문을 사용하여 불연속 열의 모든 상태를 반환할 수 있습니다. 예를 들어 Gender 열에서 이 작업을 수행하면 쿼리는 `male` 및 `female`을 반환합니다.  
  
## <a name="lesson-tasks"></a>단원 태스크  
 이 단원에서는 다음 태스크를 수행합니다.  
  
-   마이닝 모델 내에 포함된 내용 탐색  
  
-   마이닝 모델의 학습에 사용된 원본 데이터에서 사례 반환  
  
-   특정 불연속 열에 가능한 다양한 상태 탐색  
  
## <a name="returning-the-content-of-a-mining-model"></a>마이닝 모델의 내용 반환  
 이 단원에서 사용 하 여 합니다 [선택에서 &#60;모델&#62;합니다. 콘텐츠 &#40;DMX&#41; ](/sql/dmx/select-from-model-dimension-content-dmx) 문을 클러스터링 모델의 내용을 반환 합니다.  
  
 다음은 SELECT FROM의 일반적인 예 \<모델 >. 콘텐츠 문:  
  
```  
SELECT <select list> FROM [<mining model>].CONTENT  
WHERE <where clause>  
```  
  
 코드의 첫 번째 줄에서는 마이닝 모델 내용에서 반환할 열과 이 열이 연결된 마이닝 모델을 정의합니다.  
  
```  
SELECT <select list> FROM [<mining model].CONTENT  
```  
  
 마이닝 모델 이름 옆에 있는 .CONTENT 절은 해당 마이닝 모델에서 내용을 반환함을 지정합니다. 마이닝 모델에 포함 된 열에 대 한 자세한 내용은 참조 하세요. [DMSCHEMA_MINING_MODEL_CONTENT 행 집합](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset)합니다.  
  
 필요에 따라 코드의 마지막 줄을 사용하여 문에서 반환한 결과를 필터링할 수 있습니다.  
  
```  
WHERE <where clause>  
```  
  
 예를 들어 쿼리 결과를 사례 수가 많은 클러스터만으로 제한하려는 경우 SELECT 문에 다음 WHERE 절을 추가합니다.  
  
```  
WHERE NODE_SUPPORT > 100  
```  
  
 WHERE 문 사용에 대 한 자세한 내용은 참조 하세요. [선택 &#40;DMX&#41;](/sql/dmx/select-dmx)합니다.  
  
#### <a name="to-return-the-content-of-the-clustering-mining-model"></a>클러스터링 마이닝 모델의 내용을 반환하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]인스턴스를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 가리킨 다음 **DMX**를 클릭합니다.  
  
     비어 있는 새 쿼리가 포함된 쿼리 편집기가 열립니다.  
  
2.  SELECT의 일반적인 예를 복사 \<모델 >. 빈 쿼리에 콘텐츠 문입니다.  
  
3.  다음 내용을  
  
    ```  
    <select list>   
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    *  
    ```  
  
     바꿀 수도 있습니다 * 목록이 포함 된 열 중 하나는 [DMSCHEMA_MINING_MODEL_CONTENT 행 집합](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset)합니다.  
  
4.  다음 내용을  
  
    ```  
    [<mining model>]   
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    [Clustering]  
    ```  
  
     이제 전체 문이 다음과 같아야 합니다.  
  
    ```  
    SELECT * FROM [Clustering].CONTENT  
    ```  
  
5.  **파일** 메뉴에서 **다른 이름으로 DMXQuery1.dmx 저장**을 클릭합니다.  
  
6.  에 **다른 이름으로 저장** 대화 상자에서 적절 한 폴더로 이동 하 고 파일 이름을 `SELECT_CONTENT.dmx`입니다.  
  
7.  도구 모음에서 **실행** 단추를 클릭합니다.  
  
     쿼리에서 마이닝 모델의 내용이 반환됩니다.  
  
## <a name="use-drillthrough"></a>드릴스루 사용  
 다음 단계는 드릴스루 문을 사용하여 의사 결정 트리 마이닝 모델의 학습에 사용된 사례의 샘플링을 반환하는 것입니다. 이 단원에서 사용 하 여 합니다 [선택에서 &#60;모델&#62;합니다. 경우 &#40;DMX&#41; ](/sql/dmx/select-from-model-content-dmx) 문을 의사 결정 트리 모델의 내용을 반환 합니다.  
  
 다음은 SELECT FROM의 일반적인 예 \<모델 >. CASES 문은:  
  
```  
SELECT <select list>   
FROM [<mining model>].CASES  
WHERE IsInNode('<node id>')  
```  
  
 코드의 첫 번째 줄에서는 원본 데이터에서 반환할 열과 이 열이 포함된 마이닝 모델을 정의합니다.  
  
```  
SELECT <select list> FROM [<mining model>].CASES  
```  
  
 .CASES 절은 드릴스루 쿼리를 수행함을 지정합니다. 드릴스루를 사용하려면 마이닝 모델을 만들 때 드릴스루를 설정해야 합니다.  
  
 코드의 마지막 줄은 선택 사항이며 사례를 요청할 마이닝 모델의 노드를 지정합니다.  
  
```  
WHERE IsInNode('<node id>')  
```  
  
 IsInNode가 있는 WHERE 문 사용에 대 한 자세한 내용은 참조 하세요. [선택에서 &#60;모델&#62;합니다. 경우 &#40;DMX&#41;](/sql/dmx/select-from-model-content-dmx)합니다.  
  
#### <a name="to-return-the-cases-that-were-used-to-train-the-mining-model"></a>마이닝 모델의 학습에 사용된 사례를 반환하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]인스턴스를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 가리킨 다음 **DMX**를 클릭합니다.  
  
     비어 있는 새 쿼리가 포함된 쿼리 편집기가 열립니다.  
  
2.  SELECT의 일반적인 예를 복사 \<모델 >. 빈 쿼리에 사례 문입니다.  
  
3.  다음 내용을  
  
    ```  
    <select list>   
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    *  
    ```  
  
     *를 [Bike Buyer]와 같은 원본 데이터 내에 있는 임의의 열 목록으로 바꿀 수도 있습니다.  
  
4.  다음 내용을  
  
    ```  
    [<mining model>]   
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    [Decision Tree]  
    ```  
  
     이제 전체 문이 다음과 같아야 합니다.  
  
    ```  
    SELECT *   
    FROM [Decision Tree].CASES  
    ```  
  
5.  **파일** 메뉴에서 **다른 이름으로 DMXQuery1.dmx 저장**을 클릭합니다.  
  
6.  에 **다른 이름으로 저장** 대화 상자에서 적절 한 폴더로 이동 하 고 파일 이름을 `SELECT_DRILLTHROUGH.dmx`입니다.  
  
7.  도구 모음에서 **실행** 단추를 클릭합니다.  
  
     쿼리에서 의사 결정 트리 마이닝 모델의 학습에 사용된 원본 데이터가 반환됩니다.  
  
## <a name="return-the-states-of-a-discrete-mining-model-column"></a>불연속 마이닝 모델 열의 상태 반환  
 다음 단계는 SELECT DISTINCT 문을 사용하여 지정된 마이닝 모델 열에 가능한 다양한 상태를 반환하는 것입니다.  
  
 다음은 SELECT DISTINCT 문의 일반적인 예입니다.  
  
```  
SELECT DISTINCT [<column>]   
FROM [<mining model>]  
```  
  
 코드의 첫 번째 줄에서는 상태가 반환된 마이닝 모델 열을 정의합니다.  
  
```  
SELECT DISTINCT [<column>]   
```  
  
 열의 모든 상태를 반환하려면 DISTINCT를 포함해야 합니다. DISTINCT를 제외하면 전체 문이 예측의 바로 가기가 되며 지정된 열이 있을 가능성이 가장 높은 상태를 반환합니다. 자세한 내용은 [SELECT&#40;DMX&#41;](/sql/dmx/select-dmx)를 참조하세요.  
  
#### <a name="to-return-the-states-of-a-discrete-column"></a>불연속 열의 상태를 반환하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]인스턴스를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 가리킨 다음 **DMX**를 클릭합니다.  
  
     비어 있는 새 쿼리가 포함된 쿼리 편집기가 열립니다.  
  
2.  SELECT Distinct 문의 일반적인 예를 빈 쿼리에 복사합니다.  
  
3.  다음 내용을  
  
    ```  
    [<column,name>   
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    [Bike Buyer]  
    ```  
  
4.  다음 내용을  
  
    ```  
    [<mining model>]   
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    [Decision Tree]  
    ```  
  
     이제 전체 문이 다음과 같아야 합니다.  
  
    ```  
    SELECT DISTINCT [Bike Buyer]   
    FROM [Decision Tree]  
    ```  
  
5.  **파일** 메뉴에서 **다른 이름으로 DMXQuery1.dmx 저장**을 클릭합니다.  
  
6.  에 **다른 이름으로 저장** 대화 상자에서 적절 한 폴더로 이동 하 고 파일 이름을 `SELECT_DISCRETE.dmx`입니다.  
  
7.  도구 모음에서 **실행** 단추를 클릭합니다.  
  
     쿼리에서 Bike Buyer 열의 가능한 상태가 반환됩니다.  
  
 다음 단원에서는 의사 결정 트리 마이닝 모델을 사용하여 잠재 고객이 자전거 구매자가 될 것인지 여부를 예측합니다.  
  
## <a name="next-lesson"></a>다음 단원  
 [5단원: 예측 쿼리를 실행합니다.](../../2014/tutorials/lesson-5-executing-prediction-queries.md)  
  
  
