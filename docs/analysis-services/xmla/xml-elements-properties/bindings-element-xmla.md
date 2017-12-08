---
title: "Bindings 요소 (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
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
apiname: Bindings Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.bindings
- urn:schemas-microsoft-com:xml-analysis#Bindings
- http://schemas.microsoft.com/analysisservices/2003/engine#Bindings
helpviewer_keywords: Bindings element
ms.assetid: caa34cab-f61f-4f39-b800-af1601714daa
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ddf92b4ddff00a0b5a74d22efcf8d66a989bc0d2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="bindings-element-xmla"></a>Bindings 요소(XMLA)
  부모 [Batch](../../../analysis-services/xmla/xml-elements-properties/binding-element-xmla.md) 또는 [Process](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) 요소의 [Binding](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md) 요소 컬렉션을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Batch> <!-- or Process>  
...  
   <Bindings>  
      <Binding>...</Binding>  
   </Bindings>  
...  
</Alter>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Batch](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md), [Process](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)|  
|자식 요소|[바인딩](../../../analysis-services/xmla/xml-elements-properties/binding-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
