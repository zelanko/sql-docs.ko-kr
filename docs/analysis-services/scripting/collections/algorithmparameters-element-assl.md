---
title: "AlgorithmParameters 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- AlgorithmParameters Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- AlgorithmParameters
helpviewer_keywords:
- AlgorithmParameters element
ms.assetid: 240cbb60-7fa3-46ef-b5be-cd14c9ec10de
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4865e23f02c681586f9025737dd2acc21ccd93bf
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="algorithmparameters-element-assl"></a>AlgorithmParameters 요소(ASSL)
  사용 하는 알고리즘에 대 한 매개 변수 컬렉션을 포함 한 [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MiningModel>  
   ...  
   <AlgorithmParameters>  
      <AlgorithmParameter>...</AlgorithmParameter>  
   </AlgorithmParameters>  
   ...  
</MiningModel>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음(컬렉션)|  
|기본값|없음(컬렉션)|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)|  
|자식 요소|[AlgorithmParameter](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md)|  
  
## <a name="remarks"></a>주의  
 **AlgorithmParameters** 컬렉션에는 마이닝 모델 알고리즘에 대한 확장 가능한 매개 변수 집합이 이름/값 쌍으로 포함되어 있습니다. 해당되는 매개 변수 집합은 알고리즘에 따라 다릅니다. 특정 알고리즘의 알고리즘 매개 변수에 대한 자세한 내용은 해당 알고리즘에 대한 적절한 설명서를 참조하십시오.  
  
 유효성 검사 및 표시 정보 등 사용 가능한 알고리즘 매개 변수는 DMSCHEMA_MINING_SERVICE_PARAMETERS 스키마 행 집합에서 검색할 수 있습니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.AlgorithmParameterCollection>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Algorithm 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/algorithm-element-assl.md)   
 [DMSCHEMA_MINING_SERVICE_PARAMETERS 행 집합](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-service-parameters-rowset.md)   
 [컬렉션 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
