---
title: "병렬 데이터 웨어하우스에 대 한 로드 모니터"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "활성 상태이 고 최근를 모니터링할 수 있습니다 [dwloader](dwloader.md) Analytics Platform System (APS) 관리 콘솔 또는 병렬 데이터 웨어하우스 (PDW) 시스템 뷰를 사용 하 여 로드 합니다."
ms.date: 10/20/2016
ms.topic: article
ms.assetid: c0c55c16-00bc-4676-8970-a8e10b3e9408
caps.latest.revision: "6"
ms.openlocfilehash: a172b35934f35054bbe528894b04d0d69a814910
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="monitor-loads"></a>모니터 로드
활성 상태이 고 최근를 모니터링할 수 있습니다 [dwloader](dwloader.md) Analytics Platform System (APS) 관리 콘솔 또는 병렬 데이터 웨어하우스 (PDW)를 사용 하 여 로드 [시스템 뷰](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-reference-tsql-system-views/)합니다. 
  
> [!TIP]  
> 일부 부하 INSERT 문 또는 SQL 문을 사용 하 여 부하를 수행 하는 비즈니스 인텔리전스 도구를 사용 하 여 시작 됩니다. 

<!-- MISSING LINKS
To monitor this type of load, see [Monitoring Active Queries](monitor-active-queries.md).  
-->
  
## <a name="prerequisites"></a>필수 구성 요소  
부하를 모니터링 하는 데 사용 하는 방법에 관계 없이 로그인에는 기본 데이터 원본에 액세스할 수 있는 권한이 있어야 합니다. 

<!-- MISSING LINKS
For the permissions to grant, see “Use All of the Admin Console” in [Grant Permissions to Use the Admin Console](grant-permissions-admin-console.md). 

--> 
  
## <a name="monitoring-loads"></a>부하를 모니터링합니다.  
다음 섹션에서는 부하를 모니터링 하는 방법에 설명 합니다.  
  
### <a name="to-monitor-loads-by-using-the-admin-console"></a>관리 콘솔을 사용 하 여 부하를 모니터링 하려면  
  
1.  관리 콘솔에 로그온 합니다. <!-- MISSING LINKS See [Monitor the Appliance by Using the Admin Console;](monitor-admin-console.md) for instructions. --> 
  
2.  상단 메뉴에서 클릭 **로드**합니다. 최근에 사용한 모든 표시 하는 정렬 가능한 테이블 및 활성 로드 및 로드 완료 되었거나 아직 활성화 되어 있는지 여부와 같은 추가 정보를 확인할 수 있습니다. 행을 정렬 하려면 열 머리글을 클릭 합니다.  
  
3.  특정 부하에 대 한 추가 세부 정보를 보려면 클릭 부하 **ID** 왼쪽된 열에 있습니다. 자세히 보기에는 부하의 각 단계에서 진행률을 볼 수 있습니다.  
  
관리 콘솔에 표시 되는 부하에 대 한 메타 데이터에 정보에 대 한 이러한 시스템 뷰를 참조 하십시오.  
  
-   [sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)  
  
-   [sys.pdw_loader_run_stages](https://msdn.microsoft.com/library/mt203879.aspx.md)  
  
-   [sys.pdw_loader_backup_runs](../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
  
-   [sys.pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
  
### <a name="to-monitor-loads-by-using-system-views"></a>시스템 뷰를 사용 하 여 부하를 모니터링 하려면  
SQL Server PDW 뷰를 사용 하 여 활성 상태이 고 최근 부하를 모니터링 하려면 다음 단계를 수행 합니다. 사용 되는 각 시스템 뷰당 한의 열에 잠재적인 값의 보기에서 반환 된 정보에 대 한 해당 보기에 대 한 설명서를 참조 합니다.  
  
1.  찾을 `request_id` 에서 부하에 대 한는 [sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md) 로더 명령줄에서 검색 하 여 보기는 `command` 이 보기에 대 한 열입니다.  
  
    다음 명령은 명령 텍스트 및 현재 상태를 반환 하는 예를 들어과 `request_id`합니다.  
  
    ```sql  
    SELECT request_id, status, command FROM sys.dm_pdw_exec_requests;  
    ```  
  
2.  사용 하 여는 `request_id` 를 사용 하 여 부하에 대 한 추가 정보를 검색 하는 [sys.pdw_loader_run_stages](../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md) , 및 [sys.pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md) 뷰. 예를 들어 다음 쿼리에서 반환 된 `run_id` 처리 된 행의 수에 대 한 정보 및 시작, 종료 및 지속 시간 부하를 더한 모든 오류에 대 한 정보:  
  
    ```sql  
    SELECT lbr.run_id,   
    er.submit_time, er.end_time, er.total_elapsed_time, er.error_id, lbr.rows_processed, lbr.rows_rejected, lbr.rows_inserted   
    FROM sys.dm_pdw_exec_requests er   
    LEFT OUTER JOIN   
    sys.pdw_loader_backup_runs lbr   
    ON (er.request_id=lbr.requst_id)   
    WHERE er.request_id=’12738’;  
    ```  
  
<!-- MISSING LINKS

## See Also  
[Common metadata query examples](metadata-query-examples.md)
-->  
  
