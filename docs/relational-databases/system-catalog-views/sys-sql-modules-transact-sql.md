---
title: sys. sql_modules (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 11/06/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sql_modules_TSQL
- sql_modules
- sql_modules_TSQL
- sys.sql_modules
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sql_modules catalog view
ms.assetid: 23d3ccd2-f356-4d89-a2cd-bee381243f99
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: dd05afece6814beb84e3fa079b02f661f14990bd
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85783949"
---
# <a name="syssql_modules-transact-sql"></a>sys.sql_modules(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asdw-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  고유 하 게 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴파일된 스칼라 사용자 정의 함수를 포함 하 여의 SQL 언어로 정의 된 모듈인 각 개체에 대해 하나의 행을 반환 합니다. P, RF, V, TR, FN, IF, TF 및 R 유형의 개체에는 연결된 SQL 모듈이 있습니다. 이 뷰에는 독립 실행형 기본값인 유형 D 개체에 대한 SQL 모듈 정의도 있습니다. 이러한 유형에 대 한 설명은 [sys. objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) 카탈로그 뷰의 **type** 열을 참조 하세요.  
  
 자세한 내용은 [메모리 내 OLTP에 대한 사용자 정의 스칼라 함수](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)를 참조하세요.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|포함하는 개체의 개체 ID입니다. 데이터베이스 내에서 고유합니다.|  
|**정의**|**nvarchar(max)**|이 모듈을 정의하는 SQL 텍스트입니다. [OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md) 기본 제공 함수를 사용 하 여이 값을 가져올 수도 있습니다.<br /><br /> NULL = 암호화됨|  
|**uses_ansi_nulls**|**bit**|SET ANSI_NULLS ON으로 모듈을 만들었습니다.<br /><br /> 규칙과 기본값에 대해서는 항상 0입니다.|  
|**uses_quoted_identifier**|**bit**|SET QUOTED_IDENTIFIER ON으로 모듈을 만들었습니다.|  
|**is_schema_bound**|**bit**|SCHEMABINDING 옵션으로 모듈을 만들었습니다.<br /><br /> 고유하게 컴파일된 저장 프로시저의 경우 항상 1 값을 포함합니다.|  
|**uses_database_collation**|**bit**|1 = 스키마 바운드 모듈 정의는 정확한 평가를 위해 데이터베이스의 기본 데이터 정렬에 의존합니다. 그렇지 않으면 0입니다. 이러한 종속성으로 인해 데이터베이스의 기본 데이터 정렬을 바꿀 수 없습니다.|  
|**is_recompiled**|**bit**|WITH RECOMPILE 옵션으로 프로시저를 만들었습니다.|  
|**null_on_null_input**|**bit**|임의의 NULL 입력에 대해 NULL 출력을 생성하기 위해 모듈을 선언했습니다.|  
|**execute_as_principal_id**|**정수**|EXECUTE AS 데이터베이스 보안 주체의 ID입니다.<br /><br /> 기본값은 NULL이며 EXECUTE AS CALLER인 경우에도 NULL입니다.<br /><br /> EXECUTE AS SELF 또는 EXECUTE AS를 지정 하는 경우 지정 된 보안 주체의 ID입니다 \<principal> .<br /><br /> -2 = EXECUTE AS OWNER|  
|**uses_native_compilation**|**bit**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]까지<br /><br /> 0 = 고유 컴파일 아님<br /><br /> 1 = 고유 컴파일<br /><br /> 기본값은 0입니다.|  
|**is_inlineable**|**bit**|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssqlv15-md.md)] 이상<br/><br />모듈이 inlineable 인지 여부를 나타냅니다. Inlineability는 [여기](../user-defined-functions/scalar-udf-inlining.md#inlineable-scalar-udfs-requirements)에 지정 된 조건을 기반으로 합니다.<br /><br /> 0 = inlineable 안 함<br /><br /> 1 = inlineable입니다. <br /><br /> 스칼라 Udf의 경우 UDF가 inlineable 인 경우 값은 1이 고, 그렇지 않으면 0입니다. 이 값은 항상 인라인 Tvf 값 1을 포함 하 고 다른 모든 모듈 형식에 대해 0을 포함 합니다.<br />|  
|**inline_type**|**bit**|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssqlv15-md.md)] 이상<br /><br />현재 모듈에 대해 인라인이 설정 되어 있는지 여부를 나타냅니다. <br /><br />0 = 인라이닝을 해제 합니다.<br /><br /> 1 = 인라인이 설정 되어 있습니다.<br /><br /> 스칼라 Udf의 경우 인라인을 명시적 또는 암시적으로 설정 하면 값은 1이 됩니다. 인라인 Tvf 값은 항상 1이 고 다른 모듈 형식의 경우 0입니다.<br />|  

  
## <a name="remarks"></a>설명  
 기본 제약 조건에 대 한 SQL 식 인 D 형식의 개체는 [default_constraints](../../relational-databases/system-catalog-views/sys-default-constraints-transact-sql.md) 카탈로그 뷰에서 찾을 수 있습니다. CHECK 제약 조건에 대 한 SQL 식 인 C 형식의 개체는 [sys. check_constraints](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md) 카탈로그 뷰에 있습니다.  
  
 이 정보는 [dm_db_uncontained_entities &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql.md)에도 설명 되어 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="examples"></a>예제  
 다음 예에서는 현재 데이터베이스의 각 모듈에 대한 이름, 유형 및 정의를 반환합니다.  
  
```  
SELECT sm.object_id, OBJECT_NAME(sm.object_id) AS object_name, o.type, o.type_desc, sm.definition  
FROM sys.sql_modules AS sm  
JOIN sys.objects AS o ON sm.object_id = o.object_id  
ORDER BY o.type;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;카탈로그 뷰](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Transact-sql&#41;&#40;개체 카탈로그 뷰](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
