---
description: sys.all_sql_modules(Transact-SQL)
title: sys.all_sql_modules (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- all_sql_modules_TSQL
- sys.all_sql_modules
- all_sql_modules
- sys.all_sql_modules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.all_sql_modules catalog view
ms.assetid: 7477a3fe-afb3-44c8-bb2c-c6e1d9bdee6f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 031c6e5e270fed4b198b4248dc2864cd3c6aedb7
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97461704"
---
# <a name="sysall_sql_modules-transact-sql"></a>sys.all_sql_modules(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  **Sys.sql_modules** 와 **sys.system_sql_modules** 의 합집합을 반환 합니다.  
  
 뷰는 고유 하 게 컴파일된 각 스칼라 사용자 정의 함수에 대해 하나의 행을 반환 합니다. 자세한 내용은 [메모리 내 OLTP에 대한 사용자 정의 스칼라 함수](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)를 참조하세요.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|포함하는 개체의 개체 ID입니다. 데이터베이스 내에서 고유합니다.|  
|**정의**|**nvarchar(max)**|이 모듈을 정의하는 SQL 텍스트입니다.<br /><br /> NULL = 암호화됨|  
|**uses_ansi_nulls**|**bit**|SET ANSI_NULLS ON으로 모듈을 만들었습니다.|  
|**uses_quoted_identifier**|**bit**|SET QUOTED_IDENTIFIER ON으로 모듈을 만들었습니다.|  
|**is_schema_bound**|**bit**|SCHEMABINDING 옵션으로 모듈을 만들었습니다.|  
|**uses_database_collation**|**bit**|1 = 스키마 바운드 모듈 정의는 정확한 평가를 위해 데이터베이스의 기본 데이터 정렬에 의존합니다. 그렇지 않으면 0입니다. 이러한 종속성으로 인해 데이터베이스의 기본 데이터 정렬을 바꿀 수 없습니다.|  
|**is_recompiled**|**bit**|WITH RECOMPILE 옵션으로 프로시저를 만들었습니다.|  
|**null_on_null_input**|**bit**|임의의 NULL 입력에 대해 NULL 출력을 생성하기 위해 모듈을 선언했습니다.|  
|**execute_as_principal_id**|**int**|EXECUTE AS 데이터베이스 보안 주체의 ID입니다.<br /><br /> 기본값은 NULL이며 EXECUTE AS CALLER인 경우에도 NULL입니다.<br /><br /> EXECUTE AS SELF 또는 EXECUTE AS를 지정 하는 경우 지정 된 보안 주체의 ID입니다 \<principal> .<br /><br /> -2 = EXECUTE AS OWNER|  
|**uses_native_compilation**|bit|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상<br /><br /> 0 = 고유 컴파일 아님<br /><br /> 1 = 고유 컴파일<br /><br /> 기본값은 0입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [sys.sql_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [ Transact-sql&#41;&#40;tem_sql_modulessys.sys](../../relational-databases/system-catalog-views/sys-system-sql-modules-transact-sql.md)   
 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
