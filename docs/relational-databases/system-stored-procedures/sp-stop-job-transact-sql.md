---
title: sp_stop_job (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_stop_job_TSQL
- sp_stop_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_stop_job
ms.assetid: 64b4cc75-99a0-421e-b418-94e37595bbb0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9a0549d247078634feadced301570e00746d5ba7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68032725"
---
# <a name="sp_stop_job-transact-sql"></a>sp_stop_job(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 작업 실행을 중지하도록 지시합니다.  

  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_stop_job   
      [@job_name =] 'job_name'  
    | [@job_id =] job_id   
    | [@originating_server =] 'master_server'  
    | [@server_name =] 'target_server'  
```  
  
## <a name="arguments"></a>인수  
`[ @job_name = ] 'job_name'`중지할 작업의 이름입니다. *job_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @job_id = ] job_id`중지할 작업의 id입니다. *job_id* 은 **uniqueidentifier**이며 기본값은 NULL입니다.  
  
`[ @originating_server = ] 'master_server'`마스터 서버의 이름입니다. 지정된 경우 모든 다중 서버 작업이 중지됩니다. *master_server* 은 **nvarchar (128)** 이며 기본값은 NULL입니다. 대상 서버에서 **sp_stop_job** 를 호출할 때만이 매개 변수를 지정 합니다.  
  
> [!NOTE]  
>  처음 세 매개 변수 중 하나만 지정할 수 있습니다.  
  
`[ @server_name = ] 'target_server'`다중 서버 작업을 중지할 특정 대상 서버의 이름입니다. *target_server* 은 **nvarchar (128)** 이며 기본값은 NULL입니다. 다중 서버 작업에 대해 마스터 서버에서 **sp_stop_job** 를 호출할 때만이 매개 변수를 지정 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 **sp_stop_job** 는 데이터베이스에 중지 신호를 보냅니다. 일부 프로세스는 즉시 중지 될 수 있으며 일부 프로세스는 중지 하기 전에 안정 된 지점 (또는 코드 경로에 대 한 진입점)에 도달 해야 합니다. BACK, RESTORE 및 일부 DBCC 명령과 같은 일부 장기 실행 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 완료되려면 시간이 오래 걸릴 수 있습니다. 이러한 작업을 실행 하는 경우 작업이 취소 되기 전에 약간의 시간이 걸릴 수 있습니다. 작업을 중지하면 작업 기록에 "취소된 작업" 항목이 기록됩니다.  
  
 작업에서 현재 **CmdExec** 또는 **PowerShell**유형의 단계를 실행 하는 경우 실행 중인 프로세스 (예: myprogram .exe)가 강제로 중간에 종료 됩니다. 예기치 않은 종료로 인해 프로세스가 보유하고 있던 파일이 열리는 등 예기치 않은 상황이 발생할 수 있습니다. 따라서 작업에 **CmdExec** 또는 **PowerShell**유형의 단계가 포함 된 경우에는 극단적인 경우에만 **sp_stop_job** 을 사용 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
 **SQLAgentUserRole** 및 **SQLAgentReaderRole** 의 멤버는 자신이 소유한 작업만 중지할 수 있습니다. **SQLAgentOperatorRole** 의 멤버는 다른 사용자가 소유 하는 작업을 포함 하 여 모든 로컬 작업을 중지할 수 있습니다. **Sysadmin** 의 멤버는 모든 로컬 및 다중 서버 작업을 중지할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Weekly Sales Data Backup`이라는 작업을 중지합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_stop_job  
    N'Weekly Sales Data Backup' ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_delete_job &#40;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [Transact-sql&#41;sp_help_job &#40;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [Transact-sql&#41;sp_start_job &#40;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)   
 [Transact-sql&#41;sp_update_job &#40;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
