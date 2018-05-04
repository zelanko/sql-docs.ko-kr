---
title: log_shipping_monitor_secondary (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- log_shipping_monitor_secondary_TSQL
- log_shipping_monitor_secondary
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_monitor_secondary system table
ms.assetid: afbe1bb7-89a7-4020-9408-0af64a043c2e
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3200a0616ffc3db7a328322a39d1767ecefe6614
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="logshippingmonitorsecondary-transact-sql"></a>log_shipping_monitor_secondary(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  로그 전달 구성에서 보조 데이터베이스마다 하나의 모니터 레코드를 저장합니다. 이 테이블에 저장 되는 **msdb** 데이터베이스입니다.  
  
 기록 및 모니터링과 연관된 테이블은 주 서버와 보조 서버에서도 사용됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**secondary_server**|**sysname**|보조 인스턴스의 이름에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 로그 전달 구성의 합니다.|  
|**secondary_database**|**sysname**|로그 전달 구성의 보조 데이터베이스의 이름입니다.|  
|**secondary_id**|**uniqueidentifier**|로그 전달 구성의 보조 서버의 ID입니다.|  
|**primary_server**|**sysname**|로그 전달 구성의 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에 대한 주 인스턴스 이름입니다.|  
|**primary_database**|**sysname**|로그 전달 구성의 주 데이터베이스의 이름입니다.|  
|**restore_threshold**|**int**|복원 작업 간 허용되는 시간(분)입니다. 이 시간이 지나면 경고가 발생합니다.|  
|**threshold_alert**|**int**|복원 임계값을 초과할 경우 발생하는 경고입니다.|  
|**threshold_alert_enabled**|**bit**|복원 임계값 경고를 설정할지 여부를 결정합니다. 1 = 사용.<br /><br /> 0 = 사용 안 함.|  
|**last_copied_file**|**nvarchar(500)**|보조 서버로 복사된 마지막 백업 파일의 파일 이름입니다.|  
|**last_copied_date**|**datetime**|보조 서버에 수행된 마지막 복사 작업의 시간과 날짜입니다.|  
|**last_copied_date_utc**|**datetime**|보조 서버에 수행된 마지막 복사 작업의 시간과 날짜(UTC)입니다.|  
|**last_restored_file**|**nvarchar(500)**|보조 데이터베이스에 복원된 마지막 백업 파일의 이름입니다.|  
|**last_restored_date**|**datetime**|보조 데이터베이스에 수행된 마지막 복원 작업의 시간과 날짜입니다.|  
|**last_restored_date_utc**|**datetime**|보조 데이터베이스에 수행된 마지막 복원 작업의 시간과 날짜(UTC)입니다.|  
|**last_restored_latency**|**int**|로그 백업이 주 서버 또는 데이터베이스에서 생성되어 보조 서버 또는 데이터베이스에서 복원될 때까지 경과한 시간(분)입니다.<br /><br /> 초기 값은 NULL입니다.|  
|**history_retention_period**|**int**|지정된 보조 데이터베이스에서 로그 전달 기록 레코드가 삭제되기까지 보관되는 기간(분)입니다.|  
  
## <a name="remarks"></a>주의  
 보조 서버와 관련 된 정보는 보조 서버에 저장 됩니다 및 원격 모니터 서버에 저장 될 뿐만 아니라 해당 **log_shipping_monitor_secondary** 테이블입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [로그 전달 & #40;에 대 한 SQL Server & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_refresh_log_shipping_monitor &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [sp_add_log_shipping_secondary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql.md)   
 [sp_change_log_shipping_secondary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-log-shipping-secondary-database-transact-sql.md)   
 [sp_delete_log_shipping_secondary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [sp_help_log_shipping_secondary_database&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md)   
 [sp_help_log_shipping_monitor_secondary &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-secondary-transact-sql.md)   
 [sp_refresh_log_shipping_monitor &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [시스템 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
