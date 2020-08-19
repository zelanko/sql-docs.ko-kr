---
description: Close 메서드(ADO MD)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 5a0cff50bbbb238febdf5f187e6bf99cf88a4762
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441175"
---
# <a name="close-method-ado-md"></a>Close 메서드(ADO MD)
열린 셀 집합을 닫습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Cellset.Close  
```  
  
## <a name="remarks"></a>설명  
 **Close** 메서드를 사용 하 여 셀 [집합](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) 개체를 닫으면 관련 된 [셀](../../../ado/reference/ado-md-api/cell-object-ado-md.md), [축](../../../ado/reference/ado-md-api/axis-object-ado-md.md), [위치](../../../ado/reference/ado-md-api/position-object-ado-md.md)또는 [멤버](../../../ado/reference/ado-md-api/member-object-ado-md.md) 개체의 데이터를 포함 하 여 연결 된 데이터가 해제 됩니다. **셀 집합** 을 닫으면 메모리가 제거 되지 않습니다. 속성 설정을 변경 하 고 나중에 다시 열 수 있습니다. 메모리에서 개체를 완전히 제거 하려면 개체 변수를 **Nothing**으로 설정 합니다.  
  
 나중에 [Open](../../../ado/reference/ado-md-api/open-method-ado-md.md) 메서드를 호출 하 여 동일한 또는 다른 소스 문자열을 사용 하 여 **셀 집합** 을 다시 열 수 있습니다. **Cellset** 개체가 닫혀 있는 동안에는 속성을 검색 하거나 기본 데이터 또는 메타 데이터를 참조 하는 메서드를 호출 하는 동안 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Cellset 개체(ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>참고 항목  
 [Axis 개체 (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)   
 [Cell 개체 (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [Member 개체 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)   
 [Open 메서드 (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)   
 [Position 개체 (ADO MD)](../../../ado/reference/ado-md-api/position-object-ado-md.md)   
 [State 속성(ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)
