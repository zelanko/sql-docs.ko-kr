---
title: 사용자 세션
description: 분석 플랫폼 시스템의 병렬 데이터 웨어하우스의 사용자 세션입니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: a0e5b338cc616be214ef39527551ee4a6ffd8f56
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74399407"
---
# <a name="user-sessions-in-analytics-platform-system"></a>분석 플랫폼 시스템의 사용자 세션
적절 한 권한이 있는 로그인은 다음 작업 수행을 포함 하 여 SQL Server PDW 어플라이언스의 모든 로그인에 대 한 세션을 관리할 수 있습니다.  
  
-   활성 및 유휴 세션을 모두 포함 하 여 어플라이언스의 현재 세션을 확인 합니다.  
  
-   세션에 대 한 활성 및 최근 쿼리를 봅니다.  
  
-   활성 세션을 종료 합니다.  
  
이러한 작업은 아래와 같이 [관리 콘솔을 사용 하 여 어플라이언스 모니터링](monitor-the-appliance-by-using-the-admin-console.md) 또는 SQL 명령을 통해 [시스템 뷰](tsql-system-views.md) 를 사용 하 여 수행할 수 있습니다.  
  
두 방법을 사용 하 여 세션을 관리 하는 데 필요한 권한은 동일 하며 [로그인, 사용자 및 데이터베이스 역할을 관리 하는 권한 부여](grant-permissions.md#grant-permissions-to-manage-logins-users-and-database-roles)에 설명 되어 있습니다.  
  
## <a name="manage-sessions-by-using-the-admin-console"></a>관리 콘솔을 사용 하 여 세션 관리  
  
### <a name="to-view-current-sessions-by-using-the-admin-console"></a>관리 콘솔을 사용 하 여 현재 세션을 보려면  
  
1.  상단 메뉴에서 **세션**을 클릭 합니다.  
  
2.  결과 목록에는 모든 최근 세션이 표시 됩니다. ' 활성 ' 또는 ' 유휴 ' 세션만 보려면 **상태** 열 머리글을 클릭 하 여 상태별로 결과를 정렬 합니다.  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-the-admin-console"></a>관리 콘솔을 사용 하 여 세션에 대 한 활성 및 최근 쿼리를 보려면  
  
1.  상단 메뉴에서 **세션**을 클릭 합니다.  
  
2.  결과 목록에서 원하는 세션의 세션 ID를 클릭 합니다.  
  
3.  결과 쿼리 목록에는 세션에 대 한 최근 쿼리가 표시 됩니다. 쿼리 세부 정보를 보는 방법에 대 한 자세한 내용은 [활성 쿼리 모니터링](monitoring-active-queries.md)을 참조 하세요.  
  
### <a name="to-end-sessions-by-using-the-admin-console"></a>관리 콘솔을 사용 하 여 세션을 종료 하려면  
  
1.  상단 메뉴에서 **세션**을 클릭 합니다.  
  
2.  취소할 세션의 세션 ID를 찾습니다.  
  
3.  세션을 종료 하려면 세션 ID 왼쪽에 있는 빨간색 **X** 를 클릭 합니다. 상태가 ' 활성 ' 또는 ' 유휴 ' 인 세션만 빨간색 **X**가 됩니다. 이러한 세션만 종료할 수 있습니다.  
  
## <a name="manage-sessions-by-using-system-views-and-sql-commands"></a>시스템 뷰 및 SQL 명령을 사용 하 여 세션 관리  
  
### <a name="to-view-current-sessions-by-using-system-views"></a>시스템 뷰를 사용 하 여 현재 세션을 보려면  
현재 세션의 목록을 생성 하려면 [dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) 를 사용 합니다.  
  
이 예에서는 상태가 ' 활성 ' 또는 ' 유휴 ' 인 모든 세션에 대 한 session_id, login_name 및 상태를 반환 합니다.  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions WHERE status='Active' OR status='Idle';  
```  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-system-views"></a>시스템 뷰를 사용 하 여 세션에 대 한 활성 및 최근 쿼리를 보려면  
세션과 연결 된 활성 및 최근에 완료 된 쿼리를 보려면 [dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) 및 [dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md) 뷰를 사용 합니다. 이 쿼리는 모든 활성 또는 유휴 세션의 목록과 각 세션 ID와 연결 된 활성 또는 최근 쿼리 목록을 반환 합니다.  
  
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
[KILL](../t-sql/language-elements/kill-transact-sql.md) 명령을 사용 하 여 현재 세션을 종료 합니다. 종료할 프로세스의 세션 ID가 필요 합니다 .이 ID는 [sys. dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) 뷰를 사용 하 여 가져올 수 있습니다.  
  
이 예에서는 login_name, session_id 및 상태 값을 선택 하 여 로그인 이름을 기준으로 세션을 찾습니다.  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions;  
```  
  
' 활성 ' 또는 ' 유휴 ' 상태의 세션은 KILL 명령을 사용 하 여 종료할 수 있습니다.  
  
```sql  
KILL 'SID137';  
```  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
