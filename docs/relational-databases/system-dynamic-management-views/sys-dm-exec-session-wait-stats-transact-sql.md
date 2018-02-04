---
title: sys.dm_exec_session_wait_stats (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 02/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_session_wait_stats
- sys.dm_exec_session_wait_stats_tsql
- dm_exec_session_wait_stats
- dm_exec_session_wait_stats_tsql
helpviewer_keywords:
- sys.dm_exec_session_wait_stats
ms.assetid: df84842a-71eb-4fda-b448-5953cf9985dc
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 73dcc552a70ba68d7beff38ed0476b1970feefca
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmexecsessionwaitstats-transact-sql"></a>sys.dm_exec_session_wait_stats (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  각 세션에 대해 실행 중인 스레드로 인해 발생 한 모든 대기에 대 한 정보를 반환 합니다. 이 보기를 사용 하 여 성능 문제를 진단 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 세션 및 특정 쿼리 및 일괄 처리와도 합니다.  이 뷰는 세션에 대해 집계 되는 동일한 정보를 반환 [sys.dm_os_wait_stats&#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md) 하지만 제공 된 **session_id** 번호도 합니다.  
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|세션의 id입니다.|  
|wait_type|**nvarchar(60)**|대기 유형의 이름입니다. 자세한 내용은 [sys.dm_os_wait_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)를 참조하세요.|  
|waiting_tasks_count|**bigint**|이 대기 유형의 대기 수입니다. 이 카운터는 각 대기가 시작될 때 증가합니다.|  
|wait_time_ms|**bigint**|이 대기 유형의 총 대기 시간(밀리초)입니다. 이 시간은 signal_wait_time_ms를 포함합니다.|  
|max_wait_time_ms|**bigint**|이 대기 유형의 최대 대기 시간입니다.|  
|signal_wait_time_ms|**bigint**|대기 스레드가 신호를 받은 시간과 실행을 시작한 시간 사이의 차이입니다.|  
  
## <a name="remarks"></a>주의  
 이 DMV는 세션을 열 때 또는 세션 다시 설정 되는 세션에 대 한 정보를 다시 설정 (하는 경우 연결 풀링이),  
  
 대기 유형에 대 한 정보를 참조 하십시오. [sys.dm_os_wait_stats&#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 사용자에 게 있으면 **VIEW SERVER STATE** 서버 권한, 사용자는 확인할 실행 중인 모든 세션의 인스턴스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 그렇지 않으면 현재 세션에만 표시 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [SQL Server 운영 체제 관련 동적 관리 뷰 &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_os_wait_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)  
 
