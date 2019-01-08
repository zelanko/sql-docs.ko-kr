---
title: Delete 메서드 (ADO 매개 변수 컬렉션) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _DynaCollection::Delete
- _DynaCollection::raw_Delete
helpviewer_keywords:
- Delete method [ADO]
ms.assetid: 160c575e-df63-4ade-a2d3-5fd8f72e70cc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8864ac47f3fa212cc6c204cc79d587b8952512cd
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52527413"
---
# <a name="delete-method-ado-parameters-collection"></a>Delete 메서드(ADO 매개 변수 컬렉션)
개체를 삭제 합니다 [매개 변수](../../../ado/reference/ado-api/parameters-collection-ado.md) 컬렉션입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Parameters.Delete Index  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Index*  
 A **문자열** 컬렉션에서 삭제 하려는 개체 또는 개체의 서 수 위치 (인덱스)의 이름을 포함 하는 값입니다.  
  
## <a name="remarks"></a>Remarks  
 사용 하는 **삭제** 컬렉션에 대해 메서드를 사용 하면 컬렉션의 개체 중 하나를 제거 합니다. 이 메서드는 에서만 사용할 수 있습니다 합니다 **매개 변수** 의 컬렉션을 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체입니다. 사용 해야 합니다는 [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 개체의 [이름](../../../ado/reference/ado-api/name-property-ado.md) 속성 또는 호출 하는 경우 해당 컬렉션 인덱스는 **삭제** 메서드는 개체 변수는 유효한 인수가 아닙니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Parameters 컬렉션(ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [Delete 메서드 (ADO 필드 컬렉션)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [DeleteRecord 메서드(ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
