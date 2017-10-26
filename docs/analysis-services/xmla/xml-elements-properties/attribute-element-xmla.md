---
title: "요소 (XMLA) 특성 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Attribute Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Attribute
- microsoft.xml.analysis.attribute
- urn:schemas-microsoft-com:xml-analysis#Attribute
helpviewer_keywords:
- Attribute element
ms.assetid: 0df9cf44-dc5f-4234-8a5a-daac8aabc0d6
caps.latest.revision: 17
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2ac9985902b6e91fd2f69b2cc7b7ea3eec6cc79e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="attribute-element-xmla"></a>Attribute 요소(XMLA)
  정의 하거나 필터링 되는 특성의 멤버는 부모 [삽입](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md), [업데이트](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md), 또는 [Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md) 명령은 작업을 수행 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Attributes>  
   ...  
   <Attribute>  
      <AttributeName>...</AttributeName>  
      <Keys>...</Keys>  
      <!-- The following elements are included only for attributes contained in the Attributes element of a parent Insert or Update command -->  
      <Name>...</Name>  
      <Translations>...</Translations>  
      <CustomRollup>...</CustomRollup>  
      <CustomRollupProperties>...</CustomRollupProperties>  
      <UnaryOperator>...</UnaryOperator>  
      <SkippedLevels>...</SkippedLevels>  
   </Attribute>  
   ...  
</Attributes>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[특성](../../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md)|  
|자식 요소|아래 표를 참조 합니다.|  
  
|상위 항목 또는 부모|자식 요소|  
|------------------------|-------------------|  
|[Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md), [위치](../../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md)|[AttributeName](../../../analysis-services/xmla/xml-elements-properties/attributename-element-xmla.md), [키](../../../analysis-services/xmla/xml-elements-properties/keys-element-xmla.md)|  
|[삽입](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md), [업데이트](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)|[AttributeName](../../../analysis-services/xmla/xml-elements-properties/attributename-element-xmla.md), [CustomRollup](../../../analysis-services/xmla/xml-elements-properties/customrollup-element-xmla.md), [CustomRollupProperties](../../../analysis-services/xmla/xml-elements-properties/customrollupproperties-element-xmla.md), [키](../../../analysis-services/xmla/xml-elements-properties/keys-element-xmla.md), [이름](../../../analysis-services/xmla/xml-elements-properties/name-element-xmla.md), [ SkippedLevels](../../../analysis-services/xmla/xml-elements-properties/skippedlevels-element-xmla.md), [번역](../../../analysis-services/xmla/xml-elements-properties/translations-element-xmla.md), [UnaryOperator](../../../analysis-services/xmla/xml-elements-properties/unaryoperator-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
 **Attribute** 요소는 각각 **Insert**, **Update**또는 **Drop** 명령에 의해 삽입, 업데이트 또는 삭제되는 특성 멤버를 정의합니다. 이러한 명령은 한 번에 하나의 특성 멤버 에서만 작동할 수 있으므로으로 [특성](../../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md) 의 컬렉션은 **삽입**, **업데이트**, 및 **Drop**명령을 하나만 사용할 수 있습니다 **특성** 요소입니다. 그러나 **Attributes** 및 **Where** 명령에 대한 **Drop** 요소의 **Update** 컬렉션은 두 개 이상의 **Attribute** 요소를 포함할 수 있으므로 쓰기 가능 차원에서 삭제 또는 업데이트될 특성을 필터링할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)   
 [쓰기 가능 차원](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  

