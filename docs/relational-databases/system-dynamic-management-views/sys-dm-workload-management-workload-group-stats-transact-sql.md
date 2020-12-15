---
description: sys.dm_workload_management_workload_groups_stats (Transact-sql)
title: sys.dm_workload_management_workload_groups_stats (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 11/02/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
monikerRange: = azure-sqldw-latest
ms.openlocfilehash: 89daf919af43c130c23477596e34d6a19654fd12
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97474764"
---
# <a name="sysdm_workload_management_workload_groups_stats-transact-sql"></a>sys.dm_workload_management_workload_groups_stats (Transact-sql)
[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

에서 작업 그룹 통계 및 작업 그룹의 유효 값을 반환 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|group_id|**int**|작업 그룹의 고유한 ID입니다.||
|name|**sysname**|작업 그룹의 이름입니다.||
|statistics_start_time|**datetime**|작업 그룹에 대해 통계 수집이 시작 된 시간입니다.  작업 그룹을 만들거나 인스턴스가 일시 중지 또는 크기 조정 된 경우 값은입니다.||
|total_request_count|**bigint**|작업 그룹에서 완료된 요청의 누적 수입니다.||
|total_shared_resource_reqeusts|**bigint**|공유 풀에서 리소스를 사용한 작업 그룹의 완료 된 총 요청 수입니다.||
|total_queued_request_count|**bigint**|Max_concurrency 제한에 도달한 후에 큐에 대기 중인 요청의 누적 수입니다.||
|total_request_execution_timeouts|**bigint**|작업 그룹에서 query_execution_timeout_sec 설정에 따라 완료 되기 전에 시간 초과 된 총 요청 수입니다.||
|effective_min_percentage_resource|**tinyint**|서비스 수준 및 작업 그룹 설정을 고려 하 여 허용 되는 효과적인 min_percentage_resource 설정입니다. 낮은 서비스 수준에서 효과적인 min_percentage_resource을 더 높은 수준으로 조정할 수 있습니다.  예를 들어 DW100c에서 가장 낮은 min_percentage_resource 허용 되는 것은 25%입니다.  서비스 수준에서 값을 부여할 수 없으면 min_percentage_resource 0%로 조정 됩니다.  예를 들어 DW6000c에서 10%로 설정 된 min_percentage_resource DW100c으로 축소 될 때 0%의 effective_min_percentage_resource 됩니다.||
|effective_cap_percentage_resource|**tinyint**|작업 그룹에 대 한 유효한 cap_percentage_resource입니다.  Min_percentage_resource > 0 인 다른 작업 그룹이 있는 경우 effective_cap_percentage_resource 비례적으로 줄어듭니다.||
|effective_request_min_resource_grant_percent|**decimal (5, 2)**|작업 그룹의 request_min_resource_grant_percent에 대 한 유효 런타임 값입니다. 서비스 수준 및 작업 그룹을 구성 하는 방법을 고려 하는 유효한 값입니다.  서비스 수준으로 인해 min_percentage_resource 조정 된 경우 effective_request_min_resource_grant_percent 적절 하 게 조정 됩니다.||
|effective_request_max_resource_grant_percent|**decimal (5, 2)**|모든 작업 그룹의 구성을 고려 하 여 작업 그룹의 request_max_resource_grant_percent에 대 한 유효 런타임 값입니다.||
|||||

## <a name="see-also"></a>참조

 [Transact-sql&#41;&#40;Azure Synapse 분석 및 병렬 데이터 웨어하우스 동적 관리 뷰 ](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
