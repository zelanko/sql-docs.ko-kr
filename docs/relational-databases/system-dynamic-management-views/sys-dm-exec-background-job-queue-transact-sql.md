---
title: sys. dm_exec_background_job_queue (Transact-sql) | Microsoft Docs
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 09e760bac8e31ba9c78b9809a12f8d595b7ebd05
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68263926"
---
# <a name="sysdm_exec_background_job_queue-transact-sql"></a>sys.dm_exec_background_job_queue(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  비동기(백그라운드) 실행을 예약한 쿼리 프로세서 작업에 대한 행을 반환합니다.  
  
> **참고!!** 또는 **[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]** **[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]** 에서이를 호출 하려면 이름 **sys. dm_pdw_nodes_exec_background_job_queue**을 사용 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**time_queued**|**datetime**|작업이 큐에 추가된 시간입니다.|  
|**job_id**|**int**|작업 식별자입니다.|  
|**database_id**|**int**|작업을 실행할 데이터베이스입니다.|  
|**object_id1**|**int**|값이 작업 유형에 따라 달라집니다. 자세한 내용은 주의 섹션을 참조하세요.|  
|**object_id2**|**int**|값이 작업 유형에 따라 달라집니다. 자세한 내용은 주의 섹션을 참조하세요.|  
|**object_id3**|**int**|값이 작업 유형에 따라 달라집니다. 자세한 내용은 주의 섹션을 참조하세요.|  
|**object_id4**|**int**|값이 작업 유형에 따라 달라집니다. 자세한 내용은 주의 섹션을 참조하세요.|  
|**error_code**|**int**|장애로 인해 작업이 다시 삽입된 경우의 오류 코드입니다. 일시 중지되었거나 선택되지 않았거나 완료된 경우에는 NULL입니다.|  
|**request_type**|**smallint**|작업 요청 유형입니다.|  
|**retry_count**|**smallint**|작업이 큐에서 선택되었다가 리소스 부족이나 기타 이유로 큐에 다시 삽입된 횟수입니다.|  
|**in_progress**|**smallint**|작업 실행이 시작되었는지 여부를 나타냅니다.<br /><br /> 1 = 시작됨<br /><br /> 0 = 여전히 대기 중|  
|**session_id**|**smallint**|세션 식별자입니다.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포가 설정 된 노드의 식별자입니다.|  
  
## <a name="permissions"></a>사용 권한

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]는 권한이 `VIEW SERVER STATE` 필요 합니다.   
Premium [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 계층에서는 데이터베이스에 대 `VIEW DATABASE STATE` 한 권한이 필요 합니다. [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 표준 및 기본 계층에서는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정이 필요 합니다.   
  
## <a name="remarks"></a>설명  
 이 뷰는 비동기 업데이트 통계 작업에 대해서만 정보를 반환합니다. 비동기 업데이트 통계에 대 한 자세한 내용은 [통계](../../relational-databases/statistics/statistics.md)를 참조 하세요.  
  
 **Object_id4** 를 통해 **object_id1** 값은 작업 요청의 유형에 따라 달라 집니다. 다음 표에서는 작업 유형별로 이러한 열의 의미를 요약하여 보여 줍니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;관련 동적 관리 뷰 및 함수 실행](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [통계](../../relational-databases/statistics/statistics.md)   
 [KILL STATS JOB &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-stats-job-transact-sql.md)  
  
  



