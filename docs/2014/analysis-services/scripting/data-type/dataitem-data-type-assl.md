---
title: DataItem 데이터 형식 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DataItem Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DataItem
helpviewer_keywords:
- DataItem data type
ms.assetid: f4f5155f-9c3d-49a1-a390-a9c734fafbce
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9f16c23941fc1048429ced974b88bba378bc72c2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48153483"
---
# <a name="dataitem-data-type-assl"></a>DataItem 데이터 형식(ASSL)
  열 또는 특성과 같은 데이터 항목의 데이터 관련 특성을 나타내는 기본 데이터 형식을 정의합니다.  
  
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
|기본 데이터 형식|없음|  
|파생 데이터 형식|없음|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[Annotations](../collections/annotations-element-assl.md), [Collation](../properties/collation-element-assl.md), [DataSize](../properties/datasize-element-assl.md), [DataType](../properties/datatype-element-assl.md), [Format](../properties/format-element-assl.md), [InvalidXmlCharacters](../properties/invalidxmlcharacters-element-assl.md), [MimeType](../properties/mimetype-element-assl.md), [NullProcessing](../properties/nullprocessing-element-assl.md), [Source](../properties/source-element-binding-assl.md), [Trimming](../properties/trimming-element-assl.md)|  
|파생 요소|주의에 있는 표를 참조하십시오.|  
  
## <a name="remarks"></a>Remarks  
 `DataItem` 데이터 형식은 측정값, 특성 키 및 특성 이름과 같은 바인딩할 수 있는 모든 데이터 항목에 사용됩니다. 관련된 세부 사항 및 적용되는 기본값은 사용 방식에 따라 달라집니다. 예를 들어 특성 이름은 문자열이어야 합니다.  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에서는 특정 데이터 형식 집합만 허용합니다. 다른 데이터 형식을 사용하면 해당 형식이 유효한 형식으로 암시적으로 변환되지 않고 오류가 발생합니다.  
  
 다음 표에서는 `DataItem` 형식의 요소를 나열합니다.  
  
|부모 요소|`DataItem` 형식의 요소|주석|  
|--------------------|----------------------------------|--------------|  
|[AttributeTranslation](../objects/column-element-assl.md)|`Source` 요소를 `DataItem` 형식 이어야 합니다 [ColumnBinding](binding-data-type-assl.md) 또는 [AttributeBinding](attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../objects/customrollupcolumn-element-assl.md)|`Source` 요소를 `DataItem` 형식 이어야 합니다 [ColumnBinding](binding-data-type-assl.md) 또는 [AttributeBinding](attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../objects/customrolluppropertiescolumn-element-assl.md)|`Source` 요소를 `DataItem` 형식 이어야 합니다 [ColumnBinding](binding-data-type-assl.md) 또는 [AttributeBinding](attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../objects/keycolumn-element-assl.md)|`Source` 요소를 `DataItem` 형식 이어야 합니다 [ColumnBinding](binding-data-type-assl.md)하십시오 [AttributeBinding](attributebinding-data-type-assl.md) 또는 [TimeBinding](timebinding-data-type-assl.md)|  
|[DimensionAttribute](../objects/namecolumn-element-assl.md)|`Source` 요소를 `DataItem` 형식 이어야 합니다 [ColumnBinding](binding-data-type-assl.md) 또는 [AttributeBinding](attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../objects/skippedlevelscolumn-element-assl.md)|`Source` 요소를 `DataItem` 형식 이어야 합니다 [ColumnBinding](binding-data-type-assl.md) 또는 [AttributeBinding](attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../objects/unaryoperatorcolumn-element-assl.md)|`Source` 요소를 `DataItem` 형식 이어야 합니다 [ColumnBinding](binding-data-type-assl.md) 또는 [AttributeBinding](attributebinding-data-type-assl.md)|  
|[측정값](../objects/measure-element-assl.md)|[원본](../properties/source-element-binding-assl.md)|`Source` 요소를 `DataItem` 형식 이어야 합니다 [RowBinding](rowbinding-data-type-assl.md)를 [ColumnBinding](binding-data-type-assl.md)를 [MeasureBinding](measurebinding-data-type-assl.md), 또는 [CubeDimensionBinding](dimensionbinding-data-type-assl.md)|  
|[MeasureGroupAttribute](measuregroupattribute-data-type-assl.md)|[KeyColumn](../objects/keycolumn-element-assl.md)|`Source` 요소를 `DataItem` 형식 이어야 합니다 [ColumnBinding](binding-data-type-assl.md)하십시오 [AttributeBinding](attributebinding-data-type-assl.md) 또는 [InheritedBinding](inheritedbinding-data-type-assl.md)|  
|[ScalarMiningStructureColumn](miningstructurecolumn-data-type-assl.md)|[KeyColumn](../objects/keycolumn-element-assl.md)|`Source` 요소를 `DataItem` 형식 이어야 합니다 [ColumnBinding](binding-data-type-assl.md)|  
|[ScalarMiningStructureColumn](miningstructurecolumn-data-type-assl.md)|[NameColumn](../objects/namecolumn-element-assl.md)|`Source` 요소를 `DataItem` 형식 이어야 합니다 [ColumnBinding](binding-data-type-assl.md)|  
|[TableMiningStructureColumn](../objects/foreignkeycolumn-element-assl.md)|`Source` 요소를 `DataItem` 형식 이어야 합니다 [ColumnBinding](binding-data-type-assl.md)|  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.DataItem>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Scripting Language XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
