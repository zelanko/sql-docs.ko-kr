---
description: PARAMETERS(Transact-SQL)
title: PARAMETERS (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- PARAMETERS_TSQL
- PARAMETERS
dev_langs:
- TSQL
helpviewer_keywords:
- PARAMETERS view
- INFORMATION_SCHEMA.PARAMETERS view
ms.assetid: 06ded0ca-7d21-4400-864a-b801e855b257
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 46360eac7080f92f98ba3f081b7cd9ec505f12c9
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753575"
---
# <a name="parameters-transact-sql"></a>PARAMETERS(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  현재 데이터베이스에서 현재 사용자가 액세스할 수 있는 사용자 정의 함수 또는 저장 프로시저의 각 매개 변수당 한 개의 행을 반환합니다. 함수의 경우에도 이 뷰는 반환 값 정보를 담은 한 행을 반환합니다.  
  
 이러한 뷰에서 정보를 검색 하려면 INFORMATION_SCHEMA의 정규화 된 이름을 지정 합니다 **.** _view_name_.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**SPECIFIC_CATALOG**|**nvarchar (** 128 **)**|매개 변수를 가지는 대상 루틴의 카탈로그 이름입니다.|  
|**SPECIFIC_SCHEMA**|**nvarchar (** 128 **)**|매개 변수를 가지는 대상 루틴의 스키마 이름입니다.<br /><br /> 중요 개체의 스키마를 확인 하는 데 INFORMATION_SCHEMA 뷰를 사용 하지 마십시오. <strong> \* \* \* \* </strong> INFORMATION_SCHEMA 뷰는 개체의 메타 데이터 하위 집합만을 나타냅니다. 개체의 스키마를 확인하는 신뢰할 수 있는 유일한 방법은 sys.objects 카탈로그 뷰를 쿼리하는 것입니다.|  
|**SPECIFIC_NAME**|**nvarchar (** 128 **)**|매개 변수를 가지는 대상 루틴의 이름입니다.|  
|**ORDINAL_POSITION**|**int**|1에서 시작하는 매개 변수의 서수 위치입니다. 함수 반환 값인 경우에는 0입니다.|  
|**PARAMETER_MODE**|**nvarchar (** 10 **)**|입력 매개 변수인 경우에는 IN, 출력 매개 변수인 경우에는 OUT, 입/출력 매개 변수인 경우에는 INOUT을 반환합니다.|  
|**IS_RESULT**|**nvarchar (** 10 **)**|함수인 루틴의 결과를 표시하는 경우에는 YES를 반환합니다. 그렇지 않은 경우에는 NO를 반환합니다.|  
|**AS_LOCATOR**|**nvarchar (** 10 **)**|로케이터로 선언된 경우에는 YES를 반환합니다. 그렇지 않은 경우에는 NO를 반환합니다.|  
|**PARAMETER_NAME**|**nvarchar (** 128 **)**|매개 변수의 이름입니다. 이 이름이 함수의 반환 값에 해당되는 경우에는 NULL이 됩니다.|  
|**DATA_TYPE**|**nvarchar (** 128 **)**|시스템 제공 데이터 형식입니다.|  
|**CHARACTER_MAXIMUM_LENGTH**|**int**|이진 데이터 형식 또는 문자 데이터 형식의 최대 길이를 문자 단위로 표시한 것입니다.<br /><br /> **xml** 및 대량 값 형식 데이터의 경우-1입니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**CHARACTER_OCTET_LENGTH**|**int**|이진 데이터 형식 또는 문자 데이터 형식의 최대 길이를 바이트 단위로 표시한 것입니다.<br /><br /> **xml** 및 대량 값 형식 데이터의 경우-1입니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**COLLATION_CATALOG**|**nvarchar (** 128 **)**|항상 NULL을 반환합니다.|  
|**COLLATION_SCHEMA**|**nvarchar (** 128 **)**|항상 NULL을 반환합니다.|  
|**COLLATION_NAME**|**nvarchar (** 128 **)**|매개 변수의 데이터 정렬 이름입니다. 문자 형식 중 하나가 아닌 경우에는 NULL이 반환됩니다.|  
|**CHARACTER_SET_CATALOG**|**nvarchar (** 128 **)**|매개 변수의 문자 집합 카탈로그 이름입니다. 문자 형식 중 하나가 아닌 경우에는 NULL이 반환됩니다.|  
|**CHARACTER_SET_SCHEMA**|**nvarchar (** 128 **)**|항상 NULL을 반환합니다.|  
|**CHARACTER_SET_NAME**|**nvarchar (** 128 **)**|매개 변수의 문자 집합 이름입니다. 문자 형식 중 하나가 아닌 경우에는 NULL이 반환됩니다.|  
|**NUMERIC_PRECISION**|**tinyint**|근사 숫자 데이터, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터의 전체 자릿수입니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|근사 숫자 데이터, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터의 전체 자릿수 기수입니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**NUMERIC_SCALE**|**tinyint**|근사 숫자 데이터, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터의 소수 자릿수입니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**DATETIME_PRECISION**|**smallint**|매개 변수 형식이 **datetime** 또는 **smalldatetime**인 경우 소수 자릿수 초의 전체 자릿수 (초)입니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**INTERVAL_TYPE**|**nvarchar (** 30 **)**|NULL 나중에 사용하기 위해 예약되어 있습니다.|  
|**INTERVAL_PRECISION**|**smallint**|NULL 나중에 사용하기 위해 예약되어 있습니다.|  
|**USER_DEFINED_TYPE_CATALOG**|**nvarchar (** 128 **)**|NULL 나중에 사용하기 위해 예약되어 있습니다.|  
|**USER_DEFINED_TYPE_SCHEMA**|**nvarchar (** 128 **)**|NULL 나중에 사용하기 위해 예약되어 있습니다.|  
|**USER_DEFINED_TYPE_NAME**|**nvarchar (** 128 **)**|NULL 나중에 사용하기 위해 예약되어 있습니다.|  
|**SCOPE_CATALOG**|**nvarchar (** 128 **)**|NULL 나중에 사용하기 위해 예약되어 있습니다.|  
|**SCOPE_SCHEMA**|**nvarchar (** 128 **)**|NULL 나중에 사용하기 위해 예약되어 있습니다.|  
|**SCOPE_NAME**|**nvarchar (** 128 **)**|NULL 나중에 사용하기 위해 예약되어 있습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;시스템 뷰 ](../../t-sql/language-reference.md)   
 [Transact-sql&#41;&#40;정보 스키마 뷰 ](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.objects&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)  
  
