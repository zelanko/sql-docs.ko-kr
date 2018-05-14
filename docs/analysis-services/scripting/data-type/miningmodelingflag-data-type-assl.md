---
title: MiningModelingFlag 데이터 형식 (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ffbf5b43efb72e32b49cf70a1a114a4b2c07b3de
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="miningmodelingflag-data-type-assl"></a>MiningModelingFlag 데이터 형식(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  [ModelingFlag](../../../analysis-services/scripting/objects/modelingflag-element-assl.md) 요소에서 사용 가능한 모델링 플래그를 나타내는 기본 데이터 형식을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MiningModelingFlag>...</MiningModelingFlag>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|기본 데이터 형식|String(열거형)|  
|파생 데이터 형식|없음|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|없음|  
|파생 요소|[ModelingFlag](../../../analysis-services/scripting/objects/modelingflag-element-assl.md) ([MiningModelColumn](../../../analysis-services/scripting/collections/modelingflags-element-assl.md) 또는 [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md) 의 [ModelingFlags](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)컬렉션)|  
  
## <a name="remarks"></a>주의  
 플래그 이름은 공백을 포함할 수 있습니다. 기본적으로 지원되는 값은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|*MODEL_EXISTENCE_ONLY*|열이 열 값에 상관없이 누락되거나 누락되지 않은 두 가지 상태로 모델링되어야 합니다. 이는 특히 사례에 값이 희박한 중첩된 테이블의 열에서 유용합니다.|  
|*NOT NULL*|열에 NULL 값이 허용되지 않습니다.|  
|*회귀 변수*|열이 테스트 사례에 대해 회귀자 값을 제공합니다.|  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]인스턴스에 타사 OLE DB 또는 데이터 마이닝 공급자가 집계된 경우 추가 공급자별 플래그를 사용할 수 있습니다.  
  
 AMO(Analysis Management Object) 개체 모델에서 밀접한 관련이 있는 요소는 <xref:Microsoft.AnalysisServices.MiningModelingFlags>입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [스크립팅 언어 XML 데이터 형식 & #40; analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
