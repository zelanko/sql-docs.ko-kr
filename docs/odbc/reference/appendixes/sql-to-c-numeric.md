---
title: 'SQL에서 C로: Numeric | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from SQL to C types [ODBC], numeric
- numeric data type [ODBC], converting
- converting data from SQL to C types [ODBC], numeric
ms.assetid: 76f8b5d5-4bd0-4dcb-a90a-698340e0d36e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a23e60b161c09367cfb079cea1f7ca146b4ebee5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68056854"
---
# <a name="sql-to-c-numeric"></a>SQL에서 C로: 숫자

숫자 ODBC SQL 데이터 형식에 대 한 식별자는 다음과 같습니다.

- SQL_DECIMAL  
- SQL_BIGINT  
- SQL_NUMERIC  
- SQL_REAL  
- SQL_TINYINT  
- SQL_FLOAT  
- SQL_SMALLINT  
- SQL_DOUBLE SQL_INTEGER  

다음 표에서는 숫자 SQL 데이터가 변환 될 수 있는 ODBC C 데이터 형식을 보여 줍니다. 테이블의 열 및 용어에 대 한 설명은 [SQL에서 C 데이터 형식으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)을 참조 하세요.  

|C 형식 식별자|테스트|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|바이트 길이 < *Bufferlength*<br /><br /> *Bufferlength* < 소수 자릿수가 아니라 전체 수입니다.<br /><br /> 전체 수 (소수 자릿수가 아닌) >= *Bufferlength*|data<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|데이터의 길이 (바이트)<br /><br /> 데이터의 길이 (바이트)<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|문자 길이 < *Bufferlength*<br /><br /> *Bufferlength* < 소수 자릿수가 아니라 전체 수입니다.<br /><br /> 전체 수 (소수 자릿수가 아닌) >= *Bufferlength*|data<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|데이터의 길이 (문자)<br /><br /> 데이터의 길이 (문자)<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_NUMERIC|잘림 없이 변환 된 데이터 [a]<br /><br /> 소수 자릿수가 잘린 상태로 변환 된 데이터 [a]<br /><br /> 데이터를 변환 하면 소수 자릿수가 아니라 전체 손실이 발생 합니다. [a]|data<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|C 데이터 형식의 크기<br /><br /> C 데이터 형식의 크기<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01S07<br /><br /> 22003|  
|SQL_C_FLOAT<br /><br /> SQL_C_DOUBLE|데이터가 변환 되는 데이터 형식의 범위 내에 있는 경우 [a]<br /><br /> 데이터가 변환 되는 데이터 형식의 범위를 벗어났습니다. [a]|data<br /><br /> 정의되지 않음|C 데이터 형식의 크기<br /><br /> 정의되지 않음|해당 없음<br /><br /> 22003|  
|SQL_C_BIT|데이터가 0 또는 1 인 경우 [a]<br /><br /> 데이터가 0 보다 크고 2 보다 작고 1 [a]와 같지 않습니다.<br /><br /> 데이터가 0 보다 작거나 2 [a] 보다 크거나 같습니다.|data<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|1 [b]<br /><br /> 1 [b]<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01S07<br /><br /> 22003|  
|SQL_C_BINARY|데이터의 바이트 길이 <= *Bufferlength*<br /><br /> *Bufferlength* > 데이터의 바이트 길이|data<br /><br /> 정의되지 않음|데이터 길이<br /><br /> 정의되지 않음|해당 없음<br /><br /> 22003|  
|SQL_C_INTERVAL_MONTH [c] SQL_C_INTERVAL_YEAR [c] SQL_C_INTERVAL_DAY [c] SQL_C_INTERVAL_HOUR [c] SQL_C_INTERVAL_MINUTE [c] SQL_C_INTERVAL_SECOND [c]|데이터가 잘리지 않음<br /><br /> 소수 자릿수 초 부분이 잘렸습니다.<br /><br /> 잘린 숫자의 전체 부분|data<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|데이터의 길이 (바이트)<br /><br /> 데이터의 길이 (바이트)<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_INTERVAL_YEAR_TO_MONTH SQL_C_INTERVAL_DAY_TO_HOUR SQL_C_INTERVAL_DAY_TO_MINUTE SQL_C_INTERVAL_DAY_TO_SECOND SQL_C_INTERVAL_HOUR_TO_MINUTE SQL_C_INTERVAL_HOUR_TO_SECOND|잘린 숫자의 전체 부분|정의되지 않음|정의되지 않음|22015|  
  
 [a]이 변환에서 *Bufferlength* 값은 무시 됩니다. 이 드라이버는 **Targetvalueptr* 의 크기가 C 데이터 형식의 크기인 것으로 가정 합니다.  
  
 [b] 해당 C 데이터 형식의 크기입니다.  
  
 [c]이 변환은 정확한 숫자 데이터 형식 (SQL_DECIMAL, SQL_NUMERIC, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER 및 SQL_BIGINT)에 대해서만 지원 됩니다. 근사 숫자 데이터 형식 (SQL_REAL, SQL_FLOAT 또는 SQL_DOUBLE)에 대해서는 지원 되지 않습니다.  

## <a name="sql_c_numeric-and-sqlsetdescfield"></a>SQL_C_NUMERIC 및 SQLSetDescField

 [SQLSetDescField 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 는 SQL_C_NUMERIC 값을 사용 하 여 수동 바인딩을 수행 하는 데 필요 합니다. SQLSetDescField는 ODBC 3.0에 추가 되었습니다. 수동 바인딩을 수행 하려면 먼저 설명자 핸들을 가져와야 합니다.  

```cpp
if (fCType == SQL_C_NUMERIC) {   
   // special processing required for NUMERIC to get right scale & precision  
   // Modify the fields in the implicit application parameter descriptor  
   SQLHDESC hdesc=NULL;  
  
   // Use SQL_ATTR_APP_ROW_DESC for calls to SQLBindCol()  
   // Use SQL_ATTR_APP_PARAM_DESC for calls to SQLBindParameter()  
   //  
   // retcode = SQLGetStmtAttr(hstmt, SQL_ATTR_APP_ROW_DESC, &hdesc, 0, NULL);  
   retcode = SQLGetStmtAttr(hstmt, SQL_ATTR_APP_PARAM_DESC, &hdesc, 0, NULL);  
   if (!ODBC_CALL_SUCCESS(retcode)) {  
      printf ("\nSQLGetStmtAttr failed");  
      i = 1;  
      sqlstate[7] = '\0';  
      while (SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, i, sqlstate, &NativeError, wrkbuf, sizeof(wrkbuf), &len) != SQL_NO_DATA) {  
         printf("\niTestCase = %d Failed...Precision = %d, Scale = %d\nNativeError=%d, State=%s, \n  Message=%s",   
            iTestCase, Precision, Scale, NativeError, sqlstate, wrkbuf);  
         i++;  
      }  
      continue;  
   }  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_TYPE, (SQLPOINTER) SQL_C_NUMERIC, 0);  
   if (!ODBC_CALL_SUCCESS(retcode))  
      goto error;  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_PRECISION, (SQLPOINTER)num.precision, 0);  
   if (!ODBC_CALL_SUCCESS(retcode))  
      goto error;  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_SCALE, (SQLPOINTER)num.scale, 0);  
   if (!ODBC_CALL_SUCCESS(retcode))  
      goto error;  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_DATA_PTR, (SQLPOINTER) &(num), sizeof(num));  
```
