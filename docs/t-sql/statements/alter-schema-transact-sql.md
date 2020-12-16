---
description: ALTER SCHEMA(Transact-SQL)
title: ALTER SCHEMA(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER SCHEMA
- ALTER_SCHEMA_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- objects [SQL Server], transferring
- transferring objects between schemas
- ALTER SCHEMA statement
- schemas [SQL Server], modifying
- modifying schemas
ms.assetid: 0a760138-460e-410a-a3c1-d60af03bf2ed
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 02ba4172348ec740986e0d09c2d0296ce399160d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97474174"
---
# <a name="alter-schema-transact-sql"></a>ALTER SCHEMA(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  스키마 간에 보안 개체를 이동합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
-- Syntax for SQL Server and Azure SQL Database  
  
ALTER SCHEMA schema_name   
   TRANSFER [ <entity_type> :: ] securable_name   
[;]  
  
<entity_type> ::=  
    {  
    Object | Type | XML Schema Collection  
    }  
```  
  
```syntaxsql
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
ALTER SCHEMA schema_name   
   TRANSFER [ OBJECT :: ] securable_name   
[;]  
```  
  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *schema_name*  
 현재 데이터베이스에서 보안 개체가 이동될 스키마의 이름입니다. SYS 또는 INFORMATION_SCHEMA는 지정할 수 없습니다.  
  
 \<entity_type>  
 소유자가 변경될 엔터티의 클래스입니다. Object가 기본값입니다.  
  
 *securable_name*  
 스키마에 포함된 보안 개체 중에서 스키마로 이동될 보안 개체의 한 부분 또는 두 부분으로 구성된 이름입니다.  
  
## <a name="remarks"></a>설명  
 사용자와 스키마는 완전히 분리됩니다.  
  
 ALTER SCHEMA는 같은 데이터베이스에서 스키마 간에 보안 개체를 이동할 때만 사용할 수 있습니다. 스키마 내에서 보안 개체를 변경하거나 삭제하려면 해당 보안 개체와 관련된 ALTER 또는 DROP 문을 사용합니다.  
  
 한 부분으로 구성된 이름이 *securable_name* 에 사용되면 현재 적용 중인 이름 확인 규칙이 보안 개체를 찾는 데 사용됩니다.  
  
 보안 개체를 새 스키마로 이동하면 해당 보안 개체와 연결된 사용 권한이 모두 삭제됩니다. 보안 개체 소유자가 명시적으로 설정된 경우 소유자는 그대로 유지됩니다. 보안 개체 소유자가 SCHEMA OWNER로 설정된 경우에는 소유자가 SCHEMA OWNER로 유지되지만 이동 후 SCHEMA OWNER는 새 스키마의 소유자로 확인됩니다. 새 소유자의 principal_id는 NULL이 됩니다.  
  
 저장 프로시저, 함수, 뷰 또는 트리거를 이동해도 [sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) 카탈로그 뷰의 정의 열에 있거나 [OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md) 기본 함수를 사용하여 얻은 해당 개체의 스키마 이름(있는 경우)는 변경되지 않습니다. 따라서 이러한 개체 유형의 이름을 변경할 때 ALTER SCHEMA를 사용하지 않는 것이 좋습니다. 대신 해당 개체를 삭제하고 새 스키마로 다시 만듭니다.  
  
 테이블이나 동의어와 같은 개체를 이동할 경우 이 개체를 참조하는 개체는 자동으로 업데이트되지 않습니다. 이동된 개체를 참조하는 개체는 수동으로 수정해야 합니다. 예를 들어 테이블 이름을 바꿨고 해당 테이블이 트리거에서 참조되는 경우 트리거를 수정하여 새로운 스키마 이름을 적용해야 합니다. [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)를 사용하여 이 개체에 종속된 개체를 나열한 다음, 개체를 이동할 수 있습니다.  

 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 테이블의 스키마를 변경하려면 개체 탐색기에서 테이블이나 뷰를 마우스 오른쪽 단추로 클릭한 다음, **디자인** 을 클릭합니다. **F4** 키를 눌러 속성 창을 엽니다. **스키마** 상자에서 새 스키마를 선택합니다.  
 
 ALTER SCHEMA는 스키마 수준 잠금을 사용합니다.
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>사용 권한  
 한 스키마에서 다른 스키마로 보안 개체를 이동하려면 현재 사용자에게 보안 개체(스키마가 아님)에 대한 CONTROL 권한과 대상 스키마에 대한 ALTER 권한이 있어야 합니다.  
  
 보안 개체에 EXECUTE AS OWNER 사양이 있고 소유자가 SCHEMA OWNER로 설정된 경우에는 사용자가 대상 스키마의 소유자에 대한 IMPERSONATE 권한도 가져야 합니다.  
  
 이동되는 보안 개체와 연결된 사용 권한은 이동 시 모두 삭제됩니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-transferring-ownership-of-a-table"></a>A. 테이블의 소유권 이전  
 다음 예제에서는 `Address` 테이블을 `Person` 스키마에서 ‘HumanResources’ 스키마로 이동하여 `HumanResources` 스키마를 수정합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
ALTER SCHEMA HumanResources TRANSFER Person.Address;  
GO  
```  
  
### <a name="b-transferring-ownership-of-a-type"></a>B. 형식의 소유권 이전  
 다음 예에서는 `Production` 스키마에 형식을 만든 다음 해당 형식을 `Person` 스키마로 전송합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
  
CREATE TYPE Production.TestType FROM [VARCHAR](10) NOT NULL ;  
GO  
  
-- Check the type owner.  
SELECT sys.types.name, sys.types.schema_id, sys.schemas.name  
    FROM sys.types JOIN sys.schemas   
        ON sys.types.schema_id = sys.schemas.schema_id   
    WHERE sys.types.name = 'TestType' ;  
GO  
  
-- Change the type to the Person schema.  
ALTER SCHEMA Person TRANSFER type::Production.TestType ;  
GO  
  
-- Check the type owner.  
SELECT sys.types.name, sys.types.schema_id, sys.schemas.name  
    FROM sys.types JOIN sys.schemas   
        ON sys.types.schema_id = sys.schemas.schema_id   
    WHERE sys.types.name = 'TestType' ;  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-transferring-ownership-of-a-table"></a>C. 테이블의 소유권 이전  
 다음 예는 `dbo` 스키마에 `Region` 테이블을 만들고, `Sales` 스키마를 만든 다음, `Region` 스키마에서 `dbo` 스키마로 `Sales` 테이블을 이동합니다.  
  
```sql  
CREATE TABLE dbo.Region   
    (Region_id INT NOT NULL,  
    Region_Name CHAR(5) NOT NULL)  
WITH (DISTRIBUTION = REPLICATE);  
GO  
  
CREATE SCHEMA Sales;  
GO  
  
ALTER SCHEMA Sales TRANSFER OBJECT::dbo.Region;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE SCHEMA&#40;Transact-SQL&#41;](../../t-sql/statements/create-schema-transact-sql.md)   
 [DROP SCHEMA&#40;Transact-SQL&#41;](../../t-sql/statements/drop-schema-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

