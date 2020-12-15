---
description: sys.fn_listextendedproperty(Transact-SQL)
title: sys.fn_listextendedproperty (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_listextendedproperty
- fn_listextendedproperty_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_listextendedproperty function
- displaying extended properties
- database extended properties [SQL Server]
- viewing extended properties
- column extended properties [SQL Server]
- sys.fn_listextendedproperties function
- database objects [SQL Server], extended properties
- extended properties [SQL Server], columns
- table extended properties [SQL Server]
ms.assetid: 59bbb91f-a277-4a35-803e-dcb91e847a49
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3efd2428f9eeae241c0ec9be497c854ba0d91417
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478954"
---
# <a name="sysfn_listextendedproperty-transact-sql"></a>sys.fn_listextendedproperty(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  데이터베이스 개체의 확장 속성 값을 반환합니다.  
 
 
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
fn_listextendedproperty (   
    { default | 'property_name' | NULL }   
  , { default | 'level0_object_type' | NULL }   
  , { default | 'level0_object_name' | NULL }   
  , { default | 'level1_object_type' | NULL }   
  , { default | 'level1_object_name' | NULL }   
  , { default | 'level2_object_type' | NULL }   
  , { default | 'level2_object_name' | NULL }   
  )   
```  
  
## <a name="arguments"></a>인수  
 {기본값 | '*property_name*' | N  
 속성 이름입니다. *property_name* 는 **sysname** 입니다. 유효한 입력은 기본값, NULL, 속성 이름입니다.  
  
 {기본값 | '*level0_object_type*' | N  
 사용자 또는 사용자 정의 형식입니다. *level0_object_type* 는 **varchar (128)** 이며 기본값은 NULL입니다. 유효한 입력은 ASSEMBLY, CONTRACT, EVENT NOTIFICATION, FILEGROUP, MESSAGE TYPE, PARTITION FUNCTION, PARTITION SCHEME, REMOTE SERVICE BINDING, ROUTE, SCHEMA, SERVICE, TRIGGER, TYPE, USER 및 NULL입니다.  
  
> [!IMPORTANT]  
>  수준 0 유형 USER와 TYPE은 나중 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 말고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. USER 대신 SCHEMA를 수준 0 유형으로 사용합니다. TYPE의 경우 수준 0 유형으로 SCHEMA를 사용하고 수준 1 유형으로 TYPE을 사용합니다.  
  
 {기본값 | '*level0_object_name*' | N  
 지정된 수준 0 개체 유형의 이름입니다. *level0_object_name* 는 **sysname** 이며 기본값은 NULL입니다. 유효한 입력은 기본값, NULL, 개체 이름입니다.  
  
 {기본값 | '*level1_object_type*' | N  
 수준 1 개체의 유형입니다. *level1_object_type* 는 **varchar (128)** 이며 기본값은 NULL입니다. 유효한 입력은 AGGREGATE, DEFAULT, FUNCTION, LOGICAL FILE NAME, PROCEDURE, QUEUE, RULE, SYNONYM, TABLE, TYPE, VIEW, XML SCHEMA COLLECTION 및 NULL입니다.  
  
> [!NOTE]  
>  기본값은 NULL에 매핑되며 'default'는 개체 유형 DEFAULT에 매핑됩니다.  
  
 {기본값 | '*level1_object_name*' | N  
 지정된 수준 1 개체 유형의 이름입니다. *level1_object_name* 는 **sysname** 이며 기본값은 NULL입니다. 유효한 입력은 기본값, NULL, 개체 이름입니다.  
  
 {기본값 | '*level2_object_type*' | N  
 수준 2 개체의 유형입니다. *level2_object_type* 는 **varchar (128)** 이며 기본값은 NULL입니다. 유효한 입력은 DEFAULT, 기본값(NULL에 매핑됨) 및 NULL입니다. *Level2_object_type* 에 대 한 유효한 입력은 COLUMN, CONSTRAINT, EVENT NOTIFICATION, INDEX, PARAMETER, TRIGGER 및 NULL입니다.  
  
 {기본값 | '*level2_object_name*' | N  
 지정된 수준 2 개체 유형의 이름입니다. *level2_object_name* 는 **sysname** 이며 기본값은 NULL입니다. 유효한 입력은 기본값, NULL, 개체 이름입니다.  
  
## <a name="tables-returned"></a>반환된 테이블  
 fn_listextendedproperty가 반환하는 테이블의 형식은 다음과 같습니다.  
  
|열 이름|데이터 형식|  
|-----------------|---------------|  
|objtype|**sysname**|  
|objname|**sysname**|  
|name|**sysname**|  
|value|**sql_variant**|  
  
 반환되는 테이블이 비어 있는 경우는 개체에 확장 속성이 없거나 사용자에게 개체의 확장 속성을 나열할 수 있는 권한이 없기 때문입니다. 데이터베이스 자체의 확장 속성을 반환하는 경우 objtype 및 objname 열은 NULL이 됩니다.  
  
## <a name="remarks"></a>설명  
 *Property_name* 값이 NULL 또는 기본값 인 경우 fn_listextendedproperty는 지정 된 개체에 대 한 모든 속성을 반환 합니다.  
  
 개체 유형을 지정했으며 해당 개체 이름 값이 NULL 또는 기본값인 경우 fn_listextendedproperty는 지정된 유형의 모든 개체에 대한 확장 속성을 모두 반환합니다.  
  
 개체는 수준에 따라 구분하는데 수준 0은 최고, 수준 2는 최저를 나타냅니다. 더 낮은 수준의 개체(수준 1 또는 2) 유형과 이름을 지정한 경우에는 NULL이나 기본값이 아닌 부모 개체 유형 및 이름을 지정해야 합니다. 그렇지 않으면 빈 결과 집합을 반환합니다.  
  
 **objname** 은 Latin1_General_CI_AI로 고정 됩니다. 그러나 비교 시 데이터 정렬을 재정의 하 여이 문제를 해결할 수 있습니다.  
  
```  
SELECT o.[object_id] AS 'table_id', o.[name] 'table_name',  
0 AS 'column_order', NULL AS 'column_name', NULL AS 'column_datatype',  
NULL AS 'column_length', Cast(e.value AS varchar(500)) AS 'column_description'  
FROM AdventureWorks.sys.objects AS o  
LEFT JOIN sys.fn_listextendedproperty(N'MS_Description', N'user',N'HumanResources',N'table', N'Employee', null, default) AS e  
    ON o.name = e.objname COLLATE SQL_Latin1_General_CP1_CI_AS  
WHERE o.name = 'Employee';  
```  
  
## <a name="permissions"></a>사용 권한  
 개체의 확장 속성을 나열하는 권한은 개체 유형에 따라 다릅니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-displaying-extended-properties-on-a-database"></a>A. 데이터베이스의 확장 속성 표시  
 다음 예에서는 데이터베이스 개체 자체에 설정된 모든 확장 속성을 표시합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT objtype, objname, name, value  
FROM fn_listextendedproperty(default, default, default, default, default, default, default);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `objtype    objname     name            value`  
  
 `---------  ---------   -----------     ----------------------------`  
  
 `NULL       NULL        MS_Description  AdventureWorks2008 Sample OLTP Database`  
  
 `(1 row(s) affected)`  
  
### <a name="b-displaying-extended-properties-on-all-columns-in-a-table"></a>B. 테이블에 있는 모든 열의 확장 속성 표시  
 다음 예에서는 테이블의 열에 대 한 확장 속성을 나열 합니다 `ScrapReason` . 이 속성은 `Production` 스키마에 포함되어 있습니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT objtype, objname, name, value  
FROM fn_listextendedproperty (NULL, 'schema', 'Production', 'table', 'ScrapReason', 'column', default);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `objtype objname      name            value`  
  
 `------- -----------  -------------   ------------------------`  
  
 `COLUMN ScrapReasonID MS_Description  Primary key for ScrapReason records.`  
  
 `COLUMN Name          MS_Description  Failure description.`  
  
 `COLUMN ModifiedDate  MS_Description  Date the record was last updated.`  
  
 `(3 row(s) affected)`  
  
### <a name="c-displaying-extended-properties-on-all-tables-in-a-schema"></a>C. 스키마에 있는 모든 테이블의 확장 속성 표시  
 다음 예에서는 스키마에 포함 된 모든 테이블에 대 한 확장 속성을 나열 합니다 `Sales` .  
  
```  
USE AdventureWorks2012;  
GO  
SELECT objtype, objname, name, value  
FROM fn_listextendedproperty (NULL, 'schema', 'Sales', 'table', default, NULL, NULL);  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_addextendedproperty &#40;](../../relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql.md)   
 [Transact-sql&#41;sp_dropextendedproperty &#40;](../../relational-databases/system-stored-procedures/sp-dropextendedproperty-transact-sql.md)   
 [Transact-sql&#41;sp_updateextendedproperty &#40;](../../relational-databases/system-stored-procedures/sp-updateextendedproperty-transact-sql.md)   
 [Transact-sql&#41;sys.extended_properties &#40;](../../relational-databases/system-catalog-views/extended-properties-catalog-views-sys-extended-properties.md)  
  
  
