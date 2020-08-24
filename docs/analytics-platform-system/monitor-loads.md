---
title: 로드 모니터링
description: APS (분석 플랫폼 시스템) 관리 콘솔 또는 PDW (병렬 데이터 웨어하우스) 시스템 뷰를 사용 하 여 활성 및 최근 로드를 모니터링 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6bc64949b0e636a6c64e7b0ef576613f6e02c5c2
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777722"
---
# <a name="monitor-loads-into-parallel-data-warehouse"></a>병렬 데이터 웨어하우스로 부하 모니터링
APS (분석 플랫폼 시스템) 관리 콘솔 또는 PDW (병렬 데이터 웨어하우스) [시스템 뷰](/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)를 사용 하 여 활성 및 최근 [dwloader](dwloader.md) 로드를 모니터링 합니다. 
  
> [!TIP]  
> 일부 로드는 SQL 문을 사용 하 여 로드를 수행 하는 INSERT 문 또는 비즈니스 인텔리전스 도구를 사용 하 여 시작 됩니다. 

<!-- MISSING LINKS
To monitor this type of load, see [Monitoring Active Queries](monitor-active-queries.md).  
-->
  
## <a name="prerequisites"></a>필수 구성 요소  
부하를 모니터링 하는 데 사용 되는 방법에 관계 없이 로그인에는 기본 데이터 원본에 대 한 액세스 권한이 있어야 합니다. 

<!-- MISSING LINKS
For the permissions to grant, see "Use All of the Admin Console" in [Grant Permissions to Use the Admin Console](grant-permissions-admin-console.md). 

--> 
  
## <a name="monitoring-loads"></a>모니터링 로드  
다음 섹션에서는 부하를 모니터링 하는 방법을 설명 합니다.  
  
### <a name="to-monitor-loads-by-using-the-admin-console"></a>관리 콘솔을 사용 하 여 부하를 모니터링 하려면  
  
1.  관리 콘솔에 로그온 합니다. <!-- MISSING LINKS See [Monitor the Appliance by Using the Admin Console;](monitor-admin-console.md) for instructions. --> 
  
2.  상단 메뉴에서 **로드**를 클릭 합니다. 모든 최근 및 활성 로드 뿐만 아니라 부하가 완료 되었거나 아직 활성 상태 인지 여부 등의 추가 정보를 보여 주는 정렬 가능한 테이블이 표시 됩니다. 행을 정렬 하려면 열 머리글을 클릭 합니다.  
  
3.  특정 부하에 대 한 추가 세부 정보를 보려면 왼쪽 열에서 로드 **ID** 를 클릭 합니다. 자세히 보기에서 각 로드 단계에 대 한 진행률을 볼 수 있습니다.  
  
관리 콘솔에 표시 되는 부하에 대 한 메타 데이터에 대 한 자세한 내용은 다음 시스템 뷰를 참조 하세요.  
  
-   [sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)  
  
-   [sys.pdw_loader_run_stages](../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md?view=aps-pdw-2016-au7)  
  
-   [sys.pdw_loader_backup_runs](../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
  
-   [sys.pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
  
### <a name="to-monitor-loads-by-using-system-views"></a>시스템 뷰를 사용 하 여 로드를 모니터링 하려면  
SQL Server PDW 보기를 사용 하 여 활성 및 최근 로드를 모니터링 하려면 다음 단계를 수행 합니다. 사용 되는 각 시스템 뷰에 대해 뷰에서 반환 되는 열 및 잠재적 값에 대 한 자세한 내용은 해당 보기에 대 한 설명서를 참조 하십시오.  
  
1.  `request_id`이 보기의 열에서 로더 명령줄을 찾아 [dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md) 뷰의 로드를 찾습니다 `command` .  
  
    예를 들어 다음 명령은 명령 텍스트 및 현재 상태와을 반환 합니다 `request_id` .  
  
    ```sql  
    SELECT request_id, status, command FROM sys.dm_pdw_exec_requests;  
    ```  
  
2.  `request_id` [Pdw_loader_run_stages](../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md) 및 [pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md) 뷰를 사용 하 여 로드에 대 한 추가 정보를 검색 하려면를 사용 합니다. 예를 들어 다음 쿼리는 `run_id` 로드의 시작, 종료 및 기간 및 오류에 대 한 정보와 처리 된 행 수에 대 한 정보를 반환 합니다.  
  
    ```sql  
    SELECT lbr.run_id,   
    er.submit_time, er.end_time, er.total_elapsed_time, er.error_id, lbr.rows_processed, lbr.rows_rejected, lbr.rows_inserted   
    FROM sys.dm_pdw_exec_requests er   
    LEFT OUTER JOIN   
    sys.pdw_loader_backup_runs lbr   
    ON (er.request_id=lbr.requst_id)   
    WHERE er.request_id='12738';  
    ```  
  
<!-- MISSING LINKS

## See Also  
[Common metadata query examples](metadata-query-examples.md)
-->  
