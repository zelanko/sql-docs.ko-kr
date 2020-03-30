---
title: 서버 감사 및 서버 감사 사양 만들기
description: SSMS(SQL Server Management Studio) 또는 T-SQL(Transact-SQL)을 사용하여 SQL Server 감사 및 서버 감사 사양을 만드는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 10/16/2019
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.SWB.SQLAUDIT.FILTER.F1
- sql13.swb.sqlaudit.general.f1
- sql13.swb.sqlaudit.srvaudit.general.f1
helpviewer_keywords:
- server audit [SQL Server]
- audits [SQL Server], specification
ms.assetid: 6624b1ab-7ec8-44ce-8292-397edf644394
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: dff79a428833e365d0ca55b287da6154f66d9966
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "75952466"
---
# <a name="create-a-server-audit-and-server-audit-specification"></a>서버 감사 및 서버 감사 사양 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 서버 감사 및 서버 감사 사양을 만드는 방법에 대해 설명합니다. *인스턴스 또는* 데이터베이스 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 감사 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에는 시스템에서 발생하는 추적 이벤트 및 로깅 이벤트가 포함됩니다. *SQL Server Audit* 개체는 사용자가 모니터링하려는 서버 또는 데이터베이스 수준 동작 및 동작 그룹에 대한 하나의 인스턴스를 수집합니다. 감사는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 수준으로 존재합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스별로 여러 개의 감사를 가질 수 있습니다. *서버 감사 사양* 개체는 감사에 속해 있습니다. 서버 감사 사양과 감사는 모두 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 범위에서 생성되므로 감사당 하나의 서버 감사 사양을 만들 수 있습니다. 자세한 내용은 [SQL Server Audit&#40;데이터베이스 엔진&#41;](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md)을 참조하세요.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 서버 감사 및 서버 감사 사양을 만듭니다.**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   감사가 있어야 이에 대한 서버 감사 사양을 만들 수 있습니다. 서버 감사 사양을 처음 만들 때는 사용할 수 없는 상태입니다.  
  
-   CREATE SERVER AUDIT 문은 트랜잭션 범위 내에 있습니다. 트랜잭션이 롤백되면 이 문도 롤백됩니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
  
-   서버 감사를 생성, 변경 또는 삭제하려면 보안 주체에게 ALTER ANY SERVER AUDIT 또는 CONTROL SERVER 권한이 있어야 합니다.  
  
-   ALTER ANY SERVER AUDIT 권한이 있는 사용자는 서버 감사 사양을 만들어 모든 감사에 바인딩할 수 있습니다.  
  
-   만들어진 서버 감사 사양은 CONTROL SERVER 또는 ALTER ANY SERVER AUDIT 권한이 있는 보안 주체, sysadmin 계정 또는 감사에 대한 명시적인 액세스가 있는 보안 주체가 볼 수 있습니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-create-a-server-audit"></a>서버 감사를 만들려면  
  
1.  개체 탐색기에서 **보안** 폴더를 확장합니다.  
  
2.  **감사** 폴더를 마우스 오른쪽 단추로 클릭하고 **새 감사...** 를 선택합니다.  
  
     **감사 만들기** 대화 상자의 **일반** 페이지에는 다음과 같은 옵션이 제공됩니다.  
  
     **감사 이름**  
     감사의 이름입니다. 이는 새 감사를 만들 때 자동으로 생성되지만 편집할 수 있습니다.  
  
     **큐 지연(밀리초)**  
     감사 동작이 강제 처리되기 전까지 허용되는 시간(밀리초)을 지정합니다.  값이 0인 경우 동기 배달을 나타냅니다. 기본 최소값은 **1000** (1초)입니다. 최대값은 2,147,483,647로 2,147,483.647초 또는 24일, 20시간, 31분, 23.647초에 해당합니다.  
  
     **감사 로그 실패 시:**  
     **계속**  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 작업을 계속합니다. 감사 레코드는 보존되지 않습니다. 감사는 계속해서 이벤트 기록을 시도하며 실패 조건이 해결되면 재개됩니다. **계속** 옵션을 선택하면 감사되지 않는 작업이 허용되어 보안 정책을 위반할 수 있습니다. 전체 감사를 유지 관리하는 것보다 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 의 작업을 계속하는 것이 더 중요하면 이 옵션을 선택하세요. 이 옵션이 기본 옵션입니다.  
  
     **서버 종료**  
     대상에 쓰기 작업을 수행하는 서버 인스턴스가 감사 대상에 데이터를 쓰지 못할 경우 서버를 강제 종료합니다. 이 함수를 실행하는 로그인에는 **SHUTDOWN** 권한이 있어야 합니다. 이 권한이 없으면 이 함수가 실패하고 오류 메시지가 표시됩니다. 감사된 이벤트가 발생하지 않습니다. 감사 실패로 인해 시스템 무결성 또는 보안이 손상될 수 있는 경우 이 옵션을 선택하세요.  
  
     **작업 실패**  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 감사에서 감사 로그에 쓸 수 없는 경우 이 옵션을 선택하면 정상적인 경우에는 감사된 이벤트를 발생시키는 데이터베이스 동작이 실패하며, 감사된 이벤트가 발생하지 않습니다. 감사된 이벤트를 발생시키지 않는 동작은 계속할 수 있습니다. 감사는 계속해서 이벤트 기록을 시도하며 실패 조건이 해결되면 재개됩니다. [!INCLUDE[ssDE](../../../includes/ssde-md.md)]에 대한 모든 권한을 얻는 것보다 전체 감사를 유지 관리하는 것이 더 중요하면 이 옵션을 선택하십시오.  
  
    > [!IMPORTANT]  
    >  감사가 실패한 상태여도 관리자 전용 연결에서는 감사된 이벤트를 계속 수행할 수 있습니다.  
  
     **감사 대상** 목록  
     데이터를 감사할 대상을 지정합니다. 이진 파일, Windows 애플리케이션 로그, Windows 보안 로그 등이 감사 대상이 될 수 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가 Windows 보안 로그에 쓸 수 없습니다. 자세한 내용은 [보안 로그에 SQL Server Audit 이벤트 쓰기](../../../relational-databases/security/auditing/write-sql-server-audit-events-to-the-security-log.md)를 참조하세요.  
  
     **파일 경로**  
     **감사 대상** 이 파일인 경우 감사 데이터를 쓸 폴더의 위치를 지정합니다.  
  
     **줄임표(...)**  
     **폴더 찾기 –** _server\_name_ 대화 상자를 열어 파일 경로를 지정하거나 감사 파일이 기록되는 폴더를 만듭니다.  
  
     **감사 파일의 최대 제한:**  
     **최대 롤오버 파일**  
     감사 파일의 최대 수에 도달하면 가장 오래된 감사 파일을 새 파일 내용으로 덮어쓰도록 지정합니다.  
  
     **최대 파일**  
     최대 감사 파일 수에 도달하면 추가 감사 이벤트를 생성하는 동작이 실패하며 오류가 발생하도록 지정합니다.  
  
     **무제한** 확인란  
     **최대 롤오버 파일** 아래의 **무제한** 확인란이 선택된 경우 만들려는 감사 파일 수에 대한 제한이 없습니다. **무제한** 확인란은 기본적으로 선택되며 **최대 롤오버 파일** 및 **최대 파일** 선택 사항에 모두 적용됩니다.  
  
     **파일 수** 상자  
     만들려는 감사 파일 수를 최대 2,147,483,647까지 지정합니다. 이 옵션은 **무제한** 을 선택 취소한 경우에만 사용할 수 있습니다.  
  
     **최대 파일 크기**  
     MB(메가바이트), GB(기가바이트) 또는 TB(테라바이트) 단위로 감사 파일의 최대 크기를 지정합니다. 최대 2,147,483,647TB의 숫자를 지정할 수 있습니다. **무제한** 확인란을 선택하면 파일 크기에 대한 제한이 없습니다. **무제한** 확인란은 기본적으로 선택됩니다.  
  
     **디스크 공간 예약** 확인란  
     지정된 최대 파일 크기와 동일한 공간이 디스크에 미리 할당되도록 지정합니다. 이 설정은 **최대 파일 크기** 아래에서 **무제한** 을 선택하지 않은 경우에만 사용할 수 있습니다. 이 확인란은 기본적으로 선택되지 않습니다.  
  
3.  또는 **필터** 페이지에서 조건자를 입력하거나 `WHERE` 절을 서버 감사에 입력하여 **일반** 페이지에서 사용할 수 없는 추가 옵션을 지정할 수 있습니다. 조건자를 괄호로 묶습니다. 예: `(object_name = 'EmployeesTable')`  
  
4.  옵션 선택을 마쳤으면 **확인**을 클릭합니다.  
  
#### <a name="to-create-a-server-audit-specification"></a>서버 감사 사양을 만들려면  
  
1.  개체 탐색기에서 더하기 기호를 클릭하여 **보안** 폴더를 확장합니다.  
  
2.  **서버 감사 사양** 폴더를 마우스 오른쪽 단추로 클릭하고 **새 서버 감사 사양...** 을 선택합니다.  
  
     **서버 감사 사양 만들기** 대화 상자에는 다음과 같은 옵션이 제공됩니다.  
  
     **이름**  
     서버 감사 사양의 이름입니다. 새 서버 감사 사양을 만들 때 자동 생성되지만 편집할 수 있습니다.  
  
     **감사**  
     기존 서버 감사의 이름입니다. 감사 이름을 입력하거나 목록에서 선택합니다.  
  
     **감사 동작 유형**  
     캡처할 서버 수준 감사 동작 그룹 및 감사 동작을 지정합니다. 서버 수준 감사 동작 그룹 및 감사 동작의 목록과 여기에 포함된 이벤트에 대한 설명은 [SQL Server Audit 동작 그룹 및 동작](../../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md)을 참조하세요.  
  
     **개체 스키마**  
     지정된 **개체 이름**에 대한 스키마를 표시합니다.  
  
     **개체 이름**  
     감사할 개체의 이름입니다. 이 이름은 감사 동작에만 사용할 수 있으며 감사 그룹에는 적용되지 않습니다.  
  
     **줄임표(...)**  
     **개체 선택** 대화 상자를 열고 지정된 **감사 동작 유형**에 따라 사용 가능한 개체를 찾아 선택합니다.  
  
     **보안 주체 이름**  
     감사 중인 개체에 대한 감사 필터링의 기준이 되는 계정입니다.  
  
     **줄임표(...)**  
     **개체 선택** 대화 상자를 열고 지정된 **개체 이름**에 따라 사용 가능한 개체를 찾아 선택합니다.  
  
3.  작업을 마쳤으면 **확인**을 클릭합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-create-a-server-audit"></a>서버 감사를 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- Creates a server audit called "HIPAA_Audit" with a binary file as the target and no options.  
    CREATE SERVER AUDIT HIPAA_Audit  
        TO FILE ( FILEPATH ='\\SQLPROD_1\Audit\' );  
    ```  
  
#### <a name="to-create-a-server-audit-specification"></a>서버 감사 사양을 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    /*Creates a server audit specification called "HIPAA_Audit_Specification" that audits failed logins for the SQL Server audit "HIPAA_Audit" created above.  
    */  
  
    CREATE SERVER AUDIT SPECIFICATION HIPAA_Audit_Specification  
    FOR SERVER AUDIT HIPAA_Audit  
        ADD (FAILED_LOGIN_GROUP);  
    GO  
    -- Enables the audit.   
  
    ALTER SERVER AUDIT HIPAA_Audit  
    WITH (STATE = ON);  
    GO  
    ```  
  
 자세한 내용은 [CREATE SERVER AUDIT&#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-audit-transact-sql.md) 및 [CREATE SERVER AUDIT SPECIFICATION&#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-audit-specification-transact-sql.md)을 참조하세요.  
  
  
