---
title: Storage 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Storage Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.storage
- urn:schemas-microsoft-com:xml-analysis#Storage
- http://schemas.microsoft.com/analysisservices/2003/engine#Storage
helpviewer_keywords:
- Storage element
ms.assetid: c3590af8-a24b-4fd3-b846-17edbd399b6d
caps.latest.revision: 10
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 8bccf119846d699d653a480f6479412b46dcc4f9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36185057"
---
# <a name="storage-element-xmla"></a>Storage 요소(XMLA)
  [DesignAggregations](../xml-elements-commands/designaggregations-element-xmla.md) 명령에서 집계를 디자인하는 데 사용되는 최대 저장소 크기(바이트)를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DesignAggregations>  
   ...  
   <Storage>...</Storage>  
   ...  
</DesignAggregations>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Long|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DesignAggregations](../xml-elements-commands/designaggregations-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  