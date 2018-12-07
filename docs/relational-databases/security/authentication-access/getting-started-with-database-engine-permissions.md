---
title: 데이터베이스 엔진 사용 권한 시작 | Microsoft 문서
ms.custom: ''
ms.date: 01/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: security
ms.topic: quickstart
helpviewer_keywords:
- permissions [SQL Server], getting started
ms.assetid: 051af34e-bb5b-403e-bd33-007dc02eef7b
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 00d28b0750ba599e4bc73fa2ec6586271b683545
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52410860"
---
# <a name="getting-started-with-database-engine-permissions"></a>데이터베이스 엔진 권한 시작
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 의 권한은 로그인 및 서버 역할을 통해 서버 수준에서 관리되고 데이터베이스 사용자 및 데이터베이스 역할을 통해 데이터베이스 수준에서 관리됩니다. [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] 에 대한 모델은 각 데이터베이스 내에서 동일한 시스템을 노출하지만 서버 수준 권한을 사용할 수 없습니다. 이 항목에서는 몇 가지 기본 보안 개념을 검토한 다음 일반적인 권한 구현을 설명합니다.  
  
## <a name="security-principals"></a>보안 주체  
 보안 주체는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 을 사용하며, 작업 수행 권한을 할당 받을 수 있는 ID의 공식 이름입니다. 이들은 일반적으로 사람 또는 사람의 그룹이지만 사람을 가장하는 다른 엔터티일 수도 있습니다. 나열된 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 을 사용하거나 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]를 사용하여 보안 주체를 만들고 관리할 수 있습니다.  
  
 로그인  
 로그인은 [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]에 로그온하기 위한 개별 사용자 계정입니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] 는 Windows 인증 기반의 로그인 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증 기반의 로그인을 지원합니다. 두 유형의 로그인에 대한 자세한 내용은 [Choose an Authentication Mode](../../../relational-databases/security/choose-an-authentication-mode.md)를 참조하세요.  
  
 고정 서버 역할  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 고정 서버 역할은 편리한 서버 수준 권한 그룹을 제공하는 미리 구성된 역할 집합입니다. `ALTER SERVER ROLE ... ADD MEMBER` 문을 사용하여 역할에 로그인을 추가할 수 있습니다. 자세한 내용은 [ALTER SERVER ROLE&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-server-role-transact-sql.md)을 참조하세요. [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] 는 고정 서버 역할을 지원하지 않지만 master 데이터베이스에 서버 역할처럼 작동하는 두 가지 역할(`dbmanager` 및 `loginmanager`)이 있습니다.  
  
 사용자 정의 서버 역할  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 사용자 고유의 서버 역할을 만들고 서버 수준 권한을 할당할 수 있습니다. `ALTER SERVER ROLE ... ADD MEMBER` 문을 사용하여 서버 역할에 로그인을 추가할 수 있습니다. 자세한 내용은 [ALTER SERVER ROLE&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-server-role-transact-sql.md)을 참조하세요. [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] 는 사용자 정의 서버 역할을 지원하지 않습니다.  
  
 데이터베이스 사용자  
 데이터베이스에서 데이터베이스 사용자를 만들고 해당 데이터베이스 사용자를 로그인에 매핑하여 데이터베이스에 대한 액세스 권한을 로그인에 부여할 수 있습니다. 일반적으로 데이터베이스 사용자 이름은 로그인 이름과 동일하지만 반드시 그래야 하는 것은 아닙니다. 각 데이터베이스 사용자는 단일 로그인에 매핑됩니다. 하나의 로그인을 데이터베이스의 한 사용자에만 매핑할 수 있지만 여러 데이터베이스에서 데이터베이스 사용자로 매핑할 수 있습니다.  
  
 해당 로그인이 없는 데이터베이스 사용자를 만들 수도 있습니다. 이를 *포함된 데이터베이스 사용자*라고 합니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 에서는 포함된 데이터베이스 사용자를 사용하도록 권장합니다. 데이터베이스를 다른 서버로 보다 쉽게 이동할 수 있기 때문입니다. 로그인과 마찬가지로 포함된 데이터베이스 사용자는 Windows 인증 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용할 수 있습니다. 자세한 내용은 [포함된 데이터베이스 사용자 - 이식 가능한 데이터베이스 만들기](../../../relational-databases/security/contained-database-users-making-your-database-portable.md)를 참조하세요.  
  
 인증 방법 및 나타내는 사람이 약간 다른 12가지 유형의 사용자가 있습니다. 사용자 목록을 보려면 [CREATE USER&#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md)를 참조하세요.  
  
 고정 데이터베이스 역할  
 고정 데이터베이스 역할은 편리한 데이터베이스 수준 권한 그룹을 제공하는 미리 구성된 역할 집합입니다. `ALTER ROLE ... ADD MEMBER` 문을 사용하여 데이터베이스 사용자 및 사용자 정의 데이터베이스 역할을 고정 데이터베이스 역할에 추가할 수 있습니다. 자세한 내용은 [ALTER ROLE&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-role-transact-sql.md)을 참조하세요.  
  
 사용자 정의 데이터베이스 역할  
 `CREATE ROLE` 권한이 있는 사용자는 일반적인 권한이 있는 사용자 그룹을 나타내는 새 사용자 정의 데이터베이스 역할을 만들 수 있습니다. 권한 관리 및 모니터링을 간소화하기 위해 일반적으로 권한은 전체 역할에 부여되거나 거부됩니다. `ALTER ROLE ... ADD MEMBER` 문을 사용하여 데이터베이스 역할에 데이터베이스 사용자를 추가할 수 있습니다. 자세한 내용은 [ALTER ROLE&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-role-transact-sql.md)을 참조하세요.  
  
 다른 보안 주체  
 여기에 설명되지 않은 추가 보안 주체에는 응용 프로그램 역할과 인증서 또는 비대칭 키를 기반으로 하는 로그인 및 사용자가 포함됩니다.  
  
 Windows 사용자, Windows 그룹, 로그인 및 데이터베이스 사용자 간의 관계를 보여 주는 그래픽은 [Create a Database User](../../../relational-databases/security/authentication-access/create-a-database-user.md)를 참조하세요.  
  
## <a name="typical-scenario"></a>일반적인 시나리오  
 다음 예제에서는 권한 구성의 일반적인 방법 및 권장 방법을 나타냅니다.  
  
#### <a name="in-active-directory-or-azure-active-directory"></a>Active Directory 또는 Azure Active Directory에서 다음을 수행합니다.  
  
1.  각 사용자에 대한 Windows 사용자를 만듭니다.  
  
2.  작업 단위 및 작업 기능을 나타내는 Windows 그룹을 만듭니다.  
  
3.  Windows 그룹에 Windows 사용자를 추가합니다.  
  
#### <a name="if-the-person-connecting-will-be-connecting-to-many-databases"></a>연결하는 사용자를 여러 데이터베이스에 연결하는 경우  
  
1.  Windows 그룹에 대한 로그인을 만듭니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 Active Directory 단계를 건너뛰고 여기에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증 로그인을 만듭니다.  
  
2.  사용자 데이터베이스에서 Windows 그룹을 나타내는 로그인에 대한 데이터베이스 사용자를 만듭니다.  
  
3.  사용자 데이터베이스에서 각각 유사한 기능을 나타내는 하나 이상의 사용자 정의 데이터베이스 역할을 만듭니다. 예를 들어 재무 분석가 및 판매 분석가를 만듭니다.  
  
4.  하나 이상의 사용자 정의 데이터베이스 역할에 데이터베이스 사용자를 추가합니다.  
  
5.  사용자 정의 데이터베이스 역할에 권한을 부여합니다.  
  
#### <a name="if-the-person-connecting-will-be-connecting-to-only-one-database"></a>연결하는 사용자를 하나의 데이터베이스에만 연결하는 경우  
  
1.  Windows 그룹에 대한 로그인을 만듭니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 Active Directory 단계를 건너뛰고 여기에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증 로그인을 만듭니다.  
  
2.  사용자 데이터베이스에서 Windows 그룹에 대한 포함된 데이터베이스 사용자를 만듭니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 Active Directory 단계를 건너뛰고 여기에서 포함된 데이터베이스 사용자 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 만듭니다.  
  
3.  사용자 데이터베이스에서 각각 유사한 기능을 나타내는 하나 이상의 사용자 정의 데이터베이스 역할을 만듭니다. 예를 들어 재무 분석가 및 판매 분석가를 만듭니다.  
  
4.  하나 이상의 사용자 정의 데이터베이스 역할에 데이터베이스 사용자를 추가합니다.  
  
5.  사용자 정의 데이터베이스 역할에 권한을 부여합니다.  
  
 이 시점에서 Windows 사용자는 일반적으로 Windows 그룹의 멤버입니다. Windows 그룹에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]의 로그인이 있습니다. 로그인은 사용자 데이터베이스에서 사용자 ID에 매핑됩니다. 사용자는 데이터베이스 역할의 멤버입니다. 이제 역할에 권한을 추가해야 합니다.  
  
## <a name="assigning-permissions"></a>권한 할당  
 대부분의 권한 문은 다음과 같은 형식입니다.  
  
```  
AUTHORIZATION  PERMISSION  ON  SECURABLE::NAME  TO  PRINCIPAL;  
```  
  
-   `AUTHORIZATION` 은 `GRANT`, `REVOKE` 또는 `DENY`여야 합니다.  
  
-   `PERMISSION` 은 허용되거나 금지된 작업을 설정합니다. [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] 에서는 230개의 권한을 지정할 수 있습니다. [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] 에는 일부 작업이 Azure에서 관련이 없기 때문에 더 적은 권한이 있습니다. 사용 권한은 [사용 권한&#40;데이터베이스 엔진&#41;](../../../relational-databases/security/permissions-database-engine.md) 항목 및 아래에 참조된 차트에 나와 있습니다.  
  
-   `ON SECURABLE::NAME` 은 보안 개체(서버, 서버 개체, 데이터베이스 또는 데이터베이스 개체)의 형식과 해당 이름입니다. 일부 권한은 명확하거나 컨텍스트에서 부적절하므로 `ON SECURABLE::NAME` 이 필요 없습니다. 예를 들어 `CREATE TABLE` 권한에는 `ON SECURABLE::NAME` 절이 필요 없습니다. 예를 들어 `GRANT CREATE TABLE TO Mary;` 는 Mary가 테이블을 만들도록 허용합니다.  
  
-   `PRINCIPAL` 은 권한을 받거나 상실하는 보안 주체(로그인, 사용자 또는 역할)입니다. 가능한 경우 역할에 권한을 부여합니다.  
  
 다음 예제 grant 문은 `UPDATE` 스키마에 포함된 `Parts` 테이블 또는 뷰에 대한 `Production` 권한을 `PartsTeam`역할에 부여합니다.  
  
```  
GRANT UPDATE ON OBJECT::Production.Parts TO PartsTeam;  
```  
  
 `GRANT` 문을 사용하여 보안 주체(로그인, 사용자 및 역할)에 권한을 부여합니다. 권한을 명시적으로 거부하려면  `DENY` 명령을 사용합니다. 이전에 부여하거나 거부한 권한을 제거하려면 `REVOKE` 문을 사용합니다. 권한은 누적적입니다. 즉, 사용자는 사용자, 로그인 및 그룹 멤버 자격에 부여된 모든 권한을 받습니다. 그러나 권한 거부는 모든 부여를 재정의합니다.  
  
> [!TIP]  
>  일반적으로 발생하는 실수는 `GRANT` 대신 `DENY` 를 사용하여 `REVOKE`를 제거하려는 것입니다. 이는 사용자가 여러 소스에서 권한을 받는 경우 문제를 일으킬 수 있으며, 매우 일반적으로 발생합니다. 다음 예에서는 보안 주체를 보여 줍니다.  
  
 Sales 그룹은 `SELECT` 문을 통해 OrderStatus 테이블에 대한 `GRANT SELECT ON OBJECT::OrderStatus TO Sales;`권한을 받습니다. 사용자 Ted는 Sales 역할의 멤버입니다. Ted에게는 `SELECT` 문을 통해 자신의 사용자 이름에 따라 OrderStatus 테이블에 대한  `GRANT SELECT ON OBJECT::OrderStatus TO Ted;`권한도 부여되었습니다. 관리자가 Sales 역할에 대한 `GRANT` 를 제거하려고 한다고 가정해 보겠습니다.  
  
-   관리자가 `REVOKE SELECT ON OBJECT::OrderStatus TO Sales;`를 올바르게 실행하는 경우 Ted는 자신의 개인적인 `SELECT` 문을 통해 OrderStatus 테이블에 대한 `GRANT` 액세스를 유지합니다.  
  
-   관리자가 `DENY SELECT ON OBJECT::OrderStatus TO Sales;` 를 잘못 실행한 경우 Sales 역할의 멤버인 Ted는 Sales에 대한 `SELECT` 가 자신의 개인적인 `DENY` 를 재정의하므로  `GRANT`권한이 거부됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]를 사용하여 권한을 구성할 수 있습니다. 개체 탐색기에서 보안 개체를 찾아서 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다. **사용 권한** 페이지를 선택합니다. 사용 권한 페이지 사용에 대한 도움말은 [Permissions or Securables Page](../../../relational-databases/security/permissions-or-securables-page.md)를 참조하세요.  
  
## <a name="permission-hierarchy"></a>권한 계층  
 권한에는 부모/자식 계층이 있습니다. 즉, 데이터베이스에 대한 `SELECT` 권한을 부여하는 경우 이 권한에는 데이터베이스의 모든 자식 스키마에 대한 `SELECT` 권한이 포함됩니다. 스키마에 대한 `SELECT` 권한을 부여하는 경우 이 권한에는 스키마의 모든 자식 테이블과 뷰에 대한 `SELECT` 권한이 포함됩니다. 권한은 전이적입니다. 즉, 데이터베이스에 대한 `SELECT` 권한을 부여하는 경우 이 권한에는 모든 자식 스키마와 모든 손자 테이블 및 뷰에 대한 `SELECT` 권한이 포함됩니다.  
  
 권한에는 포함 권한도 있습니다. 개체에 대한 `CONTROL` 권한은 일반적으로 해당 개체에 대한 모든 권한을 부여합니다.  
  
 부모/자식 계층과 포함 계층 모두 동일한 권한에 대해 작동할 수 있으므로 권한 시스템이 복잡해질 수 있습니다. Customers 스키마와 SalesDB 데이터베이스에 있는 Region 테이블을 예로 들어 보겠습니다.  
  
-   `CONTROL` 권한에는 `ALTER`, `SELECT`, `INSERT`,  `UPDATE`, `DELETE`및 기타 권한을 포함하여 Region 테이블에 대한 다른 모든 권한이 포함됩니다.  
  
-   `SELECT` 권한에는 Region 테이블에 대한 `SELECT` 권한이 포함됩니다.  
  
 따라서 Region 테이블에 대한 `SELECT` 권한은 다음 6개 문 중 하나를 통해 구현할 수 있습니다.  
  
```  
GRANT SELECT ON OBJECT::Region TO Ted;   
  
GRANT CONTROL ON OBJECT::Region TO Ted;   
  
GRANT SELECT ON SCHEMA::Customers TO Ted;   
  
GRANT CONTROL ON SCHEMA::Customers TO Ted;   
  
GRANT SELECT ON DATABASE::SalesDB TO Ted;   
  
GRANT CONTROL ON DATABASE::SalesDB TO Ted;  
```  
  
## <a name="grant-the-least-permission"></a>최소 권한 부여  
 위에 나열된 첫 번째 권한(`GRANT SELECT ON OBJECT::Region TO Ted;`)은 가장 세분화된 권한입니다. 즉, 이 문은 `SELECT`를 부여할 수 있는 최소 권한입니다. 하위 개체에 대한 권한은 함께 제공되지 않습니다. 항상 가능한 최소 권한을 부여하는 것이 좋지만 권한 부여 시스템을 간소화하려면 상위 수준에서 부여해야 합니다. 따라서 Ted에게 전체 스키마에 대한 권한이 필요한 경우 테이블 또는 뷰 수준에서 `SELECT` 권한을 여러 번 부여하는 대신 스키마 수준에서 `SELECT` 권한을 한 번 부여합니다. 데이터베이스의 디자인은 이 전략의 성공 가능성에 큰 영향을 미칩니다. 이 전략은 동일한 권한이 필요한 개체가 단일 스키마에 포함되도록 데이터베이스가 디자인된 경우에 가장 효과적입니다.  
  
## <a name="list-of-permissions"></a>권한 목록  
 [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] 에는 230개의 권한이 있습니다. [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 에는 219개의 권한이 있습니다. [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 에는 214개의 권한이 있습니다. [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] 에는 195개의 권한이 있습니다. [!INCLUDE[ssSDS](../../../includes/sssds-md.md)], [!INCLUDE[ssDW](../../../includes/ssdw-md.md)]및 [!INCLUDE[ssAPS](../../../includes/ssaps-md.md)] 에는 각각 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 적용되지 않는 일부 권한이 있지만 데이터베이스 엔진의 일부만 노출하기 때문에 권한 수가 적습니다. 
 
 [!INCLUDE[database-engine-permissions](../../../includes/paragraph-content/database-engine-permissions.md)]
 
 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 보안 주체와 서버 및 데이터베이스 개체 간의 관계를 보여 주는 그래픽은 [사용 권한 계층 구조&#40;데이터베이스 엔진&#41;](../../../relational-databases/security/permissions-hierarchy-database-engine.md)를 참조하세요.  
  
## <a name="permissions-vs-fixed-server-and-fixed-database-roles"></a>권한과 고정 서버 및 고정 데이터베이스 역할  
 고정 서버 역할과 고정 데이터베이스 역할의 권한은 유사하지만 세분화된 권한과 정확히 동일하지는 않습니다. 예를 들어 `sysadmin` 고정 서버 역할의 멤버는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]권한으로 로그인할 경우 `CONTROL SERVER` 인스턴스에 대한 모든 권한을 가집니다. 그러나 `CONTROL SERVER` 권한을 부여할 경우 로그인이 sysadmin 고정 서버 역할의 멤버로 설정되지 않으며,  `sysadmin` 고정 서버 역할에 로그인을 추가할 경우 로그인에  `CONTROL SERVER` 권한이 명시적으로 부여되지 않습니다. 경우에 따라 저장 프로시저는 세분화된 권한을 확인하지 않고 고정 역할을 확인하여 권한을 확인합니다. 예를 들어 데이터베이스를 분리하려면 `db_owner` 고정 데이터베이스 역할의 멤버 자격이 필요합니다. 동등한 `CONTROL DATABASE` 권한으로는 부족합니다. 이 두 시스템은 병렬로 작동하지만 거의 서로 상호 작용하지 않습니다. 가능한 경우 고정 역할 대신 세분화된 새 권한 시스템을 사용하는 것이 좋습니다.
  
## <a name="monitoring-permissions"></a>권한 모니터링  
 다음 뷰는 보안 정보를 반환합니다.  
  
-   서버의 로그인 및 사용자 정의 서버 역할은 `sys.server_principals` 뷰를 사용하여 검사할 수 있습니다. 이 뷰는 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]에서 사용할 수 없습니다.  
  
-   데이터베이스의 사용자 및 사용자 정의 역할은 `sys.database_principals` 뷰를 사용하여 검사할 수 있습니다.  
  
-   로그인 및 사용자 정의 고정 서버 역할에 부여된 권한은 `sys.server_permissions` 뷰를 사용하여 검사할 수 있습니다. 이 뷰는 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]에서 사용할 수 없습니다.  
  
-   사용자 및 사용자 정의 고정 데이터베이스 역할에 부여된 권한은 `sys.database_permissions` 뷰를 사용하여 검사할 수 있습니다.  
  
-   데이터베이스 역할 멤버 자격은 `sys. sys.database_role_members` 뷰를 사용하여 검사할 수 있습니다.  
  
-   서버 역할 멤버 자격은 `sys.server_role_members` 뷰를 사용하여 검사할 수 있습니다. 이 뷰는 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]에서 사용할 수 없습니다.  
  
-   추가 보안 관련 뷰는 [보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md) 를 사용하여 보안 주체를 만들고 관리할 수 있습니다.  
  
### <a name="useful-transact-sql-statements"></a>유용한 Transact-SQL 문  
 다음 문은 권한에 대한 유용한 정보를 반환합니다.  
  
 데이터베이스에서 부여되거나 거부된 명시적 권한([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)])을 반환하려면 데이터베이스에서 다음 문을 실행합니다.  
  
```sql  
SELECT   
    perms.state_desc AS State,   
    permission_name AS [Permission],   
    obj.name AS [on Object],   
    dPrinc.name AS [to User Name]  
FROM sys.database_permissions AS perms  
JOIN sys.database_principals AS dPrinc  
    ON perms.grantee_principal_id = dPrinc.principal_id  
JOIN sys.objects AS obj  
    ON perms.major_id = obj.object_id;  
```  
  
 서버 역할의 멤버([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 만)를 반환하려면 다음 문을 실행합니다.  
  
```sql  
SELECT sRole.name AS [Server Role Name] , sPrinc.name AS [Members]  
FROM sys.server_role_members AS sRo  
JOIN sys.server_principals AS sPrinc  
    ON sRo.member_principal_id = sPrinc.principal_id  
JOIN sys.server_principals AS sRole  
    ON sRo.role_principal_id = sRole.principal_id;  
```  
  
 
 데이터베이스 역할의 멤버([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)])를 반환하려면 데이터베이스에서 다음 문을 실행합니다.  
  
```sql  
SELECT dRole.name AS [Database Role Name], dPrinc.name AS [Members]  
FROM sys.database_role_members AS dRo  
JOIN sys.database_principals AS dPrinc  
    ON dRo.member_principal_id = dPrinc.principal_id  
JOIN sys.database_principals AS dRole  
    ON dRo.role_principal_id = dRole.principal_id;  
```  
  
## <a name="next-steps"></a>Next Steps  
 시작하는 데 유용한 추가 항목은 다음을 참조하세요.  
  
-   [자습서: 데이터베이스 엔진 시작](../../../relational-databases/tutorial-getting-started-with-the-database-engine.md) [데이터베이스 만들기&#40;자습서&#41;](../../../t-sql/lesson-1-creating-database-objects.md#)  
  
-   [자습서: SQL Server Management Studio](../../../tools/sql-server-management-studio/tutorial-sql-server-management-studio.md)  
  
-   [자습서: Transact-SQL 문 작성](../../../t-sql/tutorial-writing-transact-sql-statements.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 데이터베이스 엔진 및 Azure SQL 데이터베이스에 대한 보안 센터](../../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)   
 [보안 함수&#40;Transact-SQL&#41;](../../../t-sql/functions/security-functions-transact-sql.md)   
 [보안 관련 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)   
 [보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [sys.fn_builtin_permissions&#40;Transact-SQL&#41;](../../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [효과적인 데이터베이스 엔진 사용 권한 결정](../../../relational-databases/security/authentication-access/determining-effective-database-engine-permissions.md)
  
  
