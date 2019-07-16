---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 96bd13f130966b1830d07e49633842e4154b52b4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920060"
---
# <a name="clear-method-ado"></a>Clear 메서드(ADO)
모두 제거 합니다 [오류](../../../ado/reference/ado-api/error-object.md) 에서 개체를 [오류](../../../ado/reference/ado-api/errors-collection-ado.md) 컬렉션입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Errors.Clear  
```  
  
## <a name="remarks"></a>설명  
 사용 하 여를 **지우기** 메서드는 [오류](../../../ado/reference/ado-api/errors-collection-ado.md) 기존의 모든 컬렉션 [오류](../../../ado/reference/ado-api/error-object.md) 컬렉션에서 개체입니다. ADO를 자동으로 지웁니다 오류가 발생 하는 경우는 **오류** 컬렉션으로 사용 하 여 화면을 채웁니다 **오류** 새 오류를 기반으로 개체입니다.  
  
 일부 속성 및 메서드 반환로 표시 되는 경고 **오류** 개체를 **오류** 컬렉션 하지만 프로그램의 실행을 중단 되지는 않습니다. 호출 하기 전에 [다시 동기화](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), 또는 [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) 메서드를 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) ; 개체는 [엽니다](../../../ado/reference/ado-api/open-method-ado-connection.md) 메서드를를 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체를 가져오거나 설정 합니다 [필터](../../../ado/reference/ado-api/filter-property.md) 속성을를 **레코드 집합** 개체를 호출는 **선택을취소**메서드는 **오류** 컬렉션입니다. 읽을 수 있습니다 따라서를 [수](../../../ado/reference/ado-api/count-property-ado.md) 의 속성을 **오류** 를 테스트할 컬렉션 경고를 반환 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Errors 컬렉션(ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [실행, requery, Clear 메서드 예제 (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [실행, requery, Clear 메서드 예제 (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Execute, requery, Clear 메서드 예제 (VC + +)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [CancelBatch 메서드 (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Delete 메서드 (ADO 필드 컬렉션)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 메서드 (ADO 매개 변수 컬렉션)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [필터 속성](../../../ado/reference/ado-api/filter-property.md)   
 [Resync 메서드](../../../ado/reference/ado-api/resync-method.md)   
 [UpdateBatch 메서드](../../../ado/reference/ado-api/updatebatch-method.md)
