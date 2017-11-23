---
title: sys.sp_xtp_control_proc_exec_stats (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sp_xtp_control_proc_exec_stats
- sys.sp_xtp_control_proc_exec_stats_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.sp_xtp_control_proc_exec_stats
ms.assetid: f5119808-76a1-4522-8529-9e02ee39adcb
caps.latest.revision: "15"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 721c120c200bb3142b36e06beb6e45cab1ca0805
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sysspxtpcontrolprocexecstats-transact-sql"></a>sys.sp_xtp_control_proc_exec_stats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  인스턴스의 고유하게 컴파일된 저장 프로시저에 대한 통계 수집을 설정합니다.  
  
 고유 하 게 컴파일된 저장된 프로시저에 대 한 쿼리 수준에서 통계 컬렉션을 사용 하려면 참조 [sys.sp_xtp_control_query_exec_stats&#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md).  
  
## <a name="syntax"></a>구문  
  
```  
sp_xtp_control_proc_exec_stats [ [ @new_collection_value = ] collection_value ], [ @old_collection_value]  
```  
  
## <a name="arguments"></a>인수  
 @new_collection_value= *값*  
 프로시저 수준 통계 컬렉션이 설정(1)되었는지 아니면 해제(0)되었는지를 결정합니다.  
  
 @new_collection_value때 0으로 설정 되어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하거나 데이터베이스를 시작 합니다.  
  
 @old_collection_value= *값*  
 현재 상태를 반환합니다.  
  
## <a name="return-code"></a>반환 코드  
 성공의 경우 0이고, 실패의 경우 0이 아닙니다.  
  
## <a name="permissions"></a>Permissions  
 고정 sysadmin 역할의 멤버 자격이 필요합니다.  
  
## <a name="code-samples"></a>코드 예제  
 설정 하려면 @new_collection_value 및의 값에 대 한 쿼리@new_collection_value:  
  
```  
exec [sys].[sp_xtp_control_proc_exec_stats] @new_collection_value = 1  
declare @c bit  
exec sp_xtp_control_proc_exec_stats @old_collection_value=@c output  
select @c as 'collection status'  
```  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
