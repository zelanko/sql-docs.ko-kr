---
title: PowerShell 스크립트 작업 단계 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 01/20/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- PowerShell [SQL Server], job steps
- jobs [SQL Server Agent], PowerShell
- job steps [PowerShell]
- SQL Server Agent jobs, PowerShell steps
ms.assetid: 50afcf84-fae0-4eb5-9b0f-f2cf144c1433
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f281e32dc982e3e7295665adce81740dfff64e24
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264831"
---
# <a name="create-a-powershell-script-job-step"></a>Create a PowerShell Script Job Step
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database Managed Instance T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 을 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 PowerShell 스크립트를 실행하는 [!INCLUDE[tsql](../../includes/tsql-md.md)]에이전트 작업 단계를 만들고 정의하는 방법에 대해 설명합니다.  
  
**항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
    [보안](#Security)  
  
-   **PowerShell 스크립트 작업 단계를 만들려면**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server 관리 개체](#SMO)  

## <a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="Security"></a>보안  
자세한 내용은 [SQL Server 에이전트 보안 구현](../../ssms/agent/implement-sql-server-agent-security.md)을 참조하세요.  

[!INCLUDE[Freshness](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="SSMS"></a>SQL Server Management Studio 사용  
  
#### <a name="to-create-a-powershell-script-job-step"></a>PowerShell 스크립트 작업 단계를 만들려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **SQL Server 에이전트**를 확장하고 새 작업을 만들거나 기존 작업을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다. 작업을 만드는 방법은 [작업 만들기](../../ssms/agent/create-jobs.md)를 참조하세요.  
  
3.  **작업 속성** 대화 상자에서 **단계** 페이지를 클릭한 다음 **새로 만들기**를 클릭합니다.  
  
4.  **새 작업 단계** 대화 상자에서 작업 **단계 이름**을 입력합니다.  
  
5.  **형식** 목록에서 **PowerShell**을 클릭합니다.  
  
6.  **다음 계정으로 실행** 목록에서 작업에 사용할 자격 증명을 가진 프록시 계정을 선택합니다.  
  
7.  **명령** 입력란에 작업 단계를 위해 실행될 PowerShell 스크립트 구문을 입력합니다. 아니면 **열기** 를 클릭한 다음 해당 스크립트 구문이 포함된 파일을 선택합니다. PowerShell 스크립트 예는 아래의 **Transact-SQL 사용** 을 참조하세요.  
  
8.  **고급** 페이지를 클릭하여 작업 단계가 성공 또는 실패할 경우에 수행할 동작, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트의 작업 단계 실행 시도 횟수, 그리고 다시 시도 간격 등 작업 단계 옵션을 설정합니다.  
  
## <a name="TSQL"></a>Transact-SQL 사용  
  
#### <a name="to-create-a-powershell-script-job-step"></a>PowerShell 스크립트 작업 단계를 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde_md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- creates a PowerShell job step that finds the processes
    -- that use more than 1000 MB of memory and kills them  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Kills all processes that use more than 1000 MB of memory',  
        @subsystem = N'PowerShell',  
        @command = N'Get-Process | Where-Object { $_.WS -gt 1000MB } | Stop-Process',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    ```  
  
자세한 내용은 [sp_add_jobstep(Transact-SQL)](https://msdn.microsoft.com/97900032-523d-49d6-9865-2734fba1c755)을 참조하세요.  
  
## <a name="SMO"></a>SQL Server 관리 개체 사용  
**PowerShell 스크립트 작업 단계를 만들려면**  
  
Visual Basic, Visual C#, PowerShell 등 선택한 프로그래밍 언어를 사용하여 **JobStep** 클래스를 사용합니다.  
  
