---
title: sp_post_msx_operation (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- sp_post_msx_operation
- sp_post_msx_operation_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_post_msx_operation
ms.assetid: 085deef8-2709-4da9-bb97-9ab32effdacf
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1774a033e119f14e89a0f5fe141dd99ee0453ec9
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sppostmsxoperation-transact-sql"></a>sp_post_msx_operation(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  연산 (행)에 삽입 된 **sysdownloadlist** 다운로드 및 실행 하려면 대상 서버에 대 한 시스템 테이블입니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_post_msx_operation  
     [ @operation = ] 'operation'  
     [ , [ @object_type = ] 'object' ]   
     { , [ @job_id = ] job_id }   
     [ , [ @specific_target_server = ] 'target_server' ]   
     [ , [ @value = ] value ]  
     [ , [ @schedule_uid = ] schedule_uid ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@operation =**] **'***작업***'**  
 게시된 연산의 유형입니다. *작업*은 **varchar(64)**, 기본값은 없습니다. 올바른 작업을 종속 *object_type*합니다.  
  
|개체 유형|연산|  
|-----------------|---------------|  
|**작업**|INSERT<br /><br /> UPDATE<br /><br /> DELETE<br /><br /> START<br /><br /> STOP|  
|**서버**|RE-ENLIST<br /><br /> DEFECT<br /><br /> SYNC-TIME<br /><br /> SET-POLL|  
|**일정**|INSERT<br /><br /> UPDATE<br /><br /> DELETE|  
  
 [  **@object_type =**] **'***개체***'**  
 연산을 게시할 대상이 되는 개체의 유형입니다. 올바른 유형은 **작업**, **서버**, 및 **일정**합니다. *개체* 은 **varchar(64)**, 기본값은 **작업**합니다.  
  
 [  **@job_id =**] *job_id*  
 연산을 적용할 작업의 ID입니다. *job_id* 은 **uniqueidentifier**, 기본값은 없습니다. **0x00** 모든 작업을 나타냅니다. 경우 *개체* 은 **서버**, 다음 *job_id*필요 하지 않습니다.  
  
 [  **@specific_target_server =**] **'***target_server***'**  
 지정한 연산을 적용할 대상이 되는 대상 서버의 이름입니다. 경우 *job_id* 를 지정 하지만 *target_server* 를 지정 하지 않으면 모든 작업의 서버 작업에 대해 연산이 게시 됩니다. *target_server* 은 **nvarchar (30)**, 기본값은 NULL입니다.  
  
 [  **@value =**] *값*  
 폴링 간격(초)입니다. *value* 는 **int**이며 기본값은 NULL입니다. 경우에만이 매개 변수 지정 *작업* 은 **SET-POLL**합니다.  
  
 [  **@schedule_uid=** ] *schedule_uid*  
 연산을 적용할 일정의 고유 식별자입니다. *schedule_uid* 은 **uniqueidentifier**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>주의  
 **sp_post_msx_operation** 에서 실행 되어야 합니다는 **msdb** 데이터베이스입니다.  
  
 **sp_post_msx_operation** 수를 항상 호출 안전 하 게 먼저 현재 서버가 다중 서버 Microsoft SQL Server 에이전트 경우 그리고 있다면를 결정 하기 때문에 있는지 여부를 *개체*은 다중 서버 작업입니다.  
  
 작업이 게시 된 후에 저장 되는 **sysdownloadlist** 테이블입니다. 작업이 생성 및 게시된 후에는 해당 작업의 후속 변경 내용도 대상 서버(TSX)로 통신되어야 합니다. 이는 또한 다운로드 목록을 사용하여 수행됩니다.  
  
 SQL Server Management Studio를 사용하여 다운로드 목록을 관리하는 것이 좋습니다. 자세한 내용은 참조 [보기 또는 수정 작업](http://msdn.microsoft.com/library/57f649b8-190c-4304-abd7-7ca5297deab7)합니다.  
  
## <a name="permissions"></a>Permissions  
 이 저장된 프로시저를 실행 하려면 사용자에 게 부여 해야 합니다는 **sysadmin** 고정된 서버 역할입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_add_jobserver &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_delete_job &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_delete_jobserver &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [sp_delete_targetserver &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql.md)   
 [sp_resync_targetserver &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql.md)   
 [sp_start_job&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)   
 [sp_stop_job &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-stop-job-transact-sql.md)   
 [sp_update_job &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [sp_update_operator &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
