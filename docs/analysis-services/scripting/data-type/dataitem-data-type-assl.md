---
title: DataItem 데이터 형식 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DataItem Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DataItem
helpviewer_keywords:
- DataItem data type
ms.assetid: f4f5155f-9c3d-49a1-a390-a9c734fafbce
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ec40eca06225eef5d9c7e505e4fe2c9dee6972b1
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="dataitem-data-type-assl"></a>DataItem 데이터 형식(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]데이터 항목에 열 또는 특성 등의 데이터와 관련 된 특성을 나타내는 기본 데이터 형식을 정의 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DataItem>  
   <DataType>...</DataType>  
   <DataSize>...</DataSize>  
   <MimeType>...</MimeType>  
   <NullProcessing>...</NullProcessing>  
   <Trimming>...</Trimming>  
   <InvalidXmlCharacters>...</InvalidXmlCharacters>  
      <Collation>...</Collation>  
   <Format>...</Format>  
   <Source>...</Source>  
   <Annotations>...</Annotations>  
</DataItem>  
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
|자식 요소|[Annotations](../../../analysis-services/scripting/collections/annotations-element-assl.md), [Collation](../../../analysis-services/scripting/properties/collation-element-assl.md), [DataSize](../../../analysis-services/scripting/properties/datasize-element-assl.md), [DataType](../../../analysis-services/scripting/properties/datatype-element-assl.md), [Format](../../../analysis-services/scripting/properties/format-element-assl.md), [InvalidXmlCharacters](../../../analysis-services/scripting/properties/invalidxmlcharacters-element-assl.md), [MimeType](../../../analysis-services/scripting/properties/mimetype-element-assl.md), [NullProcessing](../../../analysis-services/scripting/properties/nullprocessing-element-assl.md), [Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md), [Trimming](../../../analysis-services/scripting/properties/trimming-element-assl.md)|  
|파생 요소|주의에 있는 표를 참조하십시오.|  
  
## <a name="remarks"></a>주의  
 **DataItem** 데이터 형식은 측정값, 특성 키 및 특성 이름과 같은 바인딩할 수 있는 모든 데이터 항목에 사용됩니다. 관련된 세부 사항 및 적용되는 기본값은 사용 방식에 따라 달라집니다. 예를 들어 특성 이름은 문자열이어야 합니다.  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에서는 특정 데이터 형식 집합만 허용합니다. 다른 데이터 형식을 사용하면 해당 형식이 유효한 형식으로 암시적으로 변환되지 않고 오류가 발생합니다.  
  
 다음 표에서는 **DataItem**유형의 요소를 나열합니다.  
  
|부모 요소|**DataItem**유형의 요소|주석|  
|--------------------|----------------------------------|--------------|  
|[AttributeTranslation](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md)|[CaptionColumn](../../../analysis-services/scripting/objects/captioncolumn-element-assl.md)|**Source** 의 **DataItem** 요소는 [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md) 또는 [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[CustomRollupColumn](../../../analysis-services/scripting/objects/customrollupcolumn-element-assl.md)|**Source** 의 **DataItem** 요소는 [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md) 또는 [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[CustomRollupPropertiesColumn](../../../analysis-services/scripting/objects/customrolluppropertiescolumn-element-assl.md)|**Source** 의 **DataItem** 요소는 [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md) 또는 [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)|**Source** 의 **DataItem** 요소는 [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md), [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md) 또는 [TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[L u m n](../../../analysis-services/scripting/objects/namecolumn-element-assl.md)|**Source** 의 **DataItem** 요소는 [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md) 또는 [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[SkippedLevelsColumn](../../../analysis-services/scripting/objects/skippedlevelscolumn-element-assl.md)|**Source** 의 **DataItem** 요소는 [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md) 또는 [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[UnaryOperatorColumn](../../../analysis-services/scripting/objects/unaryoperatorcolumn-element-assl.md)|**Source** 의 **DataItem** 요소는 [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md) 또는 [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)|  
|[측정값](../../../analysis-services/scripting/objects/measure-element-assl.md)|[원본](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|**Source** 의 **DataItem** 요소는 [RowBinding](../../../analysis-services/scripting/data-type/rowbinding-data-type-assl.md), [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md), [MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)또는 [CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md)|  
|[MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)|[KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)|**Source** 의 **DataItem** 요소는 [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md), [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md) 또는 [InheritedBinding](../../../analysis-services/scripting/data-type/inheritedbinding-data-type-assl.md)|  
|[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|[KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)|**Source** 의 **DataItem** 요소는 [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)|  
|[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|[L u m n](../../../analysis-services/scripting/objects/namecolumn-element-assl.md)|**Source** 의 **DataItem** 요소는 [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)|  
|[TableMiningStructureColumn](../../../analysis-services/scripting/data-type/tableminingstructurecolumn-data-type-assl.md)|[ForeignKeyColumn](../../../analysis-services/scripting/objects/foreignkeycolumn-element-assl.md)|**Source** 의 **DataItem** 요소는 [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)|  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.DataItem>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [스크립팅 언어 XML 데이터 형식 &#40; analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
