---
title: "HideMemberIf 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: HideMemberIf Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: HideMemberIf
helpviewer_keywords: HideMemberIf element
ms.assetid: ff0e6b19-6216-43ac-ba76-1628da8c333b
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0a65a295a16153c94c2deab9770ede60c1438e4a
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="hidememberif-element-assl"></a>HideMemberIf 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]시점과 클라이언트 응용 프로그램에서 수준의 멤버를 숨길지 여부를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Level>  
   ...  
   <HideMemberIf>...</HideMemberIf>  
   ...  
</Level>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*하지*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Level](../../../analysis-services/scripting/objects/level-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 있는 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*하지*|멤버를 숨기지 않습니다.|  
|*OnlyChildWithNoName*|멤버가 부모의 유일한 자식이고 이름이 비어 있는 경우 멤버를 숨깁니다.|  
|*OnlyChildWithParentName*|멤버가 부모의 유일한 자식이고 이름이 부모와 동일한 경우 멤버를 숨깁니다.|  
|*NoName*|멤버의 이름이 비어 있는 경우 멤버를 숨깁니다.|  
|*ParentName*|멤버의 이름이 부모와 동일한 경우 멤버를 숨깁니다.|  
  
## <a name="remarks"></a>주의  
 에 대 한 허용된 된 값에 해당 하는 열거형 **HideMemberIf** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.HideIfValue>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
