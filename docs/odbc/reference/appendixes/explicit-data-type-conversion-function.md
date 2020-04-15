---
title: 명시적 데이터 형식 변환 기능 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2de8a8cb6177e9210e8d48c0ce097d13c9a276fd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306994"
---
# <a name="explicit-data-type-conversion-function"></a>명시적 데이터 형식 변환 함수
명시적 데이터 형식 변환은 SQL 데이터 형식 정의측면에서 지정됩니다.  
  
 명시적 데이터 형식 변환 함수에 대한 ODBC 구문은 변환을 제한하지 않습니다. 한 데이터 형식의 특정 변환에서 다른 데이터 유형으로의 유효성은 각 드라이버별 구현에 의해 결정됩니다. 드라이버는 ODBC 구문을 기본 구문으로 변환할 때 ODBC 구문에서 합법적이지만 데이터 원본에서 지원되지 않는 변환을 거부합니다. ODBC 함수 **SQLGetInfo는**변환 옵션(예: SQL_CONVERT_BIGINT, SQL_CONVERT_BINARY, SQL_CONVERT_INTERVAL_YEAR_MONTH 등)을 사용하여 데이터 원본에서 지원하는 변환에 대해 문의하는 방법을 제공합니다.  
  
 **CONVERT** 함수의 형식은 다음과 입니다.  
  
 **변환** _(value_exp,_ _data_type)_**)**  
  
 함수는 지정된 *data_type*변환된 *value_exp* 지정한 값을 반환하며, 여기서 *data_type* 다음 키워드 중 하나입니다.  
  
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
  
 명시적 데이터 형식 변환 함수에 대한 ODBC 구문은 변환 형식의 사양을 지원하지 않습니다. 명시적 형식의 사양이 기본 데이터 원본에서 지원되는 경우 드라이버는 기본값을 지정하거나 형식 사양을 구현해야 합니다.  
  
 *value_exp* 인수는 열 이름, 다른 스칼라 함수의 결과 또는 숫자 또는 문자열 리터럴일 수 있습니다. 다음은 그 예입니다.  
  
```  
{ fn CONVERT( { fn CURDATE() }, SQL_CHAR ) }  
```  
  
 은 CURDATE 스칼라 함수의 출력을 문자 문자열로 변환합니다.  
  
 ODBC는 scalar 함수에서 반환 값에 대 한 데이터 형식을 위임 하지 않습니다 (함수는 종종 데이터 원본에 따라 있기 때문에), 응용 프로그램은 데이터 형식 변환을 강제로 변환 할 수 있는 CONVERT scalar 함수를 사용 해야 합니다.  
  
 다음 두 예제에서는 **CONVERT** 함수의 사용을 보여 줍니다. 이러한 예제에서는 형식 SQL_SMALLINT EMPNO 열과 SQL_CHAR 형식의 EMPNAME 열이 있는 EMPLOYEES라는 테이블이 있다고 가정합니다.  
  
 응용 프로그램이 다음 SQL 문을 지정하는 경우:  
  
```  
SELECT EMPNO FROM EMPLOYEES WHERE {fn CONVERT(EMPNO,SQL_CHAR)} LIKE '1%'  
```  
  
-   ORACLE의 드라이버는 SQL 문을 다음과 같은 것으로 변환합니다.  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE to_char(EMPNO) LIKE '1%'  
    ```  
  
-   SQL Server의 드라이버는 SQL 문을 다음과 같은 것으로 변환합니다.  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE convert(char,EMPNO) LIKE '1%'  
    ```  
  
 응용 프로그램이 다음 SQL 문을 지정하는 경우:  
  
```  
SELECT {fn ABS(EMPNO)}, {fn CONVERT(EMPNAME,SQL_SMALLINT)}  
   FROM EMPLOYEES WHERE EMPNO <> 0  
```  
  
-   ORACLE의 드라이버는 SQL 문을 다음과 같은 것으로 변환합니다.  
  
    ```  
    SELECT abs(EMPNO), to_number(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```  
  
-   SQL Server의 드라이버는 SQL 문을 다음과 같은 것으로 변환합니다.  
  
    ```  
    SELECT abs(EMPNO), convert(smallint, EMPNAME) FROM EMPLOYEES  
       WHERE EMPNO <> 0  
    ```  
  
-   Ingres에 대한 드라이버는 SQL 문을 다음과 같은 것으로 변환합니다.  
  
    ```  
    SELECT abs(EMPNO), int2(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```
