---
title: GRANT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GRANT_TSQL
- GRANT
dev_langs:
- TSQL
helpviewer_keywords:
- granting permissions [SQL Server], GRANT statement
- schema-level securables [SQL Server]
- GRANT statement
- cross-database permissions
- GRANT statement, about GRANT statement
- server-level securables [SQL Server]
- database-level securables [SQL Server]
- permissions [SQL Server], granting
ms.assetid: a760c16a-4d2d-43f2-be81-ae9315f38185
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e23c4794b00daca7a228a3cd189835fcdf32628a
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68050654"
---
# <a name="grant-transact-sql"></a>GRANT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  보안 주체에 보안 개체에 대한 사용 권한을 부여합니다.  일반적인 개념은 GRANT \<사용 권한> ON \<개체> TO \<사용자, 로그인 또는 그룹>입니다. 사용 권한에 대한 일반적인 설명은 [사용 권한&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-database-engine.md)을 참조하세요.  
  
 ![문서 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "문서 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Simplified syntax for GRANT  
GRANT { ALL [ PRIVILEGES ] }  
      | permission [ ( column [ ,...n ] ) ] [ ,...n ]  
      [ ON [ class :: ] securable ] TO principal [ ,...n ]   
      [ WITH GRANT OPTION ] [ AS principal ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
GRANT   
    <permission> [ ,...n ]  
    [ ON [ <class_type> :: ] securable ]   
    TO principal [ ,...n ]  
    [ WITH GRANT OPTION ]  
[;]  
  
<permission> ::=  
{ see the tables below }  
  
<class_type> ::=  
{  
      LOGIN  
    | DATABASE  
    | OBJECT  
    | ROLE  
    | SCHEMA  
    | USER  
}  
```  
  
## <a name="arguments"></a>인수  
 ALL  
 이 옵션은 사용되지 않으며 이전 버전과의 호환성을 위해서만 유지 관리되고 모든 가능한 사용 권한을 부여하지 않습니다. ALL을 부여하는 것은 다음 사용 권한을 부여하는 것과 동일합니다. 
  
-   보안 개체가 데이터베이스인 경우 ALL은 BACKUP DATABASE, BACKUP LOG, CREATE DATABASE, CREATE DEFAULT, CREATE FUNCTION, CREATE PROCEDURE, CREATE RULE, CREATE TABLE 및 CREATE VIEW를 의미합니다.  
  
-   보안 개체가 스칼라 함수인 경우 ALL은 EXECUTE 및 REFERENCES를 의미합니다.  
  
-   보안 개체가 테이블 반환 함수인 경우 ALL은 DELETE, INSERT, REFERENCES, SELECT 및 UPDATE를 의미합니다.  
  
-   보안 개체가 저장 프로시저인 경우 ALL은 EXECUTE를 의미합니다.  
  
-   보안 개체가 테이블인 경우 ALL은 DELETE, INSERT, REFERENCES, SELECT 및 UPDATE를 의미합니다.  
  
-   보안 개체가 뷰인 경우 ALL은 DELETE, INSERT, REFERENCES, SELECT 및 UPDATE를 의미합니다.  
  
PRIVILEGES  
 ISO 호환성을 위해 포함됩니다. ALL의 동작을 변경하지 않습니다.  
  
*permission*  
 사용 권한의 이름입니다. 아래 나열된 하위 항목에서는 보안 개체에 대한 사용 권한의 올바른 매핑에 대해 설명합니다.  
  
*column*  
 사용 권한을 부여할 테이블의 열 이름을 지정합니다. 괄호()가 필요합니다.  
  
*class*  
 사용 권한을 부여할 보안 개체의 클래스를 지정합니다. 범위 한정자 **::** 가 필요합니다.  
  
*securable*  
 사용 권한을 부여할 보안 개체를 지정합니다.  
  
TO *principal*  
 보안 주체의 이름입니다. 보안 개체에 대한 사용 권한을 부여할 수 있는 대상 보안 주체는 보안 개체에 따라 달라집니다. 유효한 조합에 대해서는 아래에 나열된 하위 항목을 참조하세요.  
  
GRANT OPTION  
 지정된 사용 권한을 다른 보안 주체에게 부여할 수 있는 권한도 피부여자에게 제공됨을 나타냅니다.  
  
AS *principal*  
 권한의 부여자로 기록된 보안 주체가 해당 명령문을 실행하는 사용자 이외의 보안 주체여야 한다는 것을 표시하려면 AS principal 절을 사용합니다. 예를 들어 Mary라는 사용자가 principal_id 12이고 Raul이라는 사용자는 principal 15라고 가정해 보겠습니다. Mary가 `GRANT SELECT ON OBJECT::X TO Steven WITH GRANT OPTION AS Raul;`을 실행합니다. 이제 sys.database_permissions 테이블에 실제로 사용자 13(Mary)이 명령문을 실행했지만 grantor_prinicpal_id가 15(Raul)임이 표시됩니다.

권한 체인을 명시적으로 정의해야 하는 경우가 아니면 AS 절은 사용하지 않는 것이 좋습니다. 자세한 내용은 [사용 권한(데이터베이스 엔진)](../../relational-databases/security/permissions-database-engine.md)의 **사용 권한 검사 알고리즘 요약** 섹션을 참조하세요.

이 명령문에 AS를 사용한다고 해서 다른 사용자로 가장하는 기능을 의미하는 것은 아닙니다. 
  
## <a name="remarks"></a>설명  
 GRANT 문의 전체 구문은 복잡합니다. 위의 구문 다이어그램은 구조를 강조하기 위해 단순하게 표현되었습니다. 특정 보안 개체에 대한 사용 권한을 부여하는 완전한 구문은 아래에 나열된 문서에서 설명합니다.  
  
 REVOKE 문을 사용하여 부여된 사용 권한을 제거할 수 있으며 DENY 문을 사용하여 보안 주체가 GRANT를 통해 특정 사용 권한을 얻지 못하도록 막을 수 있습니다.  
  
 사용 권한을 부여하면 지정된 보안 개체에 대한 이 사용 권한의 DENY 또는 REVOKE가 제거됩니다. 보안 개체가 포함된 상위 범위에서 동일한 사용 권한이 거부되면 DENY가 우선 적용됩니다. 그러나 상위 범위에서 부여된 사용 권한을 취소하는 것은 우선 적용되지 않습니다.  
  
 데이터베이스 수준 사용 권한은 지정된 데이터베이스 범위 내에서 부여됩니다. 사용자가 다른 데이터베이스에 있는 개체에 대한 사용 권한을 필요로 하는 경우에는 다른 데이터베이스에서 사용자 계정을 만들거나 다른 데이터베이스와 현재 데이터베이스에 대해 사용자 계정 액세스를 부여하세요.  
  
> [!CAUTION]  
>  테이블 수준의 DENY는 열 수준의 GRANT보다 우선하지 않습니다. 사용 권한 계층에서의 이러한 불일치는 이전 버전과의 호환성을 위해 유지되었으며 후속 릴리스에서 제거될 예정입니다.  
  
 sp_helprotect 시스템 저장 프로시저는 데이터베이스 수준 보안 개체에 대한 사용 권한을 보고합니다.  
  
## <a name="with-grant-option"></a>WITH GRANT OPTION  
 **부여**... **WITH GRANT OPTION**은 사용 권한을 받는 보안 주체에게 다른 보안 계정에 지정된 권한을 부여할 수 있는 권한이 부여되도록 지정합니다. 사용 권한을 받는 보안 주체가 역할 또는 Windows 그룹인 경우, 그룹 또는 역할의 멤버가 아닌 사용자에게 개체 권한을 추가로 부여해야 할 때는 **AS** 절을 사용해야 합니다. 그룹 또는 역할이 아니라 사용자만 **GRANT** 문을 실행할 수 있으므로 그룹 또는 역할의 특정 멤버는 사용 권한을 부여할 때 **AS** 절을 사용하여 역할 또는 그룹 멤버 자격을 명시적으로 호출해야 합니다. 다음 예에서는 역할 또는 Windows 그룹에 부여될 때 **WITH GRANT OPTION**이 사용되는 방법을 보여 줍니다.  
  
```  
-- Execute the following as a database owner  
GRANT EXECUTE ON TestProc TO TesterRole WITH GRANT OPTION;  
EXEC sp_addrolemember TesterRole, User1;  
-- Execute the following as User1  
-- The following fails because User1 does not have the permission as the User1  
GRANT EXECUTE ON TestMe TO User2;  
-- The following succeeds because User1 invokes the TesterRole membership  
GRANT EXECUTE ON TestMe TO User2 AS TesterRole;  
```  
  
## <a name="chart-of-sql-server-permissions"></a>SQL Server 사용 권한 차트  
 pdf 형식의 모든 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 권한에 대한 포스터 크기의 차트를 보려면 [https://aka.ms/sql-permissions-poster](https://aka.ms/sql-permissions-poster)를 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 사용 권한을 부여한 사용자 또는 AS 옵션으로 지정한 보안 주체에게 GRANT OPTION을 통한 사용 권한이 있거나 부여할 사용 권한을 포함하는 상위 사용 권한이 있어야 합니다. AS 옵션을 사용하는 경우 추가 요구 사항이 적용됩니다. 자세한 내용은 보안 개체 관련 문서를 참조하세요.  
  
 개체 소유자는 소유하고 있는 개체에 대한 사용 권한을 부여할 수 있습니다. 보안 개체에 대한 CONTROL 사용 권한을 가진 보안 주체는 해당 보안 개체에 대한 사용 권한을 부여할 수 있습니다.  
  
 sysadmin 고정 서버 역할의 멤버와 같이 CONTROL SERVER 사용 권한이 부여된 사용자는 서버의 모든 보안 개체에 대한 사용 권한을 부여할 수 있습니다. db_owner 고정 데이터베이스 역할의 멤버와 같이 데이터베이스에 대한 CONTROL 사용 권한이 부여된 사용자는 데이터베이스의 모든 보안 개체에 대한 사용 권한을 부여할 수 있습니다. 스키마에 대한 CONTROL 권한이 부여된 사용자는 스키마 내의 모든 개체에 대한 사용 권한을 부여할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 표에는 보안 개체와 보안 개체별 구문을 설명하는 문서 목록이 정리되어 있습니다.  
  
|||  
|-|-|  
|애플리케이션 역할|[GRANT 데이터베이스 보안 주체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)|  
|어셈블리|[GRANT 어셈블리 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-assembly-permissions-transact-sql.md)|  
|비대칭 키|[GRANT 비대칭 키 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-asymmetric-key-permissions-transact-sql.md)|  
|가용성 그룹|[GRANT 가용성 그룹 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-availability-group-permissions-transact-sql.md)|  
|인증서|[GRANT 인증서 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-certificate-permissions-transact-sql.md)|  
|계약|[GRANT Service Broker 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|데이터베이스|[GRANT 데이터베이스 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md)|
|데이터베이스 범위 자격 증명|[GRANT 데이터베이스 범위 자격 증명(Transact-SQL)](../../t-sql/statements/grant-database-scoped-credential-transact-sql.md)|  
|엔드포인트|[GRANT 엔드포인트 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)|  
|전체 텍스트 카탈로그|[GRANT 전체 텍스트 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-full-text-permissions-transact-sql.md)|  
|전체 텍스트 중지 목록|[GRANT 전체 텍스트 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-full-text-permissions-transact-sql.md)|  
|함수|[GRANT 개체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|로그인|[GRANT 서버 보안 주체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-server-principal-permissions-transact-sql.md)|  
|메시지 유형|[GRANT Service Broker 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|Object|[GRANT 개체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|큐|[GRANT 개체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|원격 서비스 바인딩|[GRANT Service Broker 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|역할|[GRANT 데이터베이스 보안 주체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)|  
|라우팅|[GRANT Service Broker 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|스키마|[GRANT 스키마 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-schema-permissions-transact-sql.md)|  
|검색 속성 목록|[GRANT 검색 속성 목록 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-search-property-list-permissions-transact-sql.md)|  
|서버|[GRANT 서버 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-server-permissions-transact-sql.md)|  
|서비스|[GRANT Service Broker 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|저장 프로시저|[GRANT 개체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|대칭 키|[GRANT 대칭 키 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-symmetric-key-permissions-transact-sql.md)|  
|동의어|[GRANT 개체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|시스템 개체|[GRANT 시스템 개체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-system-object-permissions-transact-sql.md)|  
|테이블|[GRANT 개체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Type|[GRANT 형식 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-type-permissions-transact-sql.md)|  
|사용자|[GRANT 데이터베이스 보안 주체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)|  
|보기|[GRANT 개체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|XML 스키마 컬렉션|[GRANT XML 스키마 컬렉션 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-xml-schema-collection-permissions-transact-sql.md)|  
  
## <a name="see-also"></a>참고 항목  
 [DENY&#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [REVOKE&#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [sp_addlogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_adduser&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_changedbowner&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [sp_dropuser&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_helprotect&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [sp_helpuser&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)  
  
  
