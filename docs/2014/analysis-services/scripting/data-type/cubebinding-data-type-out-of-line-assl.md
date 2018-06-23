---
title: CubeBinding 데이터 형식 (아웃-아웃오브 라인) (ASSL) | Microsoft Docs
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
- CubeBinding Data Type (out-of-line)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CubeBinding
helpviewer_keywords:
- CubeBinding data type
ms.assetid: 5e1ee8ef-855c-4f3d-ae21-a33360d00d66
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b919e8f28d5cb102268ed3338aa0309e45a738c2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36181181"
---
# <a name="cubebinding-data-type-out-of-line-assl"></a>CubeBinding 데이터 형식(아웃오브 라인)(ASSL)
  간의 관계를 나타내는 기본 데이터 형식을 정의 [큐브](../objects/cube-element-assl.md) 요소와 [DataSource](../objects/datasource-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CubeBinding>  
   <ID>...</ID>  
   <DataSourceID>...</DataSourceID>  
   <DataSource>...</DataSource>  
   <MeasureGroup>...</MeasureGroup>  
</CubeBinding>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|InclusionThresholdSetting|  
|파생 데이터 형식|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|[데이터 원본](../objects/datasource-element-assl.md), [DataSourceID](../properties/id-element-assl.md), [ID](../properties/id-element-assl.md), [MeasureGroup](../objects/group-element-assl.md)|  
|파생 요소|[바인딩](../../xmla/xml-elements-properties/binding-element-xmla.md) ([바인딩](../../xmla/xml-elements-properties/bindings-element-xmla.md) 컬렉션 [프로세스](../../xmla/xml-elements-commands/process-element-xmla.md) 또는 [일괄 처리](../../xmla/xml-elements-commands/batch-element-xmla.md) 명령)|  
  
## <a name="remarks"></a>Remarks  
 아웃오브 라인 바인딩에 대 한 자세한 내용은 참조 하십시오. [데이터 원본 및 바인딩 &#40;SSAS 다차원&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Binding 데이터 형식 &#40;ASSL&#41;](binding-data-type-assl.md)   
 [Analysis Services 스크립팅 언어 XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  