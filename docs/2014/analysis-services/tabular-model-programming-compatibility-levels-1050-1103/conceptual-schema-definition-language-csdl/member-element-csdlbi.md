---
title: Member 요소 (CSDLBI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 1ba225f5-3867-4aae-a519-e3c277688d1e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f193cb746b8df43c33aa65ea3d69d87ab7c36655
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48218833"
---
# <a name="member-element-csdlbi"></a>Member 요소(CSDLBI)
  멤버 요소는 다른 요소에 대해 기준 역할을 하는 복합 유형입니다.  
  
 이 요소의 특성은 열, 측정값, 탐색 속성, 계층 및 수준에 나타날 수 있습니다.  
  
## <a name="elements-and-attributes"></a>요소 및 특성  
 다음 표에 멤버 요소를 정의하는 특성과 해당 요소가 나와 있습니다.  
  
|이름|필수 여부|Description|  
|----------|-----------------|-----------------|  
|이름||TMember 유형을 구현하여 정의되는 멤버(열, 측정값, 탐색 속성, 계층 또는 수준)에 지정된 이름입니다.|  
|Caption|사용자 계정 컨트롤|멤버의 표시 이름입니다.|  
|ContextualNameRule|사용자 계정 컨트롤|멤버를 구분하는 데 사용되는 명명 형식입니다. 이 특성의 내용은 ContextualNameRule 단순 유형에 따라 정의됩니다.|  
|숨김||멤버를 클라이언트에게 숨길지 여부를 나타내는 부울 값입니다.<br /><br /> 기본값은 클라이언트에서 열을 볼 수 있음을 의미하는 false입니다.|  
|ReferenceName||DAX 쿼리에서 멤버를 참조하는 데 사용되는 식별자입니다. 이 특성을 생략하면 필드 이름이 사용됩니다.|  
  
## <a name="contextualnamerule-element"></a>ContextualNameRule 요소  
 멤버를 구분하는 데 사용되는 명명 형식을 정의하는 단순 유형입니다.  
  
|값|Description|  
|-----------|-----------------|  
|없음|특성 이름을 사용합니다.|  
|컨텍스트|들어오는 관계 이름을 사용합니다.|  
|병합|들어오는 관계 이름과 속성 이름을 연결합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [테이블 형식 개체 모델 이해](../representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  
