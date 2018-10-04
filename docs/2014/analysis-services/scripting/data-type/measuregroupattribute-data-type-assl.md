---
title: Measuregroupattribute _ 데이터 형식 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MeasureGroupAttribute Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MeasureGroupAttribute
helpviewer_keywords:
- MeasureGroupAttribute data type
ms.assetid: dc7f71e6-3755-4d99-9fcd-5830e10eb653
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 996fdfbec8996d925c67f55f4dd6ad3cf423d0b6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48177813"
---
# <a name="measuregroupattribute-data-type-assl"></a>MeasureGroupAttribute _데이터 형식(ASSL)
  특성과 측정값 그룹 간의 관계를 나타내는 기본 데이터 형식을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MeasureGroupAttribute>  
   <AttributeID>...</AttributeID>  
      <KeyColumns>...</KeyColumns>  
   <Type>...</Type>  
   <Annotations>...</Annotations>  
</MeasureGroupAttribute>  
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
|자식 요소|[주석을](../collections/annotations-element-assl.md), [AttributeID](../properties/id-element-assl.md)합니다 [KeyColumns](../collections/columns-element-assl.md), [형식](../properties/type-element-measuregroupattribute-assl.md)|  
|파생 요소|[특성](../objects/attribute-element-assl.md) ([특성](../collections/attributes-element-assl.md) 모음인 [RegularMeasureGroupDimension](dimension-data-type-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.MeasureGroupAttribute>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Scripting Language XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
