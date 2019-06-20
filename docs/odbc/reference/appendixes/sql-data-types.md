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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 623ac38791eebc6db84380dfadd499651af938af
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63280917"
---
# <a name="sql-data-types"></a>SQL 데이터 형식
각 DBMS 자체 SQL 형식을 정의합니다. 각 ODBC 드라이버는 연결 된 DBMS를 정의 하는 SQL 데이터 형식만 제공 합니다. 드라이버를 매핑하는 방법에 대 한 정보 DBMS SQL ODBC 정의한 SQL 유형 식별자 형식과 호출을 통해 반환 되는 드라이버 DBMS SQL 형식 자체 드라이버별 SQL 유형 식별자를 매핑하는 방법 **SQLGetTypeInfo**합니다. 데이터 형식의 열과 호출을 통해 매개 변수를 설명 하는 경우 또한 드라이버 SQL 데이터 형식을 반환 **SQLColAttribute**를 **SQLColumns**하십시오 **SQLDescribeCol**, **SQLDescribeParam**하십시오 **SQLProcedureColumns**, 및 **SQLSpecialColumns**합니다.  
  
> [!NOTE]  
>  SQL 데이터 형식 구현 설명자 SQL_DESC_ CONCISE_TYPE, SQL_DESC_TYPE, 및 값을 SQL_DESC_DATETIME_INTERVAL_CODE 필드에 포함 됩니다. SQL 데이터 형식 특성은 구현 설명자의 SQL_DESC_PRECISION, 자릿수가 SQL_DESC_SCALE, SQL_DESC_LENGTH, 및 SQL_DESC_OCTET_LENGTH 필드에 포함 됩니다. 자세한 내용은 [데이터 형식 식별자 및 설명자](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) 이 부록의 뒷부분에 나오는.  
  
 지정된 된 드라이버 및 데이터 원본에서는이 부록에 정의 된 모든 SQL 데이터 형식을 반드시 지원 하지 않습니다. SQL 데이터 형식에 대 한 드라이버의 지원 드라이버를 준수 하는 SQL-92의 수준에 따라 달라 집니다. 응용 프로그램이 호출 드라이버에서 지원 되는 SQL-92 문법의 수준을 결정할 **SQLGetInfo** SQL_SQL_CONFORMANCE 정보 형식을 사용 하 여 합니다. 또한 지정된 된 드라이버 및 데이터 원본 추가, 드라이버별 SQL 데이터 형식을 지원할 수 있습니다. 지 원하는 데이터 형식 드라이버를 확인 하려면, 응용 프로그램 호출 **SQLGetTypeInfo**합니다. 드라이버별 SQL 데이터 형식에 대 한 내용은 드라이버의 설명서를 참조 하십시오. 특정 데이터 원본에서 데이터 형식에 대 한 자세한 내용은 해당 데이터 원본에 대 한 설명서를 참조 하세요.  
  
> [!IMPORTANT]  
>  이 부록 전체 테이블만 지침 및 일반적으로 사용 하는 표시 이름, 범위 및 SQL 데이터 형식의 제한 됩니다. 지정된 된 데이터 원본 나열 된 데이터 형식 중 일부만 지원할 수도 있습니다 및 지원 되는 데이터 형식의 특성 목록에서 다를 수 있습니다.  
  
 다음 표에서 모든 SQL 데이터 형식에 대 한 유효한 SQL 유형 식별자를 나열합니다. 또한 표에서 이름 및 SQL-92에서 해당 데이터 형식의 설명을 (있는 경우).  
  
|SQL 유형 식별자 [1]|일반적인 SQL 데이터<br /><br /> type[2]|일반적인 형식 설명|  
|------------------------------|------------------------------------|------------------------------|  
|SQL_CHAR|CHAR(*n*)|고정된 문자열 길이의 문자열이 *n*합니다.|  
|SQL_VARCHAR|VARCHAR (*n*)|최대 문자열 길이 사용 하 여 다양 한 길이의 문자열 *n*합니다.|  
|SQL_LONGVARCHAR|LONG VARCHAR|가변 길이 문자 데이터입니다. 최대 길이 데이터 원본에 따라 결정 됩니다. [9]|  
|SQL_WCHAR|WCHAR (*n*)|고정된 문자열 길이의 유니코드 문자열 *n*|  
|SQL_WVARCHAR|VARWCHAR (*n*)|최대 문자열 길이 사용 하 여 유니코드 가변 길이 문자 문자열 *n*|  
|SQL_WLONGVARCHAR|LONGWVARCHAR|유니코드 가변 길이 문자 데이터입니다. 최대 길이 데이터 원본에 따라 결정|  
|SQL_DECIMAL|DECIMAL(*p*,*s*)|부호 있는 정확한 숫자 값 정밀도를 가진 이상 *p* 및 확장 *s입니다.* (최대 전체 자릿수는 드라이버에서 정의 된.) (1 < = *p* < = 15; *s* <= *p*). [ 4]|  
|SQL_NUMERIC|NUMERIC(*p*,*s*)|부호 있는 정확한 숫자 값은 전체 자릿수가 *p* 및 크기 조정 *s* (1 < = *p* < = 15; *s* <= *p*). [ 4]|  
|SQL_SMALLINT|SMALLINT|전체 자릿수 5 인 정확한 숫자 값 이며 배율 0 (서명:-32,768 < = *n* < = 32,767, 부호 없음:  0 <= *n* <= 65,535)[3].|  
|SQL_INTEGER|INTEGER|전체 자릿수 10 인 정확한 숫자 값 이며 배율 0 (서명:-2 [31] < = *n* < = 2 [31]-1, 부호 없음:  0 <= *n* <= 2[32] - 1)[3].|  
|SQL_REAL|real|부호 있는 숫자 값 이진 정밀도 24 (0 또는 절대값 10 [-38] 10[38]) 하 합니다.|  
|SQL_FLOAT|FLOAT (*p*)|부호 있는 숫자 값의 이진 정밀도 사용 하 여 최소한 *p*합니다. (최대 전체 자릿수는 드라이버에서 정의 된.) [5]|  
|SQL_DOUBLE|DOUBLE PRECISION|부호 있는 숫자 값을 이진 정밀도 53 (0 또는 절대값 10 [-308] 10[308]) 하 합니다.|  
|SQL_BIT|BIT|단일 비트 이진 데이터입니다. [8]|  
|SQL_TINYINT|TINYINT|전체 자릿수가 3 인 정확한 숫자 값 이며 배율 0 (서명:-128 < = *n* < = 127, 부호 없음:  0 <= *n* <= 255)[3].|  
|SQL_BIGINT|bigint|전체 자릿수 19 (부호 있는 경우)를 사용 하 여 숫자 값 또는 20 (부호 없음) 하는 경우 정확한 이며 배율 0 (서명:-2 [63] < = *n* < = 2 [63]-1, 부호 없음: 0 <= *n* <= 2[64] - 1)[3],[9].|  
|SQL_BINARY|BINARY(*n*)|고정 길이의 이진 데이터 *n*. [ 9]|  
|SQL_VARBINARY|VARBINARY(*n*)|가변 길이 이진 데이터의 최대 길이 *n*합니다. 최대는 사용자가 설정 됩니다. [9]|  
|SQL_LONGVARBINARY|LONG VARBINARY|가변 길이 이진 데이터입니다. 최대 길이 데이터 원본에 따라 결정 됩니다. [9]|  
|SQL_TYPE_DATE[6]|DATE|연도, 월 및 날짜 필드를 일반 달력의 규칙을 준수 합니다. (참조 [일반 달력의 제약 조건](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)이 부록의 뒷부분에 나오는.)|  
|SQL_TYPE_TIME[6]|TIME(*p*)|시간, 분 및 00부터 59까지 분 00 ~ 23 사이의 유효한 값의 시간에 대 한 유효한 값 및 00-61 초에 대 한 유효한 값을 사용 하 여 두 번째 필드입니다. 전체 자릿수 *p* 초 전체 자릿수를 나타냅니다.|  
|SQL_TYPE_TIMESTAMP[6]|TIMESTAMP(*p*)|연도, 월, 일, 시간, 분 및 날짜 및 시간 데이터 형식에 대해 정의 된 유효한 값을 사용 하 여 두 번째 필드입니다.|  
|SQL_TYPE_UTCDATETIME|UTCDATETIME|연도, 월, 일, 시, 분, 초, utchour, 및 utcminute 필드입니다. Utchour 및 utcminute 필드에는 전체 자릿수가 1/10 (마이크로초)입니다.|  
|SQL_TYPE_UTCTIME|UTCTIME|시간, 분, 초, utchour, 및 utcminute 필드입니다. Utchour 및 utcminute 필드에는 1/10 마이크로초 전체 자릿수가...|  
|SQL_INTERVAL_MONTH[7]|간격이 월 (*p*)|두 날짜; 사이의 개월 수 *p* 전체 자릿수를 유도 하는 간격입니다.|  
|SQL_INTERVAL_YEAR[7]|INTERVAL YEAR (*p*)|두 날짜 사이의 연도 수 *p* 전체 자릿수를 유도 하는 간격입니다.|  
|SQL_INTERVAL_YEAR_TO_MONTH[7]|INTERVAL YEAR (*p*) 월|년 및; 두 날짜 사이의 개월 수 *p* 전체 자릿수를 유도 하는 간격입니다.|  
|SQL_INTERVAL_DAY[7]|INTERVAL DAY(*p*)|두 날짜 사이의 일 수 *p* 전체 자릿수를 유도 하는 간격입니다.|  
|SQL_INTERVAL_HOUR[7]|간격 시간 (*p*)|두 시간의 날짜/시간입니다. *p* 전체 자릿수를 유도 하는 간격입니다.|  
|SQL_INTERVAL_MINUTE[7]|INTERVAL MINUTE(*p*)|날짜/시간 간 시간 (분) 수입니다. *p* 전체 자릿수를 유도 하는 간격입니다.|  
|SQL_INTERVAL_SECOND[7]|INTERVAL SECOND(*p*,*q*)|날짜/시간 간 시간 (초) 수입니다. *p* 선행 정밀도 간격 및 *q* 간격 초 전체 자릿수입니다.|  
|SQL_INTERVAL_DAY_TO_HOUR[7]|간격 일 (*p*) 시간|두 날짜/시간의 날짜/시간입니다. *p* 전체 자릿수를 유도 하는 간격입니다.|  
|SQL_INTERVAL_DAY_TO_MINUTE[7]|간격 일 (*p*) 분|두 분/일/시간 날짜/시간입니다. *p* 전체 자릿수를 유도 하는 간격입니다.|  
|SQL_INTERVAL_DAY_TO_SECOND[7]|간격 일 (*p*) 두 번째 (*q*)|일/시간/분/시간 (초) 두 날짜/시간입니다. *p* 선행 정밀도 간격 및 *q* 간격 초 전체 자릿수입니다.|  
|SQL_INTERVAL_HOUR_TO_MINUTE[7]|간격 시간 (*p*) 분|시간/시간 (분) 두 날짜/시간입니다. *p* 전체 자릿수를 유도 하는 간격입니다.|  
|SQL_INTERVAL_HOUR_TO_SECOND[7]|간격 시간 (*p*) 두 번째 (*q*)|시간/분/시간 (초) 두 날짜/시간입니다. *p* 선행 정밀도 간격 및 *q* 간격 초 전체 자릿수입니다.|  
|SQL_INTERVAL_MINUTE_TO_SECOND[7]|INTERVAL MINUTE(*p*) TO SECOND(*q*)|분/시간 (초) 두 날짜/시간입니다. *p* 선행 정밀도 간격 및 *q* 간격 초 전체 자릿수입니다.|  
|SQL_GUID|GUID|고정된 길이 GUID입니다.|  
  
 [1]이를 호출 하 여 DATA_TYPE 열에 반환 값은 **SQLGetTypeInfo**합니다.  
  
 [2]이를 호출 하 여 이름 및 만들 매개 변수 열에 반환 값은 **SQLGetTypeInfo**합니다. 이름 열 지정을 반환 합니다.-예를 들어, CHAR-반면 만들기 매개 변수 열 전체 자릿수, 소수 자릿수 및 길이 같은 생성 매개 변수의 쉼표로 구분 된 목록을 반환 합니다.  
  
 [3] 응용 프로그램에서 사용 **SQLGetTypeInfo** 하거나 **SQLColAttribute** 특정 데이터 형식 또는 결과 집합의 특정 열 서명 되는지 확인 하려면.  
  
 [4] SQL_DECIMAL 및 SQL_NUMERIC 데이터 형식의 자릿수만 다릅니다. 10 진수의 전체 자릿수 (*p*를*s*)는 구현 시 정의 된 전체 자릿수는은 이상 *p*반면 숫자 전체 자릿수 (*p* 하십시오*s*) 정확히 같습니다 *p*합니다.  
  
 [5]에 따라 구현 SQL_FLOAT의 정밀도 24 또는 53 일 수 있습니다: 데이터 형식을 SQL_FLOAT SQL_REAL; 동일 24 인 경우 53 인 경우 SQL_DOUBLE 동일 SQL_FLOAT 데이터 유형이입니다.  
  
 [ODBC 3에서 6] *.x*, SQL date, time 및 timestamp 데이터 형식은 SQL_TYPE_DATE, SQL_TYPE_TIME 및 SQL_TYPE_TIMESTAMP, ODBC 2에서 각각;. *x*, SQL_DATE, SQL_TIME, 및 SQL_TIMESTAMP 데이터 형식이 됩니다.  
  
 [7] 간격 SQL 데이터 형식에 대 한 자세한 내용은 참조는 [Interval 데이터 형식을](../../../odbc/reference/appendixes/interval-data-types.md) 이 부록의 뒷부분에 나오는 섹션입니다.  
  
 [8] SQL_BIT 데이터 형식 특징이 다른 비트 형식 보다 SQL-92에 있습니다.  
  
 [9]이 데이터 형식은 SQL-92에 해당 데이터 형식이 없음  
  
 이 섹션에서는 다음 예제를 제공 합니다.  
  
-   [SQLGetTypeInfo 결과 집합의 예](../../../odbc/reference/appendixes/example-sqlgettypeinfo-result-set.md)
