---
title: sys. fn_my_permissions (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 0a64db42ba04e864752559bb2d2b895625f2c9f5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68122630"
---
# <a name="sysfn_my_permissions-transact-sql"></a>sys.fn_my_permissions(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  보안 개체에 대해 보안 주체에 부여된 유효 사용 권한 목록을 반환합니다. 관련 함수를 [HAS_PERMS_BY_NAME](../../t-sql/functions/has-perms-by-name-transact-sql.md)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
fn_my_permissions ( securable , 'securable_class' )  
```  
  
## <a name="arguments"></a>인수  
 *안전한*  
 보안 개체의 이름입니다. 보안 개체가 서버 또는 데이터베이스인 경우 이 값은 NULL로 설정해야 합니다. *보안* 개체는 **sysname**형식의 스칼라 식입니다. *보안* 개체는 여러 부분으로 된 이름일 수 있습니다.  
  
 '*securable_class*'  
 권한을 나열할 보안 개체의 클래스 이름입니다. *securable_class* 는 **sysname**입니다. *securable_class* 는 응용 프로그램 역할, 어셈블리, 비대칭 키, 인증서, 계약, 데이터베이스, 끝점, 전체 텍스트 카탈로그, 로그인, 메시지 유형, 개체, 원격 서비스 바인딩, 역할, 경로, 스키마, 서버, 서비스, 대칭 키, 형식, 사용자, XML 스키마 컬렉션 중 하나 여야 합니다.  
  
## <a name="columns-returned"></a>반환되는 열  
 다음 표에서는 **fn_my_permissions** 반환 하는 열을 나열 합니다. 반환되는 각 행은 해당 보안 개체에 대해 현재 보안 컨텍스트가 가지는 사용 권한을 설명합니다. 쿼리가 실패하는 경우 NULL을 반환합니다.  
  
|열 이름|Type|Description|  
|-----------------|----------|-----------------|  
|entity_name|**sysname**|나열된 사용 권한이 유효하게 부여되는 보안 개체의 이름입니다.|  
|subentity_name|**sysname**|보안 개체가 열인 경우 열 이름이며 그렇지 않은 경우에는 NULL입니다.|  
|permission_name|**nvarchar**|사용 권한의 이름입니다.|  
  
## <a name="remarks"></a>설명  
 이 테이블 반환 함수는 지정된 보안 개체에 대해 해당 보안 주체가 가진 유효 사용 권한의 목록을 반환합니다. 유효 사용 권한은 다음 중 하나입니다.  
  
-   보안 주체에게 직접 부여되고 거부되지 않은 사용 권한  
  
-   보안 주체가 소유하는 더 높은 수준의 사용 권한에 포함되고 거부되지 않은 사용 권한  
  
-   보안 주체가 멤버로 속한 역할이나 그룹에 부여되고 거부되지 않은 사용 권한  
  
-   보안 주체가 멤버로 속한 역할이나 그룹이 소유하고 거부되지 않은 사용 권한  
  
 사용 권한은 항상 호출자의 보안 컨텍스트에서 평가됩니다. 다른 보안 주체에게 유효 사용 권한이 있는지 여부를 확인하려면 호출자에게 해당 보안 주체에 대한 IMPERSONATE 권한이 있어야 합니다.  
  
 스키마 수준 엔터티의 경우 한 부분, 두 부분 또는 세 부분으로 된 Null이 아닌 이름을 사용할 수 있습니다. 데이터베이스 수준 엔터티의 경우 한 부분으로 된 이름을 사용할 수 있으며 null 값은 "*현재 데이터베이스*"를 의미 합니다. 서버 자체인 경우에는 Null 값("현재 서버"를 나타냄)이 필요합니다. **fn_my_permissions** 은 (는) 연결 된 서버에 대 한 사용 권한을 확인할 수 없습니다.  
  
 다음 쿼리는 기본 제공 보안 개체 클래스의 목록을 반환합니다.  
  
```  
SELECT DISTINCT class_desc FROM fn_builtin_permissions(default)  
    ORDER BY class_desc;  
GO  
```  
  
 기본값을 *보안* 개체 또는 *securable_class*값으로 제공 하면 값은 NULL로 해석 됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-listing-effective-permissions-on-the-server"></a>A. 서버에 대한 유효 사용 권한 나열  
 다음 예에서는 서버에 대한 호출자의 유효 사용 권한 목록을 반환합니다.  
  
```  
SELECT * FROM fn_my_permissions(NULL, 'SERVER');  
GO  
```  
  
### <a name="b-listing-effective-permissions-on-the-database"></a>B. 데이터베이스에 대한 유효 사용 권한 나열  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 대한 호출자의 유효 사용 권한 목록을 반환합니다.  
  
```  
USE AdventureWorks2012;  
SELECT * FROM fn_my_permissions (NULL, 'DATABASE');  
GO  
```  
  
### <a name="c-listing-effective-permissions-on-a-view"></a>C. 뷰에 대한 유효 사용 권한 나열  
 다음 예에서는 `vIndividualCustomer` 데이터베이스의 `Sales` 스키마에 있는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 뷰에 대한 호출자의 유효 사용 권한 목록을 반환합니다.  
  
```  
USE AdventureWorks2012;  
SELECT * FROM fn_my_permissions('Sales.vIndividualCustomer', 'OBJECT')   
    ORDER BY subentity_name, permission_name ;   
GO   
```  
  
### <a name="d-listing-effective-permissions-of-another-user"></a>D. 다른 사용자의 유효 사용 권한 나열  
 다음 예에서는 `Wanida` 데이터베이스의 `Employee` 스키마에 있는 `HumanResources` 테이블에 대한 데이터베이스 사용자 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]의 유효 사용 권한 목록을 반환합니다. 호출자는 사용자 `Wanida`에 대한 IMPERSONATE 사용 권한이 필요합니다.  
  
```  
EXECUTE AS USER = 'Wanida';  
SELECT * FROM fn_my_permissions('HumanResources.Employee', 'OBJECT')   
    ORDER BY subentity_name, permission_name ;    
REVERT;  
GO  
```  
  
### <a name="e-listing-effective-permissions-on-a-certificate"></a>E. 인증서에 대한 유효 사용 권한 나열  
 다음 예에서는 현재 데이터베이스에서 이름이 `Shipping47`인 인증서에 대한 호출자의 유효 사용 권한 목록을 반환합니다.  
  
```  
SELECT * FROM fn_my_permissions('Shipping47', 'CERTIFICATE');  
GO  
```  
  
### <a name="f-listing-effective-permissions-on-an-xml-schema-collection"></a>F. XML 스키마 컬렉션에 대한 유효 사용 권한 나열  
 다음 예에서는 `ProductDescriptionSchemaCollection` [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 있는 XML 스키마 컬렉션에 대 한 호출자의 유효 사용 권한 목록을 반환 합니다.  
  
```  
USE AdventureWorks2012;  
SELECT * FROM fn_my_permissions('ProductDescriptionSchemaCollection',  
    'XML SCHEMA COLLECTION');  
GO  
```  
  
### <a name="g-listing-effective-permissions-on-a-database-user"></a>G. 데이터베이스 사용자에 대한 유효 사용 권한 나열  
 다음 예에서는 현재 데이터베이스에서 이름이 `MalikAr`인 사용자에 대한 호출자의 유효 사용 권한 목록을 반환합니다.  
  
```  
SELECT * FROM fn_my_permissions('MalikAr', 'USER');  
GO  
```  
  
### <a name="h-listing-effective-permissions-of-another-login"></a>H. 다른 로그인의 유효 사용 권한 나열  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 `WanidaBenshoof` 스키마에 있는 `Employee` 테이블에 대한 `HumanResources` 로그인 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]의 유효 사용 권한 목록을 반환합니다. 호출자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 `WanidaBenshoof`에 대한 IMPERSONATE 사용 권한이 필요합니다.  
  
```  
EXECUTE AS LOGIN = 'WanidaBenshoof';  
SELECT * FROM fn_my_permissions('AdventureWorks2012.HumanResources.Employee', 'OBJECT')   
    ORDER BY subentity_name, permission_name ;    
REVERT;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [보안 함수&#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [권한 &#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [보안 개체](../../relational-databases/security/securables.md)   
 [사용 권한 계층&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [sys.fn_builtin_permissions&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [Transact-sql&#41;&#40;보안 카탈로그 뷰](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md)  
  
  
