---
title: sys.types (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ce1d7cbfc11a425a1e39622b379ad8b34cac6e10
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33221234"
---
# <a name="systypes-transact-sql"></a>sys.types(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  각 시스템 및 사용자 정의 형식당 한 개의 행을 포함합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|형식의 이름입니다. 스키마 내에서 고유합니다.|  
|**system_type_id**|**tinyint**|형식의 내부 시스템 형식 ID입니다.|  
|**user_type_id**|**int**|유형 ID입니다. 데이터베이스 내에서 고유합니다. 시스템 데이터 형식에 대 한 **user_type_id** = **system_type_id**합니다.|  
|**schema_id**|**int**|형식이 속한 스키마의 ID입니다.|  
|**principal_id**|**int**|스키마 소유자와 다른 경우 개별 소유자의 ID입니다. 기본적으로 스키마에 포함된 개체는 스키마 소유자가 소유합니다. 그러나 ALTER AUTHORIZATION 문으로 대체 소유자를 지정하여 소유권을 변경할 수 있습니다.<br /><br /> 대체 개별 소유자가 없으면 NULL입니다.|  
|**max_length**|**smallint**|유형의 최대 길이(바이트)입니다.<br /><br /> -1 = 열 데이터 형식이 **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, 또는 **xml**합니다.<br /><br /> 에 대 한 **텍스트** 열은 **max_length** 값은 16이 됩니다.|  
|**전체 자릿수**|**tinyint**|숫자 기반 형식인 경우에는 형식의 최대 전체 자릿수이며 그렇지 않으면 0입니다.|  
|**소수 자릿수**|**tinyint**|숫자 기반 형식인 경우에는 형식의 최대 소수 자릿수이며 그렇지 않으면 0입니다.|  
|**collation_name**|**sysname**|문자 기반인 경우에는 형식의 데이터 정렬 이름이고 그렇지 않으면 NULL입니다.|  
|**is_nullable**|**bit**|형식이 Null 값을 허용합니다.|  
|**is_user_defined**|**bit**|1 = 사용자 정의 형식입니다.<br /><br /> 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식입니다.|  
|**is_assembly_type**|**bit**|1 = 형식의 구현이 CLR 어셈블리에 정의되어 있습니다.<br /><br /> 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식을 기반으로 하는 형식입니다.|  
|**default_object_id**|**int**|사용 하 여 형식에 바인딩된 독립 실행형 기본값의 ID [sp_bindefault](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)합니다.<br /><br /> 0 = 기본값이 없습니다.|  
|**rule_object_id**|**int**|사용 하 여 형식에 바인딩된 독립 실행형 규칙의 ID [sp_bindrule](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md)합니다.<br /><br /> 0 = 규칙이 없습니다.|  
|**is_table_type**|**bit**|유형이 테이블임을 나타냅니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [스칼라 유형 카탈로그 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [OBJECTPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
