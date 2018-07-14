---
title: PendingValue 요소 (ASSL) | Microsoft Docs
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
- PendingValue Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- PendingValue
helpviewer_keywords:
- PendingValue element
ms.assetid: 386b2ec6-3d83-42d2-b83a-83e375fbdcbd
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ef24ae229f879adc15fa9f2ecfd8cb10a19d09ff
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37263399"
---
# <a name="pendingvalue-element-assl"></a>PendingValue 요소(ASSL)
  연결된 된 보류 중인 읽기 전용 포함 [ServerProperty](../objects/serverproperty-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ServerProperty>  
   ...  
   <PendingValue>...</PendingValue>  
   ...  
</ServerProperty>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|모든 simpleType|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ServerProperty](../objects/serverproperty-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 이 요소는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]의 현재 인스턴스를 다음에 시작할 때 사용할 `ServerProperty` 값을 포함합니다. 일반적으로 이 값은 서버 속성에 대한 값이 저장된 위치(초기화 파일, [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 레지스트리 또는 다른 저장 메커니즘)에서 검색됩니다.  
  
 부모에 해당 하는 요소가 `PendingValue` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ServerProperty>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ServerProperties 요소 &#40;ASSL&#41;](../collections/serverproperties-element-assl.md)   
 [Server 요소 &#40;ASSL&#41;](../objects/server-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
