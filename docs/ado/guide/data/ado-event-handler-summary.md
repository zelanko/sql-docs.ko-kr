---
title: ADO 이벤트 처리기 요약 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO], about event handlers
- event handlers [ADO]
ms.assetid: b34f4472-5e04-4a2c-ab64-38d6eca31a69
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d4fef63ff610ad85e353c2ef1dc0f8e5987c74ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926192"
---
# <a name="ado-connection-and-recordset-events"></a>ADO 연결 및 레코드 집합 이벤트
두 ADO 개체 이벤트를 발생 시킬 수 있습니다: 합니다 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체와 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다. **ConnectionEvent** 제품군 관련 작업에는 **연결** 개체 및 **RecordsetEvent** 제품군 관련 작업에는  **레코드 집합** 개체입니다.

-   **연결 이벤트**: 연결에서 트랜잭션을 시작, 커밋되지 않은 경우, 또는 롤백되면; 때 이벤트가 발생 경우는 [명령](../../../ado/reference/ado-api/command-object-ado.md) 실행 중에 경고가 발생 하는 경우를 **연결 이벤트** 작업 때나를 **연결** 시작 하거나 끝날 합니다.

-   **레코드 집합 이벤트**: 행을 탐색할 때와 비동기 인출 작업 관련 이벤트가 발생 한 **레코드 집합** 개체, 행의 필드를 변경를 **레코드 집합**에서 행을 변경를  **레코드 집합**를 엽니다는 **레코드 집합** 서버 쪽 커서를 닫습니다를 **레코드 집합**, 또는 확인에 한 어떠한 변경 합니다 **레코드 집합**.

 다음 표에서 이벤트 및 해당 설명이 요약 되어 있습니다.

|ConnectionEvent|설명|
|---------------------|-----------------|
|[BeginTransComplete, CommitTransComplete, RollbackTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|**트랜잭션 관리** -연결에서 현재 트랜잭션이 시작 되었음을 나타내는 알림이 커밋되거나 롤백됩니다.|
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md), [ConnectComplete, Disconnect](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|**연결 관리** -현재 연결을 시작 하는 알림 시작 또는 종료 되었습니다.|
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md), [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|**실행 관리 명령을** -알림 연결에서 현재 명령의 실행 시작 또는 종료 되었습니다.|
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|**정보 제공 용 이므로** -현재 작업에 대 한 추가 정보는 알림입니다.|

|RecordsetEvent|설명|
|--------------------|-----------------|
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md), [FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|**검색 상태** -데이터 검색 작업의 진행률에 대 한 알림 또는 검색 작업을 완료 합니다. 이러한 이벤트는만 사용할 수 있는 경우는 **레코드 집합** 클라이언트 쪽 커서를 사용 하 여 열린 합니다.|
|[WillChangeField, FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|**필드 변경 관리** -현재 필드의 값이 변경 또는 변경 하는 알림입니다.|
|[WillMove, MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md), [EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|**탐색 관리** -알림 현재 행에서 해당 위치를 **레코드 집합** 바뀝니다, 변경 또는 끝에 도달 했습니다 합니다 **레코드 집합**합니다.|
|[WillChangeRecord, RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|**변경 관리 행** -의 현재 행에서 인가 알림 합니다 **레코드 집합** 변경 또는 변경 되었습니다.|
|[WillChangeRecordset, RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|**레코드 집합 변경 관리** -현재에서 인가 알림을 **레코드 집합** 변경 또는 변경 되었습니다.|

## <a name="see-also"></a>관련 항목
 [언어별 ADO 이벤트 인스턴스](../../../ado/guide/data/ado-event-instantiation-by-language.md) [ADO 이벤트](../../../ado/reference/ado-api/ado-events.md) [이벤트 매개 변수](../../../ado/guide/data/event-parameters.md) [이벤트 처리기를 함께 작동](../../../ado/guide/data/how-event-handlers-work-together.md) [유형의 이벤트](../../../ado/guide/data/types-of-events.md)
