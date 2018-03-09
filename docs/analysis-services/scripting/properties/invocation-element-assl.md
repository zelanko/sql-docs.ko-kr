---
title: "Invocation 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Invocation Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Invocation
helpviewer_keywords: Invocation element
ms.assetid: f6bf64ad-ae57-4d46-bf92-1d07a65378bb
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 353e0748236cb721253cb55379456d6bb629650a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="invocation-element-assl"></a>Invocation 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]지정 방법을 [동작](../../../analysis-services/scripting/objects/action-element-assl.md) 를 호출 해야 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Action>  
   ...  
   <Invocation>...</Invocation>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*대화형*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[동작](../../../analysis-services/scripting/objects/action-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>주의  
 동작 호출은 클라이언트 응용 프로그램에 따라 다릅니다. **호출** 요소 하도록 제안 클라이언트 응용 프로그램에 어떻게 작업 처리 해야의 인스턴스를 나타내지 않는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 작업을 호출 하는 방법입니다.  
  
 이 요소의 값은 다음 표에 있는 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*대화형*|사용자가 대화형으로 호출합니다.|  
|*OnOpen*|클라이언트 응용 프로그램이 개체를 열 때 호출됩니다.|  
|*일괄 처리*|일괄 처리 명령으로 호출됩니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **호출** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Action>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
