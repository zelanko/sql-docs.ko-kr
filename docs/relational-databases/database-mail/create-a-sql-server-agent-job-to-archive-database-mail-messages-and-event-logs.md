---
title: "데이터베이스 메일 메시지 및 이벤트 로그 보관을 처리하는 SQL Server 에이전트 작업 만들기 | Microsoft 문서"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: database-mail
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- archiving mail messages and attachments [SQL Server]
- removing mail messages and attachements
- Database Mail [SQL Server], archiving
- saving mail messages and attachments
ms.assetid: 8f8f0fba-f750-4533-9b76-a9cdbcdc3b14
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8823296f7fd9a64fdc0d5b978a22e89e8b415d37
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2018
---
# <a name="create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs"></a>데이터베이스 메일 메시지 및 이벤트 로그 보관을 처리하는 SQL Server 에이전트 작업 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
데이터베이스 메일 및 첨부 파일의 복사본은 데이터베이스 메일 이벤트 로그와 함께 **msdb** 테이블에 보관됩니다. 정기적으로 테이블의 크기를 축소하고 더 이상 필요하지 않은 메시지와 이벤트를 보관할 수 있습니다. 다음 절차에서는 SQL Server 에이전트 작업을 만들어 이 프로세스를 자동화합니다.  
  
-   **시작하기 전에:**  , [필수 구성 요소](#Prerequisites), [권장 사항](#Recommendations), [권한](#Permissions)  
  
-   **[SQL Server 에이전트](#Process_Overview)를 사용하여 데이터베이스 메일 메시지 및 로그를 보관하려면:**  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Prerequisites"></a> 사전 요구 사항  
 데이터를 저장하고 보관할 새 테이블은 특수한 보관 데이터베이스에 위치할 수 있습니다. 행을 텍스트 파일로 내보낼 수도 있습니다.  
   
###  <a name="Recommendations"></a> 권장 사항  
 프로덕션 환경에서 오류 검사를 추가하고 작업이 실패할 경우 운영자에게 전자 메일 메시지를 보낼 수 있습니다.  
  
  
###  <a name="Permissions"></a> Permissions  
 이 항목에서 설명하는 저장 프로시저를 실행하려면 **sysadmin** 고정 서버 역할의 멤버여야 합니다.  
  
  
###  <a name="Process_Overview"></a> 프로세스 개요  
  
-   첫 번째 절차에서는 다음 단계를 사용하여 Archive Database Mail이라는 작업을 만듭니다.  
  
    1.  모든 메시지를 데이터베이스 메일 테이블에서 **DBMailArchive_***<year_month>* 형식으로 이전 달 이름에 따라 명명된 새 테이블로 복사합니다.  
  
    2.  첫 번째 단계에서 복사된 메시지와 관련된 첨부 파일을 데이터베이스 메일 테이블에서 **DBMailArchive_Attachments_***<year_month>* 형식으로 이전 달 이름에 따라 명명된 새 테이블로 복사합니다.  
  
    3.  첫 번째 단계에서 복사한 메시지와 관련된 데이터베이스 메일 이벤트 로그에서 **DBMailArchive_Log_***<year_month>* 형식으로 이전 달 이름을 따라 명명된 새 테이블로 이벤트를 복사합니다.  
  
    4.  전송된 메일 항목의 레코드를 데이터베이스 메일 테이블에서 삭제합니다.  
  
    5.  전송된 메일 항목과 관련된 이벤트를 데이터베이스 메일 이벤트 로그에서 삭제합니다.  
  
-   정기적으로 실행되도록 작업을 예약합니다.  
  
  
## <a name="to-create-a-sql-server-agent-job"></a>SQL Server 에이전트 작업을 만들려면  
  
1.  개체 탐색기에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 확장하고 **작업**을 마우스 오른쪽 단추로 클릭한 다음 **새 작업**을 클릭합니다.  
  
2.  **새 작업** 대화 상자의 **이름** 입력란에 **Archive Database Mail**을 입력합니다.  
  
3.  **소유자** 드롭다운 목록의 해당 소유자가 **sysadmin** 고정 서버 역할의 멤버인지 확인합니다.  
  
4.  **범주** 드롭다운 목록에서 **데이터베이스 유지 관리**를 클릭합니다.  
  
5.  **설명** 입력란에 **Archive Database Mail messages**를 입력하고 **단계**를 클릭합니다.  
  
 [개요](#Process_Overview)  
  
## <a name="to-create-a-step-to-archive-the-database-mail-messages"></a>데이터베이스 메일 메시지 보관 단계를 만들려면  
  
1.  **단계** 페이지에서 **새로 만들기**를 클릭합니다.  
  
2.  **단계 이름** 입력란에 **Copy Database Mail Items**를 입력합니다.  
  
3.  **유형** 드롭다운 목록에서 **Transact-SQL 스크립트(T-SQL)**를 선택합니다.  
  
4.  **데이터베이스** 드롭다운 목록에서 **msdb**를 선택합니다.  
  
5.  **명령** 입력란에 다음 문을 입력하여 이전 달의 이름을 딴 테이블을 만들고 현재 달의 시작일보다 이전인 행을 포함하도록 합니다.  
  
    ```sql  
    DECLARE @LastMonth nvarchar(12);  
    DECLARE @CopyDate nvarchar(20) ;  
    DECLARE @CreateTable nvarchar(250) ;  
    SET @LastMonth = (SELECT CAST(DATEPART(yyyy,GETDATE()) AS CHAR(4)) + '_' + CAST(DATEPART(mm,GETDATE())-1 AS varchar(2))) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime))  
    SET @CreateTable = 'SELECT * INTO msdb.dbo.[DBMailArchive_' + @LastMonth + '] FROM sysmail_allitems WHERE send_request_date < ''' + @CopyDate +'''';  
    EXEC sp_executesql @CreateTable ;  
    ```  
  
6.  **확인** 을 클릭하여 단계를 저장합니다.  
  
 [개요](#Process_Overview)  
  
## <a name="to-create-a-step-to-archive-the-database-mail-attachments"></a>데이터베이스 메일 첨부 파일 보관 단계를 만들려면  
  
1.  **단계** 페이지에서 **새로 만들기**를 클릭합니다.  
  
2.  **단계 이름** 입력란에 **Copy Database Mail Attachments**를 입력합니다.  
  
3.  **유형** 드롭다운 목록에서 **Transact-SQL 스크립트(T-SQL)**를 선택합니다.  
  
4.  **데이터베이스** 드롭다운 목록에서 **msdb**를 선택합니다.  
  
5.  **명령** 입력란에 다음 문을 입력하여 이전 달의 이름을 딴 테이블을 만들고 이전 단계에서 복사한 메시지에 해당하는 첨부 파일이 포함되도록 합니다.  
  
    ```sql  
    DECLARE @LastMonth nvarchar(12);  
    DECLARE @CopyDate nvarchar(20) ;  
    DECLARE @CreateTable nvarchar(250) ;  
    SET @LastMonth = (SELECT CAST(DATEPART(yyyy,GETDATE()) AS CHAR(4)) + '_' + CAST(DATEPART(mm,GETDATE())-1 AS varchar(2))) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime))  
    SET @CreateTable = 'SELECT * INTO msdb.dbo.[DBMailArchive_Attachments_' + @LastMonth + '] FROM sysmail_attachments   
     WHERE mailitem_id in (SELECT DISTINCT mailitem_id FROM [DBMailArchive_' + @LastMonth + '] )';  
    EXEC sp_executesql @CreateTable ;  
    ```  
  
6.  **확인** 을 클릭하여 단계를 저장합니다.  
  
 [개요](#Process_Overview)  
  
## <a name="to-create-a-step-to-archive-the-database-mail-log"></a>데이터베이스 메일 로그 보관 단계를 만들려면  
  
1.  **단계** 페이지에서 **새로 만들기**를 클릭합니다.  
  
2.  **단계 이름** 입력란에 **Copy Database Mail Log**를 입력합니다.  
  
3.  **유형** 드롭다운 목록에서 **Transact-SQL 스크립트(T-SQL)**를 선택합니다.  
  
4.  **데이터베이스** 드롭다운 목록에서 **msdb**를 선택합니다.  
  
5.  **명령** 입력란에 다음 문을 입력하여 이전 달의 이름을 딴 테이블을 만들고 이전 단계에서 복사한 메시지에 해당하는 로그 항목이 포함되도록 합니다.  
  
    ```sql  
    DECLARE @LastMonth nvarchar(12);  
    DECLARE @CopyDate nvarchar(20) ;  
    DECLARE @CreateTable nvarchar(250) ;  
    SET @LastMonth = (SELECT CAST(DATEPART(yyyy,GETDATE()) AS CHAR(4)) + '_' + CAST(DATEPART(mm,GETDATE())-1 AS varchar(2))) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime))  
    SET @CreateTable = 'SELECT * INTO msdb.dbo.[DBMailArchive_Log_' + @LastMonth + '] FROM sysmail_Event_Log   
     WHERE mailitem_id in (SELECT DISTINCT mailitem_id FROM [DBMailArchive_' + @LastMonth + '] )';  
    EXEC sp_executesql @CreateTable ;  
    ```  
  
6.  **확인** 을 클릭하여 단계를 저장합니다.  
  
 [개요](#Process_Overview)  
  
## <a name="to-create-a-step-to-remove-the-archived-rows-from-database-mail"></a>데이터베이스 메일에서 보관된 행을 제거하는 단계를 만들려면  
  
1.  **단계** 페이지에서 **새로 만들기**를 클릭합니다.  
  
2.  **단계 이름** 입력란에 **Remove rows from Database Mail**을 입력합니다.  
  
3.  **유형** 드롭다운 목록에서 **Transact-SQL 스크립트(T-SQL)**를 선택합니다.  
  
4.  **데이터베이스** 드롭다운 목록에서 **msdb**를 선택합니다.  
  
5.  **명령** 입력란에 다음 문을 입력하여 현재 달보다 이전인 행을 데이터베이스 테이블에서 제거합니다.  
  
    ```sql  
    DECLARE @CopyDate nvarchar(20) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime)) ;  
    EXECUTE msdb.dbo.sysmail_delete_mailitems_sp @sent_before = @CopyDate ;  
    ```  
  
6.  **확인** 을 클릭하여 단계를 저장합니다.  
  
 [개요](#Process_Overview)  
  
## <a name="to-create-a-step-to-remove-the-archived-items-from-database-mail-event-log"></a>데이터베이스 메일 이벤트 로그에서 보관된 항목을 제거하는 단계를 만들려면  
  
1.  **단계** 페이지에서 **새로 만들기**를 클릭합니다.  
  
2.  **단계 이름** 입력란에 **Remove rows from Database Mail event log**를 입력합니다.  
  
3.  **유형** 드롭다운 목록에서 **Transact-SQL 스크립트(T-SQL)**를 선택합니다.  
  
4.  **명령** 입력란에 다음 문을 입력하여 현재 달보다 이전인 행을 데이터베이스 메일 이벤트 로그에서 제거합니다.  
  
    ```sql  
    DECLARE @CopyDate nvarchar(20) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime)) ;  
    EXECUTE msdb.dbo.sysmail_delete_log_sp @logged_before = @CopyDate ;  
    ```  
  
5.  **확인** 을 클릭하여 단계를 저장합니다.  
  
 [개요](#Process_Overview)  
  
## <a name="to-schedule-the-job-to-run-periodically"></a>정기적으로 실행되도록 작업을 예약하려면  
  
1.  **새 작업** 대화 상자에서 **일정**을 클릭합니다.  
  
2.  **일정** 페이지에서 **새로 만들기**를 클릭합니다.  
  
3.  **이름** 입력란에 **Archive Database Mail**을 입력합니다.  
  
4.  **일정 유형** 드롭다운 목록에서 **되풀이**를 선택합니다.  
  
5.  **빈도** 영역에서 정기적으로 작업을 실행할 옵션을 선택합니다(예: 매월 한 번).  
  
6.  **일별 빈도** 영역에서 **한 번 수행 - \<시간>**을(를) 선택합니다.  
  
7.  다른 옵션이 원하는 대로 구성되었는지 확인하고 **확인** 을 눌러 일정을 저장합니다.  
  
8.  **확인** 을 클릭하여 작업을 저장합니다.  
  
 [개요](#Process_Overview)  
  
  
