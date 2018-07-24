---
title: REVOKE XML 스키마 컬렉션 사용 권한(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: pdw, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- REVOKE statement, XML schema collections
- XML schema collections [SQL Server], permissions
- schema collections [SQL Server], permissions
ms.assetid: 8ca0973c-30b2-4633-a165-c09b13cc81ae
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>= aps-pdw-2016 || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8cc2bc9a6eea98404ca8b4e445d182d1b06b4d12
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37987555"
---
# <a name="revoke-xml-schema-collection-permissions-transact-sql"></a>REVOKE XML 스키마 컬렉션 사용 권한(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  XML 스키마 컬렉션에 대해 부여되거나 거부된 사용 권한을 취소합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission [ ,...n ] ON   
    XML SCHEMA COLLECTION :: [ schema_name . ]  
    XML_schema_collection_name  
    { TO | FROM } <database_principal> [ ,...n ]  
        [ CASCADE ]  
    [ AS <database_principal> ]   
  
<database_principal> ::=   
        Database_user   
    | Database_role   
    | Application_role   
    | Database_user_mapped_to_Windows_User   
    | Database_user_mapped_to_Windows_Group   
    | Database_user_mapped_to_certificate   
    | Database_user_mapped_to_asymmetric_key   
    | Database_user_with_no_login   
```  
  
## <a name="arguments"></a>인수  
 *permission*  
 XML 스키마 컬렉션에 대해 취소할 수 있는 사용 권한을 지정합니다. 사용 권한 목록은 이 항목의 뒤에 나오는 주의 섹션을 참조하세요.  
  
 ON XML SCHEMA COLLECTION :: [ *schema_name***.** ] *XML_schema_collection_name*  
 사용 권한을 취소할 XML 스키마 컬렉션을 지정합니다. 범위 한정자(::)가 필요합니다. *schema_name*을 지정하지 않은 경우 기본 스키마가 사용됩니다. *schema_name*을 지정하지 않은 경우 기본 스키마 범위 한정자(.)가 사용됩니다.  
  
 GRANT OPTION  
 지정한 사용 권한을 다른 보안 주체에게 부여할 수 있는 권한이 취소됨을 나타냅니다. 사용 권한 자체는 취소되지 않습니다.  
  
> [!IMPORTANT]  
>  보안 주체에 GRANT 옵션 없이 지정된 사용 권한이 있는 경우 사용 권한 자체가 취소됩니다.  
  
 CASCADE  
 사용 권한이 취소된 보안 주체에게 사용 권한을 부여 받거나 거부당한 다른 보안 주체의 사용 권한도 취소됨을 나타냅니다.  
  
> [!CAUTION]  
>  WITH GRANT OPTION을 부여 받은 사용 권한이 연계되어 취소되면 해당 사용 권한의 GRANT 및 DENY가 모두 취소됩니다.  
  
 { TO | FROM } \<*database_principal*>  
 사용 권한을 취소할 보안 주체를 지정합니다.  
  
 \<database_principal>로서 이 쿼리를 실행하는 보안 주체가 사용 권한을 부여하는 권한을 취소할 수 있는 다른 보안 주체를 지정합니다.  
  
 *Database_user*  
 데이터베이스 사용자를 지정합니다.  
  
 *Database_role*  
 데이터베이스 역할을 지정합니다.  
  
 *Application_role*  
 응용 프로그램 역할을 지정합니다.  
  
 *Database_user_mapped_to_Windows_User*  
 Windows 사용자로 매핑된 데이터베이스 사용자를 지정합니다.  
  
 *Database_user_mapped_to_Windows_Group*  
 Windows 그룹으로 매핑된 데이터베이스 사용자를 지정합니다.  
  
 *Database_user_mapped_to_certificate*  
 인증서로 매핑된 데이터베이스 사용자를 지정합니다.  
  
 *Database_user_mapped_to_asymmetric_key*  
 비대칭 키로 매핑된 데이터베이스 사용자를 지정합니다.  
  
 *Database_user_with_no_login*  
 해당 서버 수준의 보안 주체가 없는 데이터베이스 사용자를 지정합니다.  
  
## <a name="remarks"></a>Remarks  
 XML 스키마 컬렉션에 대한 정보는 [sys.xml_schema_collections](../../relational-databases/system-catalog-views/sys-xml-schema-collections-transact-sql.md) 카탈로그 뷰에 표시됩니다.  
  
 GRANT OPTION을 지정하여 사용 권한이 부여된 보안 주체의 사용 권한을 취소할 경우 CASCADE를 지정하지 않으면 문이 실패합니다.  
  
 XML 스키마 컬렉션은 사용 권한 계층에서 해당 XML 스키마 컬렉션의 부모인 스키마에 포함된 스키마 수준 보안 개체입니다. 다음 표에는 XML 스키마 컬렉션에 대해 취소할 수 있는 가장 제한적인 특정 사용 권한이 의미상 이러한 사용 권한을 포함하는 보다 일반적인 사용 권한과 함께 나열되어 있습니다.  
  
|XML 스키마 컬렉션 사용 권한|XML 스키마 컬렉션 사용 권한에 포함된 사용 권한|스키마 사용 권한에 포함된 사용 권한|  
|--------------------------------------|-------------------------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER|  
|CONTROL|CONTROL|CONTROL|  
|CREATE 문을 실행하기 전에|CONTROL|CREATE 문을 실행하기 전에|  
|REFERENCES|CONTROL|REFERENCES|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 XML 스키마 컬렉션에 대한 CONTROL 권한이 필요합니다. AS 옵션을 사용하는 경우 지정한 보안 주체가 XML 스키마 컬렉션을 소유해야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 사용자 `EXECUTE`로부터 XML 스키마 컬렉션 `Invoices4`에 대한 `Wanida` 권한을 취소합니다. XML 스키마 컬렉션 `Invoices4`는 `Sales` 데이터베이스의 `AdventureWorks2012` 스키마에 위치합니다.  
  
 ```
 USE AdventureWorks2012;  
 REVOKE EXECUTE ON XML SCHEMA COLLECTION::Sales.Invoices4 FROM Wanida;  
 GO
 ```  
  
## <a name="see-also"></a>참고 항목  
 [GRANT XML 스키마 컬렉션 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-xml-schema-collection-permissions-transact-sql.md)   
 [DENY XML 스키마 컬렉션 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/deny-xml-schema-collection-permissions-transact-sql.md)   
 [sys.xml_schema_collections&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-xml-schema-collections-transact-sql.md)   
 [CREATE XML SCHEMA COLLECTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-xml-schema-collection-transact-sql.md)   
 [사용 권한&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

