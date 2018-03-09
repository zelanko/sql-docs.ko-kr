---
title: "AllowBrowsing 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: AllowBrowsing Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: AllowBrowsing
helpviewer_keywords: AllowBrowsing element
ms.assetid: e5d09f8c-080b-4013-8c6a-0c9775e6ab25
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 462ecdcf9bb12e536d894a5e6e46d44df7d9d7fc
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="allowbrowsing-element-assl"></a>AllowBrowsing 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]정의 여부의 멤버는 [역할](../../../analysis-services/scripting/objects/role-element-assl.md) 요소에 대 한 찾아보기 권한이 [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MiningModelPermission>  
      ...  
   <AllowBrowsing>...</AllowBrowsing>  
   ...  
</MiningModelPermission>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Boolean|  
|기본값|**True**|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[MiningModelPermission](../../../analysis-services/scripting/objects/miningmodelpermission-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>주의  
 부모에 해당 하는 요소 **AllowBrowsing** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.MiningModelPermission>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
