---
title: "여기서 요소 (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Where Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Where
- microsoft.xml.analysis.where
- http://schemas.microsoft.com/analysisservices/2003/engine#Where
helpviewer_keywords: Where element
ms.assetid: 81fb4190-3379-4ddf-8795-a0772f3b92bb
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5cff731a9673f8f811895f6dcc2b1a65c77f5716
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="where-element-xmla"></a>Where 요소(XMLA)
  부모 [Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md) 또는 [Update](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md) 명령에 사용되는 필터 조건을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Drop> <!-- or Update -->  
   ...  
   <Where>  
      <Attributes>...</Attributes>  
   </Where>  
   ...  
</Insert>  
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
|부모 요소|[Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md), [Update](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)|  
|자식 요소|[특성](../../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
 **Drop** 명령의 경우 [DeleteWithDescendants](../../../analysis-services/xmla/xml-elements-properties/deletewithdescendants-element-xmla.md) 요소와 함께 **Where** 요소를 사용하면 삭제될 특성 멤버의 범위가 식별됩니다.  
  
 **Update** 명령의 경우 **Where** 요소는 업데이트될 특성 멤버의 범위를 식별합니다. 부모 **Attributes** 명령의 **Update** 컬렉션과 **Attributes** 요소의 **Where** 컬렉션에 포함된 특성의 조합을 사용하여 여러 특성 멤버를 업데이트할 수 있습니다.  
  
 특성 멤버 삭제 및 업데이트에 대한 자세한 내용은 [멤버 삽입, 업데이트 및 삭제&#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
