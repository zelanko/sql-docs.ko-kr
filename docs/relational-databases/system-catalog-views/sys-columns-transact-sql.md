---
title: sys.columns (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/21/2017
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
- sys.columns_TSQL
- sys.columns
- columns_TSQL
- columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.columns catalog view
ms.assetid: 323ac9ea-fc52-4b8c-8a7e-e0e44f8ed86c
caps.latest.revision: 57
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a34920ed4b98537dd9a405123de1124480e0e693
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="syscolumns-transact-sql"></a>sys.columns(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  뷰 또는 테이블과 같이 열을 갖고 있는 개체의 각 열에 대한 행을 반환합니다. 다음은 열을 갖고 있는 개체 형식의 목록입니다.  
  
-   테이블 반환 어셈블리 함수(FT)  
  
-   인라인 테이블 반환 SQL 함수(IF)  
  
-   내부 테이블(IT)  
  
-   시스템 테이블(S)  
  
-   테이블 반환 SQL 함수(TF)  
  
-   사용자 테이블(U)  
  
-   뷰(V)  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|이 열이 속한 개체의 ID입니다.|  
|name|**sysname**|열의 이름입니다. 개체 내에서 고유합니다.|  
|column_id|**int**|열의 ID입니다. 개체 내에서 고유합니다.<br /><br /> 열 ID는 순차적이지 않을 수 있습니다.|  
|system_type_id|**tinyint**|열의 시스템 유형 ID입니다.|  
|user_type_id|**int**|열의 유형에 대한 사용자 정의 ID입니다.<br /><br /> 형식의 이름을 반환 하려면에 가입는 [sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) 카탈로그 뷰에서이 열에 있습니다.|  
|max_length|**smallint**|열의 최대 길이(바이트)입니다.<br /><br /> -1 = 열 데이터 형식이 **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, 또는 **xml**합니다.<br /><br /> 에 대 한 **텍스트** 열의 경우 max_length 값은 됩니다 16 또는 sp_tableoption 'text in row'에서 설정한 값입니다.|  
|전체 자릿수|**tinyint**|숫자 기반일 경우에는 열의 전체 자릿수이고, 그렇지 않으면 0입니다.|  
|소수 자릿수|**tinyint**|숫자 기반일 경우에는 열의 소수 자릿수이고, 그렇지 않으면 0입니다.|  
|collation_name|**sysname**|문자 기반일 경우에는 열의 데이터 정렬 이름이고, 그렇지 않으면 NULL입니다.|  
|is_nullable|**bit**|1 = 열이 Null 값을 허용합니다.|  
|is_ansi_padded|**bit**|1 = 열이 문자, 이진 또는 variant인 경우 ANSI_PADDING ON 동작을 사용합니다.<br /><br /> 0 = 열이 문자, 이진 또는 variant가 아닙니다.|  
|is_rowguidcol|**bit**|1 = 선언된 ROWGUIDCOL 열입니다.|  
|is_identity|**bit**|1 = 열에 ID 값이 있습니다.|  
|is_computed|**bit**|1 = 열이 계산 열입니다.|  
|is_filestream|**bit**|1 = 열이 FILESTREAM 열입니다.|  
|is_replicated|**bit**|1 = 복제된 열입니다.|  
|is_non_sql_subscribed|**bit**|1 = 열에 SQL Server 이외 구독자가 있습니다.|  
|is_merge_published|**bit**|1 = 병합 게시 열입니다.|  
|is_dts_replicated|**bit**|1 = [!INCLUDE[ssIS](../../includes/ssis-md.md)]를 사용해 복제된 열입니다.|  
|is_xml_document|**bit**|1 = 내용이 완전한 XML 문서입니다.<br /><br /> 0 = 내용이 문서 조각 또는 열 데이터 형식이 않습니다 **xml**합니다.|  
|xml_collection_id|**int**|데이터 형식이 열의 경우 0이 아닌 **xml** XML이 입력 하 고 있습니다. 이 값은 열의 유효성 검사 XML 스키마 네임스페이스가 들어 있는 컬렉션의 ID가 됩니다.<br /><br /> 0 = XML 스키마 컬렉션이 없습니다.|  
|default_object_id|**int**|독립 실행형 개체 인지에 관계 없이 기본 개체의 ID [sys.sp_bindefault](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md), 또는 인라인 열 수준 DEFAULT 제약 조건입니다. 인라인 열 수준 기본 개체의 parent_object_id 열은 테이블 자체에 대한 역참조입니다.<br /><br /> 0 = 기본값이 없습니다.|  
|rule_object_id|**int**|sys.sp_bindrule을 사용하여 열에 바인딩된 독립 실행형 규칙의 ID입니다.<br /><br /> 0 = 독립 실행형 규칙이 없습니다. 열 수준 CHECK 제약 조건에 대 한 참조 [sys.check_constraints &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)합니다.|  
|is_sparse|**bit**|1 = 열이 스파스 열입니다. 자세한 내용은 [스파스 열 사용](../../relational-databases/tables/use-sparse-columns.md)을 참조하세요.|  
|is_column_set|**bit**|1 = 열이 열 집합입니다. 자세한 내용은 [스파스 열 사용](../../relational-databases/tables/use-sparse-columns.md)을 참조하세요.|  
|generated_always_type|**tinyint**|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]까지<br /><br /> 열 값이 생성 하는 경우 식별 (항상 0이 됩니다 시스템 테이블의 열에 대 한):<br /><br /> 0 = NOT_APPLICABLE<br /><br /> 1 = AS_ROW_START<br /><br /> 2 = AS_ROW_END<br /><br /> 자세한 내용은 참조 [임시 테이블 &#40;관계형 데이터베이스&#41;](../../relational-databases/tables/temporal-tables.md)합니다.|  
|generated_always_type_desc|**nvarchar(60)**|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]까지<br /><br /> 텍스트 설명 `generated_always_type`의 값 (항상 시스템 테이블의 열에 대해 NOT_APPLICABLE) <br /><br /> NOT_APPLICABLE<br /><br /> AS_ROW_START<br /><br /> AS_ROW_END|  
|encryption_type|**int**|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]까지<br /><br /> 암호화 유형:<br /><br /> 1 = 결정적 암호화<br /><br /> 2 = 임의 암호화|  
|encryption_type_desc|**nvarchar(64)**|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]까지<br /><br /> 암호화 형식이 설명:<br /><br /> 임의<br /><br /> DETERMINISTIC|  
|encryption_algorithm_name|**sysname**|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]까지<br /><br /> 암호화 알고리즘의 이름입니다.<br /><br /> AEAD_AES_256_CBC_HMAC_SHA_512만 지원 됩니다.|  
|column_encryption_key_id|**int**|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]까지<br /><br /> CEK의 ID입니다.|  
|column_encryption_key_database_name|**sysname**|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDW_md](../../includes/sssds-md.md)]까지<br /><br /> 열의 데이터베이스와 다른 경우 열 암호화 키가 존재 하는 위치는 데이터베이스의 이름입니다. 키 열으로 동일한 데이터베이스에 있는 경우 NULL입니다.|  
|is_hidden|**bit**|**적용 대상**: [!INCLUDE[ssCurrentLong](../../includes/sscurrentlong-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]까지<br /><br /> 열이 숨겨져 경우를 나타냅니다.<br /><br /> 0 = 일반, not 숨겨진, 표시 열<br /><br /> 1 = 숨겨진된 열|  
|is_masked|**bit**|**적용 대상**: [!INCLUDE[ssCurrentLong](../../includes/sscurrentlong-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]까지<br /><br /> 동적 데이터 마스킹 하 여 열이 마스킹 경우를 나타냅니다.<br /><br /> 0 = 보통, not 마스크 된 열<br /><br /> 1 = 열이 마스킹|  


 
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 뷰 &#40;Transact SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.all_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys.system_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-columns-transact-sql.md)  
  
  
