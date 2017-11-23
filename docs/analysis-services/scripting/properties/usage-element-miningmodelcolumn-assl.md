---
title: "Usage 요소 (MiningModelColumn) (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
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
apiname: Usage Element (MiningModelColumn)
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Usage
helpviewer_keywords: Usage element
ms.assetid: 435a857e-37a9-434e-9de1-354f1ff2993f
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0e463c7b1c4410cdf134509d3afb2b3410f652db
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="usage-element-miningmodelcolumn-assl"></a>Usage 요소(MiningModelColumn)(ASSL)
  설명 어떻게 부모에 연결 된 열 [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) 사용 됩니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MiningModelColumn>  
   ...  
   <Usage>...</Usage>  
   ...  
</MiningModelColumn>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*키*|열이 키 열입니다.|  
|*입력*|열이 입력 열입니다.|  
|*Predict*|열이 예측 열입니다.|  
|*PredictOnly*|열이 예측 열 전용입니다.|  
|*없음*|열이 모델에서 사용되지 않습니다.<br /><br /> **\*\*경고 \* \***  Usage 값은 "None", Analysis Services 보내지 않습니다 값 서버에 기본적으로, 따라서 사용 특성은 요청/응답에 포함 되지 않습니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **사용량** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.MiningModelColumnUsages>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
