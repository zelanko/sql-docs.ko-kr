---
title: SQL Server 시스템 카탈로그 FAQ | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- catalog views [SQL Server], examples
- metadata [SQL Server], frequently asked questions
- metadata [SQL Server], example queries
- system catalogs [SQL Server], example queries
- catalog views [SQL Server], frequently asked questions
ms.assetid: ca202580-c37e-4ccd-9275-77ce79481f64
author: stevestein
ms.author: sstein
ms.openlocfilehash: c16bc1e0c8d8d6b5a62e2823aa011b58520b1d00
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68018357"
---
# <a name="querying-the-sql-server-system-catalog-faq"></a>SQL Server 시스템 카탈로그 쿼리에 대한 질문과 대답
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 질문과 대답 목록을 제공합니다. 질문에 대한 대답은 카탈로그 뷰를 기반으로 하는 쿼리입니다.  
  
##  <a name="_TOP"></a> 질문과 대답  
 아래 섹션에서는 질문과 대답을 범주별로 보여 줍니다.  
  
### <a name="data-types"></a>데이터 형식  
  
-   [지정된 된 테이블의 열 데이터 형식을 찾으려면 어떻게 해야 합니까?](#_FAQ7)  
  
-   [지정된 된 테이블의 LOB 데이터 형식을 찾으려면 어떻게 해야 합니까?](#_FAQ14)  
  
-   [지정 된 데이터 형식에 종속 되는 열을 찾으려면 어떻게 해야 합니까?](#_FAQ22)  
  
-   [지정한 CLR 사용자 정의 형식 또는 별칭 데이터 형식에 종속 된 계산된 열 찾기](#_FAQ23)  
  
-   [지정한 CLR 사용자 정의 형식 또는 별칭 형식에 종속 된 매개 변수를 찾으려면 어떻게 해야 합니까?](#_FAQ24)  
  
-   [지정한 CLR 사용자 정의 형식에 종속 된 CHECK 제약 조건을 찾으려면 어떻게 해야 합니까?](#_FAQ25)  
  
-   [뷰, TRANSACT-SQL 함수 및 TRANSACT-SQL 저장 프로시저는 지정한 CLR 사용자 정의 형식 또는 별칭 형식에 종속 된 찾으려면 어떻게](#_FAQ26)  
  
### <a name="tables-indexes-views-and-constraints"></a>테이블, 인덱스, 뷰 및 제약 조건  
  
-   [지정된 된 데이터베이스의 모든 사용자 정의 테이블 찾기](#_FAQ31)  
  
-   [지정된 된 데이터베이스에서 클러스터형된 인덱스가 없는 모든 테이블 찾기](#_FAQ1)  
  
-   [인덱스에 있지 않은 모든 테이블 찾기](#_FAQ4)  
  
-   [기본 키가 없는 모든 테이블 찾기](#_FAQ3)  
  
-   [Id 열이 있는 모든 테이블 찾기](#_FAQ5)  
  
-   [모든 테이블 및 인덱스 분할 된 찾으려면 어떻게](#_FAQ32)  
  
-   [데이터베이스의 모든 뷰 찾기](#_FAQ13)  
  
-   [뷰의 정의 찾으려면 어떻게 해야 합니까?](#_FAQ35)  
  
-   [최근 N 일 동안에서 수정 된 모든 엔터티를 찾으려면 어떻게 해야 합니까?](#_FAQ6)  
  
-   [지정된 된 테이블에 대 한 기본 키의 열을 찾으려면 어떻게 해야 합니까?](#_FAQ16)  
  
-   [지정된 된 테이블에 대 한 외래 키의 열을 찾으려면 어떻게 해야 합니까?](#_FAQ17)  
  
-   [열이 계산된 열 식에 사용 되 면 어떻게 확인 합니까?](#_FAQ20)  
  
-   [계산된 열 식에 사용 되는 모든 열 찾으려면 어떻게 해야 합니까?](#_FAQ21)  
  
-   [지정된 된 테이블에 대 한 모든 제약 조건을 찾으려면 어떻게 해야 합니까?](#_FAQ27)  
  
-   [지정된 된 테이블에 대 한 인덱스를 모두 찾으려면 어떻게 해야 합니까?](#_FAQ28)  
  
-   [지정 된 열 이름이 있는 모든 테이블 찾기](#_FAQ30)  
  
-   [지정된 된 개체에서 통계를 찾으려면 어떻게 해야 합니까?](#_FAQ33)  
  
-   [지정된 된 개체에서 통계 및 통계 열을 모두 찾으려면 수행는 어떻게](#_FAQ34)  
  
### <a name="modules-stored-procedures-user-defined-functions-and-triggers"></a>모듈(저장 프로시저, 사용자 정의 함수 및 트리거)  
  
-   [데이터베이스에서 저장된 프로시저를 모두 찾으려면 어떻게 해야 합니까?](#_FAQ9)  
  
-   [데이터베이스의 모든 사용자 정의 함수를 찾으려면 어떻게 해야 합니까?](#_FAQ12)  
  
-   [지정한 저장 프로시저나 함수에 대 한 매개 변수를 찾으려면 어떻게 해야 합니까?](#_FAQ10)  
  
-   [지정된 된 함수에서 종속성을 찾으려면 어떻게 해야 합니까?](#_FAQ8)  
  
-   [모듈의 정의 보는 방법](#_FAQ15)  
  
-   [서버 수준 트리거의 정의 보는 방법](#_FAQ19)  
  
### <a name="schemas-users-roles-and-permissions"></a>스키마, 사용자, 역할 및 사용 권한  
  
-   [지정된 된 스키마에 포함 된 엔터티의 모든 소유자를 찾으려면 어떻게 해야 합니까?](#_FAQ2)  
  
-   [지정한 보안 주체에 허용 또는 거부 권한을 찾으려면 어떻게 해야 합니까?](#_FAQ18)  
  
## <a name="answers"></a>대답  
  
###  <a name="_FAQ1"></a> 지정된 된 데이터베이스에서 클러스터형된 인덱스가 없는 모든 테이블 찾기  
 다음 쿼리를 실행하기 전에 `<database_name>`을 올바른 데이터베이스 이름으로 대체합니다.  
  
```  
SELECT SCHEMA_NAME(t.schema_id) AS schema_name, t.name AS table_name  
FROM sys.tables AS t  
WHERE NOT EXISTS   
   (  
     SELECT * FROM sys.indexes AS i  
     WHERE i.object_id = t.object_id  
     AND i.type = 1  -- or type_desc = 'CLUSTERED'  
   )  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
 또는 다음 예와 같이 `OBJECTPROPERTY` 함수를 사용할 수 있습니다.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name, name AS table_name  
FROM sys.tables   
WHERE OBJECTPROPERTY(object_id,'TableHasClustIndex') = 0  
ORDER BY schema_id, name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ2"></a> 지정된 된 스키마에 포함 된 엔터티의 모든 소유자를 찾으려면 어떻게 해야 합니까?  
 다음 쿼리를 실행하기 전에 `<database_name>` 및 `<schema_name>`을 올바른 이름으로 대체합니다.  
  
```  
USE <database_name>;  
GO  
SELECT 'OBJECT' AS entity_type  
    ,USER_NAME(OBJECTPROPERTY(object_id, 'OwnerId')) AS owner_name  
    ,name   
FROM sys.objects WHERE SCHEMA_NAME(schema_id) = '<schema_name>'  
UNION   
SELECT 'TYPE' AS entity_type  
    ,USER_NAME(TYPEPROPERTY(SCHEMA_NAME(schema_id) + '.' + name, 'OwnerId')) AS owner_name  
    ,name   
FROM sys.types WHERE SCHEMA_NAME(schema_id) = '<schema_name>'   
UNION  
SELECT 'XML SCHEMA COLLECTION' AS entity_type   
    ,COALESCE(USER_NAME(xsc.principal_id),USER_NAME(s.principal_id)) AS owner_name  
    ,xsc.name   
FROM sys.xml_schema_collections AS xsc JOIN sys.schemas AS s  
    ON s.schema_id = xsc.schema_id  
WHERE s.name = '<schema_name>';  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ3"></a> 기본 키가 없는 모든 테이블 찾기  
 다음 쿼리를 실행하기 전에 `<database_name>`을 올바른 데이터베이스 이름으로 대체합니다.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(t.schema_id) AS schema_name  
    ,t.name AS table_name  
FROM sys.tables t   
WHERE object_id NOT IN   
   (  
    SELECT parent_object_id   
    FROM sys.key_constraints   
    WHERE type_desc = 'PRIMARY_KEY_CONSTRAINT' -- or type = 'PK'  
    );  
GO  
  
```  
  
 또는 다음 쿼리를 실행할 수 있습니다.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    ,name AS table_name   
FROM sys.tables   
WHERE OBJECTPROPERTY(object_id,'TableHasPrimaryKey') = 0  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ4"></a> 인덱스에 있지 않은 모든 테이블 찾기  
 다음 쿼리를 실행하기 전에 `<database_name>`을 올바른 데이터베이스 이름으로 대체합니다.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    ,name AS table_name  
FROM sys.tables   
WHERE OBJECTPROPERTY(object_id,'IsIndexed') = 0  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ5"></a> Id 열이 있는 모든 테이블 찾기  
 다음 쿼리를 실행하기 전에 `<database_name>`을 올바른 데이터베이스 이름으로 대체합니다.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    , t.name AS table_name  
    , c.name AS column_name  
FROM sys.tables AS t  
JOIN sys.identity_columns c ON t.object_id = c.object_id  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
 또는 다음 쿼리를 실행할 수 있습니다.  
  
> [!NOTE]  
>  이 쿼리는 열 이름을 반환하지 않습니다.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    ,name AS table_name   
FROM sys.tables   
WHERE OBJECTPROPERTY(object_id,'TableHasIdentity') = 1  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ7"></a> 지정된 된 테이블의 열 데이터 형식을 찾으려면 어떻게 해야 합니까?  
 다음 쿼리를 실행하기 전에 `<database_name>` 및 `<schema_name.table_name>`을 올바른 이름으로 대체합니다.  
  
```  
USE <database_name>;  
GO  
SELECT c.name AS column_name  
    ,c.column_id  
    ,SCHEMA_NAME(t.schema_id) AS type_schema  
    ,t.name AS type_name  
    ,t.is_user_defined  
    ,t.is_assembly_type  
    ,c.max_length  
    ,c.precision  
    ,c.scale  
FROM sys.columns AS c   
JOIN sys.types AS t ON c.user_type_id=t.user_type_id  
WHERE c.object_id = OBJECT_ID('<schema_name.table_name>')  
ORDER BY c.column_id;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ8"></a> 지정된 된 함수에서 종속성을 찾으려면 어떻게 해야 합니까?  
 다음 쿼리를 실행하기 전에 `<database_name>` 및 `<schema_name.function_name>`을 올바른 이름으로 대체합니다.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS referencing_object_name  
    ,COALESCE(COL_NAME(object_id, column_id), '(n/a)') AS referencing_column_name  
    ,*  
FROM sys.sql_dependencies  
WHERE referenced_major_id = OBJECT_ID('<schema_name.function_name>')  
ORDER BY OBJECT_NAME(object_id), COL_NAME(object_id, column_id);  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ9"></a> 데이터베이스에서 저장된 프로시저를 모두 찾으려면 어떻게 해야 합니까?  
 다음 쿼리를 실행하기 전에 `<database_name>`을 올바른 이름으로 대체합니다.  
  
```  
  
USE <database_name>;  
GO  
SELECT name AS procedure_name   
    ,SCHEMA_NAME(schema_id) AS schema_name  
    ,type_desc  
    ,create_date  
    ,modify_date  
FROM sys.procedures;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ10"></a> 지정한 저장 프로시저나 함수에 대 한 매개 변수를 찾으려면 어떻게 해야 합니까?  
 다음 쿼리를 실행하기 전에 `<database_name>` 및 `<schema_name.object_name>`을 올바른 이름으로 대체합니다.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    ,o.name AS object_name  
    ,o.type_desc  
    ,p.parameter_id  
    ,p.name AS parameter_name  
    ,TYPE_NAME(p.user_type_id) AS parameter_type  
    ,p.max_length  
    ,p.precision  
    ,p.scale  
    ,p.is_output  
FROM sys.objects AS o  
INNER JOIN sys.parameters AS p ON o.object_id = p.object_id  
WHERE o.object_id = OBJECT_ID('<schema_name.object_name>')  
ORDER BY schema_name, object_name, p.parameter_id;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ12"></a> 데이터베이스의 모든 사용자 정의 함수를 찾으려면 어떻게 해야 합니까?  
 다음 쿼리를 실행하기 전에 `<database_name>`을 올바른 데이터베이스 이름으로 대체합니다.  
  
```  
USE <database_name>;  
GO  
SELECT name AS function_name   
  ,SCHEMA_NAME(schema_id) AS schema_name  
  ,type_desc  
  ,create_date  
  ,modify_date  
FROM sys.objects  
WHERE type_desc LIKE '%FUNCTION%';  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ13"></a> 데이터베이스의 모든 뷰 찾기  
 다음 쿼리를 실행하기 전에 `<database_name>`을 올바른 데이터베이스 이름으로 대체합니다.  
  
```  
USE <database_name>;  
GO  
SELECT name AS view_name   
  ,SCHEMA_NAME(schema_id) AS schema_name  
  ,OBJECTPROPERTYEX(object_id,'IsIndexed') AS IsIndexed  
  ,OBJECTPROPERTYEX(object_id,'IsIndexable') AS IsIndexable  
  ,create_date  
  ,modify_date  
FROM sys.views;  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ6"></a> 최근 N 일 동안에서 수정 된 모든 엔터티를 찾으려면 어떻게 해야 합니까?  
 다음 쿼리를 실행하기 전에 `<database_name>` 및 `<n_days>`를 올바른 값으로 대체합니다.  
  
```  
USE <database_name>;  
GO  
SELECT name AS object_name   
  ,SCHEMA_NAME(schema_id) AS schema_name  
  ,type_desc  
  ,create_date  
  ,modify_date  
FROM sys.objects  
WHERE modify_date > GETDATE() - <n_days>  
ORDER BY modify_date;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ14"></a> 지정된 된 테이블의 LOB 데이터 형식을 찾으려면 어떻게 해야 합니까?  
 다음 쿼리를 실행하기 전에 `<database_name>` 및 `<schema_name.table_name>`을 올바른 이름으로 대체합니다.  
  
```  
  
USE <database_name>;  
GO  
SELECT name AS column_name   
    ,column_id   
    ,TYPE_NAME(user_type_id) AS type_name  
    ,max_length  
    ,CASE   
       WHEN max_length = -1 AND TYPE_NAME(user_type_id) <> 'xml'  
            THEN 1  
            ELSE 0  
     END AS [(max)]  
FROM sys.columns  
WHERE object_id=OBJECT_ID('<schema_name.table_name>')   
    AND ( TYPE_NAME(user_type_id) IN ('xml','text', 'ntext','image')  
         OR (TYPE_NAME(user_type_id) IN ('varchar','nvarchar','varbinary')  
         AND max_length = -1)  
        );  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ15"></a> 모듈의 정의 보는 방법  
 다음 쿼리를 실행하기 전에 `<database_name>` 및 `<schema_name.object_name>`을 올바른 이름으로 대체합니다.  
  
```  
USE <database_name>;  
GO  
SELECT definition  
FROM sys.sql_modules  
WHERE object_id = OBJECT_ID('<schema_name.object_name>');  
GO  
  
```  
  
 또는 다음 예와 같이 `OBJECT_DEFINITION` 함수를 사용할 수 있습니다.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_DEFINITION (OBJECT_ID('<schema_name.object_name>')) AS ObjectDefinition;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ19"></a> 서버 수준 트리거의 정의 보는 방법  
  
```  
SELECT definition  
FROM sys.server_sql_modules;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ16"></a> 지정된 된 테이블에 대 한 기본 키의 열을 찾으려면 어떻게 해야 합니까?  
 다음 쿼리를 실행하기 전에 `<database_name>` 및 `<schema_name.table_name>`을 올바른 이름으로 대체합니다.  
  
```  
USE <database_name>;  
GO  
SELECT i.name AS index_name  
    ,ic.index_column_id  
    ,key_ordinal  
    ,c.name AS column_name  
    ,TYPE_NAME(c.user_type_id)AS column_type   
    ,is_identity  
FROM sys.indexes AS i  
INNER JOIN sys.index_columns AS ic   
    ON i.object_id = ic.object_id AND i.index_id = ic.index_id  
INNER JOIN sys.columns AS c   
    ON ic.object_id = c.object_id AND c.column_id = ic.column_id  
WHERE i.is_primary_key = 1   
    AND i.object_id = OBJECT_ID('<schema_name.table_name>');  
GO  
  
```  
  
 또는 다음 예와 같이 `COL_NAME` 함수를 사용할 수 있습니다.  
  
```  
USE <database_name>;  
GO  
SELECT i.name AS index_name  
    ,COL_NAME(ic.object_id,ic.column_id) AS column_name  
    ,ic.index_column_id  
    ,key_ordinal  
FROM sys.indexes AS i  
INNER JOIN sys.index_columns AS ic   
    ON i.object_id = ic.object_id AND i.index_id = ic.index_id  
WHERE i.is_primary_key = 1   
    AND i.object_id = OBJECT_ID('<schema_name.table_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ17"></a> 지정된 된 테이블에 대 한 외래 키의 열을 찾으려면 어떻게 해야 합니까?  
 다음 쿼리를 실행하기 전에 `<database_name>` 및 `<schema_name.table_name>`을 올바른 이름으로 대체합니다.  
  
```  
USE <database_name>;  
GO  
SELECT   
    f.name AS foreign_key_name  
   ,OBJECT_NAME(f.parent_object_id) AS table_name  
   ,COL_NAME(fc.parent_object_id, fc.parent_column_id) AS constraint_column_name  
   ,OBJECT_NAME (f.referenced_object_id) AS referenced_object  
   ,COL_NAME(fc.referenced_object_id, fc.referenced_column_id) AS referenced_column_name  
   ,is_disabled  
   ,delete_referential_action_desc  
   ,update_referential_action_desc  
FROM sys.foreign_keys AS f  
INNER JOIN sys.foreign_key_columns AS fc   
   ON f.object_id = fc.constraint_object_id   
WHERE f.parent_object_id = OBJECT_ID('<schema_name.table_name>');  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ18"></a> 지정한 보안 주체에 허용 또는 거부 권한을 찾으려면 어떻게 해야 합니까?  
 다음 예에서는 사용 권한이 확인되는 엔터티의 이름을 반환하는 함수를 만듭니다. 이 함수는 뒷부분에 나오는 쿼리에서 호출됩니다. 사용 권한을 확인할 모든 데이터베이스에서 함수를 만들어야 합니다.  
  
```  
-- Create a function to return the name of the entity on which the permissions are checked.  
IF OBJECT_ID (N'dbo.entity_instance_name', N'FN') IS NOT NULL  
    DROP FUNCTION dbo.entity_instance_name;  
GO  
CREATE FUNCTION dbo.entity_instance_name(@class_desc nvarchar(60), @major_id int)   
RETURNS sysname AS  
BEGIN  
    DECLARE @the_entity_name sysname  
    SELECT @the_entity_name = CASE  
        WHEN @class_desc = 'DATABASE' THEN DB_NAME()  
        WHEN @class_desc = 'SCHEMA' THEN SCHEMA_NAME(@major_id)  
        WHEN @class_desc = 'OBJECT_OR_COLUMN' THEN OBJECT_NAME(@major_id)  
        WHEN @class_desc = 'DATABASE_PRINCIPAL' THEN USER_NAME(@major_id)  
        WHEN @class_desc = 'ASSEMBLY' THEN   
            (SELECT name FROM sys.assemblies WHERE assembly_id=@major_id)  
        WHEN @class_desc = 'TYPE' THEN TYPE_NAME(@major_id)  
        WHEN @class_desc = 'XML_SCHEMA_COLLECTION' THEN   
            (SELECT name FROM sys.xml_schema_collections  
              WHERE xml_collection_id=@major_id)  
        WHEN @class_desc = 'MESSAGE_TYPE' THEN   
            (SELECT name FROM sys.service_message_types WHERE message_type_id=@major_id)  
        WHEN @class_desc = 'SERVICE_CONTRACT' THEN   
           (SELECT name FROM sys.service_contracts  
              WHERE service_contract_id=@major_id)  
        WHEN @class_desc = 'SERVICE' THEN  
          (SELECT name FROM sys.services WHERE service_id=@major_id)  
        WHEN @class_desc = 'REMOTE_SERVICE_BINDING' THEN  
          (SELECT name FROM sys.remote_service_bindings  
             WHERE remote_service_binding_id=@major_id)  
        WHEN @class_desc = 'ROUTE' THEN  
          (SELECT name FROM sys.routes WHERE route_id=@major_id)  
        WHEN @class_desc = 'FULLTEXT_CATALOG' THEN  
          (SELECT name FROM sys.fulltext_catalogs WHERE fulltext_catalog_id=@major_id)  
        WHEN @class_desc = 'SYMMETRIC_KEY' THEN  
          (SELECT name FROM sys.symmetric_keys WHERE symmetric_key_id=@major_id)  
        WHEN @class_desc = 'CERTIFICATE' THEN  
          (SELECT name FROM sys.certificates WHERE certificate_id=@major_id)  
        WHEN @class_desc = 'ASYMMETRIC_KEY' THEN  
          (SELECT name FROM sys.asymmetric_keys WHERE asymmetric_key_id=@major_id)  
        WHEN @class_desc = 'SERVER' THEN   
             (SELECT name FROM sys.servers WHERE server_id=@major_id)  
        WHEN @class_desc = 'SERVER_PRINCIPAL' THEN SUSER_NAME(@major_id)  
        WHEN @class_desc = 'ENDPOINT' THEN   
             (SELECT name FROM sys.endpoints WHERE endpoint_id=@major_id)        
        ELSE '?'  
    END  
    RETURN @the_entity_name  
END;  
GO  
-- Return server-level permissions for the user.  
SELECT class  
    ,class_desc  
    ,dbo.entity_instance_name(class_desc, major_id) AS entity_name   
    ,minor_id  
    ,SUSER_NAME(grantee_principal_id) AS grantee  
    ,SUSER_NAME(grantor_principal_id) AS grantor  
    ,type  
    ,permission_name  
    ,state_desc   
FROM sys.server_permissions   
WHERE grantee_principal_id = SUSER_ID('public');  
GO  
-- Return database-level permissions for the user.  
SELECT class  
    ,class_desc  
    ,dbo.entity_instance_name(class_desc , major_id) AS entity_name   
    ,minor_id  
    ,USER_NAME(grantee_principal_id) AS grantee  
    ,USER_NAME(grantor_principal_id) AS grantor  
    ,type  
    ,permission_name  
    ,state_desc     
FROM  sys.database_permissions   
WHERE grantee_principal_id = DATABASE_PRINCIPAL_ID('public');  
GO  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ20"></a> 열이 계산된 열 식에 사용 되 면 어떻게 확인 합니까?  
 다음 쿼리를 실행 하기 전에 교체 `<database_name>`, `<schema_name.table_name>`, 및 `<column_name`>을 올바른 이름입니다.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name  
    ,COL_NAME(object_id, column_id) AS computed_column   
    ,class_desc  
    ,is_selected  
    ,is_updated  
    ,is_select_all  
FROM sys.sql_dependencies  
WHERE referenced_major_id = OBJECT_ID('<schema_name.table_name>')  
    AND referenced_minor_id = COLUMNPROPERTY(referenced_major_id, '<column_name>', 'ColumnId')  
    AND class = 1;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ21"></a> 계산된 열 식에 사용 되는 모든 열 찾으려면 어떻게 해야 합니까?  
 다음 쿼리를 실행하기 전에 `<database_name>`을 올바른 이름으로 대체합니다.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(d.referenced_major_id) AS object_name  
    ,COL_NAME(d.referenced_major_id, d.referenced_minor_id) AS column_name  
    ,OBJECT_NAME(referenced_major_id) AS dependent_object_name   
    ,COL_NAME(d.object_id, d.column_id) AS dependent_computed_column  
    ,cc.definition AS computed_column_definition  
FROM sys.sql_dependencies AS d  
JOIN sys.computed_columns AS cc   
    ON cc.object_id = d.object_id AND cc.column_id = d.column_id AND d.object_id=d.referenced_major_id       
WHERE d.class = 1  
ORDER BY object_name, column_name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ22"></a> 지정한 CLR 사용자 정의 형식 또는 별칭 형식에 종속 되는 열을 찾으려면 어떻게 해야 합니까?  
 다음 쿼리를 실행 하기 전에 교체 `<database_name>` 을 올바른 이름 및 `<schema_name.data_type_name>` 올바른 스키마 한정 CLR 사용자 정의 형식, 또는 스키마 한정 별칭 형식 이름입니다. 다음 쿼리는의 멤버 자격이 필요 합니다 **db_owner** 역할 또는 권한이 모든 종속 열 및 계산된 열을 확인 하려면 데이터베이스의 메타 데이터입니다.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name   
    ,c.name AS column_name   
    ,SCHEMA_NAME(t.schema_id) AS schema_name  
    ,TYPE_NAME(c.user_type_id) AS user_type_name  
    ,c.max_length  
    ,c.precision  
    ,c.scale  
    ,c.is_nullable  
    ,c.is_computed  
FROM sys.columns AS c  
INNER JOIN sys.types AS t ON c.user_type_id = t.user_type_id  
WHERE c.user_type_id = TYPE_ID('<schema_name.data_type_name>');   
GO  
  
```  
  
 다음 쿼리는 제한적 이며 좁은 뷰의 열을 CLR 사용자 정의 형식 또는 별칭에 종속 반환 하지만 결과 집합을 표시 합니다 **공용** 역할입니다. 사용자 정의 형식에 대한 REFERENCE 권한을 다른 사용자에게 부여했고, 다른 사용자가 만들었으며 해당 형식을 사용하는 개체에 대한 메타데이터를 볼 수 있는 권한이 없는 경우 이 쿼리를 사용할 수 있습니다.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name   
    ,COL_NAME(object_id, column_id) AS column_name  
    ,TYPE_NAME(user_type_id) AS user_type  
FROM sys.column_type_usages  
WHERE user_type_id = TYPE_ID('<schema_name.data_type_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ23"></a> 지정한 CLR 사용자 정의 형식 또는 별칭 형식에 종속 된 계산된 열 찾기  
 다음 쿼리를 실행하기 전에 `<database_name>`을 올바른 이름으로 대체하고 `<schema_name.data_type_name>`을 올바른 스키마 한정 CLR 사용자 정의 형식, 별칭 형식 이름으로 대체합니다.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name  
    ,COL_NAME(object_id, column_id) AS column_name  
FROM sys.sql_dependencies  
WHERE referenced_major_id = TYPE_ID('<schema_name.data_type_name>')  
    AND class = 2 -- schema-bound references to type  
    AND OBJECTPROPERTY(object_id, 'IsTable') = 1;   -- exclude non-table dependencies  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ24"></a> 지정한 CLR 사용자 정의 형식 또는 별칭 형식에 종속 된 매개 변수를 찾으려면 어떻게 해야 합니까?  
 다음 쿼리를 실행하기 전에 `<database_name>`을 올바른 이름으로 대체하고 `<schema_name.data_type_name>`을 올바른 스키마 한정 CLR 사용자 정의 형식, 별칭 형식 이름으로 대체합니다. 다음 쿼리는의 멤버 자격이 필요 합니다 **db_owner** 역할 또는 권한이 모든 종속 열 및 계산된 열을 확인 하려면 데이터베이스의 메타 데이터입니다.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name  
    ,NULL AS procedure_number  
    ,name AS param_name  
    ,parameter_id AS param_num  
    ,TYPE_NAME(p.user_TYPE_ID) AS type_name  
FROM sys.parameters AS p  
WHERE p.user_TYPE_ID = TYPE_ID('<schema_name.data_type_name>')  
UNION   
SELECT OBJECT_NAME(object_id) AS object_name  
    ,procedure_number  
    ,name AS param_name  
    ,parameter_id AS param_num  
    ,TYPE_NAME(p.user_TYPE_ID) AS type_name  
FROM sys.numbered_procedure_parameters AS p  
WHERE p.user_TYPE_ID = TYPE_ID('<schema_name.data_type_name>')  
ORDER BY object_name, procedure_number, param_num;  
GO  
  
```  
  
 다음 쿼리는 제한적 이며 좁은 뷰의 CLR 사용자 정의 형식 또는 별칭에 종속 된 매개 변수는 반환 되지만 결과 집합은 볼 수는 **공용** 역할입니다. 사용자 정의 형식에 대한 REFERENCE 권한을 다른 사용자에게 부여했고, 다른 사용자가 만들었으며 해당 형식을 사용하는 개체에 대한 메타데이터를 볼 수 있는 권한이 없는 경우 이 쿼리를 사용할 수 있습니다.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name  
    ,parameter_id  
    ,TYPE_NAME(user_type_id) AS type_name  
FROM sys.parameter_type_usages   
WHERE user_type_id = TYPE_ID('<schema_name.data_type_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ25"></a> 지정한 CLR 사용자 정의 형식에 종속 된 CHECK 제약 조건을 찾으려면 어떻게 해야 합니까?  
 다음 쿼리를 실행 하기 전에 교체 `<database_name>` 을 올바른 이름 및 `<schema_name.data_type_name>` 유효 하 고 스키마 한정 CLR 사용자 정의 형식 이름을 사용 하 여 합니다.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(o.schema_id) AS schema_name  
    ,OBJECT_NAME(o.parent_object_id) AS table_name  
    ,OBJECT_NAME(o.object_id) AS constraint_name  
FROM sys.sql_dependencies AS d  
JOIN sys.objects AS o ON o.object_id = d.object_id  
WHERE referenced_major_id = TYPE_ID('<schema_name.data_type_name>')  
    AND class = 2 -- schema-bound references to type  
    AND OBJECTPROPERTY(o.object_id, 'IsCheckCnst') = 1; -- exclude non-CHECK dependencies  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ26"></a> 뷰, TRANSACT-SQL 함수 및 TRANSACT-SQL 저장 프로시저는 지정한 CLR 사용자 정의 형식 또는 별칭 형식에 종속 된 찾으려면 어떻게  
 다음 쿼리를 실행하기 전에 `<database_name>`을 올바른 이름으로 대체하고 `<schema_name.data_type_name>`을 올바른 스키마 한정 CLR 사용자 정의 형식, 별칭 형식 이름으로 대체합니다.  
  
 함수 또는 프로시저에 정의된 매개 변수는 암시적으로 스키마에 바인딩됩니다. CLR 사용자 정의 형식 또는 별칭 형식에 종속 된 매개 변수를 사용 하 여 볼 수 있습니다 따라서 합니다 [sys.sql_dependencies](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md) 카탈로그 뷰. 프로시저 및 트리거는 스키마에 바인딩되지 않습니다. 즉, 프로시저 또는 트리거 본문에 정의되어 있는 모든 식과 CLR 사용자 정의 형식 또는 별칭 형식 간의 종속성이 유지되지 않습니다. 스키마 바운드 뷰 및 스키마 바운드 CLR 사용자 정의 형식에 의존 하는 식이 포함 된 사용자 정의 함수 또는 별칭 형식에 유지 되는 **sys.sql_dependencies** 카탈로그 뷰에 있습니다. 형식, CLR 함수 및 CLR 프로시저 간의 종속성은 유지되지 않습니다.  
  
 다음 쿼리는 지정한 CLR 사용자 정의 형식 또는 별칭 형식에 대한 뷰, [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수 및 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저에 있는 모든 스키마 바운드 종속성을 반환합니다.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(o.schema_id) AS dependent_object_schema  
  ,OBJECT_NAME(o.object_id) AS dependent_object_name  
  ,o.type_desc AS dependent_object_type  
  ,d.class_desc AS kind_of_dependency  
  ,TYPE_NAME (d.referenced_major_id) AS type_name  
FROM sys.sql_dependencies AS d   
JOIN sys.objects AS o  
  ON d.object_id = o.object_id  
  AND o.type IN ('FN','IF','TF', 'V', 'P')  
WHERE d.class = 2 -- dependencies on types  
  AND d.referenced_major_id = TYPE_ID('<schema_name.data_type_name>')  
ORDER BY dependent_object_schema, dependent_object_name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ27"></a> 지정된 된 테이블에 대 한 모든 제약 조건을 찾으려면 어떻게 해야 합니까?  
 다음 쿼리를 실행하기 전에 `<database_name>` 및 `<schema_name.table_name>`을 올바른 이름으로 대체합니다.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) as constraint_name  
    ,SCHEMA_NAME(schema_id) AS schema_name  
    ,OBJECT_NAME(parent_object_id) AS table_name  
    ,type_desc  
    ,create_date  
    ,modify_date  
    ,is_ms_shipped  
    ,is_published  
    ,is_schema_published  
FROM sys.objects  
WHERE type_desc LIKE '%CONSTRAINT'   
    AND parent_object_id = OBJECT_ID('<schema_name.table_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ28"></a> 지정된 된 테이블에 대 한 인덱스를 모두 찾으려면 어떻게 해야 합니까?  
 다음 쿼리를 실행하기 전에 `<database_name>` 및 `<schema_name.table_name>`을 올바른 이름으로 대체합니다.  
  
```  
USE <database_name>;  
GO  
SELECT i.name AS index_name  
    ,i.type_desc  
    ,is_unique  
    ,ds.type_desc AS filegroup_or_partition_scheme  
    ,ds.name AS filegroup_or_partition_scheme_name  
    ,ignore_dup_key  
    ,is_primary_key  
    ,is_unique_constraint  
    ,fill_factor  
    ,is_padded  
    ,is_disabled  
    ,allow_row_locks  
    ,allow_page_locks  
FROM sys.indexes AS i  
INNER JOIN sys.data_spaces AS ds ON i.data_space_id = ds.data_space_id  
WHERE is_hypothetical = 0 AND i.index_id <> 0   
AND i.object_id = OBJECT_ID('<schema_name.table_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ30"></a> 지정 된 열 이름을 가진 모든 개체를 찾으려면 어떻게 해야 합니까?  
 다음 쿼리를 실행하기 전에 `<database_name>` 및 `<column_name>`을 올바른 이름으로 대체합니다.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id)  
FROM sys.columns  
WHERE name = '<column_name>';  
GO  
  
```  
  
 또는  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(o.schema_id) AS schema_name   
    ,o.name AS object_name  
    ,type_desc  
FROM sys.objects AS o  
INNER JOIN sys.columns AS c ON o.object_id = c.object_id  
WHERE c.name = '<column_name>';  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ31"></a> 지정된 된 데이터베이스의 모든 사용자 정의 테이블 찾기  
 다음 쿼리를 실행하기 전에 `<database_name>`을 올바른 이름으로 대체합니다.  
  
```  
USE <database_name>;  
GO  
SELECT *   
FROM sys.tables;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ32"></a> 모든 테이블 및 인덱스 분할 된 찾으려면 어떻게  
 다음 쿼리를 실행하기 전에 `<database_name>`을 올바른 이름으로 대체합니다.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(o.schema_id) AS schema_name  
    ,OBJECT_NAME(p.object_id) AS table_name  
    ,i.name AS index_name  
    ,p.partition_number  
    ,rows   
FROM sys.partitions AS p  
INNER JOIN sys.indexes AS i ON p.object_id = i.object_id AND p.index_id = i.index_id  
INNER JOIN sys.partition_schemes ps ON i.data_space_id=ps.data_space_id  
INNER JOIN sys.objects AS o ON o.object_id = i.object_id  
ORDER BY index_name, partition_number;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ33"></a> 지정된 된 개체에서 통계를 찾으려면 어떻게 해야 합니까?  
 다음 쿼리를 실행하기 전에 `<database_name>`을 올바른 이름으로 대체하고 `<schema_name.object_name>`을 올바른 테이블, 인덱싱된 뷰 또는 테이블 반환 함수 이름으로 대체합니다.  
  
```  
USE <database_name>;  
GO  
SELECT name AS statistics_name  
    ,stats_id  
    ,auto_created  
    ,user_created  
    ,no_recompute  
FROM sys.stats  
WHERE object_id = OBJECT_ID('<schema_name.object_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ34"></a> 지정된 된 개체에서 통계 및 통계 열을 모두 찾으려면 수행는 어떻게  
 다음 쿼리를 실행하기 전에 `<database_name>`을 올바른 이름으로 대체하고 `<schema_name.object_name>`을 올바른 테이블, 인덱싱된 뷰 또는 테이블 반환 함수 이름으로 대체합니다.  
  
```  
USE <database_name>;  
GO  
SELECT s.name AS statistics_name  
    ,c.name AS column_name  
    ,sc.stats_column_id  
FROM sys.stats AS s  
INNER JOIN sys.stats_columns AS sc   
    ON s.object_id = sc.object_id AND s.stats_id = sc.stats_id  
INNER JOIN sys.columns AS c   
    ON sc.object_id = c.object_id AND c.column_id = sc.column_id  
WHERE s.object_id = OBJECT_ID('<schema_name.object_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ35"></a> 뷰의 정의 찾으려면 어떻게 해야 합니까?  
 다음 쿼리를 실행하기 전에 `<database_name>` 및 `<schema_name.object_name>`을 올바른 이름으로 대체합니다.  
  
```  
USE <database_name>;  
GO  
SELECT definition  
FROM sys.sql_modules  
WHERE object_id = OBJECT_ID('<schema_name.object_name>');  
GO  
  
```  
  
 또는 다음 예와 같이 `OBJECT_DEFINITION` 함수를 사용할 수 있습니다.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_DEFINITION (OBJECT_ID('<schema_name.object_name>')) AS ObjectDefinition;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
## <a name="see-also"></a>관련 항목  
 [시스템 테이블을 시스템 뷰로 매핑 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)  
  
  
