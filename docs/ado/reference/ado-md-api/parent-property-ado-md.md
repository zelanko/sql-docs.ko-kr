---
title: Parent 속성 (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Parent
- Member::Parent
helpviewer_keywords:
- Parent property [ADO MD]
ms.assetid: 32c278c1-d8e1-4bb7-9ecd-2fbfdffee34b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2f6d6e03dd3288a5b0ca71bb9e129e1a57abf7c8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67949326"
---
# <a name="parent-property-ado-md"></a>Parent 속성(ADO MD)
계층에서 현재 [멤버](../../../ado/reference/ado-md-api/member-object-ado-md.md) 의 부모인 멤버를 나타냅니다.  
  
## <a name="return-values"></a>반환 값  
 는 [멤버](../../../ado/reference/ado-md-api/member-object-ado-md.md) 개체를 반환 하 고 읽기 전용입니다.  
  
## <a name="remarks"></a>설명  
 계층의 최상위 수준에 있는 멤버 (루트)에는 부모가 없습니다. 이 속성은 [수준](../../../ado/reference/ado-md-api/level-object-ado-md.md) 개체에 속한 **멤버** 개체에 대해서만 지원 됩니다. [Position](../../../ado/reference/ado-md-api/position-object-ado-md.md) 개체에 속하는 **멤버** 개체에서이 속성을 참조 하는 경우 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Member 개체(ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>참고 항목  
 [Children 속성(ADO MD)](../../../ado/reference/ado-md-api/children-property-ado-md.md)
