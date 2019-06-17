---
title: KILL STATS JOB(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- KILL STATS JOB
- KILL_STATS_JOB_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ending statistics update jobs [SQL Server]
- stopping statistics update jobs
- terminating statistics update jobs
- asynchronous statistics updates [SQL Server]
- KILL STATS JOB statement
- statistics update jobs [SQL Server]
ms.assetid: 55a8f9f1-3259-45c0-8ab9-60b9c088b4b4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c2a2a034348df16f7ea1f326d78322f578953757
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65982138"
---
# <a name="kill-stats-job-transact-sql"></a>KILL STATS JOB(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 비동기 통계 업데이트 작업을 종료합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
KILL STATS JOB job_id   
```  
  
## <a name="arguments"></a>인수  
 *job_id*  
 작업의 sys.dm_exec_background_job_queue 동적 관리 뷰에 의해 반환된 job_id 필드입니다.  
  
## <a name="remarks"></a>Remarks  
 job_id는 KILL 문의 다른 형식에 사용되는 session_id 또는 작업 단위와 관련이 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 사용자는 sys.dm_exec_background_job_queue 동적 관리 뷰에서 정보를 액세스할 수 있는 VIEW SERVER STATE 권한이 있어야 합니다.  
  
 KILL STATS JOB 권한은 sysadmin과 processadmin 고정 데이터베이스 역할의 멤버에게 기본적으로 부여되며 위임할 수 없습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 *job_id* = `53`인 작업과 관련된 통계 업데이트를 종료하는 방법을 보여 줍니다.  
  
```  
KILL STATS JOB 53;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [KILL&#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-transact-sql.md)   
 [KILL QUERY NOTIFICATION SUBSCRIPTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-query-notification-subscription-transact-sql.md)   
 [sys.dm_exec_background_job_queue&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-background-job-queue-transact-sql.md)   
 [통계](../../relational-databases/statistics/statistics.md)  
  
  
