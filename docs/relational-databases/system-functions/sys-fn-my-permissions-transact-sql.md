---
title: sys.fn_my_permissions (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.fn_my_permissions_TSQL
- fn_my_permissions_TSQL
- sys.fn_my_permissions
- fn_my_permissions
dev_langs:
- TSQL
helpviewer_keywords:
- fn_my_permissions function
- sys.fn_my_permissions function
ms.assetid: 30f97f00-03d8-443a-9de9-9ec420b7699b
caps.latest.revision: 21
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7e37caf83682bedf95cbec181a25922d3bf47d12
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysfnmypermissions-transact-sql"></a>sys.fn_my_permissions(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  보안 개체에 대해 보안 주체에 부여된 유효 사용 권한 목록을 반환합니다. 관련된 함수는 [HAS_PERMS_BY_NAME](../../t-sql/functions/has-perms-by-name-transact-sql.md)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
fn_my_permissions ( securable , 'securable_class' )  
```  
  
## <a name="arguments"></a>인수  
 *securable*  
 보안 개체의 이름입니다. 보안 개체가 서버 또는 데이터베이스인 경우 이 값은 NULL로 설정해야 합니다. *securable*은 **sysname** 형식의 스칼라 식입니다. *보안 개체* 다중 부분 이름일 수 있습니다.  
  
 '*securable_class*'  
 권한을 나열할 보안 개체의 클래스 이름입니다. *b l e _* 는 **sysname**합니다. *b l e _* 다음 중 하나 여야 합니다: 응용 프로그램 역할, 어셈블리, 비대칭 키, 인증서, 계약, 데이터베이스, ENDPOINT, FULLTEXT CATALOG, 로그인, 메시지 유형, 개체, REMOTE SERVICE BINDING, 역할, 경로, 스키마, 서버, 서비스 대칭 키, 형식, 사용자, XML 스키마 컬렉션입니다.  
  
## <a name="columns-returned"></a>반환되는 열  
 다음 표에서 열을 나열 하는 **fn_my_permissions** 반환 합니다. 반환되는 각 행은 해당 보안 개체에 대해 현재 보안 컨텍스트가 가지는 사용 권한을 설명합니다. 쿼리가 실패하는 경우 NULL을 반환합니다.  
  
|열 이름|유형|Description|  
|-----------------|----------|-----------------|  
|entity_name|**sysname**|나열된 사용 권한이 유효하게 부여되는 보안 개체의 이름입니다.|  
|subentity_name|**sysname**|보안 개체가 열인 경우 열 이름이며 그렇지 않은 경우에는 NULL입니다.|  
|permission_name|**nvarchar**|사용 권한의 이름입니다.|  
  
## <a name="remarks"></a>주의  
 이 테이블 반환 함수는 지정된 보안 개체에 대해 해당 보안 주체가 가진 유효 사용 권한의 목록을 반환합니다. 유효 사용 권한은 다음 중 하나입니다.  
  
-   보안 주체에게 직접 부여되고 거부되지 않은 사용 권한  
  
-   보안 주체가 소유하는 더 높은 수준의 사용 권한에 포함되고 거부되지 않은 사용 권한  
  
-   보안 주체가 멤버로 속한 역할이나 그룹에 부여되고 거부되지 않은 사용 권한  
  
-   보안 주체가 멤버로 속한 역할이나 그룹이 소유하고 거부되지 않은 사용 권한  
  
 사용 권한은 항상 호출자의 보안 컨텍스트에서 평가됩니다. 다른 보안 주체에게 유효 사용 권한이 있는지 여부를 확인하려면 호출자에게 해당 보안 주체에 대한 IMPERSONATE 권한이 있어야 합니다.  
  
 스키마 수준 엔터티의 경우 한 부분, 두 부분 또는 세 부분으로 된 Null이 아닌 이름을 사용할 수 있습니다. 데이터베이스 수준 엔터티의 경우 한 부분으로 된 이름을 허용 된 null 값은 "*현재 데이터베이스*"입니다. 서버 자체인 경우에는 Null 값("현재 서버"를 나타냄)이 필요합니다. **fn_my_permissions** 연결된 된 서버에 대 한 권한을 확인할 수 없습니다.  
  
 다음 쿼리는 기본 제공 보안 개체 클래스의 목록을 반환합니다.  
  
```  
SELECT DISTINCT class_desc FROM fn_builtin_permissions(default)  
    ORDER BY class_desc;  
GO  
```  
  
 값으로 기본을 제공 하는 경우 *보안* 또는 *b l e _*, 값을 NULL로 해석 됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-listing-effective-permissions-on-the-server"></a>1. 서버에 대한 유효 사용 권한 나열  
 다음 예에서는 서버에 대한 호출자의 유효 사용 권한 목록을 반환합니다.  
  
```  
SELECT * FROM fn_my_permissions(NULL, 'SERVER');  
GO  
```  
  
### <a name="b-listing-effective-permissions-on-the-database"></a>2. 데이터베이스에 대한 유효 사용 권한 나열  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 대한 호출자의 유효 사용 권한 목록을 반환합니다.  
  
```  
USE AdventureWorks2012;  
SELECT * FROM fn_my_permissions (NULL, 'DATABASE');  
GO  
```  
  
### <a name="c-listing-effective-permissions-on-a-view"></a>3. 뷰에 대한 유효 사용 권한 나열  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 `vIndividualCustomer` 스키마에 있는 `Sales` 뷰에 대한 호출자의 유효 사용 권한 목록을 반환합니다.  
  
```  
USE AdventureWorks2012;  
SELECT * FROM fn_my_permissions('Sales.vIndividualCustomer', 'OBJECT')   
    ORDER BY subentity_name, permission_name ;   
GO   
```  
  
### <a name="d-listing-effective-permissions-of-another-user"></a>4. 다른 사용자의 유효 사용 권한 나열  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 `Wanida` 스키마에 있는 `Employee` 테이블에 대한 데이터베이스 사용자 `HumanResources`의 유효 사용 권한 목록을 반환합니다. 호출자는 사용자 `Wanida`에 대한 IMPERSONATE 사용 권한이 필요합니다.  
  
```  
EXECUTE AS USER = 'Wanida';  
SELECT * FROM fn_my_permissions('HumanResources.Employee', 'OBJECT')   
    ORDER BY subentity_name, permission_name ;    
REVERT;  
GO  
```  
  
### <a name="e-listing-effective-permissions-on-a-certificate"></a>5. 인증서에 대한 유효 사용 권한 나열  
 다음 예에서는 현재 데이터베이스에서 이름이 `Shipping47`인 인증서에 대한 호출자의 유효 사용 권한 목록을 반환합니다.  
  
```  
SELECT * FROM fn_my_permissions('Shipping47', 'CERTIFICATE');  
GO  
```  
  
### <a name="f-listing-effective-permissions-on-an-xml-schema-collection"></a>6. XML 스키마 컬렉션에 대한 유효 사용 권한 나열  
 다음 예제에서는 명명 된 XML 스키마 컬렉션에는 호출자의 유효 사용 권한 목록을 반환 `ProductDescriptionSchemaCollection` 에 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스입니다.  
  
```  
USE AdventureWorks2012;  
SELECT * FROM fn_my_permissions('ProductDescriptionSchemaCollection',  
    'XML SCHEMA COLLECTION');  
GO  
```  
  
### <a name="g-listing-effective-permissions-on-a-database-user"></a>7. 데이터베이스 사용자에 대한 유효 사용 권한 나열  
 다음 예에서는 현재 데이터베이스에서 이름이 `MalikAr`인 사용자에 대한 호출자의 유효 사용 권한 목록을 반환합니다.  
  
```  
SELECT * FROM fn_my_permissions('MalikAr', 'USER');  
GO  
```  
  
### <a name="h-listing-effective-permissions-of-another-login"></a>8. 다른 로그인의 유효 사용 권한 나열  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 `WanidaBenshoof` 스키마에 있는 `Employee` 테이블에 대한 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 로그인 `HumanResources`의 유효 사용 권한 목록을 반환합니다. 호출자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 `WanidaBenshoof`에 대한 IMPERSONATE 사용 권한이 필요합니다.  
  
```  
EXECUTE AS LOGIN = 'WanidaBenshoof';  
SELECT * FROM fn_my_permissions('AdventureWorks2012.HumanResources.Employee', 'OBJECT')   
    ORDER BY subentity_name, permission_name ;    
REVERT;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [보안 함수&#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [사용 권한&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Securables](../../relational-databases/security/securables.md)   
 [사용 권한 계층&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [sys.fn_builtin_permissions&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md)  
  
  
