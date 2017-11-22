---
title: "Clear 메서드 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Errors::raw_Clear
- Errors::Clear
helpviewer_keywords: Clear method [ADO]
ms.assetid: 0a61ba7a-20b8-426a-91a0-9040e7c5a98a
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e1770a8bbf9fac82dece435a46374876b55d1c14
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="clear-method-ado"></a>Clear 메서드 (ADO)
모든 제거는 [오류](../../../ado/reference/ado-api/error-object.md) 에서 개체는 [오류](../../../ado/reference/ado-api/errors-collection-ado.md) 컬렉션입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Errors.Clear  
```  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **지우기** 에서 메서드는 [오류](../../../ado/reference/ado-api/errors-collection-ado.md) 모든 기존 제거 하려면 컬렉션 [오류](../../../ado/reference/ado-api/error-object.md) 컬렉션에서 개체입니다. ADO를 자동으로 지웁니다 오류가 발생 하면는 **오류** 컬렉션 및 사용 하 여 채우기 **오류** 새 오류를 기반으로 하는 개체입니다.  
  
 일부 속성 및 메서드로 표시 되는 경고를 반환 **오류** 개체에 **오류** 컬렉션 하지만 프로그램 실행이 중단 되지는 않습니다. 호출 하기 전에 [Resync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), 또는 [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) 에 대 한 메서드는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체는 [열](../../../ado/reference/ado-api/open-method-ado-connection.md) 메서드를 한 [연결](../../../ado/reference/ado-api/connection-object-ado.md) ; 개체 또는 설정는 [필터](../../../ado/reference/ado-api/filter-property.md) 속성에는 **레코드 집합** 개체를 호출 하는 **의선택을취소**에서 메서드는 **오류** 컬렉션입니다. 읽을 수 이런 방식으로 [개수](../../../ado/reference/ado-api/count-property-ado.md) 속성은 **오류** 테스트할 컬렉션을 경고를 반환 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Errors 컬렉션(ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [실행, Requery, 및 메서드 예제 (VB)를 지웁니다.](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [실행, Requery, 및 메서드 (VBScript) 예제를 지웁니다.](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [실행 하 고 다시 쿼리, 메서드 예제 (VC + +)을 선택 취소](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [CancelBatch 메서드 (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Delete 메서드 (ADO 필드 컬렉션)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 메서드 (ADO Parameters 컬렉션)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [필터 속성](../../../ado/reference/ado-api/filter-property.md)   
 [Resync 메서드](../../../ado/reference/ado-api/resync-method.md)   
 [UpdateBatch 메서드](../../../ado/reference/ado-api/updatebatch-method.md)
