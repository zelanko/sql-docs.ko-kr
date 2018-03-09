---
title: "SQL Server 에이전트 마스터 작업 만들기 | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server Agent], master jobs
- jobs [SQL Server Agent], creating
- master SQL Server Agent job [SQL Server]
ms.assetid: c12ab23f-d7ee-43a5-8cd2-0a9121292bcd
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: facd1c7844f38badf21ef89e240e7824af1b37ee
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="create-a-sql-server-agent-master-job"></a>SQL Server 에이전트 마스터 작업 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql_md.md)]을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)]에서 마스터 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 작업을 만드는 방법을 보여 줍니다.  
  
**항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
    [제한 사항](#Restrictions)  
  
    [보안](#Security)  
  
-   **다음을 사용하여 마스터 SQL Server 에이전트 작업을 만듭니다.**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="Restrictions"></a>제한 사항  
마스터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 작업에 대한 변경 내용은 관련된 모든 대상 서버에 전파되어야 합니다. 대상 서버는 해당 대상이 지정될 때까지 처음에 작업을 다운로드하지 않으므로 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 는 사용자가 대상 서버를 지정하기 전에 특정 작업에 대한 모든 작업 단계 및 작업 일정을 완료하도록 권장합니다. 그렇지 않으면 **sp_post_msx_operation** 저장 프로시저를 실행하거나 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]를 사용하여 작업을 수정하여 대상 서버가 수정된 작업을 다시 다운로드하도록 수동으로 요청해야 합니다. 자세한 내용은 [sp_post_msx_operation(Transact-SQL)](http://msdn.microsoft.com/en-us/085deef8-2709-4da9-bb97-9ab32effdacf) 또는 [작업 수정](../../ssms/agent/modify-a-job.md)을 참조하세요.  
  
### <a name="Security"></a>보안  
  
#### <a name="Permissions"></a>Permissions  
프록시와 연관된 단계가 있는 배포된 작업은 대상 서버의 프록시 계정 컨텍스트로 실행됩니다. 다음 조건이 만족되는지 또는 프록시와 연관된 작업 단계가 마스터 서버에서 대상으로 다운로드되지 않는지 확인하세요.  
  
-   레지스트리 하위 키 **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<&#42;instance_name&#42;>\SQL Server Agent\AllowDownloadedJobsToMatchProxyName** (REG_DWORD)을 1(true)로 설정합니다. 기본적으로 이 하위 키는 0(false)으로 설정됩니다.  
  
-   프록시 계정이 작업 단계가 실행되는 마스터 서버 프록시 계정과 동일한 이름을 가진 대상 서버에 있는지 여부  
  
마스터 서버에서 대상 서버로 다운로드할 때 프록시 계정을 사용하는 작업 단계가 실패한 경우 **msdb** 데이터베이스의 **sysdownloadlist** 테이블에 있는 **error_message** 열에서 다음 오류 메시지를 확인할 수 있습니다.  
  
-   "작업 단계에 프록시 계정이 필요하지만 일치하는 프록시를 대상 서버에서 사용할 수 없습니다." 이 오류를 해결하려면 **AllowDownloadedJobsToMatchProxyName** 레지스트리 하위 키를 1로 설정합니다.  
  
-   "프록시를 찾을 수 없습니다." 이 오류를 해결하려면 프록시 계정이 작업 단계가 실행되는 마스터 서버 프록시 계정과 동일한 이름을 가진 대상 서버에 있는지 확인합니다.  
  
## <a name="SSMSProcedure"></a>SQL Server Management Studio 사용  
  
#### <a name="to-create-a-master-sql-server-agent-job"></a>마스터 SQL Server 에이전트 작업을 만들려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 SQL Server 에이전트 작업을 만들려는 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **SQL Server 에이전트**를 확장합니다.  
  
3.  **작업** 폴더를 마우스 오른쪽 단추로 클릭하고 **새 작업...**을 선택합니다.  
  
4.  **새 작업** 대화 상자의 **일반** 페이지에서 작업의 일반 속성을 수정합니다. 이 페이지에서 사용할 수 있는 옵션에 대한 자세한 내용은 [작업 속성 - 새 작업&#40;일반 페이지&#41;](../../ssms/agent/job-properties-new-job-general-page.md)을 참조하세요.  
  
5.  **단계** 페이지에서 작업 단계를 구성합니다. 이 페이지에서 사용할 수 있는 옵션에 대한 자세한 내용은 [작업 속성 - 새 작업&#40;단계 페이지&#41;](../../ssms/agent/job-properties-new-job-steps-page.md)을 참조하세요.  
  
6.  **일정** 페이지에서 작업 일정을 구성합니다. 이 페이지에서 사용할 수 있는 옵션에 대한 자세한 내용은 [작업 속성 - 새 작업&#40;일정 페이지&#41;](../../ssms/agent/job-properties-new-job-schedules-page.md)을 참조하세요.  
  
7.  **경고** 페이지에서 작업에 대한 경고를 구성합니다. 이 페이지에서 사용할 수 있는 옵션에 대한 자세한 내용은 [작업 속성 - 새 작업&#40;경고 페이지&#41;](../../ssms/agent/job-properties-new-job-alerts-page.md)을 참조하세요.  
  
8.  **알림** 페이지에서 작업이 완료되었을 때 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트가 수행할 동작을 설정합니다. 이 페이지에서 사용할 수 있는 옵션에 대한 자세한 내용은 [작업 속성 - 새 작업&#40;알림 페이지&#41;](../../ssms/agent/job-properties-new-job-notifications-page.md)을 참조하세요.  
  
9. **대상** 페이지에서 작업의 대상 서버를 관리합니다. 이 페이지에서 사용할 수 있는 옵션에 대한 자세한 내용은 [작업 속성 - 새 작업&#40;대상 페이지&#41;](../../ssms/agent/job-properties-new-job-targets-page.md)을 참조하세요.  
  
10. 완료되었으면 **확인**을 클릭합니다.  
  
## <a name="TsqlProcedure"></a>Transact-SQL 사용  
  
#### <a name="to-create-a-master-sql-server-agent-job"></a>마스터 SQL Server 에이전트 작업을 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde_md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE msdb ;  
    GO  
    -- Adds a new job executed by the SQLServerAgent service called 'Weekly Sales Data Backup'  
    EXEC dbo.sp_add_job  
        @job_name = N'Weekly Sales Data Backup' ;  
    GO  
    -- Adds a step (operation) to the 'Weekly Sales Data Backup' job.  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Set database to read only',  
        @subsystem = N'TSQL',  
        @command = N'ALTER DATABASE SALES SET READ_ONLY',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    -- Creates a schedule called RunOnce  
    EXEC dbo.sp_add_schedule  
        @schedule_name = N'RunOnce',  
        @freq_type = 1,  
        @active_start_time = 233000 ;  
    USE msdb ;  
    GO  
    -- Sets the 'RunOnce' schedule to the "Weekly Sales Data Backup' Job  
    EXEC sp_attach_schedule  
       @job_name = N'Weekly Sales Data Backup',  
       @schedule_name = N'RunOnce';  
    GO  
    -- assigns the multiserver job Weekly Sales Backups to the server SEATTLE2  
    -- assumes that SEATTLE2 is registered as a target server for the current instance.  
    EXEC dbo.sp_add_jobserver  
        @job_name = N'Weekly Sales Data Backups',  
        @server_name = N'SEATTLE2' ;  
    GO  
    ```  
  
참조 항목:  
  
-   [sp_add_job(Transact-SQL)](http://msdn.microsoft.com/en-us/6ca8fe2c-7b1c-4b59-b4c7-e3b7485df274)  
  
-   [sp_add_jobstep(Transact-SQL)](http://msdn.microsoft.com/en-us/97900032-523d-49d6-9865-2734fba1c755)  
  
-   [sp_add_schedule(Transact-SQL)](http://msdn.microsoft.com/en-us/9060aae3-3ddd-40a5-83bb-3ea7ab1ffbd7)  
  
-   [sp_attach_schedule(Transact-SQL)](http://msdn.microsoft.com/en-us/80c80eaf-cf23-4ed8-b8dd-65fe59830dd1)  
  
-   [sp_add_jobserver(Transact-SQL)](http://msdn.microsoft.com/en-us/485252cc-0081-490a-9bd1-cbbd68eea286)  
  
