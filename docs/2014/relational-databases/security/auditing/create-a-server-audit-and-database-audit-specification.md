---
title: 서버 감사 및 데이터베이스 감사 사양 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.sqlaudit.dbaudit.general.f1
helpviewer_keywords:
- audits [SQL Server], creating database specification
- database audit [SQL Server]
ms.assetid: 26ee85de-6e97-4318-b526-900924d96e62
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: b4ee2d4ba29e6abb8536ea9a6a1173df8cef9336
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43025433"
---
# <a name="create-a-server-audit-and-database-audit-specification"></a>서버 감사 및 데이터베이스 감사 사양 만들기
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 서버 감사 및 데이터베이스 감사 사양을 만드는 방법에 대해 설명합니다.  
  
 *인스턴스 또는* 데이터베이스 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 감사 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에는 시스템에서 발생하는 추적 이벤트 및 로깅 이벤트가 포함됩니다. *SQL Server Audit* 개체는 사용자가 모니터링하려는 서버 또는 데이터베이스 수준 동작 및 동작 그룹에 대한 하나의 인스턴스를 수집합니다. 감사는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 수준으로 존재합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스별로 여러 개의 감사를 가질 수 있습니다. *데이터베이스 수준 감사 사양* 개체는 감사에 속해 있습니다. 감사의 SQL Server 데이터베이스당 하나의 데이터베이스 감사 사양을 만들 수 있습니다. 자세한 내용은 [SQL Server Audit&#40;데이터베이스 엔진&#41;](sql-server-audit-database-engine.md)을 참조하세요.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **서버 감사 및 데이터베이스 감사 사양을 만들려면:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
 데이터베이스 감사 사양은 지정된 데이터베이스에 있는 비보안 개체입니다. 데이터베이스 감사 사양을 처음 만들 때는 사용할 수 없는 상태입니다.  
  
 사용자 데이터베이스에 데이터베이스 감사 사양을 만들거나 사양을 수정할 때 시스템 뷰와 같은 서버 범위 개체에 대한 감사 동작은 포함하지 마세요. 서버 범위 개체를 포함하더라도 감사가 생성됩니다. 그러나 서버 범위 개체가 포함되지는 않으며 별도의 오류도 반환되지 않습니다. 서버 범위 개체를 감사하려면 master 데이터베이스의 데이터베이스 감사 사양을 사용합니다.  
  
 데이터베이스 감사 사양은 해당 사양이 생성된 데이터베이스 내에 있습니다(`tempdb` 시스템 데이터베이스 제외).  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
  
-   ALTER ANY DATABASE AUDIT 권한이 있는 사용자는 데이터베이스 감사 사양을 만들어 모든 감사에 바인딩할 수 있습니다.  
  
-   생성된 데이터베이스 감사 사양은 CONTROL SERVER, ALTER ANY DATABASE AUDIT 권한이 있는 보안 주체나 sysadmin 계정이 볼 수 있습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-create-a-server-audit"></a>서버 감사를 만들려면  
  
1.  개체 탐색기에서 **보안** 폴더를 확장합니다.  
  
2.  **감사** 폴더를 마우스 오른쪽 단추로 클릭하고 **새 감사...** 를 선택합니다. 자세한 내용은 [서버 감사 및 서버 감사 사양 만들기](create-a-server-audit-and-server-audit-specification.md)을 참조하세요.  
  
3.  옵션 선택을 마쳤으면 **확인**을 클릭합니다.  
  
#### <a name="to-create-a-database-level-audit-specification"></a>데이터베이스 수준 감사 사양을 만들려면  
  
1.  개체 탐색기에서 감사 사양을 만들 데이터베이스를 확장합니다.  
  
2.  **보안** 폴더를 확장합니다.  
  
3.  **데이터베이스 감사 사양** 폴더를 마우스 오른쪽 단추로 클릭하고 **새 데이터베이스 감사 사양...** 을 선택합니다.  
  
     **데이터베이스 감사 사양 만들기** 대화 상자에는 다음과 같은 옵션이 제공됩니다.  
  
     **이름**  
     데이터베이스 감사 사양의 이름입니다. 새 서버 감사 사양을 만들 때 자동 생성되지만 편집할 수 있습니다.  
  
     **감사**  
     기존 데이터베이스 감사의 이름입니다. 감사 이름을 입력하거나 목록에서 선택합니다.  
  
     **감사 동작 유형**  
     캡처할 데이터베이스 수준 감사 동작 그룹 및 감사 동작을 지정합니다. 데이터베이스 수준 감사 동작 그룹 및 감사 동작의 목록과 여기에 포함된 이벤트에 대한 설명은 [SQL Server Audit 동작 그룹 및 동작](sql-server-audit-action-groups-and-actions.md)을 참조하세요.  
  
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
  
4.  옵션 선택을 마쳤으면 **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-create-a-server-audit"></a>서버 감사를 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE master ;  
    GO  
    -- Create the server audit.   
    CREATE SERVER AUDIT Payrole_Security_Audit  
        TO FILE ( FILEPATH =   
    'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA' ) ;   
    GO  
    -- Enable the server audit.   
    ALTER SERVER AUDIT Payrole_Security_Audit   
    WITH (STATE = ON) ;  
    ```  
  
#### <a name="to-create-a-database-level-audit-specification"></a>데이터베이스 수준 감사 사양을 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 위에 정의된 서버 감사를 기반으로 `Audit_Pay_Tables` 테이블에 대해 `dbo` 사용자가 SELECT 및 INSERT 문을 감사하는 `HumanResources.EmployeePayHistory`이라는 데이터베이스 감사 사양을 만듭니다.  
  
    ```  
    USE AdventureWorks2012 ;   
    GO  
    -- Create the database audit specification.   
    CREATE DATABASE AUDIT SPECIFICATION Audit_Pay_Tables  
    FOR SERVER AUDIT Payrole_Security_Audit  
    ADD (SELECT , INSERT  
         ON HumanResources.EmployeePayHistory BY dbo )   
    WITH (STATE = ON) ;   
    GO  
  
    ```  
  
 자세한 내용은 [CREATE SERVER AUDIT&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-server-audit-transact-sql) 및 [CREATE DATABASE AUDIT SPECIFICATION&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-database-audit-specification-transact-sql)을 참조하세요.  
  
  
