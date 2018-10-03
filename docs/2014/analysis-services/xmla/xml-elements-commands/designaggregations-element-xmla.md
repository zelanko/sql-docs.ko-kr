---
title: DesignAggregations 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DesignAggregations Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#DesignAggregations
- microsoft.xml.analysis.designaggregations
- http://schemas.microsoft.com/analysisservices/2003/engine#DesignAggregations
helpviewer_keywords:
- DesignAggregations command
ms.assetid: 4c419dbc-7405-40aa-8ddd-6b46685a297d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c9ddcd70a0512273f816b633933b26fbf12d5b5a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48058993"
---
# <a name="designaggregations-element-xmla"></a>DesignAggregations 요소(XMLA)
  에 집계 디자인에 대 한 집계를 만듭니다는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Command>  
   <DesignAggregations>  
      <Object>...</Object>  
      <Time>...</Time>  
      <Steps>...</Steps>  
      <Optimization>...</Optimization>  
      <Storage>...</Storage>  
      <Materialize>...</Materialize>  
      <Queries>...</Queries>  
   </DesignAggregations>  
</Command>  
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
|부모 요소|[Command](../xml-elements-properties/command-element-xmla.md)|  
|자식 요소|[구체화](../xml-elements-properties/materialize-element-xmla.md), [개체](../xml-elements-properties/object-element-xmla.md)를 [최적화](../xml-elements-properties/optimization-element-xmla.md)를 [쿼리](../xml-elements-properties/queries-element-xmla.md)를 [단계](../xml-elements-properties/steps-element-xmla.md)를 [저장소](../xml-elements-properties/storage-element-xmla.md) [시간](../xml-elements-properties/time-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 `DesignAggregations` 명령은 집계 디자인에서 저장한 집계 정의를 생성하는 데 사용됩니다. 이때 집계 디자인을 사용하여 파티션에 대한 집계를 구체화하고 파티션 사이에서 다시 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [명령 &#40;XMLA&#41;](xml-elements-commands.md)  
  
  
