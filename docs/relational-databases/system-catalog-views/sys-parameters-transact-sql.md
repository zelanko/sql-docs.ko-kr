---
title: sys.parameters (TRANSACT-SQL) | Microsoft Docs
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
- sys.parameters_TSQL
- sys.parameters
- parameters
- parameters_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.parameters catalog view
- table-valued parameters,sys.parameters
ms.assetid: 24e2764b-c8e5-4322-97a4-7407d8b8a92b
caps.latest.revision: 49
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b2102ca6ea11d87bdc73984fea3d03ca8fbad046
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43083621"
---
# <a name="sysparameters-transact-sql"></a>sys.parameters(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  매개 변수를 받는 개체의 각 매개 변수당 하나의 행을 포함합니다. 개체가 스칼라 함수인 경우 반환 값을 설명하는 단일 행도 있으며 해당 행을 **parameter_id** 값이 0입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|이 매개 변수가 속한 개체의 ID입니다.|  
|**name**|**sysname**|매개 변수의 이름입니다. 개체 내에서 고유합니다.<br /><br /> 개체가 스칼라 함수이면 매개 변수 이름은 반환 값을 나타내는 행에서 빈 문자열입니다.|  
|**parameter_id**|**int**|매개 변수의 ID입니다. 개체 내에서 고유합니다.<br /><br /> 개체가 스칼라 함수인 경우 이면 **parameter_id** = 0 나타내는 값을 반환 합니다.|  
|**system_type_id**|**tinyint**|매개 변수 시스템 유형의 ID입니다.|  
|**user_type_id**|**int**|매개 변수의 유형에 대한 사용자 정의 ID입니다.<br /><br /> 연결할 형식의 이름을 반환할 합니다 [sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) 카탈로그 뷰에이 열입니다.|  
|**max_length**|**smallint**|매개 변수의 최대 길이(바이트)입니다.<br /><br /> 값-1 = 열 데이터 형식이 있는 경우 **varchar (max)**, **nvarchar (max)** 하십시오 **varbinary (max)**, 또는 **xml**합니다.|  
|**전체 자릿수**|**tinyint**|숫자 기반일 경우 매개 변수의 전체 자릿수이고 그렇지 않으면 0입니다.|  
|**scale**|**tinyint**|숫자 기반일 경우 매개 변수의 소수 자릿수이고 그렇지 않으면 0입니다.|  
|**is_output**|**bit**|1 = 매개 변수가 출력 또는 반환 값인 경우, 그렇지 않으면 0입니다.|  
|**is_cursor_ref**|**bit**|1 = 매개 변수가 커서 참조 매개 변수입니다.|  
|**has_default_value**|**bit**|1 = 매개 변수에 기본값이 있습니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 이 카탈로그 뷰의 CLR 개체에 대한 기본값만 유지하므로 [!INCLUDE[tsql](../../includes/tsql-md.md)] 개체의 경우 이 열 값은 0입니다. 매개 변수의 기본 값을 보려면를 [!INCLUDE[tsql](../../includes/tsql-md.md)] 개체, 쿼리는 **정의** 열의 합니다 [sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) 카탈로그 뷰를 사용할지를 [OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md)시스템 함수입니다.|  
|**is_xml_document**|**bit**|1 = 내용이 완전한 XML 문서입니다.<br /><br /> 0 = 내용이 문서 조각 또는 열의 데이터 형식은 아닙니다 **xml**합니다.|  
|**default_value**|**sql_variant**|경우 **has_default_value** 이 1 이면이 열의 값 매개 변수 기본값의 값은 그렇지 않은 경우 NULL.|  
|**xml_collection_id**|**int**|0이 아닌 매개 변수의 데이터 형식이 **xml** XML이 입력 되 고 있습니다. 매개 변수의 유효성 검사 XML 스키마 네임스페이스를 포함하는 컬렉션의 ID가 됩니다.<br /><br /> 0 = XML 스키마 컬렉션이 없습니다.|  
|**is_readonly**|**bit**|1 = 매개 변수가 읽기 전용인 경우, 그렇지 않으면 0입니다.|  
|**is_nullable**|**bit**|1 = 매개 변수가 null을 허용합니다. (기본값).<br /><br /> 0 = 고유하게 컴파일된 저장 프로시저를 보다 효율적으로 실행할 수 있도록 매개 변수가 null을 허용하지 않습니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.all_parameters &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-parameters-transact-sql.md)   
 [sys.system_parameters &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-parameters-transact-sql.md)  
  
  
