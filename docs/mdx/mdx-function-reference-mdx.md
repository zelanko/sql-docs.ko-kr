---
title: "MDX 함수 참조 (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords:
- member functions [MDX]
- level functions [MDX]
- MDX [Analysis Services], functions
- array functions
- string functions
- Multidimensional Expressions [Analysis Services], functions
- hierarchy functions [MDX]
- numeric functions [MDX]
- tuple functions
- subcube functions [MDX]
- functions [MDX]
- logical functions [MDX]
- set functions [MDX]
ms.assetid: e363722a-3e5b-40a9-a0b5-399dd2d93f6d
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: d6a0eecf1084cc17b1a2a08b7ef1c43c81d2e346
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-function-reference-mdx"></a>MDX 함수 참조(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 함수에 MDX (Multidimensional Expressions) 구문 사용할 수 있도록 제공 합니다. 유효한 모든 MDX 문에서 함수를 사용할 수 있으며, 쿼리, 사용자 지정 롤업 정의 및 기타 계산에서도 함수가 자주 사용됩니다. 이 섹션에서는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에 포함된 MDX 함수에 대해 설명합니다.  
  
 다음 표를 사용하여 반환 값의 범주별로 함수를 찾을 수도 있고, 목차의 알파벳순 목록에서 이름으로 함수를 선택할 수도 있습니다.  
  
## <a name="array-functions"></a>배열 함수  
  
|함수|Description|  
|--------------|-----------------|  
|[SetToArray &#40; Mdx&#41;](../mdx/settoarray-mdx.md)|사용자 정의 함수에서 사용하기 위해 하나 이상의 집합을 배열로 변환합니다.|  
  
## <a name="hierarchy-functions"></a>계층 함수  
  
|함수|Description|  
|--------------|-----------------|  
|[계층 구조 &#40; Mdx&#41;](../mdx/hierarchy-mdx.md)|지정한 멤버 또는 수준을 포함하고 있는 계층을 반환합니다.|  
|[차원 &#40; Mdx&#41;](../mdx/dimension-mdx.md)|지정한 멤버, 수준, 계층을 포함하고 있는 차원을 반환합니다.|  
|[차원 &#40; Mdx&#41;](../mdx/dimensions-mdx.md)|숫자 식 또는 문자열 식으로 지정된 계층을 반환합니다.|  
  
## <a name="level-functions"></a>수준 함수  
  
|함수|Description|  
|--------------|-----------------|  
|[수준 &#40; Mdx&#41;](../mdx/level-mdx.md)|멤버의 수준을 반환합니다.|  
|[수준 &#40; Mdx&#41;](../mdx/levels-mdx.md)|차원 또는 계층에서의 위치가 숫자 식에 의해 지정되거나 이름이 문자열 식에 의해 지정되는 수준을 반환합니다.|  
  
## <a name="logical-functions"></a>논리 함수  
  
|함수|Description|  
|--------------|-----------------|  
|[IsAncestor &#40; Mdx&#41;](../mdx/isancestor-mdx.md)|지정한 멤버가 지정한 다른 멤버의 상위 항목인지 여부를 반환합니다.|  
|[IsEmpty &#40; Mdx&#41;](../mdx/isempty-mdx.md)|평가 식이 빈 셀 값인지 여부를 반환합니다.|  
|[IsGeneration &#40; Mdx&#41;](../mdx/isgeneration-mdx.md)|지정한 멤버가 지정한 세대에 속하는지 여부를 반환합니다.|  
|[IsLeaf &#40; Mdx&#41;](../mdx/isleaf-mdx.md)|지정한 멤버가 리프 멤버인지 여부를 반환합니다.|  
|[IsSibling &#40; Mdx&#41;](../mdx/issibling-mdx.md)|지정한 멤버가 지정한 다른 멤버의 형제 항목인지 여부를 반환합니다.|  
  
## <a name="member-functions"></a>멤버 함수  
  
|함수|Description|  
|--------------|-----------------|  
|[상위 항목 &#40; Mdx&#41;](../mdx/ancestor-mdx.md)|지정한 수준 또는 거리에서 멤버의 상위 항목을 반환합니다.|  
|[ClosingPeriod &#40; Mdx&#41;](../mdx/closingperiod-mdx.md)|지정한 수준에서 멤버의 하위 항목 중 마지막 형제 항목을 반환합니다.|  
|[Cousin &#40; Mdx&#41;](../mdx/cousin-mdx.md)|부모 멤버 아래에서 지정한 자식 멤버와 상대적으로 동일한 위치의 자식 멤버를 반환합니다.|  
|[CurrentMember &#40; Mdx&#41;](../mdx/currentmember-mdx.md)|반복하는 동안 지정한 차원이나 계층에 따라 현재 멤버를 반환합니다.|  
|[DataMember &#40; Mdx&#41;](../mdx/datamember-mdx.md)|차원의 리프가 아닌 멤버에 관련된 시스템 생성 데이터 멤버를 반환합니다.|  
|[DefaultMember &#40; Mdx&#41;](../mdx/defaultmember-mdx.md)|차원 또는 계층의 기본 멤버를 반환합니다.|  
|[FirstChild &#40; Mdx&#41;](../mdx/firstchild-mdx.md)|멤버의 첫째 자식 항목을 반환합니다.|  
|[FirstSibling &#40; Mdx&#41;](../mdx/firstsibling-mdx.md)|멤버 부모 항목의 첫째 자식 항목을 반환합니다.|  
|[항목 &#40; 멤버 &#41; &#40; Mdx&#41;](../mdx/item-member-mdx.md)|지정한 튜플에서 멤버를 반환합니다.|  
|[Lag &#40; Mdx&#41;](../mdx/lag-mdx.md)|멤버의 차원에 따라 지정한 멤버 이전의 위치 번호로 지정된 멤버를 반환합니다.|  
|[LastChild &#40; Mdx&#41;](../mdx/lastchild-mdx.md)|지정한 멤버의 마지막 자식 항목을 반환합니다.|  
|[LastSibling &#40; Mdx&#41;](../mdx/lastsibling-mdx.md)|지정한 멤버 부모 항목의 마지막 자식 항목을 반환합니다.|  
|[잠재 고객 &#40; Mdx&#41;](../mdx/lead-mdx.md)|멤버의 차원에 따라 지정한 멤버 다음의 위치 번호로 지정된 멤버를 반환합니다.|  
|[LinkMember &#40; Mdx&#41;](../mdx/linkmember-mdx.md)|지정한 계층에서 지정한 멤버와 동일한 멤버를 반환합니다.|  
|[멤버 &#40; 문자열 &#41; &#40; Mdx&#41;](../mdx/members-string-mdx.md)|문자열 식으로 지정된 멤버를 반환합니다.|  
|[NextMember &#40; Mdx&#41;](../mdx/nextmember-mdx.md)|지정한 멤버를 포함하고 있는 수준에서 다음 멤버를 반환합니다.|  
|[OpeningPeriod &#40; Mdx&#41;](../mdx/openingperiod-mdx.md)|지정한 수준 또는 지정한 멤버의 하위 항목 중 첫 번째 형제를 반환합니다.|  
|[ParallelPeriod &#40; Mdx&#41;](../mdx/parallelperiod-mdx.md)|지정한 멤버와 상대적 위치가 같은 멤버를 이전 기간에서 반환합니다.|  
|[부모 &#40; Mdx&#41;](../mdx/parent-mdx.md)|멤버의 부모 항목을 반환합니다.|  
|[PrevMember &#40; Mdx&#41;](../mdx/prevmember-mdx.md)|지정한 멤버를 포함하고 있는 수준에서 이전 멤버를 반환합니다.|  
|[StrToMember &#40; Mdx&#41;](../mdx/strtomember-mdx.md)|MDX 형식 문자열에 의해 지정된 멤버를 반환합니다.|  
|[UnknownMember &#40; Mdx&#41;](../mdx/unknownmember-mdx.md)|수준 또는 멤버와 연결된 알 수 없는 멤버를 반환합니다.|  
|[ValidMeasure &#40; Mdx&#41;](../mdx/validmeasure-mdx.md)|적용할 수 없는 차원을 최상위 수준에 강제로 적용하여 가상 큐브에서 유효한 측정값을 반환합니다.|  
  
## <a name="numeric-functions"></a>숫자 함수  
  
|함수|Description|  
|--------------|-----------------|  
|[집계 &#40; Mdx&#41;](../mdx/aggregate-mdx.md)|측정값 또는 지정한 집합의 튜플에 대해 선택적으로 지정한 숫자 식을 집계하여 계산한 스칼라 값을 반환합니다.|  
|[Avg &#40; Mdx&#41;](../mdx/avg-mdx.md)|지정한 집합에 대해 계산된 측정값의 평균값 또는 숫자 식(옵션)의 평균값을 반환합니다.|  
|[CalculationCurrentPass&#40;MDX&#41;](../mdx/calculationcurrentpass-mdx.md)|지정한 쿼리 컨텍스트에 대한 큐브의 현재 계산 패스를 반환합니다.|  
|[CalculationPassValue&#40;MDX&#41;](../mdx/calculationpassvalue-mdx.md)|지정한 큐브의 계산 패스에 대해 계산된 MDX 식의 값을 반환합니다.|  
|[CoalesceEmpty &#40; Mdx&#41;](../mdx/coalesceempty-mdx.md)|빈 셀 값을 숫자 또는 문자열에 결합하고 결합된 값을 반환합니다.|  
|[상관 관계 &#40; Mdx&#41;](../mdx/correlation-mdx.md)|집합에 대해 계산된 두 변량의 상관 계수를 반환합니다.|  
|[Count &#40; 차원 &#41; &#40; Mdx&#41;](../mdx/count-dimension-mdx.md)|큐브의 차원 수를 반환합니다.|  
|[Count &#40; 계층 수준 &#41; &#40; Mdx&#41;](../mdx/count-hierarchy-levels-mdx.md)|차원 또는 계층의 수준 수를 반환합니다.|  
|[Count &#40; 설정 &#41; &#40; Mdx&#41;](../mdx/count-set-mdx.md)|집합의 셀 개수를 반환합니다.|  
|[Count &#40; 튜플 &#41; &#40; Mdx&#41;](../mdx/count-tuple-mdx.md)|튜플의 차원 수를 반환합니다.|  
|[공변성 (covariance) &#40; Mdx&#41;](../mdx/covariance-mdx.md)|편향 모집단 수식을 사용하여 집합에 대해 계산된 두 변량의 모집단 공변성(covariance)을 반환합니다.|  
|[CovarianceN &#40; Mdx&#41;](../mdx/covariancen-mdx.md)|비편향 모집단 수식을 사용하여 집합에 대해 계산된 두 변량의 예제 공변성(covariance)을 반환합니다.|  
|[DistinctCount &#40; Mdx&#41;](../mdx/distinctcount-mdx.md)|집합에서 공백이 아닌 고유한 튜플 수를 반환합니다.|  
|[IIf &#40; Mdx&#41;](../mdx/iif-mdx.md)|논리 테스트로 확인된 두 값 중 하나를 반환합니다.|  
|[LinRegIntercept &#40; Mdx&#41;](../mdx/linregintercept-mdx.md)|집합의 선형 회귀를 계산 하 고 회귀선의 절편의 값을 반환 y = ax + b 합니다.|  
|[LinRegPoint &#40; Mdx&#41;](../mdx/linregpoint-mdx.md)|값을 반환 하 고 집합의 선형 회귀를 계산 *y* 고 회귀선 y = ax + b 합니다.|  
|[LinRegR2 &#40; Mdx&#41;](../mdx/linregr2-mdx.md)|집합의 선형 회귀를 계산하고 결정 계수 R2를 반환합니다.|  
|[LinRegSlope &#40; Mdx&#41;](../mdx/linregslope-mdx.md)|집합의 선형 회귀를 계산 하 고 회귀선의 기울기 값을 반환 y = ax + b 합니다.|  
|[LinRegVariance &#40; Mdx&#41;](../mdx/linregvariance-mdx.md)|집합의 선형 회귀를 계산 하 고 회귀선와 연관 된 분산을 반환 y = ax + b 합니다.|  
|[LookupCube &#40; Mdx&#41;](../mdx/lookupcube-mdx.md)|같은 데이터베이스에서 지정된 또 다른 큐브에 대해 계산된 MDX 식의 값을 반환합니다.|  
|[최대 &#40; Mdx&#41;](../mdx/max-mdx.md)|집합에 대해 계산된 숫자 식의 최대값을 반환합니다.|  
|[중앙값 &#40; Mdx&#41;](../mdx/median-mdx.md)|집합에 대해 계산된 숫자 식의 중앙값을 반환합니다.|  
|[Min &#40; Mdx&#41;](../mdx/min-mdx.md)|집합에 대해 계산된 숫자 식의 최소값을 반환합니다.|  
|[서 수 &#40; Mdx&#41;](../mdx/ordinal-mdx.md)|수준과 관련된 서수 값(0부터 시작)을 반환합니다.|  
|[예측 &#40; Mdx&#41;](../mdx/predict-mdx.md)|데이터 마이닝 모델에 대해 계산되는 숫자 식의 값을 반환합니다.|  
|[순위 &#40; Mdx&#41;](../mdx/rank-mdx.md)|지정한 집합에 있는 지정한 튜플의 순위(1부터 시작)를 반환합니다.|  
|[RollupChildren &#40; Mdx&#41;](../mdx/rollupchildren-mdx.md)|지정한 단항 연산자를 통해 지정한 멤버의 자식 항목 값을 롤업하여 생성된 값을 반환합니다.|  
|[Stddev &#40; Mdx&#41;](../mdx/stddev-mdx.md)|에 대 한 별칭 [Stdev &#40; Mdx&#41; ](../mdx/stdev-mdx.md).|  
|[StddevP &#40; Mdx&#41;](../mdx/stddevp-mdx.md)|에 대 한 별칭 [StdevP &#40; Mdx&#41; ](../mdx/stdevp-mdx.md).|  
|[Stdev &#40; Mdx&#41;](../mdx/stdev-mdx.md)|비편향 모집단 수식을 사용하여 집합에 대해 계산되는 숫자 식의 예제 표준 편차를 반환합니다.|  
|[StdevP &#40; Mdx&#41;](../mdx/stdevp-mdx.md)|편향 모집단 수식을 사용하여 집합에 대해 계산되는 숫자 식의 모집단 표준 편차를 반환합니다.|  
|[StrToValue &#40; Mdx&#41;](../mdx/strtovalue-mdx.md)|MDX 형식 문자열에 의해 지정된 값을 반환합니다.|  
|[Sum &#40; Mdx&#41;](../mdx/sum-mdx.md)|집합에 계산된 숫자 식의 합을 반환합니다.|  
|[값 &#40; Mdx&#41;](../mdx/value-mdx.md)|측정값을 반환합니다.|  
|[Var &#40; Mdx&#41;](../mdx/var-mdx.md)|비편향 모집단 수식을 사용하여 집합에 대해 계산되는 숫자 식의 예제 분산을 반환합니다.|  
|[분산 &#40; Mdx&#41;](../mdx/variance-mdx.md)|에 대 한 별칭 [Var &#40; Mdx&#41; ](../mdx/var-mdx.md).|  
|[VarianceP &#40; Mdx&#41;](../mdx/variancep-mdx.md)|에 대 한 별칭 [VarP &#40; Mdx&#41; ](../mdx/varp-mdx.md).|  
|[VarP &#40; Mdx&#41;](../mdx/varp-mdx.md)|편향 모집단 수식을 사용하여 집합에 대해 계산되는 숫자 식의 모집단 분산을 반환합니다.|  
  
## <a name="set-functions"></a>집합 함수  
  
|함수|Description|  
|--------------|-----------------|  
|[AddCalculatedMembers &#40; Mdx&#41;](../mdx/addcalculatedmembers-mdx.md)|계산 멤버를 지정한 집합에 추가하여 생성된 집합을 반환합니다.|  
|[AllMembers &#40; Mdx&#41;](../mdx/allmembers-mdx.md)|계산 멤버를 비롯하여 지정한 차원, 계층 또는 수준의 모든 멤버가 포함된 집합을 반환합니다.|  
|[상위 요소 &#40; Mdx&#41;](../mdx/ancestors-mdx.md)|지정한 수준 또는 거리에서 멤버의 모든 상위 항목 집합을 반환합니다.|  
|[상위 항목 &#40; Mdx&#41;](../mdx/ascendants-mdx.md)|멤버 자체를 포함하여 지정한 멤버의 상위 항목 집합을 반환합니다.|  
|[축 &#40; Mdx&#41;](../mdx/axis-mdx.md)|축에서 정의된 집합을 반환합니다.|  
|[BottomCount &#40; Mdx&#41;](../mdx/bottomcount-mdx.md)|집합을 오름차순으로 정렬하고 가장 낮은 값을 갖는 튜플을 지정된 수만큼 반환합니다.|  
|[BottomPercent &#40; Mdx&#41;](../mdx/bottompercent-mdx.md)|집합을 오름차순으로 정렬하고 누적 합계가 지정한 백분율 이하인 하위 값 튜플 집합을 반환합니다.|  
|[BottomSum &#40; Mdx&#41;](../mdx/bottomsum-mdx.md)|집합을 오름차순으로 정렬하고 누적 합계가 지정한 백분율 이하인 하위 값 튜플 집합을 반환합니다.|  
|[자식 &#40; Mdx&#41;](../mdx/children-mdx.md)|지정한 멤버의 자식을 반환합니다.|  
|[크로스 조인 &#40; Mdx&#41;](../mdx/crossjoin-mdx.md)|하나 이상의 집합에 대한 교차곱을 반환합니다.|  
|[CurrentOrdinal &#40; Mdx&#41;](../mdx/currentordinal-mdx.md)|반복하는 동안 집합 내의 현재 반복 번호를 반환합니다.|  
|[하위 항목 &#40; Mdx&#41;](../mdx/descendants-mdx.md)|지정한 수준 또는 거리에서 멤버의 하위 항목 집합을 반환합니다. 다른 수준의 하위 항목은 포함하거나 제외할 수 있습니다.|  
|[고유한 &#40; Mdx&#41;](../mdx/distinct-mdx.md)|지정한 집합에서 중복 튜플을 제거하고 집합을 반환합니다.|  
|[DrilldownLevel &#40; Mdx&#41;](../mdx/drilldownlevel-mdx.md)|집합의 멤버를 집합에서 가장 낮게 표시되는 수준보다 한 수준 아래로 또는 집합에서 표시되는 멤버의 지정된 수준보다 한 수준 아래로 드릴다운합니다.|  
|[DrilldownLevelBottom &#40; Mdx&#41;](../mdx/drilldownlevelbottom-mdx.md)|집합의 가장 아래쪽 구성원을 지정한 수준에서 한 수준 아래로 드릴다운합니다.|  
|[DrilldownLevelTop &#40; Mdx&#41;](../mdx/drilldownleveltop-mdx.md)|집합의 최상위 구성원을 지정한 수준에서 한 수준 아래로 드릴다운합니다.|  
|[DrilldownMember &#40; Mdx&#41;](../mdx/drilldownmember-mdx.md)|지정된 집합의 멤버 중 두 번째 지정한 집합에 나타나는 멤버를 드릴다운합니다. 또는 튜플 집합을 드릴다운합니다.|  
|[DrilldownMemberBottom &#40; Mdx&#41;](../mdx/drilldownmemberbottom-mdx.md)|지정한 집합의 멤버 중 두 번째 지정한 집합에 있는 멤버를 드릴다운합니다. 결과 집합은 지정된 멤버 수로 제한됩니다. 또는 튜플 집합을 드릴다운합니다.|  
|[DrilldownMemberTop &#40; Mdx&#41;](../mdx/drilldownmembertop-mdx.md)|지정한 집합의 멤버 중 두 번째 지정한 집합에 있는 멤버를 드릴다운합니다. 결과 집합은 지정된 멤버 수로 제한됩니다. 또는 튜플 집합을 드릴다운합니다.|  
|[DrillupLevel &#40; Mdx&#41;](../mdx/drilluplevel-mdx.md)|지정한 수준 아래에 있는 집합의 멤버를 드릴업합니다.|  
|[DrillupMember &#40; Mdx&#41;](../mdx/drillupmember-mdx.md)|지정한 집합에 있는 멤버 중 두 번째 지정한 집합에 나타나는 멤버를 드릴업합니다.|  
|[제외 하 고 &#40; Mdx&#41;](../mdx/except-mdx-function.md)|두 집합의 차집합을 찾습니다. 중복 요소를 포함시킬 수도 있습니다.|  
|[존재 &#40; Mdx&#41;](../mdx/exists-mdx.md)|하나 이상의 다른 집합의 여러 튜플에 존재하는 한 집합의 멤버 집합을 반환합니다.|  
|[추출 &#40; Mdx&#41;](../mdx/extract-mdx.md)|추출된 차원 요소에서 튜플 집합을 반환합니다.|  
|[필터 &#40; Mdx&#41;](../mdx/filter-mdx.md)|검색 조건을 기준으로 지정한 집합을 필터링한 결과 집합을 반환합니다.|  
|[생성 &#40; Mdx&#41;](../mdx/generate-mdx.md)|한 집합을 다른 집합의 각 멤버에 적용하고 결과 집합을 합집합으로 결합시킵니다. 또는 집합에 대해 문자열 식을 계산하여 생성된 연결 문자열을 반환합니다.|  
|[H e a d &#40; Mdx&#41;](../mdx/head-mdx.md)|집합에서 중복된 항목을 포함하여 처음 나오는 지정한 수만큼의 요소를 반환합니다.|  
|[Hierarchize &#40; Mdx&#41;](../mdx/hierarchize-mdx.md)|집합의 멤버를 계층 구조 형태로 정렬합니다.|  
|[교차 &#40; Mdx&#41;](../mdx/intersect-mdx.md)|두 입력 집합의 교집합을 반환합니다. 중복 요소를 포함시킬 수도 있습니다.|  
|[LastPeriods &#40; Mdx&#41;](../mdx/lastperiods-mdx.md)|지정한 멤버까지 포함하는 멤버 집합을 반환합니다.|  
|[멤버 &#40; 설정 &#41; &#40; Mdx&#41;](../mdx/members-set-mdx.md)|차원, 수준 또는 계층의 멤버 집합을 반환합니다.|  
|[Mtd &#40; Mdx&#41;](../mdx/mtd-mdx.md)|지정한 멤버와 동일한 수준의 형제 멤버 집합을 반환합니다. 이 집합은 첫 번째 형제 멤버부터 시작하여 지정된 멤버에서 끝나며 Time 차원의 Year 수준에 따라 제한됩니다.|  
|[NameToSet &#40; Mdx&#41;](../mdx/nametoset-mdx.md)|MDX 형식 문자열에 의해 지정된 멤버가 포함된 집합을 반환합니다.|  
|[NonEmptyCrossjoin &#40; Mdx&#41;](../mdx/nonemptycrossjoin-mdx.md)|하나 이상의 집합에 대한 교차곱을 한 개의 집합으로 반환합니다. 빈 튜플과 관련 팩트 테이블 데이터가 없는 튜플은 제외됩니다.|  
|[순서 &#40; Mdx&#41;](../mdx/order-mdx.md)|지정한 집합의 멤버를 정렬합니다. 계층을 유지하거나 바꿀 수도 있습니다.|  
|[PeriodsToDate &#40; Mdx&#41;](../mdx/periodstodate-mdx.md)|지정한 멤버와 동일한 수준의 형제 멤버 집합을 반환합니다. 이 집합은 첫 번째 형제 멤버부터 시작하여 지정된 멤버에서 끝나며 Time 차원의 지정된 수준에 따라 제한됩니다.|  
|[Qtd &#40; Mdx&#41;](../mdx/qtd-mdx.md)|첫 번째 형제 항목부터 지정 된 멤버에서 끝나며 하 여 제한 된 지정된 된 멤버와 같은 수준에서 멤버의 형제 집합을 반환 된 *분기* 시간 차원의 수준입니다.|  
|[형제 &#40; Mdx&#41;](../mdx/siblings-mdx.md)|멤버 자체를 포함하여 지정한 멤버의 형제 항목을 반환합니다.|  
|[StripCalculatedMembers &#40; Mdx&#41;](../mdx/stripcalculatedmembers-mdx.md)|지정한 집합에서 계산 멤버를 제거하여 생성된 집합을 반환합니다.|  
|[StrToSet &#40; Mdx&#41;](../mdx/strtoset-mdx.md)|MDX 형식 문자열에 의해 지정된 집합을 반환합니다.|  
|[하위 집합 &#40; Mdx&#41;](../mdx/subset-mdx.md)|지정한 집합에서 튜플의 하위 집합을 반환합니다.|  
|[비상 &#40; Mdx&#41;](../mdx/tail-mdx.md)|집합의 끝에서 하위 집합을 반환합니다.|  
|[ToggleDrillState &#40; Mdx&#41;](../mdx/toggledrillstate-mdx.md)|멤버의 드릴 상태를 토글합니다.|  
|[TopCount &#40; Mdx&#41;](../mdx/topcount-mdx.md)|집합을 내림차순으로 정렬하고 가장 높은 값을 갖는 요소를 지정된 수만큼 반환합니다.|  
|[TopPercent &#40; Mdx&#41;](../mdx/toppercent-mdx.md)|집합을 내림차순으로 정렬하고 누적 합계가 지정한 백분율 이하인 상위 값 튜플 집합을 반환합니다.|  
|[TopSum &#40; Mdx&#41;](../mdx/topsum-mdx.md)|집합을 정렬하고 누적 합계가 지정한 값 이상이 되는 상위 요소를 반환합니다.|  
|[Union &#40; Mdx&#41;](../mdx/union-mdx.md)|두 집합의 합집합을 반환합니다. 중복 요소를 포함시킬 수도 있습니다.|  
|[Unorder &#40; Mdx&#41;](../mdx/unorder-mdx.md)|지정한 집합에서 강제 적용된 순서를 제거합니다.|  
|[VisualTotals &#40; Mdx&#41;](../mdx/visualtotals-mdx.md)|지정한 집합의 자식 멤버의 합계를 동적으로 구하여 생성된 집합을 반환합니다. 결과 셀 집합에서 부모 멤버의 이름에 대한 패턴을 사용할 수도 있습니다.|  
|[Wtd &#40; Mdx&#41;](../mdx/wtd-mdx.md)|지정한 멤버와 동일한 수준의 형제 멤버 집합을 반환합니다. 이 집합은 첫 번째 형제 멤버부터 시작하여 지정된 멤버에서 끝나며 Time 차원의 Week 수준에 따라 제한됩니다.|  
|[Ytd &#40; Mdx&#41;](../mdx/ytd-mdx.md)|첫 번째 형제 항목부터 지정 된 멤버에서 끝나며 하 여 제한 된 지정된 된 멤버와 같은 수준에서 멤버의 형제 집합을 반환 된 *연도* 시간 차원의 수준입니다.|  
  
## <a name="string-functions"></a>문자열 함수  
  
|함수|Description|  
|--------------|-----------------|  
|[CalculationPassValue&#40;MDX&#41;](../mdx/calculationpassvalue-mdx.md)|지정한 큐브의 계산 패스에 대해 계산된 MDX 식의 값을 반환합니다.|  
|[CoalesceEmpty &#40; Mdx&#41;](../mdx/coalesceempty-mdx.md)|빈 셀 값을 숫자 또는 문자열에 결합하고 결합된 값을 반환합니다.|  
|[생성 &#40; Mdx&#41;](../mdx/generate-mdx.md)|한 집합을 다른 집합의 각 멤버에 적용하고 결과 집합을 합집합으로 결합시킵니다. 또는 집합에 대해 문자열 식을 계산하여 생성된 연결 문자열을 반환합니다.|  
|[IIf &#40; Mdx&#41;](../mdx/iif-mdx.md)|논리 테스트로 확인된 두 값 중 하나를 반환합니다.|  
|[LookupCube &#40; Mdx&#41;](../mdx/lookupcube-mdx.md)|같은 데이터베이스에서 지정된 또 다른 큐브에 대해 계산된 MDX 식의 값을 반환합니다.|  
|[MemberToStr &#40; Mdx&#41;](../mdx/membertostr-mdx.md)|지정된 멤버에 해당하는 MDX 형식 문자열을 반환합니다.|  
|[이름 &#40; Mdx&#41;](../mdx/name-mdx.md)|차원, 계층, 수준 또는 멤버의 이름을 반환합니다.|  
|[속성 &#40; Mdx&#41;](../mdx/properties-mdx.md)|멤버 속성 값을 포함하는 문자열 또는 강력한 형식의 값을 반환합니다.|  
|[SetToStr &#40; Mdx&#41;](../mdx/settostr-mdx.md)|지정된 집합에 해당하는 MDX 형식 문자열을 반환합니다.|  
|[TupleToStr &#40; Mdx&#41;](../mdx/tupletostr-mdx.md)|지정된 튜플에 해당하는 MDX 형식 문자열을 반환합니다.|  
|[UniqueName &#40; Mdx&#41;](../mdx/uniquename-mdx.md)|지정한 차원, 계층, 수준 또는 멤버의 고유 이름을 반환합니다.|  
|[사용자 이름 &#40; Mdx&#41;](../mdx/username-mdx.md)|현재 연결의 도메인 이름과 사용자 이름을 반환합니다.|  
  
## <a name="subcube-functions"></a>하위 큐브 함수  
  
|함수|Description|  
|--------------|-----------------|  
|[이 &#40; Mdx&#41;](../mdx/this-mdx.md)|현재 하위 큐브를 반환합니다.|  
|[Leaves &#40; Mdx&#41;](../mdx/leaves-mdx.md)|지정한 차원, 멤버 또는 튜플의 리프 멤버 집합을 반환합니다.|  
  
## <a name="tuple-functions"></a>튜플 함수  
  
|함수|Description|  
|--------------|-----------------|  
|[현재 &#40; Mdx&#41;](../mdx/current-mdx.md)|반복하는 동안 집합에서 현재 튜플을 반환합니다.|  
|[항목 &#40; 튜플 &#41; &#40; Mdx&#41;](../mdx/item-tuple-mdx.md)|집합에서 튜플을 반환합니다.|  
|[루트 &#40; Mdx&#41;](../mdx/root-mdx.md)|구성 된 튜플을 반환 된 **모든** 큐브, 차원 또는 튜플에서 각 특성 계층의 멤버입니다.|  
|[StrToTuple &#40; Mdx&#41;](../mdx/strtotuple-mdx.md)|MDX 형식 문자열에 의해 지정된 튜플을 반환합니다.|  
  
## <a name="other-functions"></a>기타 함수  
  
|함수|Description|  
|--------------|-----------------|  
|[오류 &#40; Mdx&#41;](../mdx/error-mdx.md)|오류를 발생시킵니다. 지정된 오류 메시지를 제공할 수도 있습니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 언어 참조 &#40; Mdx&#41;](../mdx/mdx-language-reference-mdx.md)  
  
  
