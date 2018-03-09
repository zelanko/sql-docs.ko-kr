---
title: MSsubscriber_schedule (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- MSsubscriber_schedule
- MSsubscriber_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscriber_schedule system table
ms.assetid: ff428306-0ef4-49a3-b536-07ccdf6e2196
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 983ea7374e26cfae1c3313f1e4eaec9bd287ff22
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="mssubscriberschedule-transact-sql"></a>MSsubscriber_schedule(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSsubscriber_schedule** 기본 병합 및 트랜잭션 동기화 일정이 각 게시자/구독자 쌍에 대 한 테이블을 포함 합니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
> [!NOTE]  
>  이 시스템 테이블은 사용 되지 않으며 이전 버전의 지원 하기 위해 유지 되 고 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|게시자의 이름입니다.|  
|**subscriber**|**sysname**|구독자 이름입니다.|  
|**agent_type**|**smallint**|에이전트의 유형입니다.<br /><br /> 0 = 배포 에이전트<br /><br /> 1 = 병합 에이전트|  
|**frequency_type**|**int**|배포 에이전트의 일정을 지정하는 빈도입니다.<br /><br /> **1** = 한 번입니다.<br /><br /> **2** = 요청 시.<br /><br /> **4** = 매일 합니다.<br /><br /> **8** = 매주입니다.<br /><br /> **16** = 매월 합니다.<br /><br /> **32** = 매월 상대적입니다.<br /><br /> **64** = 자동 시작 합니다.<br /><br /> **128** = 되풀이 합니다.|  
|**frequency_interval**|**int**|설정 된 빈도에 적용할 값 **frequency_type**합니다.|  
|**frequency_relative_interval**|**int**|배포 에이전트의 날짜입니다.<br /><br /> **1** = 첫 번째입니다.<br /><br /> **2** = 초입니다.<br /><br /> **4** = 세 번째입니다.<br /><br /> **8** = 네 번째입니다.<br /><br /> **16** = 마지막 합니다.|  
|**frequency_recurrence_factor**|**int**|사용 하는 되풀이 비율 **frequency_type**합니다.|  
|**frequency_subday**|**int**|정의된 기간 동안 일정을 변경하는 빈도입니다.<br /><br /> **1** = 1입니다.<br /><br /> **2** = 초입니다.<br /><br /> **4** = 분입니다.<br /><br /> **8** = 시간입니다.|  
|**frequency_subday_interval**|**int**|에 대 한 간격 **frequency_subday**합니다.|  
|**active_start_time_of_day**|**int**|배포 에이전트가 처음으로 실행되도록 예약된 시간이며 HHMMSS 형식으로 표시됩니다.|  
|**active_end_time_of_day**|**int**|배포 에이전트가 마지막으로 실행되도록 예약된 시간이며 HHMMSS 형식으로 표시됩니다.|  
|**active_start_date**|**int**|배포 에이전트가 처음으로 실행되도록 예약된 날짜이며 YYYYMMDD 형식으로 표시됩니다.|  
|**active_end_date**|**int**|배포 에이전트가 마지막으로 실행되도록 예약된 날짜이며 YYYYMMDD 형식으로 표시됩니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블 &#40; Transact SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
