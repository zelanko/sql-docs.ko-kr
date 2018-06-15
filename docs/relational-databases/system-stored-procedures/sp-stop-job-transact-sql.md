---
title: sp_stop_job (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_stop_job_TSQL
- sp_stop_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_stop_job
ms.assetid: 64b4cc75-99a0-421e-b418-94e37595bbb0
caps.latest.revision: 38
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 67e1476e8f0612796e3f31644aca192c2c25a90f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33258698"
---
# <a name="spstopjob-transact-sql"></a>sp_stop_job(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 작업 실행을 중지하도록 지시합니다.  

  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_stop_job   
      [@job_name =] 'job_name'  
    | [@job_id =] job_id   
    | [@originating_server =] 'master_server'  
    | [@server_name =] 'target_server'  
```  
  
## <a name="arguments"></a>인수  
 [ **@job_name =**] **'***job_name***'**  
 중지할 작업의 이름입니다. *job_name* 은 **sysname**, 기본값은 NULL입니다.  
  
 [ **@job_id =**] *job_id*  
 중지할 작업의 ID입니다. *job_id* 은 **uniqueidentifier**, 기본값은 NULL입니다.  
  
 [ **@originating_server =**] **'***master_server***'**  
 마스터 서버의 이름입니다. 지정된 경우 모든 다중 서버 작업이 중지됩니다. *master_server* 은 **nvarchar (128)**, 기본값은 NULL입니다. 호출 하는 경우에이 매개 변수를 지정 **sp_stop_job** 대상 서버에 있습니다.  
  
> [!NOTE]  
>  처음 세 매개 변수 중 하나만 지정할 수 있습니다.  
  
 [ **@server_name =**] **'***target_server***'**  
 다중 서버 작업을 중지할 특정 대상 서버의 이름입니다. *target_server* 은 **nvarchar (128)**, 기본값은 NULL입니다. 호출 하는 경우에이 매개 변수를 지정 **sp_stop_job** 다중 서버 작업에 대 한 마스터 서버에 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>주의  
 **sp_stop_job** 데이터베이스에 중지 신호를 보냅니다. 일부 프로세스를 즉시 중지 될 수 있으며 안정적인 지점 (또는 코드 경로에 대 한 진입점)에 도달 해야 일부 전에 중지할 수 있습니다. BACK, RESTORE 및 일부 DBCC 명령과 같은 일부 장기 실행 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 완료되려면 시간이 오래 걸릴 수 있습니다. 작업을 취소 하기 전에, 실행 되는 시간이 걸릴 수 있습니다. 작업을 중지하면 작업 기록에 "취소된 작업" 항목이 기록됩니다.  
  
 작업이 현재 유형의 단계를 실행 하는 경우 **CmdExec** 또는 **PowerShell**, 중간에 종료 되도록 하면 프로세스가 실행 되 고 (예: MyProgram.exe) 강제 적용 합니다. 예기치 않은 종료로 인해 프로세스가 보유하고 있던 파일이 열리는 등 예기치 않은 상황이 발생할 수 있습니다. 따라서 **sp_stop_job** 작업 유형의 단계가 포함 되어 있는 경우 처럼 극단적인 상황 에서만에서 사용 해야 **CmdExec** 또는 **PowerShell**합니다.  
  
## <a name="permissions"></a>Permissions  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)을 참조하세요.  
  
 멤버 **SQLAgentUserRole** 및 **SQLAgentReaderRole** 는 각자 소유한 작업만 중지할 수 있습니다. 멤버 **SQLAgentOperatorRole** 다른 사용자가 소유 하는 포함 하 여 모든 로컬 작업을 중지할 수 있습니다. 멤버 **sysadmin** 모든 로컬 및 다중 서버 작업을 중지할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Weekly Sales Data Backup`이라는 작업을 중지합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_stop_job  
    N'Weekly Sales Data Backup' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sp_delete_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_help_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_start_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)   
 [sp_update_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
