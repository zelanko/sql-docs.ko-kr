---
title: 요소 (Partition) (ASSL)를 입력 합니다. | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b7c18bd4363849ee2f56e395acaae492a325b885
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="type-element-partition-assl"></a>Type 요소(Partition)(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  유형을 포함 된 [파티션](../../../analysis-services/scripting/objects/partition-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Partition>  
      ...  
   <Type>...</Type>  
   ...  
</Partition>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*데이터*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[파티션](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*데이터*|파티션이 팩트 테이블 데이터를 포함합니다.|  
|*쓰기 저장*|파티션이 쓰기 저장(writeback) 테이블 데이터를 포함합니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **형식** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.PartitionType>합니다.  
  
 부모에 해당 하는 요소 **형식** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Partition>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
