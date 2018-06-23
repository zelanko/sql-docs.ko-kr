---
title: NamingTemplate 요소 (ASSL) | Microsoft Docs
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
- NamingTemplate Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- NamingTemplate
helpviewer_keywords:
- NamingTemplate element
ms.assetid: d68d765c-f012-40c1-acd4-32741ee2eadf
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: d8eb2589b0b33a0b3268e6104b51c3e3612ad894
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36092489"
---
# <a name="namingtemplate-element-assl"></a>NamingTemplate 요소(ASSL)
  생성 된 부모-자식 계층에서 수준의 이름이 지정 되는 방식을 정의 [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md) 부모 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DimensionAttribute>  
   ...  
      <NamingTemplate>...</NamingTemplate>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 값은 `NamingTemplate` 요소 부모 특성에만 사용 됩니다 (의 값 즉,는 [사용](usage-element-dimensionattribute-assl.md) 의 요소는 `DimensionAttribute` 로 설정 된 부모 *부모*).  
  
 부모 특성을 사용하여 계층을 생성하면 부모 특성에 포함된 멤버 간 부모-자식 관계로 계층 수준이 결정됩니다. 따라서 다른 차원과는 달리 수준 이름은 계층에 사용되는 특성 이름에서 가져올 수 없습니다.  
  
 대신 명명 템플릿을 사용하여 부모-자식 계층의 수준 이름을 생성합니다. 부모 특성에 정의된 `NamingTemplate` 요소는 수준 이름을 정의하는 데 사용되는 문자열 식을 포함합니다. 부모 특성의 명명 템플릿을 정의하는 방법은 두 가지가 있습니다. 명명 패턴을 디자인하거나 이름 목록을 지정하면 됩니다.  
  
 명명 패턴은 각 새 하위 수준의 이름에 삽입되는 증분 카운터의 자리 표시자 문자로 별표(`*`)를 포함합니다. 예를 들어 어떤 수준도 정의되지 않은 경우 `Level *`를 사용하면 수준 이름이 `Level 01`, `Level 02`, `Level 03`과 같이 지정됩니다. 명명 패턴에 자리 표시자 문자가 없으면 첫 번째 수준 이름은 그대로 사용되고 다음 수준 이름은 패턴 끝에 공백과 숫자가 추가되어 지정됩니다. 예를 들어 `Level`을 사용하면 수준 이름이 `Level`, `Level 01`, `Level 02`와 같이 지정됩니다.  
  
 명명 시 특정 이름 집합을 사용하려면 `NamingTemplate` 요소 값을 세미콜론으로 구분된 수준 이름 목록으로 설정합니다. 목록에 있는 각 이름은 다음 수준 이름에 사용됩니다. 수준 개수가 목록의 이름 개수를 초과하면 목록의 마지막 이름이 추가 수준 이름의 템플릿으로 사용되고 이때 앞서 설명한 대로 마지막 이름에 공백과 서수가 추가됩니다. 예를 들어 `Division;Group;Unit`를 사용하면 수준 이름이 `Division`, `Group`, `Unit`, `Unit 01`, `Unit 02`와 같이 지정됩니다. 반대로 `Division;Group;Unit *`를 사용하면 수준 이름이 `Division`, `Group`, `Unit 03`, `Unit 04`와 같이 지정됩니다.  
  
 목록에 있는 각 이름은 템플릿으로 처리되므로 고유한 수준 이름이 지정됩니다. 예를 들어 `Manager;Team Lead;Manager;Team Lead;Worker *`를 사용하면 수준 이름이 `Manager`, `Team Lead`, `Manager 01`, `Team Lead 01`, `Worker 05`, `Worker 06`과 같이 지정됩니다.  
  
 별표를 두 개의 별표 (*)를 사용 하 여 (\*) 명명 템플릿의 일부로 수준 이름에 문자입니다.  
  
 부모에 해당 하는 요소 `NamingTemplate` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.DimensionAttribute>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [NamingTemplateTranslations 요소 &#40;ASSL&#41;](../collections/translations-element-assl.md)   
 [DimensionAttribute 데이터 형식 &#40;ASSL&#41;](../data-type/dimensionattribute-data-type-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  