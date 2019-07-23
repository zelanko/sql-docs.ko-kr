---
title: 역할 조인 | Microsoft 문서
ms.custom: ''
ms.date: 07/14/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- SQL13.SWB.DATABASEUSER.MEMBERSHIP.F1
helpviewer_keywords:
- adding a member to a role
- join a role
ms.assetid: 05c8d10d-5823-46c6-8b1a-81722da6a42b
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 909a8156556cd4a654dcfd6406de2bd45826e31b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990489"
---
# <a name="join-a-role"></a>역할 조인
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 로그인 및 데이터베이스 사용자에 역할을 할당하는 방법에 대해 설명합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 역할을 사용하면 사용 권한을 효율적으로 관리할 수 있습니다. 역할에 사용 권한을 할당하고 사용자와 로그인을 역할에 추가하거나 제거합니다. 역할을 사용하면 각 사용자의 사용 권한을 개별적으로 유지 관리할 필요가 없습니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 다음과 같은 네 가지 역할 유형을 지원합니다.  
  
-   고정 서버 역할  
  
-   사용자 정의 서버 역할  
  
-   고정 데이터베이스 역할  
  
-   사용자 정의 데이터베이스 역할  
  
 고정 역할은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 자동으로 사용할 수 있습니다. 고정 역할은 일반적인 태스크를 수행하는 데 필요한 사용 권한을 가집니다. 고정 역할에 대한 자세한 내용은 다음 링크를 참조하십시오. 사용자 정의 역할은 사용자가 만들며 사용자가 선택한 사용 권한으로 사용자 지정할 수 있습니다. 사용자 정의 역할에 대한 자세한 내용은 다음 링크를 참조하십시오.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **로그인 및 데이터베이스 사용자에 역할을 할당하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   데이터베이스 역할의 이름을 변경하더라도 역할의 ID 번호, 소유자 또는 사용 권한은 변경되지 않습니다.  
  
-   데이터베이스 역할은 sys.database_role_members 및 sys.database_principals 카탈로그 뷰에 표시됩니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 데이터베이스에 대한 **ALTER ANY ROLE** 권한, 역할에 대한 **ALTER** 권한 또는 **db_securityadmin**의 멤버 자격이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-add-a-member-to-a-fixed-server-role"></a>고정 서버 역할에 멤버를 추가하려면  
  
1.  개체 탐색기에서 고정 서버 역할을 편집할 서버를 확장합니다.  
  
2.  **보안** 폴더를 확장합니다.  
  
3.  **서버 역할** 폴더를 확장합니다.  
  
4.  편집할 역할을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
5.  **서버 역할 속성 –** _server\_role\_name_ 대화 상자의 **멤버** 페이지에서 **추가**를 클릭합니다.  
  
6.  **서버 로그인 또는 역할 선택** 대화 상자의 **선택할 개체 이름을 입력하십시오. (예)** 에 이 서버 역할에 추가할 로그인 또는 서버 역할을 입력합니다. 또는 **찾아보기…** 를 클릭하고 **개체 찾아보기** 대화 상자에서 사용 가능한 모든 개체를 선택합니다. **확인**을 클릭하여 **서버 역할 속성 –** _server\_role\_name_ 대화 상자로 돌아갑니다.  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-add-a-member-to-a-user-defined-database-role"></a>사용자 정의 데이터베이스 역할에 멤버를 추가하려면  
  
1.  개체 탐색기에서 사용자 정의 데이터베이스 역할을 편집할 서버를 확장합니다.  
  
2.  **데이터베이스** 폴더를 확장합니다.  
  
3.  사용자 정의 데이터베이스 역할을 편집할 데이터베이스 서버를 확장합니다.  
  
4.  **보안** 폴더를 확장합니다.  
  
5.  **역할** 폴더를 확장합니다.  
  
6.  **서버 역할** 폴더를 확장합니다.  
  
7.  편집할 역할을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
8.  **데이터베이스 역할 속성 –** _database\_role\_name_ 대화 상자의 **일반** 페이지에서 **추가**를 클릭합니다.  
  
9. **데이터베이스 사용자 또는 역할 선택** 대화 상자의 **선택할 개체 이름을 입력하십시오. (예)** 에 이 데이터베이스 역할에 추가할 로그인 또는 데이터베이스 역할을 입력합니다. 또는 **찾아보기…** 를 클릭하고 **개체 찾아보기** 대화 상자에서 사용 가능한 모든 개체를 선택합니다. **확인**을 클릭하여 **데이터베이스 역할 속성 –** _database\_role\_name_ 대화 상자로 돌아갑니다.  
  
10. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-add-a-member-to-a-fixed-server-role"></a>고정 서버 역할에 멤버를 추가하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    ALTER SERVER ROLE diskadmin ADD MEMBER [Domain\Juan] ;  
    GO  
    ```  
  
 자세한 내용은 [ALTER ROLE&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-role-transact-sql.md)을 참조하세요.  
  
#### <a name="to-add-a-member-to-a-user-defined-database-role"></a>사용자 정의 데이터베이스 역할에 멤버를 추가하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    ALTER ROLE Marketing ADD MEMBER [Domain\Juan] ;  
    GO  
    ```  
  
 자세한 내용은 [sp_addrolemember&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [서버 수준 역할](../../../relational-databases/security/authentication-access/server-level-roles.md)   
 [데이터베이스 수준 역할](../../../relational-databases/security/authentication-access/database-level-roles.md)   
 [애플리케이션 역할](../../../relational-databases/security/authentication-access/application-roles.md)  
  
  
