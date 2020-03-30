---
title: 작업 만들기
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], creating
- SQL Server Agent jobs, creating
ms.assetid: b35af2b6-6594-40d1-9861-4d5dd906048c
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 41e8f5b262b5018bbbc847dc57c27204783e6f32
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75245925"
---
# <a name="create-a-job"></a>작업 만들기
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database Managed Instance T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 SMO(SQL Server 관리 개체)를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 SQL Server 에이전트 작업을 만드는 방법에 대해 설명합니다.  
  
운영자에게 전송할 수 있는 작업 단계, 일정, 경고 및 알림을 추가하려면 참조 섹션에 있는 항목에 대한 링크를 참조하세요.  
  
-   **시작하기 전 주의 사항:**  
  
    [제한 사항](#Restrictions)  
  
    [보안](#Security)  
  
-   **다음을 사용하여 작업을 만듭니다.**  
  
    [SQL Server Management Studio](#SSMSProcedure),  
  
    [Transact-SQL](#TsqlProcedure)  
  
    [SQL Server 관리 개체](#SMOProcedure)  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>제한 사항  
  
-   작업을 만들려면 사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 고정 데이터베이스 역할이나 **sysadmin** 고정 서버 역할 중 하나의 멤버여야 합니다. 작업은 소유자나 **sysadmin** 역할의 멤버만 편집할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 고정 데이터베이스 역할에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
-   다른 로그인에 작업을 할당한다고 해서 새 소유자가 작업을 성공적으로 실행할 수 있는 충분한 권한을 가진다고 보장할 수 없습니다.  
  
-   로컬 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 로컬 작업을 캐시하므로 수정 내용이 있을 경우 이 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 작업을 다시 캐시하도록 암시적으로 강제 설정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sp_add_jobserver **가 호출될 때까지는** 에이전트가 작업을 캐시하지 않으므로 마지막에 **sp_add_jobserver** 를 호출하는 것이 효율적입니다.  
  
### <a name="security"></a><a name="Security"></a>보안  
  
-   작업 소유자를 변경하려면 시스템 관리자여야 합니다.  
  
-   보안을 위해 작업 소유자나 **sysadmin** 역할의 멤버만 작업 정의를 변경할 수 있습니다. **sysadmin** 고정 서버 역할의 멤버만 작업 소유권을 다른 사용자에게 할당할 수 있으며 작업 소유자가 아니어도 모든 작업을 실행할 수 있습니다.  
  
    > [!NOTE]  
    > **sysadmin** 고정 서버 역할의 멤버가 아닌 사용자로 작업 소유권을 변경하고 이 작업이 프록시 계정을 필요로 하는 작업 단계를 실행 중이면(예: [!INCLUDE[ssIS](../../includes/ssis_md.md)] 패키지 실행) 사용자가 해당 프록시 계정에 액세스할 수 있어야 작업이 실패하지 않습니다.  
  
#### <a name="permissions"></a><a name="Permissions"></a>권한  
자세한 내용은 [SQL Server 에이전트 보안 구현](../../ssms/agent/implement-sql-server-agent-security.md)을 참조하세요.  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>SQL Server Management Studio 사용  
  
#### <a name="to-create-a-sql-server-agent-job"></a>SQL Server 에이전트 작업을 만들려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 SQL Server 에이전트 작업을 만들려는 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **SQL Server 에이전트**를 확장합니다.  
  
3.  **작업** 폴더를 마우스 오른쪽 단추로 클릭하고 **새 작업...** 을 선택합니다.  
  
4.  **새 작업** 대화 상자의 **일반** 페이지에서 작업의 일반 속성을 수정합니다. 이 페이지에서 사용할 수 있는 옵션에 대한 자세한 내용은 [작업 속성 - 새 작업&#40;일반 페이지&#41;](../../ssms/agent/job-properties-new-job-general-page.md)을 참조하세요.  
  
5.  **단계** 페이지에서 작업 단계를 구성합니다. 이 페이지에서 사용할 수 있는 옵션에 대한 자세한 내용은 [작업 속성 - 새 작업&#40;단계 페이지&#41;](../../ssms/agent/job-properties-new-job-steps-page.md)을 참조하세요.  
  
6.  **일정** 페이지에서 작업 일정을 구성합니다. 이 페이지에서 사용할 수 있는 옵션에 대한 자세한 내용은 [작업 속성 - 새 작업&#40;일정 페이지&#41;](../../ssms/agent/job-properties-new-job-schedules-page.md)을 참조하세요.  
  
7.  **경고** 페이지에서 작업에 대한 경고를 구성합니다. 이 페이지에서 사용할 수 있는 옵션에 대한 자세한 내용은 [작업 속성 - 새 작업&#40;경고 페이지&#41;](../../ssms/agent/job-properties-new-job-alerts-page.md)을 참조하세요.  
  
8.  **알림** 페이지에서 작업이 완료될 때 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 수행할 동작을 설정합니다. 이 페이지에서 사용할 수 있는 옵션에 대한 자세한 내용은 [작업 속성 - 새 작업&#40;알림 페이지&#41;](../../ssms/agent/job-properties-new-job-notifications-page.md)을 참조하세요.  
  
9. **대상** 페이지에서 작업의 대상 서버를 관리합니다. 이 페이지에서 사용할 수 있는 옵션에 대한 자세한 내용은 [작업 속성 - 새 작업&#40;대상 페이지&#41;](../../ssms/agent/job-properties-new-job-targets-page.md)을 참조하세요.  
  
10. 완료되었으면 **확인**을 클릭합니다.  
  
## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a>Transact-SQL 사용  
  
#### <a name="to-create-a-sql-server-agent-job"></a>SQL Server 에이전트 작업을 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde_md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE msdb ;  
    GO  
    EXEC dbo.sp_add_job  
        @job_name = N'Weekly Sales Data Backup' ;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Set database to read only',  
        @subsystem = N'TSQL',  
        @command = N'ALTER DATABASE SALES SET READ_ONLY',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    EXEC dbo.sp_add_schedule  
        @schedule_name = N'RunOnce',  
        @freq_type = 1,  
        @active_start_time = 233000 ;  
    USE msdb ;  
    GO  
    EXEC sp_attach_schedule  
       @job_name = N'Weekly Sales Data Backup',  
       @schedule_name = N'RunOnce';  
    GO  
    EXEC dbo.sp_add_jobserver  
        @job_name = N'Weekly Sales Data Backup';  
    GO  
    ```  
  
자세한 내용은 다음을 참조하세요.  
  
-   [sp_add_job(Transact-SQL)](https://msdn.microsoft.com/6ca8fe2c-7b1c-4b59-b4c7-e3b7485df274)  
  
-   [sp_add_jobstep(Transact-SQL)](https://msdn.microsoft.com/97900032-523d-49d6-9865-2734fba1c755)  
  
-   [sp_add_schedule(Transact-SQL)](https://msdn.microsoft.com/9060aae3-3ddd-40a5-83bb-3ea7ab1ffbd7)  
  
-   [sp_attach_schedule(Transact-SQL)](https://msdn.microsoft.com/80c80eaf-cf23-4ed8-b8dd-65fe59830dd1)  
  
-   [sp_add_jobserver(Transact-SQL)](https://msdn.microsoft.com/485252cc-0081-490a-9bd1-cbbd68eea286)  
  
## <a name="using-sql-server-management-objects"></a><a name="SMOProcedure"></a>SQL Server 관리 개체 사용  
**SQL Server 에이전트 작업을 만들려면**  
  
Visual Basic, Visual C#, PowerShell 등 선택한 프로그래밍 언어를 사용하여 **Job** 클래스의 **Create** 메서드를 호출합니다. 예제 코드를 보려면 [SQL Server 에이전트에서 자동 관리 태스크 예약](../../relational-databases/server-management-objects-smo/tasks/scheduling-automatic-administrative-tasks-in-sql-server-agent.md)을 참조하세요.  
  
