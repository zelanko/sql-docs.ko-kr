---
title: sys. all_parameters (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- all_parameters_TSQL
- sys.all_parameters
- all_parameters
- sys.all_parameters_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.all_parameters catalog view
ms.assetid: eecbb68e-9b4c-4243-94e2-8096a9cc7892
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3651de5aba112eb48fcb49a066ab409c396d6f14
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85718934"
---
# <a name="sysall_parameters-transact-sql"></a>sys.all_parameters(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asdw-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  사용자 정의 개체나 시스템 개체에 속하는 모든 매개 변수의 합집합을 표시합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|이 매개 변수가 속한 개체의 ID입니다.|  
|**name**|**sysname**|매개 변수의 이름입니다. 개체 내에서 고유합니다. 개체가 스칼라 함수이면 매개 변수 이름은 반환 값을 나타내는 행에서 빈 문자열입니다.|  
|**parameter_id**|**int**|매개 변수의 ID입니다. 개체 내에서 고유합니다. 개체가 스칼라 함수인 경우 **parameter_id** = 0은 반환 값을 나타냅니다.|  
|**system_type_id**|**tinyint**|매개 변수 시스템 유형의 ID입니다.|  
|**user_type_id**|**int**|매개 변수의 유형에 대한 사용자 정의 ID입니다.<br /><br /> 형식의 이름을 반환 하려면이 열에 대 한 [sys. types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) 카탈로그 뷰에 조인 합니다.|  
|**max_length**|**smallint**|매개 변수의 최대 길이(바이트)입니다.<br /><br /> -1 = 열 데이터 형식이 **varchar (max)**, **nvarchar (max)**, **varbinary (max)** 또는 **xml**입니다.|  
|**전체 자릿수**|**tinyint**|매개 변수가 숫자 기반일 경우 매개 변수의 전체 자릿수이고, 그렇지 않으면 0입니다.|  
|**scale**|**tinyint**|매개 변수가 숫자 기반일 경우 매개 변수의 소수 자릿수이고, 그렇지 않으면 0입니다.|  
|**is_output**|**bit**|1 = 출력 매개 변수(또는 반환 값)입니다. 아닐 경우는 0입니다.|  
|**is_cursor_ref**|**bit**|1 = 매개 변수가 커서 참조 매개 변수입니다.|  
|**has_default_value**|**bit**|1 = 매개 변수에 기본값이 있습니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 이 카탈로그 뷰의 CLR 개체에 대한 기본값만 유지하므로 [!INCLUDE[tsql](../../includes/tsql-md.md)] 개체의 경우 이 열 값은 항상 0입니다. 개체에서 매개 변수의 기본값을 보려면 [!INCLUDE[tsql](../../includes/tsql-md.md)] [sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) 카탈로그 뷰의 **정의** 열을 쿼리하거나 [OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md) 시스템 함수를 사용 합니다.|  
|**is_xml_document**|**bit**|1 = 내용이 완전한 XML 문서입니다.<br /><br /> 0 = 내용이 문서 조각 이거나 열의 데이터 형식이 **xml**이 아닙니다.|  
|**default_value**|**sql_variant**|**Has_default_value** 1 인 경우이 열의 값은 매개 변수의 기본값입니다. 그렇지 않으면 NULL입니다.|  
|**xml_collection_id**|**int**|매개 변수 유효성 검사에 사용되는 XML 스키마 컬렉션의 ID입니다.<br /><br /> 매개 변수의 데이터 형식이 **xml** 이 고 xml이 입력 된 경우 0이 아닌 값입니다.<br /><br /> 0 = XML 스키마 컬렉션이 없거나 매개 변수가 XML이 아닙니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;개체 카탈로그 뷰](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Transact-sql&#41;&#40;카탈로그 뷰](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys. Transact-sql&#41;&#40;매개 변수](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)   
 [Transact-sql&#41;&#40;tem_parameterssys.sys](../../relational-databases/system-catalog-views/sys-system-parameters-transact-sql.md)  
  
  
