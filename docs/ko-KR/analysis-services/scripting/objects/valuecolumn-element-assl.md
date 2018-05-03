---
title: ValueColumn 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- ValueColumn Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- ValueColumn element
ms.assetid: 6c2d6822-8ecc-46df-9fa9-bb92ac716c36
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 62910949b84918fbf7e00d351ab3e23f33517a28
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="valuecolumn-element-assl"></a>ValueColumn 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  부모 요소의 값을 제공하는 열을 식별합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <ValueColumn xsi:type="DataItem">...</ValueColumn>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|기본값|Varies(주의 참조)|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 경우는 [l u m n](../../../analysis-services/scripting/objects/namecolumn-element-assl.md) 요소의 **DimensionAttribute** 지정 된 동일한 **DataItem** 값에 대 한 기본값 사용는 **ValueColumn** 요소입니다. 경우는 **l u m n** 요소의 **DimensionAttribute** 지정 하지 않으면 및 [KeyColumns](../../../analysis-services/scripting/collections/keycolumns-element-assl.md) 컬렉션 **DimensionAttribute** 포함 하는 하나의 [KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md) 같은 문자열 데이터 형식의 키 열을 나타내는 요소 **DataItem** 값에 대 한 기본값 사용는 **ValueColumn** 요소입니다.  
  
 에 대 한 자세한 내용은 **DataItem** 테이블의 Analysis Services Scripting Language (ASSL) 개체 및 속성을 포함 하 여는 **DataItem** 입력을 참조 하십시오. [DataItem 데이터 형식 & #40; ASSL & #41; ](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md).  
  
 부모에 해당 하는 요소 **l u m n** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.DimensionAttribute> 및 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [개체 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
