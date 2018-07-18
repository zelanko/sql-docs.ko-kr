---
title: MiningModelColumn 데이터 형식 (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 235f0a2e6b00cf96f96546e217830c9c5671f97c
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38007255"
---
# <a name="miningmodelcolumn-data-type-assl"></a>MiningModelColumn 데이터 형식(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  열에 대 한 정보를 나타내는 기본 데이터 형식을 정의 [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MiningModelColumn>  
      <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</<Description>  
      <SourceColumnID>...</SourceColumnID>  
            <Usage>...</Usage>  
            <Translations>...</Translations>  
      <Columns>...</Columns>  
      <ModelingFlags>...</ModelingFlags>  
      <Annotations>...</Annotations>  
</MiningModelColumn>  
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
|자식 요소|[주석을](../../../analysis-services/scripting/collections/annotations-element-assl.md), [열](../../../analysis-services/scripting/collections/columns-element-assl.md)를 [설명](../../../analysis-services/scripting/properties/description-element-assl.md)를 [ID](../../../analysis-services/scripting/properties/id-element-assl.md)를 [ModelingFlags](../../../analysis-services/scripting/collections/modelingflags-element-assl.md)를 [이름](../../../analysis-services/scripting/properties/name-element-assl.md) 를 [SourceColumnID](../../../analysis-services/scripting/properties/sourcecolumnid-element-assl.md)하십시오 [번역](../../../analysis-services/scripting/collections/translations-element-assl.md), [사용](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md)|  
|파생 요소|[열](../../../analysis-services/scripting/objects/column-element-assl.md) ([열](../../../analysis-services/scripting/collections/columns-element-assl.md), 컬렉션 [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.MiningModelColumn>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Scripting Language XML 데이터 형식 &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
