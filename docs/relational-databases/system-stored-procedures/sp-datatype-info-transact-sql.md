---
title: sp_datatype_info (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/25/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_datatype_info_TSQL
- sp_datatype_info
dev_langs:
- TSQL
helpviewer_keywords:
- sp_datatype_info
ms.assetid: 045f3b5d-6bb7-4748-8b4c-8deb4bc44147
author: stevestein
ms.author: sstein
ms.openlocfilehash: 39e8f688c23cffb1512be1cd1142d38c010668a7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108300"
---
# <a name="spdatatypeinfo-transact-sql"></a>sp_datatype_info(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  현재 환경에서 지원되는 데이터 형식에 대한 정보를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_datatype_info [ [ @data_type = ] data_type ]   
     [ , [ @ODBCVer = ] odbc_version ]   
```  
  
## <a name="arguments"></a>인수  
`[ @data_type = ] data_type` 지정된 된 데이터 형식에 대 한 코드입니다. 모든 데이터 형식의 목록을 가져오려면 이 매개 변수를 생략하세요. *data_type* 됩니다 **int**, 기본값은 0입니다.  
  
`[ @ODBCVer = ] odbc_version` 사용 되는 ODBC의 버전이입니다. *odbc_version* 됩니다 **tinyint**, 기본값은 2입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 없음  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|TYPE_NAME|**sysname**|DBMS에 종속된 데이터 형식입니다.|  
|DATA_TYPE|**smallint**|ODBC 형식의 열이 모두 매핑되는 해당 형식의 코드입니다.|  
|PRECISION|**int**|데이터 원본에 있는 데이터 형식의 최대 전체 자릿수입니다. 전체 자릿수가 적용되지 않는 데이터 형식에 대해서는 NULL이 반환됩니다. PRECISION 열의 값은 10진수로 반환됩니다.|  
|LITERAL_PREFIX|**varchar(** 32 **)**|상수 앞에 사용되는 문자 또는 문자열입니다. 예를 들어, 작은따옴표 ( **'** ) 형식 문자 및 이진 0 x에 대 한 합니다.|  
|LITERAL_SUFFIX|**varchar(** 32 **)**|상수 끝에 사용되는 문자 또는 문자열입니다. 예를 들어, 작은따옴표 ( **'** ) 형식 문자 및 이진 따옴표가 사용 되지 않습니다.|  
|CREATE_PARAMS|**varchar(** 32 **)**|해당 데이터 형식에 대한 매개 변수 만들기에 대한 설명입니다. 예를 들어 **10 진수** 은 "precision, scale" **float** 가 null 인 경우 및 **varchar** 는 "max_length"입니다.|  
|NULLABLE|**smallint**|NULL 허용 여부를 지정합니다.<br /><br /> 1 = NULL 값을 허용합니다.<br /><br /> 0 = NULL 값을 허용하지 않습니다.|  
|CASE_SENSITIVE|**smallint**|대/소문자 구분 여부를 지정합니다.<br /><br /> 1 = 이 형식의 열은 모두 데이터 정렬 시 대/소문자를 구분합니다.<br /><br /> 0 = 이 형식의 열은 모두 대/소문자를 구분하지 않습니다.|  
|SEARCHABLE|**smallint**|열 형식에 대한 검색 기능을 지정합니다.<br /><br /> 1 = 검색할 수 없습니다.<br /><br /> 2 = LIKE를 사용하여 검색할 수 있습니다.<br /><br /> 3 = WHERE를 사용하여 검색할 수 있습니다.<br /><br /> 4 = WHERE 또는 LIKE를 사용하여 검색할 수 있습니다.|  
|UNSIGNED_ATTRIBUTE|**smallint**|데이터 형식의 서명 여부를 지정합니다.<br /><br /> 1 = 서명되지 않은 데이터 형식입니다.<br /><br /> 0 = 서명된 데이터 형식입니다.|  
|MONEY|**smallint**|지정 된 **money** 데이터 형식입니다.<br /><br /> 1 = **money** 데이터 형식입니다.<br /><br /> 0 = 사용 안을 **money** 데이터 형식입니다.|  
|AUTO_INCREMENT|**smallint**|자동 증가를 지정합니다.<br /><br /> 1 = 자동 증가입니다.<br /><br /> 0 = 자동 증가가 아닙니다.<br /><br /> NULL = 특성이 적용되지 않습니다.<br /><br /> 응용 프로그램은 이 특성을 가진 열에 값을 삽입할 수는 있으나 열에 있는 값을 업데이트할 수 없습니다. 제외 된 **비트** 데이터 형식으로 AUTO_INCREMENT는 정확한 수치 또는 근사치 데이터 형식 범주에 속하는 데이터 형식에 대해서만 유효 합니다.|  
|LOCAL_TYPE_NAME|**sysname**|데이터 원본에 종속적인 데이터 형식 이름의 지역화된 버전입니다. 예를 들어 프랑스에서 DECIMAL은 DECIMALE이 됩니다. 데이터 원본이 지역화된 이름을 지원하지 않는 경우에는 NULL이 반환됩니다.|  
|MINIMUM_SCALE|**smallint**|데이터 원본에서 데이터 형식의 최소 소수 자릿수입니다. 데이터 형식이 고정 소수 자릿수인 경우에는 MINIMUM_SCALE 및 MAXIMUM_SCALE 열 모두 이 값을 포함합니다. 소수 자릿수가 적용되지 않는 경우에는 NULL이 반환됩니다.|  
|MAXIMUM_SCALE|**smallint**|데이터 원본에서 데이터 형식의 최대 소수 자릿수입니다. 데이터 원본에서 최대 소수 자릿수는 별도로 정의되지 않고 그 대신 최대 자릿수와 동일하게 정의된 경우에는 이 열이 PRECISION 열과 같은 값을 포함하게 됩니다.|  
|SQL_DATA_TYPE|**smallint**|설명자의 TYPE 필드에 표시되는 SQL 데이터 형식의 값입니다. 이 열은 제외 하 고는 DATA_TYPE 열과 동일 합니다 **날짜/시간** 및 ANSI **간격** 데이터 형식입니다. 이 필드는 항상 값을 반환합니다.|  
|SQL_DATETIME_SUB|**smallint**|**날짜/시간** 또는 ANSI **간격** SQL_DATA_TYPE 값이 SQL_DATETIME 또는 sql_interval 인 경우 하위 코드입니다. 이외의 다른 데이터 형식의 **날짜/시간** 및 ANSI **간격**,이 필드는 NULL입니다.|  
|NUM_PREC_RADIX|**int**|열이 보유할 수 있는 최대 수를 계산하는 데 필요한 비트 수 또는 자릿수입니다. 데이터 형식이 근사 숫자 데이터 형식인 경우 이 열은 비트를 표시하는 2라는 값을 포함할 수 있습니다. 정확한 숫자 형식인 경우에는 이 열이 10진수의 수를 표시하는 10이라는 값을 포함할 수 있습니다. 그렇지 않은 경우 이 열은 NULL입니다. 응용 프로그램에서는 전체 자릿수와 기수를 결합하여 열이 보유할 수 있는 최대 수를 계산할 수 있습니다.|  
|INTERVAL_PRECISION|**smallint**|경우에 전체 자릿수를 유도 하는 간격 값 *data_type* 됩니다 **간격**NULL이 고, 그렇지 않으면입니다.|  
|USERTYPE|**smallint**|**usertype** systypes 테이블의 값입니다.|  
  
## <a name="remarks"></a>설명  
 sp_datatype_info는 ODBC의 SQLGetTypeInfo와 같습니다. 반환되는 결과는 DATA_TYPE을 기준으로 정렬되며 데이터 형식의 근접한 정도에 따라 해당 ODBC SQL 데이터 형식에 매핑됩니다.  
  
## <a name="permissions"></a>사용 권한  
 public 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예제에 대 한 정보를 검색 합니다 **sysname** 및 **nvarchar** 데이터 형식을 지정 하 여는 *data_type* 값 `-9`합니다.  
  
```  
USE master;  
GO  
EXEC sp_datatype_info -9;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
