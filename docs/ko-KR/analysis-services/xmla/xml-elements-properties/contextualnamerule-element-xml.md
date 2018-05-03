---
title: ContextualNameRule 요소 (XML) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: eb567ef8-f412-4d34-837a-75e53b88b3ce
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: bfca085e32d314ba9007ea5d1529a849ca39de68
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="contextualnamerule-element-xml"></a>ContextualNameRule 요소(XML)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  특성의 복합 이름을 생성하는 최선의 방법에 힌트를 제공합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<RelationshipEndVisualizationProperties>  
   ...  
   <ContextualNameRule>...</ContextualNameRule>  
   ...  
</RelationshipEndVisualizationProperties>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|-1|  
|카디널리티|0-1: 한 번만 나타나는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[RelationshipEndVisualizationProperties](../../../analysis-services/scripting/data-type/relationshipendvisualizationproperties-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 특성에 대해 명확하게 구분되는 이름을 만드는 방법에 대한 힌트를 클라이언트 응용 프로그램에 제공합니다.  
  
 **ContextualNameRule** 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|Value|Description|  
|-----------|-----------------|  
|*없음*|특성의 이름을 사용합니다.|  
|*컨텍스트*|들어오는 관계의 이름을 사용합니다.|  
|*병합*|응용 프로그램 언어의 규칙에 따라 들어오는 관계의 이름 및 특성 이름을 연결합니다.|  
  
  
