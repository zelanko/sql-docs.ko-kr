---
title: 바인딩 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1b8062ed41c078d24e8e5f0c708a8840c7a18899
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="binding-element-xmla"></a>Binding 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  에 대 한 아웃오브 라인 바인딩을 정의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 개체, 예: 차원에서 특성에 대 한는 [바인딩](../../../analysis-services/xmla/xml-elements-properties/bindings-element-xmla.md) 의 컬렉션을 [일괄 처리](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) 또는 [ 프로세스](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md) 명령입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Bindings>  
   <Binding xsi:type="DimensionAttributeBinding">...</Binding>  
   <!-- or -->  
   <Binding xsi:type="MeasureGroupAttributeBinding">...</Binding>  
   <!-- or -->  
   <Binding xsi:type="PartitionBinding">...</Binding>  
</Bindings>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|[DimensionAttributeBinding](../../../analysis-services/scripting/data-type/dimensionattributebinding-data-type-out-of-line-assl.md), [MeasureGroupAttributeBinding](../../../analysis-services/scripting/data-type/measuregroupattributebinding-data-type-out-of-line-assl.md), [PartitionBinding](../../../analysis-services/scripting/data-type/partitionbinding-data-type-assl.md)|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[바인딩](../../../analysis-services/xmla/xml-elements-properties/bindings-element-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **바인딩** 요소에 대 한 데이터 원본 및 데이터 원본 뷰 이외의 아웃오브 라인 바인딩을 정의 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 에서 처리할 개체는 **일괄 처리** 또는 **프로세스** 명령입니다. 개체를 처리 하는 방법에 대 한 자세한 내용은 참조 [개체 처리 &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/processing-objects-xmla.md)합니다.  
  
 아웃오브 라인 바인딩에 대 한 자세한 내용은 참조 하십시오. [데이터 원본 및 바인딩 & #40; SSAS 다차원 & #41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
