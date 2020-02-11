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
ms.openlocfilehash: 6982f7b7caa71abc08c5b84ef1bb6211dcadaecd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67913608"
---
# <a name="explicit-data-type-conversion-function"></a>명시적 데이터 형식 변환 함수
명시적 데이터 형식 변환은 SQL 데이터 형식 정의를 기준으로 지정 됩니다.  
  
 명시적 데이터 형식 변환 함수에 대 한 ODBC 구문은 변환을 제한 하지 않습니다. 한 데이터 형식에서 다른 데이터 형식으로의 특정 변환의 유효성은 각 드라이버별 구현에 따라 결정 됩니다. 드라이버는 ODBC 구문을 네이티브 구문으로 변환 하 고, ODBC 구문의 법적 고 지는 않지만 데이터 원본에서 지원 하지 않는 변환을 거부 합니다. 변환 옵션 (예: SQL_CONVERT_BIGINT, SQL_CONVERT_BINARY, SQL_CONVERT_INTERVAL_YEAR_MONTH 등)이 포함 된 ODBC 함수 **SQLGetInfo**는 데이터 소스에서 지 원하는 변환을 제공 하는 방법을 제공 합니다.  
  
 **CONVERT** 함수의 형식은 다음과 같습니다.  
  
 **CONVERT (** _value_exp_, _data_type_**)**  
  
 함수는 지정 된 *data_type*로 변환 된 *value_exp* 에 지정 된 값을 반환 합니다. 여기서 *data_type* 는 다음 키워드 중 하나입니다.  
  
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
  
 명시적 데이터 형식 변환 함수에 대 한 ODBC 구문은 변환 형식의 사양을 지원 하지 않습니다. 기본 데이터 원본에서 명시적 형식 지정을 지 원하는 경우 드라이버는 기본값을 지정 하거나 형식 사양을 구현 해야 합니다.  
  
 *Value_exp* 인수는 열 이름, 다른 스칼라 함수의 결과 또는 숫자 또는 문자열 리터럴일 수 있습니다. 다음은 그 예입니다.  
  
```  
{ fn CONVERT( { fn CURDATE() }, SQL_CHAR ) }  
```  
  
 CURDATE 스칼라 함수의 출력을 문자열로 변환 합니다.  
  
 ODBC는 스칼라 함수에서 반환 값에 대 한 데이터 형식을 지정 하지 않기 때문에 (함수가 일반적으로 데이터 소스와 관련 되어 있기 때문에) 응용 프로그램은 가능 하면 CONVERT 스칼라 함수를 사용 하 여 데이터 형식을 강제로 변환 해야 합니다.  
  
 다음 두 예에서는 **CONVERT** 함수를 사용 하는 방법을 보여 줍니다. 이러한 예에서는 SQL_SMALLINT 형식의 EMPNO 열과 SQL_CHAR 형식의 EMPNAME 열이 있는 EMPLOYEES 라는 테이블이 있다고 가정 합니다.  
  
 응용 프로그램에서 다음 SQL 문을 지정 하는 경우:  
  
```  
SELECT EMPNO FROM EMPLOYEES WHERE {fn CONVERT(EMPNO,SQL_CHAR)} LIKE '1%'  
```  
  
-   ORACLE 용 드라이버는 SQL 문을 다음과 같이 변환 합니다.  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE to_char(EMPNO) LIKE '1%'  
    ```  
  
-   SQL Server에 대 한 드라이버는 SQL 문을로 변환 합니다.  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE convert(char,EMPNO) LIKE '1%'  
    ```  
  
 응용 프로그램에서 다음 SQL 문을 지정 하는 경우:  
  
```  
SELECT {fn ABS(EMPNO)}, {fn CONVERT(EMPNAME,SQL_SMALLINT)}  
   FROM EMPLOYEES WHERE EMPNO <> 0  
```  
  
-   ORACLE 용 드라이버는 SQL 문을 다음과 같이 변환 합니다.  
  
    ```  
    SELECT abs(EMPNO), to_number(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```  
  
-   SQL Server에 대 한 드라이버는 SQL 문을로 변환 합니다.  
  
    ```  
    SELECT abs(EMPNO), convert(smallint, EMPNAME) FROM EMPLOYEES  
       WHERE EMPNO <> 0  
    ```  
  
-   Ingres 용 드라이버는 SQL 문을로 변환 합니다.  
  
    ```  
    SELECT abs(EMPNO), int2(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```
