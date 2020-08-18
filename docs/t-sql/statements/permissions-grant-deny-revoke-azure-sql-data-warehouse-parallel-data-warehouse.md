---
description: '사용 권한: GRANT, DENY, REVOKE(Azure SQL Data Warehouse, 병렬 Data Warehouse)'
title: GRANT-DENY-REVOKE 권한
titleSuffix: Azure SQL Data Warehouse
ms.custom: seo-lt-2019
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5a3b7424-408e-4cb0-8957-667ebf4596fc
author: VanMSFT
ms.author: vanto
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: ed28cb4adb7acd80212770d5760197854d8e8539
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88357749"
---
# <a name="permissions-grant-deny-revoke-azure-sql-data-warehouse-parallel-data-warehouse"></a>사용 권한: GRANT, DENY, REVOKE(Azure SQL Data Warehouse, 병렬 Data Warehouse)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  보안 개체(예: 데이터베이스, 테이블, 뷰)에 보안 주체(로그인, 데이터베이스 사용자 또는 데이터베이스 역할)에 대한 사용 권한(예: **UPDATE**)을 부여 또는 거부하려면 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]**GRANT** 및 **DENY** 문을 사용합니다. **REVOKE**를 사용하여 권한 부여 또는 거부를 제거합니다.  
  
 서버 수준 사용 권한은 로그인에 적용됩니다. 데이터베이스 수준 사용 권한은 데이터베이스 사용자 및 데이터베이스 역할에 적용됩니다.  
  
 어떤 사용 권한이 부여 및 거부되었는지 보려면 sys.server_permissions 및 sys.database_permissions 뷰를 쿼리합니다. 보안 주체에 명시적으로 부여되거나 거부되지 않은 사용 권한은 사용 권한이 있는 역할의 멤버 자격을 가짐으로써 상속될 수 있습니다. 고정 데이터베이스 역할의 사용 권한은 변경할 수 없으며 sys.server_permissions 및 sys.database_permissions 뷰에 표시되지 않습니다.  
  
-   **GRANT**는 하나 이상의 사용 권한을 명시적으로 부여합니다.  
  
-   **DENY**는 보안 주체가 하나 이상의 사용 권한을 갖지 못하도록 명시적으로 거부합니다.  
  
-   **REVOKE**는 기존의 **GRANT** 또는 **DENY** 권한을 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙&#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
-- Azure SQL Data Warehouse and Parallel Data Warehouse  
GRANT   
    <permission> [ ,...n ]  
    [ ON [ <class_type> :: ] securable ]   
    TO principal [ ,...n ]  
    [ WITH GRANT OPTION ]  
[;]  
  
DENY   
    <permission> [ ,...n ]  
    [ ON [ <class_type> :: ] securable ]   
    TO principal [ ,...n ]  
    [ CASCADE ]  
[;]  
  
REVOKE   
    <permission> [ ,...n ]  
    [ ON [ <class_type> :: ] securable ]   
    [ FROM | TO ] principal [ ,...n ]  
    [ CASCADE ]  
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
 \<permission>[ **,** ...*n* ]  
 부여, 거부 또는 취소할 수있는 하나 이상의 사용 권한.  
  
 ON [ \<class_type> :: ] *securable* **ON** 절은 사용 권한을 부여, 거부 또는 취소하는 보안 개체 매개 변수를 설명합니다.  
  
 \<class_type> 보안 개체의 클래스 형식입니다. 이 형식으로는 **LOGIN**, **DATABASE**, **OBJECT**, **SCHEMA**, **ROLE**, 또는 **USER**가 될 수 있습니다. 사용 권한은 **SERVER**_class\_type_에도 부여될 수 있지만, 해당 사용 권한에는 **SERVER**가 지정되지 않습니다. 사용 권한에 **DATABASE**(예: **ALTER ANY DATABASE**)와 같은 단어가 포함되어 있으면 **DATABASE**는 지정되지 않습니다. *class_type*이 지정되지 권한 유형이 서버 또는 데이터베이스 클래스에 제한되지 않는 경우 클래스는 **OBJECT**로 간주됩니다.  
  
 *securable*  
 사용 권한을 부여, 거부 또는 취소 할 로그인, 데이터베이스, 테이블, 뷰, 스키마, 프로시저, 역할 또는 사용자의 이름입니다. 개체 이름은 [Transact-SQL 구문 규칙&#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)에서 설명된 세 부분 명명 규칙을 사용하여 지정할 수 있습니다.  
  
 TO *principal* [ **,** ...*n* ]  
 사용 권한이 부여, 거부 또는 취소된 하나 이상의 보안 주체입니다. 보안 주체는 로그인, 데이터베이스 사용자 또는 데이터베이스 역할의 이름입니다.  
  
 FROM *principal* [ **,** ...*n* ]  
 사용 권한을 해지할 하나 이상의 보안 주체입니다.  보안 주체는 로그인, 데이터베이스 사용자 또는 데이터베이스 역할의 이름입니다. **FROM**은 오직 **REVOKE** 문과 함께 사용할 수 있습니다. **TO**는 **GRANT**, **DENY** 또한 **REVOKE**와 함께 사용할 수 있습니다.  
  
 WITH GRANT OPTION  
 지정된 사용 권한을 다른 보안 주체에게 부여할 수 있는 권한도 피부여자에게 제공됨을 나타냅니다.  
  
 CASCADE  
 지정된 보안 주체와 이 보안 주체가 사용 권한을 부여한 다른 모든 보안 주체에 대해 사용 권한이 거부됨 또는 취소됨을 나타냅니다. 보안 주체에 **GRANT OPTION** 권한이 있는 경우에 필요합니다.  
  
 GRANT OPTION FOR  
 지정된 사용 권한을 부여할 수 있는 권한이 취소됨을 나타냅니다. **CASCADE** 인수를 사용할 경우 이 인수가 필요합니다.  
  
> [!IMPORTANT]  
>  보안 주체에 **GRANT** 옵션 없이 지정된 사용 권한이 있는 경우 사용 권한 자체가 취소됩니다.  
  
## <a name="permissions"></a>사용 권한  
 사용 권한을 부여하려면 grantor는 **WITH GRANT OPTION**이 갖춰진 사용 권한이 있거나 부여할 사용 권한을 포함하는 상위 사용 권한이 있어야 합니다.  개체 소유자는 소유하고 있는 개체에 대한 사용 권한을 부여할 수 있습니다. 보안 개체에 대한 **CONTROL** 사용 권한을 가진 보안 주체는 해당 보안 개체에 대한 사용 권한을 부여할 수 있습니다.  **db_owner** 및 **db_ddlowner** 고정 데이터베이스 역할의 멤버는 데이터베이스에서 어떤 사용 권한도 부여할 수 있습니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 보안 주체에 대한 사용 권한을 거부하거나 취소해도 권한 부여를 통과했고 현재 실행중인 요청에는 영향을 주지 않습니다. 액세스를 즉시 제한하려면 활성 요청을 취소하거나 현재 세션을 종료해야합니다.  
  
> [!NOTE]  
>  이 릴리스에서는 대부분의 고정 서버 역할을 사용할 수 없습니다. 사용자 정의 데이터베이스 역할을 대신 사용합니다. 로그인은 **sysadmin** 고정 서버 역할에 추가될 수 없습니다. **CONTROL SERVER** 사용 권한 부여는 **sysadmin** 고정 서버 역할의 멤버 자격을 갖는 것과 비슷합니다.  
  
 일부 문은 여러 사용 권한을 필요로 합니다. 예를 들어, 테이블을 만들려면 데이터베이스에서 **CREATE TABLE** 사용 권한 및 테이블을 포함할 테이블에 대한 **ALTER SCHEMA** 사용 권한이 필요합니다.  
  
 PDW는 때때로 사용자 작업을 컴퓨팅 노드에 배포하기 위해 저장된 프로시저를 실행합니다. 따라서 전체 데이터베이스에 대한 실행 권한을 거부 할 수 없습니다. (예를 들어 `DENY EXECUTE ON DATABASE::<name> TO <user>;`은 오류가 발생합니다.) 해결 방법으로 사용자 스키마 또는 특정 개체(프로시저)에 대한 실행 권한을 거부합니다.  
  
### <a name="implicit-and-explicit-permissions"></a>암시적 및 명시적 사용 권한  
 *명시적 사용 권한*은 **GRANT** 또는 **DENY**문으로 보안 주체에게 주어진 **GRANT** 또는 **DENY** 사용 권한입니다.  
  
 *암시적 권한*은 보안 주체(로그인, 사용자 또는 데이터베이스 역할)가 다른 데이터베이스 역할에서 상속한 **GRANT** 또는 **DENY** 사용 권한입니다.  
  
 암시적 권한은 또한 포괄적 또는 상위 권한을 상속할 수도 있습니다. 예를 들어, 테이블에 대한 **UPDATE** 권한은 해당 테이블, 또는 해당 테이블의 **CONTROL** 권한을 포함하는 스키마의 **UPDATE** 권한을 가짐으로써 상속할 수 있습니다,  
  
### <a name="ownership-chaining"></a>소유권 체인  
 여러 데이터베이스 개체가 서로를 순차적으로 액세스하는 경우 이러한 시퀀스를 *체인*이라고 합니다. 이러한 체인이 독립적으로 존재하지는 않지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 체인에 있는 링크를 통과할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 개체를 개별적으로 액세스할 때와는 달리 구성된 개체에 대한 사용 권한을 평가합니다. 소유권 체인은 보안 관리에 중요한 영향을 줍니다. 소유권 체인에 대한 자세한 내용은 [소유권 체인](https://msdn.microsoft.com/library/ms188676\(v=sql11\).aspx) 및 [자습서: 소유권 체인 및 컨텍스트 전환](../../relational-databases/tutorial-ownership-chains-and-context-switching.md)을 참조하세요.  
  
## <a name="permission-list"></a>허가 목록  
  
### <a name="server-level-permissions"></a>서버 수준 사용 권한  
 서버 수준 권한은 로그인에서 부여, 거부 및 취소할 수 있습니다.  
  
 **서버에 적용되는 사용 권한**  
  
-   CONTROL SERVER  
  
-   ADMINISTER BULK OPERATIONS  
  
-   ALTER ANY CONNECTION  
  
-   ALTER ANY DATABASE  
  
-   CREATE ANY DATABASE  
  
-   ALTER ANY EXTERNAL DATA SOURCE  
  
-   ALTER ANY EXTERNAL FILE FORMAT  
  
-   ALTER ANY LOGIN  
  
-   ALTER SERVER STATE  
  
-   CONNECT SQL  
  
-   VIEW ANY DEFINITION  
  
-   VIEW ANY DATABASE  
  
-   VIEW SERVER STATE  
  
 **로그인에 적용되는 권한**  
  
-   CONTROL ON LOGIN  
  
-   ALTER ON LOGIN  
  
-   IMPERSONATE ON LOGIN  
  
-   VIEW DEFINITION  
  
### <a name="database-level-permissions"></a>데이터베이스 수준 사용 권한  
 데이터베이스 수준 사용 권한은 데이터베이스 사용자 및 사용자 정의 데이터베이스 역할에서 부여, 거부 및 취소할 수 있습니다.  
  
 **모든 데이터베이스 클래스에 적용되는 권한**  
  
-   CONTROL  
  
-   ALTER  
  
-   VIEW DEFINITION  
  
 **사용자를 제외한 모든 데이터베이스 클래스에 적용되는 권한**  
  
-   TAKE OWNERSHIP  
  
 **데이터베이스에만 적용되는 권한**  
  
-   ALTER ANY DATABASE  
  
-   ALTER ON DATABASE  
  
-   ALTER ANY DATASPACE  
  
-   ALTER ANY ROLE  
  
-   ALTER ANY SCHEMA  
  
-   ALTER ANY USER  
  
-   BACKUP DATABASE  
  
-   CONNECT ON DATABASE  
  
-   CREATE PROCEDURE  
  
-   CREATE ROLE  
  
-   CREATE SCHEMA  
  
-   CREATE TABLE  
  
-   CREATE VIEW  
  
-   SHOWPLAN  
  
 **사용자에게만 적용되는 권한**  
  
-   IMPERSONATE  
  
 **데이터베이스, 스키마 및 개체에 적용되는 권한**  
  
-   ALTER  
  
-   Delete  
  
-   CREATE 문을 실행하기 전에  
  
-   INSERT  
  
-   SELECT  
  
-   UPDATE  
  
-   REFERENCES  
  
 각 사용 권한 유형에 대한 정의는 [사용 권한(데이터베이스 엔진)](https://msdn.microsoft.com/library/ms191291.aspx)을 참조하세요.  
  
### <a name="chart-of-permissions"></a>권한 목록  
 모든 사용 권한은 이 포스터에 그래픽으로 표시됩니다. 이 방법이 사용 권한의 중첩된 계층 구조를 볼 수 있는 가장 쉬운 방법입니다. 예를 들어, **ALTER ON LOGIN** 권한은 자체적으로 부여될 수 있지만, 또한 로그인에 해당 로그인에 대한 **CONTROL** 권한이 부여되거나 또는 로그인에 **ALTER ANY LOGIN** 권한이 부여된다면 포함될 수 있습니다.  
  
 ![APS 보안 권한 포스터](../../t-sql/statements/media/aps-security-perms-poster.png "APS 보안 권한 포스터")  
  
 이 포스터를 전체 크기로 다운로드하려면 APS Yammer 사이트의 파일 섹션에 있는 [SQL Server PDW 권한](https://go.microsoft.com/fwlink/?LinkId=244249)을 참조하거나 **apsdoc\@microsoft.com**에 이메일로 요청합니다.  
  
## <a name="default-permissions"></a>기본 사용 권한  
 다음 목록에서는 기본 사용 권한을 설명합니다.  
  
-   로그인이 **CREATE LOGIN** 문을 사용하여 만들어졌다면 새 로그인은 **CONNECT SQL** 권한을 받습니다.  
  
-   모든 로그인은 **public** 서버 역할의 멤버이며 **public**에서 제거할 수 없습니다.  
  
-   데이터베이스 사용자가 **CREATE USER** 권한을 사용하여 만들어질 때 데이터베이스 사용자는 데이터베이스에서 **CONNECT** 권한을 받습니다.  
  
-   **public** 역할을 포함하여 모든 보안 주체는 기본적으로 명시적 또는 암시적 사용 권한이 없습니다.  
  
-   로그인 또는 사용자가 데이터베이스 또는 개체의 소유자가 되면 로그인 또는 사용자는 항상 데이터베이스 또는 개체에 대한 모든 사용 권한을 가집니다. 소유권 사용 권한은 변경할 수 없으며 명시적 사용 권한으로 표시되지 않습니다. **GRANT**, **DENY** 및 **REVOKE** 문은 소유자에게 아무런 영향을 미치지 않습니다.  
  
-   **sa** 로그인은 어플라이언스에 대한 모든 사용 권한을 가집니다. 소유권 사용 권한과 마찬가지로 **sa** 사용 권한도 변경할 수 없으며 명시적 사용 권한으로 표시되지 않습니다. **GRANT**, **DENY** 및 **REVOKE** 문은 **sa** 로그인에 아무런 영향을 미치지 않습니다. **sa** 로그인은 이름을 바꿀 수 없습니다.  
  
-   **USE** 문은 사용 권한이 필요하지 않습니다. 모든 보안 주체는 모든 데이터베이스에서 **USE** 문을 실행할 수 있습니다.  
  
##  <a name="examples-sssdw-and-sspdw"></a><a name="Examples"></a> 예제: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-granting-a-server-level-permission-to-a-login"></a>A. 로그인에 서버 수준 사용 권한 부여  
 다음 두 문은 로그인에 서버 수준 사용 권한을 부여합니다.  
  
```  
GRANT CONTROL SERVER TO [Ted];  
```  
  
```  
GRANT ALTER ANY DATABASE TO Mary;  
```  
  
### <a name="b-granting-a-server-level-permission-to-a-login"></a>B. 로그인에 서버 수준 사용 권한 부여  
 다음 예에서는 서버 보안 주체(다른 로그인)에 하는 로그인에 서버 수준 사용 권한을 부여합니다.  
  
```  
GRANT  VIEW DEFINITION ON LOGIN::Ted TO Mary;  
```  
  
### <a name="c-granting-a-database-level-permission-to-a-user"></a>C. 사용자에게 데이터베이스 수준 사용 권한 부여  
 다음 예에서는 데이터베이스 보안 주체(다른 사용자)의 사용자에게 데이터베이스 수준 사용 권한을 부여합니다.  
  
```  
GRANT VIEW DEFINITION ON USER::[Ted] TO Mary;  
```  
  
### <a name="d-granting-denying-and-revoking-a-schema-permission"></a>D. 스키마 사용 권한 부여, 거부 및 취소  
 다음 **GRANT** 문은 Yuen에게 dbo 스키마 내의 모든 테이블 또는 뷰에서 데이터를 선택할 수 있는 기능을 부여합니다.  
  
```  
GRANT SELECT ON SCHEMA::dbo TO [Yuen];  
```  
  
 다음 **DENY** 문은 Yuen에게 dbo 스키마 내의 모든 테이블 또는 뷰에서 데이터를 선택할 수 없도록 합니다. Yuen은 역할 멤버 자격과 같은 일부 다른 방법으로 사용 권한을 가졌다 하더라도 데이터를 읽을 수 없습니다.  
  
```  
DENY SELECT ON SCHEMA::dbo TO [Yuen];  
```  
  
 다음 **REVOKE** 문은 **DENY** 권한을 제거합니다. 현재 Yuen의 명시적 사용 권한은 중립적입니다. Yuen은 역할 멤버 자격과 같은 일부 다른 암시적 사용 권한을 통해 모든 테이블에서 데이터를 선택할 수 있습니다.  
  
```  
REVOKE SELECT ON SCHEMA::dbo TO [Yuen];  
```  
  
### <a name="e-demonstrating-the-optional-object-clause"></a>E. 선택적 OBJECT :: 절 표시  
 OBJECT는 사용 권한 문에 대한 기본 클래스이므로 다음 두 명령문은 동일합니다. **OBJECT::** 절은 선택 사항입니다.  
  
```  
GRANT UPDATE ON OBJECT::dbo.StatusTable TO [Ted];  
```  
  
```  
GRANT UPDATE ON dbo.StatusTable TO [Ted];  
```  
  
  

