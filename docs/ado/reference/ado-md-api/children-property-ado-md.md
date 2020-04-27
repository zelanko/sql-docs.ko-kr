---
title: Children 속성 (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Member::Children
- Children
helpviewer_keywords:
- Children property [ADO MD]
ms.assetid: 61d36468-1ccd-467a-9cb5-17d0bfacc766
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cbec9733044127d23e75364697a41ccd7e8910e4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67911527"
---
# <a name="children-property-ado-md"></a>Children 속성(ADO MD)
현재 [멤버가](../../../ado/reference/ado-md-api/member-object-ado-md.md) 계층의 부모인 [멤버](../../../ado/reference/ado-md-api/members-collection-ado-md.md) 컬렉션을 반환 합니다.  
  
## <a name="return-values"></a>반환 값  
 **멤버** 컬렉션을 반환 하며 읽기 전용입니다.  
  
## <a name="remarks"></a>설명  
 **Children** 속성에는 현재 **멤버가** 계층적 부모인 **Members** 컬렉션이 포함 되어 있습니다. 리프 수준 **멤버** 개체의 **members** 컬렉션에는 자식 멤버가 없습니다. 이 속성은 [수준](../../../ado/reference/ado-md-api/level-object-ado-md.md) 개체에 속한 **멤버** 개체에 대해서만 지원 됩니다. [Position](../../../ado/reference/ado-md-api/position-object-ado-md.md) 개체에 속하는 **멤버** 개체에서이 속성을 참조 하는 경우 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Member 개체(ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>참고 항목  
 [ChildCount 속성(ADO MD)](../../../ado/reference/ado-md-api/childcount-property-ado-md.md)
