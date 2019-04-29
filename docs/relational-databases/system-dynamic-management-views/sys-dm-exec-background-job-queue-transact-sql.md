---
title: sys.dm_exec_background_job_queue (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_background_job_queue
- sys.dm_exec_background_job_queue_TSQL
- dm_exec_background_job_queue_TSQL
- sys.dm_exec_background_job_queue
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_background_job_queue dynamic management function
ms.assetid: 05d9884f-b74c-4e3c-a23b-c90c1ea5ef02
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 142329f80b55a18eb6724449f3e1ad68dfb72acb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63013582"
---
# <a name="sysdmexecbackgroundjobqueue-transact-sql"></a>sys.dm_exec_background_job_queue(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  비동기(백그라운드) 실행을 예약한 쿼리 프로세서 작업에 대한 행을 반환합니다.  
  
> **참고!** 이를 호출 하 **[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]** 하거나 **[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]** 에 이름을 사용 하 여 **sys.dm_pdw_nodes_exec_background_job_queue**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**time_queued**|**datetime**|작업이 큐에 추가된 시간입니다.|  
|**job_id**|**int**|작업 식별자입니다.|  
|**database_id**|**int**|작업을 실행할 데이터베이스입니다.|  
|**object_id1**|**int**|값이 작업 유형에 따라 달라집니다. 자세한 내용은 설명 섹션을 참조하세요.|  
|**object_id2**|**int**|값이 작업 유형에 따라 달라집니다. 자세한 내용은 설명 섹션을 참조하세요.|  
|**object_id3**|**int**|값이 작업 유형에 따라 달라집니다. 자세한 내용은 설명 섹션을 참조하세요.|  
|**object_id4**|**int**|값이 작업 유형에 따라 달라집니다. 자세한 내용은 설명 섹션을 참조하세요.|  
|**error_code**|**int**|장애로 인해 작업이 다시 삽입된 경우의 오류 코드입니다. 일시 중지되었거나 선택되지 않았거나 완료된 경우에는 NULL입니다.|  
|**request_type**|**smallint**|작업 요청 유형입니다.|  
|**retry_count**|**smallint**|작업이 큐에서 선택되었다가 리소스 부족이나 기타 이유로 큐에 다시 삽입된 횟수입니다.|  
|**in_progress**|**smallint**|작업 실행이 시작되었는지 여부를 나타냅니다.<br /><br /> 1 = 시작됨<br /><br /> 0 = 여전히 대기 중|  
|**session_id**|**smallint**|세션 식별자입니다.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
## <a name="permissions"></a>사용 권한

온 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요한 `VIEW SERVER STATE` 권한.   
온 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요를 `VIEW DATABASE STATE` 데이터베이스의 권한.   
  
## <a name="remarks"></a>Remarks  
 이 뷰는 비동기 업데이트 통계 작업에 대해서만 정보를 반환합니다. 비동기 업데이트 통계에 대 한 자세한 내용은 참조 하십시오 [통계](../../relational-databases/statistics/statistics.md)합니다.  
  
 값 **object_id1** 를 통해 **object_id4** 작업 요청 유형에 따라 달라 집니다. 다음 표에서는 작업 유형별로 이러한 열의 의미를 요약하여 보여 줍니다.  
  
|요청 유형|object_id1|object_id2|object_id3|object_id4|  
|------------------|-----------------|-----------------|-----------------|-----------------|  
|비동기 업데이트 통계|테이블 또는 뷰 ID|통계 ID|사용되지 않음|사용되지 않음|  
  
## <a name="examples"></a>예  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 각 데이터베이스에 대한 백그라운드 큐에 있는 활성 비동기 작업의 수를 반환합니다.  
  
```  
SELECT DB_NAME(database_id) AS [Database], COUNT(*) AS [Active Async Jobs]  
FROM sys.dm_exec_background_job_queue  
WHERE in_progress = 1  
GROUP BY database_id;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [실행 관련 동적 관리 뷰 및 함수 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [통계](../../relational-databases/statistics/statistics.md)   
 [KILL STATS JOB &#40;TRANSACT-SQL&#41;](../../t-sql/language-elements/kill-stats-job-transact-sql.md)  
  
  



