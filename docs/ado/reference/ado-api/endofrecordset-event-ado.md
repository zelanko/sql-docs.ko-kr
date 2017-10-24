---
title: "EndOfRecordset 이벤트 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- EndOfRecordset
- Recordset::EndOfRecordset
helpviewer_keywords:
- EndOfRecordset event [ADO]
ms.assetid: 475de5e2-f634-4954-9edf-0027a6ba38d6
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4cf00efb278f6ea9937bd0fa87f929d45b8294cb
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="endofrecordset-event-ado"></a>EndOfRecordset 이벤트 (ADO)
**EndOfRecordset** 이벤트의 끝을 지나서 행으로 이동 하 려 할 때 호출 됩니다는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
EndOfRecordset fMoreData, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>매개 변수  
 *fMoreData*  
 A **VARIANT_BOOL** 값을 variant_true로 설정, 더 많은 행에 추가 된 나타냅니다는 **레코드 집합**합니다.  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) 상태 값입니다.  
  
 때 **EndOfRecordset** 은 호출,이 매개 변수 설정 **adStatusOK** 이벤트를 발생 시킨 작업에 성공 하면 합니다. 로 설정 된 **adStatusCantDeny** 경우이 이벤트는이 이벤트를 발생 시킨 작업의 취소를 요청할 수 없습니다.  
  
 하기 전에 **EndOfRecordset** 반환 되 면이 매개 변수를 설정 **adStatusUnwantedEvent** 알림 메시지가 방지 하기 위해 합니다.  
  
 *pRecordset*  
 A **레코드 집합** 개체입니다. **레코드 집합** 이 이벤트가 발생 하는 것에 대 한 합니다.  
  
## <a name="remarks"></a>주의  
 **EndOfRecordset** 경우 이벤트가 발생할 수 있습니다는 [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) 작업이 실패 합니다.  
  
 끝을 지나서 이동 하려고 시도 하는 경우이 이벤트 처리기가 호출 된 **레코드 집합** 개체를 호출한 결과로 아마도 **MoveNext**합니다. 하지만이 이벤트에 있는 동안 수는 데이터베이스에서 더 많은 레코드 검색을의 끝에 추가 된 **레코드 집합**합니다. 이 경우에 설정 *fMoreData* VARIANT_TRUE 이면 및에서 반환을 **EndOfRecordset**합니다. 그런 다음 호출 **MoveNext** 다시 하 새로 검색된 된 레코드에 액세스 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ADO 이벤트 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)

