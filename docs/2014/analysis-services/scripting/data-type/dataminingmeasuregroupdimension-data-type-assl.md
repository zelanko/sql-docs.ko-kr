---
title: DataMiningMeasureGroupDimension 데이터 형식 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DataMiningMeasureGroupDimension Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DataMiningMeasureGroupDimension
helpviewer_keywords:
- DataMiningMeasureGroupDimension data type
ms.assetid: 56d5c2ec-7e03-4dc7-a668-c8d598d59e55
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9f92fb25375c3741b06ad873ac5f9facd6585570
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48171833"
---
# <a name="dataminingmeasuregroupdimension-data-type-assl"></a>DataMiningMeasureGroupDimension 데이터 형식(ASSL)
  측정값 그룹과 데이터 마이닝 차원 간의 관계를 나타내는 파생 데이터 형식을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DataMiningMeasureGroupDimension>  
   <!-- The following elements extend MeasureGroupDimension -->  
      <CaseCubeDimensionID>...</CaseCubeDimensionID>  
</DataMiningMeasureGroupDimension>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|[MeasureGroupDimension](dimension-data-type-assl.md)|  
|파생 데이터 형식|없음|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[CaseCubeDimensionID](../properties/id-element-assl.md)|  
|파생 요소|참조 [차원](../objects/dimension-element-assl.md) ([차원](../collections/dimensions-element-assl.md) 모음인 [MeasureGroup](../objects/group-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.DataMiningMeasureGroupDimension>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Scripting Language XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
