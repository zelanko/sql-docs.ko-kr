---
title: ServerProperty 요소 (ASSL) | Microsoft Docs
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
- ServerProperty Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- SERVERPROPERTY
helpviewer_keywords:
- ServerProperty element
ms.assetid: f152a1b5-0972-40d8-907f-f131c2a108bb
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 6cb62681b0c25c83d54076a67a37addc764102da
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080943"
---
# <a name="serverproperty-element-assl"></a>ServerProperty 요소(ASSL)
  와 연결 된 서버 속성을 정의 [서버](server-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ServerProperties>  
   <ServerProperty>  
      <Name>...</Name>  
      <Value>...</Value>  
            <RequiresRestart>...</RequiresRestart>  
            <PendingValue>...</PendingValue>  
      <DefaultValue>...</DefaultValue>  
      <DisplayFlag>...</DisplayFlag>  
   </ServerProperty>  
</ServerProperties>  
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
|부모 요소|[ServerProperties](../collections/serverproperties-element-assl.md)|  
|자식 요소|[DefaultValue](../properties/value-element-assl.md), [DisplayFlag](../properties/displayflag-element-assl.md), [이름](../properties/name-element-assl.md), [PendingValue](../properties/pendingvalue-element-assl.md), [RequiresRestart](../properties/requiresrestart-element-assl.md), [값](../properties/value-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 `ServerProperty` 데이터와의 인스턴스와 연결 된 서버 속성에 대 한 메타 데이터 요소 설명 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다. ASSL(Analysis Services Scripting Language)의 다른 컬렉션에 포함된 요소와는 달리 `ServerProperty` 요소에서는 명시적으로 명명된 요소 대신 이름/값 쌍을 사용하여 서버 속성을 설명합니다. 이름/값 쌍은 유연성과 확장성을 제공합니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.ServerProperty>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [서버 요소 &#40;ASSL&#41;](server-element-assl.md)   
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  