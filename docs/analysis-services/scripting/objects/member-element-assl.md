---
title: "Member 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Member Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Member
helpviewer_keywords:
- Member element
ms.assetid: 03b4cfcb-ce87-452f-9e25-8745c0423f56
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fbb9e95ecb65dd5d065bdfa8ca30b26ddb906df2
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="member-element-assl"></a>Member 요소(ASSL)
  [Group](../../../analysis-services/scripting/objects/group-element-assl.md) 요소 멤버 또는 [Role](../../../analysis-services/scripting/objects/role-element-assl.md) 요소 멤버의 이름을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Members>  
   <Member>  
      <Name>...</Name>  
   </Member>  
</Members>  
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
|부모 요소|[멤버](../../../analysis-services/scripting/collections/members-element-assl.md)|  
|자식 요소|[이름](../../../analysis-services/scripting/properties/name-element-assl.md)|  
  
## <a name="remarks"></a>주의  
 부모에 해당 하는 요소 **멤버** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Group> 및 <xref:Microsoft.AnalysisServices.Role>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [개체 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  

