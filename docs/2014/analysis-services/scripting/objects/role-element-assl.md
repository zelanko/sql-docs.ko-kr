---
title: Role 요소 (ASSL) | Microsoft Docs
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
- Role Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ROLE
helpviewer_keywords:
- Role element
ms.assetid: 56f52462-a7fd-4b51-a7fb-4311134439e9
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0486e6f0f8cc5886c5bcab5ea389440c8d26523b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37285979"
---
# <a name="role-element-assl"></a>Role 요소(ASSL)
  보안 역할에 대한 정보를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Roles>  
      <Role>  
      <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</CreateTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <Description>...</Description>  
      <Members>...</Members>  
      <Annotations>...</Annotations>  
   </Role>  
</Roles>  
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
|부모 요소|[Roles](../collections/roles-element-assl.md)|  
|자식 요소|[주석을](../collections/annotations-element-assl.md), [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)를 [설명](../properties/description-element-assl.md)를 [ID](../properties/id-element-assl.md)를 [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md), [멤버 ](../collections/members-element-assl.md), [이름](../properties/name-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 역할 정의는 역할의 멤버인 사용자를 포함합니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.Role>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Database 요소 &#40;ASSL&#41;](database-element-assl.md)   
 [Server 요소 &#40;ASSL&#41;](server-element-assl.md)   
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  
