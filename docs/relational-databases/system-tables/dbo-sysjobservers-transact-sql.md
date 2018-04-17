---
title: dbo.sysjobservers (Transact SQL) | Microsoft Docs
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
- sysjobservers
- sysjobservers_TSQL
- dbo.sysjobservers
- dbo.sysjobservers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobservers system table
ms.assetid: 9abcc20f-a421-4591-affb-62674d04575e
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0b6318809764605fe0288aa0a0638fa9aa5ee02e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="dbosysjobservers-transact-sql"></a>dbo.sysjobservers(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  특정 작업과 하나 이상의 대상 서버와의 연관 또는 관계를 저장합니다. 이 테이블은 msdb 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|job_id|**uniqueidentifier**|작업 ID입니다.|  
|server_id|**int**|서버 ID입니다.|  
|last_run_outcome|**tinyint**|작업이 마지막으로 실행되었을 때의 결과입니다.<br /><br /> **0** = 실패<br /><br /> **1** = 성공<br /><br /> **3** = 취소|  
|last_outcome_ 메시지|**nvarchar(1024)**|last_run_outcome 열과 연관된 메시지(있는 경우)입니다.|  
|last_run_date|**int**|작업을 마지막으로 실행한 날짜입니다.|  
|last_run_time|**int**|작업을 마지막으로 실행한 시간입니다.|  
|last_run_duration|**int**|작업의 실행 시간(시, 분, 초)입니다. 수식을 사용 하 여 계산: (*시간*\*10000) + (*분*\*100) + *초*합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 에이전트 테이블 &#40;Transact SQL&#41;](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)  
  
  
