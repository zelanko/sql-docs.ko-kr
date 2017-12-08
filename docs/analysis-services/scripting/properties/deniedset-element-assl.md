---
title: "DeniedSet 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DeniedSet Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: DeniedSet
helpviewer_keywords: DeniedSet element
ms.assetid: 898deefb-822d-458b-96d8-880da287b687
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2a750f409d45a50fca4c7cc5efbdf1240de74f88
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="deniedset-element-assl"></a>DeniedSet 요소(ASSL)
  연관된 특성에 대해 거부된 권한 목록을 정의하는 집합 식을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<AttributePermission>  
      ...  
   <DeniedSet>...</DeniedSet>  
      ...  
</AttributePermission>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|문자열|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[AttributePermission](../../../analysis-services/scripting/objects/attributepermission-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 부모에 해당 하는 요소 **DeniedSet** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.AttributePermission>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
