---
title: HAS_PERMS_BY_NAME (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- HAS_PERMS_BY_NAME
- HAS_PERMS_BY_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- permissions [SQL Server], verifying
- current permission status
- checking permission status
- verifying permission status
- testing permissions
- HAS_PERMS_BY_NAME function
ms.assetid: eaf8cc82-1047-4144-9e77-0e1095df6143
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 09eae4a5ea247592109c0fcbc261f1ec3ce1b3db
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="haspermsbyname-transact-sql"></a>HAS_PERMS_BY_NAME(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  보안 개체에 대한 현재 사용자의 유효 사용 권한을 평가합니다. 관련된 함수는 [fn_my_permissions](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
HAS_PERMS_BY_NAME ( securable , securable_class , permission    
    [ , sub-securable ] [ , sub-securable_class ] )  
```  
  
## <a name="arguments"></a>인수  
 *보안 개체*  
 보안 개체의 이름입니다. 보안 개체가 서버 자체인 경우 이 값을 NULL로 설정해야 합니다. *보안 개체* 형식의 스칼라 식 **sysname**합니다. 기본값은 없습니다.  
  
 *b l e _*  
 사용 권한을 테스트한 보안 개체 클래스의 이름입니다. *b l e _* 형식의 스칼라 식 **nvarchar (60)**합니다.  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], securable_class 인수는 다음 중 하나를 설정 해야: **데이터베이스**, **개체**, **역할**, **스키마**, 또는 **사용자**합니다.  
  
 *사용 권한*  
 형식의 null이 아닌 스칼라 식이 **sysname** 확인할 사용 권한 이름을 나타내는입니다. 기본값은 없습니다. 사용 권한 이름 ANY는 와일드카드입니다.  
  
 *하위 보안 개체*  
 형식의 선택적 스칼라 식 **sysname** 는 권한이 테스트 되는 보안 개체 하위 엔터티의 이름을 나타내는입니다. 기본값은 NULL입니다.  
  
> [!NOTE]  
>  버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], 하위 보안 개체 형태로 대괄호를 사용할 수 없는 **' [***하위 이름***]'**합니다. 사용 하 여 **'***하위 이름***'** 대신 합니다.  
  
 *sub-b l e _*  
 형식의 선택적 스칼라 식 **nvarchar (60)** 는 권한이 테스트 되는 보안 개체 하위 엔터티의 클래스를 나타냅니다. 기본값은 NULL입니다.  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], sub securable_class 인수는 securable_class 인수는로 설정 된 경우에 유효한 **개체**합니다. Securable_class 인수 설정 된 경우 **개체**, sub securable_class 인수로 설정 해야 **열**합니다.  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
 쿼리가 실패하면 NULL을 반환합니다.  
  
## <a name="remarks"></a>주의  
 이 기본 제공 함수는 지정된 보안 개체에 대한 특정 유효 사용 권한이 현재 보안 주체에 있는지 여부를 테스트합니다. HAS_PERMS_BY_NAME은 사용자에게 보안 개체에 대한 유효 사용 권한이 있으면 1을 반환하고, 사용자에게 보안 개체에 대한 유효 사용 권한이 없으면 0을 반환하며, 보안 개체 클래스 또는 사용 권한이 유효하지 않으면 NULL을 반환합니다. 유효 사용 권한은 다음 중 하나입니다.  
  
-   보안 주체에게 직접 부여되고 거부되지 않은 사용 권한  
  
-   보안 주체가 소유하는 더 높은 수준의 사용 권한에 포함되고 거부되지 않은 사용 권한  
  
-   보안 주체가 멤버로 속한 역할이나 그룹에 부여되고 거부되지 않은 사용 권한  
  
-   보안 주체가 멤버로 속한 역할이나 그룹이 소유하고 거부되지 않은 사용 권한  
  
 사용 권한은 항상 호출자의 보안 컨텍스트에서 평가됩니다. 다른 사용자에게 유효 사용 권한이 있는지 여부를 확인하려면 해당 사용자에 대한 IMPERSONATE 권한이 호출자에게 있어야 합니다.  
  
 스키마 수준 엔터티의 경우 한 부분, 두 부분 또는 세 부분으로 된 Null이 아닌 이름을 사용할 수 있습니다. 데이터베이스 수준 엔터티의 경우 한 부분으로 된 이름을 사용할 수 있으며 Null 값은 "현재 데이터베이스"를 나타냅니다. 서버 자체인 경우에는 Null 값("현재 서버"를 나타냄)이 필요합니다. 이 함수로는 서버 수준 보안 주체가 생성되지 않은 Windows 사용자 또는 연결된 서버의 사용 권한을 확인할 수 없습니다.  
  
 다음 쿼리는 기본 제공 보안 개체 클래스의 목록을 반환합니다.  
  
```  
SELECT class_desc FROM sys.fn_builtin_permissions(default);  
```  
  
 사용되는 데이터 정렬은 다음과 같습니다.  
  
-   현재 데이터베이스 데이터 정렬: 스키마에 포함되지 않은 보안 개체를 포함하는 데이터베이스 수준 보안 개체, 한 부분 또는 두 부분으로 된 스키마 범위 보안 개체, 세 부분으로 된 이름을 사용할 경우 대상 데이터베이스  
  
-   master 데이터베이스 데이터 정렬: 서버 수준 보안 개체  
  
-   열 수준 확인에는 'ANY'를 사용할 수 없습니다. 적절한 사용 권한을 지정해야 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-do-i-have-the-server-level-view-server-state-permission"></a>1. 서버 수준 VIEW SERVER STATE 권한이 있는지 확인  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT HAS_PERMS_BY_NAME(null, null, 'VIEW SERVER STATE');  
```  
  
### <a name="b-am-i-able-to-impersonate-server-principal-ps"></a>2. Ps 서버 보안 주체에 대한 IMPERSONATE 권한이 있는지 확인  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT HAS_PERMS_BY_NAME('Ps', 'LOGIN', 'IMPERSONATE');  
```  
  
### <a name="c-do-i-have-any-permissions-in-the-current-database"></a>3. 현재 데이터베이스에서 사용 권한이 있는지 확인  
  
```  
SELECT HAS_PERMS_BY_NAME(db_name(), 'DATABASE', 'ANY');  
```  
  
### <a name="d-does-database-principal-pd-have-any-permission-in-the-current-database"></a>4. 현재 데이터베이스에서 Pd 데이터베이스 보안 주체에 부여된 사용 권한 확인  
 `Pd` 보안 주체에 대한 IMPERSONATE 권한이 호출자에게 있다고 가정합니다.  
  
```  
EXECUTE AS user = 'Pd'  
GO  
SELECT HAS_PERMS_BY_NAME(db_name(), 'DATABASE', 'ANY');  
GO  
REVERT;  
GO  
```  
  
### <a name="e-can-i-create-procedures-and-tables-in-schema-s"></a>5. S 스키마에서 프로시저와 테이블을 만들 수 있는지 확인  
 다음 예에는 `ALTER`에 대한 `S` 권한과 데이터베이스에 대한 `CREATE PROCEDURE` 권한이 필요합니다. 테이블의 경우에도 비슷합니다.  
  
```  
SELECT HAS_PERMS_BY_NAME(db_name(), 'DATABASE', 'CREATE PROCEDURE')  
    & HAS_PERMS_BY_NAME('S', 'SCHEMA', 'ALTER') AS _can_create_procs,  
    HAS_PERMS_BY_NAME(db_name(), 'DATABASE', 'CREATE TABLE') &  
    HAS_PERMS_BY_NAME('S', 'SCHEMA', 'ALTER') AS _can_create_tables;  
```  
  
### <a name="f-which-tables-do-i-have-select-permission-on"></a>6. 어떤 테이블에 대해 SELECT 권한이 있는지 확인  
  
```  
SELECT HAS_PERMS_BY_NAME  
(QUOTENAME(SCHEMA_NAME(schema_id)) + '.' + QUOTENAME(name),   
    'OBJECT', 'SELECT') AS have_select, * FROM sys.tables  
```  
  
### <a name="g-do-i-have-insert-permission-on-the-salesperson-table-in-adventureworks2012"></a>7. AdventureWorks2012의 SalesPerson 테이블에 대한 INSERT 권한이 있는지 확인  
 다음 예에서는 `AdventureWorks2012`가 현재 데이터베이스 컨텍스트이고 두 부분으로 된 이름을 사용한다고 가정합니다.  
  
```  
SELECT HAS_PERMS_BY_NAME('Sales.SalesPerson', 'OBJECT', 'INSERT');  
```  
  
 다음 예에서는 현재 데이터베이스 컨텍스트에 대한 가정을 하지 않고 세 부분으로 된 이름을 사용합니다.  
  
```  
SELECT HAS_PERMS_BY_NAME('AdventureWorks2012.Sales.SalesPerson',   
    'OBJECT', 'INSERT');  
```  
  
### <a name="h-which-columns-of-table-t-do-i-have-select-permission-on"></a>8. T 테이블의 어떤 열에 대해 SELECT 권한이 있는지 확인  
  
```  
SELECT name AS column_name,   
    HAS_PERMS_BY_NAME('T', 'OBJECT', 'SELECT', name, 'COLUMN')   
    AS can_select   
    FROM sys.columns AS c   
    WHERE c.object_id=object_id('T');  
```  
  
## <a name="see-also"></a>관련 항목:  
 [사용 권한&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Securables](../../relational-databases/security/securables.md)   
 [사용 권한 계층&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [sys.fn_builtin_permissions&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)  
  
  

