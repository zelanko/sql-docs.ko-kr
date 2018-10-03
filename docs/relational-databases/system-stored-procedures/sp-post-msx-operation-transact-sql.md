---
title: sp_post_msx_operation (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: aa0293daf2c7dacf65450d8d3b9323b2903e77ce
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47832701"
---
# <a name="sppostmsxoperation-transact-sql"></a>sp_post_msx_operation(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  작업 (행)를 삽입 합니다 **sysdownloadlist** 다운로드 및 실행 하려면 대상 서버에 대 한 시스템 테이블입니다.  
  
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
 [ **@operation =**] **'***operation***'**  
 게시된 연산의 유형입니다. *작업이*됩니다 **varchar(64)**, 기본값은 없습니다. 유효한 작업에 종속 *object_type*합니다.  
  
|개체 유형|연산|  
|-----------------|---------------|  
|**JOB**|INSERT<br /><br /> UPDATE<br /><br /> Delete<br /><br /> START<br /><br /> STOP|  
|**서버**|RE-ENLIST<br /><br /> DEFECT<br /><br /> SYNC-TIME<br /><br /> SET-POLL|  
|**일정**|INSERT<br /><br /> UPDATE<br /><br /> Delete|  
  
 [ **@object_type =**] **'***object***'**  
 연산을 게시할 대상이 되는 개체의 유형입니다. 올바른 유형은 **작업이**, **SERVER**, 및 **일정**합니다. *개체* 됩니다 **varchar(64)**, 기본값은 **작업**합니다.  
  
 [ **@job_id =**] *job_id*  
 연산을 적용할 작업의 ID입니다. *job_id* 됩니다 **uniqueidentifier**, 기본값은 없습니다. **0x00** 모든 작업을 나타냅니다. 경우 *개체* 됩니다 **SERVER**, 한 다음 *job_id*필요 하지 않습니다.  
  
 [ **@specific_target_server =**] **'***target_server***'**  
 지정한 연산을 적용할 대상이 되는 대상 서버의 이름입니다. 하는 경우 *job_id* 지정 되어 있지만 *target_server* 지정 하지 않으면 작업의 모든 작업 서버에 대해 연산이 게시 됩니다. *target_server* 됩니다 **nvarchar(30)**, 기본값은 NULL입니다.  
  
 [ **@value =**] *value*  
 폴링 간격(초)입니다. *value* 는 **int**이며 기본값은 NULL입니다. 경우에만이 매개 변수 지정 *작업이* 됩니다 **SET-POLL**합니다.  
  
 [ **@schedule_uid=** ] *schedule_uid*  
 연산을 적용할 일정의 고유 식별자입니다. *schedule_uid* 됩니다 **uniqueidentifier**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>Remarks  
 **sp_post_msx_operation** 에서 실행 해야 합니다 **msdb** 데이터베이스입니다.  
  
 **sp_post_msx_operation** 수를 항상 호출 안전 하 게 먼저 현재 서버가 다중 서버 Microsoft SQL Server 에이전트 경우 및 경우를 결정 하기 때문에 여부 *개체*다중 서버 작업입니다.  
  
 작업이 게시 된 후에 저장 되는 **sysdownloadlist** 테이블입니다. 작업이 생성 및 게시된 후에는 해당 작업의 후속 변경 내용도 대상 서버(TSX)로 통신되어야 합니다. 이는 또한 다운로드 목록을 사용하여 수행됩니다.  
  
 SQL Server Management Studio를 사용하여 다운로드 목록을 관리하는 것이 좋습니다. 자세한 내용은 [보기 또는 수정 작업](../../ssms/agent/view-or-modify-jobs.md)합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 저장된 프로시저를 실행 하려면 사용자에 부여 해야 합니다 **sysadmin** 고정된 서버 역할입니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_add_jobserver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_delete_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_delete_jobserver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [sp_delete_targetserver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql.md)   
 [sp_resync_targetserver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql.md)   
 [sp_start_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)   
 [sp_stop_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-stop-job-transact-sql.md)   
 [sp_update_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [sp_update_operator &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
