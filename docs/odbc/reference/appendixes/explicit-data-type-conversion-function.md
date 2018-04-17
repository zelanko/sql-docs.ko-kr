---
title: 명시적 데이터 형식 변환 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- explicit data type conversion functions [ODBC]
- data type conversion functions [ODBC]
- functions [ODBC], explicit data type conversion functions
ms.assetid: d5789450-b668-4753-96c8-6789e955e7ed
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e86113ed304bc0876ce961e4c8691f53e9065d1b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="explicit-data-type-conversion-function"></a>명시적 데이터 형식 변환 함수
명시적 데이터 형식 변환이 SQL 데이터 형식 정의 기준으로 지정 됩니다.  
  
 명시적 데이터 형식 변환 함수에 대 한 ODBC 구문을 변환을 제한 하지 않습니다. 다른 데이터 형식으로 한 데이터 형식의 특정 변환의 유효성을 검사 각 드라이버 관련 구현에 의해 결정 됩니다. 드라이버는, ODBC 구문을 네이티브 구문으로 변환 하는 대로 거부 없더라도 ODBC 구문에는 데이터 원본에서 지원 되지 않는 변환 합니다. ODBC 함수 **SQLGetInfo**, 변환을 옵션 (예: SQL_CONVERT_BIGINT, SQL_CONVERT_BINARY, SQL_CONVERT_INTERVAL_YEAR_MONTH, 및 등)는 데이터 원본에서 지 원하는 변환 하는 방법을 확인 하는 방법을 제공 .  
  
 형식은 **변환** 함수는:  
  
 **변환 (** *value_exp*, *data_type * * *)**  
  
 함수에 지정 된 값을 반환 *value_exp* 지정 된 변환 *data_type*여기서 *data_type* 다음 키워드 중 하나입니다.  
  
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
  
 명시적 데이터 형식 변환 함수에 대 한 ODBC 구문을 변환 형식 사양을 지원 하지 않습니다. 명시적 형식 지정 데이터 원본으로 사용할 수, 드라이버 기본값을 지정 하거나 형식 지정을 구현 해야 합니다.  
  
 인수 *value_exp* 열 이름, 결과 다른 스칼라 함수 이거나 숫자 또는 문자열 리터럴일 수 있습니다. 예를 들어:  
  
```  
{ fn CONVERT( { fn CURDATE() }, SQL_CHAR ) }  
```  
  
 CURDATE 스칼라 함수의 출력을 문자열로 변환합니다.  
  
 반환 값에 대 한 데이터 형식을 ODBC는 필요 하지 않습니다 (함수 경우가 많기 때문에 데이터 원본에 따른 특정) 스칼라 함수 이므로 응용 프로그램 데이터 형식 변환을 강제 실행 가능 하면 CONVERT 스칼라 함수를 사용 해야 합니다.  
  
 다음 두 예제는 사용법을 보여 줍니다.는 **변환** 함수입니다. 이 예제에서는 직원, 열이 있는 EMPNO SQL_SMALLINT 유형의 테이블과 SQL_CHAR 유형의 EMPNAME 열 이라고 하는 테이블의 존재 여부를 가정 합니다.  
  
 다음 SQL 문을 지정 하는 응용 프로그램:  
  
```  
SELECT EMPNO FROM EMPLOYEES WHERE {fn CONVERT(EMPNO,SQL_CHAR)} LIKE '1%'  
```  
  
-   ORACLE에 대 한 드라이버 변환 SQL 문입니다.  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE to_char(EMPNO) LIKE '1%'  
    ```  
  
-   SQL Server에 대 한 드라이버 변환 SQL 문입니다.  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE convert(char,EMPNO) LIKE '1%'  
    ```  
  
 다음 SQL 문을 지정 하는 응용 프로그램:  
  
```  
SELECT {fn ABS(EMPNO)}, {fn CONVERT(EMPNAME,SQL_SMALLINT)}  
   FROM EMPLOYEES WHERE EMPNO <> 0  
```  
  
-   ORACLE에 대 한 드라이버 변환 SQL 문입니다.  
  
    ```  
    SELECT abs(EMPNO), to_number(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```  
  
-   SQL Server에 대 한 드라이버 변환 SQL 문입니다.  
  
    ```  
    SELECT abs(EMPNO), convert(smallint, EMPNAME) FROM EMPLOYEES  
       WHERE EMPNO <> 0  
    ```  
  
-   Ingres에 대 한 드라이버 변환 SQL 문입니다.  
  
    ```  
    SELECT abs(EMPNO), int2(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```
