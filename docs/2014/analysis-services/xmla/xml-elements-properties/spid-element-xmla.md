---
title: SPID 요소 (XMLA) | Microsoft Docs
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
- SPID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#SPID
- microsoft.xml.analysis.spid
- urn:schemas-microsoft-com:xml-analysis#SPID
helpviewer_keywords:
- SPID element
ms.assetid: c4a54dcb-a0cd-4255-9e0f-a34eb990854f
caps.latest.revision: 15
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 27244dab841ac4793d66c6b177d5382ca7cdc7a7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37167024"
---
# <a name="spid-element-xmla"></a>SPID 요소(XMLA)
  부모를 실행 하는 활성 서버 프로세스 식별자 (SPID)를 식별 [취소](../xml-elements-commands/cancel-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Cancel>  
   ...  
   <SPID>...</SPID>  
   ...  
</Cancel>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|정수|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[취소](../xml-elements-commands/cancel-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 합니다 `SPID` 요소를 서버 프로세스 ID (SPID) 인스턴스에서 지정된 된 세션에 사용 되는 나타냅니다 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
## <a name="see-also"></a>관련 항목  
 [CancelAssociated 요소 &#40;XMLA&#41;](cancelassociated-element-xmla.md)   
 [ConnectionID 요소 &#40;XMLA&#41;](id-element-xmla.md)   
 [SessionID 요소 &#40;XMLA&#41;](sessionid-element-xmla.md)   
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
