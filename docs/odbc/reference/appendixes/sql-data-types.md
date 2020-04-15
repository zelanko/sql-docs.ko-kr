---
title: SQL 데이터 유형 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305007"
---
# <a name="sql-data-types"></a>SQL 데이터 형식
각 DBMS는 자체 SQL 형식을 정의합니다. 각 ODBC 드라이버는 연결된 DBMS가 정의하는 SQL 데이터 형식만 노출합니다. 드라이버가 DBMS SQL 형식을 ODBC 정의 SQL 형식 식별자에 매핑하는 방법과 드라이버가 DBMS SQL 형식을 자체 드라이버 별 SQL 형식 식별자에 매핑하는 방법에 대한 정보는 **SQLGetTypeInfo**에 대한 호출을 통해 반환됩니다. 또한 드라이버는 **SQLColAttribute,** **SQLColumns,** **SQLDescribeCol,** **SQLDescribeParam,** **SQLProfileColumns, SQLProfileColumns**및 **SQLSpecialColumns 및 SQLSpecialColumns에**대한 호출을 통해 열 및 매개 변수의 데이터 형식을 설명할 때 SQL 데이터 형식을 반환합니다.  
  
> [!NOTE]  
>  SQL 데이터 형식은 구현 설명자의 SQL_DESC_ CONCISE_TYPE, SQL_DESC_TYPE 및 SQL_DESC_DATETIME_INTERVAL_CODE 필드에 포함됩니다. SQL 데이터 형식의 특성은 구현 설명자의 SQL_DESC_PRECISION, SQL_DESC_SCALE, SQL_DESC_LENGTH 및 SQL_DESC_OCTET_LENGTH 필드에 포함되어 있습니다. 자세한 내용은 이 부록의 후반부 [데이터 유형 식별자 및 설명자를](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) 참조하십시오.  
  
 지정된 드라이버 및 데이터 원본이 이 부록에 정의된 모든 SQL 데이터 형식을 반드시 지원하지는 않습니다. SQL 데이터 형식에 대한 드라이버의 지원은 드라이버가 준수하는 SQL-92 수준에 따라 달라집니다. 드라이버에서 지원하는 SQL-92 문법 의 수준을 결정하기 위해 응용 프로그램은 SQL_SQL_CONFORMANCE 정보 형식을 사용하여 **SQLGetInfo를** 호출합니다. 또한 지정된 드라이버 및 데이터 원본은 추가 드라이버별 SQL 데이터 형식을 지원할 수 있습니다. 드라이버가 지원하는 데이터 형식을 확인하려면 응용 프로그램에서 **SQLGetTypeInfo**를 호출합니다. 드라이버 별 SQL 데이터 형식에 대한 자세한 내용은 드라이버 설명서를 참조하십시오. 특정 데이터 원본의 데이터 형식에 대한 자세한 내용은 해당 데이터 원본에 대한 설명서를 참조하십시오.  
  
> [!IMPORTANT]  
>  이 부록 전체의 표는 지침일 뿐이며 일반적으로 사용되는 이름, 범위 및 SQL 데이터 형식의 제한을 보여 준다. 지정된 데이터 원본은 나열된 데이터 형식 중 일부만 지원할 수 있으며 지원되는 데이터 형식의 특성은 나열된 데이터 형식과 다를 수 있습니다.  
  
 다음 표에는 모든 SQL 데이터 형식에 대해 유효한 SQL 형식 식별자가 나열되어 있습니다. 또한 이 표에는 SQL-92의 해당 데이터 형식에 대한 이름과 설명이 나열되어 있습니다(있는 경우).  
  
|SQL 유형 식별자[1]|일반적인 SQL 데이터<br /><br /> [2]|일반적인 유형 설명|  
|------------------------------|------------------------------------|------------------------------|  
|SQL_CHAR|CHAR *(n)*|고정 문자열 길이 *n의*문자열 문자열|  
|SQL_VARCHAR|바르차르 *(n)*|최대 문자열 길이 *n이*있는 가변 길이 문자열 문자열|  
|SQL_LONGVARCHAR|LONG VARCHAR|가변 길이 문자 데이터입니다. 최대 길이는 데이터 원본에 따라 다릅니다. [9]|  
|SQL_WCHAR|WCHAR *(n)*|고정 문자열 길이 *n의* 유니코드 문자 문자열|  
|SQL_WVARCHAR|바르우차르 *(n)*|최대 문자열 길이 *n이* 있는 유니코드 가변 길이 문자열|  
|SQL_WLONGVARCHAR|롱바차르|유니코드 가변 길이 문자 데이터입니다. 최대 길이는 데이터 원본에 따라 다릅니다.|  
|SQL_DECIMAL|십진수 *(p*,*s)*|서명된 정확한 숫자 값으로 최소 *p* 및 배율 s의 정밀도가 *있습니다.* (최대 정밀도는 드라이버 정의입니다.) (1 <= *p* <= 15; *s)를* <= *참조하십시오.* [4]|  
|SQL_NUMERIC|숫자 *(p*,*s)*|정밀도 *p* 및 배율 *s(1* <= *p* <= 15로 서명된 정확한 숫자 값; *s)를* <= *참조하십시오.* [4]|  
|SQL_SMALLINT|SMALLINT|정밀도 5및 배율 0의 정확한 숫자 값(서명: -32,768 <= *n* <= 32,767, 서명되지 않음: 0 <= *n* <= 65,535][3].|  
|SQL_INTEGER|INTEGER|정밀도 10 및 배율 0의 정확한 숫자 값(서명됨: -2[31] <= *n* <= 2[31] - 1, 서명되지 않음: 0 <= *n* <= 2[32] - 1][3].|  
|SQL_REAL|real|이진 정밀도 24(0 또는 절대 값 10[-38]에서 10[38])로 서명된 대략적인 숫자 값입니다.|  
|SQL_FLOAT|플로트 *(p)*|서명된 근사값, 숫자 값은 최소 *p.* (최대 정밀도는 드라이버 정의입니다.) [5]|  
|SQL_DOUBLE|DOUBLE PRECISION|이진 정밀도 53(0 또는 절대 값 10[-308]에서 10[308])으로 서명된 대략적인 숫자 값입니다.|  
|SQL_BIT|BIT|단일 비트 이진 데이터입니다. [8]|  
|SQL_TINYINT|TINYINT|정밀도 3 및 배율 0의 정확한 숫자 값(서명: -128 <= *n* <= 127, 서명되지 않음: 0 <= *n* <= 255][3].|  
|SQL_BIGINT|bigint|정밀도 19(서명되지 않은 경우) 또는 20(서명되지 않은 경우) 및 배율 0(서명: -2[63] <= *n* <= 2[63] - 1, 서명되지 않음: 0 <= *n* <= 2[64] - 1][3][9].|  
|SQL_BINARY|*바이너리(n)*|고정 길이 *n.* [9]|  
|SQL_VARBINARY|VARBINARY *(n)*|최대 길이 *n.* 최대값은 사용자가 설정합니다. [9]|  
|SQL_LONGVARBINARY|긴 바바이너리|가변 길이 이진 데이터입니다. 최대 길이는 데이터 원본에 따라 다릅니다. [9]|  
|SQL_TYPE_DATE[6]|DATE|연도, 월 및 일 필드, 그레고리오 력의 규칙을 준수 합니다. (이 [부록의 대련력의 제약 조건을](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)참조하십시오.)|  
|SQL_TYPE_TIME[6]|시간 *(p)*|시간, 분 및 초 필드(00~23시간 동안 유효한 값, 00~59분)의 유효한 값, 00~61초의 유효 값입니다. 정밀도 *p는* 초 정밀도를 나타냅니다.|  
|SQL_TYPE_TIMESTAMP[6]|타임 스탬프 *(p)*|날짜 및 시간 데이터 형식에 대해 정의된 유효한 값이 있는 연도, 월, 일, 시간, 분 및 초필드입니다.|  
|SQL_TYPE_UTCDATETIME|UTCDATE 시간|연도, 월, 일, 시간, 분, 초, utchour 및 utcminute 필드입니다. utchour 및 utcminute 필드는 1/10 마이크로초의 정밀도를 갖습니다.|  
|SQL_TYPE_UTCTIME|UTC타임|시간, 분, 초, utchour 및 utcminute 필드입니다. utchour 및 utcminute 필드는 1/10 마이크로초 의 정밀도를 가합니다.|  
|SQL_INTERVAL_MONTH[7]|간격 월 *(p)*|두 날짜 사이의 월 수; *p는* 정밀도를 선도하는 간격입니다.|  
|SQL_INTERVAL_YEAR[7]|간격 연도 *(p)*|두 날짜 사이의 연도 수; *p는* 정밀도를 선도하는 간격입니다.|  
|SQL_INTERVAL_YEAR_TO_MONTH[7]|간격 연도 *(p)* 월|두 날짜 사이의 연도 및 월 수; *p는* 정밀도를 선도하는 간격입니다.|  
|SQL_INTERVAL_DAY[7]|간격 일 *(p)*|두 날짜 사이의 일 수; *p는* 정밀도를 선도하는 간격입니다.|  
|SQL_INTERVAL_HOUR[7]|간격 시간 *(p)*|두 날짜/시간 사이의 시간 수; *p는* 정밀도를 선도하는 간격입니다.|  
|SQL_INTERVAL_MINUTE[7]|간격 분 *(p)*|두 날짜/시간 사이의 분 수; *p는* 정밀도를 선도하는 간격입니다.|  
|SQL_INTERVAL_SECOND[7]|간격 두 번째 *(p*,*q)*|두 날짜/시간 사이의 초 수; *p는* 정밀도를 선도하는 간격이고 *q는* 간격 초 정밀도입니다.|  
|SQL_INTERVAL_DAY_TO_HOUR[7]|간격 일 *(p)* 시간|두 날짜 / 시간 사이의 일 / 시간 의 수; *p는* 정밀도를 선도하는 간격입니다.|  
|SQL_INTERVAL_DAY_TO_MINUTE[7]|간격 일 *(p)* 분|두 날짜 / 시간 사이의 일 / 시간 / 분 수; *p는* 정밀도를 선도하는 간격입니다.|  
|SQL_INTERVAL_DAY_TO_SECOND[7]|간격 일 *(p)* 두 번째 *(q)*|두 날짜/시간 사이의 일/시간/분/초 수; *p는* 정밀도를 선도하는 간격이고 *q는* 간격 초 정밀도입니다.|  
|SQL_INTERVAL_HOUR_TO_MINUTE[7]|간격 시간 *(p)* 분|두 날짜/시간 사이의 시간/분 수; *p는* 정밀도를 선도하는 간격입니다.|  
|SQL_INTERVAL_HOUR_TO_SECOND[7]|간격 시간 *(p)* 두 번째 *(q)*|두 날짜/시간 사이의 시간/분/초 수; *p는* 정밀도를 선도하는 간격이고 *q는* 간격 초 정밀도입니다.|  
|SQL_INTERVAL_MINUTE_TO_SECOND[7]|간격 분 *(p)* 초 *(q)*|두 날짜/시간 사이의 분/초 수; *p는* 정밀도를 선도하는 간격이고 *q는* 간격 초 정밀도입니다.|  
|SQL_GUID|GUID|고정 길이 GUID.|  
  
 [1] **SQLGetTypeInfo**에 대한 호출로 DATA_TYPE 열에서 반환되는 값입니다.  
  
 [2] **SQLGetTypeInfo**에 대한 호출로 NAME 및 CREATE PARAMS 열에 반환된 값입니다. NAME 열은 예를 들어 CHAR-를 반환하지만 CREATE PARAMS 열은 정밀도, 축척 및 길이와 같은 생성 매개 변수의 쉼표로 구분된 목록을 반환합니다.  
  
 [3] 응용 프로그램은 **SQLGetTypeInfo** 또는 **SQLColAttribute를** 사용하여 특정 데이터 형식 또는 결과 집합의 특정 열이 서명되지 않았는지 확인합니다.  
  
 [4] SQL_DECIMAL 및 SQL_NUMERIC 데이터 유형은 정밀도가 다릅니다. DECIMAL(p ,*p**s)의*정밀도는 *p보다*작은 구현 정의 소수점 정밀도인 반면 NUMERIC(p ,*s)의*정밀도는 *p와*정확히 같습니다.*p*  
  
 [5] 구현에 따라 SQL_FLOAT 정밀도는 24 또는 53일 수 있습니다: 24인 경우 SQL_FLOAT 데이터 형식은 SQL_REAL 동일합니다. 53이면 SQL_FLOAT 데이터 형식은 SQL_DOUBLE 동일합니다.  
  
 [6] ODBC *3.x에서*SQL 날짜, 시간 및 타임스탬프 데이터 형식은 각각 SQL_TYPE_DATE, SQL_TYPE_TIME 및 SQL_TYPE_TIMESTAMP. ODBC *2.x에서*데이터 형식은 SQL_DATE, SQL_TIME 및 SQL_TIMESTAMP.  
  
 [7] 간격 SQL 데이터 형식에 대 한 자세한 내용은 [간격 데이터 형식](../../../odbc/reference/appendixes/interval-data-types.md) 섹션, 이 부록의 다음을 참조 하십시오.  
  
 [8] SQL_BIT 데이터 형식은 SQL-92의 BIT 형식과 다른 특성을 가지고 있습니다.  
  
 [9] 이 데이터 형식에는 SQL-92에 해당하는 데이터 형식이 없습니다.  
  
 이 섹션에서는 다음 예제를 제공합니다.  
  
-   [SQLGetTypeInfo 결과 집합의 예](../../../odbc/reference/appendixes/example-sqlgettypeinfo-result-set.md)
