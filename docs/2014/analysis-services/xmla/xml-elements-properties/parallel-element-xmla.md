---
title: 요소 (XMLA) 병렬 | Microsoft Docs
ms.custom: ''
ms.date: 2015-12-07
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Parallel Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Parallel
- http://schemas.microsoft.com/analysisservices/2003/engine#Parallel
- microsoft.xml.analysis.parallel
helpviewer_keywords:
- Parallel element
ms.assetid: 04726d94-37ee-460b-9744-d62b45f536b9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 90c722d8bb1b32e17ef5dc27e8ea0c84b00ff80e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48091563"
---
# <a name="parallel-element-xmla"></a>Parallel Element (XMLA)
  부모 [Batch](../xml-elements-commands/batch-element-xmla.md) 명령에 의해 병렬로 실행될 명령을 식별합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Batch>  
   ....  
   <Parallel maxParallel="Integer">  
      <!-- One or more XMLA commands -->  
   </Parallel>  
   ....  
</Batch>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[일괄 처리](../xml-elements-commands/batch-element-xmla.md)|  
|자식 요소|[Process 요소](../xml-elements-commands/process-element-xmla.md)|  
  
## <a name="attributes"></a>특성  
  
|attribute|Description|  
|---------------|-----------------|  
|maxParallel|선택적 `Integer` 특성입니다. 병렬로 명령을 실행할 최대 스레드 수를 나타냅니다. 지정하지 않거나 0으로 설정하면 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스는 컴퓨터에서 사용할 수 있는 프로세서 수에 따라 최적의 스레드 수를 결정합니다.|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
