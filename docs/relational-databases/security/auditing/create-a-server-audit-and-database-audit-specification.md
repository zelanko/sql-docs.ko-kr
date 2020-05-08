---
title: 서버 감사 및 데이터베이스 감사 사양 만들기
description: SQL Server Management Studio 또는 T-SQL(Transact-SQL)을 사용하여 SQL Server 감사 및 데이터베이스 감사 사양을 만드는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.sqlaudit.dbaudit.general.f1
helpviewer_keywords:
- audits [SQL Server], creating database specification
- database audit [SQL Server]
ms.assetid: 26ee85de-6e97-4318-b526-900924d96e62
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 55b848cd43e157a9a75670a24aea645c3279f7ea
ms.sourcegitcommit: bfb5e79586fd08d8e48e9df0e9c76d1f6c2004e9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/29/2020
ms.locfileid: "82262071"
---
# <a name="create-a-server-audit-and-database-audit-specification"></a>서버 감사 및 데이터베이스 감사 사양 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 문서에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]에서 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../../includes/tsql-md.md)]을 사용하여 서버 감사 및 데이터베이스 감사 사양을 만드는 방법을 설명합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스의 감사에는 시스템에서 발생하는 추적 이벤트 및 로깅 이벤트가 포함됩니다. *SQL Server Audit* 개체는 사용자가 모니터링하려는 서버 또는 데이터베이스 수준 동작 및 동작 그룹에 대한 하나의 인스턴스를 수집합니다. 감사는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 수준으로 존재합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스별로 여러 개의 감사를 가질 수 있습니다. *데이터베이스 수준 감사 사양* 개체는 감사에 속해 있습니다. 감사의 SQL Server 데이터베이스당 하나의 데이터베이스 감사 사양을 만들 수 있습니다. 자세한 내용은 [SQL Server 감사&#40;데이터베이스 엔진&#41;](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md)을 참조하세요.  
  
 ##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
 데이터베이스 감사 사양은 지정된 데이터베이스에 있는 비보안 개체입니다. 데이터베이스 감사 사양을 처음 만들 때는 사용할 수 없는 상태입니다.  
  
 사용자 데이터베이스에 데이터베이스 감사 사양을 만들거나 사양을 수정할 때 시스템 뷰와 같은 서버 범위 개체에 대한 감사 동작은 포함하지 마세요. 서버 범위 개체를 포함하더라도 감사가 생성됩니다. 그러나 서버 범위 개체가 포함되지는 않으며 별도의 오류도 반환되지 않습니다. 서버 범위 개체를 감사하려면 master 데이터베이스의 데이터베이스 감사 사양을 사용합니다.  
  
 데이터베이스 감사 사양은 해당 사양이 생성된 데이터베이스 내에 있습니다( **TempDB** 시스템 데이터베이스 제외).  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
  
-   ALTER ANY DATABASE AUDIT 권한이 있는 사용자는 데이터베이스 감사 사양을 만들어 모든 감사에 바인딩할 수 있습니다.  
  
-   만들어진 데이터베이스 감사 사양은 CONTROL SERVER 또는 ALTER ANY DATABASE AUDIT 권한이 있는 보안 주체가 볼 수 있습니다. sysadmin 계정도 볼 수 있습니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-create-a-server-audit"></a>서버 감사를 만들려면  
  
1.  개체 탐색기에서 **보안** 폴더를 확장합니다.  
  
2.  **감사** 폴더를 마우스 오른쪽 단추로 클릭하고 **새 감사**를 선택합니다. 자세한 내용은 [서버 감사 및 서버 감사 사양 만들기](../../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)를 참조하세요.  
  
3.  옵션을 선택을 마쳤으면 **확인**을 선택합니다.  

#### <a name="to-create-a-database-level-audit-specification"></a>데이터베이스 수준 감사 사양을 만들려면  
  
1.  개체 탐색기에서 감사 사양을 만들 데이터베이스를 확장합니다.  
  
2.  **보안** 폴더를 확장합니다.  
  
3.  **데이터베이스 감사 사양** 폴더를 마우스 오른쪽 단추로 클릭하고 **새 데이터베이스 감사 사양**을 선택합니다.  
  
     **데이터베이스 감사 사양 만들기** 대화 상자에는 다음과 같은 옵션이 제공됩니다.  
  
     **이름**  
     데이터베이스 감사 사양의 이름입니다. 이름은 새 서버 감사 사양을 만들 때 자동 생성되며 편집할 수 있습니다.  
  
     **감사**  
     기존 서버 감사 개체의 이름입니다. 감사 이름을 입력하거나 목록에서 선택합니다.  
  
     **감사 동작 유형**  
     캡처할 데이터베이스 수준 감사 동작 그룹 및 감사 동작을 지정합니다. 데이터베이스 수준 감사 동작 그룹 및 감사 동작의 목록과 여기에 포함된 이벤트에 대한 설명은 [SQL Server Audit 동작 그룹 및 동작](../../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md)을 참조하세요.  
  
     **개체 스키마**  
     지정된 **개체 이름**에 대한 스키마를 표시합니다.  
  
     **개체 이름**  
     감사할 개체의 이름입니다. 이 옵션은 감사 작업에만 사용할 수 있습니다. 감사 그룹에는 적용되지 않습니다.  
  
     **줄임표(...)**  
     **개체 선택** 대화 상자를 열고 지정된 **감사 동작 유형**에 따라 사용 가능한 개체를 찾아 선택합니다.  
  
     **보안 주체 이름**  
     감사 중인 개체에 대한 감사 필터링의 기준이 되는 계정입니다.  
  
     **줄임표(...)**  
     **개체 선택** 대화 상자를 열고 지정된 **개체 이름**에 따라 사용 가능한 개체를 찾아 선택합니다.  
  
4.  옵션을 선택을 마쳤으면 **확인**을 선택합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-create-a-server-audit"></a>서버 감사를 만들려면  
  
1.  개체 탐색기에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 선택합니다.  
  
3.  다음 예를 쿼리 창에 붙여넣은 후 **실행**을 선택합니다.  
  
    ```  
    USE master ;  
    GO  
    -- Create the server audit.   
    CREATE SERVER AUDIT Payrole_Security_Audit  
        TO FILE ( FILEPATH =   
    'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA' ) ;   
    GO  
    -- Enable the server audit.   
    ALTER SERVER AUDIT Payrole_Security_Audit   
    WITH (STATE = ON) ;  
    ```  
  
#### <a name="to-create-a-database-level-audit-specification"></a>데이터베이스 수준 감사 사양을 만들려면  
  
1.  개체 탐색기에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 선택합니다.  
  
3.  다음 예를 쿼리 창에 붙여넣은 후 **실행**을 선택합니다. 이 예에서는 `Audit_Pay_Tables`이라는 데이터베이스 감사 사양을 만듭니다. 이전 섹션에서 정의된 서버 감사를 기반으로 `HumanResources.EmployeePayHistory` 테이블에 대해 `dbo` 사용자에 의해 수행된 SELECT 및 INSERT 문을 감사합니다.  
  
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
  
 자세한 내용은 [CREATE SERVER AUDIT&#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-audit-transact-sql.md) 및 [CREATE DATABASE AUDIT SPECIFICATION&#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-audit-specification-transact-sql.md)을 참조하세요.  
  
  
