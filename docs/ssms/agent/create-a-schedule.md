---
description: Create a Schedule
title: Create a Schedule
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- scheduling jobs [SQL Server]
- SQL Server Agent jobs, scheduling
- jobs [SQL Server Agent], scheduling
- schedules [SQL Server], jobs
ms.assetid: 8c7ef3b3-c06d-4a27-802d-ed329dc86ef3
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: b3a3de7f3d87cfdcda48fce509799c2107e05f05
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97474484"
---
# <a name="create-a-schedule"></a>Create a Schedule
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance)에서는 SQL Server 에이전트 기능이 대부분 지원됩니다. 자세한 내용은 [SQL Server와 Azure SQL Managed Instance 간의 T-SQL 차이점](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 SQL Server 관리 개체를 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[tsql](../../includes/tsql-md.md)]에이전트 작업에 대한 일정을 만들 수 있습니다.  
  
-   **시작하기 전 주의 사항:**  
  
    [보안](#Security)  
  
-   **일정을 만들려면:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server 관리 개체](#SMO)  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="security"></a><a name="Security"></a>보안  
자세한 내용은 [SQL Server 에이전트 보안 구현](../../ssms/agent/implement-sql-server-agent-security.md)을 참조하세요.  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMS"></a>SQL Server Management Studio 사용  
  
#### <a name="to-create-a-schedule"></a>일정을 만들려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **SQL Server 에이전트** 를 확장하고 **작업** 을 마우스 오른쪽 단추로 클릭한 후 **일정 관리** 를 클릭합니다.  
  
3.  **일정 관리** 대화 상자에서 **새로 만들기** 를 클릭합니다.  
  
4.  **이름** 입력란에 새 일정의 이름을 입력합니다.  
  
5.  만든 즉시 일정이 적용되지 않게 하려면 **사용** 확인란의 선택을 해제합니다.  
  
6.  **일정 유형** 에 대해 다음 중 하나를 선택합니다.  
  
    -   CPU가 유휴 상태일 때 작업을 시작하려면 **CPU가 유휴 상태로 될 때마다 시작** 을 클릭합니다.  
  
    -   일정을 반복적으로 실행하려면 **되풀이** 를 클릭합니다. 반복 수행 일정을 설정하려면 대화 상자에서 **빈도**, **일별 빈도** 및 **기간** 그룹을 입력하세요.  
  
    -   한 번만 실행하도록 예약하려면 **한 번** 을 클릭합니다. **한 번** 예약을 설정하려면 대화 상자에서 **한 번 발생** 그룹을 입력합니다.  
  
## <a name="using-transact-sql"></a><a name="TSQL"></a>Transact-SQL 사용  
  
#### <a name="to-create-a-schedule"></a>일정을 만들려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDE](../../includes/ssde_md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다.  
  
    ```  
    -- creates a schedule named RunOnce.   
    -- The schedule runs one time, at 23:30 on the day that the schedule is created.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_schedule  
        @schedule_name = N'RunOnce',  
        @freq_type = 1,  
        @active_start_time = 233000 ;  
  
    GO  
    ```  
  
자세한 내용은 [sp_add_schedule(Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)을 참조하세요.  
  
## <a name="using-sql-server-management-objects"></a><a name="SMO"></a>SQL Server 관리 개체 사용  
**일정을 만들려면**  
  
Visual Basic, Visual C#, PowerShell 등 선택한 프로그래밍 언어를 사용하여 **JobSchedule** 클래스를 사용합니다. 자세한 내용은 [SMO(SQL Server 관리 개체)](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)를 참조하세요.  
