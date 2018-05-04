---
title: 앱-ODBC의 호환성에 대 한 대체 함수 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 14ca73aefb033580c2770da05189e3de04a424e3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="mapping-replacement-functions-for-backward-compatibility-of-applications"></a>응용 프로그램의 이전 버전과 호환성에 대 한 매핑 대체 함수
ODBC 3 *.x* ODBC 3를 통해 작업 하는 응용 프로그램 *.x* ODBC 2에 대 한 드라이버 관리자가 작동 합니다. *x* 드라이버 있다면 없는 새로운 기능이 사용 됩니다. 그러나 둘 다 중복 기능 및 변경 된 동작 방식에 영향를 수행 하는 ODBC 3. *x* 응용 프로그램이 ODBC 2에서 작동 합니다. *x* 드라이버입니다. ODBC 2 작업할 때는. *x* 드라이버, 드라이버 관리자 매핑합니다 다음 ODBC 3. *x* 는 하나 이상의 ODBC 2를 대체 하는 함수. *x* 함수에 해당 하는 ODBC 2. *x* 함수입니다.  
  
|ODBC 3입니다. *x* 함수|ODBC 2입니다. *x* 함수|  
|-------------------------|-------------------------|  
|**SQLAllocHandle**|**SQLAllocEnv**, **SQLAllocConnect**, 또는 **SQLAllocStmt**|  
|**SQLBulkOperations**|**SQLSetPos**|  
|**SQLColAttribute**|**SQLColAttributes**|  
|**SQLEndTran**|**SQLTransact**|  
|**SQLFetch**|**SQLExtendedFetch**|  
|**SQLFetchScroll**|**SQLExtendedFetch**|  
|**SQLFreeHandle**|**SQLFreeEnv**, **SQLFreeConnect**, 또는 **SQLFreeStmt**|  
|**SQLGetConnectAttr**|**SQLGetConnectOption**|  
|**SQLGetDiagRec**|**SQLError**|  
|**SQLGetStmtAttr**|**SQLGetStmtOption**[1]|  
|**SQLSetConnectAttr**|**SQLSetConnectOption**|  
|**SQLSetStmtAttr**|**SQLSetStmtOption**[1]|  
  
 [1] 다른 작업이 요청 되는 특성에 따라 수행도 될 수 있습니다.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
 드라이버 관리자는이를 매핑합니다 **SQLAllocEnv**, **SQLAllocConnect**, 또는 **SQLAllocStmt**를 적절 하 게 합니다. 다음에 대 한 호출 **SQLAllocHandle**:  
  
```  
SQLAllocHandle(HandleType, InputHandle, OutputHandlePtr);  
```  
  
 다음을 수행 하면 드라이버 관리자에서 발생 합니다 (개념, 오류를 검사 하지 않습니다) 매핑:  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLAllocEnv(OutputHandlePtr));  
   case SQL_HANDLE_DBC: return (SQLAllocConnect (InputHandle, OutputHandlePtr));  
   case SQL_HANDLE_STMT: return (SQLAllocStmt (InputHandle, OutputHandlePtr));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlbulkoperations"></a>SQLBulkOperations  
 드라이버 관리자는이를 매핑합니다 **SQLSetPos**합니다. 다음에 대 한 호출 **SQLBulkOperations**:  
  
```  
SQLBulkOperations(hstmt, Operation);  
```  
  
 다음 단계를 순서 대로 발생 합니다.  
  
1.  드라이버 관리자를 호출 하는 작업 인수 SQL_ADD 이면 **SQLSetPos** 다음과 같습니다.  
  
    ```  
    SQLSetPos (hstmt, 0, SQL_ADD, SQL_LOCK_NO_CHANGE);  
    ```  
  
2.  연산 인수 SQL_ADD 없으면 드라이버 반환 SQLSTATE HY092 (잘못 된 특성/옵션 식별자)입니다.  
  
3.  응용 프로그램에 대 한 호출 간의 SQL_ATTR_ROW_STATUS_PTR을 변경 하려고 할 경우 **SQLFetch** 또는 **SQLFetchScroll** 및 **SQLBulkOperations**, 드라이버 관리자는 SQLSTATE HY011 반환 (특성 지금 설정할 수 없습니다).  
  
4.  응용 프로그램을 호출 해야 작업 인수 SQL_ADD 이면 **SQLBindCol** 삽입 될 데이터를 바인딩할 합니다. 호출할 수 없습니다 **SQLSetDescField** 또는 **SQLSetDescRec** 삽입 될 데이터를 바인딩할 합니다.  
  
5.  작업 인수는 SQL_ADD 삽입할 행 수 없는 경우 현재 행 집합 크기와 동일 **SQLSetStmtAttr** 호출 SQL_ATTR_ROW_ARRAY_SIZE 문 특성 수에 행 수를 설정 하 여 호출 하기 전에 삽입 **SQLBulkOperations**합니다. 응용 프로그램 해야 하기 전에 SQL_ATTR_ROW_ARRAY_SIZE 문 특성을 설정 하는 데 다시 돌아가려면 이전 행 집합 크기, **SQLFetch**, **SQLFetchScroll**, 또는 **SQLSetPos**라고 합니다.  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
 드라이버 관리자는이를 매핑합니다 **SQLColAttributes**합니다. 다음에 대 한 호출 **SQLColAttribute**:  
  
```  
SQLColAttribute(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
```  
  
 다음 단계를 순서 대로 발생 합니다.  
  
1.  경우 *FieldIdentifier* 다음 중 하나입니다.  
  
     SQL_DESC_PRECISION, SQL_DESC_SCALE, SQL_DESC_LENGTH, SQL_DESC_OCTET_LENGTH, SQL_DESC_UNNAMED, SQL_DESC_BASE_COLUMN_NAME, SQL_DESC_LITERAL_PREFIX, SQL_DESC_LITERAL_SUFFIX, 또는 SQL_DESC_LOCAL_TYPE_NAME  
  
     드라이버 관리자 SQLSTATE HY091 인 sql_error가 반환 (잘못 된 설명자 필드 식별자)입니다. 이 섹션의 추가 규칙이 적용 됩니다.  
  
2.  드라이버 관리자 매핑됩니다 SQL_COLUMN_COUNT, SQL_COLUMN_NAME, 또는 SQL_COLUMN_NULLABLE SQL_DESC_COUNT, SQL_DESC_NAME, 또는 SQL_DESC_NULLABLE, 각각. (ODBC 2 *.x* 드라이버 필요만 SQL_COLUMN_COUNT, SQL_COLUMN_NAME, 및 SQL_COLUMN_NULLABLE, 하지 SQL_DESC_COUNT, SQL_DESC_NAME, 및 지원 SQL_DESC_NULLABLE.) SQLColAttribute에 대 한 호출에 매핑됩니다.  
  
    ```  
    SQLColAttributes(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
    ```  
  
3.  다른 모든 *FieldIdentifier* 값으로 드라이버를 통해 전달 됩니다 **SQLColAttribute** 에 매핑된 **SQLColAttributes** 이전에 표시 된 것 처럼 합니다.  
  
4.  경우 *BufferLength* 드라이버 관리자 반환 된 SQLSTATE HY090 sql_error가 0 보다 작으면 (잘못 된 문자열 또는 버퍼 길이). 이 섹션의 추가 규칙이 적용 됩니다.  
  
5.  경우 *FieldIdentifier* SQL_DESC_CONCISE_TYPE 이므로 반환 되는 형식은 간결한 datetime 데이터 형식으로 반환 되는 값을 date, time 및 timestamp 코드에 대 한 드라이버 관리자 맵.  
  
6.  드라이버 관리자를 보려면 필요한 검사를 수행 하는지 여부를 SQLSTATE HY010 (함수 시퀀스 오류)가 발생 합니다. 드라이버 관리자 SQLSTATE HY010 및 SQL_ERROR를 반환 하는, (함수 시퀀스 오류). 이 섹션의 추가 규칙이 적용 됩니다.  
  
## <a name="sqlendtran"></a>SQLEndTran  
 드라이버 관리자는이를 매핑합니다 **SQLTransact**합니다. 다음에 대 한 호출 **SQLEndTran**:  
  
```  
SQLEndTran(HandleType, Handle, CompletionType);  
```  
  
 다음을 수행 하면 드라이버 관리자에서 발생 합니다 (개념, 오류를 검사 하지 않습니다) 매핑:  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV:return(SQLTransact(Handle, SQL_NULL_HDBC, CompletionType));  
   case SQL_HANDLE_DBC:return(SQLTransact(SQL_NULL_HENV, Handle, CompletionType);  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlfetch"></a>SQLFetch  
 드라이버 관리자는이를 매핑합니다 **SQLExtendedFetch** 와 *FetchOrientation* SQL_FETCH_NEXT의 인수입니다. 다음에 대 한 호출 **SQLFetch**:  
  
```  
SQLFetch (StatementHandle);  
```  
  
 드라이버 관리자 호출 하면 **SQLExtendedFetch**, 다음과 같습니다.  
  
```  
rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, &RowCount, RowStatusArray);  
```  
  
 이 호출에서는 *pcRow* 인수 응용 프로그램에 대 한 호출을 통해 SQL_ATTR_ROWS_FETCHED_PTR 문 특성을 설정 하는 값으로 설정 되어 **SQLSetStmtAttr**합니다.  
  
> [!NOTE]  
>  응용 프로그램 호출 하는 경우 **SQLSetStmtAttr** 드라이버 관리자 상태 배열을 가리키는 SQL_ATTR_ROW_STATUS_PTR을 설정 하려면 포인터를 캐시 합니다. *RowStatusArray* null 포인터 일 수 있습니다.  
  
 드라이버를 지원 하지 않는 경우 **SQLExtendedFetch** 커서 라이브러리가 로드 되 고, 드라이버 관리자는 커서 라이브러리 사용 **SQLExtendedFetch** 매핑할 **SQLFetch** 를 **SQLExtendedFetch**합니다. 드라이버를 지원 하지 않는 경우 **SQLExtendedFetch** 커서 라이브러리가 로드 되지 않았음, 드라이버 관리자에 대 한 호출을 전달 하 고 **SQLFetch** 통해 드라이버에 있습니다. 응용 프로그램을 호출 하는 경우 **SQLSetStmtAttr** SQL_ATTR_ROW_STATUS_PTR을 설정 하려면 드라이버 관리자 배열 채워져 있는지 확인 합니다. 응용 프로그램을 호출 하는 경우 **SQLSetStmtAttr** SQL_ATTR_ROWS_FETCHED_PTR을 설정 하려면 드라이버 관리자는이 필드를 1로 설정 합니다.  
  
## <a name="sqlfetchscroll"></a>SQLFetchScroll  
 드라이버 관리자는이를 매핑합니다 **SQLExtendedFetch**합니다. 다음에 대 한 호출 **SQLFetchScroll**:  
  
```  
SQLFetchScroll(StatementHandle, FetchOrientation, FetchOffset);  
```  
  
 다음 단계를 순서 대로 발생 합니다.  
  
1.  응용 프로그램 호출 하는 경우 **SQLSetStmtAttr** 드라이버 관리자 상태 배열을 가리키는 (IRD의 SQL_DESC_ARRAY_STATUS_PTR 필드 설정) 된 SQL_ATTR_ROW_STATUS_PTR을 설정 하려면이 포인터를 캐시 합니다. 이 포인터를 사용할 수 있도록 *RowStatusArray*let, 그렇지않으면 *RowStatusArray* null 포인터 일 수 있습니다. 경우는 *RowStatusArray* 인수를 null 포인터로 설정, 드라이버 관리자 행 상태 배열을 생성 합니다.  
  
2.  경우 *FetchOrientation* 하지 또는 중 하나입니다 SQL_FETCH_NEXT, SQL_FETCH_PRIOR, SQL_FETCH_ABSOLUTE, SQL_FETCH_RELATIVE, SQL_FETCH_FIRST, SQL_FETCH_LAST, SQL_FETCH_BOOKMARK, 드라이버 관리자 SQL_ERROR와 SQLSTATE 반환 HY106 (인출 유형 범위를 벗어났습니다.). 이 섹션의 추가 규칙이 적용 됩니다.  
  
3.  사례:  
  
-   경우 *FetchOrientation* 과 다음 SQL_FETCH_BOOKMARK, 같음:  
  
    -   경우 **SQLSetStmtAttr** 이전은 SQL_ATTR_FETCH_BOOKMARK_PTR의 값을 설정 하 고가에 호출한 *Bmk* SQL_DESC_FETCH_BOOKMARK_PTR 포인터를 역참조 하 여 가져온 값 이어야 합니다.  
  
    -   그렇지 않으면 SQLSTATE HY111 포함 된 sql_error가 반환 (잘못 된 책갈피 값). 이 섹션의 추가 규칙이 적용 됩니다.  
  
     드라이버 관리자는 이제 호출 **SQLExtendedFetch**, 다음과 같습니다.  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, Bmk, pcRow, RowStatusArray);  
    ```  
  
-   그렇지 않으면 드라이버 관리자 호출 **SQLExtendedFetch**다음과 같이 합니다.  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, pcRow, RowStatusArray);  
    ```  
  
     이러한 호출에는 *pcRow* 인수 응용 프로그램에 대 한 호출을 통해 SQL_ATTR_ROWS_FETCHED_PTR 문 특성을 설정 하는 값으로 설정 되어 **SQLSetStmtAttr**합니다.  
  
-   SQL_ATTR_ROW_ARRAY_SIZE는 SQL_ROWSET_SIZE에 매핑됩니다.  
  
-   경우 *rc* 가 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 쓰고 *FetchOrientation* SQL_FETCH_BOOKMARK 같은지 및 *FetchOffset* 같지 않은 경우 0, 다음 드라이버는 관리자는 경고, SQLSTATE 01S10 게시 (오프셋 값 무시를 책갈피 오프셋으로 가져오려면 시도) 하 고 SQL_SUCCESS_WITH_INFO를 반환 합니다.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 드라이버 관리자는이를 매핑합니다 **SQLFreeEnv**, **SQLFreeConnect**, 또는 **SQLFreeStmt** 적절 하 게 합니다. 다음에 대 한 호출 **SQLFreeHandle**:  
  
```  
SQLFreeHandle(HandleType, Handle);  
```  
  
 다음을 수행 하면 드라이버 관리자에서 발생 합니다 (개념, 오류를 검사 하지 않습니다) 매핑:  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLFreeEnv(Handle));  
   case SQL_HANDLE_DBC: return (SQLFreeConnect(Handle));  
   case SQL_HANDLE_STMT: return (SQLFreeStmt(Handle, SQL_DROP));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
 드라이버 관리자는이를 매핑합니다 **SQLGetConnectOption**합니다. 다음에 대 한 호출 **SQLGetConnectAttr**:  
  
```  
SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 다음 단계를 순서 대로 발생 합니다.  
  
1.  경우 *특성* 드라이버에서 정의 된 연결 또는 명령문 특성이 아니므로 및 ODBC 2에 정의 된 특성이 아닙니다. *x*, 드라이버 관리자 SQLSTATE HY092 인 sql_error가 반환 (잘못 된 특성/옵션 식별자)입니다. 이 섹션의 추가 규칙이 적용 됩니다.  
  
2.  경우 *특성* SQL_ATTR_AUTO_IPD 또는 SQL_ATTR_METADATA_ID, 드라이버 관리자 반환 된 SQLSTATE HY092 SQL_ERROR가 (잘못 된 특성/옵션 식별자)입니다.  
  
3.  확인 하는 데 필요한 검사를 수행 하는 드라이버 관리자 SQLSTATE 08003 (연결이 열려 있지 않습니다.) 또는 SQLSTATE HY010 (함수 시퀀스 오류)가 발생 해야 합니다. 이 경우 드라이버 관리자 SQL_ERROR를 반환 하 고 적절 한 오류 메시지를 게시 합니다. 이 섹션의 추가 규칙이 적용 됩니다.  
  
4.  드라이버 관리자를 호출 하 여 **SQLGetConnectOption** 다음과 같습니다.  
  
    ```  
    SQLGetConnectOption (ConnectionHandle, Attribute, ValuePtr);  
    ```  
  
     *BufferLength* 및 *StringLengthPtr* 무시 됩니다.  
  
## <a name="sqlgetdata"></a>SQLGetData  
 때 ODBC 3. *x* 작업 하는 ODBC 2 응용 프로그램 *.x* 드라이버 호출 **SQLGetData** 와 *ColumnNumber* 0 ODBC 3인수 *.x* 드라이버 관리자에 대 한 호출에이 매핑합니다 **SQLGetStmtOption** 와 *옵션* 특성이 SQL_GET_BOOKMARK로 설정 합니다.  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
 드라이버 관리자는이를 매핑합니다 **SQLGetStmtOption**합니다. 다음에 대 한 호출 **SQLGetStmtAttr**:  
  
```  
SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 다음 단계를 순서 대로 발생 합니다.  
  
1.  경우 *특성* 드라이버에서 정의 된 연결 또는 명령문 특성이 아니므로 및 ODBC 2에 정의 된 특성이 아닙니다. *x*, 드라이버 관리자 SQLSTATE HY092 인 sql_error가 반환 (잘못 된 특성/옵션 식별자)입니다. 이 섹션의 추가 규칙이 적용 됩니다.  
  
2.  경우 *특성* 다음 중 하나입니다.  
  
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
  
     드라이버 관리자 SQLSTATE HY092 인 sql_error가 반환 (잘못 된 특성/옵션 식별자)입니다. 이 섹션의 추가 규칙이 적용 됩니다.  
  
3.  드라이버 관리자를 보려면 필요한 검사를 수행 하는지 여부를 SQLSTATE HY010 (함수 시퀀스 오류)가 발생 합니다. 드라이버 관리자 SQLSTATE HY010 및 SQL_ERROR를 반환 하는, (함수 시퀀스 오류). 이 섹션의 추가 규칙이 적용 됩니다.  
  
4.  경우 *특성* SQL_ATTR_ROWS_FETCHED_PTR, 내부 드라이버 관리자 변수에 대 한 포인터 드라이버 관리자 반환 같으면 *cRow*, 것은 사용 되지 않았거나에 대 한 호출에서 사용할  **SQLExtendedFetch**합니다. 이 섹션의 추가 규칙이 적용 됩니다.  
  
5.  경우 *특성* 같은지 드라이버 관리자 SQL_DESC_FETCH_BOOKMARK_PTR를를 호출 하는 동안 캐시에 있는 적절 한 포인터를 반환 **SQLSetStmtAttr**합니다.  
  
6.  경우 *특성* 같은지 드라이버 관리자, SQL_ATTR_ROW_STATUS_PTR을 호출 하는 동안 캐시에 있는 적절 한 포인터를 반환 **SQLSetStmtAttr**합니다.  
  
7.  드라이버 관리자를 호출 하 여 **SQLGetStmtOption** 다음과 같습니다.  
  
    ```  
    SQLGetStmtOption (hstmt, fOption, pvParam);  
    ```  
  
     여기서 *hstmt*, *fOption*, 및 *pvParam* 의 값으로 설정 됩니다 *StatementHandle*, *특성*, 및 *ValuePtr*각각. *BufferLength* 및 *StringLengthPtr* 무시 됩니다.  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
 드라이버 관리자는이를 매핑합니다 **SQLSetConnectOption**합니다. 다음에 대 한 호출 **SQLSetConnectAttr**:  
  
```  
SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, StringLength);  
```  
  
 다음 단계를 순서 대로 발생 합니다.  
  
1.  경우 *특성* 드라이버에서 정의 된 연결 또는 명령문 특성이 아니므로 및 ODBC 2에 정의 된 특성이 아닙니다. *x*, 드라이버 관리자 SQLSTATE HY092 인 sql_error가 반환 (잘못 된 특성/옵션 식별자)입니다. 이 섹션의 추가 규칙이 적용 됩니다.  
  
2.  경우 *특성* SQL_ATTR_AUTO_IPD, 드라이버 관리자 반환 된 SQLSTATE HY092 sql_error가 같습니다 (잘못 된 특성/옵션 식별자)입니다.  
  
3.  드라이버 관리자를 보려면 필요한 검사를 수행 하는지 여부를 SQLSTATE 08003 (연결이 열려 있지 않습니다.) 또는 SQLSTATE HY010 (함수 시퀀스 오류)가 발생 해야 합니다. 발생 해야 이러한 오류 중 하나가 드라이버 관리자 SQL_ERROR를 반환 하 고 적절 한 오류 메시지를 게시 합니다. 이 섹션의 추가 규칙이 적용 됩니다.  
  
4.  드라이버 관리자를 호출 하 여 **SQLSetConnectOption** 다음과 같습니다.  
  
    ```  
    SQLSetConnectOption (hdbc, fOption, vParam);  
    ```  
  
     여기서 *hdbc*, *fOption*, 및 *vParam* 의 값으로 설정 됩니다 *ConnectionHandle*, *특성*, 및 *ValuePtr*각각. *StringLengthPtr* 는 무시 됩니다.  
  
> [!NOTE]  
>  연결 수준에서 문 특성을 설정 하는 기능 더 이상 사용 되지 않습니다. ODBC 3으로 문 특성 연결 수준에서 설정할 수 없습니다. *x* 응용 프로그램입니다.  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 드라이버 관리자는이를 매핑합니다 **SQLSetStmtOption**합니다. 다음에 대 한 호출 **SQLSetStmtAttr**:  
  
```  
SQLSetStmtAttr(StatementHandle, Attribute, ValuePtr, StringLength);  
```  
  
 다음 단계를 순서 대로 발생 합니다.  
  
1.  경우 *특성* 드라이버에서 정의 된 연결 또는 명령문 특성이 아니므로 및 ODBC 2에 정의 된 특성이 아닙니다. *x*, 드라이버 관리자 SQLSTATE HY092 인 sql_error가 반환 (잘못 된 특성/옵션 식별자)입니다. 이 섹션의 추가 규칙이 적용 됩니다.  
  
2.  경우 *특성* 다음 중 하나입니다.  
  
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
  
     드라이버 관리자 SQLSTATE HY092 인 sql_error가 반환 (잘못 된 특성/옵션 식별자)입니다. 이 섹션의 추가 규칙이 적용 됩니다.  
  
3.  드라이버 관리자를 보려면 필요한 검사를 수행 하는지 여부를 발생 하는 SQLSTATE HY010 (함수 시퀀스 오류) 필요 합니다. 드라이버 관리자 SQLSTATE HY010 및 SQL_ERROR를 반환 하는, (함수 시퀀스 오류). 이 섹션의 추가 규칙이 적용 됩니다.  
  
4.  경우 *특성* SQL_ATTR_PARAMSET_SIZE 또는 SQL_ATTR_PARAMS_PROCESSED_PTR에 "매핑에 대 한 처리 매개 변수 배열과" 섹션을 참조 하십시오이 항목의 뒷부분에 나오는 됩니다. 이 섹션의 추가 규칙이 적용 됩니다.  
  
5.  경우 *특성* 같은지 SQL_ATTR_ROWS_FETCHED_PTR, 나중에 사용할 수 있는 포인터 값 드라이버 관리자 캐시를 **SQLFetchScroll**합니다.  
  
6.  경우 *특성* 같은지 SQL_ATTR_ROW_STATUS_PTR을 나중에 사용할 수 있는 포인터 값 드라이버 관리자 캐시를 **SQLFetchScroll** 또는 **SQLSetPos**합니다. 이 섹션의 추가 규칙이 적용 됩니다.  
  
7.  경우 *특성* 같은지은 SQL_ATTR_FETCH_BOOKMARK_PTR, 드라이버 관리자 캐시를 *ValuePtr* 에 대 한 호출의 뒷부분에 있는 캐시 된 값을 사용 합니다 **SQLFetchScroll**합니다. 이 섹션의 추가 규칙이 적용 됩니다.  
  
8.  드라이버 관리자를 호출 하 여 **SQLSetStmtOption** 다음과 같습니다.  
  
    ```  
    SQLSetStmtOption (hstmt, fOption, vParam);  
    ```  
  
     여기서 *hstmt*, *fOption*, 및 *vParam* 의 값으로 설정 됩니다 *StatementHandle*, *특성*, 및 *ValuePtr*각각. *StringLength* 인수는 무시 됩니다.  
  
     경우에는 ODBC 2입니다. *x* 드라이버 지원 문자열, 드라이버 관련 문 옵션을 ODBC 3. *x* 응용 프로그램 호출 해야 **SQLSetStmtOption** 이러한 옵션을 설정 합니다.  
  
## <a name="mappings-for-handling-parameter-arrays"></a>매개 변수 배열 처리에 대 한 매핑  
 응용 프로그램 호출 하는 경우:  
  
```  
SQLSetStmtAttr (StatementHandle, SQL_ATTR_PARAMSET_SIZE, Size, StringLength);  
```  
  
 드라이버 관리자를 호출합니다.  
  
```  
SQLParamOptions (StatementHandle, Size, &RowCount);  
```  
  
 드라이버 관리자는 나중에 포인터를 반환이 변수는 응용 프로그램 호출 때 **SQLGetStmtAttr** SQL_ATTR_PARAMS_PROCESSED_PTR를 검색할 수 있습니다. 드라이버 관리자를 준비 또는 할당 된 상태로 문 핸들 반환 될 때까지이 내부 변수를 변경할 수 없습니다.  
  
 ODBC 3입니다. *x* 응용 프로그램에서 호출할 수 **SQLGetStmtAttr** 이 속성에 명시적으로 설정 하지 SQL_DESC_ARRAY_SIZE 필드 APD의 경우에 SQL_ATTR_PARAMS_PROCESSED_PTR의 값을 가져올 수 있습니다. 이러한 상황이 발생할 수, 예를 들어 응용 프로그램에서 현재 "행"의 매개 변수를 검사 하는 일반 루틴 때 처리 되 고 **SQLExecute** SQL_NEED_DATA를 반환 합니다. 이 루틴을 호출 하는 1에서 SQL_DESC_ARRAY_SIZE 여부는 1 보다 큰 값 또는입니다. 이를 드라이버 관리자가 응용 프로그램을 호출 하는지 여부이 내부 변수를 정의 해야 할 것 **SQLSetStmtAttr** APD의 SQL_DESC_ARRAY_SIZE 필드를 설정할 수 있습니다. 드라이버 관리자가 SQL_DESC_ARRAY_SIZE 설정 되지 않은 경우이 변수에서 반환 하기 전에 값 1에 포함 되도록 해야 **SQLExecDirect** 또는 **SQLExecute**합니다.  
  
## <a name="error-handling"></a>오류 처리  
 Odbc 3. *x*호출, **SQLFetch** 또는 **SQLFetchScroll** SQL_DESC_ARRAY_STATUS_PTR IRD 및 지정된 된 진단 레코드의 SQL_DIAG_ROW_NUMBER 필드를 채웁니다. 이 레코드에 관련 된 행 집합의 행 수가 포함 됩니다. 이 사용 하 여, 응용 프로그램 간에 상관 관계 수 오류 메시지가 특정된 행 위치와 합니다.  
  
 ODBC 2입니다. *x* 드라이버가이 기능을 제공할 수 없습니다. 그러나 SQLSTATE 01S01와 오류 경계를 제공 합니다 (행에서 오류). ODBC 3입니다. *x* 사용 중인 응용 프로그램이 **SQLFetch** 또는 **SQLFetchScroll** ODBC 2에 대 한 이동 하는 동안. *x* 드라이버가 이러한 사실을 알고 있어야 합니다. 이러한 응용 프로그램을 호출할 수 없게 됩니다는 또한 참고 **SQLGetDiagField** 가져올 실제로 요 SQL_DIAG_ROW_NUMBER 필드에 있습니다. ODBC 3입니다. *x* 응용 프로그램을 사용 하는 ODBC 2. *x* 드라이버를 호출할 수 **SQLGetDiagField** 에서만 *DiagIdentifier* SQL_DIAG_MESSAGE_TEXT, SQL_DIAG_NATIVE, SQL_DIAG_RETURNCODE, 또는 SQL_DIAG_의 인수 SQLSTATE입니다. ODBC 3 *.x* 드라이버 관리자는 ODBC 2 작업할 때 진단 데이터 구조를 유지 합니다. *x* 드라이버, 있지만 ODBC 2. *x* 드라이버는 이러한 4 개의 필드에만 반환 합니다.  
  
 경우는 ODBC 2. *x* 응용 프로그램이 작동 ODBC 2. *x* 드라이버를 작업에는 드라이버 관리자에 의해 반환 될 여러 오류가 발생할 수 있습니다 하는 경우 서로 다른 오류 반환 되는 ODBC 3 *.x* 드라이버 관리자가 ODBC 2. *x* 드라이버 관리자입니다.  
  
## <a name="mappings-for-bookmark-operations"></a>책갈피 작업에 대 한 매핑  
 ODBC 3 *.x* 드라이버 관리자는 때 ODBC 3 다음 매핑을 수행 합니다. *x* 응용 프로그램을 사용 하는 ODBC 2. *x* 드라이버 책갈피 작업을 수행 합니다.  
  
### <a name="sqlbindcol"></a>SQLBindCol  
 때 ODBC 3. *x* 응용 프로그램을 사용 하는 ODBC 2. *x* 드라이버 호출 **SQLBindCol** 0 열로 바인딩할 *fCType* SQL_C_VARBOOKMARK, ODBC 3 같음 *.x* 확인 하는 드라이버 관리자 여부는 *BufferLength* 인수 보다 작거나 4 보다 크거나 4, 이며이 경우 SQLSTATE HY090 반환 (잘못 된 문자열 또는 버퍼 길이). 경우는 *BufferLength* 인수는 4, 드라이버 관리자를 호출 **SQLBindCol** 바꾼 후 드라이버에서 *fCType* SQL_C_BOOKMARK 사용 합니다.  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 때 ODBC 3. *x* 응용 프로그램을 사용 하는 ODBC 2. *x* 드라이버 호출 **SQLColAttribute** 와 *ColumnNumber* 드라이버 관리자 반환 인수를 0으로 설정 된 *FieldIdentifier* 값 다음 표에 나열 합니다.  
  
|*FieldIdentifier*|Value|  
|-----------------------|-----------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_FALSE|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|  
|SQL_DESC_CATALOG_NAME|""(빈 문자열)|  
|SQL_DESC_CONCISE_TYPE|SQL_BINARY|  
|SQL_DESC_COUNT|동일한 값을 반환 **SQLNumResultCols**|  
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
|SQL_DESC_UNNAMED|하면|  
|SQL_DESC_UNSIGNED|SQL_FALSE|  
|SQL_DESC_UPDATEABLE|SQL_ATTR_READ_ONLY|  
  
### <a name="sqldescribecol"></a>SQLDescribeCol  
 때 ODBC 3. *x* 응용 프로그램을 사용 하는 ODBC 2. *x* 드라이버 호출 **SQLDescribeCol** 와 *ColumnNumber* 0으로 설정 하는 인수를 드라이버 관리자는 다음 표에 나열 된 값을 반환 합니다.  
  
|버퍼|Value|  
|------------|-----------|  
|ColumnName|""(빈 문자열)|  
|* NameLengthPtr|0|  
|* DataTypePtr|SQL_BINARY|  
|* ColumnSizePtr|4|  
|* DecimalDigitsPtr|0|  
|* NullablePtr|SQL_NO_NULLS|  
  
### <a name="sqlgetdata"></a>SQLGetData  
 때 ODBC 3. *x* 응용 프로그램을 사용 하는 ODBC 2. *x* 드라이버는 다음 호출을 통해 **SQLGetData** 책갈피를 검색할 수 있습니다.  
  
```  
SQLGetData(StatementHandle, 0, SQL_C_VARBOOKMARK, TargetValuePtr, BufferLength, StrLen_or_IndPtr)  
```  
  
 호출에 매핑된 **SQLGetStmtOption** 와 *fOption* 다음과 같이 SQL_GET_BOOKMARK의:  
  
```  
SQLGetStmtOption(hstmt, SQL_GET_BOOKMARK, TargetValuePtr)  
```  
  
 여기서 *hstmt* 및 *pvParam* 의 값으로 설정 된 *StatementHandle* 및 *TargetValuePtr*각각. 책갈피 가리키는 버퍼에 반환 되는 *pvParam* (*TargetValuePtr*) 인수입니다. 가리키는 버퍼에 있는 값의 *StrLen_or_IndPtr* 호출에 인수 **SQLGetData** 가 4로 설정 합니다.  
  
 이 매핑은 되는 경우를 고려 하는 데 필요한 **SQLFetch** 호출 하기 전에 호출 된 **SQLGetData** 및 ODBC 2. *x* 드라이버를 지원 하지 않았으므로 **SQLExtendedFetch**합니다. 이 경우 **SQLFetch** ODBC 2를 통해 전달 될. *x* 드라이버를 사례 책갈피 검색 지원 되지 않습니다.  
  
 **SQLGetData** ODBC 2에서 여러 번 호출할 수 없습니다. *x* 호출에서 파트, 책갈피를 검색 하도록 드라이버에 **SQLGetData** 와 *BufferLength* 인수는 4 보다 작은 값으로 설정 및 *ColumnNumber*0으로 설정 하는 인수는 SQLSTATE HY090 반환 (잘못 된 문자열 또는 버퍼 길이). **그러나 SQLGetData** 수 동일한 책갈피를 검색 하는 여러 번 호출 합니다.  
  
### <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 때 ODBC 3. *x* 응용 프로그램을 사용 하는 ODBC 2. *x* 드라이버 호출 **SQLSetStmtAttr** 특성을 원본으로 사용 하는 ODBC 2에서 SQL_UB_ON 드라이버 관리자 SQL_ATTR_USE_BOOKMARKS 특성 SQL_UB_VARIABLE을으로 설정 하려면 설정 합니다. *x* 드라이버입니다.
