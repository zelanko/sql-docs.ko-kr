---
title: log_shipping_monitor_history_detail (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_monitor_history_detail_TSQL
- log_shipping_monitor_history_detail
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_monitor_history_detail system table
ms.assetid: 7080c888-323b-4206-a1ab-e6c51f9e2579
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0f0a304020b972b29d521bd32da3f98b8d3fdfc9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67989997"
---
# <a name="log_shipping_monitor_history_detail-transact-sql"></a>log_shipping_monitor_history_detail(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  로그 전달 작업에 대한 기록 세부 정보를 저장합니다. 이 테이블은 **msdb** 데이터베이스에 저장 됩니다.  
  
 기록 및 모니터링과 연관된 테이블은 주 서버와 보조 서버에서도 사용됩니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**agent_id**|**uniqueidentifier**|백업의 경우 주 ID, 복사나 복원의 경우 보조 ID입니다.|  
|**agent_type**|**tinyint**|로그 전달 작업의 유형입니다.<br /><br /> 0 = 백업<br /><br /> 1 = 복사<br /><br /> 2 = 복원|  
|**session_id**|**int**|백업/복사/복원 작업의 세션 ID입니다.|  
|**database_name**|**sysname**|이 레코드에 연결된 데이터베이스의 이름입니다. 백업의 경우 주 데이터베이스, 복원의 경우 보조 데이터베이스이며 복사의 경우 비워 둡니다.|  
|**session_status**|**tinyint**|세션의 상태입니다.<br /><br /> 0 = 시작 중<br /><br /> 1 = 실행 중<br /><br /> 2 = 성공<br /><br /> 3 = 오류<br /><br /> 4 = 경고|  
|**log_time**|**datetime**|레코드가 생성된 날짜와 시간입니다.|  
|**log_time_utc**|**datetime**|레코드가 생성된 날짜와 시간(UTC)입니다.|  
|**message**|**nvarchar(max)**|메시지 내용입니다.|  
  
## <a name="remarks"></a>설명  
 이 테이블에는 로그 전달 에이전트에 대한 기록 세부 정보가 포함됩니다. 에이전트 세션을 식별 하려면 **agent_id**, **agent_type**및 **session_id**열을 사용 합니다. 에이전트 세션에 대 한 기록 세부 정보를 보려면 **log_time**를 기준으로 정렬 합니다.  
  
 주 서버와 관련 된 정보는 원격 모니터 서버에 저장 되는 것 외에도 주 서버에 **log_shipping_monitor_history_detail** 테이블에 저장 되 고 보조 서버와 관련 된 정보는 **log_shipping_monitor_history_detail** 테이블의 보조 서버에도 저장 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [로그 전달 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Transact-sql&#41;sp_delete_log_shipping_primary_database &#40;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [Transact-sql&#41;sp_cleanup_log_shipping_history &#40;](../../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md)   
 [Transact-sql&#41;sp_refresh_log_shipping_monitor &#40;](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [Transact-sql&#41;sp_delete_log_shipping_secondary_database &#40;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [Transact-sql&#41;&#40;시스템 테이블](../../relational-databases/system-tables/system-tables-transact-sql.md)   
 [Transact-sql&#41;log_shipping_monitor_error_detail &#40;](../../relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql.md)  
  
  
