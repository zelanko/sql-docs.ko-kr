---
title: DesignAggregations 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5338f7650cdd1f533832987f5fe79a532a9a375d
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="designaggregations-element-xmla"></a>DesignAggregations 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  에 집계 디자인에 대 한 집계를 만듭니다는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Command>  
   <DesignAggregations>  
      <Object>...</Object>  
      <Time>...</Time>  
      <Steps>...</Steps>  
      <Optimization>...</Optimization>  
      <Storage>...</Storage>  
      <Materialize>...</Materialize>  
      <Queries>...</Queries>  
   </DesignAggregations>  
</Command>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|자식 요소|[구체화](../../../analysis-services/xmla/xml-elements-properties/materialize-element-xmla.md), [개체](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md), [최적화](../../../analysis-services/xmla/xml-elements-properties/optimization-element-xmla.md), [쿼리](../../../analysis-services/xmla/xml-elements-properties/queries-element-xmla.md), [단계](../../../analysis-services/xmla/xml-elements-properties/steps-element-xmla.md), [저장소](../../../analysis-services/xmla/xml-elements-properties/storage-element-xmla.md) [시간](../../../analysis-services/xmla/xml-elements-properties/time-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
 **DesignAggregations** 명령은 집계 디자인에서 저장한 집계 정의를 생성하는 데 사용됩니다. 이때 집계 디자인을 사용하여 파티션에 대한 집계를 구체화하고 파티션 사이에서 다시 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [명령 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
