---
title: Level 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Level Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- LEVEL
helpviewer_keywords:
- Level element
ms.assetid: 66ee2c16-d6b8-4dd3-879f-1f2b6923bc43
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b057f53f04003755fecf4f297012559d48c6f09d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48048250"
---
# <a name="level-element-assl"></a>Level 요소(ASSL)
  수준을 정의 [계층](hierarchy-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Levels>  
      <Level>  
      <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</Description>  
      <SourceAttributeID>...</SourceAttributeID>  
      <HideMemberIf>...</HideMemberIf>  
      <Translations>...</Translations>  
      <Annotations>...</Annotations>  
   </Level>  
</Levels>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Levels](../collections/levels-element-assl.md)|  
|자식 요소|[주석을](../collections/annotations-element-assl.md), [설명을](../properties/description-element-assl.md), [HideMemberIf](../properties/hidememberif-element-assl.md)를 [ID](../properties/id-element-assl.md)를 [이름](../properties/name-element-assl.md), [SourceAttributeID](../properties/attributeid-element-assl.md), [번역](../collections/translations-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 이 데이터 형식은 모든 배포 모드(1-다차원 및 데이터 마이닝, 2-SharePoint, 3-테이블 형식)에서 제한되지 않습니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.Level>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  
