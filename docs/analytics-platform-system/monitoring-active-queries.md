---
title: 활성 쿼리 모니터링
description: 관리 콘솔과 병렬 데이터 웨어하우스 시스템 뷰를 사용 하 여 분석 플랫폼 시스템에서 활성 쿼리를 모니터링할 수 있습니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 9157db745b999711966f0019747ba1d61823569e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74400909"
---
# <a name="monitoring-active-queries---parallel-data-warehouse"></a>활성 쿼리 모니터링-병렬 데이터 웨어하우스
이 문서에서는 관리 콘솔과 SQL Server PDW 시스템 뷰를 사용 하 여 활성 쿼리를 모니터링 하는 방법을 보여 줍니다. 이러한 도구에 대 한 자세한 내용은 관리 콘솔 및 [시스템 뷰](tsql-system-views.md) [를 사용 하 여 어플라이언스 모니터링](monitor-the-appliance-by-using-the-admin-console.md) 을 참조 하세요.  
  
## <a name="prerequisites"></a>사전 요구 사항  
활성 쿼리를 모니터링 하는 데 사용 하는 방법에 관계 없이 로그인에는 [관리 콘솔을 사용할 수 있는 권한 부여](grant-permissions.md#grant-permissions-to-use-the-admin-console)에서 "모든 관리 콘솔 사용"에 설명 된 사용 권한이 있어야 합니다.  
  
## <a name="PermsAdminConsole"></a>활성 쿼리 모니터링  
관리 콘솔과 SQL Server PDW 시스템 뷰는 모두 활성 쿼리를 모니터링 하는 데 사용할 수 있습니다. 아래의 지침을 따르세요.  
  
### <a name="to-monitor-active-queries-by-using-the-admin-console"></a>관리 콘솔을 사용 하 여 활성 쿼리를 모니터링 하려면  
  
1.  관리 콘솔에 로그온 합니다. 지침은 [관리 콘솔을 사용 하 여 어플라이언스 모니터링](monitor-the-appliance-by-using-the-admin-console.md) 을 참조 하세요.  
  
2.  상단 메뉴에서 **쿼리**를 클릭 합니다. 여기에는 쿼리를 제출한 로그인, 쿼리의 시작 및 종료 시간, 쿼리의 현재 상태를 포함 하 여 어플라이언스의 최신 쿼리에 대 한 기본 정보가 포함 된 테이블이 표시 됩니다.  
  
3.  쿼리 명령을 보려면 해당 행의 왼쪽 열에 있는 쿼리 ID 위로 마우스 포인터를 가져갑니다.  
  
    특정 쿼리에 대 한 자세한 정보를 보려면 쿼리 ID를 클릭 합니다. 쿼리 실행의 각 단계에 대 한 상태 정보와 함께 전체 쿼리 및 쿼리 계획을 포함 하는 정보가 표시 됩니다. 오류가 반환 된 경우 오류에 대 한 자세한 정보를 볼 수도 있습니다. <!-- MISSING LINKS See [Understanding Query Plans &#40;SQL Server PDW&#41;](../sqlpdw/understanding-query-plans-sql-server-pdw.md) for information on how to interpret the query plan information available in the Admin Console.  -->
  
### <a name="to-monitor-active-queries-by-using-the-system-views"></a>시스템 뷰를 사용 하 여 활성 쿼리를 모니터링 하려면  
쿼리를 모니터링 하는 데 사용 되는 기본 시스템 뷰는 [sys. dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)입니다. 이 시스템 뷰를 사용 하 여 `request_id` 쿼리 텍스트를 기반으로 하는 활성 또는 최근 쿼리를 찾을 수 있습니다.  
  
예를 들어 다음 쿼리는 `request_id` `status` `memberAddresses` 테이블에서 모든 열을 선택 하는 쿼리에 대해 및 현재를 찾습니다.  
  
```sql  
SELECT request_id, command, status   
FROM sys.dm_pdw_exec_requests   
WHERE command   
LIKE '%SELECT * FROM db1..memberAddresses%';  
```  
  
쿼리를 `request_id` 확인 한 후에는 `dm_pdw_exec_requests` 테이블의 다른 정보를 사용 하 여 쿼리 처리 방법을 확인 하거나, [dm_pdw_request_steps](../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md) 를 사용 하 여 쿼리 실행에 대 한 개별 쿼리 단계의 상태를 확인 합니다.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
