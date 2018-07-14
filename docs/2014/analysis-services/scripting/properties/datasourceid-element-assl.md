---
title: DataSourceID 요소 (ASSL) | Microsoft Docs
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
- DataSourceID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DataSourceID
helpviewer_keywords:
- DataSourceID element
ms.assetid: 2d71ba53-1684-4da0-8da4-fb75033c971b
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 86a5e07518097e01509f24f2969580dec7ba0c34
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37263589"
---
# <a name="datasourceid-element-assl"></a>DataSourceID 요소(ASSL)
  하 게 식별 하는 [DataSource](../objects/datasource-element-assl.md) 부모 요소와 연결 된 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CubeBinding> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <DataSourceID>...</DataSourceID>  
   ...  
</CubeBinding>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|컨텍스트에 따라 다름|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CubeBinding](../data-type/cubebinding-data-type-out-of-line-assl.md), [CubeDimensionBinding](../data-type/binding-data-type-assl.md)합니다 [DimensionBinding](../data-type/dimensionbinding-data-type-assl.md)를 [MeasureGroupBinding](../data-type/measuregroupbinding-data-type-assl.md)를 [QueryBinding](../data-type/querybinding-data-type-assl.md), [DataSourceView](../objects/datasourceview-element-assl.md), [TableBinding](../data-type/tablebinding-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 AMO(Analysis Management Object) 개체 모델에서 `DataSourceID`의 부모에 해당하는 요소는 <xref:Microsoft.AnalysisServices.CubeDimensionBinding>, <xref:Microsoft.AnalysisServices.DimensionBinding>, <xref:Microsoft.AnalysisServices.MeasureGroupBinding>, <xref:Microsoft.AnalysisServices.QueryBinding>, <xref:Microsoft.AnalysisServices.DataSourceView> 및 <xref:Microsoft.AnalysisServices.TableBinding>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [ID 요소 &#40;ASSL&#41;](id-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
