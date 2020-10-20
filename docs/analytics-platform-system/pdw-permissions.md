---
title: 사용 권한
description: 이 문서에서는 병렬 데이터 웨어하우스의 데이터베이스 사용 권한을 관리 하기 위한 요구 사항 및 옵션을 설명 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 499ac56d8a462f62dac92b97654a9ace12bd356e
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257449"
---
# <a name="managing-permissions-in-parallel-data-warehouse"></a>병렬 데이터 웨어하우스의 사용 권한 관리
이 문서에서는 SQL Server PDW에 대 한 데이터베이스 사용 권한을 관리 하기 위한 요구 사항 및 옵션을 설명 합니다.

## <a name="database-engine-permission-basics"></a><a name="BackupRestoreBasics"></a>데이터베이스 엔진 권한 기본 사항
SQL Server PDW에 대 한 데이터베이스 엔진 권한은 로그인을 통해 서버 수준에서 관리 되 고 데이터베이스 사용자 및 사용자 정의 데이터베이스 역할을 통해 데이터베이스 수준에서 관리 됩니다.

**로그인** 로그인은 SQL Server PDW에 로그온 하기 위한 개별 사용자 계정입니다. SQL Server PDW는 Windows 인증 및 SQL Server 인증을 사용 하 여 로그인을 지원 합니다.  Windows 인증 로그인은 SQL Server PDW에서 신뢰 하는 모든 도메인의 windows 사용자 또는 Windows 그룹 일 수 있습니다. SQL Server 인증 로그인은 SQL Server PDW에 의해 정의 되 고 인증 되며 암호를 지정 하 여 만들어야 합니다.

**Sa** 로그인과 같은 **sysadmin** 고정 서버 역할의 멤버는 데이터베이스 사용자에 매핑되지 않고도 데이터베이스에 연결할 수 있습니다. **Dbo** 사용자에 게 매핑됩니다. 데이터베이스의 소유자도 **dbo** 사용자로 매핑됩니다.

**서버 역할** 편리한 서버 수준 권한 그룹을 제공 하는 미리 구성 된 역할 집합을 사용 하는 네 가지 특수 서버 역할이 있습니다. **Sysadmin**, **mediumrc**, **LargeRC**및 **XLargeRCfixed** 서버 역할은 현재 SQL Server PDW에서 구현 되는 유일한 서버 역할입니다. **Sa** 로그인은 **sysadmin** 고정 서버 역할의 유일한 멤버 이며 추가 로그인은 **sysadmin** 역할에 추가 될 수 없습니다. 로그인에는 **sysadmin** 고정 서버 역할과 유사 하지만 동일 하지 않은 **제어 서버** 권한이 부여 될 수 있습니다. [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md) 을 사용 하 여 다른 서버 역할에 멤버를 추가 합니다. SQL Server PDW는 사용자 정의 서버 역할을 지원 하지 않습니다.

**데이터베이스 사용자** 로그인에는 데이터베이스에 데이터베이스 사용자를 만들고 해당 데이터베이스 사용자를 로그인에 매핑하여 데이터베이스에 대 한 액세스 권한이 부여 됩니다. 일반적으로 데이터베이스 사용자 이름은 로그인 이름과 동일하지만 반드시 그래야 하는 것은 아닙니다. 각 데이터베이스 사용자는 단일 로그인에 매핑됩니다. 하나의 로그인을 데이터베이스의 한 사용자에만 매핑할 수 있지만 여러 데이터베이스에서 데이터베이스 사용자로 매핑할 수 있습니다.

**고정 데이터베이스 역할** 고정 데이터베이스 역할은 편리한 데이터베이스 수준 권한 그룹을 제공 하는 미리 구성 된 역할 집합입니다. [Sp_addrolemember](../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) 프로시저를 사용 하 여 데이터베이스 사용자 및 사용자 정의 데이터베이스 역할을 고정 데이터베이스 역할에 추가할 수 있습니다. 고정 데이터베이스 역할에 대 한 자세한 내용은 [고정 데이터베이스 역할](#fixed-database-roles)을 참조 하세요.

**사용자 정의 데이터베이스 역할** **역할 만들기** 권한이 있는 사용자는 일반적인 권한이 있는 사용자 그룹을 나타내는 새 사용자 정의 데이터베이스 역할을 만들 수 있습니다. 권한 관리 및 모니터링을 간소화하기 위해 일반적으로 권한은 전체 역할에 부여되거나 거부됩니다.

**GRANT** 문을 사용 하 여 보안 주체 (로그인, 사용자 및 역할)에 게 권한을 부여 합니다. **DENY** 명령을 사용 하면 사용 권한이 명시적으로 거부 됩니다. 이전에 부여 하거나 거부 한 권한은 **REVOKE** 문을 사용 하 여 제거 됩니다. 권한은 누적적입니다. 즉, 사용자는 사용자, 로그인 및 그룹 멤버 자격에 부여된 모든 권한을 받습니다. 그러나 권한 거부는 모든 부여를 재정의합니다. <!-- MISSING LINKS (For information, syntax, and available permissions with these commands, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md)).  -->

다음 예제에서는 권한 구성의 일반적인 방법 및 권장 방법을 나타냅니다.

1.  Windows 인증을 사용 하는 경우 SQL Server PDW에 연결할 각 Windows 사용자 또는 Windows 그룹에 대 한 로그인을 만듭니다. SQL Server 인증을 사용 하는 경우 SQL Server PDW에 연결할 각 사용자에 대 한 로그인을 만듭니다.

2.  모든 필요한 데이터베이스에서 각 로그인에 대 한 데이터베이스 사용자를 만듭니다.

3.  각각 유사한 기능을 나타내는 하나 이상의 사용자 정의 데이터베이스 역할을 만듭니다. 예를 들어 재무 분석가 및 판매 분석가를 만듭니다.

4.  하나 이상의 사용자 정의 데이터베이스 역할에 데이터베이스 사용자를 추가 합니다.

5.  사용자 정의 데이터베이스 역할에 권한을 부여합니다.

로그인은 서버 수준 개체 이며 [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)표시 하 여 나열할 수 있습니다. 서버 보안 주체에는 서버 수준 사용 권한만 부여할 수 있습니다.

사용자 및 데이터베이스 역할은 데이터베이스 수준 개체 이며 [sys.database_principals](../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)표시 하 여 나열할 수 있습니다. 데이터베이스 수준 사용 권한만 데이터베이스 보안 주체에 게 부여할 수 있습니다.

## <a name="default-permissions"></a><a name="BackupTypes"></a>기본 사용 권한
다음 목록에서는 기본 사용 권한을 설명합니다.

-   Using **CREATE login** 문에 의해 로그인이 생성 되 면 로그인이 로그인을 허용 하는 **connect SQL** 권한을 수신 하 여 SQL Server PDW에 연결 합니다.

-   **CREATE user** 문을 사용 하 여 데이터베이스 사용자를 만들 때 사용자는 **데이터베이스에 연결::** _<database_name>_ 권한을 받으며 로그인이 사용자로 해당 데이터베이스에 연결할 수 있습니다.

-   암시적 사용 권한은 명시적 사용 권한 으로부터 상속 되기 때문에 PUBLIC 역할을 비롯 한 모든 보안 주체에는 기본적으로 명시적 또는 암시적 사용 권한이 없습니다. 따라서 명시적 사용 권한이 없으면 암시적 사용 권한이 없을 수도 있습니다.

-   로그인이 개체가 나 데이터베이스의 소유자가 되 면 해당 로그인에는 항상 개체 또는 데이터베이스에 대 한 모든 권한이 포함 됩니다. 소유권 권한은 명시적 사용 권한으로 표시 되지 않습니다. **GRANT**, **REVOKE**및 **DENY** 문은 소유권 권한에 영향을 주지 않습니다. [ALTER authorization](../t-sql/statements/alter-authorization-transact-sql.md) 문을 사용 하 여 소유권을 변경할 수 있습니다.

-   sa 로그인은 어플라이언스에 대한 모든 사용 권한을 가집니다. 소유권 사용 권한과 마찬가지로 sa 사용 권한도 변경할 수 없으며 명시적 사용 권한으로 표시되지 않습니다. **GRANT**, **REVOKE**및 **DENY** 문은 sa 사용 권한에 영향을 주지 않습니다.

-   PUBLIC 서버 역할은 기본적으로 권한을 받지 않으며 다른 서버 역할의 사용 권한을 상속 하지 않습니다. PUBLIC 서버 역할에는 **GRANT**, **REVOKE**및 **DENY** 문을 사용 하 여 명시적 사용 권한을 지정할 수 있습니다.

-   트랜잭션은 사용 권한이 필요 하지 않습니다. 모든 보안 주체는 **BEGIN TRANSACTION**, **COMMIT**및 **ROLLBACK** TRANSACTION 명령을 실행할 수 있습니다. 그러나 보안 주체에는 트랜잭션 내에서 각 문을 실행할 수 있는 적절 한 권한이 있어야 합니다.

-   **USE** 문은 사용 권한이 필요하지 않습니다. 모든 보안 주체는 모든 데이터베이스에서 **use** 문을 실행할 수 있습니다. 그러나 데이터베이스에 액세스 하려면 데이터베이스에 사용자 보안 주체가 있거나 게스트 사용자를 사용 하도록 설정 해야 합니다.

### <a name="the-public-role"></a>PUBLIC 역할
모든 새 어플라이언스 로그인이 자동으로 PUBLIC 역할에 속합니다. PUBLIC 서버 역할에는 다음과 같은 특징이 있습니다.

-   PUBLIC 서버 역할에는 기본적으로 권한이 없습니다.

-   모든 보안 주체는 PUBLIC 서버 역할의 멤버이 고 PUBLIC 서버 역할은 다른 서버 역할의 멤버가 아닙니다.

-   PUBLIC 서버 역할은 암시적 권한을 상속할 수 없습니다. PUBLIC 역할에 부여 된 모든 사용 권한은 명시적으로 부여 되어야 합니다.

## <a name="determining-permissions"></a><a name="BackupProc"></a>권한 확인
로그인에 특정 작업을 수행할 수 있는 권한이 있는지 여부는 사용자가 멤버로 속해 있는 로그인, 사용자 및 역할에 부여 되거나 거부 된 사용 권한에 따라 달라 집니다. 서버 수준 권한 ( **로그인 만들기** 및 서버 **상태 보기**)은 서버 수준 보안 주체 (로그인)에서 사용할 수 있습니다. 데이터베이스 수준 사용 권한 (예: 테이블에서 **선택** 또는 프로시저에서 **실행** )은 데이터베이스 수준 보안 주체 (사용자 및 데이터베이스 역할)에 사용할 수 있습니다.

### <a name="implicit-and-explicit-permissions"></a>암시적 및 명시적 사용 권한
*명시적 사용 권한*은 **GRANT** 또는 **DENY**문으로 보안 주체에게 주어진 **GRANT** 또는 **DENY** 사용 권한입니다. 데이터베이스 수준 사용 권한은 [sys.database_permissions](../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) 뷰에 나열 됩니다. 서버 수준 사용 권한은 [sys.server_permissions](../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) 뷰에 나열 됩니다.

*암시적 권한은* 보안 주체 (로그인 또는 서버 역할)가 상속 하는 **GRANT** 또는 **DENY** 권한입니다. 권한은 다음과 같은 방법으로 상속 될 수 있습니다.

-   보안 주체가 명시적 **부여** 또는 **거부** 권한이 없는 경우에도 보안 주체가 역할의 멤버인 경우에는 보안 주체가 역할의 권한을 상속할 수 있습니다.

-   주 서버에서 개체의 부모 범위 (예: 테이블의 스키마 또는 전체 데이터베이스에 대 한 사용 권한)에 대 한 사용 권한이 있는 경우 보안 주체가 하위 개체 (예: 테이블)에 대 한 사용 권한을 상속할 수 있습니다.

-   보안 주체는 하위 권한을 포함 하는 사용 권한을 사용 하 여 권한을 상속할 수 있습니다. 예를 들어 **ALTER ANY user** 권한에는 **CREATE USER** 및 **alter ON user::** 권한이 모두 포함 됩니다 _<name>_ .

### <a name="determining-permissions-when-performing-actions"></a>작업 수행 시 사용 권한 결정
보안 주체에 할당할 권한을 결정 하는 프로세스는 복잡 합니다. 보안 주체는 여러 역할의 멤버가 될 수 있고 사용 권한이 역할 계층 구조의 여러 수준에서 전달 될 수 있으므로 암시적 사용 권한을 결정할 때 복잡성이 발생 합니다.

다음 목록에서는 사용 권한을 결정 하는 일반적인 규칙에 대해 설명 합니다.

-   소유권은 권한을 암시 합니다.

    개체 소유자에 게는 개체에 대 한 모든 권한이 있습니다. 마찬가지로 데이터베이스 소유자에 게는 데이터베이스에 대 한 모든 사용 권한과 데이터베이스의 개체에 대 한 모든 사용 권한이 있습니다. 이러한 권한은 변경할 수 없습니다.

-   서버 역할 멤버 자격 계층의 여러 수준에서 사용 권한을 상속할 수 있습니다.

    예를 들어 다음과 같은 경우를 가정 합니다.

    -   로그인 David는 데이터베이스 역할 PerfAnalysts의 멤버입니다.

    -   PerfAnalysts는 데이터베이스 역할 프로덕션의 멤버입니다.

    -   David 및 PerfAnalysts는 Customer 테이블에 대 한 **SELECT** 권한이 없습니다. 사용 권한이 해지 되었거나 명시적으로 부여 되지 않았습니다.

    -   프로덕션에는 Customer 테이블에 대 한 **SELECT** 권한이 있습니다.

    이 경우 PerfAnalysts는 프로덕션에서 Customer 테이블에 대 한 **grant** 권한을 상속 하 고 David는 프로덕션에서 customer 테이블에 대 한 **grant** 권한을 상속 합니다.

-   **DENY** 재정의는 사용 권한이 충돌할 때 **권한을 부여** 합니다.

    예를 들어, 로그인 David에 게 Customer 테이블에 대 한 권한이 없고 customer 테이블에 대 한 **DENY** 권한이 있는 Dbgroup1 및 customer 테이블에 대 한 **GRANT** 권한이 있는 dbgroup2 라는 두 개의 데이터베이스 역할의 멤버인 경우를 가정 합니다. 이 경우 David는 Customer 테이블에 대 한 **DENY** 권한을 상속 합니다. 역할이 명시적 또는 암시적으로 권한을 획득 했는지 여부입니다.

### <a name="auditing-permissions"></a>감사 권한
사용자의 권한을 조사 하려면 다음을 확인 합니다.

-   다음 쿼리를 실행 하 여 시스템 관리자 인 로그인을 확인 합니다.

    ```sql
    SELECT SPLogins.name, 'is a member of ', SPRoles.name 
    FROM sys.server_role_members AS SRM 
    JOIN sys.server_principals AS SPRoles 
        ON SRM.role_principal_id = SPRoles.principal_id 
    JOIN sys.server_principals AS SPLogins 
        ON SRM.member_principal_id = SPLogins.principal_id;
    ```

-   다음 쿼리를 실행 하 여 명시적 권한이 부여 된 로그인을 확인 합니다.

    ```sql
    SELECT name, 'has the ', state_desc , permission_name, ' permission'
    FROM sys.server_permissions AS SP
    JOIN sys.server_principals AS SPRoles 
        ON SP.grantee_principal_id = SPRoles.principal_id;
    ```

-   사용자 데이터베이스에서 다음 쿼리를 실행 하 여 데이터베이스 역할의 멤버에 해당 하는 데이터베이스 사용자를 확인 합니다.

    ```sql
    SELECT DPUsers.name, 'is a member of ', DPRoles.name  
    FROM sys.database_role_members AS DRM
    JOIN sys.database_principals AS DPRoles 
        ON DRM.role_principal_id = DPRoles.principal_id
    JOIN sys.database_principals AS DPUsers
        ON DRM.member_principal_id = DPUsers.principal_id;
    ```

-   사용자 데이터베이스에서 다음 쿼리를 실행 하 여 특정 권한이 부여 되거나 거부 된 데이터베이스 사용자 및 역할을 확인 합니다. Major_id에서 설명 하는 항목을 식별 하려면 sys. objects 및 sys.debug와 같은 추가 뷰를 쿼리해야 합니다.

    ```sql
    SELECT DPUsers.name, 'has the ', permission_name, 
    'permission on the item described as class = ', class, 'id = ', major_id
    FROM sys.database_permissions AS DP
    JOIN sys.database_principals AS DPUsers
        ON DP.grantee_principal_id = DPUsers.principal_id;
    ```

## <a name="database-permissions-best-practices"></a><a name="RestoreProc"></a>데이터베이스 사용 권한 모범 사례

-   가장 세분화 된 수준에서 사용 권한을 부여 합니다. 테이블 또는 뷰 수준 사용 권한에 대 한 사용 권한을 부여 하는 것은 관리할 수 없습니다. 그러나 데이터베이스 수준에서 사용 권한을 부여 하는 것은 너무 허용 될 수 있습니다. 데이터베이스에서 스키마를 사용 하 여 작업 경계를 정의 하는 경우 스키마에 대 한 권한을 부여 하는 것이 테이블 수준과 데이터베이스 수준 간에 적절 한 손상입니다.

-   사용자나 로그인 대신 역할에 사용 권한을 부여 합니다. 사용자 대신 역할을 사용 하 여 권한을 관리 하면 사용자 또는 로그인에 대 한 사용 권한 집합을 역할으로 이동 하거나 역할에서 이동 하 여 쉽게 신속 하 게 부여 하거나 취소할 수 있습니다. 한 사용자에서 다른 사용자로 함수를 전달할 때 역할 멤버 자격을 변경 하는 동안 권한은 역할 수준에서 그대로 유지 될 수 있습니다.

-   작업 함수를 기반으로 역할에 권한을 부여 하 고 작업을 수행 하는 회사 그룹에 따라 작업 함수 역할을 결합 하는 상위 수준 그룹 역할에 권한을 부여 합니다.

-   모든 최종 사용자에 게는 고유한 로그인이 있어야 합니다. 사용자가 로그인을 공유 하는 것을 허용 하지 않습니다. 각 사용자에 대 한 로그인을 제공 하 여 감사 내역을 확인 하 고 권한 관리를 간소화 합니다.

## <a name="fixed-database-roles"></a>고정 데이터베이스 역할
SQL Server는 서버에 대 한 사용 권한을 관리 하는 데 도움이 되는 미리 구성 된 (고정) 데이터베이스 수준 역할을 제공 합니다. 미리 구성 된 역할은 할당 된 사용 권한을 변경할 수 없다는 것을 수정 합니다. 사용자 정의 데이터베이스 역할을 만들 수도 있습니다. 사용자 정의 데이터베이스 역할에 할당 된 사용 권한을 변경할 수 있습니다.

역할은 다른 보안 주체를 그룹화 하는 보안 주체입니다. 데이터베이스 역할은 데이터베이스 전체에서 사용 권한 범위에 있습니다. 데이터베이스 사용자 및 다른 데이터베이스 역할은 데이터베이스 역할의 멤버로 추가할 수 있습니다. 고정 데이터베이스 역할은 서로 추가할 수 없습니다. *역할* 은 Windows 운영 체제의 *그룹* 과 같습니다.

9 개의 고정 데이터베이스 역할이 있습니다.

-   **db_owner**

-   **db_securityadmin**

-   **db_accessadmin**

-   **db_backupoperator**

-   **db_ddladmin**

-   **db_datawriter**

-   **db_datareader**

-   **db_denydatawriter**

-   **db_denydatareader**

### <a name="permissions-of-the-fixed-database-roles"></a>고정 데이터베이스 역할의 사용 권한
고정 서버 역할 및 고정 데이터베이스 역할의 시스템은 1980에서 시작 된 레거시 시스템입니다. 고정 역할은 계속 지원 되며, 사용자가 적고 보안 요구 사항이 단순한 환경에서 유용 합니다. SQL Server 2005부터 사용 권한을 부여 하는 보다 세부적인 시스템을 만들었습니다. 이 새로운 시스템은 보다 세부적인 사용 권한을 부여 하 고 거부 하는 더 많은 옵션을 제공 합니다. 더 세부적인 시스템의 복잡성이 복잡할수록 학습 하기가 어려워집니다. 하지만 대부분의 엔터프라이즈 시스템은 고정 역할을 사용 하는 대신 권한을 부여 해야 합니다. <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md). -->다음 차트에서는 각 고정 데이터베이스 역할과 관련 된 사용 권한을 보여 줍니다. 이 SQL Server 그래픽의 모든 권한은 AP에서 사용할 수 있거나 필요 하지 않습니다.

![APS 보안 고정 데이터베이스 역할](./media/pdw-permissions/APS_security_fixed_db_roles.png "APS_security_fixed_db_roles")

### <a name="related-content"></a>관련 내용

-   사용자 정의 역할을 만들려면 [역할 만들기](../t-sql/statements/create-role-transact-sql.md)를 참조 하세요.


## <a name="fixed-server-roles"></a>고정 서버 역할
고정 서버 역할은 SQL Server에 의해 자동으로 생성 됩니다. SQL Server PDW는 고정 서버 역할 SQL Server의 구현이 제한적입니다. **Sysadmin** 및 **공용** 만 사용자 로그인을 멤버로 가집니다. **Setupadmin** 및 **dbcreator** 역할은 SQL Server PDW에서 내부적으로 사용 됩니다. 역할에서 추가 멤버를 추가 하거나 제거할 수 없습니다.

### <a name="sysadmin-fixed-server-role"></a>sysadmin 고정 서버 역할
**sysadmin** 고정 서버 역할의 멤버는 서버에서 모든 작업을 수행할 수 있습니다. **Sa** 로그인은 **sysadmin** 고정 서버 역할의 유일한 멤버입니다. 추가 로그인은 **sysadmin** 고정 서버 역할에 추가할 수 없습니다. **CONTROL SERVER** 사용 권한 부여는 **sysadmin** 고정 서버 역할의 멤버 자격을 갖는 것과 비슷합니다. 다음 예에서는 Fay 라는 로그인에 대 한 **CONTROL SERVER** 권한을 부여 합니다.

```sql
USE master;
GO
GRANT CONTROL SERVER TO Fay;
```

> [!IMPORTANT]
> **CONTROL SERVER** 권한은 SQL Server PDW를 거의 완전히 제어 합니다. 가능 하면 대신 로그인에 보다 세부적인 사용 권한을 제공 합니다. 예를 들어 **뷰 서버 상태**를 부여 하 고, 모든 **로그인을 변경**하 고, **모든 데이터베이스를 보거나**, 데이터베이스 사용 권한을 **만듭니다** .

### <a name="public-server-role"></a>public 서버 역할
SQL Server PDW에 연결할 수 있는 모든 로그인은 **public** 서버 역할의 멤버입니다. 모든 로그인은 모든 개체에 대해 **public** 으로 부여 된 사용 권한을 상속 합니다. 개체를 모든 사용자가 사용할 수 있도록 하려는 경우에만 개체에 대 한 **public** 권한을 할당 합니다. **Public** 역할의 멤버 자격은 변경할 수 없습니다.

> [!NOTE]
> **public** 은 다른 역할과 다르게 구현 됩니다. 모든 서버 보안 주체는 공용의 멤버 이기 때문에 **public** 역할의 멤버 자격은 **sys.server_role_members** DMV에 나열 되지 않습니다.

### <a name="fixed-server-roles-vs-granting-permissions"></a>고정 서버 역할 및 권한 부여
고정 서버 역할 및 고정 데이터베이스 역할의 시스템은 1980에서 시작 된 레거시 시스템입니다. 고정 역할은 계속 지원 되며, 사용자가 적고 보안 요구 사항이 단순한 환경에서 유용 합니다. SQL Server 2005부터 사용 권한을 부여 하는 보다 세부적인 시스템을 만들었습니다. 이 새로운 시스템은 보다 세부적인 사용 권한을 부여 하 고 거부 하는 더 많은 옵션을 제공 합니다. 더 세부적인 시스템의 복잡성이 복잡할수록 학습 하기가 어려워집니다. 하지만 대부분의 엔터프라이즈 시스템은 고정 역할을 사용 하는 대신 권한을 부여 해야 합니다. <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  -->

## <a name="related-topics"></a>관련 항목

- [권한 부여](grant-permissions.md)

<!-- MISSING LINKS
## See Also
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)
-->

