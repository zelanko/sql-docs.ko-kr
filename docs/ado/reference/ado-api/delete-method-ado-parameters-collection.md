---
title: Delete 메서드 (ADO Parameters 컬렉션) | Microsoft Docs
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
- _DynaCollection::Delete
- _DynaCollection::raw_Delete
helpviewer_keywords:
- Delete method [ADO]
ms.assetid: 160c575e-df63-4ade-a2d3-5fd8f72e70cc
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cac5d27adc6ce3f6e6e445c54c7848675c54eb59
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="delete-method-ado-parameters-collection"></a>Delete 메서드 (ADO Parameters 컬렉션)
개체를 삭제는 [매개 변수](../../../ado/reference/ado-api/parameters-collection-ado.md) 컬렉션입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Parameters.Delete Index  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Index*  
 A **문자열** 컬렉션에서 삭제할 개체 또는 개체의 서 수 위치 (인덱스)의 이름을 포함 하는 값입니다.  
  
## <a name="remarks"></a>주의  
 사용 하는 **삭제** 메서드는 컬렉션에 컬렉션의 개체 중 하나를 제거할 수 있습니다. 이 메서드는 에서만 사용할 수는 **매개 변수** 컬렉션은 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체입니다. 사용 해야 합니다는 [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 개체의 [이름](../../../ado/reference/ado-api/name-property-ado.md) 속성이 나 호출할 때 해당 컬렉션 인덱스는 **삭제** 메서드-개체 변수는 유효한 인수가 아닙니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Parameters 컬렉션(ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [Delete 메서드 (ADO 필드 컬렉션)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [DeleteRecord 메서드(ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
