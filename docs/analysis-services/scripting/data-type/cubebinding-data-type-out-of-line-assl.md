---
title: "CubeBinding 데이터 형식 (아웃-아웃오브 라인) (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- CubeBinding Data Type (out-of-line)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- CubeBinding
helpviewer_keywords:
- CubeBinding data type
ms.assetid: 5e1ee8ef-855c-4f3d-ae21-a33360d00d66
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c0624bd051d8534e82b608bc925236abc0153798
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="cubebinding-data-type-out-of-line-assl"></a>CubeBinding 데이터 형식(아웃오브 라인)(ASSL)
  간의 관계를 나타내는 기본 데이터 형식을 정의 [큐브](../../../analysis-services/scripting/objects/cube-element-assl.md) 요소와 [DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md) 요소입니다.  
  
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
  
|특징|설명|  
|--------------------|-----------------|  
|기본 데이터 형식|없음|  
|파생 데이터 형식|없음|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[데이터 원본](../../../analysis-services/scripting/objects/datasource-element-assl.md), [DataSourceID](../../../analysis-services/scripting/properties/datasourceid-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|  
|파생 요소|[바인딩](../../../analysis-services/xmla/xml-elements-properties/binding-element-xmla.md) ([바인딩](../../../analysis-services/xmla/xml-elements-properties/bindings-element-xmla.md) 컬렉션 [프로세스](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md) 또는 [일괄 처리](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) 명령)|  
  
## <a name="remarks"></a>주의  
 아웃오브 라인 바인딩에 대 한 자세한 내용은 참조 하십시오. [데이터 원본 및 바인딩 &#40; SSAS 다차원 &#41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>관련 항목:  
 [Binding 데이터 형식 &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)   
 [스크립팅 언어 XML 데이터 형식 &#40; analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

