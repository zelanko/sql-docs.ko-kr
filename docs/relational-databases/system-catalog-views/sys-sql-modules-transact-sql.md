---
title: sys.sql_modules (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/09/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sql_modules_TSQL
- sql_modules
- sql_modules_TSQL
- sys.sql_modules
dev_langs: TSQL
helpviewer_keywords: sys.sql_modules catalog view
ms.assetid: 23d3ccd2-f356-4d89-a2cd-bee381243f99
caps.latest.revision: "43"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a2ed39676fc1bd477cce716b5c9d86c721df40fe
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="syssqlmodules-transact-sql"></a>sys.sql_modules(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  각 개체는 다음에서 SQL 언어로 정의 된 모듈에 대 한 행을 반환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 스칼라 사용자 정의 함수를 컴파일된 기본적으로 포함 합니다. P, RF, V, TR, FN, IF, TF 및 R 유형의 개체에는 연결된 SQL 모듈이 있습니다. 이 뷰에는 독립 실행형 기본값인 유형 D 개체에 대한 SQL 모듈 정의도 있습니다. 이러한 형식에 대 한 참조는 **형식** 열에는 [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) 카탈로그 뷰에 있습니다.  
  
 자세한 내용은 참조 [메모리 내 OLTP에 대 한 사용자 정의 스칼라 함수](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|포함하는 개체의 개체 ID입니다. 데이터베이스 내에서 고유합니다.|  
|**definition**|**nvarchar(max)**|이 모듈을 정의하는 SQL 텍스트입니다. 사용 하 여이 값 얻을 수도 있습니다는 [OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md) 기본 제공 함수입니다.<br /><br /> NULL = 암호화됨|  
|**uses_ansi_nulls**|**bit**|SET ANSI_NULLS ON으로 모듈을 만들었습니다.<br /><br /> 규칙과 기본값에 대해서는 항상 0입니다.|  
|**uses_quoted_identifier**|**bit**|SET QUOTED_IDENTIFIER ON으로 모듈을 만들었습니다.|  
|**is_schema_bound**|**bit**|SCHEMABINDING 옵션으로 모듈을 만들었습니다.<br /><br /> 고유하게 컴파일된 저장 프로시저의 경우 항상 1 값을 포함합니다.|  
|**uses_database_collation**|**bit**|1 = 스키마 바운드 모듈 정의는 정확한 평가를 위해 데이터베이스의 기본 데이터 정렬에 의존합니다. 그렇지 않으면 0입니다. 이러한 종속성으로 인해 데이터베이스의 기본 데이터 정렬을 바꿀 수 없습니다.|  
|**is_recompiled**|**bit**|WITH RECOMPILE 옵션으로 프로시저를 만들었습니다.|  
|**null_on_null_input**|**bit**|임의의 NULL 입력에 대해 NULL 출력을 생성하기 위해 모듈을 선언했습니다.|  
|**execute_as_principal_id**|**Int**|EXECUTE AS 데이터베이스 보안 주체의 ID입니다.<br /><br /> 기본값은 NULL이며 EXECUTE AS CALLER인 경우에도 NULL입니다.<br /><br /> 경우 지정한 보안 주체의 ID EXECUTE AS SELF 또는 EXECUTE AS \<주 > 합니다.<br /><br /> -2 = EXECUTE AS OWNER|  
|**uses_native_compilation**|**bit**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]까지<br /><br /> 0 = 고유 컴파일 아님<br /><br /> 1 = 고유 컴파일<br /><br /> 기본값은 0입니다.|  
  
## <a name="remarks"></a>주의  
 DEFAULT 제약 조건 유형 D 개체에 대 한 SQL 식에서 발견 되는 [sys.default_constraints](../../relational-databases/system-catalog-views/sys-default-constraints-transact-sql.md) 카탈로그 뷰에 있습니다. CHECK 제약 조건, C, 형식의 개체에 대 한 SQL 식에서 발견 되는 [sys.check_constraints](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md) 카탈로그 뷰에 있습니다.  
  
 이 정보에도 설명 되어 [sys.dm_db_uncontained_entities&#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="examples"></a>예  
 다음 예에서는 현재 데이터베이스의 각 모듈에 대한 이름, 유형 및 정의를 반환합니다.  
  
```  
SELECT sm.object_id, OBJECT_NAME(sm.object_id) AS object_name, o.type, o.type_desc, sm.definition  
FROM sys.sql_modules AS sm  
JOIN sys.objects AS o ON sm.object_id = o.object_id  
ORDER BY o.type;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [개체 카탈로그 뷰 &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
