---
title: ALTER SCHEMA (TRANSACT-SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/09/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 30ef553ccfba1f30be9b75f8d0290115be395925
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="alter-schema-transact-sql"></a>ALTER SCHEMA(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  스키마 간에 보안 개체를 이동합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
ALTER SCHEMA schema_name   
   TRANSFER [ <entity_type> :: ] securable_name   
[;]  
  
<entity_type> ::=  
    {  
    Object | Type | XML Schema Collection  
    }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER SCHEMA schema_name   
   TRANSFER [ OBJECT :: ] securable_name   
[;]  
```  
  
## <a name="arguments"></a>인수  
 *schema_name*  
 현재 데이터베이스에서 보안 개체가 이동될 스키마의 이름입니다. SYS 또는 INFORMATION_SCHEMA는 지정할 수 없습니다.  
  
 \<entity_type>  
 소유자가 변경될 엔터티의 클래스입니다. Object가 기본값입니다.  
  
 *securable_name*  
 스키마 범위의 한 부분 또는 두 부분으로 이루어진 이름을 스키마로 이동 될 보안 개체입니다.  
  
## <a name="remarks"></a>주의  
 사용자와 스키마는 완전히 분리됩니다.  
  
 ALTER SCHEMA는 같은 데이터베이스에서 스키마 간에 보안 개체를 이동할 때만 사용할 수 있습니다. 스키마 내에서 보안 개체를 변경하거나 삭제하려면 해당 보안 개체와 관련된 ALTER 또는 DROP 문을 사용합니다.  
  
 한 부분 이름에 사용 되 면 *securable_name*, 이름 확인 규칙이 현재 적용는 보안 개체를 찾으려고 합니다.  
  
 보안 개체를 새 스키마로 이동하면 해당 보안 개체와 연결된 사용 권한이 모두 삭제됩니다. 보안 개체 소유자가 명시적으로 설정된 경우 소유자는 그대로 유지됩니다. 보안 개체 소유자가 SCHEMA OWNER로 설정된 경우에는 소유자가 SCHEMA OWNER로 유지되지만 이동 후 SCHEMA OWNER는 새 스키마의 소유자로 확인됩니다. 새 소유자의 principal_id는 NULL이 됩니다.  
  
 저장된 프로시저, 함수, 뷰 또는 트리거를 이동 합니다. 변경 되지 것입니다 스키마 이름, 현재, 해당 개체가 정의 열에는 [sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) 카탈로그 뷰 또는 사용 하 여 가져온는 [ OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md) 기본 제공 함수입니다. 따라서 이러한 개체 유형의 이동 하려면 ALTER SCHEMA를 사용 하지 않도록 하는 것이 좋습니다. 대신, 삭제 하 고 새 스키마에 개체를 다시 만듭니다.  
  
 예: 테이블 또는 동의어 개체를 이동 합니다. 해당 개체에 대 한 참조가 자동으로 업데이트 되지 않습니다. 전송된 개체를 직접 참조 하는 개체를 수정 해야 합니다. 예를 들어 테이블을 이동 하는 경우 해당 테이블이 트리거에서 참조 되는 새 스키마 이름을 반영 하도록 트리거를 수정 해야 합니다. 사용 하 여 [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) 를 이동 하기 전에 개체에 종속성을 나열 합니다.  

 사용 하 여 테이블의 스키마를 변경 하려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]개체 탐색기에서 테이블 단추로 클릭 하 고 클릭 **디자인**합니다. 키를 눌러 **F4** 속성 창을 엽니다. 에 **스키마** 상자에서 새 스키마를 선택 합니다.  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>Permissions  
 한 스키마에서 다른 스키마로 보안 개체를 이동하려면 현재 사용자에게 보안 개체(스키마가 아님)에 대한 CONTROL 권한과 대상 스키마에 대한 ALTER 권한이 있어야 합니다.  
  
 사용자는 보안 개체에 EXECUTE AS OWNER 사양이 소유자가 SCHEMA OWNER로 설정 하는 경우 대상 스키마의 소유자에 대 한 IMPERSONATE 권한이 레이블에도 되어야 합니다.  
  
 이동되는 보안 개체와 연결된 사용 권한은 이동 시 모두 삭제됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-transferring-ownership-of-a-table"></a>1. 테이블의 소유권 이전  
 다음 예에서는 `HumanResources` 스키마에서 `Address` 스키마로 `Person` 테이블을 이동하여 HumanResources 스키마를 수정합니다.  
  
```  
USE AdventureWorks2012;  
GO  
ALTER SCHEMA HumanResources TRANSFER Person.Address;  
GO  
```  
  
### <a name="b-transferring-ownership-of-a-type"></a>2. 형식의 소유권 이전  
 다음 예에서는 `Production` 스키마에 형식을 만든 다음 해당 형식을 `Person` 스키마로 전송합니다.  
  
```  
USE AdventureWorks2012;  
GO  
  
CREATE TYPE Production.TestType FROM [varchar](10) NOT NULL ;  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-transferring-ownership-of-a-table"></a>3. 테이블의 소유권 이전  
 다음 예제에서는 테이블을 만듭니다 `Region` 에 `dbo` 스키마를 만듭니다는 `Sales` 스키마 및 이동의 `Region` 에서 테이블의 `dbo` 스키마를는 `Sales` 스키마.  
  
```  
CREATE TABLE dbo.Region   
    (Region_id int NOT NULL,  
    Region_Name char(5) NOT NULL)  
WITH (DISTRIBUTION = REPLICATE);  
GO  
  
CREATE SCHEMA Sales;  
GO  
  
ALTER SCHEMA Sales TRANSFER OBJECT::dbo.Region;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [스키마 &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-schema-transact-sql.md)   
 [DROP 스키마 &#40; Transact SQL &#41;](../../t-sql/statements/drop-schema-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

