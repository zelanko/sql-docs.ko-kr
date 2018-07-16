---
title: Database Mirroring State Change 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- event notifications [SQL Server], database mirroring
- database mirroring [SQL Server], event notifications
- Database Mirroring State Change event class
ms.assetid: f936a99e-2a81-4768-8177-5c969bbe2e04
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e635ff34d280affd22d5f0d7854b3c8d7f1a717d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37257345"
---
# <a name="database-mirroring-state-change-event-class"></a>Database Mirroring State Change 이벤트 클래스
  **Database Mirroring State Change** 이벤트 클래스는 미러된 데이터베이스의 상태가 변경되는 시기를 나타냅니다. 미러된 데이터베이스의 상태를 모니터링하는 추적에 이 이벤트 클래스를 포함시키십시오.  
  
 **Database Mirroring State Change** 이벤트 클래스가 추적에 포함되면 상대적인 오버헤드가 줄어듭니다. 오버헤드는 미러된 데이터베이스의 상태가 증가하면 커질 수 있습니다.  
  
## <a name="data-database-mirroring-state-change-event-class-data-columns"></a>Database Mirroring State Change 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|USE *database* 문에서 지정한 데이터베이스 ID이거나, 지정한 인스턴스에 대해 USE *database* 문을 실행하지 않은 경우 기본 데이터베이스입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ServerName **데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면** 에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|**DatabaseName**|**nvarchar**|미러된 데이터베이스의 이름입니다.|35|예|  
|**EventClass**|**int**|이벤트 유형 = 167|27|아니요|  
|**EventSequence**|**int**|일괄 처리 내의 이벤트 클래스 순서입니다.|51|아니요|  
|**IntegerData**|**int**|이전 상태의 ID입니다.|25|예|  
|**IsSystem**|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|예|  
|**LoginSid**|**image**|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 **sys.server_principals** 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|예|  
|**RequestID**|**int**|문을 포함하는 요청의 ID입니다.|49|예|  
|**데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면**|**nvarchar**|추적 중인 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|아니요|  
|**SessionLoginName**|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 **SessionLoginName** 은 Login1을 표시하고 **LoginName** 은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|예|  
|**SPID**|**int**|이벤트가 발생한 세션의 ID입니다.|12|예|  
|**StartTime**|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|**State**|**int**|새 미러링 상태의 ID입니다. 값은 다음과 같습니다.<br /><br /> 0 = Null 알림<br /><br /> 1 = 미러링 모니터와 함께 주 서버 동기화<br /><br /> 2 = 미러링 모니터 없이 주 서버 동기화<br /><br /> 3 = 미러링 모니터와 함께 미러 동기화<br /><br /> 4 = 미러링 모니터 없이 미러 동기화<br /><br /> 5 = 주 서버 연결 손실<br /><br /> 6 = 미러 연결 손실<br /><br /> 7 = 수동 장애 조치<br /><br /> 8 = 자동 장애 조치<br /><br /> 9 = 미러링 일시 중지됨<br /><br /> 10 = 쿼럼 없음<br /><br /> 11 = 미러 동기화 중<br /><br /> 12 = 주 서버 노출 실행 중|30|예|  
|**TextData**|**ntext**|상태 변경에 대한 설명입니다.|1|예|  
|**TransactionID**|**bigint**|시스템이 할당한 트랜잭션의 ID입니다.|4|예|  
  
## <a name="see-also"></a>관련 항목  
 [확장 이벤트](../extended-events/extended-events.md)   
 [sp_trace_setevent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
