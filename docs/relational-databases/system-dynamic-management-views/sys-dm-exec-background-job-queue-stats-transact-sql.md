---
title: sys.dm_exec_background_job_queue_stats (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_exec_background_job_queue_stats
- sys.dm_exec_background_job_queue_stats
- dm_exec_background_job_queue_stats_TSQL
- sys.dm_exec_background_job_queue_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_background_job_queue_stats dynamic management view
ms.assetid: 27f62ab5-46c4-417e-814d-8d6437034d1c
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: c2c9ec20376173fa23c21c626458be35f12d1f02
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39533323"
---
# <a name="sysdmexecbackgroundjobqueuestats-transact-sql"></a>sys.dm_exec_background_job_queue_stats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  비동기(백그라운드) 실행을 위해 제출된 각 쿼리 프로세서 작업에 대해 집계 통계를 제공하는 행을 반환합니다.  
  
> [!NOTE]  
>  이를 호출 하 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 나 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_exec_background_job_queue_stats**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**queue_max_len**|**int**|최대 큐 길이입니다.|  
|**enqueued_count**|**int**|큐에 성공적으로 게시된 요청 수입니다.|  
|**started_count**|**int**|실행이 시작된 요청 수입니다.|  
|**ended_count**|**int**|서비스에 성공하거나 실패한 요청 수입니다.|  
|**failed_lock_count**|**int**|잠금 경합이나 교착 상태로 인해 실패한 요청 수입니다.|  
|**failed_other_count**|**int**|다른 이유로 인해 실패한 요청 수입니다.|  
|**failed_giveup_count**|**int**|다시 시도 제한에 도달하여 실패한 요청 수입니다.|  
|**enqueue_failed_full_count**|**int**|큐가 꽉 차서 큐에 넣지 못한 시도 수입니다.|  
|**enqueue_failed_duplicate_count**|**int**|중복으로 큐에 넣는 시도 수입니다.|  
|**elapsed_avg_ms**|**int**|요청의 평균 경과 시간(밀리초)입니다.|  
|**elapsed_max_ms**|**int**|가장 긴 요청의 경과 시간(밀리초)입니다.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
## <a name="remarks"></a>Remarks  
 이 뷰는 비동기 업데이트 통계 작업에 대해서만 정보를 반환합니다. 비동기 업데이트 통계에 대 한 자세한 내용은 참조 하십시오 [통계](../../relational-databases/statistics/statistics.md)합니다.  
  
## <a name="permissions"></a>사용 권한

온 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요한 `VIEW SERVER STATE` 권한.   
온 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요를 `VIEW DATABASE STATE` 데이터베이스의 권한.   

## <a name="examples"></a>예  
  
### <a name="a-determining-the-percentage-of-failed-background-jobs"></a>1. 실패한 백그라운드 작업의 백분율 확인  
 다음 예에서는 실행된 모든 쿼리에 대해 실패한 백그라운드 작업의 백분율을 반환합니다.  
  
```  
SELECT   
        CASE ended_count WHEN 0   
                THEN 'No jobs ended'   
                ELSE CAST((failed_lock_count + failed_giveup_count + failed_other_count) / CAST(ended_count AS float) * 100 AS varchar(20))   
        END AS [Percent Failed]  
FROM sys.dm_exec_background_job_queue_stats;  
GO  
```  
  
### <a name="b-determining-the-percentage-of-failed-enqueue-attempts"></a>2. 큐에 넣지 못한 시도의 백분율 확인  
 다음 예에서는 실행된 모든 쿼리에 대해 큐에 넣지 못한 시도의 백분율을 반환합니다.  
  
```  
SELECT   
        CASE enqueued_count WHEN 0   
                THEN 'No jobs posted'   
                ELSE CAST((enqueue_failed_full_count + enqueue_failed_duplicate_count) / CAST(enqueued_count AS float) * 100 AS varchar(20))   
        END AS [Percent Enqueue Failed]  
FROM sys.dm_exec_background_job_queue_stats;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [실행 관련 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


