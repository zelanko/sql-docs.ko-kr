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
manager: craigg
ms.openlocfilehash: 1697197bf9450a6487e70b0257160221e59359f8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47822531"
---
# <a name="endofrecordset-event-ado"></a>EndOfRecordset 이벤트(ADO)
합니다 **EndOfRecordset** 이벤트의 끝을 지난 행으로 이동 하 려 할 때 호출 됩니다 합니다 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
EndOfRecordset fMoreData, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>매개 변수  
 *fMoreData*  
 **VARIANT_BOOL** 경우는 값을 variant_true로 설정, 더 많은 행에 추가 된 나타냅니다는 **레코드 집합**.  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) 상태 값입니다.  
  
 때 **EndOfRecordset** 가 호출 하 고,이 매개 변수는 설정 **adStatusOK** 이벤트를 발생 시킨 작업에 성공 하는 경우. 로 설정 되어 **adStatusCantDeny** 경우이 이벤트는이 이벤트를 발생 시킨 작업의 취소를 요청할 수 없습니다.  
  
 앞 **EndOfRecordset** 반환 되는 경우이 매개 변수를 설정 **adStatusUnwantedEvent** 후속 알림을 방지 하 합니다.  
  
 *pRecordset*  
 A **레코드 집합** 개체입니다. 합니다 **레코드 집합** 이 이벤트가 발생 한입니다.  
  
## <a name="remarks"></a>Remarks  
 **EndOfRecordset** 이벤트는 경우에 발생할 수 있습니다 합니다 [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) 작업이 실패 합니다.  
  
 끝을 넘어 이동 하려고 시도 하는 경우이 이벤트 처리기가 호출 된 **레코드 집합** 호출 등으로 인해 개체 **MoveNext**합니다. 그러나이 이벤트에서 수를 데이터베이스에서 더 많은 레코드를 검색 하 고 끝에 추가 합니다는 **레코드 집합**합니다. 이 경우에 설정할 *fMoreData* VARIANT_TRUE를 반환 **EndOfRecordset**합니다. 그런 다음 호출 **MoveNext** 새로 검색된 된 레코드에 액세스 하려면 다시 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ADO 이벤트 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)
