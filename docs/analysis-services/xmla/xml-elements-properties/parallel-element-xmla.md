---
title: "Parallel 요소 (XMLA) | Microsoft Docs"
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.custom: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Parallel Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Parallel
- http://schemas.microsoft.com/analysisservices/2003/engine#Parallel
- microsoft.xml.analysis.parallel
helpviewer_keywords: Parallel element
ms.assetid: 04726d94-37ee-460b-9744-d62b45f536b9
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0045bb8696a6f8cae8977cd5d4f2d1b6da0f8f22
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="parallel-element-xmla"></a>Parallel Element (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]처리 작업의 수는 부모를 사용 하 여 병렬로 실행할 수 있는 지정 [일괄 처리](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) 명령입니다.  
  
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
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[일괄 처리](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)|  
|자식 요소|[Process 요소](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)|  
  
## <a name="attributes"></a>특성  
  
|attribute|Description|  
|---------------|-----------------|  
|maxParallel|선택적 **Integer** 특성입니다. 병렬로 명령을 실행할 최대 스레드 수를 나타냅니다. 지정하지 않거나 0으로 설정하면 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스는 컴퓨터에서 사용할 수 있는 프로세서 수에 따라 최적의 스레드 수를 결정합니다.|  
  
## <a name="remarks"></a>주의  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
