---
title: sp_dropdynamicsnapshot_job (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_dropdynamicsnapshot_job_TSQL
- sp_dropdynamicsnapshot_job
helpviewer_keywords:
- sp_dropdynamicsnapshot_job
ms.assetid: 128e428a-01b3-4062-8c6e-d22d5fa268a9
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 2f4166aa3cfed68aae16bdccd09a001ef55f3661
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32988788"
---
# <a name="spdropdynamicsnapshotjob-transact-sql"></a>sp_dropdynamicsnapshot_job(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  매개 변수가 있는 행 필터를 사용하여 게시에 대한 필터링된 데이터 스냅숏 작업을 제거합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다. 관련된 데이터의 모든에서 삭제 작업을 삭제 하는 경우는 [MSdynamicsnapshotjobs](../../relational-databases/system-tables/msdynamicsnapshotjobs-transact-sql.md) 시스템 테이블입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dropdynamicsnapshot_job [ @publication = ] 'publication'   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]   
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]   
    [ , [ @ignore_distributor =] ignore_distributor ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@publication=**] **'***publication***'**  
 필터링된 데이터 스냅숏 작업을 제거할 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 없습니다.  
  
 [ **@dynamic_snapshot_jobname**=] **'***dynamic_snapshot_jobname***'**  
 제거할 필터링된 데이터 스냅숏 작업의 이름입니다. *dynamic_snapshot_jobname*은 sysname 이며 기본값 없으면 모든 작업에 연결 된 이름이 *dynamic_snapshot_jobid*합니다.  
  
 [ **@dynamic_snapshot_jobid**=] **'***dynamic_snapshot_jobid***'**  
 제거할 필터링된 데이터 스냅숏 작업에 대한 식별자입니다. *dynamic_snapshot_jobid*은 **uniqueidentifier**, 기본값은 NULL입니다.  
  
> [!IMPORTANT]  
>  만 *dynamic_snapshot_jobid*또는 *dynamic_snapshot_jobname* 지정할 수 있습니다. 에 대 한 값을 제공 하지 않는 경우 *dynamic_snapshot_jobid*또는 *dynamic_snapshot_jobname*, 게시에 대 한 모든 동적 스냅숏 작업이 제거 됩니다.  
  
 [  **@ignore_distributor =**] *ignore_distributor*  
 *ignore_distributor* 은 **비트**, 기본값은 **0**합니다. 이 매개 변수는 배포자에서 태스크를 정리하지 않고 동적 스냅숏 동작을 삭제하는 데 사용할 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_dropdynamicsnapshot** 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_dropdynamicsnapshot**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_adddynamicsnapshot_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql.md)  
  
  
