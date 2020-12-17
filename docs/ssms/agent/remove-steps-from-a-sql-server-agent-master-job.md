---
description: Remove Steps from a SQL Server Agent Master Job
title: Remove Steps from a SQL Server Agent Master Job
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 871e6162-1221-464d-8f7f-7e454dcd9edb
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: bc6817d379fe9fcb5c6cfc32ae40e6e52192f613
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97476984"
---
# <a name="remove-steps-from-a-sql-server-agent-master-job"></a>Remove Steps from a SQL Server Agent Master Job
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance)에서는 SQL Server 에이전트 기능이 대부분 지원됩니다. 자세한 내용은 [SQL Server와 Azure SQL Managed Instance 간의 T-SQL 차이점](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 SQL Server 에이전트 마스터 작업의 단계를 제거하는 방법에 대해 설명합니다.  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>제한 사항  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 마스터 작업은 로컬 및 원격 서버 모두에서 대상이 될 수 없습니다.  
  
### <a name="security"></a><a name="Security"></a>보안  
  
#### <a name="permissions"></a><a name="Permissions"></a>권한  
**sysadmin** 고정 서버 역할의 멤버가 아닌 경우 자신이 소유한 작업만 수정할 수 있습니다. 자세한 내용은 [SQL Server 에이전트 보안 구현](../../ssms/agent/implement-sql-server-agent-security.md)을 참조하세요.  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>SQL Server Management Studio 사용  
  
#### <a name="to-remove-steps-from-a-sql-server-agent-master-job"></a>SQL Server 에이전트 마스터 작업의 단계를 제거하려면  
  
1.  **개체 탐색기** 에서 더하기 기호를 클릭하여 단계를 삭제하려는 작업이 들어 있는 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **SQL Server 에이전트** 를 확장합니다.  
  
3.  더하기 기호를 클릭하여 **작업** 폴더를 확장합니다.  
  
4.  단계를 삭제하려는 작업을 마우스 오른쪽 단추로 클릭하고 **속성** 을 선택합니다.  
  
5.  **Job Properties -** _job_name_ 대화 상자의 **페이지 선택** 에서 **단계** 를 선택합니다.  

6.  **작업 단계 목록** 에서 삭제하려는 작업 단계를 선택하고 **삭제** 를 클릭합니다.  
  
7.  완료되었으면 **확인** 을 클릭합니다.  
  
## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a>Transact-SQL 사용  
  
#### <a name="to-remove-steps-from-a-sql-server-agent-master-job"></a>SQL Server 에이전트 마스터 작업의 단계를 제거하려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDE](../../includes/ssde_md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다.  
  
    ```  
    -- removes job step 1 from the job Weekly Sales Data Backup   
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_delete_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_id = 1 ;  
    GO  
    ```  
  
자세한 내용은 [sp_delete_jobstep(Transact-SQL)](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)을 참조하세요.  
