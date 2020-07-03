---
title: sp_post_msx_operation (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_post_msx_operation
- sp_post_msx_operation_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_post_msx_operation
ms.assetid: 085deef8-2709-4da9-bb97-9ab32effdacf
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 36759d2c90e29c0a019d8bd294a0c7e621c8d468
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85891557"
---
# <a name="sp_post_msx_operation-transact-sql"></a>sp_post_msx_operation(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  대상 서버를 다운로드 하 여 실행할 **sysdownloadlist** 시스템 테이블에 작업 (행)을 삽입 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @operation = ] 'operation'`게시 된 작업에 대 한 작업의 유형입니다. *연산은* **varchar (64)** 이며 기본값은 없습니다. 유효한 작업은 *object_type*에 따라 달라 집니다.  
  
|개체 유형|작업(Operation)|  
|-----------------|---------------|  
|**직함**|INSERT<br /><br /> UPDATE<br /><br /> Delete<br /><br /> START<br /><br /> STOP|  
|**서버인**|RE-ENLIST<br /><br /> DEFECT<br /><br /> SYNC-TIME<br /><br /> SET-POLL|  
|**일정과**|INSERT<br /><br /> UPDATE<br /><br /> Delete|  
  
`[ @object_type = ] 'object'`작업을 게시할 개체의 형식입니다. 유효한 유형은 **JOB**, **SERVER**및 **SCHEDULE**입니다. *개체가* **varchar (64)** 이며 기본값은 **JOB**입니다.  
  
`[ @job_id = ] job_id`작업이 적용 되는 작업의 id입니다. *job_id* 은 **uniqueidentifier**이며 기본값은 없습니다. **0x00** 은 모든 작업을 나타냅니다. *Object* 가 **SERVER**인 경우 *job_id*필요 하지 않습니다.  
  
`[ @specific_target_server = ] 'target_server'`지정 된 작업이 적용 되는 대상 서버의 이름입니다. *Job_id* 지정 되었지만 *target_server* 지정 되지 않은 경우 작업의 모든 작업 서버에 대해 작업이 게시 됩니다. *target_server* 은 **nvarchar (30)** 이며 기본값은 NULL입니다.  
  
`[ @value = ] value`폴링 간격 (초)입니다. *value* 는 **int**이며 기본값은 NULL입니다. *작업이* **설정-폴링**인 경우에만이 매개 변수를 지정 합니다.  
  
`[ @schedule_uid = ] schedule_uid`작업이 적용 되는 일정의 고유 식별자입니다. *schedule_uid* 은 **uniqueidentifier**이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 **sp_post_msx_operation** 는 **msdb** 데이터베이스에서 실행 해야 합니다.  
  
 항상 현재 서버가 다중 서버 Microsoft SQL Server 에이전트 인지 여부와 *개체가*다중 서버 작업 인지 여부를 결정 하므로 항상 안전 하 게 호출할 수 **sp_post_msx_operation** .  
  
 작업이 게시 된 후에는 **sysdownloadlist** 테이블에 표시 됩니다. 작업이 생성 및 게시된 후에는 해당 작업의 후속 변경 내용도 대상 서버(TSX)로 통신되어야 합니다. 이는 또한 다운로드 목록을 사용하여 수행됩니다.  
  
 SQL Server Management Studio를 사용하여 다운로드 목록을 관리하는 것이 좋습니다. 자세한 내용은 [작업 보기 또는 수정](../../ssms/agent/view-or-modify-jobs.md)을 참조 하세요.  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행 하려면 사용자에 게 **sysadmin** 고정 서버 역할을 부여 해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_add_jobserver &#40;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [Transact-sql&#41;sp_delete_job &#40;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [Transact-sql&#41;sp_delete_jobserver &#40;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [Transact-sql&#41;sp_delete_targetserver &#40;](../../relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql.md)   
 [Transact-sql&#41;sp_resync_targetserver &#40;](../../relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql.md)   
 [Transact-sql&#41;sp_start_job &#40;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)   
 [Transact-sql&#41;sp_stop_job &#40;](../../relational-databases/system-stored-procedures/sp-stop-job-transact-sql.md)   
 [Transact-sql&#41;sp_update_job &#40;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [Transact-sql&#41;sp_update_operator &#40;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
