---
title: DrilledDown 속성 (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DrilledDown
- Member::DrilledDown
helpviewer_keywords:
- DrilledDown property [ADO MD]
ms.assetid: bf39dd36-fc7a-4f6e-86c0-fa71430c0d86
author: rothja
ms.author: jroth
ms.openlocfilehash: c5819609f06b37ffad08918968530b66df169c64
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764264"
---
# <a name="drilleddown-property-ado-md"></a>DrilledDown 속성(ADO MD)
자식이 축의 [멤버](../../../ado/reference/ado-md-api/member-object-ado-md.md) 바로 뒤에 있는지 여부를 나타냅니다.  
  
## <a name="return-values"></a>반환 값  
 **부울** 값을 반환 하며 읽기 전용입니다. **DrilledDown** 은 축에 현재 멤버의 자식 멤버가 없는 경우 **True** 를 반환 합니다. 현재 멤버가 축에 하나 이상의 자식 멤버를 포함 하는 경우 **DrilledDown** 는 **False** 를 반환 합니다.  
  
## <a name="remarks"></a>설명  
 **DrilledDown** 속성을 사용 하 여이 멤버 바로 뒤에 오는 축에이 멤버의 자식이 하나 이상 있는지 여부를 확인 합니다. 이 정보는 멤버를 표시 하는 경우에 유용 합니다.  
  
 이 속성은 [Position](../../../ado/reference/ado-md-api/position-object-ado-md.md) 개체에 속하는 [멤버](../../../ado/reference/ado-md-api/member-object-ado-md.md) 개체에 대해서만 지원 됩니다. [수준](../../../ado/reference/ado-md-api/level-object-ado-md.md) 개체에 속한 **멤버** 개체에서이 속성을 참조 하는 경우 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Member 개체(ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>참고 항목  
 [ParentSameAsPrev 속성(ADO MD)](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)
