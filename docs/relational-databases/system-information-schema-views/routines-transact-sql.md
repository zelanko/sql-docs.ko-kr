---
title: 루틴 (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ROUTINES_TSQL
- ROUTINES
dev_langs:
- TSQL
helpviewer_keywords:
- ROUTINES view
- INFORMATION_SCHEMA.ROUTINES view
ms.assetid: c75561b2-c9a1-48a1-9afa-a5896b6454cf
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b4404c25500d6732db6f2346b1fdedb34e9bed8f
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43102020"
---
# <a name="routines-transact-sql"></a>ROUTINES(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  현재 데이터베이스에서 현재 사용자가 액세스할 수 있는 각 저장 프로시저와 함수에 대해 한 행을 반환합니다. 반환 값을 설명하는 열은 함수에만 적용됩니다. 저장 프로시저의 경우 이러한 열은 NULL이 됩니다.  
  
 이러한 뷰에서 정보를 검색 하려면 INFORMATION_SCHEMA의 정규화 된 이름을 지정 합니다. *view_name*합니다.  
  
> [!NOTE]  
>  ROUTINE_DEFINITION 열은 함수 또는 저장 프로시저를 만든 원본 문을 포함합니다. 이러한 원본 문은 중간 캐리지 리턴을 포함하는 경우가 많습니다. 결과를 텍스트 형식으로 표시하는 응용 프로그램에 이 열을 반환하는 경우에는 ROUTINE_DEFINITION 결과의 중간 캐리지 리턴이 전체 결과 집합의 형식에 영향을 줄 수 있습니다. ROUTINE_DEFINITION 열을 선택하는 경우에는 반드시 중간 캐리지 리턴에 맞게 조정해야 합니다. 예를 들어 결과 집합을 표 형태로 반환하거나 ROUTINE_DEFINITION을 자체 입력란 형식으로 반환해야 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|SPECIFIC_CATALOG|**nvarchar(** 128 **)**|카탈로그의 특정 이름입니다. 이 이름은 ROUTINE_CATALOG와 동일합니다.|  
|SPECIFIC_SCHEMA|**nvarchar(** 128 **)**|스키마의 특정 이름입니다.<br /><br /> **\*\* 중요 \* \***  개체의 스키마를 확인 하려면 INFORMATION_SCHEMA 뷰를 사용 하지 마십시오. 개체의 스키마를 확인하는 신뢰할 수 있는 유일한 방법은 sys.objects 카탈로그 뷰를 쿼리하는 것입니다.|  
|SPECIFIC_NAME|**nvarchar(** 128 **)**|카탈로그의 특정 이름입니다. 이 이름은 ROUTINE_NAME과 동일합니다.|  
|ROUTINE_CATALOG|**nvarchar(** 128 **)**|함수의 카탈로그 이름입니다.|  
|ROUTINE_SCHEMA|**nvarchar(** 128 **)**|이 함수를 포함하는 스키마의 이름입니다.<br /><br /> **\*\* 중요 \* \***  개체의 스키마를 확인 하려면 INFORMATION_SCHEMA 뷰를 사용 하지 마십시오. 개체의 스키마를 확인하는 신뢰할 수 있는 유일한 방법은 sys.objects 카탈로그 뷰를 쿼리하는 것입니다.|  
|ROUTINE_NAME|**nvarchar(** 128 **)**|함수의 이름입니다.|  
|ROUTINE_TYPE|**nvarchar (** 20 **)**|저장 프로시저의 경우에는 PROCEDURE를, 함수의 경우에는 FUNCTION을 반환합니다.|  
|MODULE_CATALOG|**nvarchar(** 128 **)**|NULL 나중에 사용하도록 예약되어 있습니다.|  
|MODULE_SCHEMA|**nvarchar(** 128 **)**|NULL 나중에 사용하도록 예약되어 있습니다.|  
|MODULE_NAME|**nvarchar(** 128 **)**|NULL 나중에 사용하도록 예약되어 있습니다.|  
|UDT_CATALOG|**nvarchar(** 128 **)**|NULL 나중에 사용하도록 예약되어 있습니다.|  
|UDT_SCHEMA|**nvarchar(** 128 **)**|NULL 나중에 사용하도록 예약되어 있습니다.|  
|UDT_NAME|**nvarchar(** 128 **)**|NULL 나중에 사용하도록 예약되어 있습니다.|  
|DATA_TYPE|**nvarchar(** 128 **)**|함수 반환 값의 데이터 형식입니다. 반환 **테이블** 경우 테이블 반환 함수입니다.|  
|CHARACTER_MAXIMUM_LENGTH|**int**|반환 형식이 문자 형식인 경우 최대 길이를 문자 단위로 표시한 것입니다.<br /><br /> -1 **xml** 및 큰 값 형식의 데이터입니다.|  
|CHARACTER_OCTET_LENGTH|**int**|반환 형식이 문자 형식인 경우 최대 길이를 바이트 단위로 표시한 것입니다.<br /><br /> -1 **xml** 및 큰 값 형식의 데이터입니다.|  
|COLLATION_CATALOG|**nvarchar(** 128 **)**|항상 NULL을 반환합니다.|  
|COLLATION_SCHEMA|**nvarchar(** 128 **)**|항상 NULL을 반환합니다.|  
|COLLATION_NAME|**nvarchar(** 128 **)**|반환 값의 데이터 정렬 이름입니다. 문자 형식이 아닌 경우에는 NULL을 반환합니다.|  
|CHARACTER_SET_CATALOG|**nvarchar(** 128 **)**|항상 NULL을 반환합니다.|  
|CHARACTER_SET_SCHEMA|**nvarchar(** 128 **)**|항상 NULL을 반환합니다.|  
|CHARACTER_SET_NAME|**nvarchar(** 128 **)**|반환 값 문자 집합의 이름입니다. 문자 형식이 아닌 경우에는 NULL을 반환합니다.|  
|NUMERIC_PRECISION|**smallint**|반환 값의 숫자 전체 자릿수입니다. 숫자 형식이 아닌 경우에는 NULL을 반환합니다.|  
|NUMERIC_PRECISION_RADIX|**smallint**|반환 값의 숫자 전체 자릿수 기수입니다. 문자 형식이 아닌 경우에는 NULL을 반환합니다.|  
|NUMERIC_SCALE|**smallint**|반환 값의 소수 자릿수입니다. 문자 형식이 아닌 경우에는 NULL을 반환합니다.|  
|DATETIME_PRECISION|**smallint**|반환 값 형식인 경우 초의 소수 부분 자릿수 **날짜/시간**합니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|INTERVAL_TYPE|**nvarchar (** 30 **)**|NULL 나중에 사용하도록 예약되어 있습니다.|  
|INTERVAL_PRECISION|**smallint**|NULL 나중에 사용하도록 예약되어 있습니다.|  
|TYPE_UDT_CATALOG|**nvarchar(** 128 **)**|NULL 나중에 사용하도록 예약되어 있습니다.|  
|TYPE_UDT_SCHEMA|**nvarchar(** 128 **)**|NULL 나중에 사용하도록 예약되어 있습니다.|  
|TYPE_UDT_NAME|**nvarchar(** 128 **)**|NULL 나중에 사용하도록 예약되어 있습니다.|  
|SCOPE_CATALOG|**nvarchar(** 128 **)**|NULL 나중에 사용하도록 예약되어 있습니다.|  
|SCOPE_SCHEMA|**nvarchar(** 128 **)**|NULL 나중에 사용하도록 예약되어 있습니다.|  
|SCOPE_NAME|**nvarchar(** 128 **)**|NULL 나중에 사용하도록 예약되어 있습니다.|  
|MAXIMUM_CARDINALITY|**bigint**|NULL 나중에 사용하도록 예약되어 있습니다.|  
|DTD_IDENTIFIER|**nvarchar(** 128 **)**|NULL 나중에 사용하도록 예약되어 있습니다.|  
|ROUTINE_BODY|**nvarchar (** 30 **)**|[!INCLUDE[tsql](../../includes/tsql-md.md)] 함수의 경우에는 SQL을, 외부에서 작성된 함수의 경우에는 EXTERNAL을 반환합니다.<br /><br /> 함수는 항상 SQL이 됩니다.|  
|ROUTINE_DEFINITION|**nvarchar (** 4000 **)**|함수 또는 저장 프로시저가 암호화되지 않은 경우 함수 또는 저장 프로시저의 정의 텍스트 중 처음 4000자를 반환합니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.<br /><br /> 전체 정의 얻었는지 확인, 쿼리를 [OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md) 함수 또는 definition 열을 [sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) 카탈로그 뷰.|  
|EXTERNAL_NAME|**nvarchar(** 128 **)**|NULL 나중에 사용하도록 예약되어 있습니다.|  
|EXTERNAL_LANGUAGE|**nvarchar (** 30 **)**|NULL 나중에 사용하도록 예약되어 있습니다.|  
|PARAMETER_STYLE|**nvarchar (** 30 **)**|NULL 나중에 사용하도록 예약되어 있습니다.|  
|IS_DETERMINISTIC|**nvarchar (** 10 **)**|루틴이 확정적인 경우에는 YES를 반환합니다.<br /><br /> 루틴이 확정적이지 않은 경우에는 NO를 반환합니다.<br /><br /> 저장 프로시저에 대해서는 항상 NO를 반환합니다.|  
|SQL_DATA_ACCESS|**nvarchar (** 30 **)**|다음 값 중 하나를 반환합니다.<br /><br /> NONE = 함수에 SQL이 포함되어 있지 않습니다.<br /><br /> CONTAINS = 함수에 SQL이 포함되어 있을 수 있습니다.<br /><br /> READS = 함수가 SQL 데이터를 읽을 수 있습니다.<br /><br /> MODIFIES = 함수가 SQL 데이터를 수정할 수 있습니다.<br /><br /> 모든 함수의 경우에는 READS를, 모든 저장 프로시저의 경우에는 MODIFIES를 반환합니다.|  
|IS_NULL_CALL|**nvarchar (** 10 **)**|인수 중 하나가 NULL인 경우 루틴을 호출할 것인지 여부를 표시합니다.|  
|SQL_PATH|**nvarchar(** 128 **)**|NULL 나중에 사용하도록 예약되어 있습니다.|  
|SCHEMA_LEVEL_ROUTINE|**nvarchar (** 10 **)**|스키마 수준의 함수인 경우에는 YES를, 스키마 수준의 함수가 아닌 경우에는 NO를 반환합니다.<br /><br /> 항상 YES를 반환합니다.|  
|MAX_DYNAMIC_RESULT_SETS|**smallint**|루틴에 의해 반환되는 동적 결과 집합의 최대 수입니다.<br /><br /> 함수의 경우에는 0을 반환합니다.|  
|IS_USER_DEFINED_CAST|**nvarchar (** 10 **)**|사용자 정의 캐스트 함수인 경우에는 YES를, 사용자 정의 캐스트 함수가 아닌 경우에는 NO를 반환합니다.<br /><br /> 항상 NO를 반환합니다.|  
|IS_IMPLICITLY_INVOCABLE|**nvarchar (** 10 **)**|루틴을 암시적으로 호출할 수 있는 경우에는 YES를, 함수를 암시적으로 호출할 수 없는 경우에는 NO를 반환합니다.<br /><br /> 항상 NO를 반환합니다.|  
|CREATED|**datetime**|루틴이 만들어진 시간입니다.|  
|LAST_ALTERED|**datetime**|함수를 마지막으로 수정한 시간입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [시스템 뷰 &#40;TRANSACT-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [정보 스키마 뷰 &#40;TRANSACT-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.objects&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.procedures&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-procedures-transact-sql.md)   
 [sys.sql_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)  
  
  
