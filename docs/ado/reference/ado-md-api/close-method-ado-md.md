---
title: Close 메서드 (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Close
- Cellset::Close
helpviewer_keywords:
- Close method [ADO MD]
ms.assetid: a3aa594d-f9d4-4654-8625-ec20153ff5d9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ca61f383198207223abf30ce25d9c922909f6526
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62653503"
---
# <a name="close-method-ado-md"></a>Close 메서드(ADO MD)
열려 있는 셀 집합을 닫습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Cellset.Close  
```  
  
## <a name="remarks"></a>Remarks  
 사용 하는 **닫습니다** 닫는 메서드를를 [셀 집합](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) 개체와 관련 된 모든 데이터를 포함 하 여 연결 된 데이터를 해제 합니다 [셀](../../../ado/reference/ado-md-api/cell-object-ado-md.md), [축](../../../ado/reference/ado-md-api/axis-object-ado-md.md), [위치](../../../ado/reference/ado-md-api/position-object-ado-md.md), 또는 [멤버](../../../ado/reference/ado-md-api/member-object-ado-md.md) 개체입니다. 닫기는 **Cellset** 메모리에서 제거 되지는 않습니다 속성 설정을 변경 하 고 나중에 다시 열 수 있습니다. 메모리에서 개체를 완전히 제거 하려면 개체 변수를 설정 합니다 **Nothing**합니다.  
  
 나중에 호출할 수 있습니다는 [열려](../../../ado/reference/ado-md-api/open-method-ado-md.md) 다시 여는 메서드를 **셀 집합** 같거나 다른을 사용 하 여 원본 문자열입니다. 동안 합니다 **셀 집합** 개체가 닫혀, 모든 속성을 검색 하거나 기본 데이터를 참조 하는 메서드를 호출 하거나 메타 데이터 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Cellset 개체(ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>관련 항목  
 [축 개체 (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)   
 [Cell 개체 (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [멤버 개체 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)   
 [Open 메서드 (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)   
 [Position 개체 (ADO MD)](../../../ado/reference/ado-md-api/position-object-ado-md.md)   
 [State 속성(ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)
