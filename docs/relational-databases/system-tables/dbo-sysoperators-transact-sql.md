---
description: dbo.sysoperators(Transact-SQL)
title: dbo.sys연산자 (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysoperators
- dbo.sysoperators
- dbo.sysoperators_TSQL
- sysoperators_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysoperators system table
ms.assetid: c2afa20c-b15f-46ca-ae74-2eb65909409e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a5784e4084fa8481f8293d68b81d4ab8c52f626a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540374"
---
# <a name="dbosysoperators-transact-sql"></a>dbo.sysoperators(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 운영자에 대해 한 행을 포함합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|운영자의 ID입니다.|  
|**name**|**sysname**|운영자의 이름입니다.|  
|**사용**|**tinyint**|경고 알림(부울)의 상태입니다. **1**인 경우이 운영자는 경고가 발생할 때 알림을 받을 수 있습니다.|  
|**email_address**|**nvarchar (100)**|해당 운영자의 전자 메일 주소입니다.|  
|**last_email_date**|**int**|해당 운영자가 마지막으로 전자 메일로 경고 알림을 받은 날짜입니다.|  
|**last_email_time**|**int**|해당 운영자가 마지막으로 전자 메일로 경고 알림을 받은 시간입니다.|  
|**pager_address**|**nvarchar (100)**|해당 운영자의 호출기 주소입니다.|  
|**last_pager_date**|**int**|해당 운영자가 마지막으로 호출기로 경고 알림을 받은 날짜입니다.|  
|**last_pager_time**|**int**|해당 운영자가 마지막으로 호출기로 경고 알림을 받은 시간입니다.|  
|**weekday_pager_start_time**|**int**|월요일에서 금요일까지의 평일에 해당 운영자가 호출기 경고 알림을 받기 시작하는 시간입니다.|  
|**weekday_pager_end_time**|**int**|월요일에서 금요일까지의 평일에 해당 운영자가 호출기 경고 알림을 받기를 끝내는 시간입니다.|  
|**saturday_pager_start_time**|**int**|토요일에 해당 운영자가 호출기 경고 알림을 받기 시작하는 시간입니다.|  
|**saturday_pager_end_time**|**int**|토요일에 해당 운영자가 호출기 경고 알림을 받기를 끝내는 시간입니다.|  
|**sunday_pager_start_time**|**int**|일요일에 해당 운영자가 호출기 경고 알림을 받기 시작하는 시간입니다.|  
|**sunday_pager_end_time**|**int**|일요일에 해당 운영자가 호출기 경고 알림을 받기를 끝내는 시간입니다.|  
|**pager_days**|**tinyint**|해당 운영자가 호출기 경고 알림을 받을 수 있는 평일을 표시하는 비트마스크입니다.|  
|**netsend_address**|**nvarchar (100)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**last_netsend_date**|**int**|가장 최근의 네트워크 메시지가 지정한 운영자 ID에 마지막으로 전달된 날짜입니다.|  
|**last_netsend_time**|**int**|가장 최근의 네트워크 메시지가 지정한 운영자 ID에 마지막으로 전달된 시간입니다.|  
|**category_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;테이블 SQL Server 에이전트 ](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)  
  
  
