---
title: 도메인 (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DOMAINS_TSQL
- DOMAINS
dev_langs:
- TSQL
helpviewer_keywords:
- DOMAINS view
- INFORMATION_SCHEMA.DOMAINS view
ms.assetid: f0b734d5-816f-4b10-a60c-615931b515c2
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: aeb6597d9f2969c9e06effa78752b6363fe91c51
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47599991"
---
# <a name="domains-transact-sql"></a>DOMAINS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 데이터베이스에서 현재 사용자가 액세스할 수 있는 각 별칭 데이터 형식에 대해 행 하나를 반환합니다.  
  
 이러한 뷰에서 정보를 검색할의 정규화 된 이름을 지정 **INFORMATION_SCHEMA. * * * view_name*합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**DOMAIN_CATALOG**|**nvarchar(** 128 **)**|별칭 데이터 형식이 존재하는 데이터베이스입니다.|  
|**DOMAIN_SCHEMA**|**nvarchar(** 128 **)**|별칭 데이터 형식이 들어 있는 스키마의 이름입니다.<br /><br /> **\*\* 중요 \* \***  데이터 형식의 스키마를 확인할 INFORMATION_SCHEMA 뷰를 사용 하지 마십시오. 형식의 스키마를 확인하는 신뢰할 수 있는 유일한 방법은 TYPEPROPERTY 함수를 사용하는 것입니다.|  
|**DOMAIN_NAME**|**sysname**|별칭 데이터 형식입니다.|  
|**DATA_TYPE**|**sysname**|시스템 제공 데이터 형식입니다.|  
|**때**|**int**|이진 데이터, 문자 데이터 또는 텍스트와 이미지 데이터의 최대 길이(문자)입니다.<br /><br /> -1 **xml** 및 큰 값 형식의 데이터입니다. 다른 데이터 형식에 대해서는 NULL이 반환됩니다. 자세한 내용은 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)을 참조하세요.|  
|**CHARACTER_OCTET_LENGTH**|**int**|이진 데이터, 문자 데이터 또는 텍스트와 이미지 데이터의 최대 길이(바이트)입니다.<br /><br /> -1 **xml** 및 큰 값 형식의 데이터입니다. 다른 데이터 형식에 대해서는 NULL이 반환됩니다.|  
|**COLLATION_CATALOG**|**varchar (** 6 **)**|항상 NULL을 반환합니다.|  
|**COLLATION_SCHEMA**|**varchar (** 3 **)**|항상 NULL을 반환합니다.|  
|**데이터 정렬 이름**|**nvarchar(** 128 **)**|열이 문자 데이터 정렬에 대 한 고유 이름을 반환 하거나 **텍스트** 데이터 형식입니다. 다른 데이터 형식에 대해서는 NULL이 반환됩니다.|  
|**CHARACTER_SET_CATALOG**|**varchar (** 6 **)**|반환 **마스터**합니다. 이 이면 문자 집합이 있는 데이터베이스는 열이 문자 데이터 나 **텍스트** 데이터 형식입니다. 다른 데이터 형식에 대해서는 NULL이 반환됩니다.|  
|**CHARACTER_SET_SCHEMA**|**varchar (** 3 **)**|항상 NULL을 반환합니다.|  
|**CHARACTER_SET_NAME**|**nvarchar(** 128 **)**|이 열이 문자 데이터를 설정 하는 문자에 대 한 고유 이름을 반환 하거나 **텍스트** 데이터 형식입니다. 다른 데이터 형식에 대해서는 NULL이 반환됩니다.|  
|**NUMERIC_PRECISION**|**tinyint**|근사 숫자 데이터, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터의 전체 자릿수입니다. 다른 데이터 형식에 대해서는 NULL이 반환됩니다.|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|근사 숫자 데이터, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터의 전체 자릿수 기수입니다. 다른 데이터 형식에 대해서는 NULL이 반환됩니다.|  
|**NUMERIC_SCALE**|**tinyint**|근사 숫자 데이터, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터의 소수 자릿수입니다. 다른 데이터 형식에 대해서는 NULL이 반환됩니다.|  
|**DATETIME_PRECISION 에서처럼**|**smallint**|하위 형식 코드입니다 **날짜/시간** 및 ISO **간격** 데이터 형식입니다. 다른 데이터 형식에 대해서는 이 열이 NULL을 반환합니다.|  
|**DOMAIN_DEFAULT**|**nvarchar (** 4000 **)**|[!INCLUDE[tsql](../../includes/tsql-md.md)] 정의 문의 실제 텍스트입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [시스템 뷰 &#40;TRANSACT-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [정보 스키마 뷰 &#40;TRANSACT-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.syscharsets &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)   
 [sys.sql_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.configurations&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [sys.types&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)  
  
  
