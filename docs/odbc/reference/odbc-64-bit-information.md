---
title: ODBC 64 비트 정보 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ed9851ce-44ee-4c8e-b626-1d0b52da30fe
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b9cb8e3fc42d0ad71ac83f1432c165f243f39012
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298303"
---
# <a name="odbc-64-bit-information"></a>ODBC 64비트 정보
Windows Server 2003부터 Microsoft 운영 체제는 64 비트 ODBC 라이브러리를 지원 합니다. MDAC 2.7 SDK와 함께 제공 되는 ODBC 헤더 및 라이브러리에는 프로그래머가 새 64 비트 플랫폼에 대 한 코드를 쉽게 작성할 수 있도록 변경 된 내용이 포함 되어 있습니다. 코드에서 아래 나열 된 ODBC 정의 형식을 사용 하도록 하 여 **_WIN64** 또는 **WIN32** 매크로를 기반으로 64 비트 및 32 비트 플랫폼에 대해 동일한 소스 코드를 컴파일할 수 있습니다.  
  
 64 비트 프로세서를 프로그래밍 하는 경우 다음과 같은 몇 가지 사항을 염두에 두어야 합니다.  
  
-   포인터의 크기가 4 바이트에서 8 바이트로 변경 되었지만 정수 및 long는 여전히 4 바이트 값입니다. **INT64** 및 **UINT64** 형식은 8 바이트 정수에 대해 정의 되었습니다. 새 ODBC 유형인 **Sqllen** 및 **sqlulen** 은 **_WIN64** 정의 된 경우 Odbc 헤더 파일에서 **INT64** 및 **UINT64** 로 정의 됩니다.  
  
-   ODBC의 여러 함수는 포인터 매개 변수를 가져오는 것으로 선언 됩니다. 32 비트 ODBC에서 포인터로 정의 된 매개 변수는 호출의 컨텍스트에 따라 정수 값 또는 버퍼에 대 한 포인터를 전달 하는 데 자주 사용 됩니다. 물론 포인터와 정수의 크기가 동일 하기 때문에 가능 합니다. 64 비트 Windows에서는 그렇지 않습니다.  
  
-   이전에 **Sqlinteger** 및 **SQLUINTEGER** 매개 변수를 사용 하 여 정의 된 일부 ODBC 함수가 새로운 **Sqlinteger** 및 **sqlulen** typedef를 사용 하도록 적절 하 게 변경 되었습니다. 이러한 변경 내용은 다음 섹션인 함수 선언 변경 내용에 나와 있습니다.  
  
-   다양 한 **sqlset** 및 **sqlset** 함수를 통해 설정할 수 있는 일부 설명자 필드는 64 비트 값을 수용할 수 있도록 변경 되었으며, 다른 일부는 여전히 32 비트 값입니다. 이러한 필드를 설정 하 고 검색할 때 적절 한 크기의 변수를 사용 해야 합니다. 변경 된 설명자 필드에 대 한 세부 정보는 함수 선언 변경 아래에 나열 됩니다.  
  
## <a name="function-declaration-changes"></a>함수 선언 변경  
 64 비트 프로그래밍에 대해 다음과 같은 함수 시그니처가 변경 되었습니다. 굵은 텍스트의 항목은 서로 다른 특정 매개 변수입니다.  
  
```cpp
SQLBindCol (SQLHSTMT StatementHandle, SQLUSMALLINT ColumnNumber,  
   SQLSMALLINT TargetType, SQLPOINTER TargetValuePtr, SQLLEN BufferLength,   SQLLEN * StrLen_or_Ind);  
  
SQLBindParam (SQLHSTMT StatementHandle, SQLUSMALLINT ParameterNumber,  
   SQLSMALLINT ValueType, SQLSMALLINT ParameterType,   
   SQLULEN ColumnSize, SQLSMALLINT DecimalDigits,   
   SQLPOINTER ParameterValuePtr, SQLLEN *StrLen_or_Ind);  
  
SQLBindParameter (SQLHSTMT StatementHandle, SQLUSMALLINT ParameterNumber,   
   SQLSMALLINT InputOutputType, SQLSMALLINT ValueType,   
   SQLSMALLINT ParameterType, SQLULEN ColumnSize, SQLSMALLINT DecimalDigits,   
   SQLPOINTER ParameterValuePtr, SQLLEN BufferLength, SQLLEN *StrLen_or_IndPtr);  
  
SQLColAttribute (SQLHSTMT StatementHandle, SQLUSMALLINT ColumnNumber,  
    SQLUSMALLINT FieldIdentifier, SQLPOINTER CharacterAttributePtr,   
   SQLSMALLINT BufferLength, SQLSMALLINT * StringLengthPtr,   
   SQLLEN* NumericAttributePtr)  
  
SQLColAttributes (SQLHSTMT hstmt, SQLUSMALLINT icol,   
   SQLUSMALLINT fDescType, SQLPOINTER rgbDesc,   
   SQLSMALLINT cbDescMax, SQLSMALLINT *pcbDesc, SQLLEN * pfDesc);  
  
SQLDescribeCol (SQLHSTMT StatementHandle, SQLUSMALLINT ColumnNumber,   
   SQLCHAR *ColumnName, SQLSMALLINT BufferLength,   
   SQLSMALLINT *NameLengthPtr, SQLSMALLINT *DataTypePtr, SQLULEN *ColumnSizePtr,   
   SQLSMALLINT *DecimalDigitsPtr, SQLSMALLINT *NullablePtr);  
  
SQLDescribeParam (SQLHSTMT StatementHandle, SQLUSMALLINT ParameterNumber,   
   SQLSMALLINT *DataTypePtr, SQLULEN *ParameterSizePtr, SQLSMALLINT *DecimalDigitsPtr,   
   SQLSMALLINT *NullablePtr);  
  
SQLExtendedFetch(SQLHSTMT StatementHandle, SQLUSMALLINT FetchOrientation, SQLLEN FetchOffset,   
   SQLULEN * RowCountPtr, SQLUSMALLINT * RowStatusArray);  
  
SQLFetchScroll (SQLHSTMT StatementHandle, SQLSMALLINT FetchOrientation,   
   SQLLEN FetchOffset);  
  
SQLGetData (SQLHSTMT StatementHandle, SQLUSMALLINT ColumnNumber,   
   SQLSMALLINT TargetType, SQLPOINTER TargetValuePtr, SQLLEN BufferLength,    SQLLEN *StrLen_or_Ind);  
  
SQLGetDescRec (SQLHDESC DescriptorHandle, SQLSMALLINT RecNumber,   
   SQLCHAR *Name, SQLSMALLINT BufferLength,   
   SQLSMALLINT *StringLengthPtr, SQLSMALLINT *TypePtr,   
   SQLSMALLINT *SubTypePtr, SQLLEN *LengthPtr,   
   SQLSMALLINT *PrecisionPtr, SQLSMALLINT *ScalePtr,   
   SQLSMALLINT *NullablePtr);  
  
SQLParamOptions(SQLHSTMT hstmt, SQLULEN crow, SQLULEN * pirow);  
  
SQLPutData (SQLHSTMT StatementHandle, SQLPOINTER DataPtr,   
   SQLLEN StrLen_or_Ind);  
  
SQLRowCount (SQLHSTMT StatementHandle, SQLLEN* RowCountPtr);  
  
SQLSetConnectOption(SQLHDBC ConnectHandle, SQLUSMALLINT Option,   
   SQLULEN Value);  
  
SQLSetPos (SQLHSTMT StatementHandle, SQLSETPOSIROW RowNumber, SQLUSMALLINT Operation,  
   SQLUSMALLINT LockType);  
  
SQLSetParam (SQLHSTMT StatementHandle, SQLUSMALLINT ParameterNumber,   
   SQLSMALLINT ValueType, SQLSMALLINT ParameterType,   
   SQLULEN LengthPrecision, SQLSMALLINT ParameterScale,   
   SQLPOINTER ParameterValue, SQLLEN *StrLen_or_Ind);  
  
SQLSetDescRec (SQLHDESC DescriptorHandle, SQLSMALLINT RecNumber,   
   SQLSMALLINT Type, SQLSMALLINT SubType, SQLLEN Length,   
   SQLSMALLINT Precision, SQLSMALLINT Scale, SQLPOINTER DataPtr,   
   SQLLEN *StringLengthPtr, SQLLEN *IndicatorPtr);  
  
SQLSetScrollOptions (SQLHSTMT hstmt, SQLUSMALLINT fConcurrency,   
   SQLLEN crowKeyset, SQLUSMALLINT crowRowset);  
  
SQLSetStmtOption (SQLHSTMT StatementHandle, SQLUSMALLINT Option,   
   SQLULEN Value);  
```  
  
## <a name="changes-in-sql-data-types"></a>SQL 데이터 형식의 변경 내용  
 다음 네 가지 SQL 형식은 여전히 32 비트 에서만 지원 됩니다. 64 비트 컴파일러에는 정의 되어 있지 않습니다. 이러한 형식은 MDAC 2.7의 모든 매개 변수에 더 이상 사용 되지 않습니다. 이러한 형식을 사용 하면 64 비트 플랫폼에서 컴파일러 오류가 발생 합니다.  
  
```cpp
#ifdef WIN32   
typedef SQLULEN SQLROWCOUNT;   
typedef SQLULEN SQLROWSETSIZE;   
typedef SQLULEN SQLTRANSID;   
typedef SQLLEN SQLROWOFFSET;   
#endif  
```  
  
 32 비트 및 64 비트 컴파일러에 대해 SQLSETPOSIROW의 정의가 변경 되었습니다.  
  
```cpp
#ifdef _WIN64   
typedef UINT64 SQLSETPOSIROW;   
#else   
#define SQLSETPOSIROW SQLUSMALLINT   
#endif  
```  
  
 64 비트 컴파일러의 경우 SQLLEN 및 SQLULEN의 정의가 변경 되었습니다.  
  
```cpp
#ifdef _WIN64   
typedef INT64 SQLLEN;   
typedef UINT64 SQLULEN;   
#else   
#define SQLLEN SQLINTEGER   
#define SQLULEN SQLUINTEGER   
#endif  
```  
  
 SQL_C_BOOKMARK는 ODBC 3.0에서 더 이상 사용 되지 않지만 2.0 클라이언트의 64 비트 컴파일러에서는이 값이 변경 되었습니다.  
  
```cpp
#ifdef _WIN64   
#define SQL_C_BOOKMARK SQL_C_UBIGINT   
#else   
#define SQL_C_BOOKMARK SQL_C_ULONG   
#endif  
```  
  
 책갈피 형식은 새 헤더에서 다르게 정의 됩니다.  
  
```cpp
typedef SQLULEN BOOKMARK;  
```  
  
## <a name="values-returned-from-odbc-api-calls-through-pointers"></a>포인터를 통해 ODBC API 호출에서 반환 되는 값  
 다음 ODBC 함수 호출은 데이터를 드라이버에서 반환 하는 버퍼에 대 한 포인터를 입력 매개 변수로 사용 합니다. 반환 되는 데이터의 컨텍스트 및 의미는 함수에 대 한 다른 입력 매개 변수에 의해 결정 됩니다. 경우에 따라 이러한 메서드는 일반적인 32 비트 (4 바이트) 정수 값 대신 64 비트 (8 바이트 정수) 값을 반환할 수 있습니다. 이러한 경우는 다음과 같습니다.  
  
 **SQLColAttribute**  
  
 *FieldIdentifier* 매개 변수에 다음 값 중 하나가 있는 경우 **NumericAttribute*에 64 비트 값이 반환 됩니다.  
  
 SQL_DESC_AUTO_UNIQUE_VALUE  
  
 SQL_DESC_CASE_SENSITIVE  
  
 SQL_DESC_CONCISE_TYPE  
  
 SQL_DESC_COUNT  
  
 SQL_DESC_DISPLAY_SIZE  
  
 SQL_DESC_FIXED_PREC_SCALE  
  
 SQL_DESC_LENGTH  
  
 SQL_DESC_NULLABLE  
  
 SQL_DESC_NUM_PREC_RADIX  
  
 SQL_DESC_OCTET_LENGTH  
  
 SQL_DESC_PRECISION  
  
 SQL_DESC_SCALE  
  
 SQL_DESC_SEARCHABLE  
  
 SQL_DESC_TYPE  
  
 SQL_DESC_UNNAMED  
  
 SQL_DESC_UNSIGNED  
  
 SQL_DESC_UPDATABLE  
  
 **SQLColAttributes**  
  
 *FDescType* 매개 변수에 다음 값 중 하나가 있는 경우 **pfDesc*에 64 비트 값이 반환 됩니다.  
  
 SQL_COLUMN_COUNT  
  
 SQL_COLUMN_DISPLAY_SIZE  
  
 SQL_COLUMN_LENGTH  
  
 SQL_DESC_AUTO_UNIQUE_VALUE  
  
 SQL_DESC_CASE_SENSITIVE  
  
 SQL_DESC_CONCISE_TYPE  
  
 SQL_DESC_FIXED_PREC_SCALE  
  
 SQL_DESC_SEARCHABLE  
  
 SQL_DESC_UNSIGNED  
  
 SQL_DESC_UPDATABLE  
  
 **SQLGetConnectAttr**  
  
 *특성* 매개 변수에 다음 값 중 하나가 있으면 *값*에 64 비트 값이 반환 됩니다.  
  
 SQL_ATTR_ASYNC_ENABLE  
  
 SQL_ATTR_ENLIST_IN_DTC  
  
 SQL_ATTR_ODBC_CURSORS  
  
 SQL_ATTR_QUIET_MODE  
  
 **SQLGetConnectOption**  
  
 *특성* 매개 변수에 다음 값 중 하나가 있으면 *값*에 64 비트 값이 반환 됩니다.  
  
 SQL_ATTR_QUIET_MODE  
  
 **SQLGetDescField**  
  
 *FieldIdentifier* 매개 변수에 다음 값 중 하나를 사용할 경우 **valueptr*에서 64 비트 값이 반환 됩니다.  
  
 SQL_DESC_ARRAY_SIZE  
  
 SQL_DESC_ARRAY_STATUS_PTR  
  
 SQL_DESC_BIND_OFFSET_PTR  
  
 SQL_DESC_DATA_PTR  
  
 SQL_DESC_DISPLAY_SIZE  
  
 SQL_DESC_INDICATOR_PTR  
  
 SQL_DESC_LENGTH  
  
 SQL_DESC_OCTET_LENGTH  
  
 SQL_DESC_OCTET_LENGTH_PTR  
  
 SQL_DESC_ROWS_PROCESSED_PTR  
  
 **SQLGetDiagField**  
  
 *DiagIdentifier* 매개 변수에 다음 값 중 하나가 있는 경우 **DiagInfoPtr*에 64 비트 값이 반환 됩니다.  
  
 SQL_DIAG_CURSOR_ROW_COUNT  
  
 SQL_DIAG_ROW_COUNT  
  
 SQL_DIAG_ROW_NUMBER  
  
 **SQLGetInfo**  
  
 *InfoType* 매개 변수에 다음 값 중 하나가 있는 경우 **Infovalueptr*에서 64 비트 값이 반환 됩니다.  
  
 SQL_DRIVER_HDBC  
  
 SQL_DRIVER_HENV  
  
 SQL_DRIVER_HLIB  
  
 *InfoType* 에 다음 두 값 중 하나가 있는 경우 **Infovalueptr* 은 입력 및 출력 모두에서 64 비트입니다.  
  
 SQL_DRIVER_HDESC  
  
 SQL_DRIVER_HSTMT  
  
 **SQLGetStmtAttr**  
  
 *특성* 매개 변수에 다음 값 중 하나를 사용할 경우 **valueptr*에서 64 비트 값이 반환 됩니다.  
  
 SQL_ATTR_APP_PARAM_DESC  
  
 SQL_ATTR_APP_ROW_DESC  
  
 SQL_ATTR_ASYNC_ENABLE  
  
 SQL_ATTR_CONCURRENCY  
  
 SQL_ATTR_CURSOR_SCROLLABLE  
  
 SQL_ATTR_CURSOR_SENSITIVITY  
  
 SQL_ATTR_CURSOR_TYPE  
  
 SQL_ATTR_ENABLE_AUTO_IPD  
  
 SQL_ATTR_FETCH_BOOKMARK_PTR  
  
 SQL_ATTR_ROWS_FETCHED_PTR  
  
 SQL_ATTR_IMP_PARAM_DESC  
  
 SQL_ATTR_IMP_ROW_DESC  
  
 SQL_ATTR_KEYSET_SIZE  
  
 SQL_ATTR_MAX_LENGTH  
  
 SQL_ATTR_MAX_ROWS  
  
 SQL_ATTR_METADATA_ID  
  
 SQL_ATTR_NOSCAN  
  
 SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
 SQL_ATTR_PARAM_BIND_TYPE  
  
 SQL_ATTR_PARAM_OPERATION_PTR  
  
 SQL_ATTR_PARAM_STATUS_PTR  
  
 SQL_ATTR_PARAMS_PROCESSED_PTR  
  
 SQL_ATTR_PARAMSET_SIZE  
  
 SQL_ATTR_QUERY_TIMEOUT  
  
 SQL_ATTR_RETRIEVE_DATA  
  
 SQL_ATTR_ROW_ARRAY_SIZE  
  
 SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
 SQL_ATTR_ROW_NUMBER  
  
 SQL_ATTR_ROW_OPERATION_PTR  
  
 SQL_ATTR_ROW_STATUS_PTR  
  
 SQL_ATTR_SIMULATE_CURSOR  
  
 SQL_ATTR_USE_BOOKMARKS  
  
 **SQLGetStmtOption**  
  
 *Option* 매개 변수에 다음 값 중 하나를 사용할 경우 **값*에 64 비트 값이 반환 됩니다.  
  
 SQL_KEYSET_SIZE  
  
 SQL_MAX_LENGTH  
  
 SQL_MAX_ROWS  
  
 SQL_ROWSET_SIZE  
  
 **SQLSetConnectAttr**  
  
 *특성* 매개 변수에 다음 값 중 하나가 있는 경우 64 비트 값은 *값*으로 전달 됩니다.  
  
 SQL_ATTR_ASYNC_ENABLE  
  
 SQL_ATTR_ENLIST_IN_DTC  
  
 SQL_ATTR_ODBC_CURSORS  
  
 SQL_ATTR_QUIET_MODE  
  
 **SQLSetConnectOption**  
  
 *특성* 매개 변수에 다음 값 중 하나가 있는 경우 64 비트 값은 *값*으로 전달 됩니다.  
  
 SQL_ATTR_QUIET_MODE  
  
 **SQLSetDescField**  
  
 *FieldIdentifier* 매개 변수에 다음 값 중 하나를 사용할 경우 64 비트 값은 *valueptr*에 전달 됩니다.  
  
 SQL_DESC_ARRAY_SIZE  
  
 SQL_DESC_ARRAY_STATUS_PTR  
  
 SQL_DESC_BIND_OFFSET_PTR  
  
 SQL_DESC_DATA_PTR  
  
 SQL_DESC_DISPLAY_SIZE  
  
 SQL_DESC_INDICATOR_PTR  
  
 SQL_DESC_LENGTH  
  
 SQL_DESC_OCTET_LENGTH  
  
 SQL_DESC_OCTET_LENGTH_PTR  
  
 SQL_DESC_ROWS_PROCESSED_PTR  
  
 **SQLSetStmtAttr**  
  
 *특성* 매개 변수에 다음 값 중 하나가 있는 경우 64 비트 값은 이상 값에 전달 *됩니다.*  
  
 SQL_ATTR_APP_PARAM_DESC  
  
 SQL_ATTR_APP_ROW_DESC  
  
 SQL_ATTR_ASYNC_ENABLE  
  
 SQL_ATTR_CONCURRENCY  
  
 SQL_ATTR_CURSOR_SCROLLABLE  
  
 SQL_ATTR_CURSOR_SENSITIVITY  
  
 SQL_ATTR_CURSOR_TYPE  
  
 SQL_ATTR_ENABLE_AUTO_IPD  
  
 SQL_ATTR_FETCH_BOOKMARK_PTR  
  
 SQL_ATTR_IMP_PARAM_DESC  
  
 SQL_ATTR_IMP_ROW_DESC  
  
 SQL_ATTR_KEYSET_SIZE  
  
 SQL_ATTR_MAX_LENGTH  
  
 SQL_ATTR_MAX_ROWS  
  
 SQL_ATTR_METADATA_ID  
  
 SQL_ATTR_NOSCAN  
  
 SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
 SQL_ATTR_PARAM_BIND_TYPE  
  
 SQL_ATTR_PARAM_OPERATION_PTR  
  
 SQL_ATTR_PARAM_STATUS_PTR  
  
 SQL_ATTR_PARAMS_PROCESSED_PTR  
  
 SQL_ATTR_PARAMSET_SIZE  
  
 SQL_ATTR_QUERY_TIMEOUT  
  
 SQL_ATTR_RETRIEVE_DATA  
  
 SQL_ATTR_ROW_ARRAY_SIZE  
  
 SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
 SQL_ATTR_ROW_NUMBER  
  
 SQL_ATTR_ROW_OPERATION_PTR  
  
 SQL_ATTR_ROW_STATUS_PTR  
  
 SQL_ATTR_ROWS_FETCHED_PTR  
  
 SQL_ATTR_SIMULATE_CURSOR  
  
 SQL_ATTR_USE_BOOKMARKS  
  
 **SQLSetStmtOption**  
  
 *Option* 매개 변수에 다음 값 중 하나가 있는 경우 64 비트 값은 *값*으로 전달 됩니다.  
  
 SQL_KEYSET_SIZE  
  
 SQL_MAX_LENGTH  
  
 SQL_MAX_ROWS  
  
 SQL_ROWSET_SIZE  
  
## <a name="see-also"></a>참고 항목  
 [ODBC 소개](../../odbc/reference/introduction-to-odbc.md)
