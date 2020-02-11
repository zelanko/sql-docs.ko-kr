---
title: sys. types (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- types
- types_TSQL
- sys.types_TSQL
- sys.types
dev_langs:
- TSQL
helpviewer_keywords:
- sys.types catalog view
- table-valued parameters,sys.types
ms.assetid: a5dbc842-71a0-4f62-b5e0-f560a99b7f8c
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ff4cd58fcd7d11679cf410c9f379b101d42ce4bf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68095567"
---
# <a name="systypes-transact-sql"></a>sys.types(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  각 시스템 및 사용자 정의 형식당 한 개의 행을 포함합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|형식의 이름입니다. 스키마 내에서 고유합니다.|  
|**system_type_id**|**tinyint**|형식의 내부 시스템 형식 ID입니다.|  
|**user_type_id**|**int**|유형 ID입니다. 데이터베이스 내에서 고유합니다. 시스템 데이터 형식의 경우**system_type_id**을 **user_type_id** = 합니다.|  
|**schema_id**|**int**|형식이 속한 스키마의 ID입니다.|  
|**principal_id**|**int**|스키마 소유자와 다른 경우 개별 소유자의 ID입니다. 기본적으로 스키마에 포함된 개체는 스키마 소유자가 소유합니다. 그러나 ALTER AUTHORIZATION 문으로 대체 소유자를 지정하여 소유권을 변경할 수 있습니다.<br /><br /> 대체 개별 소유자가 없으면 NULL입니다.|  
|**max_length**|**smallint**|유형의 최대 길이(바이트)입니다.<br /><br /> -1 = 열 데이터 형식이 **varchar (max)**, **nvarchar (max)**, **varbinary (max)** 또는 **xml**입니다.<br /><br /> **텍스트** 열의 경우에는 **max_length** 값이 16이 됩니다.|  
|**전체 자릿수**|**tinyint**|숫자 기반 형식인 경우에는 형식의 최대 전체 자릿수이며 그렇지 않으면 0입니다.|  
|**배율을**|**tinyint**|숫자 기반 형식인 경우에는 형식의 최대 소수 자릿수이며 그렇지 않으면 0입니다.|  
|**collation_name**|**sysname**|문자 기반인 경우에는 형식의 데이터 정렬 이름이고 그렇지 않으면 NULL입니다.|  
|**is_nullable**|**bit**|형식이 Null 값을 허용합니다.|  
|**is_user_defined**|**bit**|1 = 사용자 정의 형식입니다.<br /><br /> 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식입니다.|  
|**is_assembly_type**|**bit**|1 = 형식의 구현이 CLR 어셈블리에 정의되어 있습니다.<br /><br /> 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식을 기반으로 하는 형식입니다.|  
|**default_object_id**|**int**|[Sp_bindefault](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)를 사용 하 여 형식에 바인딩된 독립 실행형 기본값의 ID입니다.<br /><br /> 0 = 기본값이 없습니다.|  
|**rule_object_id**|**int**|[Sp_bindrule](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md)를 사용 하 여 형식에 바인딩된 독립 실행형 규칙의 ID입니다.<br /><br /> 0 = 규칙이 없습니다.|  
|**is_table_type**|**bit**|유형이 테이블임을 나타냅니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Transact-sql&#41;&#40;스칼라 형식 카탈로그 뷰](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-sql&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리에 대한 질문과 대답](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
