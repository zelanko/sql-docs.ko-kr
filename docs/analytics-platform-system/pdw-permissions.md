---
title: 병렬 데이터 웨어하우스에서 사용 권한 | Microsoft Docs
description: 이 문서에서는 요구 사항 및 Parallel Data Warehouse에 대 한 데이터베이스 권한을 관리 하기 위한 옵션을 설명 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 1ac058e42b8bad4f499210835a1f85c3cc7a08a5
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52523590"
---
# <a name="managing-permissions-in-parallel-data-warehouse"></a>병렬 데이터 웨어하우스에서 관리 권한
이 문서에서는 요구 사항 및 SQL Server PDW에 대 한 데이터베이스 권한을 관리 하기 위한 옵션을 설명 합니다.  
  
## <a name="BackupRestoreBasics"></a>데이터베이스 엔진의 권한 기초  
SQL Server PDW에서 데이터베이스 엔진 권한 로그인을 통해 서버 수준 및 데이터베이스 사용자 및 사용자 정의 데이터베이스 역할을 통해 데이터베이스 수준에서 관리 됩니다.  
  
**로그인**  
로그인은 SQL Server PDW에 로그인 하기 위해 개별 사용자 계정입니다. SQL Server PDW Windows 인증 및 SQL Server 인증을 사용 하 여 로그인을 지원 합니다.  Windows 인증 로그인에는 Windows 사용자 또는 SQL Server PDW에서 신뢰할 수 있는 모든 도메인의 Windows 그룹 수 있습니다. SQL Server 인증 로그인이 정의 되어 있고 SQL Server PDW에 의해 인증 암호를 지정 하 여 생성 되어야 합니다.  
  
멤버는 **sysadmin** 고정된 서버 역할 (같은 합니다 **sa** 로그인) 데이터베이스 사용자에 매핑되는 필요 없이 데이터베이스에 연결할 수 있습니다. 매핑되는 **dbo** 사용자입니다. 데이터베이스의 소유자와도 매핑되는 **dbo** 사용자입니다.  
  
**서버 역할**  
편리한 서버 수준 권한 그룹을 제공 하는 미리 구성 된 역할 집합이 포함 된 네 가지 특별 한 서버 역할이 있습니다. 합니다 **sysadmin**, **MediumRC**합니다 **LargeRC**, 및 **XLargeRCfixed** 서버 역할은 현재 SQL에서 구현 전용 서버 역할 PDW 서버입니다. 합니다 **sa** 로그인의 유일한 구성원입니다 합니다 **sysadmin** 고정된 서버 역할 및 추가 로그인을 추가할 수 없습니다는 **sysadmin** 역할입니다. 로그인에 부여할 수 있습니다는 **CONTROL SERVER** 권한인 마찬가지로를 동일 하지는 않지만 합니다 **sysadmin** 고정된 서버 역할입니다. 사용 하 여 [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md) 다른 서버 역할에 구성원을 추가 합니다. SQL Server PDW는 사용자 정의 서버 역할을 지원 하지 않습니다.  
  
**데이터베이스 사용자**  
로그인은 데이터베이스에서 데이터베이스 사용자를 만들고 해당 데이터베이스 사용자를 로그인에 매핑 데이터베이스에 대 한 액세스를 부여 됩니다. 일반적으로 데이터베이스 사용자 이름은 로그인 이름과 동일하지만 반드시 그래야 하는 것은 아닙니다. 각 데이터베이스 사용자는 단일 로그인에 매핑됩니다. 하나의 로그인을 데이터베이스의 한 사용자에만 매핑할 수 있지만 여러 데이터베이스에서 데이터베이스 사용자로 매핑할 수 있습니다.  
  
**고정된 데이터베이스 역할**  
고정된 데이터베이스 역할은 편리한 데이터베이스 수준 권한 그룹을 제공 하는 미리 구성 된 역할의 집합입니다. 데이터베이스 사용자 및 사용자 정의 데이터베이스 역할 사용 하 여 고정된 데이터베이스 역할에 추가할 수는 [sp_addrolemember](../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) 프로시저입니다. 고정된 데이터베이스 역할에 대 한 자세한 내용은 참조 하세요. [고정 데이터베이스 역할](#fixed-database-roles)입니다.  
  
**사용자 정의 데이터베이스 역할**  
사용자는 **CREATE ROLE** 권한 일반적인 권한 있는 사용자 그룹을 나타내는 새 사용자 정의 데이터베이스 역할을 만들 수 있습니다. 권한 관리 및 모니터링을 간소화하기 위해 일반적으로 권한은 전체 역할에 부여되거나 거부됩니다.  
  
사용 하 여 보안 주체 (로그인, 사용자 및 역할)에 권한을 부여 합니다 **부여** 문입니다. 사용 권한을 사용 하 여 명시적으로 거부 됩니다 합니다 **DENY** 명령입니다. 사용 하 여 이전에 권한이 부여 되거나 거부는 제거 되는 **해지** 문. 권한은 누적적입니다. 즉, 사용자는 사용자, 로그인 및 그룹 멤버 자격에 부여된 모든 권한을 받습니다. 그러나 권한 거부는 모든 부여를 재정의합니다. <!-- MISSING LINKS (For information, syntax, and available permissions with these commands, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md)).  -->  
  
다음 예제에서는 권한 구성의 일반적인 방법 및 권장 방법을 나타냅니다.  
  
1.  Windows 인증을 사용 하는 경우에 각 Windows 사용자 또는 SQL Server PDW에 연결 하는 Windows 그룹에 대 한 로그인을 만듭니다. SQL Server 인증을 사용 하는 경우 SQL Server PDW에 연결 하는 각 사용자에 대 한 로그인을 만듭니다.  
  
2.  필요한 모든 데이터베이스에서 각 로그인에 대 한 데이터베이스 사용자를 만듭니다.  
  
3.  유사한 기능을 나타내는 각각 하나 이상의 사용자 정의 데이터베이스 역할을 만듭니다. 예를 들어 재무 분석가 및 판매 분석가를 만듭니다.  
  
4.  하나 이상의 사용자 정의 데이터베이스 역할에 데이터베이스 사용자를 추가 합니다.  
  
5.  사용자 정의 데이터베이스 역할에 권한을 부여합니다.  
  
로그인은 서버 수준 개체 이며 확인 하 여 나열할 수 있습니다 [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)합니다. 서버 보안 주체에 서버 수준 사용 권한만 부여할 수 있습니다.  
  
사용자 및 데이터베이스 역할은 데이터베이스 수준 개체 및 확인 하 여 나열할 수 있습니다 [sys.database_principals](../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)합니다. 만 데이터베이스 수준 사용 권한은 데이터베이스 보안 주체에 부여할 수 있습니다.  
  
## <a name="BackupTypes"></a>기본 권한  
다음 목록에서는 기본 사용 권한을 설명합니다.  
  
-   Using 하 여 로그인을 만들면 **CREATE LOGIN** 문을 로그인 수신 합니다 **CONNECT SQL** SQL Server PDW에 연결할 로그인을 허용 하는 권한.  
  
-   데이터베이스 사용자를 사용 하 여 만들어질 때를 **CREATE USER** 문, 사용자에 게는 **ON DATABASE 연결::**_< database_name >_ 권한이 허용 합니다 사용자로 데이터베이스에 연결할에 로그인 합니다.  
  
-   공용 역할을 포함 한 모든 보안 주체에 명시적 사용 권한에서 암시적 사용 권한 상속 되기 때문에 기본적으로 명시적 또는 암시적 사용 권한 없음를 갖습니다. 따라서 명시적 사용 권한 없음 있을 때 있을 수도 있습니다 암시적 권한이 없습니다.  
  
-   로그인에는 개체 또는 데이터베이스의 소유자가 되 면 로그인에는 항상 개체 또는 데이터베이스에 대 한 모든 권한이 있습니다. 소유권 사용 권한은 명시적 사용 권한으로 표시 되지 않습니다. 합니다 **권한 부여**, **해지**, 및 **거부** 문을 소유권 권한에 영향을 주지 합니다. 사용 하 여 소유권을 변경할 수 있습니다 합니다 [ALTER AUTHORIZATION](../t-sql/statements/alter-authorization-transact-sql.md) 문입니다.  
  
-   Sa 로그인에 어플라이언스에서 모든 권한이 있습니다. 소유권 사용 권한과 마찬가지로 sa 권한을 변경할 수 없습니다 및 명시적 사용 권한으로 표시 되지 않습니다. 합니다 **권한 부여**, **해지**, 및 **거부** 문을 sa 사용 권한 제한에 영향을 주지 합니다.  
  
-   PUBLIC 서버 역할 사용 권한 없음를 받고 기본적으로 다른 서버 역할에서 권한을 상속 하지 않습니다. PUBLIC 서버 역할에 명시적 권한을 지정할 수 있습니다 합니다 **권한 부여**, **해지**, 및 **거부** 문.  
  
-   트랜잭션 권한이 필요 하지 않습니다. 모든 보안 주체를 실행할 수는 **BEGIN TRANSACTION**를 **커밋**, 및 **롤백** 트랜잭션 명령입니다. 그러나 보안 주체에는 트랜잭션 내에서 각 문을 실행 하려면 적절 한 권한이 있어야 합니다.  
  
-   **USE** 문은 사용 권한이 필요하지 않습니다. 하지만 모든 보안 주체를 실행할 수는 **사용 하 여** 문을 모든 데이터베이스에서 데이터베이스에 액세스 하는 사용자 계정 데이터베이스에 있거나 게스트 사용자를 사용할 수 있어야 합니다.  
  
### <a name="the-public-role"></a>PUBLIC 역할  
모든 새 어플라이언스 로그인 자동으로 PUBLIC 역할에 속해야 합니다. PUBLIC 서버 역할에는 다음과 같은 특징이 있습니다.  
  
-   PUBLIC 서버 역할에 기본적으로 권한이 없습니다.  
  
-   PUBLIC 서버 역할의 멤버인 모든 보안 주체 및은 PUBLIC 서버 역할은 다른 서버 역할의 멤버인 되지 않습니다.  
  
-   PUBLIC 서버 역할에는 암시적 권한을 상속할 수 없습니다. PUBLIC 역할에 부여 된 모든 사용 권한은 명시적으로 부여 되어야 합니다.  
  
## <a name="BackupProc"></a>사용 권한 결정  
로그인을 특정 작업을 수행할 권한이 여부는 로그인, 사용자 및 사용자가 멤버인 역할에 허용 또는 거부 한 사용 권한에 따라 달라 집니다. 서버 수준 사용 권한 (같은 **CREATE LOGIN** 하 고 **VIEW SERVER STATE**) 서버 수준 보안 주체 (로그인)에 사용할 수 있습니다. 데이터베이스 수준 사용 권한 (같은 **선택** 테이블에서 또는 **EXECUTE** 프로시저에) 데이터베이스 수준 보안 주체 (사용자 및 데이터베이스 역할)에 사용할 수 있습니다.  
  
### <a name="implicit-and-explicit-permissions"></a>암시적 및 명시적 사용 권한  
*명시적 사용 권한*은 **GRANT** 또는 **DENY**문으로 보안 주체에게 주어진 **GRANT** 또는 **DENY** 사용 권한입니다. 데이터베이스 수준 권한을 나열 합니다 [sys.database_permissions](../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) 보기. 서버 수준 권한을 나열 합니다 [sys.server_permissions](../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) 보기.  
  
*암시적 사용 권한* 는 **GRANT** 또는 **거부** 보안 주체 (로그인 또는 서버 역할)에 상속 된 사용 권한. 다음과 같은 방법으로 권한을 상속할 수 있습니다.  
  
-   보안 주체가 멤버인 경우 역할의 보안 주체에 명시적 없는 경우에 보안 주체를 역할에서 권한을 상속할 수 있습니다 **권한 부여** 하거나 **거부** 권한.  
  
-   보안 주체 개체 부모 범위 (예: 테이블 또는 전체 데이터베이스에 대 한 권한을 스키마) 중 하나에 대 한 권한이 보안 주체 하위 개체 (예: 테이블)에서 권한을 상속할 수 있습니다.  
  
-   보안 주체에서 하위 사용 권한을 포함 하는 권한이 있는 사용 권한을 상속할 수 있습니다. 예를 들어 합니다 **ALTER ANY USER** 권한을 모두 포함 합니다 **CREATE USER** 및 **ALTER ON USER::** _<name>_ 사용 권한입니다.  
  
### <a name="determining-permissions-when-performing-actions"></a>작업을 수행할 때 사용 권한 결정  
보안 주체에 할당 하는 권한을 결정 하는 프로세스는 복잡 합니다. 복잡 한 보안 주체에는 여러 역할의 멤버일 수 있습니다 및 권한 역할 계층 구조의 여러 수준으로 전달 될 수 있으므로 암시적 사용 권한 결정 하는 경우 발생 합니다.  
  
다음 목록은 사용 권한 결정 하는 것에 대 한 일반 규칙을 보여 줍니다.  
  
-   소유권 권한을 의미합니다.  
  
    개체 소유자 개체의 모든 권한이 있습니다. 마찬가지로 데이터베이스 소유자에 데이터베이스에 데이터베이스에서 모든 권한 및 개체에 대 한 모든 권한이 있습니다. 이러한 사용 권한은 변경할 수 없습니다.  
  
-   서버 역할 멤버 자격의 계층 구조에서 여러 수준에서 권한은 상속할 수 있습니다.  
  
    예를 들어, 다음과 같은 경우를 있다고 가정 합니다.  
  
    -   로그인 David PerfAnalysts 데이터베이스 역할의 멤버 임  
  
    -   PerfAnalysts는 프로덕션 데이터베이스 역할의 멤버 임  
  
    -   David 및 PerfAnalysts 없는 **선택** Customer 테이블에 대 한 권한이 있습니다. 사용 권한 해지 또는 명시적으로 부여 되었습니다.  
  
    -   프로덕션에는 **선택** Customer 테이블에 대 한 권한이 있습니다.  
  
    PerfAnalysts를 상속 하는 예에서 **권한 부여** 프로덕션 및 David에서 Customer 테이블에 대 한 권한이 상속 됩니다 **부여** 프로덕션에서 Customer 테이블에 대 한 권한.  
  
-   **DENY** 재정의 **부여** 권한 충돌 하는 경우.  
  
    예를 들어, David 로그인 권한이 없는 고객 테이블에 두 데이터베이스 역할의 멤버 이며-있는 dbgroup1 **거부** dbgroup2 있는 고 Customer 테이블에 대 한 권한이 **GRANT** Customer 테이블에 대 한 권한이 있습니다. David를 상속 하는 경우에 **DENY** Customer 테이블에 대 한 권한. 이 경우 역할 명시적 또는 암시적으로 해당 권한을 얻은 여부입니다.  
  
### <a name="auditing-permissions"></a>감사 사용 권한  
사용자의 권한 조사 하려면 다음을 확인 합니다.  
  
-   시스템 관리자는 로그인 확인 하려면 다음 쿼리를 실행 합니다.  
  
    ```sql  
    SELECT SPLogins.name, 'is a member of ', SPRoles.name   
    FROM sys.server_role_members AS SRM   
    JOIN sys.server_principals AS SPRoles   
        ON SRM.role_principal_id = SPRoles.principal_id   
    JOIN sys.server_principals AS SPLogins   
        ON SRM.member_principal_id = SPLogins.principal_id;  
    ```  
  
-   로그인 명시적 권한이 부여 되었는지 확인 하려면 다음 쿼리를 실행 합니다.  
  
    ```sql  
    SELECT name, 'has the ', state_desc , permission_name, ' permission'  
    FROM sys.server_permissions AS SP  
    JOIN sys.server_principals AS SPRoles   
        ON SP.grantee_principal_id = SPRoles.principal_id;  
    ```  
  
-   데이터베이스 역할의 멤버인 데이터베이스 사용자를 확인 하려면 사용자 데이터베이스에서 다음 쿼리를 실행 합니다.  
  
    ```sql  
    SELECT DPUsers.name, 'is a member of ', DPRoles.name    
    FROM sys.database_role_members AS DRM  
    JOIN sys.database_principals AS DPRoles   
        ON DRM.role_principal_id = DPRoles.principal_id  
    JOIN sys.database_principals AS DPUsers  
        ON DRM.member_principal_id = DPUsers.principal_id;  
    ```  
  
-   데이터베이스 사용자 및 역할 부여 되거나 거부 된 특정 사용 권한이 확인 하려면 사용자 데이터베이스에서 다음 쿼리를 실행 합니다. Sys.objects 및 sys.schemas에는 major_id를 사용 하 여 설명 되어 있는 항목을 식별 하는 등 추가 뷰 쿼리를 해야 합니다.  
  
    ```sql  
    SELECT DPUsers.name, 'has the ', permission_name,   
    'permission on the item described as class = ', class, 'id = ', major_id  
    FROM sys.database_permissions AS DP  
    JOIN sys.database_principals AS DPUsers  
        ON DP.grantee_principal_id = DPUsers.principal_id;  
    ```  
  
## <a name="RestoreProc"></a>데이터베이스 사용 권한 모범 사례  
  
-   실제로 가장 세부적인 수준 권한을 부여 합니다. 테이블 권한 부여 권한 또는 뷰 수준 많아지기 때문 될 수 있습니다. 하지만 데이터베이스 수준에서 권한을 부여 너무 서 수 있습니다. 데이터베이스를 작업 경계를 정의 하도록 스키마를 사용 하 여 디자인 된 가장 스키마 사용 권한 부여를 적절 한 절충 테이블 수준 및 데이터베이스 수준입니다.  
  
-   사용자 또는 로그인 대신 역할에 권한을 부여 합니다. 사용자 대신 역할을 사용 하 여 권한 관리에서는 신속 하 게 권한을 부여 하거나 역할 안팎으로 이동 하 여 사용자 또는 로그인에 대 한 사용 권한 집합을 취소 하기가 쉽습니다. 함수는 다른 사람이 전달할 때 사용 권한을 수 그대로 역할 멤버 자격 변경 하는 동안 역할 수준입니다.  
  
-   작업 함수를 기반으로 작업을 수행 하는 회사 그룹 작업 함수 역할을 결합 하는 더 높은 수준의 그룹 역할에 기반 하는 역할에 권한을 부여 합니다.  
  
-   모든 최종 사용자는 고유한 로그인을 해야 합니다. 사용자가 로그인을 공유할 수 없도록 합니다. 각 사용자에 대 한 로그인을 제공 하는 감사 내역을 확인 및 권한 관리를 간소화 합니다.  
  
## <a name="fixed-database-roles"></a>고정 데이터베이스 역할
SQL Server 서버에 대 한 권한을 관리할 수 있도록 미리 구성 된 (고정된) 데이터베이스 수준 역할을 제공 합니다. 미리 구성 된 역할에 할당 된 권한은 변경할 수 없습니다에 고정 됩니다. 사용자 정의 데이터베이스 역할을 만들 수도 있습니다. 사용자 정의 데이터베이스 역할에 할당 된 사용 권한을 변경할 수 있습니다.  
  
역할은 다른 보안 주체를 그룹핑하는 보안 주체입니다. 데이터베이스 역할은 데이터베이스 수준 사용 권한 범위에 있습니다. 데이터베이스 사용자 및 다른 데이터베이스 역할은 데이터베이스 역할의 구성원으로 추가할 수 있습니다. 고정된 데이터베이스 역할에 추가할 수 없습니다. *역할* 은 Windows 운영 체제의 *그룹* 과 같습니다.  
  
가지 9 고정된 데이터베이스 역할도 있습니다.  
  
-   **db_owner**  
  
-   **db_securityadmin**  
  
-   **db_accessadmin**  
  
-   **db_backupoperator**  
  
-   **db_ddladmin**  
  
-   **db_datawriter**  
  
-   **db_datareader**  
  
-   **db_denydatawriter**  
  
-   **db_denydatareader**  
  
### <a name="permissions-of-the-fixed-database-roles"></a>고정된 데이터베이스 역할의 사용 권한  
고정된 서버 역할과 고정된 데이터베이스 역할의 시스템은는 1980's에서 발생 하는 레거시 시스템입니다. 고정된 역할은 계속 지원 하며 몇 가지 사용자가 보안 요구 사항은 간단 하는 환경에서 유용 합니다. SQL Server 2005 부터는 권한을 부여 하는 자세한 시스템 생성 되었습니다. 이 새 시스템은 세부적인 모두 권한 부여 및 거부에 대 한 더 많은 옵션을 제공 합니다. 보다 세분화 된 시스템의 추가 복잡성을 어렵게 자세한 하지만 대부분의 엔터프라이즈 시스템에는 고정된 역할을 사용 하는 대신 사용 권한을 부여 해야 합니다. <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md). -->다음 차트에서는 각 고정된 데이터베이스 역할과 연관 된 사용 권한을 보여 줍니다. 이 SQL Server 그래픽에 대 한 모든 권한을 사용할 수 있습니다 (또는 필요한) 없는 AP에서.  
  
![APS 보안 고정 데이터베이스 역할](./media/pdw-permissions/APS_security_fixed_db_roles.png "APS_security_fixed_db_roles")  
  
### <a name="related-content"></a>관련 내용  
  
-   사용자 정의 역할을 만들려면 참조 [CREATE ROLE](../t-sql/statements/create-role-transact-sql.md)합니다.  
  
  
## <a name="fixed-server-roles"></a>고정 서버 역할
고정된 서버 역할은 SQL Server에서 자동으로 생성 됩니다. SQL Server PDW에 SQL Server 고정 서버 역할의 제한 된 구현이 있습니다. 만 **sysadmin** 및 **공용** 구성원으로 사용자 로그인이 포함 되어 있습니다. 합니다 **setupadmin** 하 고 **dbcreator** SQL Server PDW에서 내부적으로 사용 됩니다. 추가 멤버를 추가 하거나 모든 역할에서 제거 될 수 없습니다.  
  
### <a name="sysadmin-fixed-server-role"></a>sysadmin 고정 서버 역할  
**sysadmin** 고정 서버 역할의 멤버는 서버에서 모든 작업을 수행할 수 있습니다. **sa** 로그인의 유일한 멤버인 합니다 **sysadmin** 고정된 서버 역할입니다. 추가 로그인을 추가할 수 없습니다는 **sysadmin** 고정된 서버 역할입니다. **CONTROL SERVER** 사용 권한 부여는 **sysadmin** 고정 서버 역할의 멤버 자격을 갖는 것과 비슷합니다. 다음 예에서는 권한을 부여 합니다 **CONTROL SERVER** 로그인 권한이 라는 fay에 게 합니다.  
  
```sql  
USE master;  
GO  
GRANT CONTROL SERVER TO Fay;  
```  
  
> [!IMPORTANT]  
> 합니다 **CONTROL SERVER** 권한이 SQL Server PDW의 거의 완벽 한 제어를 제공 합니다. 가능 하면 보다 세부적인 권한을 로그인을 대신 제공 합니다. 예를 들어, 권한을 부여 합니다 **VIEW SERVER STATE**, **ALTER ANY LOGIN**합니다 **VIEW ANY DATABASE**, 또는 **CREATE ANY DATABASE** 사용 권한입니다.  
  
### <a name="public-server-role"></a>public 서버 역할  
SQL Server PDW에 연결할 수 있는 모든 로그인의 멤버인 합니다 **공용** 서버 역할입니다. 모든 로그인에 부여 된 사용 권한을 상속 **공용** 모든 개체에 있습니다. 할당할 **공용** 개체를 모든 사용자에 게 사용할 수 하려는 경우 개체에 대 한 권한. 멤버 자격을 변경할 수 없습니다는 **공용** 역할입니다.  
  
> [!NOTE]  
> **공용** 다른 역할과 다른 방식으로 구현 됩니다. 모든 서버 보안 주체는 공용,의 멤버 자격 멤버를 **공용** 역할에 나열 되지 합니다 **sys.server_role_members** DMV.  
  
### <a name="fixed-server-roles-vs-granting-permissions"></a>고정된 서버 역할 및 권한 부여  
고정된 서버 역할과 고정된 데이터베이스 역할의 시스템은는 1980's에서 발생 하는 레거시 시스템입니다. 고정된 역할은 계속 지원 하며 몇 가지 사용자가 보안 요구 사항은 간단 하는 환경에서 유용 합니다. SQL Server 2005 부터는 권한을 부여 하는 자세한 시스템 생성 되었습니다. 이 새 시스템은 세부적인 모두 권한 부여 및 거부에 대 한 더 많은 옵션을 제공 합니다. 보다 세분화 된 시스템의 추가 복잡성을 어렵게 자세한 하지만 대부분의 엔터프라이즈 시스템에는 고정된 역할을 사용 하는 대신 사용 권한을 부여 해야 합니다. <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  -->  
  
## <a name="related-topics"></a>관련 항목  
  
- [사용 권한 부여](grant-permissions.md)

<!-- MISSING LINKS
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->

