---
title: EndOfRecordset 이벤트 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EndOfRecordset
- Recordset::EndOfRecordset
helpviewer_keywords:
- EndOfRecordset event [ADO]
ms.assetid: 475de5e2-f634-4954-9edf-0027a6ba38d6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0a83f101d46a94a4ea43a85424677fc1c8da08be
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67918945"
---
# <a name="endofrecordset-event-ado"></a>EndOfRecordset 이벤트(ADO)
**EndOfRecordset** 이벤트는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)의 끝을 지나서 행으로 이동 하려고 할 때 호출 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
EndOfRecordset fMoreData, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>매개 변수  
 *fMoreData*  
 VARIANT_TRUE로 설정 된 경우 **레코드 집합**에 추가 된 행이 있음을 나타내는 **VARIANT_BOOL** 값입니다.  
  
 *adStatus*  
 [Eventstatusenum](../../../ado/reference/ado-api/eventstatusenum.md) 상태 값입니다.  
  
 **EndOfRecordset** 가 호출 되 면이 매개 변수는 이벤트를 발생 시킨 작업이 성공한 경우 **adstatusok** 로 설정 됩니다. 이 이벤트가이 이벤트를 발생 시킨 작업의 취소를 요청할 수 없는 경우 **adStatusCantDeny** 로 설정 됩니다.  
  
 **EndOfRecordset** 가 반환 되기 전에이 매개 변수를 **adStatusUnwantedEvent** 로 설정 하 여 후속 알림이 발생 하지 않도록 합니다.  
  
 *pRecordset*  
 **레코드 집합** 개체입니다. 이 이벤트가 발생 한 **레코드 집합** 입니다.  
  
## <a name="remarks"></a>설명  
 **EndOfRecordset** 이벤트는 [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) 작업이 실패 하는 경우 발생할 수 있습니다.  
  
 이 이벤트 처리기는 **MoveNext**를 호출한 결과로 **레코드 집합** 개체의 끝을 지나서 이동 하려고 할 때 호출 됩니다. 그러나이 경우에는 데이터베이스에서 더 많은 레코드를 검색 하 여 **레코드 집합**의 끝에 추가할 수 있습니다. 이 경우 *fMoreData* 을 VARIANT_TRUE로 설정 하 고 **EndOfRecordset**에서 반환 합니다. 그런 다음 **MoveNext** 를 다시 호출 하 여 새로 검색 된 레코드에 액세스 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ADO Events 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)
