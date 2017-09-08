---
title: KILL STATS JOB (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7f1738c96709d2eb1489c9ec25c598459842e3ab
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="kill-stats-job-transact-sql"></a>KILL STATS JOB(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 비동기 통계 업데이트 작업을 종료합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
KILL STATS JOB job_id   
```  
  
## <a name="arguments"></a>인수  
 *job_id*  
 작업의 sys.dm_exec_background_job_queue 동적 관리 뷰에 의해 반환된 job_id 필드입니다.  
  
## <a name="remarks"></a>주의  
 job_id는 KILL 문의 다른 형식에 사용되는 session_id 또는 작업 단위와 관련이 없습니다.  
  
## <a name="permissions"></a>Permissions  
 사용자는 sys.dm_exec_background_job_queue 동적 관리 뷰에서 정보를 액세스할 수 있는 VIEW SERVER STATE 권한이 있어야 합니다.  
  
 KILL STATS JOB 권한은 sysadmin과 processadmin 고정 데이터베이스 역할의 멤버에게 기본적으로 부여되며 위임할 수 없습니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 작업과 관련 된 통계 업데이트를 종료 하는 방법을 보여 줍니다. 여기서는 *job_id* = `53`합니다.  
  
```  
KILL STATS JOB 53;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Kill&#40; Transact SQL &#41;](../../t-sql/language-elements/kill-transact-sql.md)   
 [KILL QUERY NOTIFICATION SUBSCRIPTION &#40; Transact SQL &#41;](../../t-sql/language-elements/kill-query-notification-subscription-transact-sql.md)   
 [sys.dm_exec_background_job_queue &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-background-job-queue-transact-sql.md)   
 [통계](../../relational-databases/statistics/statistics.md)  
  
  

