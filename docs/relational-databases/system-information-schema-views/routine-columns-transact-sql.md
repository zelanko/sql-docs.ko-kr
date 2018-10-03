---
title: ROUTINE_COLUMNS (TRANSACT-SQL) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a64a34e0b127aba39b1fe38d7f42bd61c72ea411
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47815071"
---
# <a name="routinecolumns-transact-sql"></a>ROUTINE_COLUMNS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 데이터베이스에서 현재 사용자가 액세스할 수 있는 테이블 반환 함수에 의해 반환되는 각 열당 한 개의 행을 반환합니다.  
  
 이 뷰에서 정보를 검색할의 정규화 된 이름을 지정 **INFORMATION_SCHEMA. * * * view_name*합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**nvarchar(** 128 **)**|테이블 반환 함수의 카탈로그 이름 또는 데이터베이스 이름입니다.|  
|**TABLE_SCHEMA**|**nvarchar(** 128 **)**|테이블 반환 함수가 포함된 스키마의 이름입니다.<br /><br /> **\*\* 중요 \* \***  개체의 스키마를 확인 하려면 INFORMATION_SCHEMA 뷰를 사용 하지 마십시오. 개체의 스키마를 확인하는 신뢰할 수 있는 유일한 방법은 sys.objects 카탈로그 뷰를 쿼리하는 것입니다.|  
|**TABLE_NAME**|**nvarchar(** 128 **)**|테이블 반환 함수의 이름입니다.|  
|**COLUMN_NAME**|**nvarchar(** 128 **)**|열 이름입니다.|  
|**ORDINAL_POSITION**|**int**|열 ID입니다.|  
|**COLUMN_DEFAULT**|**nvarchar (** 4000 **)**|열의 기본값입니다.|  
|**IS_NULLABLE**|**varchar (** 3 **)**|이 열이 NULL을 허용하는 경우 YES를 반환합니다. 그렇지 않은 경우에는 NO를 반환합니다.|  
|**DATA_TYPE**|**nvarchar(** 128 **)**|시스템 제공 데이터 형식입니다.|  
|**때**|**int**|이진 데이터, 문자 데이터 또는 텍스트와 이미지 데이터의 최대 길이(문자)입니다.<br /><br /> -1 **xml** 및 큰 값 형식의 데이터입니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다. 자세한 내용은 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)을 참조하세요.|  
|**CHARACTER_OCTET_LENGTH**|**int**|이진 데이터, 문자 데이터 또는 텍스트와 이미지 데이터의 최대 길이(바이트)입니다.<br /><br /> -1 **xml** 및 큰 값 형식의 데이터입니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**NUMERIC_PRECISION**|**tinyint**|근사 숫자 데이터, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터의 전체 자릿수입니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|근사 숫자 데이터, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터의 전체 자릿수 기수입니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**NUMERIC_SCALE**|**tinyint**|근사 숫자 데이터, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터의 소수 자릿수입니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**DATETIME_PRECISION 에서처럼**|**smallint**|하위 형식 코드입니다 **날짜/시간** 및 ISO**정수** 데이터 형식입니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**CHARACTER_SET_CATALOG**|**varchar (** 6 **)**|반환 **마스터**합니다. 이 데이터베이스 나타냅니다는 문자 집합을 찾을 열이 문자 데이터 또는 **텍스트** 데이터 형식입니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**CHARACTER_SET_SCHEMA**|**varchar (** 3 **)**|항상 NULL을 반환합니다.|  
|**CHARACTER_SET_NAME**|**nvarchar(** 128 **)**|이 열이 문자 데이터를 설정 하는 문자에 대 한 고유 이름을 반환 하거나 **텍스트** 데이터 형식입니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**COLLATION_CATALOG**|**varchar (** 6 **)**|항상 NULL을 반환합니다.|  
|**COLLATION_SCHEMA**|**varchar (** 3 **)**|항상 NULL을 반환합니다.|  
|**데이터 정렬 이름**|**nvarchar(** 128 **)**|열이 문자 데이터 정렬에 대 한 고유 이름을 반환 하거나 **텍스트** 데이터 형식입니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**DOMAIN_CATALOG**|**nvarchar(** 128 **)**|열이 별칭 데이터 형식인 경우 이 열은 사용자 정의 데이터 형식이 생성된 데이터베이스 이름이 됩니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**DOMAIN_SCHEMA**|**nvarchar(** 128 **)**|열이 사용자 정의 데이터 형식인 경우 이 열은 사용자 정의 데이터 형식이 포함된 스키마의 이름이 됩니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.<br /><br /> **\*\* 중요 \* \***  개체의 스키마를 확인 하려면 INFORMATION_SCHEMA 뷰를 사용 하지 마십시오. 개체의 스키마를 확인하는 신뢰할 수 있는 유일한 방법은 sys.objects 카탈로그 뷰를 쿼리하는 것입니다.|  
|**DOMAIN_NAME**|**nvarchar(** 128 **)**|열이 사용자 정의 데이터 형식인 경우 이 열은 사용자 정의 데이터 형식의 이름이 됩니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [시스템 뷰 &#40;TRANSACT-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [정보 스키마 뷰 &#40;TRANSACT-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  
