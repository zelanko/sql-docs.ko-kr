---
title: "ADO MD DrilledDown 속성 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- DrilledDown
- Member::DrilledDown
helpviewer_keywords:
- DrilledDown property [ADO MD]
ms.assetid: bf39dd36-fc7a-4f6e-86c0-fa71430c0d86
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8dfa880e78bdeccf722723a7d05f2f0ca1938ed6
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="drilleddown-property-ado-md"></a>ADO MD DrilledDown 속성
자식 즉시 따르는지 여부를 나타냅니다는 [멤버](../../../ado/reference/ado-md-api/member-object-ado-md.md) 축에 있습니다.  
  
## <a name="return-values"></a>반환 값  
 반환 된 **부울** 값 및 읽기 전용입니다. **DrilledDown** 반환 **True** 축에 현재 멤버의 자식 멤버가 없는 경우. **DrilledDown** 반환 **False** 현재 멤버 축에 하나 이상의 자식 멤버의 경우.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **DrilledDown** 속성을이 멤버 바로 뒤에 축이 멤버에 자식이 하나 이상 있는지 여부를 확인 합니다. 이 정보는 구성원을 표시할 때 유용 합니다.  
  
 이 속성은 에서만 지원 [멤버](../../../ado/reference/ado-md-api/member-object-ado-md.md) 에 속하는 개체는 [위치](../../../ado/reference/ado-md-api/position-object-ado-md.md) 개체입니다. 이 속성에서 참조 되는 동안 오류가 발생 **멤버** 에 속하는 개체는 [수준](../../../ado/reference/ado-md-api/level-object-ado-md.md) 개체입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Member 개체(ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>관련 항목:  
 [ParentSameAsPrev 속성(ADO MD)](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)
