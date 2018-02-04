---
title: log_shipping_monitor_alert (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- log_shipping_monitor_alert
- log_shipping_monitor_alert_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_monitor_alert system table
ms.assetid: 1c775e48-9898-4149-b9d1-04d465f23438
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c724c417c90e0d596f3846feb1a2f454ba291a01
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="logshippingmonitoralert-transact-sql"></a>log_shipping_monitor_alert(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  로그 전달에 대한 경고 작업 ID를 저장합니다. 이 테이블에 저장 되는 **msdb** 데이터베이스입니다.   
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**alert_job_id**|**uniqueidentifier**|로그 전달 경고 작업의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 ID입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [로그 전달 &#40;에 대 한 SQL Server &#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_add_log_shipping_alert_job &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-alert-job-transact-sql.md)   
 [sp_delete_log_shipping_alert_job &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-alert-job-transact-sql.md)   
 [sp_help_log_shipping_alert_job &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-alert-job-transact-sql.md)   
 [시스템 테이블 &#40; Transact SQL &#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
