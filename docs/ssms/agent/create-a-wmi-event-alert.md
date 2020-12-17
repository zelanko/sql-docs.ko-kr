---
description: WMI 이벤트 경고 만들기
title: WMI 이벤트 경고 만들기
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- WMI event alerts [SQL Server Management Studio]
ms.assetid: b8c46db6-408b-484e-98f0-a8af3e7ec763
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 1ae08f86a984f4a8bdbc73db02fb41e335250e4f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464474"
---
# <a name="create-a-wmi-event-alert"></a>WMI 이벤트 경고 만들기
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance)에서는 SQL Server 에이전트 기능이 대부분 지원됩니다. 자세한 내용은 [SQL Server와 Azure SQL Managed Instance 간의 T-SQL 차이점](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 서버 이벤트용 WMI 공급자가 모니터링하여 특정 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 이벤트가 발생할 때 [!INCLUDE[tsql](../../includes/tsql-md.md)]에이전트 경고를 만드는 방법에 대해 설명합니다.  
  
WMI 공급자를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이벤트를 모니터링하는 방법에 대한 자세한 내용은 [서버 이벤트용 WMI 공급자 클래스 및 속성](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)을 참조하세요. WMI 이벤트 경고 알림을 받는 데 필요한 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 서비스의 계정 선택](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md)을 참조하세요. WQL에 대한 자세한 내용은 [서버 이벤트용 WMI 공급자에 WQL 사용](../../relational-databases/wmi-provider-server-events/using-wql-with-the-wmi-provider-for-server-events.md)을 참조하세요.  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>제한 사항  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 전체 경고 시스템을 간편하게 그래픽 방식으로 관리할 수 있도록 해 줄 뿐만 아니라 경고 인프라를 구성하는 데 있어서도 권장되는 방법입니다.  
  
-   master 데이터베이스에서 **xp_logevent** 로 생성된 이벤트가 발생합니다. 따라서 경고에 대한 **\@database_name** 이 **'master'** 또는 NULL이 아닌 경우 **xp_logevent** 는 경고를 트리거하지 않습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 실행하는 컴퓨터의 WMI 네임스페이스만 지원됩니다.  
  
### <a name="security"></a><a name="Security"></a>보안  
  
#### <a name="permissions"></a><a name="Permissions"></a>권한  
기본적으로 **sysadmin** 고정 서버 역할의 멤버만 **sp_add_alert** 를 실행할 수 있습니다.  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>SQL Server Management Studio 사용  
  
#### <a name="to-create-a-wmi-event-alert"></a>WMI 이벤트 경고를 만들려면  
  
1.  **개체 탐색기** 에서 더하기 기호를 클릭하여 WMI 이벤트 경고를 만들려는 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **SQL Server 에이전트** 를 확장합니다.  
  
3.  **경고** 를 마우스 오른쪽 단추로 클릭하고 **새 경고** 를 선택합니다.  
  
4.  **새 경고** 대화 상자의 **이름** 상자에 이 경고의 이름을 입력합니다.  
  
5.  **사용** 확인란을 선택하여 경고를 실행할 수 있도록 합니다. 기본적으로 **사용** 이 선택됩니다.  
  
6.  **유형** 목록에서 **WMI 이벤트 경고** 를 선택합니다.  
  
7.  **WMI 이벤트 경고 정의** 의 **네임스페이스** 상자에 이 경고를 트리거할 WMI 이벤트를 식별하는 WQL(WMI Query Language) 문에 대한 WMI 네임스페이스를 지정합니다.  
  
8.  **쿼리** 상자에 이 경고가 응답하는 이벤트를 식별할 WQL 문을 지정합니다.  
  
9. **확인** 을 클릭합니다.  
  
## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a>Transact-SQL 사용  
  
#### <a name="to-create-a-wmi-event-alert"></a>WMI 이벤트 경고를 만들려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDE](../../includes/ssde_md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다.  
  
    ```  
    -- creates a WMI event alert that retrieves all event properties for any ALTER_TABLE event that occurs on table AdventureWorks2012.Sales.SalesOrderDetail  
    -- This example assumes that the message 54001 already exists.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_alert  
        @name = N'Test Alert 2',  
        @message_id = 54001  
        @notification_message = N'Error 54001 has occurred on the Sales.SalesOrderDetail table on the AdventureWorks2012 database.',  
        @wmi_namespace = '\\.\root\Microsoft\SqlServer\ServerEvents\,  
        @wmi_query = N'SELECT * FROM ALTER_TABLE   
    WHERE DatabaseName = 'AdventureWorks2012' AND SchemaName = 'Sales'   
        AND ObjectType='Table' AND ObjectName = 'SalesOrderDetail'';  
    GO  
    ```  
  
자세한 내용은 [sp_add_alert(Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)를 참조하세요.  
