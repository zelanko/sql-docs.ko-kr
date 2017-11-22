---
title: "AggregationFunction 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: AggregationFunction Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: AggregationFunction
helpviewer_keywords: AggregationFunction element
ms.assetid: 40cfc7f9-1089-45f9-be90-a29770ed9682
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 68f13efcbd341ce11f7529f9396753649099e237
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="aggregationfunction-element-assl"></a>AggregationFunction 요소(ASSL)
  계정 유형에 사용할 집계 함수를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Account>  
   ...  
   <AggregationFunction>...</AggregationFunction>  
   ...  
</Account>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*Sum*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[계정](../../../analysis-services/scripting/objects/account-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*Sum*|측정값이 **Sum** 함수를 사용하여 집계됩니다.|  
|*개수*|측정값이 **Count** 함수를 사용하여 집계됩니다.|  
|*Min*|측정값이 **Min** 함수를 사용하여 집계됩니다.|  
|*Max*|측정값이 **Max** 함수를 사용하여 집계됩니다.|  
|*DistinctCount*|측정값이 **DistinctCount** 함수를 사용하여 집계됩니다.|  
|*없음*|측정값이 집계되지 않습니다.|  
|*AverageOfChildren*|측정값은 자식의 평균을 반환하여 집계됩니다.|  
|*FirstChild*|측정값이 해당 첫 번째 자식 멤버를 반환하여 집계됩니다.|  
|*LastChild*|측정값이 해당 마지막 자식 멤버를 반환하여 집계됩니다.|  
|*FirstNonEmpty*|측정값이 비어 있지 않은 해당 첫 번째 멤버를 반환하여 집계됩니다.|  
|*LastNonEmpty*|측정값이 비어 있지 않은 해당 마지막 멤버를 반환하여 집계됩니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **AggregationFunction** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.AggregationFunction>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Accounts 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/accounts-element-assl.md)   
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
