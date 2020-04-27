---
title: 서버 역할 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.serverrole.members.f1
- SQL12.SWB.SERVERROLE.GENERAL.F1
- sql12.swb.serverrole.memberships.f1
helpviewer_keywords:
- SERVER ROLE, creating
ms.assetid: 74f19992-8082-4ed7-92a1-04fe676ee82d
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 22e08b5eb0bccc02303201b7fae46b55f1012fd8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63011969"
---
# <a name="create-a-server-role"></a>서버 역할 만들기
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 새 서버 역할을 만드는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 새 서버 역할을 만듭니다.**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
 데이터베이스 수준 보안 개체에서는 서버 역할에 사용 권한을 부여할 수 없습니다. 데이터베이스 역할을 만들려면 [CREATE ROLE&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-role-transact-sql)을 참조하세요.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
  
-   CREATE SERVER ROLE 권한 또는 sysadmin 고정 서버 역할의 멤버 자격이 필요합니다.  
  
-   로그인의 경우 *server_principal* 에 대한 IMPERSONATE이 필요하고 *server_principal*로 사용되는 서버 역할의 경우 ALTER 권한이 필요합니다. 또는 server_principal로 사용되는 Windows 그룹의 멤버 자격이 필요합니다.  
  
-   AUTHORIZATION 옵션을 사용하여 서버 역할 소유권을 할당할 경우 다음 사용 권한도 필요합니다.  
  
    -   다른 로그인에 서버 역할의 소유권을 할당하려면 해당 로그인에 대한 IMPERSONATE 권한이 필요합니다.  
  
    -   다른 서버 역할에 서버 역할의 소유권을 할당하려면 받는 서버 역할의 멤버 자격이나 해당 서버 역할에 대한 ALTER 권한이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-create-a-new-server-role"></a>새 서버 역할을 만들려면  
  
1.  개체 탐색기에서 새 서버 역할을 만들 서버를 확장합니다.  
  
2.  **보안** 폴더를 확장합니다.  
  
3.  **서버 역할** 폴더를 마우스 오른쪽 단추로 클릭하고 **새 서버 역할...** 을 선택합니다.  
  
4.  **새 서버 역할-**_Server_role_name_ 대화 상자의 **일반** 페이지에서 **서버 역할 이름** 상자에 새 서버 역할의 이름을 입력 합니다.  
  
5.  **소유자** 상자에 새 역할을 소유할 서버 보안 주체의 이름을 입력합니다. 또는 줄임표 **(...)** 를 클릭하여 **서버 로그인 또는 역할 선택** 대화 상자를 엽니다.  
  
6.  **보안 개체**에서 서버 수준 보안 개체를 하나 이상 선택합니다. 보안 개체를 선택하면 해당 보안 개체에 대한 사용 권한을 이 서버 역할에 부여하거나 거부할 수 있습니다.  
  
7.  **사용 권한: 명시적** 상자에서 이 서버 역할에 선택한 보안 개체에 대한 부여 권한, 권한 부여 권한 또는 거부 권한을 부여하는 확인란을 선택합니다. 선택한 보안 개체 중 일부에 대해 사용 권한을 부여하거나 거부할 수 없는 경우 해당 사용 권한은 부분적으로 선택된 것으로 표시됩니다.  
  
8.  **멤버** 페이지에서 **추가** 단추를 사용하여 개인이나 그룹을 나타내는 로그인을 새 서버 역할에 추가합니다.  
  
9. 사용자 정의 서버 역할은 다른 서버 역할의 멤버가 될 수 있습니다. **멤버 자격** 페이지에서 현재 사용자 정의 서버 역할을 선택한 서버 역할의 멤버로 설정하는 확인란을 선택합니다.  
  
10. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-create-a-new-server-role"></a>새 서버 역할을 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    --Creates the server role auditors that is owned the securityadmin fixed server role.  
    USE master;  
    CREATE SERVER ROLE auditors AUTHORIZATION securityadmin;  
    GO  
    ```  
  
 자세한 내용은 [CREATE SERVER ROLE&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-server-role-transact-sql)을 참조하세요.  
  
  
