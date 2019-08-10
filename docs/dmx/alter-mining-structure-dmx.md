---
title: ALTER 마이닝 구조 (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5535428d89a0d14b60e3ac79d281f63b4c69bfb5
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68889870"
---
# <a name="alter-mining-structure-dmx"></a>ALTER MINING STRUCTURE(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  기존 마이닝 구조를 기반으로 새 마이닝 모델을 만듭니다.  **ALTER 마이닝 structure** 문을 사용 하 여 새 마이닝 모델을 만드는 경우 구조가 이미 존재 해야 합니다. 반면, 문을 사용 하 여 [마이닝 &#40;모델 DMX&#41;를 만들](../dmx/create-mining-model-dmx.md)때는 모델을 만들고 자동으로 기본 마이닝 구조를 생성 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
ALTER MINING STRUCTURE <structure>  
ADD MINING MODEL <model>  
(  
    <column definition list>  
  [(<nested column definition list>) [WITH FILTER (<nested filter criteria>)]]  
)  
USING <algorithm> [(<parameter list>)]   
[WITH DRILLTHROUGH]  
[,FILTER(<filter criteria>)]  
```  
  
## <a name="arguments"></a>인수  
 *structure*  
 마이닝 모델을 추가할 마이닝 구조의 이름입니다.  
  
 *model*  
 고유한 마이닝 모델 이름입니다.  
  
 *열 정의 목록*  
 쉼표로 구분된 열 정의 목록입니다.  
  
 *중첩 열 정의 목록*  
 쉼표로 구분된 중첩 테이블 열 목록입니다(해당될 경우).  
  
 *중첩 필터 조건*  
 중첩 테이블의 열에 적용되는 필터 식입니다.  
  
 *algorithm*  
 공급자가 정의한 데이터 마이닝 알고리즘의 이름입니다.  
  
> [!NOTE]  
>  [DMSCHEMA_MINING_SERVICES 행 집합](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-services-rowset)을 사용 하 여 현재 공급자가 지 원하는 알고리즘 목록을 검색할 수 있습니다. 현재 인스턴스에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]지원 되는 알고리즘을 보려면 [데이터 마이닝 속성](https://docs.microsoft.com/analysis-services/server-properties/data-mining-properties)을 참조 하세요.  
  
 *매개 변수 목록*  
 (선택 사항) 알고리즘에 대해 공급자가 정의한 매개 변수의 쉼표로 구분된 목록입니다.  
  
 *필터 조건*  
 사례 테이블의 열에 적용되는 필터 식입니다.  
  
## <a name="remarks"></a>설명  
 마이닝 구조에 복합 키가 포함된 경우 이 구조에서 정의한 모든 키 열이 마이닝 모델에 포함되어야 합니다.  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] 클러스터링 및 [!INCLUDE[msCoName](../includes/msconame-md.md)] 시퀀스 클러스터링 알고리즘을 사용하여 작성한 모델과 같이 모델에 예측 가능한 열이 필요하지 않을 경우에는 문에 열 정의를 포함하지 않아도 됩니다. 결과 모델의 모든 특성은 입력으로 처리됩니다.  
  
 사례 테이블에 적용 되는 **WITH** 절에서 필터링 및 드릴스루에 대 한 옵션을 지정할 수 있습니다.  
  
-   **필터** 키워드 및 필터 조건을 추가 합니다. 그러면 필터가 마이닝 모델의 사례에 적용됩니다.  
  
-   **드릴스루** 키워드를 추가 하 여 마이닝 모델 사용자가 모델 결과에서 사례 데이터로 드릴 다운할 수 있도록 합니다. DMX(Data Mining Extensions)에서는 모델을 만들 때만 드릴스루를 사용할 수 있습니다.  
  
 사례 필터링과 드릴스루를 모두 사용 하려면 다음 예제에 나와 있는 구문을 사용 하 여 단일 **WITH** 절에서 키워드를 결합 합니다.  
  
 `WITH DRILLTHROUGH, FILTER(Gender = 'Male')`  
  
## <a name="column-definition-list"></a>열 정의 목록  
 각 열에 대해 다음과 같은 정보가 포함된 열 정의 목록을 지정하여 모델 구조를 정의합니다.  
  
-   이름(필수)  
  
-   별칭(옵션)  
  
-   모델링 플래그  
  
-   예측 요청-열에 예측 또는 **PREDICT_ONLY** 절로 표시 되는 예측 가능한 값이 포함 되는지 여부 를 알고리즘에 나타냅니다.  
  
 열 정의 목록에 대해 다음 구문을 사용하여 단일 열을 정의합니다.  
  
```  
<structure column name>  [AS <model column name>]  [<modeling flags>]    [<prediction>]  
```  
  
### <a name="column-name-and-alias"></a>열 이름 및 별칭  
 열 정의 목록에 사용하는 열 이름은 마이닝 구조에 사용된 열 이름이어야 합니다. 그러나 필요에 따라 마이닝 모델의 구조 열을 나타내는 별칭을 정의할 수 있습니다. 또한 같은 구조 열에 대한 열 정의를 여러 개 만든 다음 각각의 열 복사본에 서로 다른 별칭과 예측 사용을 할당할 수 있습니다. 기본적으로 구조 열 이름은 별칭을 정의하지 않은 경우에 사용됩니다. 자세한 내용은 [모델 열에 대 한 별칭 만들기](https://docs.microsoft.com/analysis-services/data-mining/create-an-alias-for-a-model-column)를 참조 하세요.  
  
 중첩 테이블 열에 대해 중첩 테이블의 이름을 지정 하 고, 데이터 형식을 **table**로 지정한 다음 모델에 포함할 중첩 열 목록을 괄호로 묶습니다.  
  
 필터 조건 식을 중첩 테이블 열 정의 뒤에 추가하여 중첩 테이블에 적용되는 필터 식을 정의할 수 있습니다.  
  
### <a name="modeling-flags"></a>모델링 플래그  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]는 마이닝 모델 열에 사용할 수 있도록 다음 모델링 플래그를 지원합니다.  
  
> [!NOTE]  
>  NOT_NULL 모델링 플래그는 마이닝 구조 열에 적용됩니다. 자세한 내용은 [CREATE MINING STRUCTURE&#40;DMX&#41;](../dmx/create-mining-structure-dmx.md)를 참조하세요.  
  
|||  
|-|-|  
|용어|정의|  
|**회귀 변수**|회귀 알고리즘의 회귀 수식에 지정된 열을 사용할 수 있음을 나타냅니다.|  
|**MODEL_EXISTENCE_ONLY**|특성의 존재 여부가 특성 열의 값보다 더 중요함을 나타냅니다.|  
  
 열 하나에 대해 여러 개의 모델링 플래그를 정의할 수 있습니다. 모델링 플래그를 사용 하는 방법에 대 한 자세한 내용은 [DMX &#40;flags&#41;DMX](../dmx/modeling-flags-dmx.md)를 참조 하세요.  
  
### <a name="prediction-clause"></a>예측 절  
 예측 절은 예측 열의 사용 방법을 설명합니다. 다음 표에서는 가능한 절을 보여 줍니다.  
  
|||  
|-|-|  
|**PREDICT**|모델에서 이 열을 예측할 수 있으며 열 값은 다른 예측 가능한 열의 값을 예측하기 위한 입력으로 사용할 수 있습니다.|  
|**PREDICT_ONLY**|이 열은 모델에 의해 예측될 수 있지만 이 열의 값을 입력 사례에 사용하여 다른 예측 가능 열 값을 예측할 수는 없습니다.|  
  
## <a name="filter-criteria-expressions"></a>필터 조건 식  
 마이닝 모델에 사용되는 사례를 제한하는 필터를 정의할 수 있습니다. 필터는 사례 테이블의 열 또는 중첩 테이블의 행에 적용하거나 둘 다에 적용할 수 있습니다.  
  
 필터 조건 식은 간단한 DMX 조건자로서 WHERE 절과 비슷합니다. 필터 식은 기본 수치 연산자, 스칼라 및 열 이름을 사용하는 수식으로 제한됩니다. 단, EXISTS 연산자는 예외입니다. 이 연산자는 하위 쿼리에 대해 반환되는 행이 한 개 이상일 경우 True로 평가됩니다. 공통 논리 연산자를 사용 하 여 조건자를 결합할 수 있습니다. AND, OR 및 NOT  
  
 마이닝 모델에 사용 되는 필터에 대 한 자세한 내용은 [마이닝 &#40;모델에 대 한 필터 Analysis Services&#41;-데이터 마이닝](https://docs.microsoft.com/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining)을 참조 하십시오.  
  
> [!NOTE]  
>  필터의 열은 마이닝 구조 열이어야 합니다. 모델 열이나 별칭이 지정된 열에 대한 필터는 만들 수 없습니다.  
  
 DMX 연산자 및 구문에 대 한 자세한 내용은 [마이닝 모델 열](https://docs.microsoft.com/analysis-services/data-mining/mining-model-columns)을 참조 하세요.  
  
## <a name="parameter-definition-list"></a>매개 변수 정의 목록  
 매개 변수 목록에 알고리즘 매개 변수를 추가하여 모델의 성능과 기능을 조정할 수 있습니다. 사용할 수 있는 매개 변수는 USING 절에 지정한 알고리즘에 따라 달라집니다. 각 알고리즘과 연결 된 매개 변수 목록은 [데이터 마이닝 알고리즘 &#40;&#41;Analysis Services 데이터 마이닝](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)을 참조 하세요.  
  
 매개 변수 목록의 구문은 다음과 같습니다.  
  
```  
[<parameter> = <value>, <parameter> = <value>,...]  
```  
  
## <a name="example-1-add-a-model-to-a-structure"></a>예제 1: 구조에 모델 추가  
 다음 예에서는 **새 메일링** 마이닝 구조에 Naive Bayes 마이닝 모델을 추가 하 고 최대 특성 상태 수를 50으로 제한 합니다.  
  
```  
ALTER MINING STRUCTURE [New Mailing]  
ADD MINING MODEL [Naive Bayes]  
(  
    CustomerKey,   
    Gender,  
    [Number Cars Owned],  
    [Bike Buyer] PREDICT  
)  
USING Microsoft_Naive_Bayes (MAXIMUM_STATES = 50)  
```  
  
## <a name="example-2-add-a-filtered-model-to-a-structure"></a>예제 2: 구조에 필터링 된 모델 추가  
 다음 예에서는 **새 메일링** 마이닝 구조에 `Naive Bayes Women`마이닝 모델을 추가 합니다. 새 모델의 기본 구조는 예 1에서 추가한 마이닝 모델과 같지만 이 모델에서는 마이닝 구조의 사례를 51세 이상의 여성 고객으로 제한합니다.  
  
```  
ALTER MINING STRUCTURE [New Mailing]  
ADD MINING MODEL [Naive Bayes Women]  
(  
    CustomerKey,   
    Gender,  
    [Number Cars Owned],  
    [Bike Buyer] PREDICT  
)  
USING Microsoft_Naive_Bayes  
WITH FILTER([Gender] = 'F' AND [Age] >50)  
```  
  
## <a name="example-3-add-a-filtered-model-to-a-structure-with-a-nested-table"></a>예제 3: 중첩 테이블을 사용 하 여 구조에 필터링 된 모델 추가  
 다음 예에서는 시장 바구니 마이닝 구조의 수정된 버전에 마이닝 모델을 추가합니다. 예제에 사용 된 마이닝 구조는 customer region에 대 한 특성을 포함 하는 **region** 열을 추가 하 고, **High**, 보통 값을 사용 하 여 고객 수입을 분류 하는 **소득 그룹** 열을 추가 하도록 수정 되었습니다.또는 **낮음**.  
  
 이 마이닝 구조에는 고객이 구매한 항목을 나열하는 중첩 테이블도 포함되어 있습니다.  
  
 마이닝 구조에 중첩 테이블이 포함되어 있으므로 사례 테이블, 중첩 테이블 또는 두 테이블 모두에 대한 필터를 정의할 수 있습니다. 이 예에서는 Road Tire 모델 중 하나를 구매한 부유한 유럽 고객으로 사례를 제한하기 위해 사례 필터와 중첩 행 필터를 결합합니다.  
  
```  
ALTER MINING STRUCTURE [Market Basket with Region and Income]  
ADD MINING MODEL [Decision Trees]  
(  
    CustomerKey,   
    Region,  
    [Income Group],  
    [Product] PREDICT (Model)   
WITH FILTER (EXISTS (SELECT * FROM [v Assoc Seq Line Items] WHERE   
 [Model] = 'HL Road Tire' OR  
 [Model] = 'LL Road Tire' OR  
 [Model] = 'ML Road Tire' )  
)  
) WITH FILTER ([Income Group] = 'High' AND [Region] = 'Europe')  
USING Microsoft_Decision Trees  
```  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 확장 &#40;DMX&#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [DMX&#40;Data Mining Extensions&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
