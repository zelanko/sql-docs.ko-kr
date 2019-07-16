---
title: Requery 메서드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Requery
- Recordset15::raw_Requery
helpviewer_keywords:
- Requery method [ADO]
ms.assetid: d81ab76f-1aa8-4ccf-92ec-b65254dc3ea1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c3626f91018714fa4d67304c92ce464d82fb5c8e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917218"
---
# <a name="requery-method"></a>Requery 메서드
데이터를 업데이트 한 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 다시 개체의 기반이 되는 쿼리를 실행 하 여 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
recordset.Requery Options  
```  
  
#### <a name="parameters"></a>매개 변수  
 *옵션*  
 (선택 사항) 포함 하는 비트 마스크 [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) 하 고 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) 이 작업에 영향을 주는 값입니다.  
  
> [!NOTE]
>  경우 *옵션* 로 설정 된 **adAsyncExecute**에서이 작업을 비동기적으로 실행 됩니다 및 [RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md) 없다고 때 이벤트가 발생 합니다. 합니다 **ExecuteOpenEnum** 의 값 **adExecuteNoRecords** 또는 **adExecuteStream** 사용 하 여 사용할 수 없습니다 **Requery**합니다.  
  
## <a name="remarks"></a>설명  
 사용 하 여는 **Requery** 의 전체 내용을 새로 고치려면 메서드는 **레코드 집합** 원래 명령을 다시 실행 하 고 두 번째 시간 데이터를 검색 하 여 데이터 소스에서 개체입니다. 이 메서드를 호출 하는 것은 [닫기](../../../ado/reference/ado-api/close-method-ado.md) 및 [열려](../../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드를 연속 해 서입니다. 현재 레코드를 편집 또는 새 레코드를 추가 하는 경우 오류가 발생 했습니다.  
  
 동안 합니다 **레코드 집합** 개체가 열려 커서의 특성을 정의 하는 속성 ([CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)를 [LockType](../../../ado/reference/ado-api/locktype-property-ado.md)를 [MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md) 등)는 읽기 전용입니다. 따라서 합니다 **Requery** 메서드만 현재 커서를 새로 고칠 수 있습니다. 커서 속성을 변경 하 고 결과 확인을 사용 해야 합니다 [닫기](../../../ado/reference/ado-api/close-method-ado.md) 메서드 속성 읽기/쓰기를 다시 수 있도록 합니다. 속성 설정 및 호출을 변경할 수 있습니다 합니다 [열고](../../../ado/reference/ado-api/open-method-ado-recordset.md) 커서를 닫은 방법입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [실행, requery, Clear 메서드 예제 (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [실행, requery, Clear 메서드 예제 (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Execute, requery, Clear 메서드 예제 (VC + +)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [CommandText 속성(ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)
