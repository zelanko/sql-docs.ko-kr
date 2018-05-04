---
title: Member 요소 (CSDLBI) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 1ba225f5-3867-4aae-a519-e3c277688d1e
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 606cba0e1f0a9a6d595c0cf4316a454d4e3464d5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="member-element-csdlbi"></a>Member 요소(CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  멤버 요소는 다른 요소에 대해 기준 역할을 하는 복합 유형입니다.  
  
 이 요소의 특성은 열, 측정값, 탐색 속성, 계층 및 수준에 나타날 수 있습니다.  
  
## <a name="elements-and-attributes"></a>요소 및 특성  
 다음 표에 멤버 요소를 정의하는 특성과 해당 요소가 나와 있습니다.  
  
|이름|필수 여부|설명|  
|----------|-----------------|-----------------|  
|이름||TMember 유형을 구현하여 정의되는 멤버(열, 측정값, 탐색 속성, 계층 또는 수준)에 지정된 이름입니다.|  
|Caption|예|멤버의 표시 이름입니다.|  
|ContextualNameRule|예|멤버를 구분하는 데 사용되는 명명 형식입니다. 이 특성의 내용은 ContextualNameRule 단순 유형에 따라 정의됩니다.|  
|숨김||멤버를 클라이언트에게 숨길지 여부를 나타내는 부울 값입니다.<br /><br /> 기본값은 클라이언트에서 열을 볼 수 있음을 의미하는 false입니다.|  
|ReferenceName||DAX 쿼리에서 멤버를 참조하는 데 사용되는 식별자입니다. 이 특성을 생략하면 필드 이름이 사용됩니다.|  
  
## <a name="contextualnamerule-element"></a>ContextualNameRule 요소  
 멤버를 구분하는 데 사용되는 명명 형식을 정의하는 단순 유형입니다.  
  
|값|Description|  
|-----------|-----------------|  
|없음|특성 이름을 사용합니다.|  
|컨텍스트|들어오는 관계 이름을 사용합니다.|  
|병합|들어오는 관계 이름과 속성 이름을 연결합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [1050-1103을 수준 테이블 형식 개체 모델 호환성을 이해 합니다.](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  
