---
description: Clear 메서드(ADO)
title: Clear 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Errors::raw_Clear
- Errors::Clear
helpviewer_keywords:
- Clear method [ADO]
ms.assetid: 0a61ba7a-20b8-426a-91a0-9040e7c5a98a
author: rothja
ms.author: jroth
ms.openlocfilehash: 502592df71938e31ff50462878659df52c95f127
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450995"
---
# <a name="clear-method-ado"></a>Clear 메서드(ADO)
[Errors](../../../ado/reference/ado-api/errors-collection-ado.md) 컬렉션에서 [오류](../../../ado/reference/ado-api/error-object.md) 개체를 모두 제거 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Errors.Clear  
```  
  
## <a name="remarks"></a>설명  
 [Errors](../../../ado/reference/ado-api/errors-collection-ado.md) 컬렉션에서 **Clear** 메서드를 사용 하 여 컬렉션에서 기존 [오류](../../../ado/reference/ado-api/error-object.md) 개체를 모두 제거 합니다. 오류가 발생 하면 ADO에서 자동으로 **오류** 컬렉션을 지우고 새 오류에 따라 **오류** 개체를 채웁니다.  
  
 일부 속성 및 **메서드는 오류 컬렉션에** **오류** 개체로 표시 되지만 프로그램의 실행을 중단 하지 않는 경고를 반환 합니다. [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체의 [Resync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)또는 [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) 메서드를 호출 하기 전에 [Connection](../../../ado/reference/ado-api/connection-object-ado.md) 개체의 [Open](../../../ado/reference/ado-api/open-method-ado-connection.md) 메서드 또는 **레코드 집합** 개체에 대해 [Filter](../../../ado/reference/ado-api/filter-property.md) 속성을 설정 하 고 **Errors** 컬렉션에서 **Clear** 메서드를 호출 합니다. 이렇게 하면 **Errors** 컬렉션의 [Count](../../../ado/reference/ado-api/count-property-ado.md) 속성을 읽어 반환 된 경고를 테스트할 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Errors 컬렉션(ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Execute, Requery 및 Clear 메서드 예제 (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Execute, Requery 및 Clear 메서드 예제 (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Execute, Requery 및 Clear 메서드 예제 (VC + +)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [CancelBatch 메서드 (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Delete 메서드 (ADO Fields Collection)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 메서드 (ADO Parameters Collection)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [필터 속성](../../../ado/reference/ado-api/filter-property.md)   
 [Resync 메서드](../../../ado/reference/ado-api/resync-method.md)   
 [UpdateBatch 메서드](../../../ado/reference/ado-api/updatebatch-method.md)
