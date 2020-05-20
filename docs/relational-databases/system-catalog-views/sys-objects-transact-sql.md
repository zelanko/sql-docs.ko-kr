---
title: sys. objects (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 05/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.objects_TSQL
- objects
- sys.objects
- objects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.objects catalog view
- table-valued parameters, sys.objects catalog view
- user-defined table types [SQL Server]
- table types [SQL Server]
ms.assetid: f8d6163a-2474-410c-a794-997639f31b3b
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0673c55c64c623bd112cbf63c50bc803764ce04c
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82825033"
---
# <a name="sysobjects-transact-sql"></a>sys.objects(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  고유 하 게 컴파일된 스칼라 사용자 정의 함수를 포함 하 여 데이터베이스 내에서 생성 되는 각 사용자 정의 스키마 범위 개체에 대 한 행을 포함 합니다.  
  
 자세한 내용은 [메모리 내 OLTP에 대한 사용자 정의 스칼라 함수](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)를 참조하세요.  
  
> [!NOTE]  
>  sys.objects는 스키마 범위가 아니기 때문에 DDL 트리거를 표시하지 않습니다. 모든 트리거 (DML 및 DDL)는 모두 [sys. 트리거에](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)있습니다. sys.triggers는 다양한 종류의 트리거에 대한 이름-범위 혼합 규칙을 지원합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|name|**sysname**|개체 이름입니다.|  
|object_id|**int**|개체 ID입니다. 데이터베이스 내에서 고유합니다.|  
|principal_id|**int**|스키마 소유자와 다른 경우 개별 소유자의 ID입니다. 기본적으로 스키마에 포함된 개체는 스키마 소유자가 소유합니다. 그러나 ALTER AUTHORIZATION 문으로 대체 소유자를 지정하여 소유권을 변경할 수 있습니다.<br /><br /> 대체 개별 소유자가 없으면 NULL입니다.<br /><br /> 개체 형식이 다음 중 하나인 경우 NULL입니다.<br /><br /> C = CHECK 제약 조건<br /><br /> D = DEFAULT(제약 조건 또는 독립 실행형)<br /><br /> F = FOREIGN KEY 제약 조건<br /><br /> PK = PRIMARY KEY 제약 조건<br /><br /> R = 규칙 (이전 스타일, 독립 실행형)<br /><br /> TA = 어셈블리(CLR 통합) 트리거<br /><br /> TR = SQL 트리거<br /><br /> UQ = UNIQUE 제약 조건<br /><br /> EC =에 지 제약 조건 |  
|schema_id|**int**|개체가 포함된 스키마의 ID입니다.<br /><br /> 스키마 범위 시스템 개체는 항상 sys 또는 INFORMATION_SCHEMA 스키마에 포함됩니다.|  
|parent_object_id|**int**|이 개체가 속하는 개체의 ID입니다.<br /><br /> 0 = 자식 개체가 아닙니다.|  
|형식|**char(2)**|개체 유형:<br /><br /> AF = 집계 함수(CLR)<br /><br /> C = CHECK 제약 조건<br /><br /> D = DEFAULT(제약 조건 또는 독립 실행형)<br /><br /> F = FOREIGN KEY 제약 조건<br /><br /> FN = SQL 스칼라 함수<br /><br /> FS = 어셈블리(CLR) 스칼라 함수<br /><br /> FT = 어셈블리(CLR) 테이블 반환 함수<br /><br /> IF = SQL 인라인 테이블 반환 함수<br /><br /> IT = 내부 테이블<br /><br /> P = SQL 저장 프로시저<br /><br /> PC = 어셈블리(CLR) 저장 프로시저<br /><br /> PG = 계획 지침<br /><br /> PK = PRIMARY KEY 제약 조건<br /><br /> R = 규칙 (이전 스타일, 독립 실행형)<br /><br /> RF = 복제 필터 프로시저<br /><br /> S = 시스템 기본 테이블<br /><br /> SN = 동의어<br /><br /> SO = 시퀀스 개체<br /><br /> U = 테이블(사용자 정의)<br /><br /> V = 뷰<br /><br /> EC =에 지 제약 조건 <br /><br /> <br /><br /> **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상<br /><br /> <br /><br /> SQ = 서비스 큐<br /><br /> TA = 어셈블리(CLR) DML 트리거<br /><br /> TF = SQL 테이블 반환 함수<br /><br /> TR = SQL DML 트리거<br /><br /> TT = 테이블 유형<br /><br /> UQ = UNIQUE 제약 조건<br /><br /> X = 확장 저장 프로시저<br /><br /> <br /><br /> **적용**대상: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상,, [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] , [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> <br /><br /> ET = 외부 테이블|  
|type_desc|**nvarchar(60)**|개체 유형에 대한 설명:<br /><br /> AGGREGATE_FUNCTION<br /><br /> CHECK_CONSTRAINT<br /><br /> CLR_SCALAR_FUNCTION<br /><br /> CLR_STORED_PROCEDURE<br /><br /> CLR_TABLE_VALUED_FUNCTION<br /><br /> CLR_TRIGGER<br /><br /> DEFAULT_CONSTRAINT<br /><br /> EXTENDED_STORED_PROCEDURE<br /><br /> FOREIGN_KEY_CONSTRAINT<br /><br /> INTERNAL_TABLE<br /><br /> PLAN_GUIDE<br /><br /> PRIMARY_KEY_CONSTRAINT<br /><br /> REPLICATION_FILTER_PROCEDURE<br /><br /> RULE<br /><br /> SEQUENCE_OBJECT<br /><br /> <br /><br /> **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상<br /><br /> <br /><br /> SERVICE_QUEUE<br /><br /> SQL_INLINE_TABLE_VALUED_FUNCTION<br /><br /> SQL_SCALAR_FUNCTION<br /><br /> SQL_STORED_PROCEDURE<br /><br /> SQL_TABLE_VALUED_FUNCTION<br /><br /> SQL_TRIGGER<br /><br /> SYNONYM<br /><br /> SYSTEM_TABLE<br /><br /> TABLE_TYPE<br /><br /> UNIQUE_CONSTRAINT<br /><br /> USER_TABLE<br /><br /> VIEW|  
|create_date|**datetime**|개체를 만든 날짜입니다.|  
|modify_date|**datetime**|ALTER 문을 사용하여 개체를 마지막으로 수정한 날짜입니다. 개체가 테이블이나 뷰인 경우 테이블이나 뷰에서 클러스터형 인덱스가 생성되거나 변경되면 modify_date도 변경됩니다.|  
|is_ms_shipped|**bit**|개체가 내부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소로 만들어집니다.|  
|is_published|**bit**|개체가 게시됩니다.|  
|is_schema_published|**bit**|개체의 스키마만 게시됩니다.|  
  
## <a name="remarks"></a>설명  
 [OBJECT_ID](../../t-sql/functions/object-id-transact-sql.md), [OBJECT_NAME](../../t-sql/functions/object-name-transact-sql.md)및 [objectproperty](../../t-sql/functions/objectproperty-transact-sql.md)() 기본 제공 함수를 sys. 개체에 표시 된 개체에 적용할 수 있습니다.  
  
 시스템 개체를 표시 하는 동일한 스키마 ( [system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md))가 있는이 뷰의 버전이 있습니다. 시스템 개체와 사용자 개체를 모두 표시 하는 [all_objects](../../relational-databases/system-catalog-views/sys-all-objects-transact-sql.md) 라는 다른 뷰가 있습니다. 세 카탈로그 뷰 모두 구조가 같습니다.  
  
 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서는 XML 인덱스 또는 공간 인덱스와 같은 확장 인덱스를 sys.objects(type = IT 및 type_desc = INTERNAL_TABLE)의 내부 테이블로 간주합니다. 확장 인덱스에 대한 설명은 다음과 같습니다.  
  
-   name은 인덱스 테이블의 내부 이름입니다.  
  
-   parent_object_id는 기본 테이블의 object_id입니다.  
  
-   is_ms_shipped, is_published 및 is_schema_published 열은 0으로 설정됩니다.  

**관련 된 유용한 시스템 뷰**  
개체의 하위 집합은 다음과 같은 특정 개체 형식에 대 한 시스템 뷰를 사용 하 여 볼 수 있습니다.  
- [sys.tables](sys-tables-transact-sql.md)  
- [sys.views](sys-views-transact-sql.md)  
- [sys.procedures](sys-procedures-transact-sql.md)  
  
## <a name="permissions"></a>권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-returning-all-the-objects-that-have-been-modified-in-the-last-n-days"></a>A. 최근 N일 동안 수정된 모든 개체 반환  
 다음 쿼리를 실행하기 전에 `<database_name>` 및 `<n_days>`를 올바른 값으로 대체합니다.  
  
```sql  
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
  
### <a name="b-returning-the-parameters-for-a-specified-stored-procedure-or-function"></a>B. 지정한 저장 프로시저나 함수에 대한 매개 변수 반환  
 다음 쿼리를 실행하기 전에 `<database_name>` 및 `<schema_name.object_name>`을 올바른 이름으로 대체합니다.  
  
```sql  
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
  
### <a name="c-returning-all-the-user-defined-functions-in-a-database"></a>C. 데이터베이스의 모든 사용자 정의 함수 반환  
 다음 쿼리를 실행하기 전에 `<database_name>`을 올바른 데이터베이스 이름으로 대체합니다.  
  
```sql  
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
  
### <a name="d-returning-the-owner-of-each-object-in-a-schema"></a>D. 스키마에서 각 개체의 소유자 반환  
 다음 쿼리를 실행하기 전에 모든 `<database_name>` 및 `<schema_name>`을 올바른 이름으로 대체합니다.  
  
```sql  
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
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;카탈로그 뷰](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [all_objects &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-all-objects-transact-sql.md)   
 [system_objects &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md)   
 [sys.triggers&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)   
 [Transact-sql&#41;&#40;개체 카탈로그 뷰](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [internal_tables &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-internal-tables-transact-sql.md)  
  
  
