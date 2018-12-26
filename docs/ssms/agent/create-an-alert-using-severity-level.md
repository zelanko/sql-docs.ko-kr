---
title: 심각도를 사용하여 경고 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server], creating
- SQL Server Agent, alerts
- severity levels [SQL Server]
- alerts [SQL Server], severity levels
ms.assetid: a1fd71bf-5bf9-4ce2-9a1d-032576a4a6e9
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 11d0e5fcc8400f3272d07439adb4658ed46a9675
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51702301"
---
# <a name="create-an-alert-using-severity-level"></a>Create an Alert Using Severity Level
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database Managed Instance T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 경고를 만들어 특정 심각도의 이벤트가 발생할 때 실행되도록 하는 방법에 대해 설명합니다.  
  
**항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
    [제한 사항](#Restrictions)  
  
    [보안](#Security)  
  
-   **다음을 통해 심각도를 사용하여 경고를 만듭니다.**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="Restrictions"></a>제한 사항  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 전체 경고 시스템을 간편하게 그래픽 방식으로 관리할 수 있도록 해 줄 뿐만 아니라 경고 인프라를 구성하는 데 있어서도 권장되는 방법입니다.  
  
-   master 데이터베이스에서 **xp_logevent** 로 생성된 이벤트가 발생합니다. 따라서 경고에 대한 **xp_logevent** 이 **@database_name** 또는 NULL이 아닌 경우 **xp_logevent** 는 경고를 트리거하지 않습니다.  
  
-   19부터 25까지의 심각도를 가진 이벤트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메시지를 [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows 애플리케이션 로그에 보내고 경고를 트리거합니다. 19보다 낮은 심각도를 가진 이벤트는 **sp_altermessage**, RAISERROR WITH LOG 또는 **xp_logevent** 를 사용하여 강제로 Windows 애플리케이션 로그에 경고를 기록하도록 한 경우에만 경고를 트리거합니다.  
  
### <a name="Security"></a>보안  
  
#### <a name="Permissions"></a>Permissions  
기본적으로 **sysadmin** 고정 서버 역할의 멤버만 **sp_add_alert**를 실행할 수 있습니다.  
  
## <a name="SSMSProcedure"></a>SQL Server Management Studio 사용  
  
#### <a name="to-create-an-alert-using-severity-level"></a>심각도를 사용하여 경고를 만들려면  
  
1.  **개체 탐색기** 에서 더하기 기호를 클릭하여 심각도 수준으로 경고를 만들려는 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **SQL Server 에이전트**를 확장합니다.  
  
3.  **경고** 를 마우스 오른쪽 단추로 클릭하고 **새 경고**를 선택합니다.  
  
4.  **새 경고** 대화 상자의 **이름** 상자에 이 경고의 이름을 입력합니다.  
  
5.  **유형** 목록에서 **SQL Server 이벤트 경고**를 선택합니다.  
  
6.  **이벤트 경고 정의**아래의 **데이터베이스 이름** 목록에서 데이터베이스를 선택하여 경고를 특정 데이터베이스로 제한합니다.  
  
7.  **경고 발생 기준**에서 **심각도** 를 클릭한 다음 경고가 발생할 특정 심각도를 선택합니다.  
  
8.  **메시지에 다음 텍스트가 포함될 때 경고 발생** 에 해당하는 확인란을 선택하여 경고를 특정 문자 시퀀스로 제한한 다음 **메시지 텍스트**에 대한 키워드나 문자열을 입력합니다. 최대 문자 수는 100자입니다.  
  
9. **확인**을 클릭합니다.  
  
## <a name="TsqlProcedure"></a>Transact-SQL 사용  
  
#### <a name="to-create-an-alert-using-severity-level"></a>심각도를 사용하여 경고를 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde_md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- adds an alert (Test Alert) that runs the Back up
    -- the AdventureWorks2012 Database job when fired   
    -- assumes that the message 55001 and the Back up
    -- the AdventureWorks2012 Database job already exist.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_alert  
        @name = N'Test Alert',  
        @message_id = 55001,   
       @severity = 0,   
       @notification_message = N'Error 55001 has occurred. The DB will be backed up...',   
       @job_name = N'Back up the AdventureWorks2012 Database' ;  
    GO  
    ```  
  
자세한 내용은 [sp_add_alert(Transact-SQL)](https://msdn.microsoft.com/d9b41853-e22d-4813-a79f-57efb4511f09)를 참조하세요.  
  
