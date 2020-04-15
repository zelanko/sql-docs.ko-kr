---
title: 'SQL 에서 C까지: 숫자 | 마이크로 소프트 문서'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 36b24da4023a96b686742416b83bb5790e129278
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296413"
---
# <a name="sql-to-c-numeric"></a>SQL에서 C로: 숫자

숫자 ODBC SQL 데이터 형식의 식별자는 다음과 같습니다.

- SQL_DECIMAL  
- SQL_BIGINT  
- SQL_NUMERIC  
- SQL_REAL  
- SQL_TINYINT  
- SQL_FLOAT  
- SQL_SMALLINT  
- SQL_DOUBLE SQL_INTEGER  

다음 표에서는 숫자 SQL 데이터를 변환할 수 있는 ODBC C 데이터 형식을 보여 주며 있습니다. 표의 열 및 용어에 대한 설명은 [SQL에서 C 데이터 유형으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)을 참조하십시오.  

|C 유형 식별자|테스트|**대상 밸류프트*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|문자 바이트 길이 < *버퍼길이*<br /><br /> *버퍼길이에* < 전체 자릿수(소수와 반대) 자릿수<br /><br /> 전체 숫자(소수와 반대) >= *버퍼길이*|데이터<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|바이트 내 데이터 길이<br /><br /> 바이트 내 데이터 길이<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|문자 길이 < *버퍼길이*<br /><br /> *버퍼길이에* < 전체 자릿수(소수와 반대) 자릿수<br /><br /> 전체 숫자(소수와 반대) >= *버퍼길이*|데이터<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|문자로 된 데이터 길이<br /><br /> 문자로 된 데이터 길이<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_NUMERIC|잘리지 않고 변환된 데이터[a]<br /><br /> 소수 자릿수의 잘림으로 변환된 데이터[a]<br /><br /> 데이터를 변환하면 전체(소수와 는 반대)가 손실됩니다[a]|데이터<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|C 데이터 형식의 크기<br /><br /> C 데이터 형식의 크기<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01S07<br /><br /> 22003|  
|SQL_C_FLOAT<br /><br /> SQL_C_DOUBLE|데이터가 변환되는 데이터 형식의 범위 내에 있습니다[a]<br /><br /> 데이터가 변환되는 데이터 형식의 범위를 벗어났습니다[a]|데이터<br /><br /> 정의되지 않음|C 데이터 형식의 크기<br /><br /> 정의되지 않음|해당 없음<br /><br /> 22003|  
|SQL_C_BIT|데이터는 0 또는 1[a]<br /><br /> 데이터가 0보다 크고 2보다 크며 1[a] 같지 않음<br /><br /> 데이터가 0보다 크거나 2[a]|데이터<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|1[b]<br /><br /> 1[b]<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01S07<br /><br /> 22003|  
|SQL_C_BINARY|데이터 <바이트 길이 = *버퍼길이*<br /><br /> *버퍼길이>* 데이터의 바이트 길이|데이터<br /><br /> 정의되지 않음|데이터 길이<br /><br /> 정의되지 않음|해당 없음<br /><br /> 22003|  
|SQL_C_INTERVAL_MONTH[c] SQL_C_INTERVAL_YEAR[c] SQL_C_INTERVAL_DAY[c] SQL_C_INTERVAL_HOUR[c] SQL_C_INTERVAL_MINUTE[c] SQL_C_INTERVAL_SECOND[c]|데이터가 잘리지 않음<br /><br /> 잘린 분수 초 부분<br /><br /> 잘린 숫자의 전체 부분|데이터<br /><br /> 잘린 데이터<br /><br /> 정의되지 않음|바이트 내 데이터 길이<br /><br /> 바이트 내 데이터 길이<br /><br /> 정의되지 않음|해당 없음<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_INTERVAL_YEAR_TO_MONTH SQL_C_INTERVAL_DAY_TO_HOUR SQL_C_INTERVAL_DAY_TO_MINUTE SQL_C_INTERVAL_DAY_TO_SECOND SQL_C_INTERVAL_HOUR_TO_MINUTE SQL_C_INTERVAL_HOUR_TO_SECOND|잘린 숫자의 전체 부분|정의되지 않음|정의되지 않음|22015|  
  
 [a] 이 변환에 대해 *BufferLength* 의 값은 무시됩니다. 드라이버는 **TargetValuePtr의* 크기가 C 데이터 형식의 크기라고 가정합니다.  
  
 [b] 해당 C 데이터 형식의 크기입니다.  
  
 [c] 이 변환은 정확한 숫자 데이터 유형(SQL_DECIMAL, SQL_NUMERIC, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER 및 SQL_BIGINT)에 대해서만 지원됩니다. 대략적인 숫자 데이터 유형(SQL_REAL, SQL_FLOAT 또는 SQL_DOUBLE)에는 지원되지 않습니다.  

## <a name="sql_c_numeric-and-sqlsetdescfield"></a>SQL_C_NUMERIC 및 SQLSetDescField

 [SQLSetDescField 함수는](../../../odbc/reference/syntax/sqlsetdescfield-function.md) SQL_C_NUMERIC 값으로 수동 바인딩을 수행해야 합니다. (SQLSetDescField는 ODBC 3.0에 추가되었습니다.) 수동 바인딩을 수행하려면 먼저 설명자 핸들을 얻어야 합니다.  

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
