---
title: sys.system_parameters (TRANSACT-SQL) | Microsoft Docs
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
- sys.system_parameters
- sys.system_parameters_TSQL
- system_parameters_TSQL
- system_parameters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.system_parameters catalog view
ms.assetid: 0d135c5f-68b5-4009-a0da-35e6abfee0ff
caps.latest.revision: 35
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c3ab19e49735f34a6fed0d8fcef78f7b4df77e87
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43095848"
---
# <a name="syssystemparameters-transact-sql"></a>sys.system_parameters(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  매개 변수가 있는 각 시스템 개체당 한 개의 행을 포함합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|이 매개 변수가 속한 개체의 ID입니다.|  
|**name**|**sysname**|매개 변수의 이름입니다. 개체 내에서 고유합니다.<br /><br /> 개체가 스칼라 함수이면 매개 변수 이름은 반환 값을 나타내는 행에서 빈 문자열입니다.|  
|**parameter_id**|**int**|매개 변수의 ID입니다. 개체 내에서 고유합니다. 개체가 스칼라 함수인 경우 이면 **parameter_id** = 0 나타내는 값을 반환 합니다.|  
|**system_type_id**|**tinyint**|매개 변수 시스템 유형의 ID입니다.|  
|**user_type_id**|**int**|매개 변수의 유형에 대한 사용자 정의 ID입니다.<br /><br /> 연결할 형식의 이름을 반환할 합니다 [sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) 카탈로그 뷰에이 열입니다.|  
|**max_length**|**smallint**|매개 변수의 최대 길이(바이트)입니다. 값은 열 데이터 형식을 저장 하는 경우-1이 됩니다 **(는) 트랜잭션**, **nvarchar(max)**, **varbinary (max)**, 또는 **xml**.|  
|**전체 자릿수**|**tinyint**|숫자 기반일 경우 매개 변수의 전체 자릿수이고 그렇지 않으면 0입니다.|  
|**scale**|**tinyint**|숫자 기반일 경우 매개 변수의 소수 자릿수이고 그렇지 않으면 0입니다.|  
|**is_output**|**bit**|1 = 출력 매개 변수(또는 반환 값)입니다. 아닐 경우는 0입니다.|  
|**is_cursor_ref**|**bit**|1 = 매개 변수가 커서 참조 매개 변수입니다.|  
|**has_default_value**|**bit**|1 = 매개 변수에 기본값이 있습니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 이 카탈로그 뷰의 CLR 개체에 대한 기본값만 유지하므로 [!INCLUDE[tsql](../../includes/tsql-md.md)] 개체의 경우 이 열 값은 항상 0입니다. 매개 변수의 기본 값을 보려면를 [!INCLUDE[tsql](../../includes/tsql-md.md)] 개체, 쿼리는 **정의** 열의 합니다 [sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) 카탈로그 뷰를 사용할지를 [OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md)시스템 함수입니다.|  
|**is_xml_document**|**bit**|1 = 내용이 완전한 XML 문서입니다.<br /><br /> 0 = 내용이 문서 조각 이거나 열 데이터 형식이 아닙니다 **xml**.|  
|**default_value**|**sql_variant**|하는 경우 **has_default_value** 이 1 이면이 열의 값이 매개 변수에 대해 기본값이 고 그렇지 않으면 NULL입니다.|  
|**xml_collection_id**|**int**|0이 아닌 매개 변수의 데이터 형식이 **xml** XML이 입력 되 고 있습니다. 이 값은 매개 변수의 유효성 검사 XML 스키마 네임스페이스를 포함하는 컬렉션의 ID입니다.<br /><br /> 0 = XML 스키마 컬렉션이 없습니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.parameters&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)   
 [sys.all_parameters &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-parameters-transact-sql.md)  
  
  
