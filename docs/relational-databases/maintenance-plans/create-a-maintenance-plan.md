---
title: 유지 관리 계획 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- maintenance plans [SQL Server], creating
ms.assetid: a945cb65-ba7a-42f4-bbd9-6ec675745523
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: fb094e4b31cdb70f7f9950ae7a82cc884e5fce9a
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51217968"
---
# <a name="create-a-maintenance-plan"></a>유지 관리 계획 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 단일 서버 또는 다중 서버 유지 관리 계획을 만드는 방법에 대해 설명합니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]를 사용하면 유지 관리 계획 마법사나 디자인 화면을 통해 이러한 유지 관리 계획을 만들 수 있습니다. 기본 유지 관리 계획을 만들 때는 마법사가 적합한 반면 디자인 화면을 사용하여 계획을 만들면 워크플로의 향상된 기능을 활용할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
     
     [사전 요구 사항](#Prerequisite)  
  
     [보안](#Security)  
  
-   **유지 관리 계획을 만들려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Restrictions"></a> 제한 사항  
 다중 서버 유지 관리 계획을 만들려면 하나의 마스터 서버 및 하나 이상의 대상 서버가 있는 다중 서버 환경을 구성해야 합니다. 다중 서버 유지 관리 계획은 마스터 서버에서 만들고 유지 관리해야 합니다. 이러한 계획을 대상 서버에서 볼 수 있지만 유지 관리할 수는 없습니다. 
 
###  <a name="Prerequisite"></a> 사전 요구 사항  
[에이전트 XPs 서버 구성 옵션](../../database-engine/configure-windows/agent-xps-server-configuration-option.md) 을 사용하도록 설정해야 합니다.
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 유지 관리 계획을 만들거나 관리하려면 **sysadmin** 고정 서버 역할의 멤버여야 합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-create-a-maintenance-plan-using-the-maintenance-plan-wizard"></a>유지 관리 계획 마법사를 사용하여 유지 관리 계획을 만들려면  
  
1.  개체 탐색기에서 더하기 기호를 클릭하여 유지 관리 계획을 만들 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **관리** 폴더를 확장합니다.  
  
3.  **유지 관리 계획** 폴더를 마우스 오른쪽 단추로 클릭하고 **유지 관리 계획 마법사**를 선택합니다.  
  
4.  마법사의 단계에 따라 유지 관리 계획을 만듭니다. 자세한 내용은 [Use the Maintenance Plan Wizard](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)을 참조하세요.  
  
#### <a name="to-create-a-maintenance-plan-using-the-design-surface"></a>디자인 화면을 사용하여 유지 관리 계획을 만들려면  
  
1.  개체 탐색기에서 더하기 기호를 클릭하여 유지 관리 계획을 만들 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **관리** 폴더를 확장합니다.  
  
3.  **유지 관리 계획** 폴더를 마우스 오른쪽 단추로 클릭하고 **새 유지 관리 계획**을 선택합니다.  
  
4.  [유지 관리 계획 만들기&#40;유지 관리 계획 디자인 화면&#41;](../../relational-databases/maintenance-plans/create-a-maintenance-plan-maintenance-plan-design-surface.md)의 단계에 따라 유지 관리 계획을 만듭니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-create-a-maintenance-plan"></a>유지 관리 계획을 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE msdb;  
    GO  
    --  Adds a new job, executed by the SQL Server Agent service, called "HistoryCleanupTask_1".  
    EXEC dbo.sp_add_job  
       @job_name = N'HistoryCleanupTask_1',   
       @enabled = 1,   
       @description = N'Clean up old task history' ;   
    GO  
    -- Adds a job step for reorganizing all of the indexes in the HumanResources.Employee table to the HistoryCleanupTask_1 job.   
    EXEC dbo.sp_add_jobstep  
        @job_name = N'HistoryCleanupTask_1',   
        @step_name = N'Reorganize all indexes on HumanResources.Employee table',   
        @subsystem = N'TSQL',   
        @command = N'USE AdventureWorks2012  
    GO  
    ALTER INDEX AK_Employee_LoginID ON HumanResources.Employee REORGANIZE WITH ( LOB_COMPACTION = ON )   
    GO  
    USE AdventureWorks2012  
    GO  
    ALTER INDEX AK_Employee_NationalIDNumber ON HumanResources.Employee REORGANIZE WITH ( LOB_COMPACTION = ON )   
    GO  
    USE AdventureWorks2012  
    GO  
    ALTER INDEX AK_Employee_rowguid ON HumanResources.Employee REORGANIZE WITH ( LOB_COMPACTION = ON )   
    GO  
    USE AdventureWorks2012  
    GO  
    ALTER INDEX IX_Employee_OrganizationLevel_OrganizationNode ON HumanResources.Employee REORGANIZE WITH ( LOB_COMPACTION = ON )   
    GO  
    USE AdventureWorks2012  
    GO  
    ALTER INDEX IX_Employee_OrganizationNode ON HumanResources.Employee REORGANIZE WITH ( LOB_COMPACTION = ON )   
    GO  
    USE AdventureWorks2012  
    GO  
    ALTER INDEX PK_Employee_BusinessEntityID ON HumanResources.Employee REORGANIZE WITH ( LOB_COMPACTION = ON )   
    GO  
    ',   
        @retry_attempts = 5,   
        @retry_interval = 5 ;   
    GO  
    -- Creates a schedule named RunOnce that executes every day when the time on the server is 23:00.   
    EXEC dbo.sp_add_schedule  
        @schedule_name = N'RunOnce',   
        @freq_type = 4,   
        @freq_interval = 1,   
        @active_start_time = 233000 ;   
    GO  
    -- Attaches the RunOnce schedule to the job HistoryCleanupTask_1.   
    EXEC sp_attach_schedule  
       @job_name = N'HistoryCleanupTask_1'  
       @schedule_name = N'RunOnce' ;   
    GO  
  
    ```  
  
 참조 항목:  
  
-   [sp_add_job&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)  
  
-   [sp_add_jobstep&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)  
  
-   [sp_add_schedule&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)  
  
-   [sp_attach_schedule&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
  
