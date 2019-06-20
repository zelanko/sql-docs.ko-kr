---
title: 명시적 데이터 형식 변환 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- explicit data type conversion functions [ODBC]
- data type conversion functions [ODBC]
- functions [ODBC], explicit data type conversion functions
ms.assetid: d5789450-b668-4753-96c8-6789e955e7ed
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77cb69877324b36120b3a277688bb1ad737f5c4d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188979"
---
# <a name="explicit-data-type-conversion-function"></a>명시적 데이터 형식 변환 함수
명시적 데이터 형식 변환이 SQL 데이터 형식 정의 기준으로 지정 됩니다.  
  
 ODBC 구문을 명시적 데이터 형식 변환 함수에 대 한 변환 제한 하지 않습니다. 다른 데이터 형식으로 한 데이터 형식의 특정 변환의 유효성을 검사 각 드라이버별 구현에 의해 결정 됩니다. 드라이버는 ODBC 구문은 기본 구문으로 변환 하는 대로 거부 하지만 ODBC 구문에서 사용할 데이터 원본에서 지원 되지 않는 이러한 변환 합니다. ODBC 함수 **SQLGetInfo**, 변환을 옵션 (예: SQL_CONVERT_BIGINT, SQL_CONVERT_BINARY, SQL_CONVERT_INTERVAL_YEAR_MONTH, 및 등)를 통해 데이터 원본에서 지 원하는 변환에 대 한 질의 시에 .  
  
 형식의 합니다 **변환** 함수는:  
  
 **CONVERT(** _value_exp_, _data_type_ **)**  
  
 함수에 지정 된 값을 반환 합니다. *value_exp* 지정 된 변환 *data_type*여기서 *data_type* 다음 키워드 중 하나입니다.  
  
|||  
|-|-|  
|SQL_BIGINT|SQL_INTERVAL_HOUR_TO_MINUTE|  
|SQL_BINARY|SQL_INTERVAL_HOUR_TO_SECOND|  
|SQL_BIT|SQL_INTERVAL_MINUTE_TO_SECOND|  
|SQL_CHAR|SQL_LONGVARBINARY|  
|SQL_DECIMAL|SQL_LONGVARCHAR|  
|SQL_DOUBLE|SQL_NUMERIC|  
|SQL_FLOAT|SQL_REAL|  
|SQL_GUID|SQL_SMALLINT|  
|SQL_INTEGER|SQL_DATE|  
|SQL_INTERVAL_MONTH|SQL_TIME|  
|SQL_INTERVAL_YEAR|SQL_TIMESTAMP|  
|SQL_INTERVAL_YEAR_TO_MONTH|SQL_TINYINT|  
|SQL_INTERVAL_DAY|SQL_VARBINARY|  
|SQL_INTERVAL_HOUR|SQL_VARCHAR|  
|SQL_INTERVAL_MINUTE|SQL_WCHAR|  
|SQL_INTERVAL_SECOND|SQL_WLONGVARCHAR|  
|SQL_INTERVAL_DAY_TO_HOUR|SQL_WVARCHAR|  
|SQL_INTERVAL_DAY_TO_MINUTE||  
|SQL_INTERVAL_DAY_TO_SECOND||  
  
 ODBC 구문을 명시적 데이터 형식 변환 함수에 대 한 변환 형식 지정을 지원 하지 않습니다. 명시적 형식 지정 데이터 원본에서 지원 되는 드라이버 기본값을 지정 하거나 형식 사양을 구현 해야 합니다.  
  
 인수 *value_exp* 수 열 이름, 결과 다른 스칼라 함수 또는 숫자 또는 문자열 리터럴일 수 있습니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
```  
{ fn CONVERT( { fn CURDATE() }, SQL_CHAR ) }  
```  
  
 CURDATE 스칼라 함수의 출력을 문자열로 변환합니다.  
  
 ODBC는 반환 값에 대 한 데이터 형식을 위임 하지 때문에 (함수 경우가 종종 있으므로 데이터 소스 관련) 스칼라 함수, 응용 프로그램에서 데이터 형식 변환에 적용할 가능한 CONVERT 스칼라 함수를 사용 해야 합니다.  
  
 다음 두 예제는 사용법을 보여 줍니다.는 **변환** 함수입니다. 이러한 예제는 EMPNO 열 SQL_SMALLINT 형식의 및 SQL_CHAR 형식의 EMPNAME 열을 사용 하 여 EMPLOYEES 라는 테이블의 존재 여부를 가정 합니다.  
  
 다음 SQL 문을 지정 하는 응용 프로그램:  
  
```  
SELECT EMPNO FROM EMPLOYEES WHERE {fn CONVERT(EMPNO,SQL_CHAR)} LIKE '1%'  
```  
  
-   ORACLE 용 드라이버에는 SQL 문을 변환합니다.  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE to_char(EMPNO) LIKE '1%'  
    ```  
  
-   SQL Server 용 driver에는 SQL 문을 변환합니다.  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE convert(char,EMPNO) LIKE '1%'  
    ```  
  
 다음 SQL 문을 지정 하는 응용 프로그램:  
  
```  
SELECT {fn ABS(EMPNO)}, {fn CONVERT(EMPNAME,SQL_SMALLINT)}  
   FROM EMPLOYEES WHERE EMPNO <> 0  
```  
  
-   ORACLE 용 드라이버에는 SQL 문을 변환합니다.  
  
    ```  
    SELECT abs(EMPNO), to_number(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```  
  
-   SQL Server 용 driver에는 SQL 문을 변환합니다.  
  
    ```  
    SELECT abs(EMPNO), convert(smallint, EMPNAME) FROM EMPLOYEES  
       WHERE EMPNO <> 0  
    ```  
  
-   Ingres 드라이버에는 SQL 문을 변환합니다.  
  
    ```  
    SELECT abs(EMPNO), int2(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```
