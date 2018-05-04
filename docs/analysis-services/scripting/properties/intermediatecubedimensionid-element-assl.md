---
title: IntermediateCubeDimensionID 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IntermediateCubeDimensionID Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- IntermediateCubeDimensionID
helpviewer_keywords:
- IntermediateCubeDimensionID element
ms.assetid: 305c0a91-7bc2-4268-ba94-8f19d8c22ca3
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: cb5428d2acb3271a70d9dc006d3929a5045e6987
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="intermediatecubedimensionid-element-assl"></a>IntermediateCubeDimensionID 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  참조 차원을 측정값 그룹에 연결하는 차원 ID를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ReferenceMeasureGroupDimension>  
   ...  
   <IntermediateCubeDimensionID>...</IntermediateCubeDimensionID>  
   ...  
</ReferenceMeasureGroupDimension>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|문자열|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ReferenceMeasureGroupDimension](../../../analysis-services/scripting/data-type/referencemeasuregroupdimension-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 부모에 해당 하는 요소 **IntermediateCubeDimensionID** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ReferenceMeasureGroupDimension>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
