---
description: sys.columns(Transact-SQL)
title: sys. columns (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 11/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9a2d25739eaf041a5c69b52b8c0ce27dc56cde89
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477534"
---
# <a name="syscolumns-transact-sql"></a>sys.columns(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

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
|user_type_id|**int**|열의 유형에 대한 사용자 정의 ID입니다.<br /><br /> 형식의 이름을 반환 하려면이 열에 대 한 [sys. types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) 카탈로그 뷰에 조인 합니다.|  
|max_length|**smallint**|열의 최대 길이(바이트)입니다.<br /><br /> -1 = 열 데이터 형식이 **varchar (max)**, **nvarchar (max)**, **varbinary (max)** 또는 **xml** 입니다.<br /><br /> **텍스트** 열의 경우 max_length 값은 16 이거나 ' text in row ' sp_tableoption 값으로 설정 됩니다.|  
|정밀도|**tinyint**|숫자 기반일 경우에는 열의 전체 자릿수이고, 그렇지 않으면 0입니다.|  
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
|is_xml_document|**bit**|1 = 내용이 완전한 XML 문서입니다.<br /><br /> 0 = 내용이 문서 조각 이거나 열 데이터 형식이 **xml** 이 아닙니다.|  
|xml_collection_id|**int**|열의 데이터 형식이 **xml** 이 고 xml이 입력 된 경우 0이 아닌 값입니다. 이 값은 열의 유효성 검사 XML 스키마 네임스페이스가 들어 있는 컬렉션의 ID가 됩니다.<br /><br /> 0 = XML 스키마 컬렉션이 없습니다.|  
|default_object_id|**int**|독립 실행형 개체 [sys.sp_bindefault](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)인지 또는 인라인 열 수준 기본 제약 조건에 관계 없이 기본 개체의 ID입니다. 인라인 열 수준 기본 개체의 parent_object_id 열은 테이블 자체에 대한 역참조입니다.<br /><br /> 0 = 기본값이 없습니다.|  
|rule_object_id|**int**|sys.sp_bindrule을 사용하여 열에 바인딩된 독립 실행형 규칙의 ID입니다.<br /><br /> 0 = 독립 실행형 규칙이 없습니다. 열 수준 CHECK 제약 조건에 대해서는 [sys.check_constraints &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)을 참조 하십시오.|  
|is_sparse|**bit**|1 = 열이 스파스 열입니다. 자세한 내용은 [스파스 열 사용](../../relational-databases/tables/use-sparse-columns.md)을 참조하세요.|  
|is_column_set|**bit**|1 = 열이 열 집합입니다. 자세한 내용은 [스파스 열 사용](../../relational-databases/tables/use-sparse-columns.md)을 참조하세요.|  
|generated_always_type|**tinyint**|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상, [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> 열 값이 생성 되는 시기를 식별 합니다. 시스템 테이블의 열에 대해서는 항상 0입니다.<br /><br /> 0 = NOT_APPLICABLE<br /><br /> 1 = AS_ROW_START<br /><br /> 2 = AS_ROW_END<br /><br /> 자세한 내용은 [Temporal Tables &#40;관계형 데이터베이스&#41;](../../relational-databases/tables/temporal-tables.md)를 참조 하세요.|  
|generated_always_type_desc|**nvarchar(60)**|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상, [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> 의 값에 대 한 텍스트 설명 `generated_always_type` (시스템 테이블의 열에 대해 항상 NOT_APPLICABLE) <br /><br /> NOT_APPLICABLE<br /><br /> AS_ROW_START<br /><br /> AS_ROW_END|  
|encryption_type|**int**|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상, [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> 암호화 유형:<br /><br /> 1 = 결정적 암호화<br /><br /> 2 = 임의 암호화|  
|encryption_type_desc|**nvarchar (64)**|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상, [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> 암호화 유형 설명:<br /><br /> 임의<br /><br /> DETERMINISTIC|  
|encryption_algorithm_name|**sysname**|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상, [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> 암호화 알고리즘의 이름입니다.<br /><br /> AEAD_AES_256_CBC_HMAC_SHA_512만 지원 됩니다.|  
|column_encryption_key_id|**int**|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상, [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> CEK의 ID입니다.|  
|column_encryption_key_database_name|**sysname**|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상, [!INCLUDE[ssSDW_md](../../includes/sssds-md.md)].<br /><br /> 열의 데이터베이스와 다른 경우 열 암호화 키가 있는 데이터베이스의 이름입니다. 키가 열과 동일한 데이터베이스에 있으면 NULL입니다.|  
|is_hidden|**bit**|**적용 대상**: [!INCLUDE[ssCurrentLong](../../includes/sscurrent-md.md)] 이상, [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> 열이 숨겨져 있는지 여부를 나타냅니다.<br /><br /> 0 = 일반, 숨김, 표시 열<br /><br /> 1 = 숨겨진 열|  
|is_masked|**bit**|**적용 대상**: [!INCLUDE[ssCurrentLong](../../includes/sscurrent-md.md)] 이상, [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> 열이 동적 데이터 마스킹에 의해 마스킹 되는지 여부를 나타냅니다.<br /><br /> 0 = 일반, 마스크 되지 않은 열<br /><br /> 1 = 열이 마스킹 됨|  


 
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;시스템 뷰 ](../../t-sql/language-reference.md)   
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [Transact-sql&#41;sys.all_columns &#40;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [ Transact-sql&#41;&#40;tem_columnssys.sys](../../relational-databases/system-catalog-views/sys-system-columns-transact-sql.md)  
  
