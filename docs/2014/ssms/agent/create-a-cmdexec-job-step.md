---
title: CmdExec 작업 단계 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- CmdExec jobs
ms.assetid: b48da5b4-6fe7-4eb7-bade-dc7d697c6d5c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7ba283ef2ff426521c881f733bc29465eebc0c76
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798160"
---
# <a name="create-a-cmdexec-job-step"></a>CmdExec 작업 단계 만들기
  이 항목에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Server 관리 개체를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 실행 프로그램이나 운영 체제 명령을 사용하는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] 에이전트 작업 단계를 만들고 정의하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [보안](#Security)  
  
-   **CmdExec 작업 단계를 만들려면:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server 관리 개체](#SMO)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버만 CmdExec 작업 단계를 만들 수 있습니다. **sysadmin** 사용자가 프록시 계정을 만들지 않으면 이 작업 단계들은 SQL Server 에이전트 서비스 계정의 컨텍스트로 실행됩니다. **sysadmin** 역할의 멤버가 아니더라도 CmdExec 프록시 계정에 액세스할 수 있는 사용자는 CmdExec 작업 단계를 만들 수 있습니다.  
  
####  <a name="Permissions"></a> Permissions  
 자세한 내용은 [SQL Server 에이전트 보안 구현](implement-sql-server-agent-security.md)을 참조하세요.  
  
##  <a name="SSMS"></a> SQL Server Management Studio 사용  
  
#### <a name="to-create-a-cmdexec-job-step"></a>CmdExec 작업 단계를 만들려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **SQL Server 에이전트**를 확장하고 새 작업을 만들거나 기존 작업을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **작업 속성** 대화 상자에서 **단계** 페이지를 클릭한 다음 **새로 만들기**를 클릭합니다.  
  
4.  **새 작업 단계** 대화 상자에서 작업 **단계 이름**을 입력합니다.  
  
5.  **유형** 목록에서 **운영 체제(CmdExec)** 를 선택합니다.  
  
6.  **다음 계정으로 실행** 목록에서 해당 작업이 사용할 자격 증명을 가진 프록시 계정을 선택합니다. 기본적으로 CmdExec 작업 단계는 SQL Server 에이전트 서비스 계정의 컨텍스트에서 실행됩니다.  
  
7.  **성공한 명령의 프로세스 종료 코드** 상자에 0에서 999999까지의 값을 입력합니다.  
  
8.  **명령** 입력란에 운영 체제 명령이나 실행 프로그램을 입력합니다. 예를 보려면 "Transact T-SQL 사용"을 참조하세요.  
  
9. **고급** 페이지를 클릭하여 작업 단계의 성공 또는 실패 여부에 따라 수행할 동작, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 작업 단계를 수행할 횟수, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 작업 단계 출력을 쓸 파일 등의 작업 단계 옵션을 설정합니다. **sysadmin** 고정 서버 역할의 멤버만 운영 체제 파일에 작업 단계 출력을 쓸 수 있습니다.  
  
##  <a name="TSQL"></a> Transact-SQL 사용  
  
### <a name="to-create-a-cmdexec-job-step"></a>CmdExec 작업 단계를 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```sql
    -- creates a job step that uses CmdExec  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Set database to read only',  
        @subsystem = N'CMDEXEC',  
        @command = C:\clickme_scripts\SQL11\PostBOLReorg GetHsX.exe',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    ```  
  
 자세한 내용은 [sp_add_jobstep &#40;transact-sql&#41; ](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql) 을 참조 하세요.  
  
##  <a name="SMO"></a>SQL Server 관리 개체 사용  

### <a name="to-create-a-cmdexec-job-step"></a>CmdExec 작업 단계를 만들려면
  
 Visual Basic, Visual C#, PowerShell 등 선택한 프로그래밍 언어를 사용하여 `JobStep` 클래스를 사용합니다.  
