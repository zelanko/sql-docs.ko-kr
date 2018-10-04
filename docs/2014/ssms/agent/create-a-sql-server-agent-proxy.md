---
title: SQL Server 에이전트 프록시 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- proxies [SQL Server Agent], creating
ms.assetid: 142e0c55-a8b9-4669-be49-b9dc602d5988
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ef4a623dca8ecdc92753b80438682f12521bfe8f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48108813"
---
# <a name="create-a-sql-server-agent-proxy"></a>SQL Server 에이전트 프록시 만들기
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 SQL Server 에이전트 프록시를 만드는 방법에 대해 설명합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시 계정은 작업 단계를 실행할 수 있는 보안 컨텍스트를 정의합니다. 각 프록시는 보안 자격 증명에 해당됩니다. 특정 작업 단계의 사용 권한을 설정하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 하위 시스템에 대한 필요 권한을 가진 프록시를 만든 다음 해당 프록시를 작업 단계에 할당하세요.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **SQL Server 에이전트 프록시를 만들려면:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   사용 가능한 자격 증명이 없는 경우 프록시를 만들기 전에 먼저 자격 증명을 만들어야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시는 자격 증명을 사용하여 Windows 사용자 계정에 대한 정보를 저장합니다. 자격 증명에 지정된 사용자에게 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 실행 중인 컴퓨터에 대한 "일괄 작업으로 로그온" 권한이 있어야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 프록시에 대한 하위 시스템 액세스 권한을 확인하고 작업 단계가 실행될 때마다 프록시에 대한 액세스 권한을 부여합니다. 프록시에 하위 시스템에 대한 액세스 권한이 없으면 작업 단계가 실패합니다. 그렇지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 프록시에 지정된 사용자를 가장하여 작업 단계를 실행합니다.  
  
-   프록시를 만들 때 프록시에 대한 자격 증명에 지정된 사용자의 권한은 변경되지 않습니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에 연결할 수 있는 권한이 없는 사용자에 대한 프록시를 만들 수 있습니다. 이 경우 해당 프록시를 사용하는 작업 단계에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결할 수 없습니다.  
  
-   사용자의 로그인에 프록시에 대한 액세스 권한이 있거나 사용자가 프록시에 대한 액세스 권한이 있는 역할에 속하는 경우 해당 사용자는 작업 단계에서 프록시를 사용할 수 있습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
  
-   **sysadmin** 고정 서버 역할의 멤버만 프록시 계정을 생성, 수정 또는 삭제할 수 있는 권한을 가집니다. 프록시를 사용하려면 **sysadmin** 고정 서버 역할의 멤버가 아닌 사용자를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의** 에이전트 고정 데이터베이스 역할 **SQLAgentUserRole**, **SQLAgentReaderRole**또는 **SQLAgentOperatorRole**중 하나에 추가해야 합니다.  
  
-   프록시와 자격 증명을 만드는 경우 `ALTER ANY CREDENTIAL` 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-create-a-sql-server-agent-proxy"></a>SQL Server 에이전트 프록시를 만들려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 SQL Server 에이전트에 프록시를 만들려는 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **SQL Server 에이전트**를 확장합니다.  
  
3.  **프록시** 폴더를 마우스 오른쪽 단추로 클릭하고 **새 프록시**를 선택합니다.  
  
4.  **새 프록시 계정** 대화 상자의 **일반** 페이지에서 **인덱스 이름** 상자에 프록시 계정의 이름을 입력합니다.  
  
5.  **자격 증명 이름** 대화 상자에서 프록시 계정에 사용할 보안 자격 증명의 이름을 입력합니다.  
  
6.  **설명** 상자에 프록시 계정에 대한 설명을 입력합니다.  
  
7.  **다음 하위 시스템에 대해 활성화**에서 이 프록시에 대한 적절한 하위 시스템을 선택합니다.  
  
8.  **보안 주체** 페이지에서 프록시 계정에 대한 액세스 권한을 부여 또는 제거할 로그인이나 역할을 추가하거나 제거합니다.  
  
9. 완료되었으면 **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-create-a-sql-server-agent-proxy"></a>SQL Server 에이전트 프록시를 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- creates credential CatalogApplicationCredential  
    USE msdb ;  
    GO  
    CREATE CREDENTIAL CatalogApplicationCredential WITH IDENTITY = 'REDMOND/TestUser',   
        SECRET = 'G3$1o)lkJ8HNd!';  
    GO  
    -- creates proxy "Catalog application proxy" and assigns the credential 'CatalogApplicationCredential' to it.  
    EXEC dbo.sp_add_proxy  
        @proxy_name = 'Catalog application proxy',  
        @enabled = 1,  
        @description = 'Maintenance tasks on catalog application.',  
        @credential_name = 'CatalogApplicationCredential' ;  
    GO  
    -- grants the proxy "Catalog application proxy" access to the ActiveX Scripting subsystem.  
    EXEC dbo.sp_grant_proxy_to_subsystem  
        @proxy_name = N'Catalog application proxy',  
        @subsystem_id = 2 ;  
    GO  
    ```  
  
 참조 항목:  
  
-   [CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)  
  
-   [sp_add_proxy &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-proxy-transact-sql)  
  
-   [sp_grant_proxy_to_subsystem &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-grant-proxy-to-subsystem-transact-sql)  
  
  
