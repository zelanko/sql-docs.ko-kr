---
title: Analysis Services 작업 단계 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- job steps [Analysis Services]
ms.assetid: 03d4bb86-514b-4a55-97b9-c2c0fa08b428
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 832e49db5221c2e978cac584e8f1e406d33be30f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63134995"
---
# <a name="create-an-analysis-services-job-step"></a>Create an Analysis Services Job Step
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 SQL Server 관리 개체를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]Analysis Services 명령 및 쿼리를 실행하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 에이전트 작업 단계를 만들고 정의하는 방법에 대해 설명합니다.  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **Analysis Services 명령 및/또는 쿼리를 사용하여 SQL Server 작업 단계를 만들려면:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server 관리 개체](#SMO)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   작업 단계에서 Analysis Services 명령을 사용하는 경우 명령 문은 XML for Analysis Services **Execute** 메서드여야 합니다. 문에 전체 SOAP(Simple Object Access Protocol) Envelope 또는 XML for Analysis **Discover** 메서드를 포함할 수 없습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서는 전체 SOAP Envelope와 **Discover** 메서드를 지원하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 단계에서는 지원하지 않습니다. XML for Analysis Services에 대한 자세한 내용은 [XML for Analysis 개요(XMLA)](https://msdn.microsoft.com/library/ms187190.aspx)를 참조하세요.  
  
-   작업 단계에서 Analysis Services 쿼리를 사용하는 경우 쿼리 문은 MDX(Multidimensional Expressions) 쿼리여야 합니다. MDX에 대 한 자세한 내용은 참조 하세요. [MDX 쿼리 기본 사항 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
  
-   Analysis Services 하위 시스템을 사용하는 작업 단계를 실행하려면 사용자가 **sysadmin** 고정 서버 역할의 멤버이거나 이 하위 시스템을 사용하도록 정의된 올바른 프록시 계정에 액세스할 수 있어야 합니다. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 계정이나 프록시가 Analysis Services 관리자이고 올바른 Windows 도메인 계정이어야 합니다.  
  
-   **sysadmin** 고정 서버 역할의 멤버만 작업 단계 출력을 파일에 쓸 수 있습니다. **msdb** 데이터베이스에서 **SQLAgentUserRole** 데이터베이스 역할 멤버인 사용자가 작업 단계를 실행하면 테이블에만 출력을 쓸 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 **msdb** 데이터베이스의 **sysjobstepslog** 테이블에 작업 단계 출력을 씁니다.  
  
-   자세한 내용은 [Implement SQL Server Agent Security](implement-sql-server-agent-security.md)을 참조하세요.  
  
##  <a name="SSMS"></a> SQL Server Management Studio 사용  
  
#### <a name="to-create-an-analysis-services-command-job-step"></a>Analysis Services 명령 작업 단계를 만들려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **SQL Server 에이전트**를 확장하고 새 작업을 만들거나 기존 작업을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다. 작업을 만드는 방법은 [작업 만들기](create-jobs.md)를 참조하세요.  
  
3.  **작업 속성** 대화 상자에서 **단계** 페이지를 클릭한 다음 **새로 만들기**를 클릭합니다.  
  
4.  **새 작업 단계** 대화 상자에서 작업 **단계 이름**을 입력합니다.  
  
5.  **유형** 목록에서 **SQL Server Analysis Services 명령**을 클릭합니다.  
  
6.  **다음 계정으로 실행** 목록에서 Analysis Services 명령 하위 시스템을 사용하도록 정의된 프록시를 선택합니다. **sysadmin** 고정 서버 역할의 멤버인 사용자는 **SQL 에이전트 서비스 계정** 을 선택하여 이 작업 단계를 실행할 수도 있습니다.  
  
7.  작업 단계를 실행할 **서버** 를 선택하거나 서버 이름을 입력합니다.  
  
8.  **명령** 입력란에 실행할 문을 입력하거나 **열기** 를 클릭하여 문을 선택합니다.  
  
9. 작업 단계가 성공하거나 실패할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 수행할 동작으로 작업 단계를 시도할 횟수 및 작업 단계 출력이 쓸 위치와 같은 작업 단계에 대한 옵션을 정의하려면 **고급** 페이지를 클릭합니다.  
  
#### <a name="to-create-an-analysis-services-query-job-step"></a>Analysis Services 쿼리 작업 단계를 만들려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **SQL Server 에이전트**를 확장하고 새 작업을 만들거나 기존 작업을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다. 작업을 만드는 방법은 [작업 만들기](create-jobs.md)를 참조하세요.  
  
3.  **작업 속성** 대화 상자에서 **단계** 페이지를 클릭한 다음 **새로 만들기**를 클릭합니다.  
  
4.  **새 작업 단계** 대화 상자에서 작업 **단계 이름**을 입력합니다.  
  
5.  **유형** 목록에서 **SQL Server Analysis Services 쿼리**를 클릭합니다.  
  
6.  **다음 계정으로 실행** 목록에서 Analysis Services 쿼리 하위 시스템을 사용하도록 정의된 프록시를 선택합니다. **sysadmin** 고정 서버 역할의 멤버인 사용자는 **SQL 에이전트 서비스 계정** 을 선택하여 이 작업 단계를 실행할 수도 있습니다.  
  
7.  작업 단계를 실행할 **서버** 와 **데이터베이스** 를 선택하거나 서버 또는 데이터베이스 이름을 입력합니다.  
  
8.  **명령** 입력란에 실행할 문을 입력하거나 **열기** 를 클릭하여 문을 선택합니다.  
  
9. 작업 단계가 성공하거나 실패할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 수행할 동작으로 작업 단계를 시도할 횟수 및 작업 단계 출력이 쓸 위치와 같은 작업 단계에 대한 옵션을 정의하려면 **고급** 페이지를 클릭합니다.  
  
##  <a name="TSQL"></a> Transact-SQL 사용  
  
#### <a name="to-create-an-analysis-services-command-job-step"></a>Analysis Services 명령 작업 단계를 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
  
              -- Creates a job step that uses XMLA to create a relational data source that references the AdventureWorks2012 Microsoft SQL Server database  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Create a relational data source that references the AdventureWorks2012 Microsoft SQL Server database ',  
        @subsystem = N'ANALYSISCOMMAND',  
        @command = N' <Create xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
        <ParentObject>  
            <DatabaseID>AdventureWorks2012</DatabaseID>  
        </ParentObject>  
        <ObjectDefinition>  
            <DataSource xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RelationalDataSource">  
                <ID>AdventureWorks2012</ID>  
                <Name>Adventure Works 2012</Name>  
                <ConnectionString>Data Source=localhost;Initial Catalog=AdventureWorks2012;Integrated Security=True</ConnectionString>  
                <ImpersonationInfo>  
                    <ImpersonationMode>ImpersonateServiceAccount</ImpersonationMode>  
                </ImpersonationInfo>  
                <ManagedProvider>System.Data.SqlClient</ManagedProvider>  
                <Timeout>PT0S</Timeout>  
            </DataSource>  
        </ObjectDefinition>  
    </Create>', ;  
    GO  
    ```  
  
 자세한 내용은 [sp_add_jobstep &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql)합니다.  
  
#### <a name="to-create-an-analysis-services-query-job-step"></a>Analysis Services 쿼리 작업 단계를 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
  
              -- Creates a job step that uses MDX to return data  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Returns the Internet sales amount by state',  
        @subsystem = N'ANALYSISQUERY',  
        @command = N' SELECT  
       [Measures].[Internet Sales Amount] ON COLUMNS,  
       [Customer].[State-Province].Members ON ROWS  
    FROM [AdventureWorks2012]',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    ```  
  
 자세한 내용은 [sp_add_jobstep &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql)합니다.  
  
##  <a name="SMO"></a> SQL Server 관리 개체를 사용 하 여  
 **PowerShell 스크립트 작업 단계를 만들려면**  
  
 선택한 프로그래밍 언어(예: XMLA 또는 MDX)를 사용하여 `JobStep` 클래스를 사용합니다. 자세한 내용은 [SMO(SQL Server 관리 개체)](https://msdn.microsoft.com/library/ms162169.aspx)를 참조하세요.  
  
  
