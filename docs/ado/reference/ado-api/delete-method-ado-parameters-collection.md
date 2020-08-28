---
description: Delete 메서드(ADO 매개 변수 컬렉션)
title: Delete 메서드 (ADO Parameters Collection) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3860a824690d9dca469a22135d35e040cc000dca
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974124"
---
# <a name="delete-method-ado-parameters-collection"></a>Delete 메서드(ADO 매개 변수 컬렉션)
[Parameters](../../../ado/reference/ado-api/parameters-collection-ado.md) 컬렉션에서 개체를 삭제 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Parameters.Delete Index  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Index*  
 삭제할 개체의 이름 또는 컬렉션의 개체의 서 수 위치 (인덱스)를 포함 하는 **문자열** 값입니다.  
  
## <a name="remarks"></a>설명  
 컬렉션에서 **Delete** 메서드를 사용 하면 컬렉션의 개체 중 하나를 제거할 수 있습니다. 이 메서드는 [Command](../../../ado/reference/ado-api/command-object-ado.md) 개체의 **Parameters** 컬렉션에 대해서만 사용할 수 있습니다. **Delete** 메서드를 호출할 때 [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 개체의 [Name](../../../ado/reference/ado-api/name-property-ado.md) 속성 또는 해당 컬렉션 인덱스를 사용 해야 합니다. 개체 변수가 올바른 인수가 아닙니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Parameters 컬렉션(ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Delete 메서드 (ADO Fields Collection)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [DeleteRecord 메서드(ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
