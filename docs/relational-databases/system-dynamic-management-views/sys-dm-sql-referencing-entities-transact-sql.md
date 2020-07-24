---
title: sys. dm_sql_referencing_entities (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_sql_referencing_entities
- dm_sql_referencing_entities_TSQL
- sys.dm_sql_referencing_entities_TSQL
- dm_sql_referencing_entities
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_sql_referencing_entities dynamic management function
ms.assetid: c16f8f0a-483f-4feb-842e-da90426045ae
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a467a445dda5f4d950c5bf4813f5ec69606df487
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86943068"
---
# <a name="sysdm_sql_referencing_entities-transact-sql"></a>sys.dm_sql_referencing_entities(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  이름별로 다른 사용자 정의 엔터티를 참조하는 현재 데이터베이스의 각 엔터티에 대해 한 개의 행을 반환합니다. 두 엔터티 간의 종속성은 *참조 된 엔터티*라고 하는 한 엔터티가 *참조 엔터티*라고 하는 다른 엔터티의 지속형 SQL 식에서 이름별로 표시 될 때 생성 됩니다. 예를 들어 UDT(사용자 정의 형식)가 참조 엔터티로 지정된 경우 이 함수는 정의에서 이름별로 해당 유형을 참조하는 각 사용자 정의 엔터티를 반환합니다. 지정된 엔터티를 참조하는 다른 데이터베이스의 엔터티는 반환하지 않습니다. 이 함수는 master 데이터베이스 컨텍스트에서 실행되어 서버 수준 DDL 트리거를 참조 엔터티로 반환해야 합니다.  
  
 이 동적 관리 함수를 사용하면 지정된 엔터티를 참조하는 현재 데이터베이스에 있는 다음과 같은 엔터티 유형을 보고할 수 있습니다.  
  
-   스키마 바운드 또는 비스키마 바운드 엔터티  
  
-   데이터베이스 수준 DDL 트리거  
  
-   서버 수준 DDL 트리거  
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]( [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sys.dm_sql_referencing_entities (  
    ' schema_name.referenced_entity_name ' , ' <referenced_class> ' )  
  
<referenced_class> ::=  
{  
    OBJECT  
  | TYPE  
  | XML_SCHEMA_COLLECTION  
  | PARTITION_FUNCTION  
}  
```  
  
## <a name="arguments"></a>인수  
 `schema_name.referenced_entity_name`참조 된 엔터티의 이름입니다.  
  
 `schema_name`은 참조된 클래스가 PARTITION_FUNCTION일 경우를 제외하고 필요합니다.  
  
 `schema_name.referenced_entity_name`는 **nvarchar (517)** 입니다.  
  
 `<referenced_class> ::= { OBJECT  | TYPE | XML_SCHEMA_COLLECTION | PARTITION_FUNCTION }`는 참조 된 엔터티의 클래스입니다. 각 문에는 하나의 클래스만 지정할 수 있습니다.  
  
 `<referenced_class>`은 **nvarchar**(60)입니다.  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|referencing_schema_name|**sysname**|참조 엔터티가 속한 스키마입니다. Null을 허용합니다.<br /><br /> 데이터베이스 수준 및 서버 수준 DDL 트리거의 경우 NULL입니다.|  
|referencing_entity_name|**sysname**|참조 엔터티의 이름입니다. Null을 허용하지 않습니다.|  
|referencing_id|**int**|참조 엔터티의 ID입니다. Null을 허용하지 않습니다.|  
|referencing_class|**tinyint**|참조 엔터티의 클래스입니다. Null을 허용하지 않습니다.<br /><br /> 1 = 개체<br /><br /> 12 = 데이터베이스 수준 DDL 트리거<br /><br /> 13 = 서버 수준 DDL 트리거|  
|referencing_class_desc|**nvarchar(60)**|참조 엔터티 클래스에 대한 설명입니다.<br /><br /> OBJECT<br /><br /> DATABASE_DDL_TRIGGER<br /><br /> SERVER_DDL_TRIGGER|  
|is_caller_dependent|**bit**|참조된 엔터티 ID 확인은 호출자의 스키마에 종속되기 때문에 런타임에 발생함을 나타냅니다.<br /><br /> 1 = 참조 엔터티는 엔터티를 참조할 수 있습니다. 그러나 참조된 엔터티 ID의 확인은 호출자에 종속되므로 확인할 수 없습니다. 이는 EXECUTE 문에서 호출되는 저장 프로시저, 확장 저장 프로시저 또는 사용자 정의 함수에 대한 비스키마 바운드 참조에서만 발생합니다.<br /><br /> 0 = 참조된 엔터티는 호출자에 종속되지 않습니다.|  
  
## <a name="exceptions"></a>예외  
 다음과 같은 경우 빈 결과 집합을 반환합니다.  
  
-   시스템 개체가 지정되어 있습니다.  
  
-   지정된 엔터티가 현재 데이터베이스에 없습니다.  
  
-   지정된 엔터티가 아무런 엔터티도 참조하지 않습니다.  
  
-   잘못된 매개 변수가 전달되었습니다.  
  
 해당 참조된 엔터티가 번호가 매겨진 저장 프로시저인 경우 오류를 반환합니다.  
  
## <a name="remarks"></a>설명  
 다음 표에서는 종속성 정보가 생성 및 유지되는 엔터티 유형을 보여 줍니다. 종속성 정보는 규칙, 기본값, 임시 테이블, 임시 저장 프로시저 또는 시스템 개체에 대해서는 생성 및 유지되지 않습니다.  
  
|엔터티 유형|참조 엔터티|참조된 엔터티|  
|-----------------|------------------------|-----------------------|  
|테이블|예*|예|  
|보기|예|예|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저**|예|예|  
|CLR 저장 프로시저|예|예|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] 사용자 정의 함수|예|예|  
|CLR 사용자 정의 함수|예|예|  
|CLR 트리거(DML 및 DDL)|아니요|아니요|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] DML 트리거|예|아니요|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] 데이터베이스 수준 DDL 트리거|예|아니요|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] 서버 수준 DDL 트리거|예|아니요|  
|확장된 저장 프로시저|아니요|예|  
|큐|아니요|예|  
|동의어|아니요|예|  
|형식(별칭 및 CLR 사용자 정의 형식)|아니요|예|  
|XML 스키마 컬렉션|아니요|예|  
|파티션 함수|아니요|예|  
  
 \*테이블은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 계산 열, CHECK 제약 조건 또는 DEFAULT 제약 조건 정의에서 모듈, 사용자 정의 형식 또는 XML 스키마 컬렉션을 참조 하는 경우에만 참조 엔터티로 추적 됩니다.  
  
 ** 정수 값 1보다 큰 번호가 있는 저장 프로시저는 참조 엔터티나 참조된 엔터티로 추적되지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
  
### <a name="sskatmai---sssql11"></a>[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] - [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   참조된 개체에 대한 CONTROL 권한이 필요합니다. 참조된 엔터티가 파티션 함수인 경우 데이터베이스에 대한 CONTROL 권한이 필요합니다.  
  
-   Dm_sql_referencing_entities에 대 한 SELECT 권한이 필요 합니다. 기본적으로 SELECT 권한은 public에 부여됩니다.  
  
### <a name="sssql14---sscurrent"></a>[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] - [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
-   참조된 개체에 대해 필요한 권한이 없습니다. 사용자가 참조 엔터티 일부에 대해서만 VIEW DEFINITION이 있는 경우 결과 일부만 반환될 수 있습니다.  
  
-   참조 엔터티가 개체인 경우 개체에 대한 VIEW DEFINITION이 필요합니다.  
  
-   참조 엔터티가 데이터베이스 수준 DDL 트리거인 경우 데이터베이스에 대한 VIEW DEFINITION이 필요합니다.  
  
-   참조 엔터티가 서버 수준 DDL 트리거인 경우 서버에 대한 VIEW ANY DEFINITION이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-returning-the-entities-that-refer-to-a-given-entity"></a>A. 지정된 엔터티를 참조하는 엔터티 반환  
 다음 예에서는 지정된 테이블을 참조하는 현재 데이터베이스의 엔터티를 반환합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT referencing_schema_name, referencing_entity_name, referencing_id, referencing_class_desc, is_caller_dependent  
FROM sys.dm_sql_referencing_entities ('Production.Product', 'OBJECT');  
GO  
```  
  
### <a name="b-returning-the-entities-that-refer-to-a-given-type"></a>B. 지정된 유형을 참조하는 엔터티 반환  
 다음 예에서는 `dbo.Flag` 별칭 유형을 참조하는 엔터티를 반환합니다. 결과 집합은 두 개의 저장 프로시저가 이 유형을 사용한다는 것을 보여 줍니다. `dbo.Flag`형식은 테이블의 여러 열에 대 한 정의에도 사용 되지만 테이블에 `HumanResources.Employee` 있는 계산 열, CHECK 제약 조건 또는 DEFAULT 제약 조건의 정의에는 없습니다. 테이블에 대해서는 행이 반환 되지 않습니다 `HumanResources.Employee` .  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT referencing_schema_name, referencing_entity_name, referencing_id, referencing_class_desc, is_caller_dependent  
FROM sys.dm_sql_referencing_entities ('dbo.Flag', 'TYPE');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 referencing_schema_name referencing_entity_name   referencing_id referencing_class_desc is_caller_dependent  
 ----------------------- -------------------------  ------------- ---------------------- -------------------  
 HumanResources          uspUpdateEmployeeHireInfo  1803153469    OBJECT_OR_COLUMN       0  
 HumanResources          uspUpdateEmployeeLogin     1819153526    OBJECT_OR_COLUMN       0  
 (2 row(s) affected)`  
 ``` 
 
## <a name="see-also"></a>참고 항목  
 [sys.dm_sql_referenced_entities&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.sql_expression_dependencies&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
  
  
