---
description: COLUMNS(Transact-SQL)
title: COLUMNS (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- COLUMNS
- COLUMNS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- COLUMNS view
- INFORMATION_SCHEMA.COLUMNS view
ms.assetid: bbf7ac4a-7444-4351-a590-a9f71e0bc495
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f4f49fe215279782a5f2e8df8fe501e0619f4bd2
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753638"
---
# <a name="columns-transact-sql"></a>COLUMNS(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  현재 데이터베이스에서 현재 사용자가 액세스할 수 있는 열마다 한 행을 반환합니다.  
  
 이러한 뷰에서 정보를 검색 하려면 **INFORMATION_SCHEMA**_.view_name_의 정규화 된 이름을 지정 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**nvarchar (** 128 **)**|테이블 한정자입니다.|  
|**TABLE_SCHEMA**|**nvarchar (** 128 **)**|테이블이 포함된 스키마의 이름입니다.<br /><br /> **&#42;&#42; 중요 &#42;&#42;** INFORMATION_SCHEMA 뷰를 사용 하 여 개체의 스키마를 확인 하지 마십시오. INFORMATION_SCHEMA 뷰는 개체의 메타 데이터 하위 집합만을 나타냅니다. 개체의 스키마를 확인하는 신뢰할 수 있는 유일한 방법은 sys.objects 카탈로그 뷰를 쿼리하는 것입니다.|  
|**TABLE_NAME**|**nvarchar (** 128 **)**|테이블 이름입니다.|  
|**COLUMN_NAME**|**nvarchar (** 128 **)**|열 이름입니다.|  
|**ORDINAL_POSITION**|**int**|열 ID입니다.|  
|**COLUMN_DEFAULT**|**nvarchar (** 4000 **)**|열의 기본값입니다.|  
|**IS_NULLABLE**|**varchar (** 3 **)**|열의 NULL 허용 여부입니다. 열이 NULL을 허용하는 경우에는 이 열이 YES를 반환하고 허용하지 않는 경우에는 NO가 반환됩니다.|  
|**DATA_TYPE**|**nvarchar (** 128 **)**|시스템 제공 데이터 형식입니다.|  
|**CHARACTER_MAXIMUM_LENGTH**|**int**|이진 데이터, 문자 데이터 또는 텍스트와 이미지 데이터의 최대 길이(문자)입니다.<br /><br /> **xml** 및 대량 값 형식 데이터의 경우-1입니다. 다른 데이터 형식에 대해서는 NULL이 반환됩니다. 자세한 내용은 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)을 참조하세요.|  
|**CHARACTER_OCTET_LENGTH**|**int**|이진 데이터, 문자 데이터 또는 텍스트와 이미지 데이터의 최대 길이(바이트)입니다.<br /><br /> **xml** 및 대량 값 형식 데이터의 경우-1입니다. 다른 데이터 형식에 대해서는 NULL이 반환됩니다.|  
|**NUMERIC_PRECISION**|**tinyint**|근사 숫자 데이터, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터의 전체 자릿수입니다. 다른 데이터 형식에 대해서는 NULL이 반환됩니다.|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|근사 숫자 데이터, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터의 전체 자릿수 기수입니다. 다른 데이터 형식에 대해서는 NULL이 반환됩니다.|  
|**NUMERIC_SCALE**|**int**|근사 숫자 데이터, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터의 소수 자릿수입니다. 다른 데이터 형식에 대해서는 NULL이 반환됩니다.|  
|**DATETIME_PRECISION**|**smallint**|**Datetime** 및 ISO **interval** 데이터 형식에 대 한 하위 형식 코드입니다. 다른 데이터 형식에 대해서는 NULL이 반환됩니다.|  
|**CHARACTER_SET_CATALOG**|**nvarchar (** 128 **)**|**Master**를 반환 합니다. 이 열이 문자 데이터 또는 **텍스트** 데이터 형식인 경우 문자 집합이 있는 데이터베이스를 나타냅니다. 다른 데이터 형식에 대해서는 NULL이 반환됩니다.|  
|**CHARACTER_SET_SCHEMA**|**nvarchar (** 128 **)**|항상 NULL을 반환합니다.|  
|**CHARACTER_SET_NAME**|**nvarchar (** 128 **)**|이 열이 문자 데이터 또는 **텍스트** 데이터 형식이 면 문자 집합의 고유 이름을 반환 합니다. 다른 데이터 형식에 대해서는 NULL이 반환됩니다.|  
|**COLLATION_CATALOG**|**nvarchar (** 128 **)**|항상 NULL을 반환합니다.|  
|**COLLATION_SCHEMA**|**nvarchar (** 128 **)**|항상 NULL을 반환합니다.|  
|**COLLATION_NAME**|**nvarchar (** 128 **)**|열이 문자 데이터 또는 **텍스트** 데이터 형식인 경우 데이터 정렬의 고유 이름을 반환 합니다. 다른 데이터 형식에 대해서는 NULL이 반환됩니다.|  
|**DOMAIN_CATALOG**|**nvarchar (** 128 **)**|열이 별칭 데이터 형식인 경우 이 열은 사용자 정의 데이터 형식이 생성된 데이터베이스 이름이 됩니다. 다른 데이터 형식에 대해서는 NULL이 반환됩니다.|  
|**DOMAIN_SCHEMA**|**nvarchar (** 128 **)**|열이 사용자 정의 데이터 형식인 경우 이 열은 사용자 정의 데이터 형식의 스키마 이름을 반환합니다. 다른 데이터 형식에 대해서는 NULL이 반환됩니다.<br /><br /> **&#42;&#42; 중요 &#42;&#42;** INFORMATION_SCHEMA 뷰를 사용 하 여 데이터 형식의 스키마를 확인 하지 마십시오. 형식의 스키마를 확인하는 신뢰할 수 있는 유일한 방법은 TYPEPROPERTY 함수를 사용하는 것입니다.|  
|**DOMAIN_NAME**|**nvarchar (** 128 **)**|열이 사용자 정의 데이터 형식인 경우 이 열은 사용자 정의 데이터 형식의 이름이 됩니다. 다른 데이터 형식에 대해서는 NULL이 반환됩니다.|  
  
## <a name="remarks"></a>설명  
 INFORMATION_SCHEMA의 **ORDINAL_POSITION** 열 **입니다. 열** 뷰는 COLUMNS_UPDATED 함수에서 반환 된 열의 비트 패턴과 호환 되지 않습니다. COLUMNS_UPDATED와 호환 되는 비트 패턴을 얻으려면 INFORMATION_SCHEMA를 쿼리할 때 COLUMNPROPERTY 시스템 함수의 **ColumnID** 속성을 참조 해야 합니다 **. 열** 뷰입니다. 예를 들면 다음과 같습니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT TABLE_NAME, COLUMN_NAME, COLUMNPROPERTY(OBJECT_ID(TABLE_SCHEMA + '.' + TABLE_NAME), COLUMN_NAME, 'ColumnID') AS COLUMN_ID  
FROM AdventureWorks2012.INFORMATION_SCHEMA.COLUMNS  
WHERE TABLE_NAME = 'Person';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;시스템 뷰 ](../../t-sql/language-reference.md)   
 [Transact-sql&#41;&#40;정보 스키마 뷰 ](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.sys문자 집합 &#40;transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)   
 [sys.columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.sql_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.configurations&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [sys.objects&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.types&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)   
 [COLUMNS_UPDATED&#40;Transact-SQL&#41;](../../t-sql/functions/columns-updated-transact-sql.md)  
  
