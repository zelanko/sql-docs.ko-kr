---
title: MemberUniqueNameStyle 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MemberUniqueNameStyle Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- MemberUniqueNameStyle element
ms.assetid: f0771c81-0127-4203-9501-ae4f864730fa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 204f29e7bfb90894fded974b78cfd136aa39eaeb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48133463"
---
# <a name="memberuniquenamestyle-element-assl"></a>MemberUniqueNameStyle 요소(ASSL)
  어떻게 고유한 이름을 결정에 포함 된 계층의 멤버에 대해 생성 되는 [CubeDimension](../data-type/dimension-data-type-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CubeDimension>  
   ...  
   <MemberUniqueNameStyle>...</MemberUniqueNameStyle>  
   ...  
</CubeDimension>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*네이티브*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CubeDimension](../data-type/dimension-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*네이티브*|인스턴스에서 자동으로 멤버의 고유한 이름을 결정합니다.|  
|*NamePath*|인스턴스에서 각 수준과 멤버의 캡션으로 구성된 복합 이름을 생성합니다.|  
  
## <a name="remarks"></a>Remarks  
 부모에 해당 하는 요소가 `MemberUniqueNameStyle` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.CubeDimension>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [큐브 요소 &#40;ASSL&#41;](../objects/cube-element-assl.md)   
 [차원 요소 &#40;ASSL&#41;](../objects/dimension-element-assl.md)   
 [CubeDimension 데이터 형식 &#40;ASSL&#41;](../data-type/dimension-data-type-assl.md)  
  
  
