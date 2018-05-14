---
title: StandardAction 데이터 형식 (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 67e1de4dfcc2c87079cb5c2b1158e4374a03d959
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="standardaction-data-type-assl"></a>StandardAction 데이터 형식(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  [DrillThroughAction](../../../analysis-services/scripting/objects/action-element-assl.md) 요소 또는 [ReportAction](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md) 요소 이외의 모든 [Action](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md) 요소를 나타내는 파생 데이터 형식을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<StandardAction>  
   <!-- The following elements extend Action -->  
   <Expression>...</Expression>  
</StandardAction>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|기본 데이터 형식|[작업](../../../analysis-services/scripting/data-type/action-data-type-assl.md)|  
|파생 데이터 형식|없음|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[식](../../../analysis-services/scripting/properties/expression-element-assl.md)|  
|파생 요소|[동작](../../../analysis-services/scripting/objects/action-element-assl.md) ([동작](../../../analysis-services/scripting/collections/actions-element-assl.md) 컬렉션 [큐브](../../../analysis-services/scripting/objects/cube-element-assl.md) 또는 [관점](../../../analysis-services/scripting/objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>주의  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.StandardAction>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [스크립팅 언어 XML 데이터 형식 & #40; analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
