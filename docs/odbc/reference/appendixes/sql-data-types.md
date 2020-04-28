---
title: SQL 데이터 형식 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL data types [ODBC]
- SQL data types [ODBC], about SQL data types
- data types [ODBC], SQL data types
ms.assetid: 1b22f985-f5e4-4779-87eb-e43329a442b1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3cc91213533aa39f30be1bc838cc014c20e70884
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305007"
---
# <a name="sql-data-types"></a>SQL 데이터 형식
각 DBMS는 자체 SQL 형식을 정의 합니다. 각 ODBC 드라이버는 관련 DBMS에서 정의 하는 SQL 데이터 형식만 노출 합니다. 드라이버가 DBMS SQL 형식을 ODBC 정의 SQL 형식 식별자에 매핑하는 방법 및 드라이버가 DBMS SQL 형식을 고유한 드라이버별 SQL 형식 식별자에 매핑하는 방법에 대 한 정보는 **SQLGetTypeInfo**를 호출 하 여 반환 됩니다. 또한 드라이버는 **Sqlcolattribute**, **sqlcolumns**, **SQLDescribeCol**, **SQLDescribeParam**, **SQLProcedureColumns**및 **SQLSpecialColumns**에 대 한 호출을 통해 열과 매개 변수의 데이터 형식을 설명 하는 경우 SQL 데이터 형식을 반환 합니다.  
  
> [!NOTE]  
>  SQL 데이터 형식은 구현 설명자의 SQL_DESC_ CONCISE_TYPE, SQL_DESC_TYPE 및 SQL_DESC_DATETIME_INTERVAL_CODE 필드에 포함 되어 있습니다. SQL 데이터 형식의 특징은 구현 설명자의 SQL_DESC_PRECISION, SQL_DESC_SCALE, SQL_DESC_LENGTH 및 SQL_DESC_OCTET_LENGTH 필드에 포함 되어 있습니다. 자세한 내용은이 부록의 뒷부분에 나오는 [데이터 형식 식별자 및 설명자](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) 를 참조 하세요.  
  
 지정 된 드라이버 및 데이터 원본은이 부록에 정의 된 모든 SQL 데이터 형식을 지원 하지 않을 수 있습니다. SQL 데이터 형식에 대 한 드라이버 지원은 드라이버가 준수 하는 SQL-92 수준에 따라 달라 집니다. 드라이버가 지 원하는 SQL-92 문법의 수준을 확인 하기 위해 응용 프로그램은 SQL_SQL_CONFORMANCE 된 정보 형식으로 **SQLGetInfo** 를 호출 합니다. 또한 지정 된 드라이버와 데이터 원본은 드라이버 특정 SQL 데이터 형식을 추가로 지원할 수 있습니다. 드라이버가 지 원하는 데이터 형식을 확인 하기 위해 응용 프로그램은 **SQLGetTypeInfo**를 호출 합니다. 드라이버별 SQL 데이터 형식에 대 한 자세한 내용은 드라이버 설명서를 참조 하십시오. 특정 데이터 원본에 있는 데이터 형식에 대 한 자세한 내용은 해당 데이터 원본에 대 한 설명서를 참조 하십시오.  
  
> [!IMPORTANT]  
>  이 부록 전체의 표는 지침 이며 일반적으로 사용 되는 이름, 범위 및 SQL 데이터 형식의 제한을 보여 줍니다. 지정 된 데이터 원본은 나열 된 데이터 형식 중 일부만 지원할 수 있으며, 지원 되는 데이터 형식의 특성은 나열 된 데이터 형식에 따라 다를 수 있습니다.  
  
 다음 표에서는 모든 SQL 데이터 형식에 대 한 유효한 SQL 형식 식별자를 보여 줍니다. 테이블에는 SQL-92 (있는 경우)의 해당 데이터 형식에 대 한 이름 및 설명도 나열 됩니다.  
  
|SQL 유형 식별자 [1]|일반적인 SQL 데이터<br /><br /> 유형 [2]|일반 형식 설명|  
|------------------------------|------------------------------------|------------------------------|  
|SQL_CHAR|CHAR (*n*)|고정 문자열 길이 *n*의 문자열입니다.|  
|SQL_VARCHAR|VARCHAR (*n*)|최대 문자열 길이가 *n*인 가변 길이 문자열입니다.|  
|SQL_LONGVARCHAR|LONG VARCHAR|가변 길이 문자 데이터입니다. 최대 길이는 데이터 소스에 따라 다릅니다. 되었는지|  
|SQL_WCHAR|WCHAR (*n*)|고정 문자열 길이 *n* 의 유니코드 문자열|  
|SQL_WVARCHAR|VARWCHAR (*n*)|최대 문자열 길이가 *n* 인 유니코드 가변 길이 문자열|  
|SQL_WLONGVARCHAR|LONGWVARCHAR|유니코드 가변 길이 문자 데이터입니다. 최대 길이는 데이터 소스에 따라 다릅니다.|  
|SQL_DECIMAL|DECIMAL (*p*,*s*)|최소 *p* 와 소수 자릿수의 전체 자릿수를 가진 부호 있는 정확한 숫자 값 *입니다.* 최대 전체 자릿수는 드라이버에 정의 되어 있습니다. (1 <= *p* <= 15; *s* <= *p*). 3-4|  
|SQL_NUMERIC|숫자 (*p*,*s*)|전체 자릿수가 *p* 및 소수 자릿수 *s* 인 부호 있는 정확한 숫자 값 (1 <= *p* <= 15; *s* <= *p*). 3-4|  
|SQL_SMALLINT|SMALLINT|전체 자릿수가 5이 고 소수 자릿수가 0 인 정확한 숫자 값 (부호 있음:-32768 <= *n* <= 32767, unsigned: 0 <= *n* <= 65535) [3].|  
|SQL_INTEGER|INTEGER|전체 자릿수가 10 이며 소수 자릿수가 0 인 정확한 숫자 값 (부호 있음:-2 [31] <= *n* <= 2 [31]-1, unsigned: 0 <= *n* <= 2 [32]-1) [3].|  
|SQL_REAL|real|이진 정밀도 24 (0 또는 절대값 10 [-38] ~ 10 [38])를 포함 하는 부호 있는 근사 숫자 값입니다.|  
|SQL_FLOAT|FLOAT (*p*)|최소 *p*의 이진 전체 자릿수를 사용 하는 부호 있는 근사 숫자 값입니다. 최대 전체 자릿수는 드라이버에 정의 되어 있습니다. 5|  
|SQL_DOUBLE|DOUBLE PRECISION|이진 전체 자릿수 53 (0 또는 절대값 10 [-308] ~ 10 [308])를 사용 하는 부호 있는 근사 숫자 값입니다.|  
|SQL_BIT|BIT|단일 비트 이진 데이터입니다. 20cm(8|  
|SQL_TINYINT|TINYINT|전체 자릿수 3 및 소수 자릿수 0 인 정확한 숫자 값 (부호 있음:-128 <= *n* <= 127, unsigned: 0 <= *n* <= 255) [3].|  
|SQL_BIGINT|bigint|전체 자릿수가 19 인 정확한 숫자 값 (서명 된 경우) 또는 20 (부호 없는 경우) 및 소수 자릿수 0 (부호 있음:-2 [63] <= *n* <= 2 [63]-1, unsigned: 0 <= *n* <= 2 [64]-1) [3], [9].|  
|SQL_BINARY|BINARY (*n*)|고정 길이 *n*의 이진 데이터입니다. 되었는지|  
|SQL_VARBINARY|VARBINARY (*n*)|최대 길이 *n*의 가변 길이 이진 데이터입니다. 최대값은 사용자가 설정 합니다. 되었는지|  
|SQL_LONGVARBINARY|긴 VARBINARY|가변 길이 이진 데이터입니다. 최대 길이는 데이터 소스에 따라 다릅니다. 되었는지|  
|SQL_TYPE_DATE [6]|DATE|연도, 월 및 일 필드는 양력의 규칙을 준수 합니다. 이 부록의 뒷부분에 나오는 [양력의 제약 조건](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)을 참조 하세요.|  
|SQL_TYPE_TIME [6]|시간 (*p*)|시간, 분 및 초 필드, 시간에 대 한 유효한 값은 00-23, 분의 경우 00에서 59,에 대 한 유효한 값은 00 ~ 61. 전체 자릿수 *p* 는 초 전체 자릿수를 나타냅니다.|  
|SQL_TYPE_TIMESTAMP [6]|타임 스탬프 (*p*)|날짜 및 시간 데이터 형식에 대해 정의 된 유효한 값이 있는 연도, 월, 일, 시, 분 및 초 필드|  
|SQL_TYPE_UTCDATETIME|DATETIMEOFFSET.UTCDATETIME|년, 월, 일, 시, 분, 초, utchour 및 utcminute 필드입니다. Utchour 및 utcminute 필드에는 1/10 마이크로초 정밀도가 있습니다.|  
|SQL_TYPE_UTCTIME|UTCTIME|시간, 분, 초, utchour 및 utcminute 필드가 있습니다. Utchour 및 utcminute 필드의 마이크로초 precision은 1/10입니다.|  
|SQL_INTERVAL_MONTH [7]|간격 월 (*p*)|두 날짜 사이의 개월 수입니다. *p* 는 간격의 선행 전체 자릿수입니다.|  
|SQL_INTERVAL_YEAR [7]|간격 연도 (*p*)|두 날짜 사이의 연도 수 *p* 는 간격의 선행 전체 자릿수입니다.|  
|SQL_INTERVAL_YEAR_TO_MONTH [7]|간격 연도 (*p*) ~ 월|두 날짜 사이의 연도 및 월 수 *p* 는 간격의 선행 전체 자릿수입니다.|  
|SQL_INTERVAL_DAY [7]|간격 일 (*p*)|두 날짜 사이의 일 수 *p* 는 간격의 선행 전체 자릿수입니다.|  
|SQL_INTERVAL_HOUR [7]|간격 시간 (*p*)|두 날짜/시간 사이의 시간 (시)입니다. *p* 는 간격의 선행 전체 자릿수입니다.|  
|SQL_INTERVAL_MINUTE [7]|간격 (분) (*p*)|두 날짜/시간 사이의 시간 (분)입니다. *p* 는 간격의 선행 전체 자릿수입니다.|  
|SQL_INTERVAL_SECOND [7]|간격 초 (*p*,*q*)|두 날짜/시간 사이의 시간 (초)입니다. *p* 는 간격 선행 전체 자릿수이 고 *q* 는 간격 초 전체 자릿수입니다.|  
|SQL_INTERVAL_DAY_TO_HOUR [7]|간격 일 (*p*)-시간|두 날짜/시간 사이의 일 수/시간 *p* 는 간격의 선행 전체 자릿수입니다.|  
|SQL_INTERVAL_DAY_TO_MINUTE [7]|간격 일 (*p*) ~ 분|두 날짜/시간 사이의 일/시간/분 수 *p* 는 간격의 선행 전체 자릿수입니다.|  
|SQL_INTERVAL_DAY_TO_SECOND [7]|간격 일 (*p*)-초 (*q*)|두 날짜/시간 사이의 일/시간/분/초 수 *p* 는 간격 선행 전체 자릿수이 고 *q* 는 간격 초 전체 자릿수입니다.|  
|SQL_INTERVAL_HOUR_TO_MINUTE [7]|간격 시간 (*p*) ~ 분|두 날짜/시간 사이의 시간/분 수 *p* 는 간격의 선행 전체 자릿수입니다.|  
|SQL_INTERVAL_HOUR_TO_SECOND [7]|간격 시간 (*p*)-초 (*q*)|두 날짜/시간 사이의 시간/분/초 수 *p* 는 간격 선행 전체 자릿수이 고 *q* 는 간격 초 전체 자릿수입니다.|  
|SQL_INTERVAL_MINUTE_TO_SECOND [7]|간격 분 (*p*)-초 (*q*)|두 날짜/시간 사이의 분/초 수 *p* 는 간격 선행 전체 자릿수이 고 *q* 는 간격 초 전체 자릿수입니다.|  
|SQL_GUID|GUID|고정 길이 GUID입니다.|  
  
 [1] **SQLGetTypeInfo**을 호출 하 여 DATA_TYPE 열에 반환 된 값입니다.  
  
 [2] **SQLGetTypeInfo**을 호출 하 여 NAME 및 CREATE PARAMS 열에서 반환 된 값입니다. 이름 열은 지정 (예: CHAR)을 반환 하는 반면 CREATE PARAMS 열은 전체 자릿수, 소수 자릿수 및 길이와 같은 생성 매개 변수의 쉼표로 구분 된 목록을 반환 합니다.  
  
 [3] 응용 프로그램은 **SQLGetTypeInfo** 또는 **sqlcolattribute** 를 사용 하 여 특정 데이터 형식 또는 결과 집합의 특정 열이 서명 되지 않는지 여부를 확인 합니다.  
  
 [4] SQL_DECIMAL 및 SQL_NUMERIC 데이터 형식이 전체 자릿수에만 다릅니다. DECIMAL (*p*,*s*)의 전체 자릿수는 *p*보다는 구현에 정의 된 10 진수 이지만 숫자 (*p*,*s*)의 전체 자릿수는 *p*와 정확히 같습니다.  
  
 [5] 구현에 따라 SQL_FLOAT의 전체 자릿수는 24 또는 53 일 수 있습니다. 24 이면 SQL_FLOAT 데이터 형식이 SQL_REAL와 동일 합니다. 53 인 경우 SQL_FLOAT 데이터 형식은 SQL_DOUBLE와 동일 합니다.  
  
 [6 *] ODBC 3.x에서는 SQL*날짜, 시간 및 타임 스탬프 데이터 형식이 각각 SQL_TYPE_DATE, SQL_TYPE_TIME 및 SQL_TYPE_TIMESTAMP 됩니다. *ODBC 2.x에서 데이터*형식은 SQL_DATE, SQL_TIME 및 SQL_TIMESTAMP입니다.  
  
 [7] interval SQL 데이터 형식에 대 한 자세한 내용은이 부록의 뒷부분에 나오는 [Interval 데이터 형식](../../../odbc/reference/appendixes/interval-data-types.md) 섹션을 참조 하세요.  
  
 [8] SQL_BIT 데이터 형식에는 SQL-92의 비트 형식과 다른 특징이 있습니다.  
  
 [9]이 데이터 형식은 SQL-92에 해당 하는 데이터 형식이 없습니다.  
  
 이 섹션에서는 다음 예제를 제공 합니다.  
  
-   [SQLGetTypeInfo 결과 집합의 예](../../../odbc/reference/appendixes/example-sqlgettypeinfo-result-set.md)
