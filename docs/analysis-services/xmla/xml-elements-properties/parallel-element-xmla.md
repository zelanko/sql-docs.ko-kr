---
title: Parallel 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f9bbf11a8cc3718a9538f0563e6f4f5680e87c9c
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="parallel-element-xmla"></a>Parallel Element (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  처리 작업의 수는 부모를 사용 하 여 병렬로 실행할 수 있는 지정 [일괄 처리](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) 명령입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Batch>  
   ....  
   <Parallel maxParallel="Integer">  
      <!-- An XMLA process command -->  
   </Parallel>  
   ....  
</Batch>  
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
|부모 요소|[일괄 처리](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)|  
|자식 요소|[Process 요소](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)|  
  
## <a name="attributes"></a>특성  
  
|Attribute|Description|  
|---------------|-----------------|  
|maxParallel|선택적 **Integer** 특성입니다. 병렬로 명령을 실행할 최대 스레드 수를 나타냅니다. 지정하지 않거나 0으로 설정하면 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스는 컴퓨터에서 사용할 수 있는 프로세서 수에 따라 최적의 스레드 수를 결정합니다.|  
  
## <a name="remarks"></a>주의  
  
## <a name="see-also"></a>참고 항목  
 [속성 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
