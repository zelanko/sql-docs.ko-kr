---
title: MeasureGroupAttributeBinding 데이터 형식 (아웃 아웃오브 라인) (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MeasureGroupAttributeBinding Data Type (out-of-line)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- MeasureGroupAttributeBinding data type
ms.assetid: bfe09a95-4e04-4f93-9389-7dd0b4c8f5e4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 247e96f7994fa076b8641394231b772e80685e32
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48156583"
---
# <a name="measuregroupattributebinding-data-type-out-of-line-assl"></a>MeasureGroupAttributeBinding 데이터 형식(아웃오브 라인)(ASSL)
  측정값 그룹에 포함된 차원에 있는 특성의 아웃오브 라인 바인딩을 나타내는 파생 데이터 형식을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MeasureGroupAttributeBinding>  
   <!-- The following elements extend Binding -->  
   <DatabaseID>...</DatabaseID>  
   <CubeID>...</CubeID>  
   <MeasureGroupID>...</MeasureGroupID>  
   <GranularityAttributeID>...</GranularityAttributeID>  
   <Source>...</Source>  
</MeasureGroupAttributeBinding>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|[바인딩](binding-data-type-assl.md)|  
|파생 데이터 형식|없음|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[CubeID](../properties/id-element-assl.md), [DatabaseID](../../xmla/xml-elements-properties/id-element-xmla.md), [MeasureGroupID](../properties/measuregroupid-element-assl.md)하십시오 [GranularityAttributeID](../properties/attributeid-element-assl.md), [원본](../properties/source-element-binding-assl.md)|  
|파생 요소|[바인딩](../../xmla/xml-elements-properties/binding-element-xmla.md) ([바인딩을](../collections/attributes-element-assl.md) Analysis (XMLA)에 대 한 xml 컬렉션 [일괄 처리](../../xmla/xml-elements-commands/batch-element-xmla.md) 하 고 [프로세스](../../xmla/xml-elements-commands/process-element-xmla.md) 명령)|  
  
## <a name="remarks"></a>Remarks  
 아웃오브 라인 바인딩에 대 한 자세한 내용은 참조 하세요. [데이터 원본 및 바인딩 &#40;SSAS 다차원&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Scripting Language XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
