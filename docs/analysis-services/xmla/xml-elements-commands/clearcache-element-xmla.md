---
title: "ClearCache 요소 (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: ClearCache Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#ClearCache
- urn:schemas-microsoft-com:xml-analysis#ClearCache
- microsoft.xml.analysis.clearcache
helpviewer_keywords: ClearCache command
ms.assetid: e154b489-e443-469a-9490-43c62da62e11
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 26ee325d084fa98576b9c108f5ffda6e5da400d6
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="clearcache-element-xmla"></a>ClearCache 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]에 지정된 된 개체에 대 한 메모리 캐시를 지웁니다는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Command>  
   <ClearCache>  
      <Object>...</Object>  
   </ClearCache>  
</Command>  
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
|부모 요소|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|자식 요소|[개체](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
 **ClearCache** 명령에 지정 된 데이터베이스, 차원, 큐브, 측정값 그룹 또는 파티션에 대 한 캐시를 플러시합니다는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스. **Object** 요소에 데이터베이스, 차원, 큐브, 측정값 그룹 또는 파티션 이외의 개체가 지정되면 오류가 발생합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [명령 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
