---
title: 데이터베이스 사용자 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.DATABASEUSER.GENERAL.F1
- sql12.swb.user.securables.f1
helpviewer_keywords:
- database users, creating
- creating users with Management Studio
- mapping users
- users [SQL Server], creating
- database user additions [SQL Server]
- database users, mapping
- CREATE USER [Management Studio]
- users [SQL Server], adding
- mapping database users
ms.assetid: 782798d3-9552-4514-9f58-e87be4b264e4
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 8d99b7e43a2218c79538fc2e7245733dec44e39f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68211964"
---
# <a name="create-a-database-user"></a>데이터베이스 사용자 만들기
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 로그인에 매핑되는 데이터베이스 사용자를 만드는 방법에 대해 설명합니다. 데이터베이스 사용자는 데이터베이스 연결 시의 로그인 ID입니다. 데이터베이스 사용자는 원하는 경우 로그인과 같은 이름을 사용할 수 있습니다. 이 항목에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 로그인이 이미 있다고 가정합니다. 로그인을 만드는 방법에 대 한 자세한 내용은 [로그인 만들기](create-a-login.md)를 참조 하세요.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [배경](#Restrictions)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 데이터베이스를 만들려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="background"></a><a name="Restrictions"></a> 배경  
 사용자는 데이터베이스 수준의 보안 주체입니다. 데이터베이스에 연결하려면 로그인을 데이터베이스 사용자로 매핑해야 합니다. 로그인을 다른 데이터베이스에 다른 사용자로 매핑할 수 있지만 각 데이터베이스에서 한 명의 사용자로만 매핑할 수 있습니다. 부분적으로 포함된 데이터베이스에서는 로그인을 포함하지 않는 사용자를 만들 수 있습니다. 포함된 데이터베이스 사용자에 대한 자세한 내용은 [CREATE USER&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)를 참조하세요. 데이터베이스에서 게스트 사용자가 설정된 경우 데이터베이스 사용자에 매핑되지 않은 로그인이 게스트 사용자로 데이터베이스에 진입할 수 있습니다.  
  
> [!IMPORTANT]  
>  게스트 사용자는 보통 사용하지 않도록 설정됩니다. 반드시 필요한 경우가 아니면 게스트 사용자를 사용하도록 설정하지 마세요.  
  
 보안 주체는 사용 권한을 사용자에게 부여할 수 있습니다. 사용자의 범위는 데이터베이스입니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스에서 특정 데이터베이스에 연결하려면 로그인을 데이터베이스 사용자에 매핑해야 합니다. 이 경우 로그인이 아니라 데이터베이스 내의 사용 권한이 데이터베이스 사용자에게 부여되며 거부됩니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 데이터베이스에 대한 `ALTER ANY USER` 권한이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
##### <a name="to-create-a-database-user"></a>데이터베이스 사용자를 만들려면  
  
1.  개체 탐색기에서 **데이터베이스** 폴더를 확장합니다.  
  
2.  새 데이터베이스 사용자를 만들 데이터베이스를 확장합니다.  
  
3.  **보안** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **새로 만들기**를 가리킨 다음 **사용자 ...** 를 선택 합니다.  
  
4.  **데이터베이스 사용자-신규** 대화 상자의 **일반** 페이지에 있는 **사용자 유형** 목록에서 로그인을 사용 하는 **sql 사용자**, 로그인을 사용 **하지 않는 sql 사용자**, **인증서에 매핑된**사용자, **비대칭 키에 매핑된 사용자**또는 **Windows 사용자**의 사용자 유형 중 하나를 선택 합니다.  
  
5.  **사용자 이름** 상자에 새 사용자의 이름을 입력합니다. **사용자 유형** 목록에서 **Windows 사용자**를 선택한 경우 줄임표 **(…)** 를 클릭하여 **사용자 또는 그룹 선택** 대화 상자를 열 수도 있습니다.  
  
6.  **로그인 이름** 상자에 사용자의 로그인을 입력합니다. 또는 줄임표 **(...)** 를 클릭 하 여 **로그인 선택** 대화 상자를 엽니다. **로그인 이름** 은 **사용자 유형** 목록에서 **로그인을 사용하는 SQL 사용자** 또는 **Windows 사용자** 를 선택한 경우 사용할 수 있습니다.  
  
7.  **기본 스키마** 상자에서 이 사용자가 만든 개체를 소유할 스키마를 지정합니다. 또는 줄임표 **(...)** 를 클릭 하 여 **스키마 선택** 대화 상자를 엽니다. **기본 스키마** 는 **사용자 유형**목록에서 **로그인을 사용하는 SQL 사용자**, **로그인을 사용하지 않는 SQL 사용자** 또는 **Windows 사용자** 를 선택한 경우 사용할 수 있습니다.  
  
8.  **인증서 이름** 상자에 데이터베이스 사용자에 대해 사용할 인증서를 입력합니다. 또는 줄임표 **(...)** 를 클릭 하 여 **인증서 선택** 대화 상자를 엽니다. **인증서 이름** 은 **사용자 유형** 목록에서 **인증서에 매핑된 사용자** 를 선택한 경우 사용할 수 있습니다.  
  
9. **비대칭 키 이름**  상자에 데이터베이스 사용자에 대해 사용할 키를 입력합니다. 또는 줄임표 **(...)** 를 클릭 하 여 **비대칭 키 선택** 대화 상자를 엽니다. **비대칭 키 이름** 은 **사용자 유형** 목록에서 **비대칭 키에 매핑된 사용자** 를 선택한 경우 사용할 수 있습니다.  
  
10. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="additional-options"></a>추가 옵션  
 **데이터베이스 사용자-신규** 대화 상자에는 **소유한 스키마**, **멤버 자격**, **보안 개체**및 **확장 속성**의 네 가지 추가 페이지에 대 한 옵션도 제공 됩니다.  
  
-   **소유한 스키마** 페이지에는 새 데이터베이스 사용자가 소유할 수 있는 모든 가능한 스키마가 나열됩니다. 데이터베이스 사용자로부터 스키마를 추가하거나 제거하려면 **이 사용자가 소유한 스키마**아래에서 스키마 옆에 있는 확인란을 선택하거나 선택을 취소합니다.  
  
-   **멤버 자격** 페이지에는 새 데이터베이스 사용자가 소유할 수 있는 모든 가능한 데이터베이스 멤버 자격 역할이 나열됩니다. 데이터베이스 사용자로부터 역할을 추가하거나 제거하려면 **데이터베이스 역할 멤버 자격**아래에서 역할 옆에 있는 확인란을 선택하거나 선택을 취소합니다.  
  
-   **보안 개체** 페이지에는 사용 가능한 모든 보안 개체와 이러한 보안 개체에서 로그인에 부여할 수 있는 권한이 나열됩니다.  
  
-   **확장 속성** 페이지에서는 데이터베이스 사용자에 사용자 지정 속성을 추가할 수 있습니다. 이 페이지에서는 다음과 같은 옵션을 선택할 수 있습니다.  
  
     **Database**  
     선택한 데이터베이스의 이름을 표시합니다. 이 필드는 읽기 전용입니다.  
  
     **데이터 정렬**  
     선택한 데이터베이스에 사용된 데이터 정렬을 표시합니다. 이 필드는 읽기 전용입니다.  
  
     **속성**  
     개체의 확장 속성을 확인하거나 지정합니다. 각 확장 속성은 개체에 연결된 메타데이터의 이름/값 쌍으로 이루어져 있습니다.  
  
     **줄임표(...)**  
     **확장 속성 값** 대화 상자를 열려면 **값** 뒤에 있는 줄임표 **(...)** 를 클릭합니다. 더 큰 범위에서 확장 속성 값을 입력하거나 확인할 수 있습니다. 자세한 내용은 [확장 속성 값 대화 상자](../../databases/value-for-extended-property-dialog-box.md)를 참조하십시오.  
  
     **Delete**  
     선택한 확장 속성을 제거합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-create-a-database-user"></a>데이터베이스 사용자를 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- Creates the login AbolrousHazem with password '340$Uuxwp7Mcxo7Khy'.  
    CREATE LOGIN AbolrousHazem   
        WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';  
    GO  
  
    -- Creates a database user for the login created above.  
    CREATE USER AbolrousHazem FOR LOGIN AbolrousHazem;  
    GO  
    ```  
  
 자세한 내용은 [CREATE USER&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [보안 주체&#40;데이터베이스 엔진&#41;](principals-database-engine.md)  
  
  
