---
title: Analytics Platform System에서 사용자 세션 | Microsoft Docs "
description: Analytics Platform System의 병렬 데이터 웨어하우스에서 사용자 세션입니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 33bf052e27640ee08784927351579378bffbec2b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63316354"
---
# <a name="user-sessions-in-analytics-platform-system"></a>Analytics Platform System에서 사용자 세션
적절 한 권한이 있는 로그인에는 이러한 작업을 수행 하는 포함 하 여 SQL Server PDW 어플라이언스에 대 한 모든 로그인의 세션을 관리할 수 있습니다.  
  
-   현재 세션을 활성 및 유휴 세션을 포함 하 여 어플라이언스의 보기입니다.  
  
-   세션에 대 한 활성 및 최근 쿼리를 봅니다.  
  
-   활성 세션을 종료 합니다.  
  
이러한 작업 중 하나를 사용 하 여 수행할 수는 [관리자 콘솔을 사용 하 여 어플라이언스 모니터링](monitor-the-appliance-by-using-the-admin-console.md) 또는 [시스템 뷰](tsql-system-views.md) 아래와 같이 SQL 명령을 통해.  
  
두 방법 중 하나를 사용 하 여 세션을 관리 하는 데 필요한 사용 권한을 동일 하 고에 설명 되어 있습니다 [로그인 관리, 사용자 및 데이터베이스 역할에 권한을 부여](grant-permissions.md#grant-permissions-to-manage-logins-users-and-database-roles)합니다.  
  
## <a name="manage-sessions-by-using-the-admin-console"></a>관리 콘솔을 사용 하 여 세션을 관리 합니다.  
  
### <a name="to-view-current-sessions-by-using-the-admin-console"></a>관리 콘솔을 사용 하 여 현재 세션을 보려면  
  
1.  위쪽 메뉴에서 클릭 **세션**합니다.  
  
2.  모든 최근 세션 결과 목록에 표시 됩니다. 'Active' 또는 '유휴' 세션만 보려면 클릭 합니다 **상태** 상태별으로 결과 정렬 하려면 열 머리글입니다.  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-the-admin-console"></a>관리 콘솔을 사용 하 여 세션에 대 한 활성 및 최근 쿼리를 보려면  
  
1.  위쪽 메뉴에서 클릭 **세션**합니다.  
  
2.  결과 목록에서 원하는 세션의 세션 ID를 클릭 합니다.  
  
3.  결과 쿼리 목록 세션에 대 한 최근 쿼리를 보여 줍니다. 쿼리 세부 정보 보기에 대 한 내용은 참조 하세요 [활성 쿼리 모니터링](monitoring-active-queries.md)합니다.  
  
### <a name="to-end-sessions-by-using-the-admin-console"></a>관리 콘솔을 사용 하 여 세션을 종료 하려면  
  
1.  위쪽 메뉴에서 클릭 **세션**합니다.  
  
2.  취소 하려면 세션에 대 한 세션 ID를 찾습니다.  
  
3.  빨간색 클릭 **X** 세션을 종료 하려면 세션 ID의 왼쪽에 있습니다. 'Active' 또는 '유휴'의 상태를 사용 하 여 세션에는 빨간색 해야만 **X**;만 이러한 세션을 종료할 수 있습니다.  
  
## <a name="manage-sessions-by-using-system-views-and-sql-commands"></a>시스템 뷰 및 SQL 명령을 사용 하 여 세션을 관리 합니다.  
  
### <a name="to-view-current-sessions-by-using-system-views"></a>시스템 뷰를 사용 하 여 현재 세션을 보려면  
사용 하 여 [sys.dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) 현재 세션의 목록을 생성 합니다.  
  
이 예제에서는 'Active' 또는 '유휴'의 상태를 사용 하 여 모든 세션에 대 한 session_id, login_name, 및 상태를 반환합니다.  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions WHERE status='Active' OR status='Idle';  
```  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-system-views"></a>시스템 뷰를 사용 하 여 세션에 대 한 활성 및 최근 쿼리를 보려면  
세션과 연결 된 활성 및 최근에 완료 된 쿼리를 보려면 사용 하는 [sys.dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) 하 고 [sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md) 뷰. 이 쿼리는 모든 활성 또는 유휴 세션의 각 세션 ID와 연결 된 모든 활성 또는 최근 쿼리 목록 반환  
  
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
사용 합니다 [KILL](../t-sql/language-elements/kill-transact-sql.md) 명령을 현재 세션을 종료 합니다. 사용 하 여 가져올 수 있는 프로세스를 종료 하려면 세션 ID가 필요 합니다 [sys.dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) 보기.  
  
이 예제에서는 login_name, session_id에 및 로그인 이름을 기반으로 세션을 찾을 수 있는 상태 값을 선택 합니다.  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions;  
```  
  
KILL 명령을 사용 하 여 '활성' 또는 '유휴' 상태를 사용 하 여 세션을 종료할 수 있습니다.  
  
```sql  
KILL 'SID137';  
```  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
