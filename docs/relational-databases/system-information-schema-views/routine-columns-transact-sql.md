---
description: ROUTINE_COLUMNS(Transact-SQL)
title: ROUTINE_COLUMNS (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- ROUTINE_COLUMNS_TSQL
- ROUTINE_COLUMNS
dev_langs:
- TSQL
helpviewer_keywords:
- ROUTINE_COLUMNS view
- INFORMATION_SCHEMA.ROUTINE_COLUMNS view
ms.assetid: 91dbc61b-e4c0-4826-976c-b2fce88b7793
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: eb990b9cb78d36bfe680562574eda0688422c7c3
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97462734"
---
# <a name="routine_columns-transact-sql"></a>ROUTINE_COLUMNS(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  현재 데이터베이스에서 현재 사용자가 액세스할 수 있는 테이블 반환 함수에 의해 반환되는 각 열당 한 개의 행을 반환합니다.  
  
 이 뷰에서 정보를 검색 하려면 INFORMATION_SCHEMA의 정규화 된 이름을 지정 합니다 **.** _view_name_.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**nvarchar (** 128 **)**|테이블 반환 함수의 카탈로그 이름 또는 데이터베이스 이름입니다.|  
|**TABLE_SCHEMA**|**nvarchar (** 128 **)**|테이블 반환 함수가 포함된 스키마의 이름입니다.<br /><br /> 중요 개체의 스키마를 확인 하는 데 INFORMATION_SCHEMA 뷰를 사용 하지 마십시오. <strong> \* \* \* \* </strong> INFORMATION_SCHEMA 뷰는 개체의 메타 데이터 하위 집합만을 나타냅니다. 개체의 스키마를 확인하는 신뢰할 수 있는 유일한 방법은 sys.objects 카탈로그 뷰를 쿼리하는 것입니다.|  
|**TABLE_NAME**|**nvarchar (** 128 **)**|테이블 반환 함수의 이름입니다.|  
|**COLUMN_NAME**|**nvarchar (** 128 **)**|열 이름입니다.|  
|**ORDINAL_POSITION**|**int**|열 ID입니다.|  
|**COLUMN_DEFAULT**|**nvarchar (** 4000 **)**|열의 기본값입니다.|  
|**IS_NULLABLE**|**varchar (** 3 **)**|이 열이 NULL을 허용하는 경우 YES를 반환합니다. 그렇지 않은 경우에는 NO를 반환합니다.|  
|**DATA_TYPE**|**nvarchar (** 128 **)**|시스템 제공 데이터 형식입니다.|  
|**CHARACTER_MAXIMUM_LENGTH**|**int**|이진 데이터, 문자 데이터 또는 텍스트와 이미지 데이터의 최대 길이(문자)입니다.<br /><br /> **xml** 및 대량 값 형식 데이터의 경우-1입니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다. 자세한 내용은 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)을 참조하세요.|  
|**CHARACTER_OCTET_LENGTH**|**int**|이진 데이터, 문자 데이터 또는 텍스트와 이미지 데이터의 최대 길이(바이트)입니다.<br /><br /> **xml** 및 대량 값 형식 데이터의 경우-1입니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**NUMERIC_PRECISION**|**tinyint**|근사 숫자 데이터, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터의 전체 자릿수입니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|근사 숫자 데이터, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터의 전체 자릿수 기수입니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**NUMERIC_SCALE**|**tinyint**|근사 숫자 데이터, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터의 소수 자릿수입니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**DATETIME_PRECISION**|**smallint**|**Datetime** 및 ISO **정수** 데이터 형식에 대 한 하위 형식 코드입니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**CHARACTER_SET_CATALOG**|**varchar (** 6 **)**|**Master** 를 반환 합니다. 이 열이 문자 데이터 또는 **텍스트** 데이터 형식인 경우 문자 집합이 있는 데이터베이스를 나타냅니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**CHARACTER_SET_SCHEMA**|**varchar (** 3 **)**|항상 NULL을 반환합니다.|  
|**CHARACTER_SET_NAME**|**nvarchar (** 128 **)**|이 열이 문자 데이터 또는 **텍스트** 데이터 형식이 면 문자 집합의 고유 이름을 반환 합니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**COLLATION_CATALOG**|**varchar (** 6 **)**|항상 NULL을 반환합니다.|  
|**COLLATION_SCHEMA**|**varchar (** 3 **)**|항상 NULL을 반환합니다.|  
|**COLLATION_NAME**|**nvarchar (** 128 **)**|열이 문자 데이터 또는 **텍스트** 데이터 형식인 경우 정렬 순서에 대 한 고유 이름을 반환 합니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**DOMAIN_CATALOG**|**nvarchar (** 128 **)**|열이 별칭 데이터 형식인 경우 이 열은 사용자 정의 데이터 형식이 생성된 데이터베이스 이름이 됩니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**DOMAIN_SCHEMA**|**nvarchar (** 128 **)**|열이 사용자 정의 데이터 형식인 경우 이 열은 사용자 정의 데이터 형식이 포함된 스키마의 이름이 됩니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.<br /><br /> 중요 개체의 스키마를 확인 하는 데 INFORMATION_SCHEMA 뷰를 사용 하지 마십시오. <strong> \* \* \* \* </strong> INFORMATION_SCHEMA 뷰는 개체의 메타 데이터 하위 집합만을 나타냅니다. 개체의 스키마를 확인하는 신뢰할 수 있는 유일한 방법은 sys.objects 카탈로그 뷰를 쿼리하는 것입니다.|  
|**DOMAIN_NAME**|**nvarchar (** 128 **)**|열이 사용자 정의 데이터 형식인 경우 이 열은 사용자 정의 데이터 형식의 이름이 됩니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;시스템 뷰 ](../../t-sql/language-reference.md)   
 [Transact-sql&#41;&#40;정보 스키마 뷰 ](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.objects&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
