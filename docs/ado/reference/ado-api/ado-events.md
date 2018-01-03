---
title: "ADO 이벤트 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- events [ADO]
- ADO, events
ms.assetid: 0ded5ad9-8f83-4224-95af-38512783b972
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dec529bcbc7130ea29fac793a82a5979974f396e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="ado-events"></a>ADO 이벤트
|||  
|-|-|  
|[BeginTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|다음에 호출 된 **BeginTrans** 작업 합니다.|  
|[CommitTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|다음에 호출 된 **CommitTrans** 작업 합니다.|  
|[ConnectComplete](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|연결이 시작 된 후 호출 됩니다.|  
|[연결 끊기](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|연결이 종료 된 후 호출 됩니다.|  
|[EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|끝을 지나서 행으로 이동 하 려 할 때 호출 된 **레코드 집합**합니다.|  
|[ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|명령 실행을 마친 후 호출 됩니다.|  
|[FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|긴 비동기 작업의 모든 레코드도 가져온 후에 호출 된 **레코드 집합**합니다.|  
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)|에 현재으로 가져온 행 수를 보고 하기 위해 시간이 오래 걸리는 비동기 작업을 하는 동안에 주기적으로 호출 된 **레코드 집합**합니다.|  
|[FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|하나 이상의 값 다음에 호출 **필드** 개체 변경 되었습니다.|  
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|경고 하는 동안 발생할 때마다 호출 됩니다는 **ConnectionEvent** 작업 합니다.|  
|[두](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|현재 위치에 다음에 호출 된 **레코드 집합** 변경 합니다.|  
|[RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|하나 이상의 레코드 변경 후 호출 됩니다.|  
|[RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|다음에 호출 된 **레코드 집합** 변경 되었습니다.|  
|[RollbackTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|다음에 호출 된 **RollbackTrans** 작업 합니다.|  
|[WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|보류 중인 작업이 하나 이상의 값을 변경 하기 전에 호출 **필드** 개체에 **레코드 집합**합니다.|  
|[WillChangeRecord](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|하나 이상의 레코드 (행) 전에 호출 된 **레코드 집합** 변경 합니다.|  
|[WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|보류 중인 작업을 변경 하기 전에 호출 됩니다는 **레코드 집합**합니다.|  
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md)|연결을 시작 하기 전에 호출 됩니다.|  
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md)|이 연결에서 실행 하 고 사용자 검사 하 고 보류 중인 실행 매개 변수를 수정할 수 있는 기회를 제공 하는 보류 중인 명령이 바로 전에 호출 됩니다.|  
|[WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|**WillMove** 라고 이벤트 *전에* 보류 중인 작업의 현재 위치를 변경 합니다.는 **레코드 집합**합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [ADO API 참조](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO 컬렉션](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO 동적 속성](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [ADO 열거 상수](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [부록 b: ADO 오류](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 이벤트 처리](../../../ado/guide/data/handling-ado-events.md)   
 [ADO 메서드](../../../ado/reference/ado-api/ado-methods.md)   
 [ADO 개체 모델](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO 개체 및 인터페이스](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [ADO 속성](../../../ado/reference/ado-api/ado-properties.md)
