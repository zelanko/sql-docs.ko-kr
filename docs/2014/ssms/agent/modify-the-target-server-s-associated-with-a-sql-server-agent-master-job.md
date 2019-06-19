---
title: SQL Server 에이전트 마스터 작업과 연결 된 대상 서버 수정 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 176e73b6-08aa-48ec-b349-e84b431e65cc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 61173f4b9ef6c8f836b3654bdc5b7366a8a54461
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62654071"
---
# <a name="modify-the-target-servers-associated-with-a-sql-server-agent-master-job"></a>SQL Server 에이전트 마스터 작업과 연관된 대상 서버 수정
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 SQL Server 에이전트 마스터 작업과 연결된 대상 서버를 수정하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 SQL Server 에이전트 마스터 작업과 연결된 대상 서버를 수정하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 마스터 작업은 로컬 및 원격 서버 모두에서 대상이 될 수 없습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 **sysadmin** 고정 서버 역할의 멤버가 아닌 경우 자신이 소유한 작업만 수정할 수 있습니다. 자세한 내용은 [Implement SQL Server Agent Security](implement-sql-server-agent-security.md)을 참조하세요.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-modify-the-target-servers-associated-with-a-sql-server-agent-master-job"></a>SQL Server 에이전트 마스터 작업과 연결된 대상 서버를 수정하려면  
  
1.  **개체 탐색기** 에서 더하기 기호를 클릭하여 대상 서버를 수정할 작업이 포함된 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **SQL Server 에이전트**를 확장합니다.  
  
3.  더하기 기호를 클릭하여 **작업** 폴더를 확장합니다.  
  
4.  대상 서버를 수정할 작업을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
5.  **작업 속성 -** _job_name_ 대화 상자의 **페이지 선택**에서 **대상**을 선택합니다. 이 페이지에서 사용 가능한 옵션에 대 한 자세한 내용은 참조 하세요. [작업 속성: 새 작업 &#40;페이지를 대상으로&#41;](job-properties-new-job-targets-page.md)합니다.  
  
6.  완료되었으면 **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-delete-a-target-server-currently-associated-with-a-sql-server-agent-master-job"></a>현재 SQL Server 에이전트 마스터 작업과 연결되어 있는 대상 서버를 삭제하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- removes the server SEATTLE2 from processing the Weekly Sales Backupsjob   
    -- assumes that the Weekly Sales Backups job exists  
    USE msdb ;  
    GO  
  
    EXEC sp_delete_jobserver  
        @job_name = N'Weekly Sales Backups',  
        @server_name = N'SEATTLE2' ;  
    GO  
    ```  
  
 자세한 내용은 [sp_delete_jobserver &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql)합니다.  
  
#### <a name="to-associate-a-target-server-with-the-current-sql-server-agent-master-job"></a>대상 서버를 현재 SQL Server 에이전트 마스터 작업과 연결하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- assigns the multiserver job Weekly Sales Backups to the server SEATTLE2   
    -- assumes that the Weekly Sales Backups job already exists and that   
    -- SEATTLE2 is registered as a target server for the current instance  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_jobserver  
        @job_name = N'Weekly Sales Backups',  
        @server_name = N'SEATTLE2' ;  
    GO  
    ```  
  
 자세한 내용은 [sp_add_jobserver &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql)합니다.  
  
  
