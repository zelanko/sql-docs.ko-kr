---
title: 개체 요소 (XMLA) | Microsoft Docs
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
- Object Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Object
- urn:schemas-microsoft-com:xml-analysis#Object
- microsoft.xml.analysis.object
helpviewer_keywords:
- Object element
ms.assetid: 99470537-2c4a-4072-9613-940c41c12487
caps.latest.revision: 16
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 678838cd084fb8d3c7905f3e7363059fea28f541
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37229583"
---
# <a name="object-element-xmla"></a>Object 요소(XMLA)
  부모 요소에 사용되는 개체 참조를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Alter> <!-- or any of the parent elements in the Element Relationships table -->  
...  
   <Object>  
      <!-- One or more object identifiers, depending on the parent element -->  
   </Object>  
...  
</Alter>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|상위 항목 또는 부모: [Alter](../xml-elements-commands/create-element-xmla.md) &#124; 0-1: 한 번만 나타날 수 있는 선택적 요소입니다.<br /><br /> 상위 항목 또는 부모: 다른 모든 &#124; 1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Alter](../xml-elements-commands/alter-element-xmla.md), [Backup](../xml-elements-commands/backup-element-xmla.md), [ClearCache](../xml-elements-commands/clearcache-element-xmla.md)를 [삭제](../xml-elements-commands/delete-element-xmla.md)를 [DesignAggregations](../xml-elements-commands/designaggregations-element-xmla.md), [잠금](../xml-elements-commands/lock-element-xmla.md), [NotifyTableChange](../xml-elements-commands/notifytablechange-element-xmla.md), [프로세스](../xml-elements-commands/process-element-xmla.md)하십시오 [구독](../xml-elements-commands/subscribe-element-xmla.md), [동기화](../xml-elements-commands/synchronize-element-xmla.md)|  
|자식 요소|필수 ASSL(Analysis Services Scripting Language) 요소. 개체 및 해당 상위 항목(`Server` 개체 제외)의 ID 요소를 나열하여 지정됩니다. 예를 들어 다음 `Object` 요소에서는 파티션을 식별합니다.<br /><br /> `<Object>`<br /><br /> `<DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>`<br /><br /> `<CubeID>Adventure Works</CubeID>`<br /><br /> `<MeasureGroupID>Internet Sales</MeasureGroupID>`<br /><br /> `<PartitionID>Inernet_Sales_2001</PartitionID>`<br /><br /> `</Object>`|  
  
## <a name="remarks"></a>Remarks  
 식별자가 나타나는 순서는 중요하지 않습니다.  
  
 에 대 한 `Alter` 요소, 인스턴스의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 하는 경우 기본 개체로 사용 되는 `Object` 요소가 지정 되지 않은 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
