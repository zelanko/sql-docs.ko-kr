---
title: dbo.sysjobschedules (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysjobschedules
- dbo.sysjobschedules
- dbo.sysjobschedules_TSQL
- sysjobschedules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobschedules system table
ms.assetid: ccdafec7-2a9b-4356-bffb-1caa3a12db59
caps.latest.revision: 32
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2818512730a99bf7352c87f7d651d3084870767f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="dbosysjobschedules-transact-sql"></a>dbo.sysjobschedules(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 실행할 작업에 관한 일정 정보를 포함합니다. 이 테이블에 저장 되는 **msdb** 데이터베이스입니다.  
  
> **참고:** 는 **sysjobschedules** 테이블 반환 하는 값에 영향을 줄 수는 20 분 마다 새로 **sp_help_jobschedule** 저장 프로시저입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|일정의 ID입니다.|  
|**job_id**|**uniqueidentifier**|작업의 ID입니다.|  
|**next_run_date**|**int**|작업을 실행하도록 예약된 다음 날짜입니다. 날짜 형식은 YYYYMMDD입니다.|  
|**next_run_time**|**int**|작업을 실행하도록 예약된 시간입니다. 시간 형식은 HHMMSS이며 24시간제를 사용합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [dbo.sysschedules &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-sysschedules-transact-sql.md)  
  
  
