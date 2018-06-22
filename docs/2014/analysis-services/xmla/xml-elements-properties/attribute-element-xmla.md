---
title: 요소 (XMLA) 특성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Attribute Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Attribute
- microsoft.xml.analysis.attribute
- urn:schemas-microsoft-com:xml-analysis#Attribute
helpviewer_keywords:
- Attribute element
ms.assetid: 0df9cf44-dc5f-4234-8a5a-daac8aabc0d6
caps.latest.revision: 17
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 665626323e435eeed50b73f4d94de4506dba4f19
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081919"
---
# <a name="attribute-element-xmla"></a>Attribute 요소(XMLA)
  정의 하거나 필터링 되는 특성의 멤버는 부모 [삽입](../xml-elements-commands/insert-element-xmla.md), [업데이트](../xml-elements-commands/update-element-xmla.md), 또는 [Drop](../xml-elements-commands/drop-element-xmla.md) 명령은 작업을 수행 합니다.  
  
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
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[특성](attributes-element-xmla.md)|  
  
 **자식 요소**  
  
|||  
|-|-|  
|**상위 항목 또는 부모**|**자식 요소**|  
|[Drop](../xml-elements-commands/drop-element-xmla.md), [여기서](name-element-xmla.md), [키](keys-element-xmla.md)|  
|[삽입](../xml-elements-commands/insert-element-xmla.md), [업데이트](../xml-elements-commands/update-element-xmla.md)|[AttributeName](name-element-xmla.md), [CustomRollup](customrollup-element-xmla.md), [CustomRollupProperties](properties-element-xmla.md), [키](keys-element-xmla.md), [이름](name-element-xmla.md), [ SkippedLevels](skippedlevels-element-xmla.md), [번역](translations-element-xmla.md), [UnaryOperator](unaryoperator-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 `Attribute` 요소 정의 특성 멤버를 삽입, 업데이트 또는 삭제 하 여 각각의 `Insert`, `Update`, 또는 `Drop` 명령입니다. 이러한 명령은 한 번에 하나의 특성 멤버 에서만 작동할 수 있으므로 대로 [특성](attributes-element-xmla.md) 의 컬렉션은 `Insert`, `Update`, 및 `Drop` 명령을 하나만 사용할 수 있습니다 `Attribute` 요소입니다. 그러나 `Attributes` 및 `Where` 명령에 대한 `Drop` 요소의 `Update` 컬렉션은 두 개 이상의 `Attribute` 요소를 포함할 수 있으므로 쓰기 가능 차원에서 삭제 또는 업데이트될 특성을 필터링할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)   
 [쓰기 가능 차원](../../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  