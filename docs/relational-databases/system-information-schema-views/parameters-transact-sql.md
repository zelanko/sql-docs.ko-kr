---
title: 매개 변수 (Transact SQL) | Microsoft Docs
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
- PARAMETERS_TSQL
- PARAMETERS
dev_langs:
- TSQL
helpviewer_keywords:
- PARAMETERS view
- INFORMATION_SCHEMA.PARAMETERS view
ms.assetid: 06ded0ca-7d21-4400-864a-b801e855b257
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 9b73215f275f2171f72a70a71f1855d88d60c034
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33238510"
---
# <a name="parameters-transact-sql"></a>PARAMETERS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  현재 데이터베이스에서 현재 사용자가 액세스할 수 있는 사용자 정의 함수 또는 저장 프로시저의 각 매개 변수당 한 개의 행을 반환합니다. 함수의 경우에도 이 뷰는 반환 값 정보를 담은 한 행을 반환합니다.  
  
 이러한 뷰에서 정보를 검색 하려면의 정규화 된 이름을 지정 **INFORMATION_SCHEMA. * * * view_name*합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**SPECIFIC_CATALOG**|**nvarchar(** 128 **)**|매개 변수를 가지는 대상 루틴의 카탈로그 이름입니다.|  
|**SPECIFIC_SCHEMA**|**nvarchar(** 128 **)**|매개 변수를 가지는 대상 루틴의 스키마 이름입니다.<br /><br /> **\*\* 중요 한 \* \***  개체의 스키마를 확인 하려면 INFORMATION_SCHEMA 뷰를 사용 하지 마십시오. 개체의 스키마를 확인하는 신뢰할 수 있는 유일한 방법은 sys.objects 카탈로그 뷰를 쿼리하는 것입니다.|  
|**SPECIFIC_NAME 순으로**|**nvarchar(** 128 **)**|매개 변수를 가지는 대상 루틴의 이름입니다.|  
|**ORDINAL_POSITION**|**int**|1에서 시작하는 매개 변수의 서수 위치입니다. 함수 반환 값인 경우에는 0입니다.|  
|**PARAMETER_MODE**|**nvarchar (** 10 **)**|입력 매개 변수인 경우에는 IN, 출력 매개 변수인 경우에는 OUT, 입/출력 매개 변수인 경우에는 INOUT을 반환합니다.|  
|**IS_RESULT**|**nvarchar (** 10 **)**|함수인 루틴의 결과를 표시하는 경우에는 YES를 반환합니다. 그렇지 않은 경우에는 NO를 반환합니다.|  
|**AS_LOCATOR**|**nvarchar (** 10 **)**|로케이터로 선언된 경우에는 YES를 반환합니다. 그렇지 않은 경우에는 NO를 반환합니다.|  
|**P A R A**|**nvarchar(** 128 **)**|매개 변수의 이름입니다. 이 이름이 함수의 반환 값에 해당되는 경우에는 NULL이 됩니다.|  
|**DATA_TYPE**|**nvarchar(** 128 **)**|시스템 제공 데이터 형식입니다.|  
|**때**|**int**|이진 데이터 형식 또는 문자 데이터 형식의 최대 길이를 문자 단위로 표시한 것입니다.<br /><br /> 에 대 한-1 **xml** 및 큰 값 형식의 데이터입니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**CHARACTER_OCTET_LENGTH**|**int**|이진 데이터 형식 또는 문자 데이터 형식의 최대 길이를 바이트 단위로 표시한 것입니다.<br /><br /> 에 대 한-1 **xml** 및 큰 값 형식의 데이터입니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**COLLATION_CATALOG**|**nvarchar(** 128 **)**|항상 NULL을 반환합니다.|  
|**COLLATION_SCHEMA**|**nvarchar(** 128 **)**|항상 NULL을 반환합니다.|  
|**데이터 정렬 이름**|**nvarchar(** 128 **)**|매개 변수의 데이터 정렬 이름입니다. 문자 형식 중 하나가 아닌 경우에는 NULL이 반환됩니다.|  
|**CHARACTER_SET_CATALOG**|**nvarchar(** 128 **)**|매개 변수의 문자 집합 카탈로그 이름입니다. 문자 형식 중 하나가 아닌 경우에는 NULL이 반환됩니다.|  
|**CHARACTER_SET_SCHEMA**|**nvarchar(** 128 **)**|항상 NULL을 반환합니다.|  
|**CHARACTER_SET_NAME**|**nvarchar(** 128 **)**|매개 변수의 문자 집합 이름입니다. 문자 형식 중 하나가 아닌 경우에는 NULL이 반환됩니다.|  
|**NUMERIC_PRECISION**|**tinyint**|근사 숫자 데이터, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터의 전체 자릿수입니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|근사 숫자 데이터, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터의 전체 자릿수 기수입니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**NUMERIC_SCALE**|**tinyint**|근사 숫자 데이터, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터의 소수 자릿수입니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**DATETIME_PRECISION**|**smallint**|에 매개 변수 형식이 경우 소수 자릿수 초의 전체 자릿수를 **datetime** 또는 **smalldatetime**합니다. 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|**INTERVAL_TYPE**|**nvarchar (** 30 **)**|NULL 나중에 사용하도록 예약되어 있습니다.|  
|**INTERVAL_PRECISION**|**smallint**|NULL 나중에 사용하도록 예약되어 있습니다.|  
|**USER_DEFINED_TYPE_CATALOG**|**nvarchar(** 128 **)**|NULL 나중에 사용하도록 예약되어 있습니다.|  
|**USER_DEFINED_TYPE_SCHEMA**|**nvarchar(** 128 **)**|NULL 나중에 사용하도록 예약되어 있습니다.|  
|**USER_DEFINED_TYPE_NAME**|**nvarchar(** 128 **)**|NULL 나중에 사용하도록 예약되어 있습니다.|  
|**SCOPE_CATALOG**|**nvarchar(** 128 **)**|NULL 나중에 사용하도록 예약되어 있습니다.|  
|**SCOPE_SCHEMA**|**nvarchar(** 128 **)**|NULL 나중에 사용하도록 예약되어 있습니다.|  
|**SCOPE_NAME**|**nvarchar(** 128 **)**|NULL 나중에 사용하도록 예약되어 있습니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 뷰 &#40;Transact SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [정보 스키마 뷰 &#40;Transact SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.objects&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.parameters& #40; Transact SQL & #41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)  
  
  
