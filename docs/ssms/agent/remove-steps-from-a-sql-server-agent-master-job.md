---
title: "SQL Server 에이전트 마스터 작업의 단계 제거 | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 871e6162-1221-464d-8f7f-7e454dcd9edb
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 06d852437a2c3f01d0e15956123c4766b79e70e5
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/23/2018
---
# <a name="remove-steps-from-a-sql-server-agent-master-job"></a>Remove Steps from a SQL Server Agent Master Job
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql_md.md)]에서 SQL Server 에이전트 마스터 작업의 단계를 제거하는 방법에 대해 설명합니다.  
  
**항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
    [제한 사항](#Restrictions)  
  
    [보안](#Security)  
  
-   **다음을 사용하여 SQL Server 에이전트 마스터 작업의 단계를 제거하려면:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="Restrictions"></a>제한 사항  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 마스터 작업은 로컬 및 원격 서버 모두에서 대상이 될 수 없습니다.  
  
### <a name="Security"></a>보안  
  
#### <a name="Permissions"></a>Permissions  
**sysadmin** 고정 서버 역할의 멤버가 아닌 경우 자신이 소유한 작업만 수정할 수 있습니다. 자세한 내용은 [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)을 참조하세요.  
  
## <a name="SSMSProcedure"></a>SQL Server Management Studio 사용  
  
#### <a name="to-remove-steps-from-a-sql-server-agent-master-job"></a>SQL Server 에이전트 마스터 작업의 단계를 제거하려면  
  
1.  **개체 탐색기** 에서 더하기 기호를 클릭하여 단계를 삭제하려는 작업이 들어 있는 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **SQL Server 에이전트**를 확장합니다.  
  
3.  더하기 기호를 클릭하여 **작업** 폴더를 확장합니다.  
  
4.  단계를 삭제하려는 작업을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
5.  **작업 속성-***job_name* 대화 상자의 **페이지 선택**에서 **단계**를 선택합니다.  
  
6.  **작업 단계 목록**에서 삭제하려는 작업 단계를 선택하고 **삭제**를 클릭합니다.  
  
7.  완료되었으면 **확인**을 클릭합니다.  
  
## <a name="TsqlProcedure"></a>Transact-SQL 사용  
  
#### <a name="to-remove-steps-from-a-sql-server-agent-master-job"></a>SQL Server 에이전트 마스터 작업의 단계를 제거하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde_md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- removes job step 1 from the job Weekly Sales Data Backup   
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_delete_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_id = 1 ;  
    GO  
    ```  
  
자세한 내용은 [sp_delete_jobstep(Transact-SQL)](http://msdn.microsoft.com/en-us/421ede8e-ad57-474a-9fb9-92f70a3e77e3)을 참조하세요.  
  
