---
title: "Requery 메서드 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::Requery
- Recordset15::raw_Requery
helpviewer_keywords:
- Requery method [ADO]
ms.assetid: d81ab76f-1aa8-4ccf-92ec-b65254dc3ea1
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a6e81cda01f894b87d2741f80735b21b23423ce6
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="requery-method"></a>Requery 메서드
데이터를 업데이트 한 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 다시 개체의 기반이 되는 쿼리를 실행 하 여 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
recordset.Requery Options  
```  
  
#### <a name="parameters"></a>매개 변수  
 *옵션*  
 (선택 사항) 포함 하는 비트 마스크 [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) 및 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) 이 작업에 영향을 주는 값입니다.  
  
> [!NOTE]
>  경우 *옵션* 로 설정 된 **adAsyncExecute**,이 작업은 비동기적으로 실행 및 [RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md) 것으로 결론 때 이벤트를 발생 합니다. **ExecuteOpenEnum** 값 **adExecuteNoRecords** 또는 **adExecuteStream** 으로 쓰일 수 없습니다 **Requery**합니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **Requery** 의 전체 내용을 새로 고치려면 메서드는 **레코드 집합** 원래 명령을 다시 실행 하 고 데이터를 두 번째로 검색 하 여 데이터 원본에서 개체입니다. 이 메서드를 호출 하는 것은 [닫기](../../../ado/reference/ado-api/close-method-ado.md) 및 [열려](../../../ado/reference/ado-api/open-method-ado-recordset.md) 연속적으로 메서드. 현재 레코드를 편집 하거나 새 레코드를 추가, 오류가 발생 합니다.  
  
 반면는 **레코드 집합** 개체가 열려, 커서의 특성을 정의 하는 속성 ([모두](../../../ado/reference/ado-api/cursortype-property-ado.md), [LockType](../../../ado/reference/ado-api/locktype-property-ado.md), [MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md) 등)은 읽기 전용입니다. 따라서는 **Requery** 메서드만 현재 커서를 새로 고칠 수 있습니다. 커서 속성을 변경 하 고 결과 확인 하려면 사용 해야 합니다는 [닫기](../../../ado/reference/ado-api/close-method-ado.md) 메서드 속성 읽기/쓰기를 다시 수 있도록 합니다. 속성 설정 및 호출을 변경할 수 있습니다는 [열려](../../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드는 커서를 다시 열입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [실행, Requery, 및 메서드 예제 (VB)를 지웁니다.](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [실행, Requery, 및 메서드 (VBScript) 예제를 지웁니다.](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [실행 하 고 다시 쿼리, 메서드 예제 (VC + +)을 선택 취소](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [CommandText 속성(ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)
