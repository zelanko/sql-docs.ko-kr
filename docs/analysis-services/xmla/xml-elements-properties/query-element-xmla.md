---
title: 요소 (XMLA) 쿼리 | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 861f216ac263de32b9f2afc3e0fcd4e43b3dfb4a
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37984644"
---
# <a name="query-element-xmla"></a>Query 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  내에서 쿼리를 포함 합니다 [쿼리](../../../analysis-services/xmla/xml-elements-properties/queries-element-xmla.md) 사용 되는 컬렉션의 [DesignAggregations](../../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md) 사용 빈도 기반 최적화 중 명령을.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Queries>  
   ...  
   <Query>...</Query>  
   ...  
</Queries>  
```  
  
## <a name="element-characteristics"></a>요소 특성  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[쿼리](../../../analysis-services/xmla/xml-elements-properties/queries-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 **DesignAggregations** 명령은 명령의 **Query** 컬렉션에 하나 이상의 **Queries** 요소를 포함하여 사용 빈도 기반 최적화를 지원합니다. 각 **Query** 요소는 가장 자주 사용하는 쿼리를 대상으로 하는 집계를 정의하기 위해 디자인 프로세스에서 사용하는 목표 쿼리를 나타냅니다. 사용자 고유의 목표 쿼리를 지정 하거나 또는 자주 사용 하는 쿼리에 대 한 정보를 검색 하는 인스턴스의 Analysis Services 쿼리 로그에 저장 된 정보를 사용할 수 있습니다.  
  
 만 첫 번째 범위에서 목표 쿼리를 전달 해야 집계를 반복적으로 디자인 하는 경우 **DesignAggregations** 있기 때문에 명령을 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스가 이러한 목표 쿼리를 저장 하 고 이러한 쿼리를 사용 하 여 후속 중 **DesignAggregations** 명령입니다. 반복 프로세스의 첫 번째 **DesignAggregations** 명령에서 목표 쿼리를 전달하면 **DesignAggregations** 속성에 목표 쿼리를 포함하는 모든 후속 **Queries** 명령은 오류를 생성합니다.  
  
 **Query** 요소에는 다음 인수를 포함하는 쉼표로 구분된 값이 포함됩니다.  
  
 *Frequency*,*Dataset*[,*Dataset*...]  
  
 *빈도*  
 쿼리가 이전에 실행된 횟수에 해당하는 가중 요인입니다. **Query** 요소가 새 쿼리를 나타내는 경우 *Frequency* 값은 쿼리를 평가하기 위해 디자인 프로세스에 사용되는 가중 요인을 나타냅니다. 빈도 값이 증가하면서 디자인 프로세스 중 쿼리에 적용되는 가중치도 증가합니다.  
  
 *데이터 집합*  
 쿼리에 포함될 차원 특성을 지정하는 숫자 문자열입니다. 이 문자열에는 차원의 특성 수와 같은 문자 수가 있어야 합니다. 영(0)은 지정된 서수 위치의 특성이 지정된 차원의 쿼리에 포함되지 않음을 나타내고 일(1)은 지정된 서수 위치의 특성이 지정된 차원의 쿼리에 포함됨을 나타냅니다.  
  
 예를 들어 문자열 "011"은 세 개의 특성이 있는 차원을 사용하는 쿼리를 참조하며 여기서 두 번째 및 세 번째 특성이 쿼리에 포함됩니다.  
  
> [!NOTE]  
>  일부 특성은 데이터 집합에서 고려되지 않습니다. 제외 되는 특성에 대 한 자세한 내용은 참조 하세요. [Properties (XMLA)](../../../analysis-services/xmla/xml-elements-properties/query-element-xmla.md)합니다.  
  
 집계 디자인을 포함하는 측정값 그룹의 각 차원은 *Query* 요소의 **Dataset** 값으로 나타납니다. *Dataset* 값의 순서는 측정값 그룹에 포함된 차원의 순서와 일치해야 합니다.  
  
## <a name="see-also"></a>참고자료
 [집계 디자인 &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/designing-aggregations-xmla.md)   
 [속성 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
