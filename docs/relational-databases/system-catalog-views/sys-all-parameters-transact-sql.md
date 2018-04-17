---
title: sys.all_parameters (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8de0c0b19a858bd129797edad00f86cd92bbaef8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sysallparameters-transact-sql"></a>sys.all_parameters(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  사용자 정의 개체나 시스템 개체에 속하는 모든 매개 변수의 합집합을 표시합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|이 매개 변수가 속한 개체의 ID입니다.|  
|**name**|**sysname**|매개 변수의 이름입니다. 개체 내에서 고유합니다. 개체가 스칼라 함수이면 매개 변수 이름은 반환 값을 나타내는 행에서 빈 문자열입니다.|  
|**parameter_id**|**int**|매개 변수의 ID입니다. 개체 내에서 고유합니다. 개체가 스칼라 함수인 경우 **parameter_id** = 0 반환 값입니다.|  
|**system_type_id**|**tinyint**|매개 변수 시스템 유형의 ID입니다.|  
|**user_type_id**|**int**|매개 변수의 유형에 대한 사용자 정의 ID입니다.<br /><br /> 형식의 이름을 반환 하려면에 가입는 [sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) 카탈로그 뷰에서이 열에 있습니다.|  
|**max_length**|**smallint**|매개 변수의 최대 길이(바이트)입니다.<br /><br /> -1 = 열 데이터 형식이 **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, 또는 **xml**합니다.|  
|**전체 자릿수**|**tinyint**|매개 변수가 숫자 기반일 경우 매개 변수의 전체 자릿수이고, 그렇지 않으면 0입니다.|  
|**소수 자릿수**|**tinyint**|매개 변수가 숫자 기반일 경우 매개 변수의 소수 자릿수이고, 그렇지 않으면 0입니다.|  
|**is_output**|**bit**|1 = 출력 매개 변수(또는 반환 값)입니다. 아닐 경우는 0입니다.|  
|**is_cursor_ref**|**bit**|1 = 매개 변수가 커서 참조 매개 변수입니다.|  
|**has_default_value**|**bit**|1 = 매개 변수에 기본값이 있습니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 이 카탈로그 뷰의 CLR 개체에 대한 기본값만 유지하므로 [!INCLUDE[tsql](../../includes/tsql-md.md)] 개체의 경우 이 열 값은 항상 0입니다. 매개 변수 기본값을 보려면는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 개체, 쿼리는 **정의** 의 열은 [sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) 카탈로그 뷰를 사용 하 여 또는 [OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md)시스템 함수입니다.|  
|**is_xml_document**|**bit**|1 = 내용이 완전한 XML 문서입니다.<br /><br /> 0 = 내용이 문서 조각 또는 열의 데이터 형식이 않습니다 **xml**합니다.|  
|**default_value**|**sql_variant**|경우 **has_default_value** 1 이면이 열의 값 매개 변수의 기본값이 가치가 고 그렇지 않으면 NULL입니다.|  
|**xml_collection_id**|**int**|매개 변수 유효성 검사에 사용되는 XML 스키마 컬렉션의 ID입니다.<br /><br /> 매개 변수 데이터 형식의 경우 0이 아닌 **xml** XML이 입력 하 고 있습니다.<br /><br /> 0 = XML 스키마 컬렉션이 없거나 매개 변수가 XML이 아닙니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.parameters&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)   
 [sys.system_parameters &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-parameters-transact-sql.md)  
  
  
