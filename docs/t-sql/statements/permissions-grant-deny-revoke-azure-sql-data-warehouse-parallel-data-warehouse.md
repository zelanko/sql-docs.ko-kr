---
title: "GRANT 거부 REVOKE Perms-Azure SQL 데이터 및 병렬 데이터 웨어하우스 | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 5a3b7424-408e-4cb0-8957-667ebf4596fc
caps.latest.revision: "9"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: a21ee8a4a525e2b8c522de140a3f482915cdb361
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="permissions-grant-deny-revoke-azure-sql-data-warehouse-parallel-data-warehouse"></a>사용 권한: GRANT, DENY, REVOKE (Azure SQL 데이터 웨어하우스, 병렬 데이터 웨어하우스)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  사용 하 여 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] **GRANT** 및 **DENY** 는 권한을 부여 하거나 거부 하는 문을 (같은 **업데이트**) 보안 개체 (예: 데이터베이스, 테이블, 보기에 등입니다.) 보안 주체 (로그인, 데이터베이스 사용자 또는 데이터베이스 역할)에. 사용 하 여 **해지** 를 권한 부여를 제거 하거나 사용 권한 거부 합니다.  
  
 서버 수준 사용 권한은 로그인에 적용 됩니다. 데이터베이스 수준 사용 권한은 데이터베이스 사용자 및 데이터베이스 역할에 적용 됩니다.  
  
 사용 권한을 부여 및 거부 된을 보려면 sys.database_permissions 및 sys.server_permissions 뷰를 쿼리 합니다. 사용 권한을 가진 역할의 멤버 자격을 보유 하 여 명시적으로 부여 되거나 보안 주체에 대 한 거부 된 사용 권한은 상속할 수 있습니다. 고정된 데이터베이스 역할의 사용 권한을 변경할 수 없습니다 및 sys.database_permissions 및 sys.server_permissions 보기에 표시 되지 않습니다.  
  
-   **GRANT** 명시적으로 하나 이상의 사용 권한을 부여 합니다.  
  
-   **DENY** 에서 하나 이상의 권한을 가진 보안 주체의 권한이 명시적으로 거부 합니다.  
  
-   **해지** 기존 제거 **GRANT** 또는 **거부** 사용 권한.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [TRANSACT-SQL 구문 표기 규칙 &#40; Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
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
 \<사용 권한 > [ **,**... *n* ]  
 하나 이상의 권한을 부여, 거부 또는 취소 합니다.  
  
 ON [ \<class_type >::] *보안* 는 **ON** 절에 권한을 부여, 거부 또는 사용 권한을 취소 하는 보안 개체 매개 변수를 설명 합니다.  
  
 \<class_type > 보안 개체의 클래스 형식입니다. 이 수 **로그인**, **데이터베이스**, **개체**, **스키마**, **역할**, 또는 **사용자** . 에 사용 권한을 부여할 수도 있습니다는 **서버***class_type*, 하지만 **서버** 이러한 사용 권한은 지정 되지 않았습니다. **데이터베이스** 권한을 단어를 포함 하는 시기를 지정 하지 않으면 **데이터베이스** (예를 들어 **ALTER ANY DATABASE**). No *class_type* 지정 된 사용 권한 유형을 서버 또는 데이터베이스 클래스에 제한 되지 않습니다, 클래스 것으로 간주 되 고 **개체**합니다.  
  
 *보안 개체*  
 로그인, 데이터베이스, 테이블, 뷰, 스키마, 프로시저, 역할 또는 사용자에 게 부여 하려면 이름, 거부 또는 사용 권한을 취소 합니다. 개체 이름에 설명 된의 세 부분으로 이루어진 명명 규칙을 지정할 수 있습니다 [TRANSACT-SQL 구문 표기 규칙 &#40; Transact SQL &#41; ](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
 *주* [ **,**... *n* ]  
 하나 이상의 보안 주체 권한을 부여 하기 거부 또는 사용 권한을 취소 합니다. 보안 주체에는 로그인, 데이터베이스 사용자 또는 데이터베이스 역할의 이름입니다.  
  
 *주* [ **,**... *n* ]  
 사용 권한을 해지 하려면 하나 이상의 보안 주체입니다.  보안 주체에는 로그인, 데이터베이스 사용자 또는 데이터베이스 역할의 이름입니다. **에** 사용할 수는 **해지** 문. **함께** 사용할 수 있습니다 **GRANT** , **DENY** , 또는 **해지** 합니다.  
  
 WITH GRANT OPTION  
 지정된 사용 권한을 다른 보안 주체에게 부여할 수 있는 권한도 피부여자에게 제공됨을 나타냅니다.  
  
 CASCADE  
 사용 권한을 거부 되었거나 지정된 된 보안 주체를 다른 보안 주체의 사용 권한을 부여 모든 보안 주체를 취소 되었음을 나타냅니다. 보안 주체에 권한이 있는 경우 필수 **GRANT OPTION**합니다.  
  
 GRANT OPTION FOR  
 지정된 사용 권한을 부여할 수 있는 권한이 취소됨을 나타냅니다. 이 사용 하는 경우 필요는 **CASCADE** 인수입니다.  
  
> [!IMPORTANT]  
>  보안 주체에 없이 지정 된 사용 권한이 있는 경우는 **GRANT** 옵션을 사용 권한이 해지 됩니다.  
  
## <a name="permissions"></a>Permissions  
 사용 권한을 부여할 grant 권한이 있어야 하거나 자체와 **WITH GRANT OPTION**, 부여할 사용 권한을 나타내는 상위 사용 권한이 있어야 합니다.  개체 소유자는 소유하고 있는 개체에 대한 사용 권한을 부여할 수 있습니다. 주체를 **제어** 에 보안 개체에 대 한 권한이 필요한 권한을 부여할 수 해당 보안 개체입니다.  멤버는 **db_owner** 및 **db_securityadmin** 고정된 데이터베이스 역할에는 데이터베이스에 대 한 사용 권한을 부여할 수 있습니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 보안 주체에 대 한 사용 권한을 취소 또는 거부 권한 부여를 통과 했는지를 현재 실행 중인 요청이 영향을 주지 않습니다. 액세스를 제한 하려면 즉시 활성 요청을 취소 하거나 해야 현재 세션을 중지 합니다.  
  
> [!NOTE]  
>  가장 고정된 서버 역할이 릴리스에서 사용할 수 없는 경우입니다. 사용자 정의 데이터베이스 역할을 대신 사용 합니다. 에 로그인을 추가할 수 없습니다는 **sysadmin** 고정된 서버 역할입니다. 부여는 **제어 서버** 권한의 멤버 자격이 근사치로 계산 된 **sysadmin** 고정된 서버 역할입니다.  
  
 일부 문을 여러 가지 권한이 있어야합니다. 예를 들어 테이블을 만들 필요는 **CREATE TABLE** 데이터베이스에 대 한 사용 권한 및 **ALTER SCHEMA** 는 테이블이 포함 될 테이블에 대 한 사용 권한입니다.  
  
 PDW 때때로 사용자 작업을 계산 노드를 배포 하는 저장된 프로시저를 실행 합니다. 전체 데이터베이스에 대 한 execute 권한을 거부할 수 없습니다. (예를 들어 `DENY EXECUTE ON DATABASE::<name> TO <user>;` 실패 합니다.) 해결 방법으로, 사용자 스키마 또는 특정 개체 (프로시저)에 execute 권한을 거부 합니다.  
  
### <a name="implicit-and-explicit-permissions"></a>암시적 및 명시적 사용 권한  
 *명시적 사용 권한을* 는 **GRANT** 또는 **DENY** 권한에서 보안 주체에 부여는 **GRANT** 또는 **DENY**문입니다.  
  
 *암시적 사용 권한이* 는 **GRANT** 또는 **거부** 보안 주체 (로그인, 사용자 또는 데이터베이스 역할)가 다른 데이터베이스 역할에서 상속 되며, 사용 권한입니다.  
  
 하나의 암시적 사용 권한 포함 또는 상위 권한을 상속할 수 수도 있습니다. 예를 들어 **업데이트** 하도록 하 여 테이블에 대 한 권한이 상속 될 수 **업데이트** 테이블을 포함 하는 스키마에 대 한 권한 또는 **제어** 테이블에 대 한 합니다.  
  
### <a name="ownership-chaining"></a>소유권 체인  
 시퀀스 라고 여러 데이터베이스 개체가 서로 순차적으로 액세스, 한 *체인*합니다. 이러한 체인이 독립적으로 존재하지는 않지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 체인에 있는 링크를 통과할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 개체를 개별적으로 액세스할 때와는 달리 구성된 개체에 대한 사용 권한을 평가합니다. 소유권 체인에 보안을 관리 하기 위한 중요 한 이점이 있습니다. 소유권 체인에 대 한 자세한 내용은 참조 [소유권 체인](http://msdn.microsoft.com/en-us/library/ms188676\(v=sql11\).aspx) 및 [자습서: 소유권 체인 및 컨텍스트 전환](http://msdn.microsoft.com/en-us/library/bb153640\(v=sql11\).aspx)합니다.  
  
## <a name="permission-list"></a>사용 권한 목록  
  
### <a name="server-level-permissions"></a>서버 수준 사용 권한  
 서버 수준 사용 권한은 부여, 거부 하 고 로그인에서 해지 되었습니다 될 수 있습니다.  
  
 **서버에 적용 되는 사용 권한**  
  
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
  
 **로그인에 적용 되는 권한**  
  
-   로그인에서 제어  
  
-   로그인에 대 한 ALTER  
  
-   로그인에 대 한 가장  
  
-   VIEW DEFINITION  
  
### <a name="database-level-permissions"></a>데이터베이스 수준 사용 권한  
 데이터베이스 수준 사용 권한은 부여할 수 있습니다, denied 및 해지 된 데이터베이스 사용자 및 사용자 정의 데이터베이스 역할.  
  
 **모든 데이터베이스 클래스에 적용 되는 권한**  
  
-   CONTROL  
  
-   ALTER  
  
-   VIEW DEFINITION  
  
 **사용자를 제외한 모든 데이터베이스 클래스에 적용 되는 권한**  
  
-   TAKE OWNERSHIP  
  
 **데이터베이스에만 적용 되는 권한**  
  
-   ALTER ANY DATABASE  
  
-   데이터베이스에 대 한 ALTER  
  
-   ALTER ANY DATASPACE  
  
-   ALTER ANY ROLE  
  
-   ALTER ANY SCHEMA  
  
-   ALTER ANY USER  
  
-   BACKUP DATABASE  
  
-   데이터베이스에 연결  
  
-   CREATE PROCEDURE  
  
-   CREATE ROLE  
  
-   CREATE SCHEMA  
  
-   CREATE TABLE  
  
-   CREATE VIEW  
  
-   SHOWPLAN  
  
 **한 사용자 에게만 적용 되는 권한**  
  
-   IMPERSONATE  
  
 **데이터베이스, 스키마 및 개체에 적용 되는 사용 권한**  
  
-   ALTER  
  
-   DELETE  
  
-   EXECUTE  
  
-   INSERT  
  
-   SELECT  
  
-   UPDATE  
  
-   참조  
  
 각 사용 권한 유형에 정의 참조 하십시오. [사용 권한 (데이터베이스 엔진)](http://msdn.microsoft.com/library/ms191291.aspx)합니다.  
  
### <a name="chart-of-permissions"></a>사용 권한 차트  
 모든 사용 권한은이 포스터에 그래픽으로 표시 됩니다. 사용 권한 중첩 된 계층 구조를 볼 수는 가장 쉬운 방법은 이것이입니다. 예를 들어는 **ALTER ON LOGIN** 자체적으로 권한을 부여할 수 있습니다 하지만 포함 되어는 로그인에 부여 하는 경우는 **제어** 권한을 해당 로그인에는 로그인에 부여 하는 경우 또는 **ALTER ANY 로그인** 권한.  
  
 ![APS 보안 권한 포스터](../../t-sql/statements/media/aps-security-perms-poster.png "APS 보안 권한 포스터")  
  
 이 포스터의 전체 크기 버전을 다운로드 하려면 참조 [SQL Server PDW 권한](http://go.microsoft.com/fwlink/?LinkId=244249)APS Yammer 사이트의 파일 섹션에 (또는에서 전자 메일을 통해 요청  **apsdoc@microsoft.com** 합니다.  
  
## <a name="default-permissions"></a>기본 사용 권한  
 다음 목록에는 기본 사용 권한을 설명합니다.  
  
-   사용 하 여 로그인을 만들면는 **CREATE LOGIN** 새 로그인 수신 문에 **CONNECT SQL** 권한.  
  
-   멤버인 모든 로그인은 **공용** 서버 역할에서 제거할 수 없습니다 및 **공용**합니다.  
  
-   데이터베이스 사용자를 사용 하 여 만들어질 때는 **CREATE USER** 권한, 데이터베이스 사용자에 게는 **연결** 데이터베이스에는 권한이 있습니다.  
  
-   포함 한 모든 보안 주체는 **공용** 역할을 기본적으로 명시적 또는 암시적 사용 권한이 없는 합니다.  
  
-   로그인 또는 사용자가 데이터베이스 또는 개체의 소유자, 로그인 또는 사용자 데이터베이스 또는 개체에 대 한 모든 권한을 항상에 있습니다. 소유권 권한을 변경할 수 없습니다 하며 명시적 사용 권한으로 표시 되지 않습니다. **GRANT**, **거부**, 및 **해지** 문을 소유자에 아무 영향도 있습니다.  
  
-   **sa** 로그인 어플라이언스에서 모든 사용 권한을 갖습니다. 소유자 권한이 비슷합니다는 **sa** 사용 권한을 변경할 수 없습니다 하며 명시적 사용 권한으로 표시 되지 않습니다. **GRANT**, **DENY**, 및 **해지** 아무런 영향을 주지에 나타나 문을 **sa** 로그인 합니다. **sa** 로그인 이름을 바꿀 수 없습니다.  
  
-   **사용** 문을 권한이 필요 하지 않습니다. 모든 보안 주체를 실행할 수는 **사용** 모든 데이터베이스에서 문입니다.  
  
##  <a name="Examples"></a>예: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-granting-a-server-level-permission-to-a-login"></a>1. 로그인에 서버 수준 사용 권한 부여  
 다음 두 문이 로그인에 서버 수준 권한을 부여합니다.  
  
```  
GRANT CONTROL SERVER TO [Ted];  
```  
  
```  
GRANT ALTER ANY DATABASE TO Mary;  
```  
  
### <a name="b-granting-a-server-level-permission-to-a-login"></a>2. 로그인에 서버 수준 사용 권한 부여  
 다음 예에서는 서버 보안 주체일 (다른 로그인)에 대 한 로그인에 서버 수준 권한을 부여합니다.  
  
```  
GRANT  VIEW DEFINITION ON LOGIN::Ted TO Mary;  
```  
  
### <a name="c-granting-a-database-level-permission-to-a-user"></a>3. 사용자에 게 데이터베이스 수준 사용 권한 부여  
 다음 예제에서는 사용자에 게는 데이터베이스 보안 주체 (다른 사용자)는 데이터베이스 수준 사용 권한을 부여합니다.  
  
```  
GRANT VIEW DEFINITION ON USER::[Ted] TO Mary;  
```  
  
### <a name="d-granting-denying-and-revoking-a-schema-permission"></a>4. 권한을 부여, 거부 및 스키마 사용 권한 취소  
 다음 **GRANT** 문을 Yuen 테이블이 나 뷰 dbo 스키마에서에서 데이터를 선택할 수 있는 기능을 부여 합니다.  
  
```  
GRANT SELECT ON SCHEMA::dbo TO [Yuen];  
```  
  
 다음 **거부** 문은 테이블이 나 뷰 dbo 스키마에서에서 데이터를 선택에서 Yuen를 수 없도록 합니다. Yuen도 그 권한이 있으면 다른 방법으로과 같은 역할 멤버 자격을 통해 데이터를 읽을 수 없습니다.  
  
```  
DENY SELECT ON SCHEMA::dbo TO [Yuen];  
```  
  
 다음 **해지** 문 제거는 **거부** 권한. 이제 Yuen의 명시적 사용 권한을 중립 됩니다. Yuen 몇 가지 다른 암시적 사용 권한 등 역할 멤버 자격을 통해 모든 테이블에서 데이터를 선택할 수 있습니다.  
  
```  
REVOKE SELECT ON SCHEMA::dbo TO [Yuen];  
```  
  
### <a name="e-demonstrating-the-optional-object-clause"></a>5. 선택적 개체를 보여 주는:: 절  
 개체 사용 권한 문에 대 한 기본 클래스 이기 때문에 다음 두 문은 동일 합니다. **개체::** 절은 선택 사항입니다.  
  
```  
GRANT UPDATE ON OBJECT::dbo.StatusTable TO [Ted];  
```  
  
```  
GRANT UPDATE ON dbo.StatusTable TO [Ted];  
```  
  
  

