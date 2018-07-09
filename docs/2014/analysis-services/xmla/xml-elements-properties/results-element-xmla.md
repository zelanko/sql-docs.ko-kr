---
title: 요소 (XMLA) 결과 | Microsoft Docs
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
- results Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.results
- urn:schemas-microsoft-com:xml-analysis#results
- http://schemas.microsoft.com/analysisservices/2003/engine#results
helpviewer_keywords:
- results element
ms.assetid: 3249a17a-7bfa-4753-b605-8f611ba7ae2b
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1e42f6aa620b57630df690ee92bdbbd849ab100b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37165234"
---
# <a name="results-element-xmla"></a>results 요소(XMLA)
  [Batch](root-element-xmla.md) 명령을 사용하여 [Execute](../xml-elements-methods-execute.md) 메서드에 의해 반환되는 [root](../xml-elements-commands/batch-element-xmla.md) 요소의 컬렉션을 포함합니다.  
  
 **Namespace** http://schemas.microsoft.com/analysisservices/2003/xmla-multipleresults  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<return>  
   <results>  
      <root>...</root>  
   </results>  
</return>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[반환](return-element-xmla.md)|  
|자식 요소|[root](root-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 `Batch` 메서드에 의해 `Execute` 명령이 실행되면 `return` 요소는 단일 `results` 요소가 아닌 단일 `root` 요소를 포함합니다. `results` 요소의 내용은 `Batch` 명령을 실행하는 데 사용된 설정에 따라 달라집니다.  
  
 비트랜잭션 `Batch` 명령의 경우 `results` 요소는 `root` 명령에 의해 실행되는 각 명령에 대해 명령의 성공적인 실행 여부에 관계없이 하나의 `Batch` 요소를 포함합니다. 트랜잭션 `Batch` 명령의 경우 `results` 요소는 하나의 `root` 요소만 포함하며, 이 요소는 `Batch` 명령 내에서 실패한 명령에 대한 오류 정보를 포함합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
