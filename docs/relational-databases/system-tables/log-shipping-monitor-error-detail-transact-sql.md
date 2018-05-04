---
title: log_shipping_monitor_error_detail (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- log_shipping_monitor_error_detail_TSQL
- log_shipping_monitor_error_detail
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_monitor_error_detail system table
ms.assetid: 0c38a625-60d2-4ee2-bcf3-2ba367914220
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7a594771827da8a3af6b5158725e632f4488eed5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="logshippingmonitorerrordetail-transact-sql"></a>log_shipping_monitor_error_detail(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  로그 전달 작업에 대한 오류 정보를 저장합니다. 이 테이블에 저장 되는 **msdb** 데이터베이스입니다.  
  
 기록 및 모니터링과 연관된 테이블은 주 서버와 보조 서버에서도 사용됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**uniqueidentifier**|백업의 경우 주 ID, 복사나 복원의 경우 보조 ID입니다.|  
|**agent_type**|**tinyint**|로그 전달 작업의 유형입니다.<br /><br /> 0 = 백업<br /><br /> 1 = 복사<br /><br /> 2 = 복원|  
|**session_id**|**int**|백업/복사/복원 작업의 세션 ID입니다.|  
|**database_name**|**sysname**|이 오류 레코드와 연관된 데이터베이스의 이름입니다. 백업의 경우 주 데이터베이스, 복원의 경우 보조 데이터베이스이며 복사의 경우 비워 둡니다.|  
|**sequence_number**|**int**|여러 개의 레코드에 걸친 오류 정보의 올바른 순서를 나타내는 증분값입니다.|  
|**log_time**|**datetime**|레코드가 생성된 날짜와 시간입니다.|  
|**log_time_utc**|**datetime**|레코드가 생성된 날짜와 시간(UTC)입니다.|  
|**message**|**nvarchar**|메시지 내용입니다.|  
|**원본(source)**|**nvarchar**|오류 메시지 또는 이벤트의 원본입니다.|  
|**help_url**|**nvarchar**|오류에 대한 자세한 내용을 참조할 수 있는 URL(사용 가능한 경우)입니다.|  
  
## <a name="remarks"></a>주의  
 이 테이블은 로그 전달 에이전트에 대한 오류 세부 정보를 포함합니다. 각 오류는 예외 시퀀스로 기록됩니다. 각 에이전트 세션에 여러 개의 오류(시퀀스)가 있을 수 있습니다.  
  
 주 서버와 관련 된 정보에 주 서버에 저장 된 원격 모니터 서버에 저장 될 뿐만 아니라 해당 **log_shipping_monitor_error_detail** 테이블 및 보조 서버와 관련 된 정보 보조 서버에 저장 됩니다는 **log_shipping_monitor_error_detail** 테이블입니다.  
  
 에이전트 세션을 식별 하려면 열을 사용 하 여 **agent_id**, **agent_type**, 및 **session_id**합니다. 정렬할 **log_time** 오류가 기록 된 순서로 표시 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [로그 전달 & #40;에 대 한 SQL Server & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [log_shipping_monitor_history_detail &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/log-shipping-monitor-history-detail-transact-sql.md)   
 [sp_cleanup_log_shipping_history&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md)   
 [sp_delete_log_shipping_primary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [sp_delete_log_shipping_secondary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [sp_refresh_log_shipping_monitor &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [시스템 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
