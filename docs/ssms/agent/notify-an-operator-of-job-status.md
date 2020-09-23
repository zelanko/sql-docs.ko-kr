---
description: Notify an Operator of Job Status
title: Notify an Operator of Job Status
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- status information [SQL Server], jobs
- jobs [SQL Server Agent], notification options
- SQL Server Agent jobs, status
- jobs [SQL Server Agent], status
- SQL Server Agent jobs, notification options
- notifications [SQL Server], job status
ms.assetid: e7399505-27ac-48d9-a637-73bf92b9df49
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 520495002a15790451321f486a069154e6469199
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418109"
---
# <a name="notify-an-operator-of-job-status"></a>Notify an Operator of Job Status
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서는 SQL Server 에이전트 기능이 대부분 지원됩니다. 자세한 내용은 [SQL Server와 Azure SQL Managed Instance 간의 T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 문서에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 SQL Server 관리 개체로 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 알림 옵션을 설정하여 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 작업에 대한 알림을 운영자에게 전송할 수 있도록 하는 방법에 대해 설명합니다.  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="security"></a><a name="Security"></a>보안  
자세한 내용은 [SQL Server 에이전트 보안 구현](../../ssms/agent/implement-sql-server-agent-security.md)을 참조하세요.  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMS"></a>SQL Server Management Studio 사용  
  
#### <a name="to-notify-an-operator-of-job-status"></a>운영자에게 작업 상태를 알리려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **SQL Server 에이전트**, **작업**을 차례로 확장한 다음 편집할 작업을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
3.  **작업 속성** 대화 상자에서 **알림** 페이지를 선택합니다.  
  
4.  전자 메일을 통해 운영자에게 알리려면 **전자 메일**확인란을 선택하고 목록에서 운영자를 선택한 후 다음 중 하나를 선택합니다.  
  
    -   **작업 성공 시** - 작업이 성공적으로 완료되면 운영자에게 알립니다.  
  
    -   **작업 실패 시** - 작업이 성공적으로 완료되지 않았을 때 운영자에게 알립니다.  
  
    -   **작업 완료 시** - 완료 상태에 관계없이 운영자에게 알립니다.  
  
5.  무선 호출기를 통해 운영자에게 알리려면 **호출**확인란을 선택하고 목록에서 운영자를 선택한 후 다음 중 하나를 선택합니다.  
  
    -   **작업 성공 시** - 작업이 성공적으로 완료되면 운영자에게 알립니다.  
  
    -   **작업 실패 시** - 작업이 성공적으로 완료되지 않았을 때 운영자에게 알립니다.  
  
    -   **작업 완료 시** - 완료 상태에 관계없이 운영자에게 알립니다.  
  
6.  Net Send로 운영자에게 알리려면 **Net Send**확인란을 선택하고 목록에서 운영자를 선택한 후 다음 중 하나를 선택합니다.  
  
    -   **작업 성공 시** - 작업이 성공적으로 완료되면 운영자에게 알립니다.  
  
    -   **작업 실패 시** - 작업이 성공적으로 완료되지 않았을 때 운영자에게 알립니다.  
  
    -   **작업 완료 시** - 완료 상태에 관계없이 운영자에게 알립니다.  
  
## <a name="using-transact-sql"></a><a name="TSQL"></a>Transact-SQL 사용  
  
#### <a name="to-notify-an-operator-of-job-status"></a>운영자에게 작업 상태를 알리려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde_md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- adds an e-mail notification for the specified alert (Test Alert).  
    -- This example assumes that Test Alert already exists
    --  and that François Ajenstat is a valid operator name.  
    USE msdb ;  
    GO  
    EXEC dbo.sp_add_notification   
    @alert_name = N'Test Alert',   
    @operator_name = N'François Ajenstat',   
    @notification_method = 1 ;  
    GO  
    ```  
  
자세한 내용은 [sp_add_notification(Transact-SQL)](https://msdn.microsoft.com/0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd)을 참조하세요.  
  
## <a name="using-sql-server-management-objects"></a><a name="SMO"></a>SQL Server 관리 개체 사용  
**운영자에게 작업 상태를 알리려면**  
  
Visual Basic, Visual C#, PowerShell 등 선택한 프로그래밍 언어를 사용하여 **Job** 클래스를 사용합니다. 자세한 내용은 [SMO(SQL Server 관리 개체)](https://msdn.microsoft.com/library/ms162169.aspx)를 참조하세요.  
  
