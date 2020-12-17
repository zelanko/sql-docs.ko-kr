---
description: Disable or Enable a Job
title: Disable or Enable a Job
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- stopping jobs
- disabling jobs
- SQL Server Agent jobs, disabling
- jobs [SQL Server Agent], disabling
ms.assetid: 5041261f-0c32-4d4a-8bee-59a6c16200dd
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: f0e345b59e3bd625e65dcc9d4c28d063735c9c03
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97423867"
---
# <a name="disable-or-enable-a-job"></a>Disable or Enable a Job
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Managed Instance](/azure/azure-sql/managed-instance/sql-managed-instance-paas-overview)에서는 SQL Server 에이전트 기능이 대부분 지원됩니다. 자세한 내용은 [Azure SQL Managed Instance와 SQL Server 간의 차이점](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 을 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 [!INCLUDE[tsql](../../includes/tsql-md.md)]에이전트 작업을 비활성화하는 방법에 대해 설명합니다. 작업을 사용하지 않도록 설정하더라도 해당 작업은 삭제되지 않으며 필요할 때 사용하도록 설정할 수 있습니다.  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="security"></a><a name="Security"></a>보안  
자세한 내용은 [SQL Server 에이전트 보안 구현](../../ssms/agent/implement-sql-server-agent-security.md)을 참조하세요.  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMS"></a>SQL Server Management Studio 사용  
  
#### <a name="to-disable-or-enable-a-job"></a>작업을 사용하지 않거나 사용하도록 설정하려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **SQL Server 에이전트** 를 확장합니다.  
  
3.  **작업** 을 확장한 다음 사용하지 않거나 사용하도록 설정할 작업을 마우스 오른쪽 단추로 클릭합니다.  
  
4.  작업을 사용하지 않도록 설정하려면 **사용 안 함** 을 클릭합니다. 작업을 사용하도록 설정하려면 **사용** 을 클릭합니다.  
  
## <a name="using-transact-sql"></a><a name="TSQL"></a>Transact-SQL 사용  
  
#### <a name="to-disable-or-enable-a-job"></a>작업을 사용하지 않거나 사용하도록 설정하려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDE](../../includes/ssde_md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다.  
  
    ```  
    -- changes the name, description, and disables status of the job NightlyBackups.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_update_job  
        @job_name = N'NightlyBackups',  
        @new_name = N'NightlyBackups -- Disabled',  
        @description = N'Nightly backups disabled during server migration.',  
        @enabled = 0 ;  
    GO  
    ```  
  
자세한 내용은 [sp_update_job(Transact-SQL)](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)을 참조하세요.  
