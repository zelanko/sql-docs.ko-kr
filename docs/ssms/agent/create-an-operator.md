---
description: 운영자 만들기
title: 운영자 만들기
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, operators
- jobs [SQL Server Agent], notification options
- operators (users) [Database Engine], creating with Management Studio
- SQL Server Agent jobs, notification options
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
ms.assetid: 1359d790-5905-4927-a208-e7155e7768a2
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 1c3aa127a22f45d403de94484b590a3fc5db1616
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477124"
---
# <a name="create-an-operator"></a>운영자 만들기
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance)에서는 SQL Server 에이전트 기능이 대부분 지원됩니다. 자세한 내용은 [SQL Server와 Azure SQL Managed Instance 간의 T-SQL 차이점](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 문서에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업에 대한 알림을 받도록 사용자를 구성하는 방법에 대해 설명합니다.  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>제한 사항  
  
-   **이후 버전에서는** 에이전트에서 호출기 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] net send [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]옵션이 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 말고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요.  
  
-   SQL Server 에이전트는 데이터베이스 메일을 사용하여 운영자에게 전자 메일 및 호출기 알림을 보내도록 구성해야 합니다. 자세한 내용은 [경고를 운영자에게 할당](assign-alerts-to-an-operator.md)을 참조하세요.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 작업 구조를 만들고 관리할 수 있는 바람직한 방법을 제공하는데 이는 그래픽을 사용하여 쉽게 작업을 관리할 수 있는 방법입니다.  
  
### <a name="security"></a><a name="Security"></a>보안  
  
#### <a name="permissions"></a><a name="Permissions"></a>권한  
**sysadmin** 고정 서버 역할의 멤버만이 운영자를 만들 수 있습니다.  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>SQL Server Management Studio 사용  
  
#### <a name="to-create-an-operator"></a>운영자를 만들려면  
  
1.  **개체 탐색기** 에서 더하기 기호를 클릭하여 SQL Server 에이전트 운영자를 만들려는 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **SQL Server 에이전트** 를 확장합니다.  
  
3.  **운영자** 폴더를 마우스 오른쪽 단추로 클릭하고 **새 운영자** 를 선택합니다.  
  
    **새 운영자** 대화 상자의 **일반** 페이지에는 다음과 같은 옵션이 제공됩니다.  
  
    **Name**  
    운영자의 이름을 변경합니다.  
  
    **Enabled**  
    운영자를 활성화합니다. 활성화하지 않으면 해당 운영자에게 알림이 전송되지 않습니다.  
  
    **전자 메일 이름**  
    운영자의 전자 메일 주소를 지정합니다.  
  
    **Net Send 주소**  
    **net send** 에 사용할 주소를 지정합니다.  
  
    **호출기 전자 메일 이름**  
    운영자의 호출기에 사용할 전자 메일 주소를 지정합니다.  
  
    **호출기 연락 가능 근무 일정**  
    호출기로 연락 가능한 시간을 설정합니다.  
  
    **월요일 - 일요일**  
    호출기로 연락 가능한 요일을 선택합니다.  
  
    **업무 시작 시간**  
    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 호출기로 메시지를 보내기 시작하는 시간을 선택합니다.  
  
    **업무 종료 시간**  
    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 호출기로 메시지를 더 이상 보내지 않는 기준 시간을 선택합니다.  
  
    **새 운영자** 대화 상자의 **알림** 페이지에는 다음과 같은 옵션이 제공됩니다.  
  
    **경고**  
    인스턴스의 경고를 표시합니다.  
  
    **작업**  
    인스턴스의 작업을 표시합니다.  
  
    **경고 목록**  
    인스턴스의 경고를 나열합니다.  
  
    **작업 목록**  
    인스턴스의 작업을 나열합니다.  
  
    **전자 메일**  
    전자 메일을 사용하여 이 운영자에게 알립니다.  
  
    **호출기**  
    호출기 주소로 전자 메일을 보내 이 운영자에게 알립니다.  
  
    **Net Send**  
    **net send** 를 사용하여 이 운영자에게 알립니다.  
  
4.  새 운영자 만들기를 마쳤으면 **확인** 을 클릭합니다.  
  
## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a>Transact-SQL 사용  
  
#### <a name="to-create-an-operator"></a>운영자를 만들려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDE](../../includes/ssde_md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다.  
  
    ```  
    -- sets up the operator information for user 'danwi.'
    -- The operator is enabled.   
    -- SQL Server Agent sends notifications by pager 
    -- from Monday through Friday from 8 A.M. to 5 P.M.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_operator  
        @name = N'Dan Wilson',  
        @enabled = 1,  
        @email_address = N'danwi',  
        @pager_address = N'5551290AW@pager.Adventure-Works.com',  
        @weekday_pager_start_time = 080000,  
        @weekday_pager_end_time = 170000,  
        @pager_days = 62 ;  
    GO  
    ```  
  
자세한 내용은 [sp_add_operator(Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)를 참조하세요.  
