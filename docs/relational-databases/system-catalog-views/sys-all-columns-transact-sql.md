---
title: sys.all_columns (TRANSACT-SQL) | Microsoft Docs
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
- all_columns_TSQL
- all_columns
- sys.all_columns_TSQL
- sys.all_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.all_columns catalog view
ms.assetid: 40e04fe9-0b64-4799-84c0-57f128b2bdc2
caps.latest.revision: 48
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: aecb0e276bff562dcafa072418c5f31c48fde3a4
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39540507"
---
# <a name="sysallcolumns-transact-sql"></a>sys.all_columns(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  사용자 정의 개체 및 시스템 개체에 속하는 모든 열을 보여 줍니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|이 열이 속한 개체의 ID입니다.|  
|NAME|**sysname**|열의 이름입니다. 개체 내에서 고유합니다.|  
|column_id|**int**|열의 ID입니다. 개체 내에서 고유합니다.<br /><br /> 열 ID는 순차적이지 않을 수 있습니다.|  
|system_type_id|**tinyint**|열의 시스템 유형 ID입니다.|  
|user_type_id|**int**|열의 유형에 대한 사용자 정의 ID입니다.<br /><br /> 연결할 형식의 이름을 반환할 합니다 [sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) 카탈로그 뷰에이 열입니다.|  
|max_length|**smallint**|열의 최대 길이(바이트)입니다.<br /><br /> -1 = 열 데이터 형식이 **varchar (max)**, **nvarchar (max)** 하십시오 **varbinary (max)**, 또는 **xml**.<br /><br /> 에 대 한 **텍스트** 열의 경우 max_length 값은 16 이거나 sp_tableoption 'text in row'에서 설정한 값입니다.|  
|전체 자릿수|**tinyint**|숫자 기반일 경우에는 열의 전체 자릿수이고, 그렇지 않으면 0입니다.|  
|소수 자릿수|**tinyint**|숫자 기반일 경우에는 열의 소수 자릿수이고, 그렇지 않으면 0입니다.|  
|collation_name|**sysname**|문자 기반일 경우에는 열의 데이터 정렬 이름이고, 그렇지 않으면 NULL입니다.|  
|is_nullable|**bit**|1 = 열이 Null 값을 허용합니다.|  
|is_ansi_padded|**bit**|1 = 열이 문자, 이진 또는 variant인 경우 ANSI_PADDING ON 동작을 사용합니다.<br /><br /> 0 = 열이 문자, 이진 또는 variant가 아닙니다.|  
|is_rowguidcol|**bit**|1 = 선언된 ROWGUIDCOL 열입니다.|  
|is_identity|**bit**|1 = 열에 ID 값이 있습니다.|  
|is_computed|**bit**|1 = 열이 계산 열입니다.|  
|is_filestream|**bit**|1 = 파일 스트림 저장소를 사용하도록 선언된 열입니다.|  
|is_replicated|**bit**|1 = 복제된 열입니다.|  
|is_non_sql_subscribed|**bit**|1 = 열에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자가 있습니다.|  
|is_merge_published|**bit**|1 = 병합 게시 열입니다.|  
|is_dts_replicated|**bit**|1 = [!INCLUDE[ssIS](../../includes/ssis-md.md)]를 사용해 복제된 열입니다.|  
|is_xml_document|**bit**|1 = 내용이 완전한 XML 문서입니다.<br /><br /> 0 = 내용이 문서 조각이거나 열 데이터 형식이 XML이 아닙니다.|  
|xml_collection_id|**int**|0이 아닌 열의 데이터 형식이 면 **xml** XML이 입력 되 고 있습니다. 이 값은 열의 유효성 검사 XML 스키마 네임스페이스가 들어 있는 컬렉션의 ID가 됩니다.<br /><br /> 0 = XML 스키마 컬렉션이 없습니다.|  
|default_object_id|**int**|독립 실행형 인지에 관계 없이 기본 개체의 ID [sys.sp_bindefault](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md), 또는 인라인, 열 수준 DEFAULT 제약 조건입니다. 인라인 열 수준 기본 개체의 parent_object_id 열은 테이블 자체에 대한 역참조입니다.<br /><br /> 0 = 기본값이 없습니다.|  
|rule_object_id|**int**|sys.sp_bindrule을 사용하여 열에 바인딩된 독립 실행형 규칙의 ID입니다.<br /><br /> 0 = 독립 실행형 규칙이 없습니다.<br /><br /> 열 수준 CHECK 제약 조건 참조 [sys.check_constraints &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)합니다.|  
|is_sparse|bit|1 = 열이 스파스 열입니다. 자세한 내용은 [스파스 열 사용](../../relational-databases/tables/use-sparse-columns.md)을 참조하세요.|  
|is_column_set|bit|1 = 열이 열 집합입니다. 자세한 내용은 [열 집합 사용](../../relational-databases/tables/use-column-sets.md)을 참조하세요.|  
|generated_always_type|**tinyint**|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 열 형식을 나타내는 숫자 값입니다.<br /><br /> 0 = NOT_APPLICABLE<br /><br /> 1 = AS_ROW_START<br /><br /> 2 = AS_ROW_END|  
|generated_always_type_desc|**nvarchar(60)**|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 열 형식에 대 한 텍스트 설명.<br /><br /> NOT_APPLICABLE<br /><br /> AS_ROW_START<br /><br /> AS_ROW_END|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.system_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-columns-transact-sql.md)   
 [sys.computed_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)  
  
  
