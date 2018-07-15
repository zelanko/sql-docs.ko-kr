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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9c6af3d46fac2b6ed02ff4cd261a8f5361d466ae
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37300933"
---
# <a name="serverproperty-element-assl"></a>ServerProperty 요소(ASSL)
  연결 된 서버 속성을 정의 [Server](server-element-assl.md) 요소입니다.  
  
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
|자식 요소|[DefaultValue](../properties/value-element-assl.md), [DisplayFlag](../properties/displayflag-element-assl.md)를 [이름](../properties/name-element-assl.md)를 [PendingValue](../properties/pendingvalue-element-assl.md)를 [RequiresRestart](../properties/requiresrestart-element-assl.md), [값](../properties/value-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 합니다 `ServerProperty` 요소는 데이터 및 메타 데이터의 인스턴스와 연결 된 서버 속성을 설명 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다. ASSL(Analysis Services Scripting Language)의 다른 컬렉션에 포함된 요소와는 달리 `ServerProperty` 요소에서는 명시적으로 명명된 요소 대신 이름/값 쌍을 사용하여 서버 속성을 설명합니다. 이름/값 쌍은 유연성과 확장성을 제공합니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.ServerProperty>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Server 요소 &#40;ASSL&#41;](server-element-assl.md)   
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  
