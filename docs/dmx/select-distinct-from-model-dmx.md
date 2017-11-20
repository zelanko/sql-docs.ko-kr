---
title: "SELECT DISTINCT FROM &lt;모델 &gt; (DMX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DISTINCT
- SELECT
dev_langs:
- DMX
helpviewer_keywords:
- discrete columns [DMX]
- discretized columns [DMX]
- SELECT DISTINCT FROM <model> statement
- continuous columns
ms.assetid: 0ab44ef6-1c3b-4809-a687-4d5d13f343af
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9aa916d15654b1fb4f806291d7d05ca7a683709f
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="select-distinct-from-ltmodel-gt-dmx"></a>SELECT DISTINCT FROM &lt;모델 &gt; (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  모델에서 선택한 열에 대해 가능한 모든 상태를 반환합니다. 반환되는 값은 지정된 열에 불연속 값, 불연속화된 숫자 값 또는 연속 숫자 값이 들어 있는지 여부에 따라 다릅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SELECT [FLATTENED] DISTINCT [TOP <n>] <expression list> FROM <model>   
[WHERE <condition list>][ORDER BY <expression>]  
```  
  
## <a name="arguments"></a>인수  
 *n*  
 (선택 사항) 반환할 행 수를 지정하는 정수입니다.  
  
 *식 목록*  
 관련 열 식별자(모델에서 파생됨) 또는 식의 쉼표로 구분된 목록입니다.  
  
 *모델*  
 모델 식별자입니다.  
  
 *조건 목록*  
 열 목록에서 반환되는 값을 제한하는 조건입니다.  
  
 *expression*  
 (선택 사항) 스칼라 값을 반환하는 식입니다.  
  
## <a name="remarks"></a>주의  
 **SELECT DISTINCT FROM** 문이 단일 열 또는 관련된 열 집합에만 작동 합니다. 이 절은 관련 없는 열 집합에는 적용되지 않습니다.  
  
 **SELECT DISTINCT FROM** 문을 사용 하면 중첩된 테이블 안의 열을 직접 참조할 수 있습니다. 예를 들어  
  
```  
<model>.<table column reference>.<column reference>  
```  
  
 결과 **SELECT DISTINCT FROM \<모델 >** 문에 열 유형에 따라 달라 집니다. 다음 표에서는 지원되는 열 유형 및 문의 출력 결과에 대해 설명합니다.  
  
|열 유형|출력|  
|-----------------|------------|  
|불연속|열의 고유 값|  
|불연속화됨|열에서 불연속화된 각 버킷의 중간점|  
|연속|열에서 값의 중간점|  
  
## <a name="discrete-column-example"></a>불연속 열의 예  
 다음 코드 예제에 따라는 `[TM Decision Tree]` 에서 만드는 모델은 [기본 데이터 마이닝 자습서](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)합니다. 이 쿼리는 불연속 열 `Gender`에 있는 고유 값을 반환합니다.  
  
```  
SELECT DISTINCT [Gender]  
FROM [TM Decision Tree]  
```  
  
 예제 결과:  
  
|Gender|  
|------------|  
||  
|F|  
|M|  
  
 열에 불연속 값이 들어 있으면 결과에 null 값으로 표시되는 누락된 상태가 항상 포함됩니다.  
  
## <a name="continuous-column-example"></a>연속 열의 예  
 다음 코드 샘플은 열에 있는 모든 값의 중간점, 최소 기간 및 최대 기간을 반환합니다.  
  
```  
SELECT DISTINCT [Age] AS [Midpoint Age],   
    RangeMin([Age]) AS [Minimum Age],   
    RangeMax([Age]) AS [Maximum Age]  
FROM [TM Decision Tree]  
```  
  
 예제 결과:  
  
|Midpoint Age|Minimum Age|Maximum Age|  
|------------------|-----------------|-----------------|  
||||  
|62|26|97|  
  
 또한 이 쿼리는 누락된 값을 나타내는 null 값의 행 하나를 반환합니다.  
  
## <a name="discretized-column-example"></a>불연속화된 열의 예  
 다음 코드 예제는 [`Yearly Income]` 열의 알고리즘으로 작성된 각 버킷의 중간점, 최대값 및 최소값을 반환합니다. 이 예의 결과를 재현하려면 `[Targeted Mailing]`과 동일한 새 마이닝 구조를 만들어야 합니다. 마법사에서 변경 내용 유형을 `Yearly Income` 열에서 **Continuous** 를 **Discretized**합니다.  
  
> [!NOTE]  
>  기본 마이닝 자습서에서 만든 마이닝 모델을 변경하여 마이닝 구조 열인 [`Yearly Income]`을 불연속화할 수도 있습니다. 이 작업을 수행 하는 방법에 대 한 정보를 참조 하십시오. [마이닝 모델에서 열의 분할 변경](../analysis-services/data-mining/change-the-discretization-of-a-column-in-a-mining-model.md)합니다. 그러나 열의 분할을 변경하면 마이닝 구조가 다시 처리되어 해당 구조를 사용하여 작성한 다른 모델의 결과가 변경됩니다.  
  
```  
SELECT DISTINCT [Yearly Income] AS [Bucket Average],   
    RangeMin([Yearly Income]) AS [Bucket Minimum],   
    RangeMax([Yearly Income]) AS [Bucket Maximum]  
FROM [TM Decision Tree]  
```  
  
 예제 결과:  
  
|Bucket Average|Bucket Minimum|Bucket Maximum|  
|--------------------|--------------------|--------------------|  
||||  
|24610.7|10000|39221.41|  
|55115.73|39221.41|71010.05|  
|84821.54|71010.05|98633.04|  
|111633.9|98633.04|124634.7|  
|147317.4|124634.7|170000|  
  
 [Yearly Income] 열의 값이 다섯 개의 버킷으로 불연속화되었고, 누락된 값을 나타내는 null 값의 열이 하나 추가되었습니다.  
  
 결과의 소수 자릿수는 쿼리에 사용하는 클라이언트에 따라 다릅니다. 여기에서는 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 표시되는 값을 반영하기 위해 편의상 소수점 이하 두 자리로 반올림되었습니다.  
  
 예를 들어 의사 결정 트리 뷰어를 사용하여 모델을 탐색하면서 수입별로 그룹화된 고객이 들어 있는 노드를 클릭하면 도구 설명에 다음과 같은 노드 속성이 표시됩니다.  
  
 Age >=69 AND Yearly Income < 39221.41  
  
> [!NOTE]  
>  최소 버킷의 최소값과 최대 버킷의 최대값은 단순히 관측 값 중 가장 높은 값과 가장 낮은 값입니다. 이러한 관측 범위에서 벗어나는 값은 최소 버킷과 최대 버킷에 속하는 것으로 간주됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SELECT&#40; DMX &#41;](../dmx/select-dmx.md)   
 [Data Mining Extensions &#40; DMX &#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [Data Mining Extensions &#40; DMX &#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

