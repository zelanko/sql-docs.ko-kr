---
title: sys.sql_expression_dependencies (TRANSACT-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sql_expression_dependencies
- sql_expression_dependencies_TSQL
- sql_expression_dependencies
- sys.sql_expression_dependencies_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sql_expression_dependencies catalog view
ms.assetid: 78a218e4-bf99-4a6a-acbf-ff82425a5946
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 099229e10b875d738e970d8f2c4a0c9ac3e7b5e6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="syssqlexpressiondependencies-transact-sql"></a>sys.sql_expression_dependencies(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  현재 데이터베이스에서 사용자 정의 엔터티의 이름별 종속성마다 한 개의 행을 포함합니다. 여기에 코드 및 기타 고유 하 게 컴파일된 스칼라 사용자 정의 함수 간 종속성 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 모듈입니다. 한 엔터티의 호출 될 때 두 엔터티 간의 종속성 만들어집니다는 *엔터티를 참조*, 라는 다른 엔터티의 영구 SQL 식에 이름별으로 나타나는 *참조 엔터티*합니다. 예를 들어 뷰 정의에서 테이블을 참조하면 참조 엔터티인 뷰는 참조된 엔터티인 테이블에 종속됩니다. 테이블이 삭제되면 뷰를 사용할 수 없습니다.  
  
 자세한 내용은 참조 [메모리 내 OLTP에 대 한 사용자 정의 스칼라 함수](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)합니다.  
  
 이 카탈로그 뷰를 사용하여 다음 엔터티에 대한 종속성 정보를 보고할 수 있습니다.  
  
-   스키마 바운드 엔터티  
  
-   비스키마 바운드 엔터티  
  
-   데이터베이스 간 및 서버 간 엔터티. 엔터티 이름이 보고되지만 엔터티 ID는 확인되지 않습니다.  
  
-   스키마 바운드 엔터티에 대한 열 수준 종속성. 비 스키마 바운드 개체에 대 한 열 수준 종속성을 사용 하 여 반환 될 수 [sys.dm_sql_referenced_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)합니다.  
  
-   master 데이터베이스의 컨텍스트에서 서버 수준 DLL 트리거  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|referencing_id|**int**|참조 엔터티의 ID입니다. Null을 허용하지 않습니다.|  
|referencing_minor_id|**int**|참조 엔터티가 열인 경우 열 ID이며 그렇지 않은 경우 0입니다. Null을 허용하지 않습니다.|  
|referencing_class|**tinyint**|참조 엔터티의 클래스입니다.<br /><br /> 1 = 개체 또는 열<br /><br /> 12 = 데이터베이스 DDL 트리거<br /><br /> 13 = 서버 DDL 트리거<br /><br /> Null을 허용하지 않습니다.|  
|referencing_class_desc|**nvarchar (60)**|참조 엔터티 클래스에 대한 설명입니다.<br /><br /> OBJECT_OR_COLUMN<br /><br /> DATABASE_DDL_TRIGGER<br /><br /> SERVER_DDL_TRIGGER<br /><br /> Null을 허용하지 않습니다.|  
|is_schema_bound_reference|**bit**|1 = 참조된 엔터티가 스키마 바운드입니다.<br /><br /> 0 = 참조된 엔터티가 비스키마 바운드입니다.<br /><br /> Null을 허용하지 않습니다.|  
|referenced_class|**tinyint**|참조된 엔터티의 클래스입니다.<br /><br /> 1 = 개체 또는 열<br /><br /> 6 = 형식<br /><br /> 10 = XML 스키마 컬렉션<br /><br /> 21 = 파티션 함수<br /><br /> Null을 허용하지 않습니다.|  
|referenced_class_desc|**nvarchar (60)**|참조된 엔터티의 클래스에 대한 설명입니다.<br /><br /> OBJECT_OR_COLUMN<br /><br /> TYPE<br /><br /> XML_SCHEMA_COLLECTION<br /><br /> PARTITION_FUNCTION<br /><br /> Null을 허용하지 않습니다.|  
|referenced_server_name|**sysname**|참조된 엔터티의 서버 이름입니다.<br /><br /> 이 열은 네 부분으로 된 올바른 이름을 지정하여 생성되는 서버 간 종속성에 대해 채워집니다. 다중 부분 이름에 대 한 정보를 참조 하십시오. [TRANSACT-SQL 구문 표기 규칙 &#40; Transact SQL &#41; ](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).<br /><br /> 네 부분 이름을 지정하지 않고 엔터티가 참조되는 비스키마 바운드 엔터티의 경우 NULL입니다.<br /><br /> 동일한 데이터베이스에 있어야 하며 따라서만 정의 될 수는 두 부분을 사용 하 여 있기 때문에 스키마 바운드 엔터티에 대 한 NULL (*schema.object*) 이름입니다.|  
|referenced_database_name|**sysname**|참조된 엔터티의 데이터베이스 이름입니다.<br /><br /> 이 열은 세 부분 또는 네 부분으로 된 올바른 이름을 지정하여 생성되는 데이터베이스 간 또는 서버 간 참조에 대해 채워집니다.<br /><br /> 한 부분 또는 두 부분으로 된 이름을 사용하여 지정된 비스키마 바운드 참조의 경우 NULL입니다.<br /><br /> 동일한 데이터베이스에 있어야 하며 따라서만 정의 될 수는 두 부분을 사용 하 여 있기 때문에 스키마 바운드 엔터티에 대 한 NULL (*schema.object*) 이름입니다.|  
|referenced_schema_name|**sysname**|참조된 엔터티가 속한 스키마입니다.<br /><br /> 스키마 이름 지정 없이 엔터티가 참조되는 비스키마 바운드 참조의 경우 NULL입니다.<br /><br /> 스키마 바운드 엔터티는 두 부분 이름을 사용하여 정의 및 참조되어야 하므로 스키마 바운드 참조의 경우 NULL이 될 수 없습니다.|  
|referenced_entity_name|**sysname**|참조된 엔터티의 이름입니다. Null을 허용하지 않습니다.|  
|referenced_id|**int**|참조된 엔터티의 ID입니다. 이 열의 값은 스키마 바운드 참조에 대 한 NULL입니다. 이 열의 값은 항상 서버 간 및 데이터베이스 간 참조에 대해 NULL입니다.<br /><br /> 데이터베이스 내 참조의 경우 ID를 확인할 수 없으면 NULL입니다. 비스키마 바운드 참조는 다음과 같은 경우 ID를 확인할 수 없습니다.<br /><br /> 참조된 엔터티가 데이터베이스에 없는 경우<br /><br /> 호출자 스키마에 종속되는 참조된 엔터티의 스키마이며 런타임에 확인됩니다. 이 경우 is_caller_dependent는 1로 설정됩니다.|  
|referenced_minor_id|**int**|참조 엔터티가 열인 경우 참조된 열의 ID이며 그렇지 않은 경우 0입니다. Null을 허용하지 않습니다.<br /><br /> 열이 참조 엔터티에서 이름으로 식별되거나 부모 엔터티가 SELECT * 문에 사용된 경우 참조된 엔터티는 열입니다.|  
|is_caller_dependent|**bit**|참조된 엔터티에 대한 스키마 바인딩이 런타임에 발생하므로 엔터티 ID 확인이 호출자의 스키마에 종속됨을 나타냅니다. 이는 참조된 엔터티가 저장 프로시저, 확장 저장 프로시저, 또는 EXECUTE 문에서 호출되는 비스키마 바운드 사용자 정의 함수인 경우에 발생합니다.<br /><br /> 1 = 참조된 엔터티가 호출자에 종속되고 런타임에 확인됩니다. 이 경우 referenced_id는 NULL입니다.<br /><br /> 0 = 참조된 엔터티 ID가 호출자에 종속되지 않습니다.<br /><br /> 스키마 이름을 명시적으로 지정하는 스키마 바운드 참조와 데이터베이스 간 및 서버 간 참조의 경우 항상 0입니다. 예를 들어 `EXEC MyDatabase.MySchema.MyProc` 형식의 엔터티에 대한 참조는 호출자에 종속되지 않습니다. 하지만 `EXEC MyDatabase..MyProc` 형식의 참조는 호출자에 종속됩니다.|  
|is_ambiguous|**bit**|대 한 참조가 모호 하며 런타임에 사용자 정의 함수, 사용자 정의 형식 (UDT) 또는 형식의 열에 대 한 xquery 참조로 확인할 수 나타냅니다 **xml**합니다.<br /><br /> 예를 들어 `SELECT Sales.GetOrder() FROM Sales.MySales` 문이 저장 프로시저에 정의되어 있다고 가정해 보겠습니다. `Sales.GetOrder()`가 `Sales` 스키마의 사용자 정의 함수인지, 아니면 `Sales`라는 메서드가 있는 UDT 형식의 `GetOrder()` 열인지는 저장 프로시저가 실행될 때까지 알 수 없습니다.<br /><br /> 1 = 참조가 모호합니다.<br /><br /> 0 = 참조가 명확하거나 뷰를 호출할 때 엔터티를 바인딩할 수 있습니다.<br /><br /> 스키마 바운드 참조의 경우 항상 0입니다.|  
  
## <a name="remarks"></a>주의  
 다음 표에서는 종속성 정보가 생성 및 유지되는 엔터티 유형을 보여 줍니다. 종속성 정보는 규칙, 기본값, 임시 테이블, 임시 저장 프로시저 또는 시스템 개체에 대해서는 생성 및 유지되지 않습니다.  
  
|엔터티 유형|참조 엔터티|참조된 엔터티|  
|-----------------|------------------------|-----------------------|  
|테이블|예*|예|  
|보기|예|예|  
|필터링된 인덱스|예**|아니요|  
|필터링된 통계|예**|아니요|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저***|예|예|  
|CLR 저장 프로시저|아니요|예|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] 사용자 정의 함수|예|예|  
|CLR 사용자 정의 함수|아니요|예|  
|CLR 트리거(DML 및 DDL)|아니요|아니요|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] DML 트리거|예|아니요|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] 데이터베이스 수준 DDL 트리거|예|아니요|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] 서버 수준 DDL 트리거|예|아니요|  
|확장 저장 프로시저|아니요|예|  
|큐|아니요|예|  
|동의어|아니요|예|  
|형식(별칭 및 CLR 사용자 정의 형식)|아니요|예|  
|XML 스키마 컬렉션|아니요|예|  
|파티션 함수|아니요|예|  
  
 \*한 테이블에서 참조 하는 경우에 참조 엔터티로 추적 하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 모듈, 사용자 정의 형식 또는 계산된 열, CHECK 제약 조건 또는 DEFAULT 제약 조건 정의에서 XML 스키마 컬렉션입니다.  
  
 ** 필터 조건자에 사용된 각 열은 참조 엔터티로 추적됩니다.  
  
 *** 1보다 큰 정수 값의 번호가 부여된 저장 프로시저는 참조 엔터티나 참조된 엔터티로 추적되지 않습니다.  
  
## <a name="permissions"></a>Permissions  
 데이터베이스에 대한 VIEW DEFINITION 권한과 데이터베이스의 sys.sql_expression_dependencies에 대한 SELECT 권한이 필요합니다. 기본적으로 SELECT 권한은 db_owner 고정 데이터베이스 역할의 멤버에게만 부여됩니다. SELECT와 VIEW DEFINITION 권한을 다른 사용자에게 부여하면 피부여자는 데이터베이스의 모든 종속성을 볼 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-returning-entities-that-are-referenced-by-another-entity"></a>1. 다른 엔터티에서 참조한 엔터티 반환  
 다음 예는 `Production.vProductAndDescription` 뷰에서 참조되는 테이블과 열을 반환합니다. 이 뷰는 `referenced_entity_name` 및 `referenced_column_name` 열에 반환된 엔터티(테이블 및 열)에 종속됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT OBJECT_NAME(referencing_id) AS referencing_entity_name,   
    o.type_desc AS referencing_desciption,   
    COALESCE(COL_NAME(referencing_id, referencing_minor_id), '(n/a)') AS referencing_minor_id,   
    referencing_class_desc,  
    referenced_server_name, referenced_database_name, referenced_schema_name,  
    referenced_entity_name,   
    COALESCE(COL_NAME(referenced_id, referenced_minor_id), '(n/a)') AS referenced_column_name,  
    is_caller_dependent, is_ambiguous  
FROM sys.sql_expression_dependencies AS sed  
INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
WHERE referencing_id = OBJECT_ID(N'Production.vProductAndDescription');  
GO  
  
```  
  
### <a name="b-returning-entities-that-reference-another-entity"></a>2. 다른 엔터티를 참조하는 엔터티 반환  
 다음 예는 `Production.Product` 테이블을 참조하는 엔터티를 반환합니다. `referencing_entity_name` 열에 반환된 엔터티는 `Product` 테이블에 종속됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT OBJECT_SCHEMA_NAME ( referencing_id ) AS referencing_schema_name,  
    OBJECT_NAME(referencing_id) AS referencing_entity_name,   
    o.type_desc AS referencing_desciption,   
    COALESCE(COL_NAME(referencing_id, referencing_minor_id), '(n/a)') AS referencing_minor_id,   
    referencing_class_desc, referenced_class_desc,  
    referenced_server_name, referenced_database_name, referenced_schema_name,  
    referenced_entity_name,   
    COALESCE(COL_NAME(referenced_id, referenced_minor_id), '(n/a)') AS referenced_column_name,  
    is_caller_dependent, is_ambiguous  
FROM sys.sql_expression_dependencies AS sed  
INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
WHERE referenced_id = OBJECT_ID(N'Production.Product');  
GO  
  
```  
  
### <a name="c-returning-cross-database-dependencies"></a>3. 데이터베이스 간 종속성 반환  
 다음 예에서는 모든 데이터베이스 간 종속성을 반환합니다. 예에서는 먼저 `db1` 데이터베이스를 만들고 `db2` 및 `db3` 데이터베이스의 테이블을 참조하는 두 개의 저장 프로시저를 만듭니다. 그런 다음 `sys.sql_expression_dependencies` 테이블을 쿼리하여 프로시저와 테이블 사이의 데이터베이스 간 종속성을 보고합니다. 참조된 엔터티 `referenced_schema_name`에 대한 스키마 이름이 프로시저 정의에 지정되지 않았으므로 해당 엔터티에 대한 `t3` 열에서 NULL이 반환됩니다.  
  
```  
CREATE DATABASE db1;  
GO  
USE db1;  
GO  
CREATE PROCEDURE p1 AS SELECT * FROM db2.s1.t1;  
GO  
CREATE PROCEDURE p2 AS  
    UPDATE db3..t3  
    SET c1 = c1 + 1;  
GO  
SELECT OBJECT_NAME (referencing_id),referenced_database_name,   
    referenced_schema_name, referenced_entity_name  
FROM sys.sql_expression_dependencies  
WHERE referenced_database_name IS NOT NULL;  
GO  
USE master;  
GO  
DROP DATABASE db1;  
GO  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sys.dm_sql_referenced_entities&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.dm_sql_referencing_entities&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)  
  
  
