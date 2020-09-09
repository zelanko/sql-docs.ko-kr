---
description: sys.dm_broker_activated_tasks(Transact-SQL)
title: sys. dm_broker_activated_tasks (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_broker_activated_tasks
- sys.dm_broker_activated_tasks_TSQL
- dm_broker_activated_tasks
- dm_broker_activated_tasks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_broker_activated_tasks dynamic management view
ms.assetid: 17e6f87f-8f56-489d-9aed-216afc8ef310
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e89f0caf5eb3181a59e653ca1a64f4a68ec3fbc5
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544791"
---
# <a name="sysdm_broker_activated_tasks-transact-sql"></a>sys.dm_broker_activated_tasks(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Service Broker가 활성화한 각 저장 프로시저에 대한 행을 반환합니다.  
 

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**spid**|**int**|활성화된 저장 프로시저 세션의 ID입니다. NULL을 허용합니다.|  
|**database_id**|**smallint**|큐가 정의된 데이터베이스의 ID입니다. NULL을 허용합니다.|  
|**queue_id**|**int**|저장 프로시저가 활성화된 큐 개체의 ID입니다. NULL을 허용합니다.|  
|**procedure_name**|**nvarchar (650)**|활성화된 저장 프로시저의 이름입니다. NULL을 허용합니다.|  
|**execute_as**|**int**|저장 프로시저가 실행되는 사용자의 ID입니다. NULL을 허용합니다.|  
  
## <a name="permissions"></a>사용 권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="physical-joins"></a>물리적 조인  
 ![sys.dm_broker_activated_tasks에 대한 조인](../../relational-databases/system-dynamic-management-views/media/join-dm-broker-activated-tasks-1.gif "sys.dm_broker_activated_tasks에 대한 조인")  
  
## <a name="relationship-cardinalities"></a>관계 카디널리티  
  
|시작|대상|관계|  
|----------|--------|------------------|  
|dm_broker_activated_tasks.spid|dm_exec_sessions.session_id|일대일|  
  
## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Service Broker 관련 동적 관리 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
  

