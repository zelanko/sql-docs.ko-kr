---
title: SessionID 요소 (XMLA) | Microsoft Docs
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
- SessionID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#SessionID
- http://schemas.microsoft.com/analysisservices/2003/engine#SessionID
- microsoft.xml.analysis.sessionid
helpviewer_keywords:
- SessionID element
ms.assetid: 18220e00-76cf-48f6-9465-200465a0c553
caps.latest.revision: 10
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c7f0466ac9a175a6e31df235fa11cd4662e46b73
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37207563"
---
# <a name="sessionid-element-xmla"></a>SessionID 요소(XMLA)
  부모를 실행할 활성 세션을 식별 [취소](../xml-elements-commands/cancel-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Cancel>  
   ...  
   <SessionID>...</SessionID>  
   ...  
</Cancel>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[취소](../xml-elements-commands/cancel-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>관련 항목  
 [CancelAssociated 요소 &#40;XMLA&#41;](cancelassociated-element-xmla.md)   
 [ConnectionID 요소 &#40;XMLA&#41;](id-element-xmla.md)   
 [SPID 요소 &#40;XMLA&#41;](spid-element-xmla.md)   
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
