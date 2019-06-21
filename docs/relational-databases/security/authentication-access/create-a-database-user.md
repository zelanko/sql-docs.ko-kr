---
title: 데이터베이스 사용자 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.user.securables.f1
- SQL13.SWB.DATABASEUSER.GENERAL.F1
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 11e155be4678c2cb57b9b551b412570e4578eb46
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62715858"
---
# <a name="create-a-database-user"></a>데이터베이스 사용자 만들기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  이 항목에서는 가장 일반적인 데이터베이스 사용자 유형을 만드는 방법을 설명합니다. 사용자 유형에는 다음과 같이 11가지가 있습니다. 전체 목록은 [CREATE USER&#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md) 항목에서 제공됩니다. 모든 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 변형에서 데이터베이스 사용자를 지원하지만 반드시 모든 사용자 유형을 지원하는 것은 아닙니다.  
  
 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../../includes/tsql-md.md)]을 사용하여 데이터베이스 사용자를 만들 수 있습니다.  
  
##  <a name="Understanding"></a> 사용자 유형 이해  
 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 에서는 데이터베이스 사용자를 만들 때 6가지 옵션을 표시합니다. 다음 그래픽은 녹색 상자에 6가지 옵션을 보여 주고 나타내는 정보를 표시합니다.  
  
 ![TypesOfUsers](../../../relational-databases/security/authentication-access/media/typesofusers.png "TypesOfUsers")  
  
### <a name="selecting-the-type-of-user"></a>사용자 유형 선택  
 **로그인 또는 로그인에 매핑되지 않은 사용자**  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]을 처음 사용하는 경우 만들 사용자 유형을 결정하기 어려울 수 있습니다. 먼저 데이터베이스에 액세스해야 하는 개인 또는 그룹이 로그인을 가지고 있는지 자문해 봅니다. master 데이터베이스의 로그인은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 을 관리하는 사용자와 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스에서 여러 또는 모든 데이터베이스에 액세스해야 하는 사용자에게 일반적입니다. 이런 상황에서는 **로그인을 사용하는 SQL 사용자**를 만듭니다. 데이터베이스 사용자는 데이터베이스 연결 시의 로그인 ID입니다. 데이터베이스 사용자는 원하는 경우 로그인과 같은 이름을 사용할 수 있습니다. 이 항목에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 로그인이 이미 있다고 가정합니다. 로그인을 만드는 방법은 [로그인 만들기](../../../relational-databases/security/authentication-access/create-a-login.md)를 참조하세요.  
  
 데이터베이스에 액세스해야 하는 개인 또는 그룹에 로그인이 없고 하나 또는 일부 데이터베이스에만 액세스해야 하는 경우 **Windows 사용자** 또는 **암호를 사용하는 SQL 사용자**를 만듭니다. 포함된 데이터베이스 사용자라고도 하며 master 데이터베이스의 로그인과 연결되지 않습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스 간에 데이터베이스를 쉽게 이동할 수 있기를 원하는 경우 매우 적합합니다. [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)]에서 이 옵션을 사용하려면 먼저 관리자가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대해 포함된 데이터베이스를 사용하도록 설정하고 포함할 데이터베이스가 설정되어야 합니다. 자세한 내용은 [포함된 데이터베이스 사용자 - 이식 가능한 데이터베이스 만들기](../../../relational-databases/security/contained-database-users-making-your-database-portable.md)를 참조하세요.  
  
> **중요!** 포함된 데이터베이스 사용자로 연결할 때 연결 문자열의 일부로 데이터베이스 이름을 제공해야 합니다. [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]에서 데이터베이스를 지정하려면 **연결 대상** 대화 상자에서 **옵션**을 클릭하고 **연결 속성** 탭을 클릭합니다.  
  
 연결 중인 개인이 Windows에서 인증할 수 없는 경우 **SQL Server 인증 로그인** 에 따라 **암호를 사용하는 SQL 사용자** 또는 **로그인을 사용하는 SQL 사용자**를 선택합니다. 조직에 속하지 않은 개인(예: 고객)이 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결하는 경우 일반적입니다.  
  
> **팁** 조직에 속한 개인의 경우 추가 암호를 기억하지 않아도 되며 Windows 인증에서 Kerberos와 같은 추가 보안 기능을 제공하므로 Windows 인증이 보다 적합합니다.  
  
##  <a name="Restrictions"></a> 배경  
 사용자는 데이터베이스 수준의 보안 주체입니다. 데이터베이스에 연결하려면 로그인을 데이터베이스 사용자로 매핑해야 합니다. 로그인을 다른 데이터베이스에 다른 사용자로 매핑할 수 있지만 각 데이터베이스에서 한 명의 사용자로만 매핑할 수 있습니다. 부분적으로 포함된 데이터베이스에서는 로그인을 포함하지 않는 사용자를 만들 수 있습니다. 포함된 데이터베이스 사용자에 대한 자세한 내용은 [CREATE USER&#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md)를 참조하세요. 데이터베이스에서 게스트 사용자가 설정된 경우 데이터베이스 사용자에 매핑되지 않은 로그인이 게스트 사용자로 데이터베이스에 진입할 수 있습니다.  
  
> **중요!** 게스트 사용자는 보통 사용하지 않도록 설정됩니다. 반드시 필요한 경우가 아니면 게스트 사용자를 사용하도록 설정하지 마세요.  
  
 보안 주체는 사용 권한을 사용자에게 부여할 수 있습니다. 사용자의 범위는 데이터베이스입니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스에서 특정 데이터베이스에 연결하려면 로그인을 데이터베이스 사용자에 매핑해야 합니다. 이 경우 로그인이 아니라 데이터베이스 내의 사용 권한이 데이터베이스 사용자에게 부여되며 거부됩니다.  
  
##  <a name="Permissions"></a> 사용 권한  
 데이터베이스에 대한 **ALTER ANY USER** 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SSMS를 사용하여 사용자 만들기  
  
 
1.  개체 탐색기에서 **데이터베이스** 폴더를 확장합니다.  
  
2.  새 데이터베이스 사용자를 만들 데이터베이스를 확장합니다.  
  
3.  **보안** 폴더를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 가리킨 후 **사용자...** 를 선택합니다.  
  
4.  **데이터베이스 사용자 – 신규** 대화 상자의 **일반** 페이지에 있는 **사용자 유형** 목록에서 다음 사용자 유형 중 하나를 선택합니다.  
  
    -   **로그인을 사용하는 SQL 사용자**  
  
    -   **암호를 사용하는 SQL 사용자**  
  
    -   **로그인을 사용하지 않는 SQL 사용자**  
  
    -   **인증서에 매핑된 사용자**  
  
    -   **비대칭 키에 매핑된 사용자**  
  
    -   **Windows 사용자**  
  
5.  옵션을 선택하면 대화 상자의 나머지 옵션이 변경될 수 있습니다. 일부 옵션은 특정 유형의 데이터베이스 사용자에게만 적용됩니다. 일부 옵션 비워둘 수 있으며 기본값을 사용합니다.  
  
     **사용자 이름**  
     새 사용자의 이름을 입력합니다. **사용자 유형** 목록에서 **Windows 사용자**를 선택한 경우 줄임표 **(…)** 를 클릭하여 **사용자 또는 그룹 선택** 대화 상자를 열 수도 있습니다.  
  
     **로그인 이름**  
     사용자에 대한 로그인을 입력합니다. 또는 줄임표 **(...)** 를 클릭하여 **로그인 선택** 대화 상자를 엽니다. **로그인 이름** 은 **사용자 유형** 목록에서 **로그인을 사용하는 SQL 사용자** 또는 **Windows 사용자** 를 선택한 경우 사용할 수 있습니다.  
  
     **암호** 및 **암호 확인**  
     데이터베이스에서 인증할 사용자의 암호를 입력합니다.  
  
     **기본 언어**  
     사용자의 기본 언어를 입력합니다.  
  
     **기본 스키마**  
     이 사용자가 만든 개체를 소유할 스키마를 입력합니다. 또는 줄임표 **(...)** 를 클릭하여 **스키마 선택** 대화 상자를 엽니다. **기본 스키마** 는 **사용자 유형**목록에서 **로그인을 사용하는 SQL 사용자**, **로그인을 사용하지 않는 SQL 사용자** 또는 **Windows 사용자** 를 선택한 경우 사용할 수 있습니다.  
  
     **인증서 이름**  
     데이터베이스 사용자에 대해 사용할 인증서를 입력합니다. 또는 줄임표 **(...)** 를 클릭하여 **인증서 선택** 대화 상자를 엽니다. **인증서 이름** 은 **사용자 유형** 목록에서 **인증서에 매핑된 사용자** 를 선택한 경우 사용할 수 있습니다.  
  
     **비대칭 키 이름**  
     데이터베이스 사용자에 대해 사용할 키를 입력합니다. 또는 줄임표 **(...)** 를 클릭하여 **비대칭 키 선택** 대화 상자를 엽니다. **비대칭 키 이름** 은 **사용자 유형** 목록에서 **비대칭 키에 매핑된 사용자** 를 선택한 경우 사용할 수 있습니다.  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="additional-options"></a>추가 옵션  
 **데이터베이스 사용자 - 신규** 대화 상자에서는 다음 네 가지 추가 페이지에 대한 옵션도 제공합니다. **소유한 스키마**, **멤버 자격**, **보안 개체** 및 **확장 속성**의 네 가지 추가 페이지에 대한 옵션이 제공됩니다.  
  
-   **소유한 스키마** 페이지에는 새 데이터베이스 사용자가 소유할 수 있는 모든 가능한 스키마가 나열됩니다. 데이터베이스 사용자로부터 스키마를 추가하거나 제거하려면 **이 사용자가 소유한 스키마**아래에서 스키마 옆에 있는 확인란을 선택하거나 선택을 취소합니다.  
  
-   **멤버 자격** 페이지에는 새 데이터베이스 사용자가 소유할 수 있는 모든 가능한 데이터베이스 멤버 자격 역할이 나열됩니다. 데이터베이스 사용자로부터 역할을 추가하거나 제거하려면 **데이터베이스 역할 멤버 자격**아래에서 역할 옆에 있는 확인란을 선택하거나 선택을 취소합니다.  
  
-   **보안 개체** 페이지에는 사용 가능한 모든 보안 개체와 이러한 보안 개체에서 로그인에 부여할 수 있는 권한이 나열됩니다.  
  
-   **확장 속성** 페이지에서는 데이터베이스 사용자에 사용자 지정 속성을 추가할 수 있습니다. 이 페이지에서는 다음과 같은 옵션을 선택할 수 있습니다.  
  
     **데이터베이스**  
     선택한 데이터베이스의 이름을 표시합니다. 이 필드는 읽기 전용입니다.  
  
     **데이터 정렬**  
     선택한 데이터베이스에 사용된 데이터 정렬을 표시합니다. 이 필드는 읽기 전용입니다.  
  
     **Properties**  
     개체의 확장 속성을 확인하거나 지정합니다. 각 확장 속성은 개체에 연결된 메타데이터의 이름/값 쌍으로 이루어져 있습니다.  
  
     **줄임표(...)**  
     **확장 속성 값** 대화 상자를 열려면 **값** 뒤에 있는 줄임표 **(...)** 를 클릭합니다. 더 큰 범위에서 확장 속성 값을 입력하거나 확인할 수 있습니다. 자세한 내용은 [확장 속성 값 대화 상자](../../databases/value-for-extended-property-dialog-box.md)를 참조하십시오.  
  
     **Delete**  
     선택한 확장 속성을 제거합니다.  
  
##  <a name="TsqlProcedure"></a> T-SQL을 사용하여 사용자 만들기  
    
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  **표준** 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
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
  
 자세한 내용은 추가 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 예제가 포함된 [CREATE USER&#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [보안 주체&#40;데이터베이스 엔진&#41;](../../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [로그인 만들기](../../../relational-databases/security/authentication-access/create-a-login.md)   
 [CREATE LOGIN&#40;Transact-SQL&#41;](../../../t-sql/statements/create-login-transact-sql.md)  
  
  
