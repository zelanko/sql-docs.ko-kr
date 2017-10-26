---
title: "요소 (XMLA) 결과 | Microsoft Docs"
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
- results Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.results
- urn:schemas-microsoft-com:xml-analysis#results
- http://schemas.microsoft.com/analysisservices/2003/engine#results
helpviewer_keywords:
- results element
ms.assetid: 3249a17a-7bfa-4753-b605-8f611ba7ae2b
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 791512ba71ef92a9e220936b138faf9eff2a4872
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="results-element-xmla"></a>results 요소(XMLA)
  [Batch](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) 명령을 사용하여 [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) 메서드에 의해 반환되는 [root](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) 요소의 컬렉션을 포함합니다.  
  
 **Namespace**`http://schemas.microsoft.com/analysisservices/2003/xmla-multipleresults`  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<return>  
   <results>  
      <root>...</root>  
   </results>  
</return>  
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
|부모 요소|[반환](../../../analysis-services/xmla/xml-elements-properties/return-element-xmla.md)|  
|자식 요소|[루트](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
 **Batch** 메서드에 의해 **Execute** 명령이 실행되면 **return** 요소는 단일 **results** 요소가 아닌 단일 **root** 요소를 포함합니다. **results** 요소의 내용은 **Batch** 명령을 실행하는 데 사용된 설정에 따라 달라집니다.  
  
 비트랜잭션 **Batch** 명령의 경우 **results** 요소는 **root** 명령에 의해 실행되는 각 명령에 대해 명령의 성공적인 실행 여부에 관계없이 하나의 **Batch** 요소를 포함합니다. 트랜잭션 **Batch** 명령의 경우 **results** 요소는 하나의 **root** 요소만 포함하며, 이 요소는 **Batch** 명령 내에서 실패한 명령에 대한 오류 정보를 포함합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

