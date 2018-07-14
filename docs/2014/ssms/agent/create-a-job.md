---
title: 작업 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], creating
- SQL Server Agent jobs, creating
ms.assetid: b35af2b6-6594-40d1-9861-4d5dd906048c
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d161129b14da33645c1a9238307c0eefe9539097
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37181540"
---
# <a name="create-a-job"></a>작업 만들기
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 SMO(SQL Server 관리 개체)를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 SQL Server 에이전트 작업을 만드는 방법에 대해 설명합니다.  
  
 운영자에게 전송할 수 있는 작업 단계, 일정, 경고 및 알림을 추가하려면 참조 섹션에 있는 항목에 대한 링크를 참조하세요.  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 작업을 만듭니다.**  
  
     [SQL Server Management Studio](#SSMSProcedure),  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [SQL Server 관리 개체](#SMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   작업을 만들려면 사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 고정 데이터베이스 역할이나 **sysadmin** 고정 서버 역할 중 하나의 멤버여야 합니다. 작업은 소유자나 **sysadmin** 역할의 멤버만 편집할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 고정 데이터베이스 역할에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
-   다른 로그인에 작업을 할당한다고 해서 새 소유자가 작업을 성공적으로 실행할 수 있는 충분한 권한을 가진다고 보장할 수 없습니다.  
  
-   로컬 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 로컬 작업을 캐시하므로 수정 내용이 있을 경우 이 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 작업을 다시 캐시하도록 암시적으로 강제 설정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sp_add_jobserver **가 호출될 때까지는** 에이전트가 작업을 캐시하지 않으므로 마지막에 **sp_add_jobserver** 를 호출하는 것이 효율적입니다.  
  
###  <a name="Security"></a> 보안  
  
-   작업 소유자를 변경하려면 시스템 관리자여야 합니다.  
  
-   보안을 위해 작업 소유자나 **sysadmin** 역할의 멤버만 작업 정의를 변경할 수 있습니다. **sysadmin** 고정 서버 역할의 멤버만 작업 소유권을 다른 사용자에게 할당할 수 있으며 작업 소유자가 아니어도 모든 작업을 실행할 수 있습니다.  
  
    > [!NOTE]  
    >  **sysadmin** 고정 서버 역할의 멤버가 아닌 사용자로 작업 소유권을 변경하고 이 작업이 프록시 계정을 필요로 하는 작업 단계를 실행 중이면(예: [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 실행) 사용자가 해당 프록시 계정에 액세스할 수 있어야 작업이 실패하지 않습니다.  
  
####  <a name="Permissions"></a> Permissions  
 자세한 내용은 [Implement SQL Server Agent Security](implement-sql-server-agent-security.md)을 참조하세요.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-create-a-sql-server-agent-job"></a>SQL Server 에이전트 작업을 만들려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 SQL Server 에이전트 작업을 만들려는 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **SQL Server 에이전트**를 확장합니다.  
  
3.  **작업** 폴더를 마우스 오른쪽 단추로 클릭하고 **새 작업...** 을 선택합니다.  
  
4.  **새 작업** 대화 상자의 **일반** 페이지에서 작업의 일반 속성을 수정합니다. 이 페이지에서 사용 가능한 옵션에 대 한 자세한 내용은 참조 하세요. [작업 속성 및 새 작업 &#40;일반 페이지&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
5.  **단계** 페이지에서 작업 단계를 구성합니다. 이 페이지에서 사용 가능한 옵션에 대 한 자세한 내용은 참조 하세요. [작업 속성: 새 작업 &#40;단계 페이지&#41;](job-properties-new-job-steps-page.md)  
  
6.  **일정** 페이지에서 작업 일정을 구성합니다. 이 페이지에서 사용 가능한 옵션에 대 한 자세한 내용은 참조 하세요. [작업 속성: 새 작업 &#40;일정 페이지&#41;](job-properties-new-job-schedules-page.md)  
  
7.  **경고** 페이지에서 작업에 대한 경고를 구성합니다. 이 페이지에서 사용 가능한 옵션에 대 한 자세한 내용은 참조 하세요. [작업 속성: 새 작업 &#40;경고 페이지&#41;](job-properties-new-job-alerts-page.md)  
  
8.  **알림** 페이지에서 작업이 완료되었을 때 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 수행할 동작을 설정합니다. 이 페이지에서 사용 가능한 옵션에 대 한 자세한 내용은 참조 하세요. [작업 속성: 새 작업 &#40;알림 페이지&#41;](job-properties-new-job-notifications-page.md)합니다.  
  
9. **대상** 페이지에서 작업의 대상 서버를 관리합니다. 이 페이지에서 사용 가능한 옵션에 대 한 자세한 내용은 참조 하세요. [작업 속성: 새 작업 &#40;대상 페이지&#41;](job-properties-new-job-targets-page.md)합니다.  
  
10. 완료되었으면 **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-create-a-sql-server-agent-job"></a>SQL Server 에이전트 작업을 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
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
  
 참조 항목:  
  
-   [sp_add_job&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-job-transact-sql)  
  
-   [sp_add_jobstep&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql)  
  
-   [sp_add_schedule&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-schedule-transact-sql)  
  
-   [sp_attach_schedule&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql)  
  
-   [sp_add_jobserver &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql)  
  
##  <a name="SMOProcedure"></a> SQL Server 관리 개체를 사용 하 여  
 **SQL Server 에이전트 작업을 만들려면**  
  
 Visual Basic, Visual C#, PowerShell 등 선택한 프로그래밍 언어를 사용하여 `Create` 클래스의 `Job` 메서드를 호출합니다. 예제 코드를 보려면 [SQL Server 에이전트에서 자동 관리 태스크 예약](sql-server-agent.md)을 참조하세요.  
  
##  <a name="SSMSProc2"></a>  
