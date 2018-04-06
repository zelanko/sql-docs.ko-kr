---
title: Roles 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Roles Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Roles
helpviewer_keywords:
- Roles element
ms.assetid: 4191b7ce-bae4-4200-8550-3904420efafd
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 06fe47cbf3a13cc1c816f698b2ee80bec9e09f63
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="roles-element-assl"></a>Roles 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]컬렉션을 포함 [역할](../../../analysis-services/scripting/objects/role-element-assl.md) 부모 요소 아래에 정의 된 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Database> <!-- or Server -->  
   ...  
   <Roles>  
      <Role>...</Role>  
   </Roles>  
   ...  
</Database>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Database](../../../analysis-services/scripting/objects/database-element-assl.md), [Server](../../../analysis-services/scripting/objects/server-element-assl.md)|  
|자식 요소|[역할](../../../analysis-services/scripting/objects/role-element-assl.md)|  
  
## <a name="remarks"></a>주의  
 **Roles** 요소와 연결된 **Server** 요소는 관리자라는 하나의 역할만 포함하며, 이는 서버 관리자 역할을 나타냅니다. 서버 관리자 역할은 변경 또는 삭제할 수 없으며 컬렉션에 다른 역할을 추가할 수도 없습니다.  
  
 **Roles** 요소와 연결된 **Database** 요소는 해당 데이터베이스에 대해 정의된 역할을 포함합니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.RoleCollection>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [컬렉션 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
