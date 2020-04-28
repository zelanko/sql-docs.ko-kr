---
title: sp_dropdynamicsnapshot_job (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropdynamicsnapshot_job_TSQL
- sp_dropdynamicsnapshot_job
helpviewer_keywords:
- sp_dropdynamicsnapshot_job
ms.assetid: 128e428a-01b3-4062-8c6e-d22d5fa268a9
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5994201f7e6b2b859ef85a7a24e0c0465f59ec31
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68056490"
---
# <a name="sp_dropdynamicsnapshot_job-transact-sql"></a>sp_dropdynamicsnapshot_job(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  매개 변수가 있는 행 필터를 사용하여 게시에 대한 필터링된 데이터 스냅샷 작업을 제거합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다. 작업이 삭제 되 면 관련 된 모든 데이터가 [MSdynamicsnapshotjobs](../../relational-databases/system-tables/msdynamicsnapshotjobs-transact-sql.md) 시스템 테이블에서 삭제 됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dropdynamicsnapshot_job [ @publication = ] 'publication'   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]   
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]   
    [ , [ @ignore_distributor =] ignore_distributor ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`필터링 된 데이터 스냅숏 작업을 제거할 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname'`제거할 필터링 된 데이터 스냅숏 작업의 이름입니다. *dynamic_snapshot_jobname*는 sysname 이며, 지정 되지 않은 경우 *dynamic_snapshot_jobid*와 연결 된 작업 이름을 기본값으로 사용 합니다.  
  
`[ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid'`제거할 필터링 된 데이터 스냅숏 작업의 식별자입니다. *dynamic_snapshot_jobid*은 **uniqueidentifier**이며 기본값은 NULL입니다.  
  
> [!IMPORTANT]  
>  *Dynamic_snapshot_jobid*또는 *dynamic_snapshot_jobname* 만 지정할 수 있습니다. *Dynamic_snapshot_jobid*또는 *dynamic_snapshot_jobname*에 대해 값이 제공 되지 않은 경우 게시에 대 한 모든 동적 스냅숏 작업이 제거 됩니다.  
  
`[ @ignore_distributor = ] ignore_distributor`*ignore_distributor* 은 **bit**이며 기본값은 **0**입니다. 이 매개 변수는 배포자에서 태스크를 정리하지 않고 동적 스냅샷 동작을 삭제하는 데 사용할 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_dropdynamicsnapshot** 는 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_dropdynamicsnapshot**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_adddynamicsnapshot_job &#40;](../../relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql.md)  
  
  
