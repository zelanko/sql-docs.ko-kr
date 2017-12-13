---
title: "InstanceSelection 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: InstanceSelection Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords: InstanceSelection element
ms.assetid: 908a2da9-274c-40d2-87dc-4641cb8d77e6
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 539c7259235437b39690f7c5241b63bd0b18a2f7
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="instanceselection-element-assl"></a>InstanceSelection 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]목록에 있는 항목의 예상된 개수에 따라 항목 목록이 방법을 제안 하는 클라이언트 응용 프로그램에 힌트를 표시할지를 제공 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <InstanceSelection>...</InstanceSelection>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*없음*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*없음*|선택 목록을 표시하지 않습니다. 사용자가 직접 값을 입력합니다.|  
|*드롭다운*|항목 수가 드롭다운 목록에 표시할 수 있을 만큼 적습니다.|  
|*목록*|항목 수가 드롭다운 목록에 표시하기에는 너무 많지만 필터링이 필요한 정도는 아닙니다.|  
|*FilteredList*|항목 수가 많아 표시할 항목을 사용자가 필터링해야 합니다.|  
|*MandatoryFilter*|항목 수가 너무 많아 표시 항목을 항상 필터링해야 합니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **InstanceSelection** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.InstanceSelection>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
