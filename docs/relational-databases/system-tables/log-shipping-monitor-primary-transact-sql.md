---
title: log_shipping_monitor_primary (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_monitor_primary
- log_shipping_monitor_primary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_monitor_primary system table
ms.assetid: 5f629a29-1a62-40e6-ae33-6f6b7dd09a36
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 650fb8c3b043940658bcc50720c0e5dd1da822db
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47690031"
---
# <a name="logshippingmonitorprimary-transact-sql"></a>log_shipping_monitor_primary(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  각 로그 전달 구성에서 주 데이터베이스마다 하나의 모니터 레코드를 저장합니다. 이 테이블에 저장 되는 **msdb** 데이터베이스입니다.  
  
 기록 및 모니터링과 연관된 테이블은 주 서버와 보조 서버에서도 사용됩니다.   
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**primary_id**|**uniqueidentifier**|로그 전달 구성의 주 데이터베이스의 ID입니다.|  
|**primary_server**|**sysname**|기본 인스턴스 이름을 합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 로그 전달 구성에서 합니다.|  
|**primary_database**|**sysname**|로그 전달 구성의 주 데이터베이스의 이름입니다.|  
|**backup_threshold**|**int**|백업 작업 간 허용되는 시간(분)입니다. 이 시간이 지나면 경고가 발생합니다.|  
|**threshold_alert**|**int**|백업 임계값이 초과될 때 발생하는 경고입니다.|  
|**threshold_alert_enabled**|**bit**|백업 임계값 경고를 설정할지 여부를 결정합니다. 1 = 사용.<br /><br /> 0 = 사용 안 함.|  
|**last_backup_file**|**nvarchar(500)**|가장 최근 트랜잭션 로그 백업의 절대 경로입니다.|  
|**last_backup_date**|**datetime**|주 데이터베이스에서 마지막으로 수행된 트랜잭션 로그 백업 작업의 시간과 날짜입니다.|  
|**last_backup_date_utc**|**datetime**|주 데이터베이스에서 마지막으로 수행된 트랜잭션 로그 백업 작업의 시간과 날짜(UTC)입니다.|  
|**history_retention_period**|**int**|지정된 기본 데이터베이스의 로그 전달 기록 레코드가 삭제되기까지 보관되는 기간(분)입니다.|  
  
## <a name="remarks"></a>Remarks  
 주 서버와 관련 된 정보에서 주 서버에 저장 됩니다 원격 모니터 서버에 저장 되는 것 외에도 해당 **log_shipping_monitor_primary** 테이블입니다.  
  
## <a name="see-also"></a>관련 항목  
 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_add_log_shipping_primary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md)   
 [sp_change_log_shipping_primary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-log-shipping-primary-database-transact-sql.md)   
 [sp_delete_log_shipping_primary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [sp_help_log_shipping_primary_database&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md)   
 [sp_refresh_log_shipping_monitor &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [sp_help_log_shipping_monitor_primary &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-primary-transact-sql.md)   
 [sp_delete_log_shipping_alert_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-alert-job-transact-sql.md)   
 [시스템 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
