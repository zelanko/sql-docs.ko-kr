---
title: BaseProperty 요소 (CSDLBI) | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fd4720036bfefd243a7e48ac0b7cf45a1950a597
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/08/2018
---
# <a name="baseproperty-element-csdlbi"></a>BaseProperty 요소(CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  BaseProperty 요소는 다른 요소에 대해 기준 역할을 하는 복합 유형입니다.  
  
 이 요소의 특성은 열과 측정값에 나타날 수 있습니다.  
  
## <a name="elements-and-attributes"></a>요소 및 특성  
 다음 표는 BaseProperty 요소를 정의하는 특성과 해당 요소를 보여 줍니다.  
  
|이름|필수 여부|설명|  
|----------|-----------------|-----------------|  
|맞춤|아니요|Member 유형의 구현을 통해 정의되는 멤버(열, 측정값, 탐색 속성, 계층 또는 수준)에 지정된 이름입니다.|  
|FormatString|아니요|멤버의 표시 이름입니다.|  
|IsRightToLeft|아니요|오른쪽에서 왼쪽으로 읽을 수 있는 텍스트가 필드에 포함되는지 여부를 나타내는 부울 값입니다.<br /><br /> 이 특성이 생략된 경우 모델의 기본 설정이 사용됩니다.|  
|SortDirection|아니요|필드 값이 일반적으로 정렬되는 방법을 나타내는 값입니다. 이 특성의 내용은 SortDirection 단순 유형에 따라 정의됩니다.<br /><br /> 이 특성을 생략하면 필드의 데이터 형식을 기반으로 정렬 방향이 지정됩니다.|  
|단위|아니요|단위를 표현하기 위해 필드 값에 적용되는 기호입니다.<br /><br /> 이 특성을 생략하면 단위를 알 수 없습니다.|  
  
## <a name="alignment-element"></a>Alignment 요소  
 멤버를 구분하는 데 사용되는 명명 형식을 정의하는 단순 유형입니다.  
  
|값|Description|  
|-----------|-----------------|  
|없음|특성 이름을 사용합니다.|  
|컨텍스트|들어오는 관계 이름을 사용합니다.|  
|병합|현재 문법의 규칙에 따라 들어오는 관계 이름과 속성 이름을 연결합니다.|  
  
## <a name="sortdirection-element"></a>SortDirection 요소  
 멤버를 구분하는 데 사용되는 명명 형식을 정의하는 단순 유형입니다.  
  
|값|Description|  
|-----------|-----------------|  
|없음|특성 이름을 사용합니다.|  
|컨텍스트|들어오는 관계 이름을 사용합니다.|  
|병합|들어오는 관계 이름과 속성 이름을 연결합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [1050-1103을 수준 테이블 형식 개체 모델 호환성을 이해 합니다.](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  
