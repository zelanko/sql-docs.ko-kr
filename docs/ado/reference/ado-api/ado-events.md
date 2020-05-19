---
title: ADO 이벤트 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO]
- ADO, events
ms.assetid: 0ded5ad9-8f83-4224-95af-38512783b972
author: rothja
ms.author: jroth
ms.openlocfilehash: e1b69ced6c5d55b3b393ec30247c1a9f35f9fc57
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82747332"
---
# <a name="ado-events"></a>ADO 이벤트

|||  
|-|-|  
|[BeginTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|**BeginTrans** 작업 후에 호출 됩니다.|  
|[CommitTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|**CommitTrans** 작업 후에 호출 됩니다.|  
|[ConnectComplete](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|연결이 시작 된 후에 호출 됩니다.|  
|[케이블](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|연결이 종료 된 후에 호출 됩니다.|  
|[EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|**레코드 집합**의 끝을 지나서 행으로 이동 하려고 할 때 호출 됩니다.|  
|[ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|명령 실행이 완료 된 후에 호출 됩니다.|  
|[FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|긴 비동기 작업의 모든 레코드를 **레코드 집합**으로 검색 한 후에 호출 됩니다.|  
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)|**레코드 집합**으로 현재 검색 된 행 수를 보고 하기 위해 시간이 오래 걸리는 비동기 작업 중에 주기적으로 호출 됩니다.|  
|[FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|하나 이상의 **Field** 개체의 값이 변경 된 후에 호출 됩니다.|  
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|**Connectionevent** 작업 중에 경고가 발생할 때마다 호출 됩니다.|  
|[MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|**레코드 집합** 의 현재 위치가 변경 된 후에 호출 됩니다.|  
|[RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|하나 이상의 레코드가 변경 된 후에 호출 됩니다.|  
|[RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|**레코드 집합이** 변경 된 후에 호출 됩니다.|  
|[RollbackTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|**RollbackTrans** 작업 후에 호출 됩니다.|  
|[WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|보류 중인 작업에서 **레코드 집합**에 있는 하나 이상의 **필드** 개체 값이 변경 되기 전에 호출 됩니다.|  
|[WillChangeRecord](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|**레코드 집합** 에 있는 하나 이상의 레코드 (행)가 변경 되기 전에 호출 됩니다.|  
|[WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|보류 중인 작업에서 **레코드 집합**을 변경 하기 전에 호출 됩니다.|  
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md)|연결이 시작 되기 전에 호출 됩니다.|  
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md)|이 연결에서 보류 중인 명령이 실행 되 고 사용자가 보류 중인 실행 매개 변수를 검사 하 고 수정할 수 있는 기회를 발생 하기 직전에 호출 됩니다.|  
|[WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|**WillMove** 이벤트는 보류 중인 작업이 **레코드 집합**의 현재 위치를 변경 *하기 전에* 호출 됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [ADO API 참조](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO 컬렉션](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO 동적 속성](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [ADO 열거 상수](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [부록 B: ADO 오류](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 이벤트 처리](../../../ado/guide/data/handling-ado-events.md)   
 [ADO 메서드](../../../ado/reference/ado-api/ado-methods.md)   
 [ADO 개체 모델](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO 개체 및 인터페이스](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [ADO 속성](../../../ado/reference/ado-api/ado-properties.md)
