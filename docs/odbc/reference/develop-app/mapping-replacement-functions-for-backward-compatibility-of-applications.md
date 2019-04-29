---
title: 앱-ODBC의 호환성을 위한 대체 함수 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping replacement functions [ODBC]
- upgrading applications [ODBC], mapping replacement functions
- compatibility [ODBC], mapping replacement functions
- ODBC drivers [ODBC], backward compatibility
- functions [ODBC], mapping replacement functions
- application upgrades [ODBC], mapping replacement functions
- backward compatibility [ODBC], mapping replacement functions
ms.assetid: f5e6d9da-76ef-42cb-b3f5-f640857df732
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6cecc7fcd5ffa7234544dd0a9bc10407b1ea5cb1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63032831"
---
# <a name="mapping-replacement-functions-for-backward-compatibility-of-applications"></a>애플리케이션의 이전 버전과의 호환성을 위한 대체 함수 매핑
ODBC 3 *.x* ODBC 3을 통해 작업 응용 프로그램 *.x* 드라이버 관리자는 ODBC 2에 대해 작동 합니다. *x* 드라이버 없는 새 기능을 사용 하기만 합니다. 그러나 모두 중복 기능 및 변경 된 동작 방식에 영향 그렇게 하는 ODBC 3. *x* 응용 프로그램 작동에 ODBC 2. *x* 드라이버입니다. ODBC 2 작업할 때. *x* 드라이버를 드라이버 관리자 매핑됩니다 다음 ODBC 3. *x* 함수를 하나 이상의 ODBC 2를 대체 했습니다. *x* 함수에 해당 하는 ODBC 2. *x* 함수입니다.  
  
|ODBC 3입니다. *x* 함수|ODBC 2입니다. *x* 함수|  
|-------------------------|-------------------------|  
|**SQLAllocHandle**|**SQLAllocEnv**, **SQLAllocConnect**, or **SQLAllocStmt**|  
|**SQLBulkOperations**|**SQLSetPos**|  
|**SQLColAttribute**|**SQLColAttributes**|  
|**SQLEndTran**|**SQLTransact**|  
|**SQLFetch**|**SQLExtendedFetch**|  
|**SQLFetchScroll**|**SQLExtendedFetch**|  
|**SQLFreeHandle**|**SQLFreeEnv**, **SQLFreeConnect**, or **SQLFreeStmt**|  
|**SQLGetConnectAttr**|**SQLGetConnectOption**|  
|**SQLGetDiagRec**|**SQLError**|  
|**SQLGetStmtAttr**|**SQLGetStmtOption**[1]|  
|**SQLSetConnectAttr**|**SQLSetConnectOption**|  
|**SQLSetStmtAttr**|**SQLSetStmtOption**[1]|  
  
 [1] 다른 작업이 요청 되는 특성에 따라 수행도 될 수 있습니다.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
 드라이버 관리자는이를 매핑합니다 **SQLAllocEnv**하십시오 **SQLAllocConnect**, 또는 **SQLAllocStmt**를 적절 하 게 합니다. 다음에 호출할 **SQLAllocHandle**:  
  
```  
SQLAllocHandle(HandleType, InputHandle, OutputHandlePtr);  
```  
  
 드라이버 관리자는 다음을 수행 하면 (개념적에서 오류 검사) 매핑:  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLAllocEnv(OutputHandlePtr));  
   case SQL_HANDLE_DBC: return (SQLAllocConnect (InputHandle, OutputHandlePtr));  
   case SQL_HANDLE_STMT: return (SQLAllocStmt (InputHandle, OutputHandlePtr));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlbulkoperations"></a>SQLBulkOperations  
 드라이버 관리자는이를 매핑합니다 **SQLSetPos**합니다. 다음에 호출할 **SQLBulkOperations**:  
  
```  
SQLBulkOperations(hstmt, Operation);  
```  
  
 단계의 다음 시퀀스에서는 발생 됩니다.  
  
1.  드라이버 관리자를 호출 하는 작업 인수가 SQL_ADD **SQLSetPos** 다음과 같습니다.  
  
    ```  
    SQLSetPos (hstmt, 0, SQL_ADD, SQL_LOCK_NO_CHANGE);  
    ```  
  
2.  연산 인수 SQL_ADD 없으면 드라이버에서 SQLSTATE HY092 반환 합니다 (잘못 된 특성/옵션 식별자)입니다.  
  
3.  응용 프로그램에 대 한 호출 간의 SQL_ATTR_ROW_STATUS_PTR을 변경 하려고 할 경우 **SQLFetch** 하거나 **SQLFetchScroll** 하 고 **SQLBulkOperations**, 드라이버 관리자는 SQLSTATE HY011 반환 (특성 지금 설정할 수 없습니다).  
  
4.  연산 인수 SQL_ADD 인 경우에 응용 프로그램 호출 해야 합니다 **SQLBindCol** 삽입할 데이터를 바인딩할 합니다. 호출할 수 없습니다 **SQLSetDescField** 하거나 **SQLSetDescRec** 삽입할 데이터를 바인딩할 합니다.  
  
5.  연산 인수는 SQL_ADD 행을 삽입할 수 없는 경우 현재 행 집합 크기와 동일 **SQLSetStmtAttr** SQL_ATTR_ROW_ARRAY_SIZE 문 특성 수에 행 수를 설정 하려면 호출 해야 호출 앞에 삽입 **SQLBulkOperations**합니다. 응용 프로그램 해야 앞 SQL_ATTR_ROW_ARRAY_SIZE 문 특성을 설정 하는 데 이전 행 집합 크기로 다시 되돌리려면 **SQLFetch**를 **SQLFetchScroll**, 또는 **SQLSetPos**라고 합니다.  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
 드라이버 관리자는이를 매핑합니다 **SQLColAttributes**합니다. 다음에 호출할 **SQLColAttribute**:  
  
```  
SQLColAttribute(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
```  
  
 단계의 다음 시퀀스에서는 발생 됩니다.  
  
1.  하는 경우 *FieldIdentifier* 다음 중 하나입니다.  
  
     SQL_DESC_PRECISION, 자릿수가 SQL_DESC_SCALE, SQL_DESC_LENGTH, SQL_DESC_OCTET_LENGTH, SQL_DESC_UNNAMED, SQL_DESC_BASE_COLUMN_NAME, SQL_DESC_LITERAL_PREFIX, SQL_DESC_LITERAL_SUFFIX, 또는 SQL_DESC_LOCAL_TYPE_NAME  
  
     드라이버 관리자 SQLSTATE HY091 인 sql_error가 반환 (잘못 된 설명자 필드 식별자)입니다. 이 섹션에서는 없습니다 추가 규칙이 적용 됩니다.  
  
2.  드라이버 관리자 매핑됩니다 SQL_COLUMN_COUNT, SQL_COLUMN_NAME, 또는 SQL_COLUMN_NULLABLE SQL_DESC_COUNT, SQL_DESC_NAME, 또는 SQL_DESC_NULLABLE, 각각. (는 ODBC 2 *.x* 드라이버 필요만 SQL_COLUMN_COUNT, SQL_COLUMN_NAME, 및 SQL_COLUMN_NULLABLE, 없습니다 SQL_DESC_COUNT, SQL_DESC_NAME, 및 지원 SQL_DESC_NULLABLE.) SQLColAttribute에 대 한 호출에 매핑됩니다.  
  
    ```  
    SQLColAttributes(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
    ```  
  
3.  다른 모든 *FieldIdentifier* 값으로 드라이버를 통해 전달 됩니다 **SQLColAttribute** 매핑할 **SQLColAttributes** 앞서 나온 것 처럼 합니다.  
  
4.  하는 경우 *BufferLength* 드라이버 관리자는 SQLSTATE HY090 인 sql_error가 0 보다 작습니다 (잘못 된 문자열 또는 버퍼 길이). 이 섹션에서는 없습니다 추가 규칙이 적용 됩니다.  
  
5.  하는 경우 *FieldIdentifier* SQL_DESC_CONCISE_TYPE 이며 반환 되는 형식은 간결한 datetime 데이터 형식, 드라이버 관리자 맵에 date, time 및 timestamp 코드에 대 한 값을 반환 합니다.  
  
6.  드라이버 관리자를 필요한 검사를 수행 하는지 여부를 올려야 SQLSTATE HY010 (함수 시퀀스 오류) 해야 합니다. 드라이버 관리자 SQLSTATE HY010 및 SQL_ERROR를 반환 하는, 하는 경우 (함수 시퀀스 오류). 이 섹션에서는 없습니다 추가 규칙이 적용 됩니다.  
  
## <a name="sqlendtran"></a>SQLEndTran  
 드라이버 관리자는이를 매핑합니다 **SQLTransact**합니다. 다음에 호출할 **SQLEndTran**:  
  
```  
SQLEndTran(HandleType, Handle, CompletionType);  
```  
  
 드라이버 관리자는 다음을 수행 하면 (개념적에서 오류 검사) 매핑:  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV:return(SQLTransact(Handle, SQL_NULL_HDBC, CompletionType));  
   case SQL_HANDLE_DBC:return(SQLTransact(SQL_NULL_HENV, Handle, CompletionType);  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlfetch"></a>SQLFetch  
 드라이버 관리자는이를 매핑합니다 **SQLExtendedFetch** 사용 하 여를 *FetchOrientation* SQL_FETCH_NEXT의 인수입니다. 다음에 호출할 **SQLFetch**:  
  
```  
SQLFetch (StatementHandle);  
```  
  
 드라이버 관리자 호출 하면 **SQLExtendedFetch**다음과 같이 합니다.  
  
```  
rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, &RowCount, RowStatusArray);  
```  
  
 이 호출을 *pcRow* 인수는 응용 프로그램에 대 한 호출을 통해 SQL_ATTR_ROWS_FETCHED_PTR 문 특성을 설정 하는 값으로 설정 됩니다 **SQLSetStmtAttr**합니다.  
  
> [!NOTE]  
>  응용 프로그램을 호출할 때 **SQLSetStmtAttr** 드라이버 관리자 상태 배열을 가리키는 SQL_ATTR_ROW_STATUS_PTR을 설정 하려면 포인터를 캐시 합니다. *RowStatusArray* null 포인터로 같을 수 있습니다.  
  
 드라이버를 지원 하지 않는 경우 **SQLExtendedFetch** 커서 라이브러리가 로드 되 고 드라이버 관리자는 커서 라이브러리 사용 **SQLExtendedFetch** 매핑할 **SQLFetch** 를 **SQLExtendedFetch**합니다. 드라이버를 지원 하지 않는 경우 **SQLExtendedFetch** 커서 라이브러리가 로드 되지 않았음, 드라이버 관리자에 대 한 호출을 전달 **SQLFetch** 통해 드라이버입니다. 응용 프로그램을 호출 하는 경우 **SQLSetStmtAttr** SQL_ATTR_ROW_STATUS_PTR을 설정 하려면 드라이버 관리자 배열이 채워져 있는지 확인 합니다. 응용 프로그램을 호출 하는 경우 **SQLSetStmtAttr** SQL_ATTR_ROWS_FETCHED_PTR을 설정 하려면 드라이버 관리자를 1로이 필드를 설정 합니다.  
  
## <a name="sqlfetchscroll"></a>SQLFetchScroll  
 드라이버 관리자는이를 매핑합니다 **SQLExtendedFetch**합니다. 다음에 호출할 **SQLFetchScroll**:  
  
```  
SQLFetchScroll(StatementHandle, FetchOrientation, FetchOffset);  
```  
  
 단계의 다음 시퀀스에서는 발생 됩니다.  
  
1.  응용 프로그램을 호출할 때 **SQLSetStmtAttr** 상태 배열을 가리키는 SQL_ATTR_ROW_STATUS_PTR (있음 IRD SQL_DESC_ARRAY_STATUS_PTR 필드 설정)을 설정 하려면 드라이버 관리자는이 포인터를 캐시 합니다. 이 포인터를 사용할 수 있도록 *RowStatusArray*고, 그렇지 않으면 let *RowStatusArray* null 포인터와 같아야 합니다. 경우는 *RowStatusArray* 인수를 null 포인터로 설정, 드라이버 관리자 행 상태 배열을 생성 합니다.  
  
2.  하는 경우 *FetchOrientation* 없습니다 또는 중 하나입니다 SQL_FETCH_NEXT, SQL_FETCH_PRIOR, SQL_FETCH_ABSOLUTE, SQL_FETCH_RELATIVE, SQL_FETCH_FIRST, SQL_FETCH_LAST, SQL_FETCH_BOOKMARK, SQLSTATE SQL_ERROR와 드라이버 관리자를 반환 합니다. HY106 (반입 형식이 범위를 벗어났습니다.). 이 섹션에서는 없습니다 추가 규칙이 적용 됩니다.  
  
3.  사례:  
  
-   하는 경우 *FetchOrientation* 이면 SQL_FETCH_BOOKMARK, 같음:  
  
    -   하는 경우 **SQLSetStmtAttr** 이전은 SQL_ATTR_FETCH_BOOKMARK_PTR의 값을 설정 하 고가에 호출한 *Bmk* SQL_DESC_FETCH_BOOKMARK_PTR 포인터를 역참조 하 여 가져온 값 이어야 합니다.  
  
    -   그렇지 않으면 SQLSTATE HY111를 사용 하 여 SQL_ERROR가 반환 (잘못 된 책갈피 값). 이 섹션에서는 없습니다 추가 규칙이 적용 됩니다.  
  
     드라이버 관리자는 이제 호출 **SQLExtendedFetch**다음과 같이 합니다.  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, Bmk, pcRow, RowStatusArray);  
    ```  
  
-   드라이버 관리자를 호출 하는 고, 그렇지 **SQLExtendedFetch**다음과 같이 합니다.  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, pcRow, RowStatusArray);  
    ```  
  
     이러한 호출에는 *pcRow* 인수는 응용 프로그램에 대 한 호출을 통해 SQL_ATTR_ROWS_FETCHED_PTR 문 특성을 설정 하는 값으로 설정 됩니다 **SQLSetStmtAttr**합니다.  
  
-   SQL_ATTR_ROW_ARRAY_SIZE는 SQL_ROWSET_SIZE에 매핑됩니다.  
  
-   경우 *rc* SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를가 경우에 *FetchOrientation* SQL_FETCH_BOOKMARK 같은지 및 *FetchOffset* 다음과 같지 않은 경우 0, 다음 드라이버는 Manager 경고, SQLSTATE 01S10 게시 (책갈피 오프셋으로 인출, 오프셋 값이 무시 되었습니다)을 시도 하 고 SQL_SUCCESS_WITH_INFO를 반환 합니다.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 드라이버 관리자는이를 매핑합니다 **SQLFreeEnv**하십시오 **SQLFreeConnect**, 또는 **SQLFreeStmt** 적절 하 게 합니다. 다음에 호출할 **SQLFreeHandle**:  
  
```  
SQLFreeHandle(HandleType, Handle);  
```  
  
 드라이버 관리자는 다음을 수행 하면 (개념적에서 오류 검사) 매핑:  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLFreeEnv(Handle));  
   case SQL_HANDLE_DBC: return (SQLFreeConnect(Handle));  
   case SQL_HANDLE_STMT: return (SQLFreeStmt(Handle, SQL_DROP));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
 드라이버 관리자는이를 매핑합니다 **SQLGetConnectOption**합니다. 다음에 호출할 **SQLGetConnectAttr**:  
  
```  
SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 단계의 다음 시퀀스에서는 발생 됩니다.  
  
1.  하는 경우 *특성* 드라이버에서 정의 된 연결 또는 명령문 특성 아니며 ODBC 2에 정의 된 특성이 아닙니다. *x*, SQLSTATE HY092를 사용 하 여 SQL_ERROR를 반환 하는 드라이버 관리자 (잘못 된 특성/옵션 식별자)입니다. 이 섹션에 없는 추가 규칙이 적용 됩니다.  
  
2.  하는 경우 *특성* SQL_ATTR_AUTO_IPD 또는 SQL_ATTR_METADATA_ID, 드라이버 관리자는 SQLSTATE HY092를 사용 하 여 SQL_ERROR가 (잘못 된 특성/옵션 식별자)입니다.  
  
3.  드라이버 관리자에 있는지 검사 필요한 SQLSTATE 08003 (연결에 열려 있지 않은 경우) 또는 SQLSTATE HY010 (함수 시퀀스 오류)가 발생 해야 합니다. 그렇다면 드라이버 관리자 SQL_ERROR를 반환 하 고 적절 한 오류 메시지를 게시 합니다. 이 섹션에서는 없습니다 추가 규칙이 적용 됩니다.  
  
4.  드라이버 관리자 호출 **SQLGetConnectOption** 다음과 같습니다.  
  
    ```  
    SQLGetConnectOption (ConnectionHandle, Attribute, ValuePtr);  
    ```  
  
     유의 합니다 *BufferLength* 하 고 *StringLengthPtr* 무시 됩니다.  
  
## <a name="sqlgetdata"></a>SQLGetData  
 때 ODBC 3. *x* 는 ODBC 2를 사용 하는 응용 프로그램 *.x* 드라이버 호출 **SQLGetData** 사용 하 여 합니다 *ColumnNumber* ODBC 30인수 *.x* 드라이버 관리자에 대 한 호출으로이 매핑합니다 **SQLGetStmtOption** 사용 하 여 합니다 *옵션* 특성이 SQL_GET_BOOKMARK로 설정 합니다.  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
 드라이버 관리자는이를 매핑합니다 **SQLGetStmtOption**합니다. 다음에 호출할 **SQLGetStmtAttr**:  
  
```  
SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 단계의 다음 시퀀스에서는 발생 됩니다.  
  
1.  하는 경우 *특성* 드라이버에서 정의 된 연결 또는 명령문 특성 아니며 ODBC 2에 정의 된 특성이 아닙니다. *x*, SQLSTATE HY092를 사용 하 여 SQL_ERROR를 반환 하는 드라이버 관리자 (잘못 된 특성/옵션 식별자)입니다. 이 섹션에 없는 추가 규칙이 적용 됩니다.  
  
2.  하는 경우 *특성* 다음 중 하나입니다.  
  
     SQL_ATTR_APP_ROW_DESC  
  
     SQL_ATTR_APP_PARAM_DESC  
  
     SQL_ATTR_AUTO_IPD  
  
     SQL_ATTR_ROW_BIND_TYPE  
  
     SQL_ATTR_IMP_ROW_DESC  
  
     SQL_ATTR_IMP_PARAM_DESC  
  
     SQL_ATTR_METADATA_ID  
  
     SQL_ATTR_PARAM_BIND_TYPE  
  
     SQL_ATTR_PREDICATE_PTR  
  
     SQL_ATTR_PREDICATE_OCTET_LENGTH_PTR  
  
     SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_OPERATION_PTR  
  
     SQL_ATTR_PARAM_OPERATION_PTR  
  
     드라이버 관리자 SQLSTATE HY092 인 sql_error가 반환 (잘못 된 특성/옵션 식별자)입니다. 이 섹션에서는 없습니다 추가 규칙이 적용 됩니다.  
  
3.  드라이버 관리자를 필요한 검사를 수행 하는지 여부를 올려야 SQLSTATE HY010 (함수 시퀀스 오류) 해야 합니다. 드라이버 관리자 SQLSTATE HY010 및 SQL_ERROR를 반환 하는, 하는 경우 (함수 시퀀스 오류). 이 섹션에서는 없습니다 추가 규칙이 적용 됩니다.  
  
4.  하는 경우 *특성* sql_attr_rows_fetched_ptr을 설정, 드라이버 관리자는 포인터를 내부 드라이버 관리자 변수에 같으면 *cRow*에 대 한 호출에서 사용 또는 사용에  **SQLExtendedFetch**합니다. 이 섹션에서는 없습니다 추가 규칙이 적용 됩니다.  
  
5.  하는 경우 *특성* 같은지 드라이버 관리자 SQL_DESC_FETCH_BOOKMARK_PTR를 호출 하는 동안 캐시 된는 적절 한 포인터를 반환 **SQLSetStmtAttr**합니다.  
  
6.  하는 경우 *특성* 같은지 드라이버 관리자 SQL_ATTR_ROW_STATUS_PTR을를 호출 하는 동안 캐시 된는 적절 한 포인터를 반환 **SQLSetStmtAttr**합니다.  
  
7.  드라이버 관리자 호출 **SQLGetStmtOption** 다음과 같습니다.  
  
    ```  
    SQLGetStmtOption (hstmt, fOption, pvParam);  
    ```  
  
     여기서 *hstmt*를 *fOption*, 및 *pvParam* 의 값으로 설정 됩니다 *StatementHandle*, *특성*, 및 *ValuePtr*, 각각. 합니다 *BufferLength* 하 고 *StringLengthPtr* 무시 됩니다.  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
 드라이버 관리자는이를 매핑합니다 **SQLSetConnectOption**합니다. 다음에 호출할 **SQLSetConnectAttr**:  
  
```  
SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, StringLength);  
```  
  
 단계의 다음 시퀀스에서는 발생 됩니다.  
  
1.  하는 경우 *특성* 드라이버에서 정의 된 연결 또는 명령문 특성 아니며 ODBC 2에 정의 된 특성이 아닙니다. *x*, SQLSTATE HY092를 사용 하 여 SQL_ERROR를 반환 하는 드라이버 관리자 (잘못 된 특성/옵션 식별자)입니다. 이 섹션에 없는 추가 규칙이 적용 됩니다.  
  
2.  하는 경우 *특성* SQL_ATTR_AUTO_IPD, 드라이버 관리자는 SQLSTATE HY092 인 sql_error가 같으면 (잘못 된 특성/옵션 식별자)입니다.  
  
3.  드라이버 관리자를 필요한 검사를 수행 하는지 여부를 SQLSTATE 08003 (연결에 열려 있지 않은 경우) 또는 SQLSTATE HY010 (함수 시퀀스 오류)가 발생 해야 합니다. 발생 해야 이러한 오류 중 하나가 드라이버 관리자는 SQL_ERROR를 반환 하 고 적절 한 오류 메시지를 게시 합니다. 이 섹션에서는 없습니다 추가 규칙이 적용 됩니다.  
  
4.  드라이버 관리자 호출 **SQLSetConnectOption** 다음과 같습니다.  
  
    ```  
    SQLSetConnectOption (hdbc, fOption, vParam);  
    ```  
  
     여기서 *hdbc*를 *fOption*, 및 *갖고* 의 값으로 설정 됩니다 *ConnectionHandle*, *특성*, 및 *ValuePtr*, 각각. *StringLengthPtr* 무시 됩니다.  
  
> [!NOTE]  
>  연결 수준에서 문 특성을 설정 하는 기능이 더 이상 사용 되지 않습니다. 되지 문 특성을 ODBC 3 씩 연결 수준에서 설정 되어야 합니다. *x* 응용 프로그램입니다.  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 드라이버 관리자는이를 매핑합니다 **SQLSetStmtOption**합니다. 다음에 호출할 **SQLSetStmtAttr**:  
  
```  
SQLSetStmtAttr(StatementHandle, Attribute, ValuePtr, StringLength);  
```  
  
 단계의 다음 시퀀스에서는 발생 됩니다.  
  
1.  하는 경우 *특성* 드라이버에서 정의 된 연결 또는 명령문 특성 아니며 ODBC 2에 정의 된 특성이 아닙니다. *x*, SQLSTATE HY092를 사용 하 여 SQL_ERROR를 반환 하는 드라이버 관리자 (잘못 된 특성/옵션 식별자)입니다. 이 섹션에 없는 추가 규칙이 적용 됩니다.  
  
2.  하는 경우 *특성* 다음 중 하나입니다.  
  
     SQL_ATTR_APP_ROW_DESC  
  
     SQL_ATTR_APP_PARAM_DESC  
  
     SQL_ATTR_AUTO_IPD  
  
     SQL_ATTR_ROW_BIND_TYPE  
  
     SQL_ATTR_IMP_ROW_DESC  
  
     SQL_ATTR_IMP_PARAM_DESC  
  
     SQL_ATTR_METADATA_ID  
  
     SQL_ATTR_PARAM_BIND_TYPE  
  
     SQL_ATTR_PREDICATE_PTR  
  
     SQL_ATTR_PREDICATE_OCTET_LENGTH_PTR  
  
     SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_OPERATION_PTR  
  
     SQL_ATTR_PARAM_OPERATION_PTR  
  
     드라이버 관리자 SQLSTATE HY092 인 sql_error가 반환 (잘못 된 특성/옵션 식별자)입니다. 이 섹션에서는 없습니다 추가 규칙이 적용 됩니다.  
  
3.  드라이버 관리자를 필요한 검사를 수행 하는지 여부를 발생할 SQLSTATE HY010 (함수 시퀀스 오류) 필요 합니다. 드라이버 관리자 SQLSTATE HY010 및 SQL_ERROR를 반환 하는, 하는 경우 (함수 시퀀스 오류). 이 섹션에서는 없습니다 추가 규칙이 적용 됩니다.  
  
4.  하는 경우 *특성* SQL_ATTR_PARAMSET_SIZE SQL_ATTR_PARAMS_PROCESSED_PTR 같은 "매핑을 배열에 대 한 처리 매개 변수를" 섹션을 참조 하십시오이 항목의 뒷부분에 나오는 됩니다. 이 섹션에서는 없습니다 추가 규칙이 적용 됩니다.  
  
5.  하는 경우 *특성* sql_attr_rows_fetched_ptr을 설정, 드라이버 관리자 캐시를 사용 하 여 나중에 사용에 대 한 포인터 값과 같으면 **SQLFetchScroll**합니다.  
  
6.  경우 *특성* SQL_ATTR_ROW_STATUS_PTR을 드라이버 관리자 캐시를 사용 하 여 나중에 사용에 대 한 포인터 값과 같으면 **SQLFetchScroll** 하거나 **SQLSetPos**합니다. 이 섹션에서는 없습니다 추가 규칙이 적용 됩니다.  
  
7.  하는 경우 *특성* 은 SQL_ATTR_FETCH_BOOKMARK_PTR, 드라이버 관리자 캐시 같으면 *ValuePtr* 에 대 한 호출의 나중에 캐시 된 값을 사용 합니다 **SQLFetchScroll**합니다. 이 섹션에서는 없습니다 추가 규칙이 적용 됩니다.  
  
8.  드라이버 관리자 호출 **SQLSetStmtOption** 다음과 같습니다.  
  
    ```  
    SQLSetStmtOption (hstmt, fOption, vParam);  
    ```  
  
     여기서 *hstmt*를 *fOption*, 및 *갖고* 의 값으로 설정 됩니다 *StatementHandle*, *특성*, 및 *ValuePtr*, 각각. 합니다 *StringLength* 인수는 무시 됩니다.  
  
     경우에는 ODBC 2입니다. *x* 드라이버 지원 문자열, 드라이버별 문 옵션에는 ODBC 3. *x* 응용 프로그램을 호출 해야 **SQLSetStmtOption** 해당 옵션을 설정 합니다.  
  
## <a name="mappings-for-handling-parameter-arrays"></a>매개 변수 배열 처리에 대 한 매핑  
 응용 프로그램 호출 하는 경우:  
  
```  
SQLSetStmtAttr (StatementHandle, SQL_ATTR_PARAMSET_SIZE, Size, StringLength);  
```  
  
 드라이버 관리자를 호출합니다.  
  
```  
SQLParamOptions (StatementHandle, Size, &RowCount);  
```  
  
 드라이버 관리자 응용 프로그램을 호출 하는 경우이 변수에 대 한 포인터 이상 반환 **SQLGetStmtAttr** SQL_ATTR_PARAMS_PROCESSED_PTR 검색할 합니다. 드라이버 관리자는 문 핸들 할당 또는 준비 된 상태로 반환 될 때까지이 내부 변수를 변경할 수 없습니다.  
  
 ODBC 3입니다. *x* 응용 프로그램에서 호출할 수 있습니다 **SQLGetStmtAttr** 명시적으로 설정 하지 SQL_DESC_ARRAY_SIZE 필드 APD의 경우에 sql_attr_params_processed_ptr은 값을 가져오려고 합니다. 응용 프로그램에는 현재 "행" 매개 변수를 확인 하는 제네릭 루틴에이 상황이 발생할 수 있습니다 때 프로세싱이 **SQLExecute** SQL_NEED_DATA를 반환 합니다. 이 루틴의 SQL_DESC_ARRAY_SIZE 1 인지 여부에 호출 됩니다 1 보다 큽니다. 이 고려 하기에 드라이버 관리자가 응용 프로그램을 호출 하는지 여부이 내부 변수를 정의 해야 할 것 **SQLSetStmtAttr** APD의 SQL_DESC_ARRAY_SIZE 필드를 설정할 수 있습니다. 드라이버 관리자는이 변수에서 반환 하기 전에 값 1에 포함 되도록 SQL_DESC_ARRAY_SIZE 설정 되지 않은 경우 **SQLExecDirect** 하거나 **SQLExecute**합니다.  
  
## <a name="error-handling"></a>오류 처리  
 Odbc 3. *x*를 호출 **SQLFetch** 하거나 **SQLFetchScroll** IRD 및 지정된 된 진단 레코드의 SQL_DIAG_ROW_NUMBER 필드 SQL_DESC_ARRAY_STATUS_PTR 채웁니다 이 레코드에 관련 된 행 집합의 행 수가 포함 됩니다. 이 사용 하는 응용 프로그램 상호 연결할 수 오류 메시지가 지정 된 행 위치를 사용 하 여.  
  
 ODBC 2입니다. *x* 드라이버에이 기능을 제공 하는 일을 할 수 없습니다. 그러나 SQLSTATE 01S01 사용 하 여 오류 경계를 제공 합니다 (행의 오류). ODBC 3입니다. *x* 사용 하는 응용 프로그램 **SQLFetch** 하거나 **SQLFetchScroll** 는 ODBC 2에 대 한 이동 하는 동안. *x* 드라이버 이러한 점에 주의 해야 합니다. 이러한 응용 프로그램을 호출할 수 됩니다는 또한 **SQLGetDiagField** 를 실제로 그래도 SQL_DIAG_ROW_NUMBER 필드를 가져옵니다. ODBC 3입니다. *x* 응용 프로그램을 사용 하는 ODBC 2. *x* 드라이버를 호출할 수 있게 됩니다 **SQLGetDiagField** 만 *DiagIdentifier* SQL_DIAG_MESSAGE_TEXT, SQL_DIAG_NATIVE, SQL_DIAG_RETURNCODE, 또는 SQL_DIAG_ 인수 SQLSTATE입니다. ODBC 3 *.x* 는 ODBC 2를 사용 하 여 작업할 때 드라이버 관리자 진단 데이터 구조를 유지 합니다. *x* 드라이버, 있지만 ODBC 2. *x* 드라이버에는 이러한 4 개의 필드만 반환 합니다.  
  
 경우는 ODBC 2. *x* 는 ODBC 2를 사용 하 여 응용 프로그램이 작동 합니다. *x* 드라이버를 작업에는 드라이버 관리자에 의해 반환 될 여러 오류가 발생할 수 있습니다 하는 경우 다른 오류가 반환 되는 ODBC 3 *.x* ODBC 2 보다 드라이버 관리자입니다. *x* 드라이버 관리자입니다.  
  
## <a name="mappings-for-bookmark-operations"></a>책갈피 작업에 대 한 매핑  
 ODBC 3 *.x* 드라이버 관리자는 때를 ODBC 3 다음 매핑을 수행 합니다. *x* 응용 프로그램을 사용 하는 ODBC 2. *x* 드라이버 책갈피 작업을 수행 합니다.  
  
### <a name="sqlbindcol"></a>SQLBindCol  
 때 ODBC 3. *x* 응용 프로그램을 사용 하는 ODBC 2. *x* 드라이버 호출 **SQLBindCol** 사용 하 여 0 열에 바인딩할 *fCType* SQL_C_VARBOOKMARK, ODBC 3 같음 *.x* 드라이버 관리자 확인 여부를 합니다 *BufferLength* 인수 보다 작거나 4 보다 크거나 4 및 그렇다면 SQLSTATE HY090 반환 (잘못 된 문자열 또는 버퍼 길이). 경우는 *BufferLength* 인수는 4, 드라이버 관리자 호출 **SQLBindCol** 바꾼 후 드라이버에서 *fCType* SQL_C_BOOKMARK를 사용 하 여 합니다.  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 때 ODBC 3. *x* 응용 프로그램을 사용 하는 ODBC 2. *x* 드라이버 호출 **SQLColAttribute** 사용 하 여 합니다 *ColumnNumber* 드라이버 관리자 반환 인수를 0으로 설정 합니다 *FieldIdentifier* 값 다음 표에 나열 합니다.  
  
|*FieldIdentifier*|값|  
|-----------------------|-----------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_FALSE|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|  
|SQL_DESC_CATALOG_NAME|""(빈 문자열)|  
|SQL_DESC_CONCISE_TYPE|SQL_BINARY|  
|SQL_DESC_COUNT|반환 되는 동일한 값 **SQLNumResultCols**|  
|SQL_DESC_DATETIME_INTERVAL_CODE|0|  
|SQL_DESC_DISPLAY_SIZE|8|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|  
|SQL_DESC_LABEL|""(빈 문자열)|  
|SQL_DESC_LENGTH|0|  
|SQL_DESC_LITERAL_PREFIX|""(빈 문자열)|  
|SQL_DESC_LITERAL_SUFFIX|""(빈 문자열)|  
|SQL_DESC_LOCAL_TYPE_NAME|""(빈 문자열)|  
|SQL_DESC_NAME|""(빈 문자열)|  
|SQL_DESC_NULLABLE|SQL_NO_NULLS|  
|SQL_DESC_OCTET_LENGTH|4|  
|SQL_DESC_PRECISION|4|  
|SQL_DESC_SCALE|0|  
|SQL_DESC_SCHEMA_NAME|""(빈 문자열)|  
|SQL_DESC_SEARCHABLE|SQL_PRED_NONE|  
|SQL_DESC_TABLE_NAME|""(빈 문자열)|  
|SQL_DESC_TYPE|SQL_BINARY|  
|SQL_DESC_TYPE_NAME|""(빈 문자열)|  
|SQL_DESC_UNNAMED|SQL_UNNAMED|  
|SQL_DESC_UNSIGNED|SQL_FALSE|  
|SQL_DESC_UPDATEABLE|SQL_ATTR_READ_ONLY|  
  
### <a name="sqldescribecol"></a>SQLDescribeCol  
 때 ODBC 3. *x* 응용 프로그램을 사용 하는 ODBC 2. *x* 드라이버 호출 **SQLDescribeCol** 사용 하 여 합니다 *ColumnNumber* 0으로 설정 하는 인수를 드라이버 관리자는 다음 표에 나열 된 값을 반환 합니다.  
  
|버퍼|값|  
|------------|-----------|  
|ColumnName|""(빈 문자열)|  
|*NameLengthPtr|0|  
|*DataTypePtr|SQL_BINARY|  
|*ColumnSizePtr|4|  
|*DecimalDigitsPtr|0|  
|*NullablePtr|SQL_NO_NULLS|  
  
### <a name="sqlgetdata"></a>SQLGetData  
 때 ODBC 3. *x* 응용 프로그램을 사용 하는 ODBC 2. *x* 에 다음 호출을 수행 하는 드라이버 **SQLGetData** 책갈피를 검색 하려면:  
  
```  
SQLGetData(StatementHandle, 0, SQL_C_VARBOOKMARK, TargetValuePtr, BufferLength, StrLen_or_IndPtr)  
```  
  
 호출에 매핑된 **SQLGetStmtOption** 사용 하 여는 *fOption* 같이 SQL_GET_BOOKMARK의:  
  
```  
SQLGetStmtOption(hstmt, SQL_GET_BOOKMARK, TargetValuePtr)  
```  
  
 여기서 *hstmt* 하 고 *pvParam* 의 값으로 설정 됩니다 *StatementHandle* 및 *TargetValuePtr*, 각각. 책갈피에서 가리키는 버퍼에 반환 되는 *pvParam* (*TargetValuePtr*) 인수입니다. 가리키는 버퍼의 값을 *StrLen_or_IndPtr* 호출에서 인수 **SQLGetData** 가 4로 설정 합니다.  
  
 이 매핑은는 대/소문자를 고려 하는 데 필요한 **SQLFetch** 호출 하기 전에 호출한 **SQLGetData** 및 ODBC 2. *x* 드라이버를 지원 하지 않았습니다 **SQLExtendedFetch**합니다. 이 예에서 **SQLFetch** ODBC 2를 통해 전달 될. *x* 드라이버를 사례 책갈피 검색 지원 되지 않습니다.  
  
 **SQLGetData** 는 ODBC 2에서 여러 번 호출할 수 없습니다. *x* 호출 하므로 부분에서 책갈피를 검색 하도록 드라이버 **SQLGetData** 사용 하 여 합니다 *BufferLength* 인수는 4 보다 작은 값으로 설정 하며 *ColumnNumber*0으로 설정 하는 인수에는 SQLSTATE HY090 반환 됩니다 (잘못 된 문자열 또는 버퍼 길이). **하지만 SQLGetData** 될 수 있습니다 동일한 책갈피를 검색 하는 여러 번 호출 합니다.  
  
### <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 때 ODBC 3. *x* 응용 프로그램을 사용 하는 ODBC 2. *x* 드라이버 호출 **SQLSetStmtAttr** SQL_ATTR_USE_BOOKMARKS 특성 SQL_UB_VARIABLE을 설정 하려면 드라이버 관리자 특성을 설정 합니다 SQL_UB_ON 기본 ODBC 2에서. *x* 드라이버입니다.
