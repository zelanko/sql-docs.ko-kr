---
title: Close 메서드 (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Close
- Cellset::Close
helpviewer_keywords:
- Close method [ADO MD]
ms.assetid: a3aa594d-f9d4-4654-8625-ec20153ff5d9
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 48550f8d2f830505e960c483da8c8c05c11d3d0b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="close-method-ado-md"></a>Close 메서드 (ADO MD)
열려 있는 셀 집합을 닫습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Cellset.Close  
```  
  
## <a name="remarks"></a>주의  
 사용 하는 **닫습니다** 을 닫는 메서드는 [셀 집합](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) 개체와 관련 된 모든 데이터를 포함 하 여 연결 된 데이터는 해제 [셀](../../../ado/reference/ado-md-api/cell-object-ado-md.md), [축](../../../ado/reference/ado-md-api/axis-object-ado-md.md), [위치](../../../ado/reference/ado-md-api/position-object-ado-md.md), 또는 [멤버](../../../ado/reference/ado-md-api/member-object-ado-md.md) 개체입니다. 닫기는 **셀 집합** ; 메모리에서 제거 하지는 않습니다 속성 설정을 변경 하 고 나중에 다시 열 수 있습니다. 메모리에서 개체를 완전히 제거 하려면 개체 변수를 설정 **Nothing**합니다.  
  
 나중에 호출할 수 있습니다는 [열려](../../../ado/reference/ado-md-api/open-method-ado-md.md) 메서드를 다시 열려면는 **셀 집합** 같거나 다른을 사용 하 여 원본 문자열입니다. 반면는 **셀 집합** 모든 속성을 검색 하는 기본 데이터를 참조 하는 메서드를 호출 하거나 개체를 닫을 또는 메타 데이터 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Cellset 개체(ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>관련 항목:  
 [축 개체 (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)   
 [ADO MD cell 개체](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [멤버 개체 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)   
 [ADO MD open 메서드](../../../ado/reference/ado-md-api/open-method-ado-md.md)   
 [ADO MD 위치 개체](../../../ado/reference/ado-md-api/position-object-ado-md.md)   
 [State 속성(ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)
