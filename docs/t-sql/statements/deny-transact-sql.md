---
title: "(Transact SQL) 거부 | Microsoft Docs"
ms.custom: 
ms.date: 05/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DENY
- DENY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- schema-level securables [SQL Server]
- security [SQL Server], denying access
- DENY statement
- permissions [SQL Server], denying
- server-level securables [SQL Server]
- inherited security settings [SQL Server]
- denying permissions [SQL Server], DENY statement
- principal security [SQL Server]
- database-level securables [SQL Server]
- denying permissions [SQL Server]
ms.assetid: c32d1e01-9ee9-4665-a516-fcfece58078e
caps.latest.revision: 48
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 08f2d3c555dceef71e331b6df8727afb5780b86b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="deny-transact-sql"></a>DENY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  보안 주체에 대한 사용 권한을 거부합니다. 보안 주체가 해당 그룹 또는 역할의 멤버 자격을 통해 사용 권한을 상속받는 것을 방지합니다. DENY 보다 우선 모든 사용 권한을 제외 하 고 거부 개체 소유자 또는 sysadmin 고정된 서버 역할의 멤버에 적용 되지 않습니다.
  **보안 정보** 멤버나 sysadmin 고정 서버 역할 및 개체 소유자는 사용 권한을 거부할 수 없습니다. "
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Simplified syntax for DENY  
DENY   { ALL [ PRIVILEGES ] } 
     | <permission>  [ ( column [ ,...n ] ) ] [ ,...n ]  
    [ ON [ <class> :: ] securable ] 
    TO principal [ ,...n ]   
    [ CASCADE] [ AS principal ]  
[;]

<permission> ::=  
{ see the tables below }  
  
<class> ::=  
{ see the tables below }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DENY   
    <permission> [ ,...n ]  
    [ ON [ <class_> :: ] securable ]   
    TO principal [ ,...n ]  
    [ CASCADE ]  
[;]  
  
<permission> ::=  
{ see the tables below }  
  
<class> ::=  
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
 이 옵션은 모든 가능한 사용 권한을 거부하지 않습니다. ALL을 거부하는 것은 다음 사용 권한을 거부하는 것과 같습니다.  
  
-   보안 개체가 데이터베이스인 경우 ALL은 BACKUP DATABASE, BACKUP LOG, CREATE DATABASE, CREATE DEFAULT, CREATE FUNCTION, CREATE PROCEDURE, CREATE RULE, CREATE TABLE 및 CREATE VIEW를 의미합니다.  
  
-   보안 개체가 스칼라 함수인 경우 ALL은 EXECUTE 및 REFERENCES를 의미합니다.  
  
-   보안 개체가 테이블 반환 함수인 경우 ALL은 DELETE, INSERT, REFERENCES, SELECT 및 UPDATE를 의미합니다.  
  
-   보안 개체가 저장 프로시저인 경우 ALL은 EXECUTE를 의미합니다.  
  
-   보안 개체가 테이블인 경우 ALL은 DELETE, INSERT, REFERENCES, SELECT 및 UPDATE를 의미합니다.  
  
-   보안 개체가 뷰인 경우 ALL은 DELETE, INSERT, REFERENCES, SELECT 및 UPDATE를 의미합니다.  
  
> [!NOTE]  
>  DENY ALL 구문은 더 이상 사용되지 않습니다. 대신 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Deny 관련 권한을 사용하세요.  
  
 PRIVILEGES  
 ISO 호환성을 위해 포함됩니다. ALL의 동작을 변경하지 않습니다.  
  
 *사용 권한*  
 사용 권한의 이름입니다. 아래 나열된 하위 항목에서는 보안 개체에 대한 사용 권한의 올바른 매핑에 대해 설명합니다.  
  
 *열*  
 사용 권한을 거부할 테이블의 열 이름을 지정합니다. 괄호()가 필요합니다.  
  
 *클래스*  
 사용 권한을 거부할 보안 개체의 클래스를 지정합니다. 범위 한정자 **::** 가 필요 합니다.  
  
 *보안 개체*  
 사용 권한을 거부할 보안 개체를 지정합니다.  
  
 *주*  
 보안 주체의 이름입니다. 보안 개체에 대한 사용 권한을 거부할 수 있는 대상 보안 주체는 보안 개체에 따라 달라집니다. 유효한 조합에 대해서는 아래에 나열된 보안 개체 관련 항목을 참조하세요.  
  
 CASCADE  
 지정된 보안 주체와 이 보안 주체가 사용 권한을 부여한 다른 모든 보안 주체에 대해 사용 권한이 거부됨을 나타냅니다. 보안 주체에 GRANT OPTION 권한이 있는 경우에 필요합니다.  
  
 AS *주*  
  보안 주체 권한의 데니어 속도가 문을 실행 하는 사용자 이외의 다른 보안 주체를 기록 나타내려면 AS 주 절을 사용 합니다. 예를 들어 사용자 Mary가 principal_id 12 및 Raul 사용자가 주 15 한다고 가정해 보겠습니다. Mary 실행 `DENY SELECT ON OBJECT::X TO Steven WITH GRANT OPTION AS Raul;` 이제 sys.database_permissions 테이블 deny 문 grantor_prinicpal_id 했음을 15 (Raul)는 문이 13 (Mary) 사용자가 실제로 실행 하는 경우에 표시 됩니다.
  
이 문 에서처럼 사용 하는 다른 사용자를 가장 하는 기능을 의미 하지 않습니다.  
  
## <a name="remarks"></a>주의  
 DENY 문의 전체 구문은 복잡합니다. 위의 구문 다이어그램은 구조를 강조하기 위해 단순하게 표현되었습니다. 특정 보안 개체에 대한 사용 권한을 거부하는 완전한 구문은 아래에 나열된 항목에서 설명합니다.  
  
 GRANT OPTION을 지정하여 사용 권한이 부여된 보안 주체의 사용 권한을 거부할 경우 CASCADE를 지정하지 않으면 DENY 문이 실패합니다.  
  
 sp_helprotect 시스템 저장 프로시저는 데이터베이스 수준 보안 개체에 대한 사용 권한을 보고합니다.  
  
> [!CAUTION]  
>  테이블 수준의 DENY는 열 수준의 GRANT보다 우선하지 않습니다. 사용 권한 계층에서의 이러한 불일치는 이전 버전과의 호환성을 위해 유지되었으며 후속 릴리스에서 제거될 예정입니다.  
  
> [!CAUTION]  
>  데이터베이스에 대한 CONTROL 권한을 거부하면 암시적으로 데이터베이스에 대한 CONNECT 권한이 거부됩니다. 데이터베이스에 대한 CONTROL 권한이 거부된 보안 주체는 해당 데이터베이스에 연결할 수 없습니다.  
  
> [!CAUTION]  
>  CONTROL SERVER 권한을 거부하면 암시적으로 서버에 대한 CONNECT SQL 권한이 거부됩니다. 따라서 서버에 대한 CONTROL SERVER 권한이 거부된 보안 주체는 해당 서버에 연결할 수 없게 됩니다.  
  
## <a name="permissions"></a>Permissions  
 호출자 또는 AS 옵션으로 지정한 보안 주체에게 보안 개체에 대한 CONTROL 권한이 있거나 보안 개체에 대한 CONTROL 권한을 포함하는 상위 사용 권한이 있어야 합니다. AS 옵션을 사용하는 경우 지정된 보안 주체가 사용 권한을 거부할 보안 개체를 소유해야 합니다.  
  
 sysadmin 고정 서버 역할의 멤버와 같이 CONTROL SERVER 권한이 부여된 사용자는 서버의 모든 보안 개체에 대한 모든 사용 권한을 거부할 수 있습니다. db_owner 고정 데이터베이스 역할의 멤버와 같이 데이터베이스에 대한 CONTROL 권한이 부여된 사용자는 데이터베이스의 모든 보안 개체에 대한 모든 사용 권한을 거부할 수 있습니다. 스키마에 대한 CONTROL 권한이 부여된 사용자는 스키마의 모든 개체에 대한 모든 사용 권한을 거부할 수 있습니다. AS 절을 사용하는 경우 지정된 보안 주체가 사용 권한을 거부할 보안 개체를 소유해야 합니다.  
  
## <a name="examples"></a>예  
 다음 표에는 보안 개체와 보안 개체별 구문을 설명하는 항목 목록이 정리되어 있습니다.  
  
|||  
|-|-|  
|응용 프로그램 역할|[데이터베이스 보안 주체 사용 권한 &#40; 거부 Transact SQL &#41;](../../t-sql/statements/deny-database-principal-permissions-transact-sql.md)|  
|어셈블리|[어셈블리 사용 권한 &#40; 거부 Transact SQL &#41;](../../t-sql/statements/deny-assembly-permissions-transact-sql.md)|  
|비대칭 키|[비대칭 키 사용 권한 &#40; 거부 Transact SQL &#41;](../../t-sql/statements/deny-asymmetric-key-permissions-transact-sql.md)|  
|가용성 그룹|[가용성 그룹 사용 권한 &#40; 거부 Transact SQL &#41;](../../t-sql/statements/deny-availability-group-permissions-transact-sql.md)|  
|인증서|[인증서 사용 권한 &#40; 거부 Transact SQL &#41;](../../t-sql/statements/deny-certificate-permissions-transact-sql.md)|  
|계약|[Service Broker 권한 &#40; 거부 Transact SQL &#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|데이터베이스|[데이터베이스 사용 권한 &#40; 거부 Transact SQL &#41;](../../t-sql/statements/deny-database-permissions-transact-sql.md)|  
|데이터베이스 범위 자격 증명|[DENY 데이터베이스 범위 자격 증명 (Transact SQL)](../../t-sql/statements/deny-database-scoped-credential-transact-sql.md)|  
|끝점|[끝점 사용 권한 &#40; 거부 Transact SQL &#41;](../../t-sql/statements/deny-endpoint-permissions-transact-sql.md)|  
|전체 텍스트 카탈로그|[전체 텍스트 사용 권한 &#40; 거부 Transact SQL &#41;](../../t-sql/statements/deny-full-text-permissions-transact-sql.md)|  
|전체 텍스트 중지 목록|[전체 텍스트 사용 권한 &#40; 거부 Transact SQL &#41;](../../t-sql/statements/deny-full-text-permissions-transact-sql.md)|  
|함수|[개체 사용 권한 &#40; 거부 Transact SQL &#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|로그인|[서버 보안 주체 사용 권한 &#40; 거부 Transact SQL &#41;](../../t-sql/statements/deny-server-principal-permissions-transact-sql.md)|  
|메시지 유형|[Service Broker 권한 &#40; 거부 Transact SQL &#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|개체|[개체 사용 권한 &#40; 거부 Transact SQL &#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|큐|[개체 사용 권한 &#40; 거부 Transact SQL &#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|원격 서비스 바인딩|[Service Broker 권한 &#40; 거부 Transact SQL &#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|역할|[데이터베이스 보안 주체 사용 권한 &#40; 거부 Transact SQL &#41;](../../t-sql/statements/deny-database-principal-permissions-transact-sql.md)|  
|경로|[Service Broker 권한 &#40; 거부 Transact SQL &#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|스키마|[DENY 스키마 사용 권한 &#40; Transact SQL &#41;](../../t-sql/statements/deny-schema-permissions-transact-sql.md)|  
|검색 속성 목록|[검색 속성 목록 사용 권한 &#40; 거부 Transact SQL &#41;](../../t-sql/statements/deny-search-property-list-permissions-transact-sql.md)|  
|Server|[서버 사용 권한 &#40; 거부 Transact SQL &#41;](../../t-sql/statements/deny-server-permissions-transact-sql.md)|  
|서비스|[Service Broker 권한 &#40; 거부 Transact SQL &#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|저장 프로시저|[개체 사용 권한 &#40; 거부 Transact SQL &#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|대칭 키|[대칭 키 사용 권한 &#40; 거부 Transact SQL &#41;](../../t-sql/statements/deny-symmetric-key-permissions-transact-sql.md)|  
|동의어|[개체 사용 권한 &#40; 거부 Transact SQL &#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|시스템 개체|[시스템 개체 사용 권한 &#40; 거부 Transact SQL &#41;](../../t-sql/statements/deny-system-object-permissions-transact-sql.md)|  
|테이블|[개체 사용 권한 &#40; 거부 Transact SQL &#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|형식|[DENY 유형 사용 권한 &#40; Transact SQL &#41;](../../t-sql/statements/deny-type-permissions-transact-sql.md)|  
|사용자|[데이터베이스 보안 주체 사용 권한 &#40; 거부 Transact SQL &#41;](../../t-sql/statements/deny-database-principal-permissions-transact-sql.md)|  
|보기|[개체 사용 권한 &#40; 거부 Transact SQL &#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|XML 스키마 컬렉션|[XML 스키마 컬렉션 사용 권한 &#40; 거부 Transact SQL &#41;](../../t-sql/statements/deny-xml-schema-collection-permissions-transact-sql.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [REVOKE&#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [sp_addlogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_adduser&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_changedbowner &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [sp_dropuser&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_helprotect&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [sp_helpuser &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)  
  
  

