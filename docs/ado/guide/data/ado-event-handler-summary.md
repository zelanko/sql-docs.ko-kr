---
description: ADO 연결 및 레코드 집합 이벤트
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 92d1dcd202c4e115cda4198f90e3410c2cb44319
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453845"
---
# <a name="ado-connection-and-recordset-events"></a>ADO 연결 및 레코드 집합 이벤트
두 ADO 개체는 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체와 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체와 같은 이벤트를 발생 시킬 수 있습니다. **Connectionevent** Family는 **연결** 개체에 대 한 작업과 관련 되며 **RecordsetEvent** 패밀리는 **레코드 집합** 개체에 대 한 작업과 관련이 있습니다.

-   **연결 이벤트**: 연결의 트랜잭션이 시작 되거나 커밋되거나 커밋되거나 롤백될 때 이벤트가 발생 합니다. [명령이](../../../ado/reference/ado-api/command-object-ado.md) 실행 되는 경우 **연결 이벤트** 작업 중에 경고가 발생 하는 경우 **연결** 을 시작 하거나 종료 하는 경우입니다.

-   **레코드 집합 이벤트**: 비동기 인출 작업을 통해 이벤트가 발생 하 고 **, 레코드 집합 개체의** 행을 탐색 하거나 **, 레코드 집합**의 행을 변경 하거나 **, 레코드 집합**의 행을 변경 하거나, 서버 쪽 커서를 **사용 하 여 레코드 집합** 을 열거나, 레코드 집합을 **닫거나,** **레코드 집합**에 변경 내용을 적용할 수 없습니다.

 다음 표에서는 이벤트와 그에 대 한 설명을 요약 합니다.

|ConnectionEvent|설명|
|---------------------|-----------------|
|[BeginTransComplete, CommitTransComplete, RollbackTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|**트랜잭션 관리** -연결의 현재 트랜잭션이 시작, 커밋 또는 롤백 되었다는 알림입니다.|
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md), [Connectcomplete, Disconnect](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|**연결 관리** -현재 연결이 시작, 시작 또는 종료 되었다는 알림입니다.|
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md), [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|**명령 실행 관리** -연결에 대 한 현재 명령의 실행이 시작 되거나 종료 되었다는 알림입니다.|
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|**정보** -현재 작업에 대 한 추가 정보가 있음을 알립니다.|

|RecordsetEvent|설명|
|--------------------|-----------------|
|[Fetchprogress](../../../ado/reference/ado-api/fetchprogress-event-ado.md), [fetchprogress](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|**검색 상태** -데이터 검색 작업의 진행률에 대 한 알림 또는 검색 작업이 완료 되었습니다. 이러한 이벤트는 클라이언트 쪽 커서를 사용 하 여 **레코드 집합** 을 연 경우에만 사용할 수 있습니다.|
|[WillChangeField, FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|**필드 변경 관리** -현재 필드의 값이 변경 되거나 변경 되었음을 알립니다.|
|[WillMove, MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md), [EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|**탐색 관리** - **레코드** 집합의 현재 행 위치가 변경 되거나 변경 되거나 **레코드 집합**의 끝에 도달 했음을 알립니다.|
|[WillChangeRecord, RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|**행 변경 관리** - **레코드 집합** 의 현재 행에 있는 항목의 변경 또는 변경 된 알림입니다.|
|[WillChangeRecordset, RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|**레코드 집합 변경 관리** -현재 **레코드 집합** 의 내용이 변경 되거나 변경 됨을 알립니다.|

## <a name="see-also"></a>참고 항목
 [언어별 Ado 이벤트 인스턴스](../../../ado/guide/data/ado-event-instantiation-by-language.md) [Ado](../../../ado/reference/ado-api/ado-events.md) [이벤트 이벤트](../../../ado/guide/data/event-parameters.md) 처리기에서 이벤트 [유형을](../../../ado/guide/data/types-of-events.md) [함께 사용 하는 방법](../../../ado/guide/data/how-event-handlers-work-together.md)
