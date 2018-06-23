---
title: Source 요소 (ComAssembly) (ASSL) | Microsoft Docs
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
- Source Element (ComAssembly)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Source
helpviewer_keywords:
- Source element
ms.assetid: 5c9209e8-ace6-4688-a64d-4987a7648ab9
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ae014f12e15dd27957ab77eb03720457f3c99b28
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36180952"
---
# <a name="source-element-comassembly-assl"></a>Source 요소(ComAssembly)(ASSL)
  COM(구성 요소 개체 모델) 구성 요소의 파일 이름 또는 ProgID(프로그래밍 식별자)를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ComAssembly>  
   ...  
   <Source>...</Source>  
   ...  
</ComAssembly>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ComAssembly](../data-type/assembly-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 부모에 해당 하는 요소 `Source` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ComAssembly>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Assembly 요소 &#40;ASSL&#41;](../objects/assembly-element-assl.md)   
 [ClrAssembly 데이터 형식 &#40;ASSL&#41;](../data-type/clrassembly-data-type-assl.md)   
 [Assemblies 요소 &#40;ASSL&#41;](../collections/assemblies-element-assl.md)   
 [Database 요소 &#40;ASSL&#41;](../objects/database-element-assl.md)   
 [서버 요소 &#40;ASSL&#41;](../objects/server-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  