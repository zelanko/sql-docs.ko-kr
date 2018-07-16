---
title: LastSchemaUpdate 요소 (ASSL) | Microsoft Docs
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
- LastSchemaUpdate Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- LastSchemaUpdate
helpviewer_keywords:
- LastSchemaUpdate element
ms.assetid: 0634c105-91cc-4882-87be-97ca29a251a6
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 94fe98ca4a898e3cb126dcddcd45f367999b7daf
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37306473"
---
# <a name="lastschemaupdate-element-assl"></a>LastSchemaUpdate 요소(ASSL)
  부모 요소의 읽기 전용 메타데이터 업데이트 타임스탬프를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Assembly> <!-- or one of the elements that are listed in the Element Relationships table -->  
   ...  
   <LastSchemaUpdate>...</LastSchemaUpdate>  
   ...  
</Assembly>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|DateTime|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[어셈블리](../objects/assembly-element-assl.md), [큐브](../objects/cube-element-assl.md)를 [데이터베이스](../objects/database-element-assl.md)를 [DataSource](../objects/datasource-element-assl.md)를 [DataSourceView](../objects/datasourceview-element-assl.md), [차원](../objects/dimension-element-assl.md), [MdxScript](../objects/mdxscript-element-assl.md)를 [MeasureGroup](../objects/group-element-assl.md)를 [MiningModel](../objects/miningmodel-element-assl.md)를 [MiningStructure](../objects/miningstructure-element-assl.md), [파티션](../objects/partition-element-assl.md)하십시오 [권한을](../data-type/permission-data-type-assl.md), [관점](../objects/perspective-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `LastSchemaUpdate` 요소는 개체의 메타데이터가 지정된 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에서 변경된 날짜 및 시간을 나타내는 읽기 전용 `DateTime` 값을 포함합니다.  
  
 부모에 해당 하는 요소 `LastSchemaUpdate` Analysis Management Objects (AMO) 개체 모델 <xref:Microsoft.AnalysisServices.Assembly>, <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.Database>를 <xref:Microsoft.AnalysisServices.DataSource>를 <xref:Microsoft.AnalysisServices.DataSourceView>, <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.MdxScript>, <xref:Microsoft.AnalysisServices.MeasureGroup>, <xref:Microsoft.AnalysisServices.MiningModel>, <xref:Microsoft.AnalysisServices.MiningStructure>, <xref:Microsoft.AnalysisServices.Partition>합니다 <xref:Microsoft.AnalysisServices.Permission>, 및 <xref:Microsoft.AnalysisServices.Perspective>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
