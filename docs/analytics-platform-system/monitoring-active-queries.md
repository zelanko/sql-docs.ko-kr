---
title: 활성 쿼리-병렬 데이터 웨어하우스 모니터링 | Microsoft Docs
description: Analytics Platform System에 대 한 활성 쿼리를 모니터링 하 고 관리자 콘솔 및 병렬 데이터 웨어하우스 시스템 뷰를 사용 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d2b1ee84b2ae738d7790e1238176331a221ac473
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62640010"
---
# <a name="monitoring-active-queries---parallel-data-warehouse"></a>활성 쿼리-병렬 데이터 웨어하우스를 모니터링합니다.
이 문서에서는 관리 콘솔 및 SQL Server PDW 시스템 뷰를 사용 하 여 활성 쿼리를 모니터링 하는 방법을 보여 줍니다. 참조 [관리자 콘솔을 사용 하 여 어플라이언스 모니터링](monitor-the-appliance-by-using-the-admin-console.md) 하 고 [시스템 뷰](tsql-system-views.md) 이러한 도구에 대 한 정보에 대 한 합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
활성 쿼리를 모니터링 하는 데 사용 하는 방법에 관계 없이 로그인에서 사용 하 여 모든의 the Admin "콘솔"에 설명 된 권한이 있어야 합니다 [관리 콘솔을 사용할 수 있는 권한을 부여](grant-permissions.md#grant-permissions-to-use-the-admin-console)합니다.  
  
## <a name="PermsAdminConsole"></a>활성 쿼리 모니터링  
관리 콘솔 및 SQL Server PDW 시스템 뷰를 모두 사용할 수 활성 쿼리를 모니터링 합니다. 아래 지침을 따르세요.  
  
### <a name="to-monitor-active-queries-by-using-the-admin-console"></a>관리 콘솔을 사용 하 여 활성 쿼리를 모니터링 하려면  
  
1.  관리 콘솔에 로그온 합니다. 참조 [관리자 콘솔을 사용 하 여 어플라이언스 모니터링](monitor-the-appliance-by-using-the-admin-console.md) 지침에 대 한 합니다.  
  
2.  위쪽 메뉴에서 클릭 **쿼리**합니다. 쿼리 및 쿼리의 현재 상태에 대 한 시작 및 종료 시간, 쿼리를 제출한 로그인을 포함 하 여 어플라이언스에서 최신 쿼리에 대 한 기본 정보를 사용 하 여 테이블을 표시 됩니다.  
  
3.  쿼리 ID를 해당 행의 왼쪽된 열 위로 마우스 포인터를 가져가면 쿼리 명령을 확인할 수 있습니다.  
  
    특정 쿼리에 대 한 자세한 내용은 하려면 쿼리 id입니다. 전체 쿼리 및 쿼리 실행의 각 단계에 대 한 상태 정보를 사용 하 여 쿼리 계획을 포함 하는 정보가 표시 됩니다. 모든 오류를 반환 하는 경우에 오류 세부 정보를 볼 수 있습니다. <!-- MISSING LINKS See [Understanding Query Plans &#40;SQL Server PDW&#41;](../sqlpdw/understanding-query-plans-sql-server-pdw.md) for information on how to interpret the query plan information available in the Admin Console.  -->
  
### <a name="to-monitor-active-queries-by-using-the-system-views"></a>시스템 뷰를 사용 하 여 활성 쿼리 모니터링  
쿼리를 모니터링 하는 데 기본 시스템 뷰 [sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)합니다. 이 시스템 뷰를 사용 하 여 찾을 수는 `request_id` 는 활성 또는 최근 쿼리의 쿼리 텍스트를 기반 합니다.  
  
예를 들어 다음 쿼리를 찾습니다는 `request_id` 및 현재 `status` 에서 모든 열을 선택 하는 모든 쿼리에 `memberAddresses` 테이블입니다.  
  
```sql  
SELECT request_id, command, status   
FROM sys.dm_pdw_exec_requests   
WHERE command   
LIKE '%SELECT * FROM db1..memberAddresses%';  
```  
  
후는 `request_id` 되었습니다 기타 정보를 사용 하 여 쿼리를 식별 합니다 `dm_pdw_exec_requests` 쿼리 처리에 대 한 테이블이 나 사용 하 여 [sys.dm_pdw_request_steps](../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md) 개별 쿼리 상태를 보려면 쿼리 실행에 대 한 단계입니다.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
