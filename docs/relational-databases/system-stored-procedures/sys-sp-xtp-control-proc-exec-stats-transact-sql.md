---
title: sys. sp_xtp_control_proc_exec_stats (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_xtp_control_proc_exec_stats
- sys.sp_xtp_control_proc_exec_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_xtp_control_proc_exec_stats
ms.assetid: f5119808-76a1-4522-8529-9e02ee39adcb
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9d011be97c90f156b8cd26cfb8fcc85963b75161
ms.sourcegitcommit: 039fb38c583019b3fd06894160568387a19ba04e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2020
ms.locfileid: "87442397"
---
# <a name="syssp_xtp_control_proc_exec_stats-transact-sql"></a>sys.sp_xtp_control_proc_exec_stats(Transact-SQL)
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

  인스턴스의 고유하게 컴파일된 저장 프로시저에 대한 통계 수집을 설정합니다.  
  
 고유 하 게 컴파일된 저장 프로시저에 대 한 쿼리 수준에서 통계 컬렉션을 사용 하도록 설정 하려면 [sp_xtp_control_query_exec_stats &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md)을 참조 하십시오.  
  
## <a name="syntax"></a>구문  
  
```  
sp_xtp_control_proc_exec_stats [ [ @new_collection_value = ] collection_value ], [ @old_collection_value]  
```  
  
## <a name="arguments"></a>인수  
 @new_collection_value= *값*  
 프로시저 수준 통계 컬렉션이 설정(1)되었는지 아니면 해제(0)되었는지를 결정합니다.  
  
 @new_collection_value는 또는 데이터베이스가 시작 될 때 0으로 설정 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 @old_collection_value= *값*  
 현재 상태를 반환합니다.  
  
## <a name="return-code"></a>반환 코드  
 성공의 경우 0이고, 실패의 경우 0이 아닙니다.  
  
## <a name="permissions"></a>사용 권한  
 고정 sysadmin 역할의 멤버 자격이 필요합니다.  
  
## <a name="code-samples"></a>코드 샘플  
 의 값을 설정 하 @new_collection_value 고 쿼리하려면@new_collection_value:  
  
```  
exec [sys].[sp_xtp_control_proc_exec_stats] @new_collection_value = 1  
declare @c bit  
exec sp_xtp_control_proc_exec_stats @old_collection_value=@c output  
select @c as 'collection status'  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
