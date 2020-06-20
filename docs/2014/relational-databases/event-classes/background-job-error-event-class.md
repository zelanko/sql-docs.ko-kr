---
title: Background Job Error 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Background Job Error event class
ms.assetid: 9e6d2a0e-919d-4fe2-a306-b20b8d41c197
author: stevestein
ms.author: sstein
ms.openlocfilehash: 11aeaa058209eebd93b83fc812db2173167bf65a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85030773"
---
# <a name="background-job-error-event-class"></a>Background Job Error 이벤트 클래스
  **Background Job Error** 이벤트 클래스는 백그라운드 작업이 비정상적으로 종료되었을 때 발생합니다. 이 경우 시스템 관리자의 조치가 필요할 수 있습니다.  
  
## <a name="background-job-error-event-class-data-columns"></a>Background Job Error 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|작업에서 지정한 데이터베이스의 ID입니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|yes|  
|**DatabaseName**|**nvarchar**|사용자 문이 실행되는 데이터베이스의 이름입니다.|35|yes|  
|**오류**|**int**|마지막 시도의 오류 번호입니다(**EventSubClass** 1에만 해당).|31|yes|  
|**EventClass**|**int**|이벤트 유형 = 193|27|예|  
|**EventSequence**|**int**|요청 내의 지정된 이벤트 시퀀스입니다.|51|예|  
|**EventSubClass**|**int**|이벤트 하위 클래스의 유형입니다.<br /><br /> 1 = 실패 후 백그라운드 작업 포기 중<br /><br /> 2 = 백그라운드 작업 삭제됨 - 큐가 꽉 참<br /><br /> 3 = 백그라운드 작업이 오류를 반환했음|21|yes|  
|**IndexID**|**int**|이벤트에 의해 영향 받는 개체의 인덱스 ID입니다. 개체의 인덱스 ID를 확인하려면 **sysindexes** 시스템 테이블의 **indid** 열을 사용하십시오.|24|yes|  
|**IntegerData**|**int**|작업이 시도한 횟수입니다(**EventSubClass** 1에만 해당).|25|yes|  
|**IntegerData2**|**int**|작업 시퀀스 번호입니다.|55|yes|  
|**Exchange Spill**|**int**|시스템이 할당한 개체의 ID입니다.|22|yes|  
|**SessionLoginName**|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 **SessionLoginName** 은 Login1을 표시하고 **LoginName** 은 Login2를 표시합니다. 이 열에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 로그인이 모두 표시됩니다.|64|yes|  
|**Severity**|**int**|마지막 시도에서 발생한 오류의 심각도입니다(**EventSubClass** 1에만 해당).|20|yes|  
|**StartTime**|**datetime**|이 작업이 만들어진 시간입니다.|14|yes|  
|**State**|**int**|마지막 시도에서 발생한 오류의 상태입니다(**EventSubClass** 1에만 해당).|30|yes|  
|**TextData**|**ntext**|이벤트 하위 클래스 값의 텍스트 설명입니다.|1|yes|  
|**형식**|**int**|작업 유형입니다.|57|yes|  
  
## <a name="see-also"></a>참고 항목  
 [확장 이벤트](../extended-events/extended-events.md)   
 [sp_trace_setevent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Auto Stats 이벤트 클래스](auto-stats-event-class.md)  
  
  
