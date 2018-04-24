---
title: 분석 플랫폼 시스템에 사용자 세션이 | "Microsoft Docs
description: 병렬 데이터 웨어하우스 분석 플랫폼 시스템에에서 사용자 세션이 있습니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: fc2e759d77953f739d77f6ad4eb371cc9747efdc
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/19/2018
---
# <a name="user-sessions-in-analytics-platform-system"></a>분석 플랫폼 시스템에서 사용자 세션
적절 한 사용 권한 가진 로그인 이러한 작업을 수행 하는 포함 하는 SQL Server PDW 어플라이언스의 모든 로그인의 세션을 관리할 수 있습니다.  
  
-   활성 및 유휴 세션 포함 하 여 장치에서 현재 세션을 확인 합니다.  
  
-   세션에 대 한 활성 상태이 고 최근 쿼리를 봅니다.  
  
-   활성 세션을 종료 합니다.  
  
이러한 작업 중 하나를 사용 하 여 수행할 수 있습니다는 [관리 콘솔을 사용 하 여 어플라이언스에 모니터링](monitor-the-appliance-by-using-the-admin-console.md) 또는 [시스템 뷰](tsql-system-views.md) 아래와 같이 SQL 명령을 통해 합니다.  
  
두 방법 중 하나를 사용 하 여 세션을 관리 하는 데 필요한 권한을 동일 하 고에 설명 된 [로그인 관리, 사용자 및 데이터베이스 역할에 권한을 부여](grant-permissions.md#grant-permissions-to-manage-logins-users-and-database-roles)합니다.  
  
## <a name="manage-sessions-by-using-the-admin-console"></a>관리 콘솔을 사용 하 여 세션을 관리 합니다.  
  
### <a name="to-view-current-sessions-by-using-the-admin-console"></a>관리 콘솔을 사용 하 여 현재 세션을 보려면  
  
1.  상단 메뉴에서 클릭 **세션**합니다.  
  
2.  결과 목록에는 최근에 사용한 세션을 모두 표시 됩니다. 'Active' 또는 '유휴' 세션을 보려면 클릭는 **상태** 상태별으로 결과 정렬 하려면 열 머리글입니다.  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-the-admin-console"></a>관리 콘솔을 사용 하 여 세션에 대 한 활성 상태이 고 최근 쿼리를 보려면  
  
1.  상단 메뉴에서 클릭 **세션**합니다.  
  
2.  결과 목록에서 원하는 세션의 세션 ID를 클릭 합니다.  
  
3.  결과 쿼리 목록 세션에 대 한 최근 쿼리를 보여 줍니다. 쿼리 세부 정보를 보는 방법은 참조 하세요. [활성 쿼리 모니터링](monitoring-active-queries.md)합니다.  
  
### <a name="to-end-sessions-by-using-the-admin-console"></a>관리 콘솔을 사용 하 여 세션을 종료 하려면  
  
1.  상단 메뉴에서 클릭 **세션**합니다.  
  
2.  취소 하는 세션에 대 한 세션 ID를 찾습니다.  
  
3.  빨간색 클릭 **X** 세션을 종료 하려면 세션 ID의 왼쪽에 있습니다. 'Active' 또는 '유휴'의 상태를 사용 하 여 세션에 빨간색 갖습니다만 **X**만 이러한 세션을 종료할 수 있습니다.  
  
## <a name="manage-sessions-by-using-system-views-and-sql-commands"></a>시스템 뷰 및 SQL 명령을 사용 하 여 세션을 관리 합니다.  
  
### <a name="to-view-current-sessions-by-using-system-views"></a>시스템 뷰를 사용 하 여 현재 세션을 보려면  
사용 하 여 [sys.dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) 현재 세션의 목록을 생성 합니다.  
  
이 예에서는 'Active' 또는 '유휴' 상태와 함께 모든 세션에 대 한 세션 id, login_name, 및 상태를 반환합니다.  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions WHERE status='Active' OR status='Idle';  
```  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-system-views"></a>시스템 뷰를 사용 하 여 세션에 대 한 활성 상태이 고 최근 쿼리를 보려면  
세션과 연결 된 활성 상태이 고 최근에 완료 된 쿼리를 보려면 사용 하 여 [sys.dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) 및 [sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md) 뷰. 이 쿼리는 모든 활성 또는 유휴 세션을 각 세션 ID와 연결 된 모든 활성 또는 최근 쿼리 목록이 반환 합니다.  
  
```sql  
SELECT es.session_id, es.login_name, es.status AS sessionStatus,   
er.request_id, er.status AS requestStatus, er.command   
FROM sys.dm_pdw_exec_sessions es   
LEFT OUTER JOIN sys.dm_pdw_exec_requests er   
ON (es.session_id=er.session_id)   
WHERE (es.status='Active' OR es.status='Idle') AND   
(er.status!= 'Completed' AND er.status!= 'Failed' AND er.status!= 'Cancelled');  
```  
  
### <a name="to-end-sessions-by-using-sql-commands"></a>SQL 명령을 사용 하 여 세션을 종료 하려면  
사용 하 여는 [KILL](../t-sql/language-elements/kill-transact-sql.md) 명령을 현재 세션을 종료할 수 있습니다. 프로세스의 종료를 사용 하 여 가져올 수에 대 한 세션 ID가 필요는 [sys.dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) 보기.  
  
이 예에서는 login_name, session_id, 및 로그인 이름을 기반으로 세션을 찾을 수 있는 상태 값을 선택 합니다.  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions;  
```  
  
KILL 명령을 사용 하 여 'Active' 또는 '유휴' 상태를 사용 하 여 세션을 종료할 수 있습니다.  
  
```sql  
KILL 'SID137';  
```  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
