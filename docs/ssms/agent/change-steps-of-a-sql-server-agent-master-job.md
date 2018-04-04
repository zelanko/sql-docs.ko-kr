---
title: SQL Server 에이전트 마스터 작업의 단계 변경 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8f1a0ee6-49ff-4080-94ca-d661daeff2a6
caps.latest.revision: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8e6604550fd8d34e6a1beeff7734eb67344d1e5c
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="change-steps-of-a-sql-server-agent-master-job"></a>Change Steps of a SQL Server Agent Master Job
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database 관리되는 인스턴스](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database 관리되는 인스턴스 T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql_md.md)]에서 SQL Server 에이전트 마스터 작업의 단계를 변경하는 방법에 대해 설명합니다.  
  
**항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
    [제한 사항](#Restrictions)  
  
    [보안](#Security)  
  
-   **다음을 사용하여 SQL Server 에이전트 마스터 작업의 단계를 변경하려면:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="Restrictions"></a>제한 사항  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 마스터 작업은 로컬 및 원격 서버 모두에서 대상이 될 수 없습니다.  
  
### <a name="Security"></a>보안  
  
#### <a name="Permissions"></a>Permissions  
**sysadmin** 고정 서버 역할의 멤버가 아닌 경우 자신이 소유한 작업만 수정할 수 있습니다. 자세한 내용은 [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)을 참조하세요.  
  
## <a name="SSMSProcedure"></a>SQL Server Management Studio 사용  
  
#### <a name="to-make-changes-to-the-steps-of-a-sql-server-agent-master-job"></a>SQL Server 에이전트 마스터 작업의 단계를 변경하려면  
  
1.  **개체 탐색기** 에서 더하기 기호를 클릭하여 단계를 수정하려는 작업이 들어 있는 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **SQL Server 에이전트**를 확장합니다.  
  
3.  더하기 기호를 클릭하여 **작업** 폴더를 확장합니다.  
  
4.  단계를 수정하려는 작업을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
5.  **작업 속성-***job_name* 대화 상자의 **페이지 선택**에서 **단계**를 선택합니다.  
  
6.  **편집**을 클릭하여 **작업 단계 속성 –***job_step_name* 대화 상자를 엽니다. 이 대화 상자에서 사용할 수 있는 옵션에 대한 자세한 내용은 [작업 단계 속성 - 새 작업 단계&#40;일반 페이지&#41;](../../ssms/agent/job-step-properties-new-job-step-general-page.md) 및 [작업 단계 속성 - 새 작업 단계&#40;고급 페이지&#41;](../../ssms/agent/job-step-properties-new-job-step-advanced-page.md)를 참조하세요.  
  
7.  완료되었으면 **확인**을 클릭합니다.  
  
8.  **작업 속성-***job_name* 대화 상자에서 **확인**을 클릭합니다.  
  
## <a name="TsqlProcedure"></a>Transact-SQL 사용  
  
#### <a name="to-make-changes-to-the-steps-of-a-sql-server-agent-master-job"></a>SQL Server 에이전트 마스터 작업의 단계를 변경하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde_md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- changes the number of retry attempts for the first step
    -- of the Weekly Sales Data Backup job.   
    -- After running this example, the number of retry attempts is 10   
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_update_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_id = 1,  
        @retry_attempts = 10 ;  
    GO  
    ```  
  
자세한 내용은 [sp_update_jobstep(Transact-SQL)](http://msdn.microsoft.com/en-us/e158802c-c347-4a5d-bf75-c03e5ae56e6b)을 참조하세요.  
  
