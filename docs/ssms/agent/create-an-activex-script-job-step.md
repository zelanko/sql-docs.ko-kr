---
title: ActiveX 스크립트 작업 단계 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- ActiveX scripting jobs [SQL Server]
- job steps [Analysis Services]
ms.assetid: e6c46c6b-2d61-4571-bc8e-a831cd6e6302
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a6ac4c4174b814577340b2d571c2f9b76944482a
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51696991"
---
# <a name="create-an-activex-script-job-step"></a>Create an ActiveX Script Job Step
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database Managed Instance T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 SQL Server 관리 개체를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 ActiveX 스크립트를 실행하는 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 단계를 만들고 정의하는 방법에 대해 설명합니다.  
  
-   **시작하기 전 주의 사항:**  
  
    [제한 사항](#Restrictions)  
  
    [보안](#Security)  
  
-   **Transact-SQL 작업 단계를 만들려면:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server 관리 개체](#SMO)  
  
## <a name="before-you-begin"></a>시작하기 전 주의 사항  
  
### <a name="Restrictions"></a>제한 사항  
[!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
### <a name="Security"></a>보안  
자세한 내용은 [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)을 참조하세요.  
  
## <a name="SSMS"></a>SQL Server Management Studio 사용  
  
#### <a name="to-create-an-activex-script-job-step"></a>ActiveX 스크립트 작업 단계를 만들려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **SQL Server 에이전트**를 확장하고 새 작업을 만들거나 기존 작업을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다. 작업을 만드는 방법은 [작업 만들기](../../ssms/agent/create-jobs.md)를 참조하세요.  
  
3.  **작업 속성** 대화 상자에서 **단계** 페이지를 클릭한 다음 **새로 만들기**를 클릭합니다.  
  
4.  **새 작업 단계** 대화 상자에서 작업 **단계 이름**을 입력합니다.  
  
5.  **유형** 목록에서 **ActiveX 스크립트**를 클릭합니다.  
  
6.  **다음 계정으로 실행** 목록에서 작업에 사용할 자격 증명을 가진 프록시 계정을 선택합니다.  
  
7.  스크립트 작성에 사용한 **언어** 를 선택합니다. 또는 **기타** 를 클릭한 다음 스크립트 작성에 사용할 [!INCLUDE[msCoName](../../includes/msconame_md.md)] ActiveX 스크립트 언어의 이름을 입력합니다.  
  
8.  **명령** 입력란에 작업 단계를 위해 실행될 스크립트 구문을 입력합니다. 아니면 **열기** 를 클릭한 다음 해당 스크립트 구문이 포함된 파일을 선택합니다.  
  
9. **고급** 페이지를 클릭하여 작업 단계가 성공 또는 실패할 경우에 수행할 동작, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트의 작업 단계 실행 시도 횟수, 그리고 다시 시도 간격 등 작업 단계 옵션을 설정합니다.  
  
## <a name="TSQL"></a>Transact-SQL 사용  
  
#### <a name="to-create-an-activex-script-job-step"></a>ActiveX 스크립트 작업 단계를 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde_md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- create an ActiveX Script job step written in VBScript that creates a restore point  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Create a restore point',  
        @subsystem = N'ACTIVESCRIPTING',  
        @command = N'Const RESTORE_POINT = 20  
  
    strComputer = "."  
    Set objWMIService = GetObject("winmgmts:" _  
        & "{impersonationLevel=impersonate}!\\" & strComputer & "\root\default")  
  
    Set objItem = objWMIService.Get("SystemRestore")  
    errResults = objItem.Restore(RESTORE_POINT)',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    ```  
  
자세한 내용은 [sp_add_jobstep(Transact-SQL)](https://msdn.microsoft.com/97900032-523d-49d6-9865-2734fba1c755)을 참조하세요.  
  
## <a name="SMO"></a>SQL Server 관리 개체 사용  
**ActiveX 스크립트 작업 단계를 만들려면**  
  
Visual Basic, Visual C#, PowerShell 등 선택한 프로그래밍 언어를 사용하여 **JobStep** 클래스를 사용합니다.  
  
