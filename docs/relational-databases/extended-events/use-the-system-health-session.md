---
title: system_health 세션 사용
ms.date: 11/27/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
helpviewer_keywords:
- extended events [SQL Server], system health session
- extended events [SQL Server], system_health session
- system_health session [SQL Server extended events]
- system health session [SQL Server extended events]
ms.assetid: 1e1fad43-d747-4775-ac0d-c50648e56d78
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ab31461888588ee54f1715f5e98ddb0f3b9aa23b
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75246138"
---
# <a name="use-the-system_health-session"></a>system_health 세션 사용

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

system_health 세션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 기본적으로 포함된 확장 이벤트 세션입니다. 이 세션은 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 이 시작될 때 자동으로 시작되며 성능에 별다른 영향을 주지 않고 실행됩니다. 이 세션은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 성능 문제를 해결하는 데 사용할 수 있는 시스템 데이터를 수집합니다. 

> [!IMPORTANT]
> system_health 세션을 중지, 변경 또는 삭제하지 않는 것이 좋습니다. system_health 세션 설정에 대한 변경 내용은 이후 제품 업데이트로 덮어쓸 수 있습니다.
  
이 세션에서 수집하는 정보는 다음과 같습니다.  
  
-   심각도가 20보다 높거나 같은 오류가 발생한 모든 세션의 *sql_text* 및 *session_id*  
  
-   메모리 관련 오류가 발생한 모든 세션의 *sql_text* 및 *session_id* 이러한 오류에는 17803, 701, 802, 8645, 8651, 8657 및 8902가 포함됩니다.  
  
-   잠긴 스케줄러 문제에 대한 기록. 이러한 오류는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에서 오류 17883으로 나타납니다.  
  
-   교착 상태 그래프를 포함하여 검색되는 모든 교착 상태입니다.  
  
-   래치(또는 사용하려는 다른 리소스)로 인해 15초 이상 대기한 모든 세션의 *callstack*, *sql_text* 및 *session_id*  
  
-   잠금으로 인해 30초 이상 대기한 모든 세션의 *callstack*, *sql_text* 및 *session_id*  
  
-   선점형 대기로 인해 오래 동안 대기한 모든 세션의 *callstack*, *sql_text* 및 *session_id* 기간은 대기 유형마다 다릅니다. 선점형 대기는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 외부 API 호출을 대기하는 상황입니다.  
  
-   CLR 할당 및 가상 할당 오류의 *callstack* 및 *session_id*입니다.  
  
-   메모리 브로커, 스케줄러 모니터, 메모리 노드 OOM, 보안 및 연결용 ring buffer 이벤트입니다.  
  
-   `sp_server_diagnostics`의 시스템 구성 요소 결과입니다.  
  
-   *scheduler_monitor_system_health_ring_buffer_recorded*에 의해 수집되는 인스턴스 상태입니다.  
  
-   CLR 할당 실패  
  
-   *connectivity_ring_buffer_recorded*를 사용하는 동안 연결 오류가 발생합니다.  
  
-   *security_error_ring_buffer_recorded*를 사용하는 동안 보안 오류가 발생합니다.  

> [!NOTE]
> 교착 상태에 대한 자세한 내용은 [트랜잭션 잠금 및 행 버전 관리 지침에서 교착 상태](../../relational-databases/sql-server-transaction-locking-and-row-versioning-guide.md#deadlocks)를 참조하세요.   
> SQL 오류 메시지에 대한 자세한 내용은 [데이터베이스 엔진 오류](../../relational-databases/errors-events/database-engine-events-and-errors.md)를 참조하세요.

## <a name="viewing-the-session-data"></a>세션 데이터 보기  
이 세션에서는 링 버퍼 대상 및 이벤트 파일 대상을 사용하여 데이터를 저장합니다. 이벤트 파일 대상은 5MB의 최대 크기 및 4개 파일의 파일 보존 정책으로 구성됩니다. 

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 사용할 수 있는 확장 이벤트 사용자 인터페이스를 사용하여 링 버퍼 대상에서 세션 데이터를 보려면 [SQL Server 확장 이벤트의 대상 데이터 고급 보기 - 라이브 데이터 감시](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md#b3-watch-live-data)를 참조하세요.

[!INCLUDE[tsql](../../includes/tsql-md.md)]을(를) 사용하여 링 버퍼 대상의 세션 데이터를 보려면 다음 쿼리를 사용합니다.  
  
```sql  
SELECT CAST(xet.target_data as xml) 
FROM sys.dm_xe_session_targets xet  
JOIN sys.dm_xe_sessions xe ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'system_health'  
```  
  
이벤트 파일의 세션 데이터를 보려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 사용할 수 있는 확장 이벤트 사용자 인터페이스를 사용합니다. 자세한 내용은 [SQL Server 확장 이벤트의 대상 데이터 고급 보기](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md)를 참조하세요.
  
## <a name="restoring-the-system_health-session"></a>system_health 세션 복원  
system_health 세션을 삭제한 경우 쿼리 편집기에서 **u_tables.sql** 파일을 실행하여 세션을 복원할 수 있습니다. 이 파일은 다음 폴더에 있으며 여기서 **C:** 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로그램 파일을 설치한 드라이브를 나타내며, **MSSQL1x**는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 주 버전을 나타냅니다.  
  
 `C:\Program Files\Microsoft SQL Server\MSSQL1x.\<*instanceid*>\MSSQL\Install`  
  
세션을 복원한 후에는 `ALTER EVENT SESSION` 명령을 사용하거나 개체 탐색기에서 **확장 이벤트** 노드를 사용하여 세션을 시작해야 합니다. 그렇지 않으면 다음에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 다시 시작할 때 세션이 자동으로 시작됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)    
 [확장 이벤트 도구](../../relational-databases/extended-events/extended-events-tools.md)    
 [데이터베이스 엔진 오류](../../relational-databases/errors-events/database-engine-events-and-errors.md)    
 [오류 메시지 카탈로그 뷰 - sys.messages](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md) 
