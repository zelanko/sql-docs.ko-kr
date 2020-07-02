---
title: sys. dm_exec_session_wait_stats (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_session_wait_stats
- sys.dm_exec_session_wait_stats_tsql
- dm_exec_session_wait_stats
- dm_exec_session_wait_stats_tsql
helpviewer_keywords:
- sys.dm_exec_session_wait_stats
ms.assetid: df84842a-71eb-4fda-b448-5953cf9985dc
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f553207a348511a98a331eb54a7090b217bc04fa
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85734666"
---
# <a name="sysdm_exec_session_wait_stats-transact-sql"></a>sys. dm_exec_session_wait_stats (Transact-sql)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asdw](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asdw.md)]

  각 세션에 대해 실행 된 스레드에서 발생 한 모든 대기에 대 한 정보를 반환 합니다. 이 뷰를 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 세션과 특정 쿼리 및 일괄 처리의 성능 문제를 진단할 수 있습니다.  이 뷰는 [transact-sql&#41;&#40;dm_os_wait_stats](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md) 에 대해 집계 되는 것과 동일한 정보를 세션을 반환 하지만 **session_id** 수도 제공 합니다.  
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]( [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상).  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|세션의 id입니다.|  
|wait_type|**nvarchar(60)**|대기 유형의 이름입니다. 자세한 내용은 [sys.dm_os_wait_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)를 참조하세요.|  
|waiting_tasks_count|**bigint**|이 대기 유형의 대기 수입니다. 이 카운터는 각 대기가 시작될 때 증가합니다.|  
|wait_time_ms|**bigint**|이 대기 유형의 총 대기 시간(밀리초)입니다. 이 시간은 signal_wait_time_ms를 포함합니다.|  
|max_wait_time_ms|**bigint**|이 대기 유형의 최대 대기 시간입니다.|  
|signal_wait_time_ms|**bigint**|대기 스레드가 신호를 받은 시간과 실행을 시작한 시간 사이의 차이입니다.|  
  
## <a name="remarks"></a>설명  
 이 DMV는 세션이 열릴 때 또는 세션이 다시 설정 될 때 (연결 풀링 인 경우) 세션 정보를 다시 설정 합니다.  
  
 대기 유형에 대 한 자세한 내용은 [dm_os_wait_stats &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)을 참조 하십시오.  
  
## <a name="permissions"></a>사용 권한  
 사용자에 게 서버에 대 한 **VIEW SERVER STATE** 권한이 있는 경우 사용자는 인스턴스에서 실행 중인 모든 세션을 볼 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 있습니다. 그렇지 않으면 사용자에 게 현재 세션만 표시 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;동적 관리 뷰 및 함수](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;운영 체제 관련 동적 관리 뷰 SQL Server](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_os_wait_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)  
 
