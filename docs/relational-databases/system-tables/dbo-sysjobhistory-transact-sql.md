---
title: dbo.sysjobhistory (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/24/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysjobhistory_TSQL
- dbo.sysjobhistory
- sysjobhistory
- sysjobhistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobhistory system table
ms.assetid: 1b1fcdbb-2af2-45e6-bf3f-e8279432ce13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 809e8c80ec1734c24f6930b4042b5e1a84356597
ms.sourcegitcommit: 65ceea905030582f8d89e75e97758abf3b1f0bd6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2019
ms.locfileid: "67400110"
---
# <a name="dbosysjobhistory-transact-sql"></a>dbo.sysjobhistory(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트의 예약된 작업 실행에 대한 정보를 포함합니다.
  
> [!NOTE]
> 대부분의 경우에만 기본 프로세스의 경우 작업 단계가 완료 된 후 테이블에는 일반적으로 현재 진행 중인 작업 단계에 대 한 레코드가 포함 되지만 일부 데이터가 업데이트 되 *수행* 에 대 한 정보 제공 작업 단계를 진행 합니다.

이 테이블에 저장 되는 **msdb** 데이터베이스입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**instance_id**|**int**|행의 고유한 식별자입니다.|  
|**job_id**|**uniqueidentifier**|작업 ID입니다.|  
|**step_id**|**int**|작업 단계의 ID입니다.|  
|**step_name**|**sysname**|단계의 이름입니다.|  
|**sql_message_id**|**int**|작업이 실패한 경우 반환된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 메시지의 ID입니다.|  
|**sql_severity**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류의 심각도입니다.|  
|**message**|**nvarchar(4000)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류의 텍스트(있는 경우)입니다.|  
|**run_status**|**int**|작업의 실행 상태입니다.<br /><br /> **0** = 실패<br /><br /> **1** = 성공<br /><br /> **2** = Retry<br /><br /> **3** = 취소<br /><br />**4** = 진행 중|  
|**run_date**|**int**|작업 또는 단계가 실행을 시작한 날짜입니다. 진행 기록에서는 기록이 작성된 날짜 및 시간입니다.|  
|**run_time**|**int**|작업 또는 단계가 시작된 시간입니다.|  
|**run_duration**|**int**|작업 또는 단계 실행의 경과 시간 **HHMMSS** 형식입니다.|  
|**operator_id_emailed**|**int**|작업이 완료되었을 때 알리는 대상이 되는 운영자의 ID입니다.|  
|**operator_id_netsent**|**int**|작업이 완료되었을 때 메시지로 알리는 대상이 되는 운영자의 ID입니다.|  
|**operator_id_paged**|**int**|작업이 완료되었을 때 호출기로 알리는 대상이 되는 운영자의 ID입니다.|  
|**retries_attempted**|**int**|작업 또는 단계를 다시 시도하는 횟수입니다.|  
|**server**|**sysname**|작업이 실행된 서버의 이름입니다.|  
  
  ## <a name="example"></a>예제
 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리를 변환 합니다 **run_time** 및 **run_duration** 자세한 사용자 친숙 한 형식으로 열입니다.  스크립트를 실행 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다.
 
 ```sql
 SET NOCOUNT ON;
 
 SELECT sj.name,
        sh.run_date,
        sh.step_name,
        STUFF(STUFF(RIGHT(REPLICATE('0', 6) +  CAST(sh.run_time as varchar(6)), 6), 3, 0, ':'), 6, 0, ':') 'run_time',
        STUFF(STUFF(STUFF(RIGHT(REPLICATE('0', 8) + CAST(sh.run_duration as varchar(8)), 8), 3, 0, ':'), 6, 0, ':'), 9, 0, ':') 'run_duration (DD:HH:MM:SS)  '
FROM msdb.dbo.sysjobs sj
JOIN msdb.dbo.sysjobhistory sh
ON sj.job_id = sh.job_id
```
