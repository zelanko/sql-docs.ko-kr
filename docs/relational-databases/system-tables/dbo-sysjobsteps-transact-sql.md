---
title: dbo.sysjobsteps (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.sysjobsteps
- dbo.sysjobsteps_TSQL
- sysjobsteps
- sysjobsteps_TSQL
dev_langs: TSQL
helpviewer_keywords: sysjobsteps system table
ms.assetid: 978b8205-535b-461c-91f3-af9b08eca467
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 4f316e40cc6bf89cf7296b5a2d864406142f7f87
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="dbosysjobsteps-transact-sql"></a>dbo.sysjobsteps(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 실행될 작업의 각 단계에 대한 정보를 포함합니다. 이 테이블에 저장 되는 **msdb** 데이터베이스입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|작업의 ID입니다.|  
|**step_id**|**int**|작업 단계의 ID입니다.|  
|**step_name**|**sysname**|작업 단계의 이름입니다.|  
|**하위 시스템**|**nvarchar (40)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 작업 단계를 실행하는 데 사용하는 하위 시스템의 이름입니다.|  
|**명령**|**nvarchar(max)**|실행할 명령 **하위 시스템**합니다.|  
|**플래그**|**int**|예약되어 있습니다.|  
|**additional_parameters**|**ntext**|예약되어 있습니다.|  
|**cmdexec_success_code**|**int**|반환 된 오류 수준 값 **CmdExec** 하위 시스템 단계가 성공 여부를 표시 합니다.|  
|**on_success_action**|**tinyint**|단계가 성공적으로 실행되었을 때 수행되는 동작입니다.|  
|**on_success_step_id**|**int**|단계가 성공적으로 실행되었을 때 다음으로 실행되는 단계의 ID입니다.|  
|**on_fail_action**|**tinyint**|단계가 성공적으로 실행되지 않았을 때 수행되는 동작입니다.|  
|**on_fail_step_id**|**int**|단계가 성공적으로 실행되지 않았을 때 다음으로 실행되는 단계의 ID입니다.|  
|**서버**|**sysname**|예약되어 있습니다.|  
|**database_name**|**sysname**|데이터베이스의 이름 **명령** 경우 실행 됩니다 **하위 시스템** t s q l.|  
|**database_user_name**|**sysname**|단계를 실행할 때 그 계정을 사용할 데이터베이스 사용자의 이름입니다.|  
|**retry_attempts**|**int**|단계가 실패했을 때 재시도하는 횟수입니다.|  
|**retry_interval**|**int**|재시도 간에 대기하는 시간입니다.|  
|**os_run_priority**|**int**|예약되어 있습니다.|  
|**output_file_name**|**nvarchar(200)**|때 저장 되는 단계의 출력 파일의 이름 **하위 시스템** 이 TSQL, PowerShell 또는 **CmdExec***합니다.*|  
|**last_run_outcome**|**int**|작업 단계의 이전 실행 결과입니다.<br /><br /> **0** = 실패<br /><br /> **1** = 성공<br /><br /> **2** = 다시 시도<br /><br /> **3** = 취소<br /><br /> **5** = 알 수 없음|  
|**last_run_duration**|**int**|단계가 마지막으로 실행되었을 때의 시간(hhmmss)입니다.|  
|**last_run_retries**|**int**|작업 단계의 마지막 실행에서 재시도한 횟수입니다.|  
|**last_run_date**|**int**|단계가 마지막으로 실행을 시작했을 때의 날짜(yyyymmdd)입니다.|  
|**last_run_time**|**int**|단계가 마지막으로 실행을 시작했을 때의 시간(hhmmss)입니다.|  
|**proxy_id**|**int**|작업 단계에 대한 프록시입니다.|  
|**step_uid**|**uniqueidentifier**|작업 단계에 대한 식별자입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 에이전트 테이블 &#40; Transact SQL &#41;](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)  
  
  
