---
title: 로그인 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.LOGIN.SERVERROLES.F1
- sql12.swb.login.databaseaccess.f1
- sql12.swb.login.general.f1
- sql12.swb.login.effectivepermissions.f1
- sql12.swb.login.status.f1
helpviewer_keywords:
- authentication [SQL Server], logins
- logins [SQL Server], creating
- creating logins with Management Studio
- Create login [SQL Server]
- SQL Server logins
ms.assetid: fb163e47-1546-4682-abaa-8c9494e9ddc7
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: b765248e43dc66b9e1c038df27ca9a8b6135706d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63012026"
---
# <a name="create-a-login"></a>로그인 만들기
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 로그인을 만드는 방법에 대해 설명합니다. 로그인은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스에 연결하는 사용자 또는 프로세스의 ID입니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [배경](#Background)  
  
     [보안](#Security)  
  
-   **로그인을 만들려면 사용 합니다.**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **후속 작업:**  [로그인을 만든 후 수행할 단계](#FollowUp)  
  
##  <a name="Background"></a> 배경  
 로그인은 보안 시스템에서 인증을 수행할 수 있는 보안 주체 또는 엔터티입니다. 사용자가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결하려면 로그인이 필요합니다. 도메인 사용자 또는 Windows 도메인 그룹 등의 Windows 주체에 기반한 로그인을 만들거나 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인과 같은 Windows 주체에 기반한 로그인을 만들 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용하려면 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]에서 혼합 모드 인증을 사용해야 합니다. 자세한 내용은 [인증 모드 선택](../choose-an-authentication-mode.md)을 참조하세요.  
  
 보안 주체는 사용 권한을 로그인에 부여할 수 있습니다. 로그인의 범위는 전체 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]입니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스에서 특정 데이터베이스에 연결하려면 로그인을 데이터베이스 사용자에 매핑해야 합니다. 이 경우 로그인이 아니라 데이터베이스 내의 사용 권한이 데이터베이스 사용자에게 부여되며 거부됩니다. 범위가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 전체 인스턴스에 속하는 사용 권한(예: `CREATE ENDPOINT` 권한)을 로그인에 부여할 수 있습니다.  
  
##  <a name="Security"></a> 보안  
  
### <a name="permissions"></a>사용 권한  
 서버에 대한 `ALTER ANY LOGIN` 또는 `ALTER LOGIN` 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
##### <a name="to-create-a-sql-server-login"></a>SQL Server 로그인을 만들려면  
  
1.  개체 탐색기에서 새 로그인을 만들려는 서버 인스턴스의 폴더를 확장합니다.  
  
2.  **보안** 폴더를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 가리킨 후 **로그인...** 을 선택합니다.  
  
3.  **로그인 - 신규** 대화 상자의 **일반** 페이지에서 **로그인 이름** 상자에 사용자 이름을 입력합니다. 또는 **검색...** 을 클릭하여 **사용자 또는 그룹 선택** 대화 상자를 엽니다.  
  
     **검색...** 을 클릭한 경우:  
  
    1.  **개체 유형 선택**에서 **개체 유형...** 을 클릭하여 **개체 유형** 대화 상자를 열고 다음 중에서 일부 또는 전부를 선택합니다. **기본 제공 보안 주체**, **그룹** 및 **사용자**. **기본 제공 보안 주체** 및 **사용자** 는 기본적으로 선택됩니다. 완료되었으면 **확인**을 클릭합니다.  
  
    2.  **찾을 위치를 선택하세요.** 에서 **위치...** 를 클릭하여 **위치** 대화 상자를 열고 사용 가능한 서버 위치 중 하나를 선택합니다. 완료되었으면 **확인**을 클릭합니다.  
  
    3.  **선택할 개체 이름을 입력하세요(예제)** 에서 찾으려는 사용자 또는 그룹 이름을 입력합니다. 자세한 내용은 [사용자, 컴퓨터 또는 그룹 선택 대화 상자](https://technet.microsoft.com/library/cc771712.aspx)를 참조하세요.  
  
    4.  고급 검색 옵션을 보려면 **고급...** 을 클릭합니다. 자세한 내용은 [사용자, 컴퓨터 또는 그룹 선택 대화 상자 - 고급 페이지](https://technet.microsoft.com/library/cc733110.aspx)를 참조하세요.  
  
    5.  **확인**을 클릭합니다.  
  
4.  보안 주체에 따라 로그인을 만들려면 **Windows 인증**을 선택합니다. 이 옵션이 기본 옵션입니다.  
  
5.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 저장된 로그인을 만들려면 **SQL Server 인증**을 선택합니다.  
  
    1.  **암호** 상자에 새 사용자의 암호를 입력합니다. **암호 확인** 상자에 암호를 다시 입력합니다.  
  
    2.  기존 암호를 변경할 때는 **이전 암호 지정**을 선택하고 **이전 암호** 상자에 이전 암호를 입력합니다.  
  
    3.  복잡성 및 강제 적용에 대한 암호 정책 옵션을 강제로 적용하려면 **암호 정책 강제 적용**을 선택합니다. 자세한 내용은 [Password Policy](../password-policy.md)을 참조하세요. 이 옵션은 **SQL Server 인증** 을 선택한 경우 기본 옵션입니다.  
  
    4.  만료에 대한 암호 정책 옵션을 강제로 적용하려면 **암호 만료 강제 적용**을 선택합니다. 이 확인란은**암호 정책 강제 적용** 을 선택한 경우에만 사용할 수 있습니다. 이 옵션은 **SQL Server 인증** 을 선택한 경우 기본 옵션입니다.  
  
    5.  사용자가 처음 로그인을 사용한 후 새 암호를 만들도록 하려면 **다음 로그인할 때 반드시 암호 변경**을 선택합니다. 이 확인란은**암호 만료 강제 적용** 을 선택한 경우에만 사용할 수 있습니다. 이 옵션은 **SQL Server 인증** 을 선택한 경우 기본 옵션입니다.  
  
6.  로그인을 독립형 보안 인증서와 연결하려면 **인증서로 매핑** 을 선택한 후 목록에서 기존 인증서의 이름을 선택합니다.  
  
7.  로그인을 독립형 비대칭 키와 연결하려면 **비대칭 키로 매핑** 을 선택한 후 목록에서 기존 키의 이름을 선택합니다.  
  
8.  로그인을 보안 인증서와 연결하려면 **인증서로 매핑** 확인란을 선택한 후 목록에서 기존 인증서를 선택하거나 **추가** 를 클릭하여 새 인증서를 만듭니다. 로그인에서 보안 인증서에 대한 매핑을 제거하려면 **인증서로 매핑** 에서 인증서를 선택하고 **제거**를 클릭합니다. 일반적으로 인증서에 대한 자세한 내용은 [자격 증명&#40;데이터베이스 엔진&#41;](credentials-database-engine.md)을 참조하세요.  
  
9. **기본 데이터베이스** 목록에서 로그인에 대한 기본 데이터베이스를 선택합니다. **Master** 는 이 옵션의 기본값입니다.  
  
10. **기본 언어** 목록에서 로그인에 대한 기본 언어를 선택합니다.  
  
11. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="additional-options"></a>추가 옵션  
 **로그인 - 신규** 대화 상자에서는 다음 네 가지 추가 페이지에 대한 옵션도 제공합니다. **서버 역할**, **사용자 매핑**, **보안 개체** 및 **상태**.  
  
### <a name="server-roles"></a>서버 역할  
 **서버 역할** 페이지에는 새 로그인에 할당할 수 있는 모든 사용 가능한 역할이 나열됩니다. 사용할 수 있는 옵션은 다음과 같습니다.  
  
 **bulkadmin** 확인란  
 **bulkadmin** 고정 서버 역할의 멤버는 BULK INSERT 문을 실행할 수 있습니다.  
  
 **dbcreator** 확인란  
 **dbcreator** 고정 서버 역할의 멤버는 데이터베이스를 생성, 변경, 삭제, 복원할 수 있습니다.  
  
 **diskadmin** 확인란  
 **dbcreator** 고정 서버 역할의 멤버는 디스크 파일을 관리할 수 있습니다.  
  
 **processadmin** 확인란  
 **processadmin** 고정 서버 역할의 멤버는 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]의 인스턴스에서 실행되는 프로세스를 종료할 수 있습니다.  
  
 **public** 확인란  
 모든 SQL Server 사용자, 그룹 및 역할은 기본적으로 **public** 고정 서버 역할에 속합니다.  
  
 **securityadmin** 확인란  
 **securityadmin** 고정 서버 역할의 멤버는 로그인 및 해당 속성을 관리합니다. 이러한 멤버는 서버 수준의 사용 권한을 부여(GRANT), 거부(DENY) 및 취소(REVOKE)할 수 있습니다. 또한 데이터베이스 수준의 사용 권한을 부여(GRANT), 거부(DENY) 및 취소(REVOKE)할 수 있습니다. 또한 이 역할의 멤버는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 로그인 암호를 다시 설정할 수 있습니다.  
  
 **serveradmin** 확인란  
 **serveradmin** 고정 서버 역할의 멤버는 서버 차원의 구성 옵션을 변경하고 서버를 종료할 수 있습니다.  
  
 **setupadmin** 확인란  
 **setupadmin** 고정 서버 역할의 멤버는 연결된 서버를 추가하거나 제거하고 일부 시스템 저장 프로시저를 실행할 수 있습니다.  
  
 **sysadmin** 확인란  
 **sysadmin** 고정 서버 역할의 멤버는 모든 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]작업을 수행할 수 있습니다.  
  
### <a name="user-mapping"></a>사용자 매핑  
 **사용자 매핑** 페이지에는 사용 가능한 모든 데이터베이스와 이러한 데이터베이스에서 해당 로그인에 적용할 수 있는 데이터베이스 역할이 나열됩니다. 선택한 데이터베이스에 따라 로그인에 사용할 수 있는 역할 멤버 자격이 결정됩니다. 이 페이지에서는 다음과 같은 옵션을 사용할 수 있습니다.  
  
 **이 로그인으로 매핑된 사용자**  
 이 로그인으로 액세스할 수 있는 데이터베이스를 선택합니다. 데이터베이스를 선택하면 **데이터베이스 역할 멤버 자격:** _database_name_ 창에 유효한 데이터베이스 역할이 표시됩니다.  
  
 **지도**  
 아래 나열되는 데이터베이스에 해당 로그인이 액세스하는 것을 허용합니다.  
  
 **데이터베이스 백업**  
 서버의 사용 가능한 데이터베이스를 나열합니다.  
  
 **사용자**  
 로그인에 매핑할 데이터베이스 사용자를 지정합니다. 기본적으로 데이터베이스 사용자의 이름은 로그인과 같습니다.  
  
 **기본 스키마**  
 사용자의 기본 스키마를 지정합니다. 사용자를 처음 만들 경우 기본 스키마는 **dbo**입니다. 아직 존재하지 않는 기본 스키마를 지정할 수도 있습니다. Windows 그룹, 인증서 또는 비대칭 키에 매핑된 사용자에 대해서는 기본 스키마를 지정할 수 없습니다.  
  
 **Guest account enabled for:**  _database_name_  
 선택한 데이터베이스에 게스트 계정이 설정되어 있는지 여부를 나타내는 읽기 전용 특성입니다. 게스트 계정에 대한 **로그인 속성** 대화 상자의 **상태** 페이지를 사용하여 게스트 계정을 설정하거나 해제할 수 있습니다.  
  
 **Database role membership for:**  _database_name_  
 지정한 데이터베이스 사용자에 대한 역할을 선택합니다. 모든 사용자는 모든 데이터베이스에서 **public** 역할의 멤버이며 제거할 수 없습니다. 데이터베이스 역할에 대한 자세한 내용은 [데이터베이스 수준 역할](database-level-roles.md)을 참조하세요.  
  
### <a name="securables"></a>보안 개체  
 **보안 개체** 페이지에는 사용 가능한 모든 보안 개체와 이러한 보안 개체에서 로그인에 부여할 수 있는 권한이 나열됩니다. 이 페이지에서는 다음과 같은 옵션을 사용할 수 있습니다.  
  
 **상단 표**  
 사용 권한을 설정할 수 있는 항목이 하나 이상 포함됩니다. 상단 표에 표시되는 열은 보안 주체 또는 보안 개체에 따라 달라집니다.  
  
 상단 표에 항목을 추가하려면  
  
1.  **검색**을 클릭합니다.  
  
2.  **개체 추가** 대화 상자에서 다음 옵션 중 하나를 선택합니다. **특정 개체...** , **유형의 모든 개체...** , 또는 **서버**_server_name_합니다. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  **서버**_server_name_을 선택하면 상단 표에 해당 서버의 모든 보안 개체가 자동으로 채워집니다.  
  
3.  **특정 개체...** 를 선택한 경우:  
  
    1.  **개체 선택** 대화 상자의 **개체 유형 선택**에서 **개체 유형...** 을 클릭합니다.  
  
    2.  **개체 유형 선택** 대화 상자에서 다음 개체 유형 중 하나를 선택합니다. **엔드포인트**, **로그인**, **서버**, **가용성 그룹** 및 **서버 역할**. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    3.  **선택할 개체 이름을 입력하세요(예제)** 에서 **찾아보기...** 를 클릭합니다.  
  
    4.  **개체 찾아보기** 대화 상자에서 **개체 유형 선택** 대화 상자에서 선택한 유형에 대해 사용 가능한 모든 개체를 선택하고 **확인**을 클릭합니다.  
  
    5.  **개체 선택** 대화 상자에서 **확인**을 클릭합니다.  
  
4.  **선택한 유형의 모든 개체...** 를 선택한 경우 **개체 유형 선택** 대화 상자에서 다음 개체 유형 중 일부 또는 전부를 선택합니다. **엔드포인트**, **로그인**, **서버**, **가용성 그룹** 및 **서버 역할**. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 **이름**  
 표에 추가된 각 보안 주체 또는 보안 개체의 이름입니다.  
  
 **형식**  
 각 항목의 유형입니다.  
  
 **명시적 탭**  
 상단 표에서 선택한 보안 개체에 대해 사용 가능한 사용 권한이 나열됩니다. 모든 명시적 사용 권한에 대해 모든 옵션을 사용할 수 있는 것은 아닙니다.  
  
 **사용 권한**  
 사용 권한의 이름입니다.  
  
 **Grantor**  
 사용 권한을 부여한 보안 주체입니다.  
  
 **허용**  
 로그인에 이 사용 권한을 허용하려면 선택하고 사용 권한을 해제하려면 선택을 취소합니다.  
  
 **허용 권한 소유**  
 나열된 사용 권한에 대한 WITH GRANT 옵션 상태를 나타냅니다. 이 부분은 읽기 전용입니다. 이 사용 권한을 적용하려면 [GRANT](/sql/t-sql/statements/grant-transact-sql) 문을 사용합니다.  
  
 **거부**  
 로그인에 이 사용 권한을 거부하려면 선택하고 사용 권한을 해제하려면 선택을 취소합니다.  
  
### <a name="status"></a>상태  
 **상태** 페이지에는 선택한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인에 대해 구성할 수 있는 몇 가지 인증 및 권한 부여 옵션이 나열됩니다.  
  
 이 페이지에서는 다음과 같은 옵션을 사용할 수 있습니다.  
  
 **데이터베이스 엔진 연결 권한**  
 이 설정을 사용할 때 사용자는 선택한 로그인을 보안 개체에 대한 권한을 부여하거나 거부할 수 있는 보안 주체로 간주해야 합니다.  
  
 로그인에 CONNECT SQL 권한을 부여하려면 **허용** 을 선택합니다. 로그인에 CONNECT SQL을 거부하려면 **거부** 를 선택합니다.  
  
 **Login**  
 이 설정을 사용할 때 사용자는 선택한 로그인을 테이블에 있는 레코드로 간주해야 합니다. 여기에 나열된 값의 변경 내용은 레코드에 적용됩니다.  
  
 사용하지 않도록 선택한 로그인은 레코드로 계속 존재합니다. 그러나 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결하려는 경우 로그인이 인증되지 않습니다.  
  
 이 로그인을 사용하거나 사용하지 않도록 선택합니다. 이 옵션은 ALTER LOGIN 문에 ENABLE 또는 DISABLE 옵션을 사용합니다.  
  
 **SQL Server Authentication**  
 **로그인 잠겨 있음** 확인란은 선택한 로그인을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용하여 연결하고 로그인이 잠겨 있는 경우에만 사용할 수 있습니다. 이 설정은 읽기 전용입니다. 잠긴 로그인을 잠금 해제하려면 UNLOCK 옵션을 사용하여 ALTER LOGIN을 실행합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-create-a-login-using-windows-authentication"></a>Windows 인증을 사용하여 로그인을 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- Create a login for SQL Server by specifying a server name and a Windows domain account name.  
  
    CREATE LOGIN [<domainName>\<loginName>] FROM WINDOWS;  
    GO  
  
    ```  
  
#### <a name="to-create-a-login-using-sql-server-authentication"></a>SQL Server 인증을 사용하여 로그인을 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- Creates the user "shcooper" for SQL Server using the security credential "RestrictedFaculty"   
    -- The user login starts with the password "Baz1nga," but that password must be changed after the first login.  
  
    CREATE LOGIN shcooper   
       WITH PASSWORD = 'Baz1nga' MUST_CHANGE,  
       CREDENTIAL = RestrictedFaculty;  
    GO  
  
    ```  
  
 자세한 내용은 [CREATE LOGIN&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)을 참조하세요.  
  
##  <a name="FollowUp"></a> 후속 작업: 로그인을 만든 후 수행할 단계  
 이와 같이 작성한 로그인은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결할 수 있지만 유용한 작업을 수행하는 데 필요한 사용 권한은 가지고 있지 않습니다. 다음 목록에서는 일반적인 로그인 동작 관련 내용이 포함된 링크를 제공합니다.  
  
-   로그인이 역할에 조인하도록 하려면 [역할 조인](join-a-role.md)을 참조하세요.  
  
-   로그인에 데이터베이스 사용 권한을 부여하려면 [데이터베이스 사용자 만들기](../authentication-access/create-a-database-user.md)를 참조하세요.  
  
-   로그인에 사용 권한을 부여하려면 [보안 주체에 사용 권한 부여](grant-a-permission-to-a-principal.md)를 참조하세요.  
  
  
