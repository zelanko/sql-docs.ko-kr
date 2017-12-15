---
title: "LOGON 트리거 이벤트 데이터 캡처 | Microsoft 문서"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: triggers
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e05b1ab4-c10b-402a-9591-f6ec1e3db8c0
caps.latest.revision: "5"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f416a2ce4e59d9d097348fb601825867df10d7b4
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="capture-logon-trigger-event-data"></a>LOGON 트리거 이벤트 데이터 캡처
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)] LOGON 트리거 내에서 사용할 LOGON 이벤트에 대한 XML 데이터를 캡처하려면 [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md) 함수를 사용합니다. LOGON 이벤트는 다음 이벤트 데이터 스키마를 반환합니다.  
  
 `<EVENT_INSTANCE>`  
  
 `<EventType>event_type</EventType>`  
  
 `<PostTime>post_time</PostTime>`  
  
 `<SPID>spid</SPID>`  
  
 `<ServerName>server_name</ServerName>`  
  
 `<LoginName>login_name</LoginName>`  
  
 `<LoginType>login_type</LoginType>`  
  
 `<SID>sid</SID>`  
  
 `<ClientHost>client_host</ClientHost>`  
  
 `<IsPooled>is_pooled</IsPooled>`  
  
 `</EVENT_INSTANCE>`  
  
 `<EventType>`  
 `LOGON`을 포함합니다.  
  
 `<PostTime>`  
 세션 설정이 요청된 시간을 포함합니다.  
  
 `<SID>`  
 지정된 로그인 이름에 대한 SID(보안 ID)의 base 64로 인코딩된 이진 스트림을 포함합니다.  
  
 `<ClientHost>`  
 연결을 설정할 클라이언트의 호스트 이름을 포함합니다. 클라이언트 이름과 서버 이름이 같을 경우 이 값은 '`<local_machine>`'입니다. 그렇지 않으면 값은 클라이언트의 IP 주소입니다.  
  
 `<IsPooled>`  
 연결 풀링을 사용하여 연결이 다시 사용될 경우 `1` 입니다. 그렇지 않으면 값은 `0`입니다.  
  
  
