---
title: sys.dm_broker_queue_monitors (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_broker_queue_monitors
- sys.dm_broker_queue_monitors_TSQL
- dm_broker_queue_monitors_TSQL
- sys.dm_broker_queue_monitors
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_broker_queue_monitors dynamic management view
ms.assetid: 401207dc-ef4a-4a3f-879c-76dcbb52d6bc
author: stevestein
ms.author: sstein
ms.openlocfilehash: f2f363998699846ca5020127f19be6dc0ad59712
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948630"
---
# <a name="sysdmbrokerqueuemonitors-transact-sql"></a>sys.dm_broker_queue_monitors(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  인스턴스의 큐 모니터에 대한 행을 반환합니다. 한 큐 모니터에 대해 한 행을 반환합니다 큐 모니터는 큐 활성화를 관리합니다.  
  

|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|모니터에서 감시하는 큐를 포함하는 데이터베이스의 개체 식별자입니다. NULL을 허용합니다.|  
|**queue_id**|**int**|모니터에서 감시하는 큐의 개체 식별자입니다. NULL을 허용합니다.|  
|**state**|**nvarchar(32)**|모니터의 상태입니다. NULL을 허용합니다. 다음 중 하나일 수 있습니다.<br /><br /> **비활성**<br /><br /> **알림을**<br /><br /> **RECEIVES_OCCURRING**|  
|**last_empty_rowset_time**|**datetime**|큐에서 RECEIVE가 마지막으로 빈 결과를 반환한 시간입니다. NULL을 허용합니다.|  
|**last_activated_time**|**datetime**|이 큐 모니터에서 마지막으로 저장 프로시저를 활성화한 시간입니다. NULL을 허용합니다.|  
|**tasks_waiting**|**int**|이 큐에 대해 RECEIVE 문 내에서 현재 대기하고 있는 세션 수입니다. NULL을 허용합니다.<br /><br /> 참고: 이 수에는 큐 모니터에서 세션을 시작 하는 여부에 관계 없이 receive 문을 실행 하는 모든 세션이 포함 됩니다. RECEIVE와 함께 WAITFOR를 사용하는 경우 해당됩니다. 기본적으로 이러한 태스크는 메시지가 큐에 도착할 때까지 대기하고 있습니다.|  
  
## <a name="permissions"></a>사용 권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-current-status-queue-monitor"></a>A. 현재 상태 큐 모니터  
 이 시나리오에서는 모든 메시지 큐의 현재 상태를 제공합니다.  
  
```  
SELECT t1.name AS [Service_Name],  t3.name AS [Schema_Name],  t2.name AS [Queue_Name],    
CASE WHEN t4.state IS NULL THEN 'Not available'   
ELSE t4.state   
END AS [Queue_State],    
CASE WHEN t4.tasks_waiting IS NULL THEN '--'   
ELSE CONVERT(VARCHAR, t4.tasks_waiting)   
END AS tasks_waiting,   
CASE WHEN t4.last_activated_time IS NULL THEN '--'   
ELSE CONVERT(varchar, t4.last_activated_time)   
END AS last_activated_time ,    
CASE WHEN t4.last_empty_rowset_time IS NULL THEN '--'   
ELSE CONVERT(varchar,t4.last_empty_rowset_time)   
END AS last_empty_rowset_time,   
(   
SELECT COUNT(*)   
FROM sys.transmission_queue t6   
WHERE (t6.from_service_name = t1.name) ) AS [Tran_Message_Count]   
FROM sys.services t1    INNER JOIN sys.service_queues t2   
ON ( t1.service_queue_id = t2.object_id )     
INNER JOIN sys.schemas t3 ON ( t2.schema_id = t3.schema_id )    
LEFT OUTER JOIN sys.dm_broker_queue_monitors t4   
ON ( t2.object_id = t4.queue_id  AND t4.database_id = DB_ID() )    
INNER JOIN sys.databases t5 ON ( t5.database_id = DB_ID() );  
```  
  
## <a name="see-also"></a>관련 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Service Broker 관련 동적 관리 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
  

