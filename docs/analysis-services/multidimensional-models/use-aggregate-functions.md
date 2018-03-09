---
title: "집계 함수를 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: aggregate functions [Analysis Services]
ms.assetid: c42166ef-b75c-45f4-859c-09a3e9617664
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: b22f964bbc9659187cf67320951b75d93cb89331
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="use-aggregate-functions"></a>집계 함수 사용
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]차원을 사용 하 여 측정값을 분할 하, 하는 경우 측정값은 해당 차원에 포함 된 계층에서 요약 됩니다. 이러한 요약 동작은 측정값에 대해 지정된 집계 함수에 따라 달라집니다. 숫자 데이터가 포함된 대부분 측정값의 경우 집계 함수는 **Sum**입니다. 측정값은 활성 상태인 계층의 수준에 따라 다른 금액으로 합계됩니다.  
  
 Analysis Services에서 만드는 모든 측정값은 측정값의 연산을 결정하는 집계 함수에 의해 지원됩니다. 미리 정의된 집계 유형으로는 **합계**, **최소값**, **최대값**, **개수**, **고유 카운트**및 몇 가지 기타 추가 특수 함수가 있습니다. 또는 복잡한 수식이나 사용자 지정 수식을 기반으로 한 집계가 필요한 경우 미리 작성된 집계 함수를 사용하는 대신 MDX 계산을 작성할 수 있습니다. 예를 들어 백분율 값에 대한 측정값을 정의하려는 경우 MDX에서 계산된 측정값을 사용하여 정의할 수 있습니다. [CREATE MEMBER 문&#40;MDX&#41;](../../mdx/mdx-data-definition-create-member.md)을 참조하세요.  
  
 큐브 마법사를 통해 만들어진 측정값은 측정값 정의의 일부로 집계 유형이 할당됩니다. 원본 열에 숫자 데이터가 포함되었다고 가정하면 집계 유형은 항상 **Sum**입니다. **Sum** 은 원본 열의 데이터 형식과 관계없이 할당됩니다. 예를 들어 큐브 마법사를 사용하여 측정값을 만든 경우 팩트 테이블의 모든 열을 가져오면 원본이 날짜 시간 열이더라도 모든 결과 측정값의 집계가 **Sum**임을 알 수 있습니다. 마법사를 통해 만든 측정값의 미리 할당된 집계 방법을 항상 검토하여 집계 함수가 적합한지 확인하세요.  
  
 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]또는 MDX를 통해 큐브 정의에서 집계 방법을 할당하거나 변경할 수 있습니다. 자세한 내용은 [다차원 모델의 측정값 및 측정값 그룹 만들기](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md) 또는 [집계&#40;MDX&#41;](../../mdx/aggregate-mdx.md)를 참조하세요.  
  
##  <a name="AggFunction"></a> 집계 함수  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 측정값 그룹에 포함된 차원에 따라 측정값을 집계하는 함수를 제공합니다. 집계 함수의 *가산성* 은 큐브에 있는 모든 차원에서 측정값이 집계되는 방식을 결정합니다. 집계 함수의 가산성 수준은 다음과 같이 세 가지로 구분됩니다.  
  
 가산적  
 완전 가산적 측정값이라고도 하는 가산적 측정값은 아무런 제한 없이 측정값이 포함된 측정값 그룹 내의 모든 차원에 따라 집계할 수 있습니다.  
  
 반가산적  
 반가산적 측정값은 측정값이 포함된 측정값 그룹 내의 모든 차원이 아니라 차원 중 일부에 대해서만 집계할 수 있습니다. 예를 들어 재고로 보유할 수 있는 수량을 나타내는 측정값을 지리 차원에 따라 집계하여 모든 창고의 가용 총 수량을 산출할 수 있습니다. 그러나 이 측정값은 가용 수량에 대한 정기적인 스냅숏을 의미하기 때문에 이 측정값을 시간 차원에 따라 집계할 수는 없습니다. 이러한 측정값을 시간 차원에 따라 집계하면 잘못된 결과가 산출됩니다. 자세한 내용은 [Define Semiadditive Behavior](../../analysis-services/multidimensional-models/define-semiadditive-behavior.md) 를 참조하세요.  
  
 비가산적  
 비가산적 측정값은 측정값이 포함된 측정값 그룹 내의 차원에 대해서는 집계할 수 없습니다. 대신에 측정값을 나타내는 큐브의 각 셀에 대해 개별적으로 측정값을 계산해야 합니다. 예를 들어 수익률과 같은 백분율을 반환하는 계산된 측정값은 임의의 차원에 있는 자식 멤버의 백분율 값으로부터 집계할 수 없습니다.  
  
 다음 표에서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 집계 함수를 나열하고 함수의 가산성과 예상 출력에 대해 설명합니다.  
  
|집계 함수|가산성|반환 값|  
|--------------------------|----------------|--------------------|  
|**Sum**|가산적|모든 자식 멤버의 값 합계를 계산합니다. 이것은 기본 집계 함수입니다.|  
|**개수**|가산적|모든 자식 멤버 수를 검색합니다.|  
|**최소값**|반가산적|모든 자식 멤버의 최소값을 검색합니다.|  
|**최대값**|반가산적|모든 자식 멤버의 최대값을 검색합니다.|  
|**DistinctCount**|비가산적|모든 고유 자식 멤버의 수를 검색합니다. 자세한 내용은 다음 섹션의 [About Distinct Count Measures](../../analysis-services/multidimensional-models/use-aggregate-functions.md#bkmk_distinct) 를 참조하세요.|  
|**없음**|비가산적|집계가 수행되지 않습니다. 차원에 있는 리프 멤버 및 리프가 아닌 멤버의 모든 값은 측정값이 포함된 측정값 그룹의 팩트 테이블에서 직접 제공됩니다. 멤버의 팩트 테이블에서 값을 읽을 수 없는 경우 해당 멤버의 값은 Null로 설정됩니다.|  
|**ByAccount**|반가산적|계정 차원에 있는 멤버의 계정 유형에 할당된 집계 함수에 따라 집계를 계산합니다. 측정값 그룹에 계정 유형 차원이 없는 경우에는 **None** 집계 함수로 처리합니다.<br /><br /> 계정 차원에 대한 자세한 내용은 [부모-자식 유형 차원의 재무 계정 만들기](../../analysis-services/multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md)를 참조하세요.|  
|**AverageOfChildren**|반가산적|비어 있지 않은 모든 자식 멤버 값의 평균을 계산합니다.|  
|**FirstChild**|반가산적|첫 번째 자식 멤버의 값을 검색합니다.|  
|**LastChild**|반가산적|마지막 자식 멤버의 값을 검색합니다.|  
|**FirstNonEmpty**|반가산적|비어 있지 않은 첫 번째 자식 멤버의 값을 검색합니다.|  
|**LastNonEmpty**|반가산적|비어 있지 않은 마지막 자식 멤버의 값을 검색합니다.|  
  
##  <a name="bkmk_distinct"></a> About Distinct Count Measures  
 **집계 함수** 속성 값이 **Distinct Count** 인 측정값을 고유 카운트 측정값이라고 합니다. 고유 카운트 측정값은 팩트 테이블에서 차원의 최하위 수준 멤버의 발생 수를 계산하는 데 사용할 수 있습니다. 고유 카운트이므로 한 멤버가 여러 번 발생할 경우 한 번만 계산됩니다. 고유 카운트 측정값은 항상 전용 측정값 그룹에 배치됩니다. 고유 카운트 측정값을 자체 측정값 그룹에 배치하는 것은 디자이너에 성능 최적화 기술로 빌드된 모범 사례입니다.  
  
 고유 카운트 측정값은 일반적으로 각 차원의 멤버에 대해 다른 차원의 최하위 수준 멤버가 팩트 테이블의 행을 공유하는 방법을 지정하는 데 사용됩니다. 예를 들어 Sales 큐브에서는 각 고객과 고객 그룹에 대해 몇 개의 고유 제품이 구매되었습니까? 즉, 고객 차원의 각 멤버에 대해 제품 차원에서 몇 개의 최하위 수준 고유 멤버가 팩트 테이블의 행을 공유합니까? 또는 예를 들어 인터넷 사이트 방문 큐브에서 각 사이트 방문자와 사이트 방문자 그룹에 대해 인터넷 사이트에서 몇 개의 고유 페이지가 방문되었습니까? 즉, 사이트 방문자 차원의 각 멤버에 대해 페이지 차원에서 몇 개의 최하위 수준 고유 멤버가 팩트 테이블의 행을 공유합니까? 이러한 각 예에서 두 번째 차원의 최하위 수준 멤버는 고유 카운트 측정값으로 계산됩니다.  
  
 이 종류의 분석을 두 가지 차원으로 제한할 필요는 없습니다. 실제로 계산된 멤버가 포함된 차원을 포함하여 큐브의 모든 차원 조합으로 고유 카운트 측정값을 구분하고 조각화할 수 있습니다.  
  
 멤버를 계산하는 고유 카운트 측정값은 팩트 테이블의 외래 키 열을 기반으로 합니다. 즉, 측정값의 **Source Column** 속성은 이 열을 식별합니다. 이 열은 고유 카운트 측정값으로 계산되는 멤버를 식별하는 차원 테이블 열을 조인합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [측정값 및 측정값 그룹](../../analysis-services/multidimensional-models/measures-and-measure-groups.md)   
 [MDX 함수 참조 &#40; Mdx&#41;](../../mdx/mdx-function-reference-mdx.md)   
 [반가산적 동작 정의](../../analysis-services/multidimensional-models/define-semiadditive-behavior.md)  
  
  
