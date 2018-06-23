---
title: MiningModelingFlag 데이터 형식 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- MiningModelingFlag Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningModelingFlag
helpviewer_keywords:
- MiningModelingFlag data type
ms.assetid: aaa72ba8-051e-4b01-b1e9-9c8d83b8b752
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 32ee744bdfcd084c4be88511ecba025ca9a270de
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36184144"
---
# <a name="miningmodelingflag-data-type-assl"></a>MiningModelingFlag 데이터 형식(ASSL)
  사용 가능한 모델링 플래그를 나타내는 기본 데이터 형식을 정의 [ModelingFlag](../objects/modelingflag-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MiningModelingFlag>...</MiningModelingFlag>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|String(열거형)|  
|파생 데이터 형식|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|InclusionThresholdSetting|  
|파생 요소|[ModelingFlag](../objects/modelingflag-element-assl.md) ([ModelingFlags](../collections/modelingflags-element-assl.md) 컬렉션 [MiningModelColumn](miningmodelcolumn-data-type-assl.md) 또는 [ScalarMiningStructureColumn](miningstructurecolumn-data-type-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 플래그 이름은 공백을 포함할 수 있습니다. 기본적으로 지원되는 값은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|*MODEL_EXISTENCE_ONLY*|열이 열 값에 상관없이 누락되거나 누락되지 않은 두 가지 상태로 모델링되어야 합니다. 이는 특히 사례에 값이 희박한 중첩된 테이블의 열에서 유용합니다.|  
|*NOT NULL*|열에 NULL 값이 허용되지 않습니다.|  
|*회귀 변수*|열이 테스트 사례에 대해 회귀자 값을 제공합니다.|  
  
 인스턴스에 타사 OLE DB 또는 데이터 마이닝 공급자가 집계 된 경우 추가 공급자별 플래그를 사용할 수 있습니다 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
 AMO(Analysis Management Object) 개체 모델에서 밀접한 관련이 있는 요소는 <xref:Microsoft.AnalysisServices.MiningModelingFlags>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 스크립팅 언어 XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  