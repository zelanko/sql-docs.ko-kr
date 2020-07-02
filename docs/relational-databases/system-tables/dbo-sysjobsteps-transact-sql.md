---
title: dbo.sysjobsteps (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysjobsteps
- dbo.sysjobsteps_TSQL
- sysjobsteps
- sysjobsteps_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobsteps system table
ms.assetid: 978b8205-535b-461c-91f3-af9b08eca467
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 00432619ac30e7f5e0fefc87d335634563a270df
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750343"
---
# <a name="dbosysjobsteps-transact-sql"></a>dbo.sysjobsteps(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 실행될 작업의 각 단계에 대한 정보를 포함합니다. 이 테이블은 **msdb** 데이터베이스에 저장 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|작업의 ID입니다.|  
|**step_id**|**int**|작업 단계의 ID입니다.|  
|**step_name**|**sysname**|작업 단계의 이름입니다.|  
|**하위**|**nvarchar(40)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 작업 단계를 실행하는 데 사용하는 하위 시스템의 이름입니다.|  
|**command**|**nvarchar(max)**|**하위 시스템**에서 실행할 명령입니다.|  
|**flags**|**int**|예약되어 있습니다.|  
|**additional_parameters**|**ntext**|예약되어 있습니다.|  
|**cmdexec_success_code**|**int**|성공을 표시 하기 위해 **CmdExec** 하위 시스템 단계에서 반환 되는 오류 수준 값입니다.|  
|**on_success_action**|**tinyint**|단계가 성공적으로 실행되었을 때 수행되는 동작입니다.<br /><br /> **1** = (기본값) 성공으로 종료<br /><br /> **2** = 실패로 종료<br /><br /> **3** = 다음 단계로 이동<br /><br /> **4** = 단계로 이동 _on_success_step_id_|
|**on_success_step_id**|**int**|단계가 성공적으로 실행되었을 때 다음으로 실행되는 단계의 ID입니다.|  
|**on_fail_action**|**tinyint**|단계가 성공적으로 실행되지 않았을 때 수행되는 동작입니다.<br /><br /> **1** = 성공으로 종료<br /><br /> **2** = (기본값) 실패로 종료<br /><br /> **3** = 다음 단계로 이동<br /><br /> **4** = 단계로 이동 _on_fail_step_id_|
|**on_fail_step_id**|**int**|단계가 성공적으로 실행되지 않았을 때 다음으로 실행되는 단계의 ID입니다.|  
|**server**|**sysname**|예약되어 있습니다.|  
|**database_name**|**sysname**|**하위 시스템이** TSQL 인 경우 **명령이** 실행 되는 데이터베이스의 이름입니다.|  
|**database_user_name**|**sysname**|단계를 실행할 때 그 계정을 사용할 데이터베이스 사용자의 이름입니다.|  
|**retry_attempts**|**int**|단계가 실패했을 때 재시도하는 횟수입니다.|  
|**retry_interval**|**int**|재시도 간에 대기하는 시간입니다.|  
|**os_run_priority**|**int**|예약되어 있습니다.|  
|**output_file_name**|**nvarchar(200)**|**Subsystem** 이 TSQL, PowerShell 또는 **CmdExec**일 때 단계의 출력이 저장 되는 파일의 이름입니다 _._|  
|**last_run_outcome**|**int**|작업 단계의 이전 실행 결과입니다.<br /><br /> **0** = 실패<br /><br /> **1** = 성공<br /><br /> **2** = 다시 시도<br /><br /> **3** = 취소 됨<br /><br /> **5** = 알 수 없음|  
|**last_run_duration**|**int**|단계가 마지막으로 실행되었을 때의 시간(hhmmss)입니다.|  
|**last_run_retries**|**int**|작업 단계의 마지막 실행에서 재시도한 횟수입니다.|  
|**last_run_date**|**int**|단계가 마지막으로 실행을 시작했을 때의 날짜(yyyymmdd)입니다.|  
|**last_run_time**|**int**|단계가 마지막으로 실행을 시작했을 때의 시간(hhmmss)입니다.|  
|**proxy_id**|**int**|작업 단계에 대한 프록시입니다.|  
|**step_uid**|**uniqueidentifier**|작업 단계에 대한 식별자입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;테이블 SQL Server 에이전트](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)  
  
  
