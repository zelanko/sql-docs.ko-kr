---
title: dbo.sysoperators (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 32
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a19301b897480e71fbaf62d502709e082d57da05
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33261219"
---
# <a name="dbosysoperators-transact-sql"></a>dbo.sysoperators(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 운영자에 대해 한 행을 포함합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|운영자의 ID입니다.|  
|**name**|**sysname**|운영자의 이름입니다.|  
|**enabled**|**tinyint**|경고 알림(부울)의 상태입니다. 경우 **1**,이 연산자는 경고가 발생할 때 알림을 받을 수 있습니다.|  
|**email_address**|**nvarchar(100)**|해당 운영자의 전자 메일 주소입니다.|  
|**last_email_date**|**int**|해당 운영자가 마지막으로 전자 메일로 경고 알림을 받은 날짜입니다.|  
|**last_email_time**|**int**|해당 운영자가 마지막으로 전자 메일로 경고 알림을 받은 시간입니다.|  
|**pager_address**|**nvarchar(100)**|해당 운영자의 호출기 주소입니다.|  
|**last_pager_date**|**int**|해당 운영자가 마지막으로 호출기로 경고 알림을 받은 날짜입니다.|  
|**last_pager_time**|**int**|해당 운영자가 마지막으로 호출기로 경고 알림을 받은 시간입니다.|  
|**weekday_pager_start_time**|**int**|월요일에서 금요일까지의 평일에 해당 운영자가 호출기 경고 알림을 받기 시작하는 시간입니다.|  
|**weekday_pager_end_time**|**int**|월요일에서 금요일까지의 평일에 해당 운영자가 호출기 경고 알림을 받기를 끝내는 시간입니다.|  
|**saturday_pager_start_time**|**int**|토요일에 해당 운영자가 호출기 경고 알림을 받기 시작하는 시간입니다.|  
|**saturday_pager_end_time**|**int**|토요일에 해당 운영자가 호출기 경고 알림을 받기를 끝내는 시간입니다.|  
|**sunday_pager_start_time**|**int**|일요일에 해당 운영자가 호출기 경고 알림을 받기 시작하는 시간입니다.|  
|**sunday_pager_end_time**|**int**|일요일에 해당 운영자가 호출기 경고 알림을 받기를 끝내는 시간입니다.|  
|**pager_days**|**tinyint**|해당 운영자가 호출기 경고 알림을 받을 수 있는 평일을 표시하는 비트마스크입니다.|  
|**netsend_address**|**nvarchar(100)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**last_netsend_date**|**int**|가장 최근의 네트워크 메시지가 지정한 운영자 ID에 마지막으로 전달된 날짜입니다.|  
|**last_netsend_time**|**int**|가장 최근의 네트워크 메시지가 지정한 운영자 ID에 마지막으로 전달된 시간입니다.|  
|**category_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 에이전트 테이블 &#40;Transact SQL&#41;](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)  
  
  
