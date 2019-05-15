---
title: 작업 단계 성공 또는 실패 흐름 설정 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, action flow logic
- successful jobs [SQL Server]
- failed jobs [SQL Server]
- jobs [SQL Server Agent], action flow logic
ms.assetid: 23041ccf-8a07-41d3-85b9-c449a54b7e1e
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c14f10c9bba7dbdd40c1e2554fb590cd6f814043
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65105988"
---
# <a name="set-job-step-success-or-failure-flow"></a>Set Job Step Success or Failure Flow
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database Managed Instance T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 만들 때 작업 실행 중에 오류가 발생할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 수행해야 할 동작을 지정할 수 있습니다. 각 작업 단계의 성공이나 실패에 따라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 수행해야 할 동작을 결정합니다. 그런 후에 다음 프로시저를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 통해 작업 단계 동작 흐름 논리를 구성합니다.  
  
-   **시작하기 전 주의 사항:**  
  
    [보안](#Security)  
  
-   **작업 단계 성공 또는 실패 흐름을 설정하려면:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server 관리 개체](#SMO)  
  
## <a name="before-you-begin"></a>시작하기 전 주의 사항  
  
### <a name="Security"></a>보안  
자세한 내용은 [SQL Server 에이전트 보안 구현](../../ssms/agent/implement-sql-server-agent-security.md)을 참조하세요.  
  
## <a name="SSMS"></a>SQL Server Management Studio 사용  
  
#### <a name="to-set-job-step-success-or-failure-flow"></a>작업 단계 성공 또는 실패 흐름을 설정하려면  
  
1.  **개체 탐색기**에서 **SQL Server 에이전트**, **작업**을 차례로 확장합니다.  
  
2.  편집할 작업을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **단계** 페이지를 선택하고 단계를 클릭한 다음 **편집**을 클릭합니다.  
  
4.  **작업 단계 속성** 대화 상자에서 **고급** 페이지를 선택합니다.  
  
5.  실패한 것으로 간주될 때까지 작업 단계를 반복할 횟수를 0부터 9999 범위에서 **성공한 경우 동작**목록에서 작업 단계가 성공적으로 완료된 경우 수행할 동작을 클릭합니다.  
  
6.  실패한 것으로 간주될 때까지 작업 단계를 반복할 횟수를 0부터 9999 범위에서 **다시 시도 횟수** 상자에 입력합니다. **다시 시도 횟수** 상자에 0보다 큰 값을 입력한 경우 작업 단계를 다시 시도하기 전에 경과해야 하는 시간(분)을 1부터 9999 범위에서 **다시 시도 간격(분)** 상자에 입력합니다.  
  
7.  **실패한 경우 동작** 목록에서 작업 단계가 실패한 경우 수행할 동작을 클릭합니다.  
  
8.  작업이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트인 경우 다음 옵션을 선택할 수 있습니다.  
  
    -   **출력 파일** 상자에 스크립트 출력을 작성할 출력 파일 이름을 입력합니다. 기본적으로 작업 단계가 실행될 때마다 파일을 덮어씁니다. 출력 파일을 덮어쓰지 않으려면 **기존 파일에 출력 추가**를 선택합니다.  
  
    -   작업 단계를 데이터베이스 테이블에 기록하려면 **테이블에 기록** 을 선택합니다. 기본적으로 작업 단계가 실행될 때마다 테이블 내용을 덮어씁니다. 테이블 내용을 덮어쓰지 않으려면 **테이블의 기존 항목에 출력 추가**를 선택합니다. 작업 단계가 실행된 다음에는 **뷰**를 클릭하여 이 테이블의 내용을 볼 수 있습니다.  
  
    -   출력을 단계 기록에 포함하려면 **기록에 단계 출력 포함** 을 선택합니다. 출력은 오류가 없을 때만 표시됩니다. 또한 출력이 잘릴 수도 있습니다.  
  
9. **다음 사용자 이름으로 실행** 목록을 사용할 수 있으면 작업에서 사용할 자격 증명이 있는 프록시 계정을 선택합니다.  
  
## <a name="TSQL"></a>Transact-SQL 사용  
  
#### <a name="to-set-job-step-success-or-failure-flow"></a>작업 단계 성공 또는 실패 흐름을 설정하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde_md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Set database to read only',  
        @subsystem = N'TSQL',  
        @command = N'ALTER DATABASE SALES SET READ_ONLY',   
        @on_success_action = 1;  
    GO  
    ```  
  
자세한 내용은 [sp_add_jobstep(Transact-SQL)](https://msdn.microsoft.com/97900032-523d-49d6-9865-2734fba1c755)을 참조하세요.  
  
## <a name="SMO"></a>SQL Server 관리 개체 사용  
**작업 단계 성공 또는 실패 흐름을 설정하려면**  
  
Visual Basic, Visual C#, PowerShell 등 선택한 프로그래밍 언어를 사용하여 **JobStep** 클래스를 사용합니다. 자세한 내용은 [SMO(SQL Server 관리 개체)](https://msdn.microsoft.com/library/ms162169.aspx)를 참조하세요.  
  
