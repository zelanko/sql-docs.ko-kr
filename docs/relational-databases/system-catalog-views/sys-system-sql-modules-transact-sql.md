---
description: sys.system_sql_modules(Transact-SQL)
title: sys.system_sql_modules (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- system_sql_modules_TSQL
- sys.system_sql_modules
- sys.system_sql_modules_TSQL
- system_sql_modules
dev_langs:
- TSQL
helpviewer_keywords:
- sys.system_sql_modules catalog view
ms.assetid: ad3548bc-4780-4821-b962-b421d52daed9
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3f91a0f22a4091af3e535b548925cad83293a11a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97428897"
---
# <a name="syssystem_sql_modules-transact-sql"></a>sys.system_sql_modules(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  SQL 언어로 정의된 모듈을 포함하는 각 시스템 개체에 대해 행을 반환합니다. FN, IF, P, PC, TF, V 형식의 시스템 개체에는 연관된 SQL 모듈이 있습니다. 포함 하는 개체를 식별 하려면이 뷰를 [sys.system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md)에 조인할 수 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|포함하는 개체의 개체 ID이며 데이터베이스 내에서 고유합니다.|  
|**정의**|**nvarchar(max)**|이 모듈을 정의하는 SQL 텍스트입니다.|  
|**uses_ansi_nulls**|**bit**|1 = SET ANSI_NULLS 데이터베이스 옵션을 ON으로 설정하여 모듈을 만들었습니다.<br /><br /> 항상 1을 반환 합니다.|  
|**uses_quoted_identifier**|**bit**|1 = SET QUOTED_IDENTIFIER를 ON으로 설정하여 모듈을 만들었습니다.<br /><br /> 항상 1을 반환 합니다.|  
|**is_schema_bound**|**bit**|0 = SCHEMABINDING 옵션으로 모듈을 만들지 않았습니다.<br /><br /> 항상 0을 반환합니다.|  
|**uses_database_collation**|**bit**|0 = 모듈이 데이터베이스의 기본 데이터 정렬에 종속되지 않습니다.<br /><br /> 항상 0을 반환합니다.|  
|**is_recompiled**|**bit**|0 = WITH RECOMPILE 옵션을 사용하여 프로시저를 만들지 않았습니다.<br /><br /> 항상 0을 반환합니다.|  
|**null_on_null_input**|**bit**|0 = NULL 입력에 NULL 출력을 만들어내도록 모듈을 만들지 않았습니다.<br /><br /> 항상 0을 반환합니다.|  
|**execute_as_principal_id**|**int**|항상 NULL을 반환합니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [sys.sql_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [Transact-sql&#41;sys.all_sql_modules &#40;](../../relational-databases/system-catalog-views/sys-all-sql-modules-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
