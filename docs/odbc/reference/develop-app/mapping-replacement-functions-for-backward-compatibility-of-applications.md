---
title: 앱의 호환성을 위한 대체 함수 매핑-ODBC | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b18669fe9b6edbd39859166e382ad18d1b04a99a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301093"
---
# <a name="mapping-replacement-functions-for-backward-compatibility-of-applications"></a>애플리케이션의 이전 버전과의 호환성을 위한 대체 함수 매핑
Odbc 3.x 드라이버 관리자를 통해 작업 하는 ODBC *2.x 응용 프로그램* 은 새로운 기능을 사용 하지 않는 *한 odbc* *2.x 드라이버에* 대해 작동 합니다. 그러나 중복 된 기능과 동작 변경 *모두 odbc 2.x 드라이버* *에서 odbc 2.x 응용 프로그램이* 작동 하는 방식에 영향을 줍니다. ODBC *2.x 드라이버를* 사용 하 여 작업 하는 경우 드라이버 관리자는 하나 이상의 odbc *2.x 함수를* *해당 ODBC 2.x 함수로 바꾼* 다음 odbc 2.x 함수 *를* 매핑합니다.  
  
|ODBC *3.x* 함수|ODBC *2.x* 함수|  
|-------------------------|-------------------------|  
|**SQLAllocHandle**|**Sqlallocenv**, **sqlallocenv**또는 **sqlallocenv**|  
|**SQLBulkOperations**|**SQLSetPos**|  
|**SQLColAttribute**|**SQLColAttributes**|  
|**SQLEndTran**|**SQLTransact**|  
|**SQLFetch**|**SQLExtendedFetch**|  
|**SQLFetchScroll**|**SQLExtendedFetch**|  
|**SQLFreeHandle**|**Sqlfreeenv**, **SQLFreeConnect**또는 **SQLFreeStmt**|  
|**SQLGetConnectAttr**|**SQLGetConnectOption**|  
|**SQLGetDiagRec**|**SQLError**|  
|**SQLGetStmtAttr**|**SQLGetStmtOption**[1]|  
|**SQLSetConnectAttr**|**SQLSetConnectOption**|  
|**SQLSetStmtAttr**|**SQLSetStmtOption**[1]|  
  
 [1] 요청 되는 특성에 따라 다른 작업을 수행할 수도 있습니다.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
 드라이버 관리자는이를 **Sqlallocenv**, **sqlallocenv**또는 **sqlallocenv**에 적절 하 게 매핑합니다. **SQLAllocHandle**에 대 한 다음 호출입니다.  
  
```  
SQLAllocHandle(HandleType, InputHandle, OutputHandlePtr);  
```  
  
 그러면 드라이버 관리자에서 다음을 수행 합니다 (개념, 오류 검사 안 함).  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLAllocEnv(OutputHandlePtr));  
   case SQL_HANDLE_DBC: return (SQLAllocConnect (InputHandle, OutputHandlePtr));  
   case SQL_HANDLE_STMT: return (SQLAllocStmt (InputHandle, OutputHandlePtr));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlbulkoperations"></a>SQLBulkOperations  
 드라이버 관리자는이를 **SQLSetPos**에 매핑합니다. **SQLBulkOperations**에 대 한 다음 호출입니다.  
  
```  
SQLBulkOperations(hstmt, Operation);  
```  
  
 는 다음과 같은 일련의 단계를 발생 합니다.  
  
1.  작업 인수가 SQL_ADD 이면 드라이버 관리자는 다음과 같이 **SQLSetPos** 를 호출 합니다.  
  
    ```  
    SQLSetPos (hstmt, 0, SQL_ADD, SQL_LOCK_NO_CHANGE);  
    ```  
  
2.  작업 인수가 SQL_ADD 되지 않은 경우 드라이버는 SQLSTATE HY092 (잘못 된 특성/옵션 식별자)를 반환 합니다.  
  
3.  응용 프로그램이 **Sqlfetch** 또는 **sqlfetchscroll** 및 **SQLBulkOperations**에 대 한 호출 사이에 SQL_ATTR_ROW_STATUS_PTR를 변경 하려고 하면 드라이버 관리자는 SQLSTATE HY011 (특성을 지금 설정할 수 없음)을 반환 합니다.  
  
4.  작업 인수가 SQL_ADD 이면 응용 프로그램에서 **SQLBindCol** 를 호출 하 여 삽입할 데이터를 바인딩해야 합니다. **SQLSetDescField** 또는 **SQLSetDescRec** 를 호출 하 여 삽입할 데이터를 바인딩할 수 없습니다.  
  
5.  작업 인수가 SQL_ADD이 고 삽입할 행 수가 현재 행 집합 크기와 같지 않은 경우 **SQLBulkOperations**를 호출 하기 전에 SQL_ATTR_ROW_ARRAY_SIZE statement 특성을 삽입할 행 수로 설정 하려면 **SQLSetStmtAttr** 를 호출 해야 합니다. 이전 행 집합 크기로 되돌리려면 **Sqlfetch**, **sqlfetchscroll**또는 **SQLSetPos** 를 호출 하기 전에 응용 프로그램에서 SQL_ATTR_ROW_ARRAY_SIZE statement 특성을 설정 해야 합니다.  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
 드라이버 관리자는이를 **Sqlcolattributes**에 매핑합니다. **Sqlcolattribute**에 대 한 다음 호출:  
  
```  
SQLColAttribute(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
```  
  
 는 다음과 같은 일련의 단계를 발생 합니다.  
  
1.  *FieldIdentifier* 가 다음 중 하나입니다.  
  
     SQL_DESC_PRECISION, SQL_DESC_SCALE, SQL_DESC_LENGTH, SQL_DESC_OCTET_LENGTH, SQL_DESC_UNNAMED, SQL_DESC_BASE_COLUMN_NAME, SQL_DESC_LITERAL_PREFIX, SQL_DESC_LITERAL_SUFFIX 또는 SQL_DESC_LOCAL_TYPE_NAME  
  
     드라이버 관리자는 SQLSTATE HY091 (잘못 된 설명자 필드 식별자)를 사용 하 여 SQL_ERROR을 반환 합니다. 이 섹션에 대 한 추가 규칙은 적용 되지 않습니다.  
  
2.  드라이버 관리자는 SQL_COLUMN_COUNT, SQL_COLUMN_NAME 또는 SQL_COLUMN_NULLABLE를 각각 SQL_DESC_COUNT, SQL_DESC_NAME 또는 SQL_DESC_NULLABLE에 매핑합니다. ODBC 2.x 드라이버는 SQL_DESC_COUNT, SQL_DESC_NAME 및 SQL_DESC_NULLABLE이 아닌 SQL_COLUMN_COUNT, SQL_COLUMN_NAME 및 SQL_COLUMN_NULLABLE 지원 하기만 하면 *됩니다.* SQLColAttribute에 대 한 호출은 다음에 매핑됩니다.  
  
    ```  
    SQLColAttributes(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
    ```  
  
3.  다른 모든 *FieldIdentifier* 값은 이전에 표시 된 대로 Sqlcolattribute에 매핑된 **sqlcolattribute** **를 사용** 하 여 드라이버에 전달 됩니다.  
  
4.  *Bufferlength* 가 0 보다 작은 경우 드라이버 관리자는 SQLSTATE HY090 (잘못 된 문자열 또는 버퍼 길이)를 사용 하 여 SQL_ERROR을 반환 합니다. 이 섹션에 대 한 추가 규칙은 적용 되지 않습니다.  
  
5.  *FieldIdentifier* 가 SQL_DESC_CONCISE_TYPE 되 고 반환 된 형식이 간결한 datetime 데이터 형식인 경우 드라이버 관리자는 날짜, 시간 및 타임 스탬프 코드에 대 한 반환 값을 매핑합니다.  
  
6.  드라이버 관리자는 필요한 검사를 수행 하 여 SQLSTATE HY010 (함수 시퀀스 오류)가 발생 해야 하는지 여부를 확인 합니다. 이 경우 드라이버 관리자는 SQL_ERROR 및 SQLSTATE HY010 (함수 시퀀스 오류)를 반환 합니다. 이 섹션에 대 한 추가 규칙은 적용 되지 않습니다.  
  
## <a name="sqlendtran"></a>SQLEndTran  
 드라이버 관리자는이를 **Sqltransact**에 매핑합니다. **Sqlendtran**에 대 한 다음 호출입니다.  
  
```  
SQLEndTran(HandleType, Handle, CompletionType);  
```  
  
 그러면 드라이버 관리자에서 다음을 수행 합니다 (개념, 오류 검사 안 함).  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV:return(SQLTransact(Handle, SQL_NULL_HDBC, CompletionType));  
   case SQL_HANDLE_DBC:return(SQLTransact(SQL_NULL_HENV, Handle, CompletionType);  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlfetch"></a>SQLFetch  
 드라이버 관리자는 SQL_FETCH_NEXT의 *Fetchorientation* 인수를 사용 하 여이를 **sqlextendedfetch** 에 매핑합니다. **Sqlfetch**에 대 한 다음 호출:  
  
```  
SQLFetch (StatementHandle);  
```  
  
 는 다음과 같이 **Sqlextendedfetch**를 호출 하는 드라이버 관리자를 생성 합니다.  
  
```  
rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, &RowCount, RowStatusArray);  
```  
  
 이 호출에서 *Pcrow* 인수는 **SQLSetStmtAttr**호출을 통해 응용 프로그램이 SQL_ATTR_ROWS_FETCHED_PTR statement 특성을로 설정 하는 값으로 설정 됩니다.  
  
> [!NOTE]  
>  응용 프로그램에서 **SQLSetStmtAttr** 를 호출 하 여 상태 배열을 가리키도록 SQL_ATTR_ROW_STATUS_PTR를 설정 하는 경우 드라이버 관리자는 포인터를 캐시 합니다. *Rowstatusarray* 는 null 포인터와 같을 수 있습니다.  
  
 드라이버가 **Sqlextendedfetch** 를 지원 하지 않고 커서 라이브러리가 로드 된 경우 드라이버 관리자는 커서 라이브러리의 **sqlextendedfetch** 를 사용 하 여 **Sqlfetch** 를 **sqlextendedfetch**에 매핑합니다. 드라이버가 **Sqlextendedfetch** 를 지원 하지 않고 커서 라이브러리가 로드 되지 않은 경우 드라이버 관리자는를 통해 **sqlfetch** 호출을 드라이버로 전달 합니다. 응용 프로그램에서 **SQLSetStmtAttr** 를 호출 하 여 SQL_ATTR_ROW_STATUS_PTR를 설정 하는 경우 드라이버 관리자는 배열이 채워지는지 확인 합니다. 응용 프로그램에서 **SQLSetStmtAttr** 를 호출 하 여 SQL_ATTR_ROWS_FETCHED_PTR를 설정 하는 경우 드라이버 관리자는이 필드를 1로 설정 합니다.  
  
## <a name="sqlfetchscroll"></a>SQLFetchScroll  
 드라이버 관리자는이를 **Sqlextendedfetch**에 매핑합니다. **Sqlfetchscroll**에 대 한 다음 호출:  
  
```  
SQLFetchScroll(StatementHandle, FetchOrientation, FetchOffset);  
```  
  
 는 다음과 같은 일련의 단계를 발생 합니다.  
  
1.  응용 프로그램에서 **SQLSetStmtAttr** 를 호출 하 여 상태 배열을 가리키도록 SQL_ATTR_ROW_STATUS_PTR (IRD의 SQL_DESC_ARRAY_STATUS_PTR 필드를 설정)를 호출 하면 드라이버 관리자가이 포인터를 캐시 합니다. 이 포인터를 *Rowstatusarray*로 지정 합니다. 그렇지 않으면 *Rowstatusarray* 를 null 포인터와 동일 하 게 만듭니다. *Rowstatusarray* 인수가 null 포인터로 설정 된 경우 드라이버 관리자는 행 상태 배열을 생성 합니다.  
  
2.  *Fetchorientation* 가 SQL_FETCH_NEXT, SQL_FETCH_PRIOR, SQL_FETCH_ABSOLUTE, SQL_FETCH_RELATIVE, SQL_FETCH_FIRST, SQL_FETCH_LAST 또는 SQL_FETCH_BOOKMARK 중 하나가 아닌 경우 드라이버 관리자는 SQL_ERROR 및 SQLSTATE HY106 (인출 유형 범위를 벗어남)로 반환 합니다. 이 섹션에 대 한 추가 규칙은 적용 되지 않습니다.  
  
3.  사례:  
  
-   *Fetchorientation* 가 SQL_FETCH_BOOKMARK 같은 경우 다음을 수행 합니다.  
  
    -   SQLSetStmtAttr SQL_ATTR_FETCH_BOOKMARK_PTR의 값을 설정 하기 위해 **SQLSetStmtAttr** 가 이전에 호출 된 경우에는 SQL_DESC_FETCH_BOOKMARK_PTR 포인터를 역참조 하 여 얻은 값으로 *Bmk* 수 있습니다.  
  
    -   그렇지 않으면 SQLSTATE HY111 (잘못 된 책갈피 값)를 사용 하 여 SQL_ERROR 반환 합니다. 이 섹션에 대 한 추가 규칙은 적용 되지 않습니다.  
  
     이제 드라이버 관리자는 다음과 같이 **Sqlextendedfetch**를 호출 합니다.  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, Bmk, pcRow, RowStatusArray);  
    ```  
  
-   그렇지 않으면 드라이버 관리자는 다음과 같이 **Sqlextendedfetch**를 호출 합니다.  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, pcRow, RowStatusArray);  
    ```  
  
     이러한 호출에서 *Pcrow* 인수는 **SQLSetStmtAttr**호출을 통해 응용 프로그램이 SQL_ATTR_ROWS_FETCHED_PTR statement 특성을로 설정 하는 값으로 설정 됩니다.  
  
-   SQL_ATTR_ROW_ARRAY_SIZE SQL_ROWSET_SIZE에 매핑됩니다.  
  
-   *Rc* 가 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO와 동일 하 고 *fetchorientation* 가 SQL_FETCH_BOOKMARK이 고 *fetchorientation* 이 0과 같지 않은 경우 드라이버 관리자는 경고, SQLSTATE 01S10 (책갈피 오프셋으로 인출 시도, 오프셋 값이 무시 됨)를 게시 하 고 SQL_SUCCESS_WITH_INFO를 반환 합니다.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 드라이버 관리자는이를 **Sqlfreeenv**, **SQLFreeConnect**또는 **SQLFreeStmt** 에 적절 하 게 매핑합니다. **Sqlfreehandle**에 대 한 다음 호출입니다.  
  
```  
SQLFreeHandle(HandleType, Handle);  
```  
  
 그러면 드라이버 관리자에서 다음을 수행 합니다 (개념, 오류 검사 안 함).  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLFreeEnv(Handle));  
   case SQL_HANDLE_DBC: return (SQLFreeConnect(Handle));  
   case SQL_HANDLE_STMT: return (SQLFreeStmt(Handle, SQL_DROP));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
 드라이버 관리자는이를 **SQLGetConnectOption**에 매핑합니다. **SQLGetConnectAttr**에 대 한 다음 호출입니다.  
  
```  
SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 는 다음과 같은 일련의 단계를 발생 합니다.  
  
1.  *특성이* 드라이버 정의 연결 또는 문 특성이 아니고 ODBC 2.x에 정의 된 특성이 아닌 경우 드라이버 관리자는 SQLSTATE HY092 (잘못 된 특성/옵션 식별자 *)를 사용*하 여 SQL_ERROR을 반환 합니다. 이 섹션에는 추가 규칙이 적용 되지 않습니다.  
  
2.  *특성이* SQL_ATTR_AUTO_IPD 또는 SQL_ATTR_METADATA_ID와 같으면 드라이버 관리자는 SQLSTATE HY092 (잘못 된 특성/옵션 식별자)를 사용 하 여 SQL_ERROR를 반환 합니다.  
  
3.  드라이버 관리자는 SQLSTATE 08003 (연결이 열려 있지 않음) 또는 SQLSTATE HY010 (함수 시퀀스 오류)가 발생 하는지 확인 하는 데 필요한 검사를 수행 합니다. 이 경우 드라이버 관리자는 SQL_ERROR를 반환 하 고 적절 한 오류 메시지를 게시 합니다. 이 섹션에 대 한 추가 규칙은 적용 되지 않습니다.  
  
4.  드라이버 관리자는 다음과 같이 **SQLGetConnectOption** 를 호출 합니다.  
  
    ```  
    SQLGetConnectOption (ConnectionHandle, Attribute, ValuePtr);  
    ```  
  
     *Bufferlength* 및 *StringLengthPtr* 는 무시 됩니다.  
  
## <a name="sqlgetdata"></a>SQLGetData  
 Odbc 2.x 드라이버를 사용 하 여 작업 하 *는 odbc* *2.X 응용 프로그램이* *columnnumber* 인수를 0으로 설정 하 여 **SQLGetData** 를 호출 *하면 odbc 3.x* 드라이버 관리자는 *Option* 특성이 SQL_GET_BOOKMARK로 설정 된 **SQLGetStmtOption** 에 대 한 호출에이를 매핑합니다.  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
 드라이버 관리자는이를 **SQLGetStmtOption**에 매핑합니다. **SQLGetStmtAttr**에 대 한 다음 호출입니다.  
  
```  
SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 는 다음과 같은 일련의 단계를 발생 합니다.  
  
1.  *특성이* 드라이버 정의 연결 또는 문 특성이 아니고 ODBC 2.x에 정의 된 특성이 아닌 경우 드라이버 관리자는 SQLSTATE HY092 (잘못 된 특성/옵션 식별자 *)를 사용*하 여 SQL_ERROR을 반환 합니다. 이 섹션에는 추가 규칙이 적용 되지 않습니다.  
  
2.  *특성* 은 다음 중 하나입니다.  
  
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
  
     드라이버 관리자는 SQLSTATE HY092 (잘못 된 특성/옵션 식별자)를 사용 하 여 SQL_ERROR을 반환 합니다. 이 섹션에 대 한 추가 규칙은 적용 되지 않습니다.  
  
3.  드라이버 관리자는 필요한 검사를 수행 하 여 SQLSTATE HY010 (함수 시퀀스 오류)가 발생 해야 하는지 여부를 확인 합니다. 이 경우 드라이버 관리자는 SQL_ERROR 및 SQLSTATE HY010 (함수 시퀀스 오류)를 반환 합니다. 이 섹션에 대 한 추가 규칙은 적용 되지 않습니다.  
  
4.  *특성이* SQL_ATTR_ROWS_FETCHED_PTR와 같은 경우 드라이버 관리자는 사용 하거나 **sqlextendedfetch**호출에서 사용 하는 내부 드라이버 관리자 변수 *crowa*에 대 한 포인터를 반환 합니다. 이 섹션에 대 한 추가 규칙은 적용 되지 않습니다.  
  
5.  *특성이* SQL_DESC_FETCH_BOOKMARK_PTR와 같으면 드라이버 관리자는 **SQLSetStmtAttr**를 호출 하는 동안 캐시 된 적절 한 포인터를 반환 합니다.  
  
6.  *특성이* SQL_ATTR_ROW_STATUS_PTR와 같으면 드라이버 관리자는 **SQLSetStmtAttr**를 호출 하는 동안 캐시 된 적절 한 포인터를 반환 합니다.  
  
7.  드라이버 관리자는 다음과 같이 **SQLGetStmtOption** 를 호출 합니다.  
  
    ```  
    SQLGetStmtOption (hstmt, fOption, pvParam);  
    ```  
  
     여기서 *hstmt*, *Foption*및 *pvParam* 는 각각 *StatementHandle*, *Attribute*및 *valueptr*의 값으로 설정 됩니다. *Bufferlength* 및 *StringLengthPtr* 는 무시 됩니다.  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
 드라이버 관리자는이를 **SQLSetConnectOption**에 매핑합니다. **SQLSetConnectAttr**에 대 한 다음 호출입니다.  
  
```  
SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, StringLength);  
```  
  
 는 다음과 같은 일련의 단계를 발생 합니다.  
  
1.  *특성이* 드라이버 정의 연결 또는 문 특성이 아니고 ODBC 2.x에 정의 된 특성이 아닌 경우 드라이버 관리자는 SQLSTATE HY092 (잘못 된 특성/옵션 식별자 *)를 사용*하 여 SQL_ERROR을 반환 합니다. 이 섹션에는 추가 규칙이 적용 되지 않습니다.  
  
2.  *특성이* SQL_ATTR_AUTO_IPD와 같으면 드라이버 관리자는 SQLSTATE HY092 (잘못 된 특성/옵션 식별자)를 사용 하 여 SQL_ERROR을 반환 합니다.  
  
3.  드라이버 관리자는 필요한 검사를 수행 하 여 SQLSTATE 08003 (연결이 열려 있지 않음) 또는 SQLSTATE HY010 (함수 시퀀스 오류)를 발생 시켜야 하는지 확인 합니다. 이러한 오류 중 하나를 발생 시켜야 하는 경우 드라이버 관리자는 SQL_ERROR를 반환 하 고 적절 한 오류 메시지를 게시 합니다. 이 섹션에 대 한 추가 규칙은 적용 되지 않습니다.  
  
4.  드라이버 관리자는 다음과 같이 **SQLSetConnectOption** 를 호출 합니다.  
  
    ```  
    SQLSetConnectOption (hdbc, fOption, vParam);  
    ```  
  
     여기서 *hdbc*, *Foption*및 *vparam* 은 각각 *ConnectionHandle*, *Attribute*및 *veptr*의 값으로 설정 됩니다. *StringLengthPtr* 은 무시 됩니다.  
  
> [!NOTE]  
>  연결 수준에서 문 특성을 설정 하는 기능은 더 이상 사용 되지 않습니다. 문 특성 *은 ODBC 3.x* 응용 프로그램에 의해 연결 수준에서 설정 하면 안 됩니다.  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 드라이버 관리자는이를 **SQLSetStmtOption**에 매핑합니다. **SQLSetStmtAttr**에 대 한 다음 호출입니다.  
  
```  
SQLSetStmtAttr(StatementHandle, Attribute, ValuePtr, StringLength);  
```  
  
 는 다음과 같은 일련의 단계를 발생 합니다.  
  
1.  *특성이* 드라이버 정의 연결 또는 문 특성이 아니고 ODBC 2.x에 정의 된 특성이 아닌 경우 드라이버 관리자는 SQLSTATE HY092 (잘못 된 특성/옵션 식별자 *)를 사용*하 여 SQL_ERROR을 반환 합니다. 이 섹션에는 추가 규칙이 적용 되지 않습니다.  
  
2.  *특성* 은 다음 중 하나입니다.  
  
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
  
     드라이버 관리자는 SQLSTATE HY092 (잘못 된 특성/옵션 식별자)를 사용 하 여 SQL_ERROR을 반환 합니다. 이 섹션에 대 한 추가 규칙은 적용 되지 않습니다.  
  
3.  드라이버 관리자는 필요한 검사를 수행 하 여 SQLSTATE HY010 (함수 시퀀스 오류)가 발생 해야 하는지 여부를 확인 합니다. 이 경우 드라이버 관리자는 SQL_ERROR 및 SQLSTATE HY010 (함수 시퀀스 오류)를 반환 합니다. 이 섹션에 대 한 추가 규칙은 적용 되지 않습니다.  
  
4.  *특성이* SQL_ATTR_PARAMSET_SIZE 또는 SQL_ATTR_PARAMS_PROCESSED_PTR와 같은 경우이 항목의 뒷부분에 나오는 "매개 변수 배열 처리를 위한 매핑" 단원을 참조 하십시오. 이 섹션에 대 한 추가 규칙은 적용 되지 않습니다.  
  
5.  *특성이* SQL_ATTR_ROWS_FETCHED_PTR와 같으면 드라이버 관리자는 나중에 **sqlfetchscroll**에서 사용할 포인터 값을 캐시 합니다.  
  
6.  *특성이* SQL_ATTR_ROW_STATUS_PTR와 같으면 드라이버 관리자는 나중에 **sqlfetchscroll** 또는 **SQLSetPos**에서 사용할 포인터 값을 캐시 합니다. 이 섹션에 대 한 추가 규칙은 적용 되지 않습니다.  
  
7.  *특성이* SQL_ATTR_FETCH_BOOKMARK_PTR와 같으면 드라이버 관리자는 이상 값을 캐시 *하 고* **sqlfetchscroll**에 대 한 호출에서 나중에 캐시 된 값을 사용 합니다. 이 섹션에 대 한 추가 규칙은 적용 되지 않습니다.  
  
8.  드라이버 관리자는 다음과 같이 **SQLSetStmtOption** 를 호출 합니다.  
  
    ```  
    SQLSetStmtOption (hstmt, fOption, vParam);  
    ```  
  
     여기서 *hstmt*, *Foption*및 *vparam* 은 각각 *StatementHandle*, *Attribute*및 *veptr*의 값으로 설정 됩니다. *Stringlength* 인수는 무시 됩니다.  
  
     ODBC 2.x 드라이버가 문자 문자열 드라이버 관련 문 옵션을 지 원하는 *경우 odbc 2.x* 응용 프로그램은 **SQLSetStmtOption** 를 호출 하 여 이러한 옵션을 설정 해야 *합니다.*  
  
## <a name="mappings-for-handling-parameter-arrays"></a>매개 변수 배열 처리를 위한 매핑  
 응용 프로그램에서 다음을 호출 하는 경우:  
  
```  
SQLSetStmtAttr (StatementHandle, SQL_ATTR_PARAMSET_SIZE, Size, StringLength);  
```  
  
 드라이버 관리자는 다음을 호출 합니다.  
  
```  
SQLParamOptions (StatementHandle, Size, &RowCount);  
```  
  
 나중에 드라이버 관리자는 응용 프로그램에서 **SQLGetStmtAttr** 를 호출 하 여 SQL_ATTR_PARAMS_PROCESSED_PTR를 검색할 때이 변수에 대 한 포인터를 반환 합니다. 문 핸들이 준비 됨 또는 할당 됨 상태로 반환 될 때까지 드라이버 관리자는이 내부 변수를 변경할 수 없습니다.  
  
 ODBC 3.x 응용 프로그램은 APD에서 SQL_DESC_ARRAY_SIZE 필드를 명시적으로 설정 하지 않은 경우에도 **SQLGetStmtAttr** 를 호출 하 여 SQL_ATTR_PARAMS_PROCESSED_PTR 값을 가져올 수 *있습니다.* 예를 들어 **Sqlexecute** 가 SQL_NEED_DATA 반환 될 때 처리 되는 매개 변수의 현재 "행"을 확인 하는 일반 루틴이 응용 프로그램에 있는 경우 이러한 상황이 발생할 수 있습니다. 이 루틴은 SQL_DESC_ARRAY_SIZE 1 인지 아니면 1 보다 큰지를 호출 합니다. 이를 고려 하기 위해 드라이버 관리자는 응용 프로그램에서 APD의 SQL_DESC_ARRAY_SIZE 필드를 설정 하는 데 **SQLSetStmtAttr** 를 호출 했는지 여부에 관계 없이이 내부 변수를 정의 해야 합니다. SQL_DESC_ARRAY_SIZE를 설정 하지 않은 경우에는 **Sqlexecdirect** 또는 **sqlexecute**에서 반환 하기 전에 드라이버 관리자가이 변수에 값 1이 포함 되어 있는지 확인 해야 합니다.  
  
## <a name="error-handling"></a>오류 처리  
 ODBC 3.x에서 **Sqlfetch** 또는 **sqlfetchscroll** 을 *호출 하면 IRD*의 SQL_DESC_ARRAY_STATUS_PTR 채워지고 지정 된 진단 레코드의 SQL_DIAG_ROW_NUMBER 필드에는이 레코드가 관련 된 행 집합의 행 번호가 포함 됩니다. 이를 사용 하면 응용 프로그램에서 지정 된 행 위치와 오류 메시지의 상관 관계를 지정할 수 있습니다.  
  
 ODBC 2.x 드라이버는이 기능을 제공할 수 *없습니다.* 그러나 SQLSTATE 01S01 (행 오류)와 함께 오류 경계을 제공 합니다. ODBC *2.x 드라이버를* 사용 하는 동안 **Sqlfetch** 또는 **SQLFETCHSCROLL** 을 사용 하는 odbc *3(sp3)* 응용 프로그램은 이러한 사실을 인식 해야 합니다. 또한 이러한 응용 프로그램은 **SQLGetDiagField** 를 호출 하 여 실제로 SQL_DIAG_ROW_NUMBER 필드를 가져올 수 없습니다. Odbc 2.x 드라이버를 사용 하 여 작업 하는 *odbc* *2.x 응용 프로그램* 은 SQL_DIAG_MESSAGE_TEXT, SQL_DIAG_NATIVE, SQL_DIAG_RETURNCODE 또는 SQL_DIAG_SQLSTATE의 *DiagIdentifier* 인수를 사용 하 여 **SQLGetDiagField** 를 호출할 수 있습니다. Odbc 3.x *드라이버 관리자* 는 odbc *2.x 드라이버를* 사용 하는 경우 진단 데이터 구조를 유지 *하지만 odbc 2.x* 드라이버는 이러한 4 개의 필드만 반환 합니다.  
  
 *Odbc 2.x 응용 프로그램* 에서 odbc *2.x 드라이버를* 사용 하 여 작업 하는 경우 드라이버 관리자에서 여러 오류를 반환할 수 있는 경우 odbc *2.x 드라이버 관리자* *에서 odbc 2.x* 드라이버 관리자에 비해 다른 오류가 반환 될 수 있습니다.  
  
## <a name="mappings-for-bookmark-operations"></a>책갈피 작업 매핑  
 Odbc 3.x *드라이버 관리자* *는 odbc 2.x 드라이버를* 사용 하 여 작업 하 *는 odbc 2.x 응용 프로그램이* 책갈피 작업을 수행할 때 다음 매핑을 수행 합니다.  
  
### <a name="sqlbindcol"></a>SQLBindCol  
 Odbc 2.x 드라이버를 사용 하 여 작업 하 *는 odbc* *2.X 응용 프로그램이* **SQLBindCol** 와 SQL_C_VARBOOKMARK 동일한 *fctype* 을 사용 하 여 열 0에 바인딩하려는 *경우 odbc 3.x* 드라이버 관리자는 *bufferlength* 인수가 4 보다 작거나 4 보다 큰지 확인 하 고, 그럴 경우 SQLSTATE HY090 (잘못 된 문자열 또는 버퍼 길이)를 반환 합니다. *Bufferlength* 인수가 4 이면 드라이버 관리자는 *fctype* 을 SQL_C_BOOKMARK로 바꾼 후 드라이버에서 **SQLBindCol** 를 호출 합니다.  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 *Odbc 2.x 드라이버를* 사용 하 여 작업 하는 odbc *3(Sp3)* 응용 프로그램이 *columnnumber* 인수를 0으로 설정 하 여 **Sqlcolattribute** 를 호출 하면 드라이버 관리자는 다음 표에 나열 된 *FieldIdentifier* 값을 반환 합니다.  
  
|*FieldIdentifier*|값|  
|-----------------------|-----------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_FALSE|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|  
|SQL_DESC_CATALOG_NAME|""(빈 문자열)|  
|SQL_DESC_CONCISE_TYPE|SQL_BINARY|  
|SQL_DESC_COUNT|**Sqlnumresultcols** 에서 반환 된 것과 동일한 값|  
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
 Odbc 2.x 드라이버를 사용 하 여 작업 하 *는 odbc* *2.X 응용 프로그램이* *columnnumber* 인수를 0으로 설정 하 여 **SQLDescribeCol** 를 호출 하면 드라이버 관리자는 다음 표에 나열 된 값을 반환 합니다.  
  
|Buffer|값|  
|------------|-----------|  
|ColumnName|""(빈 문자열)|  
|*NameLengthPtr|0|  
|*DataTypePtr|SQL_BINARY|  
|*ColumnSizePtr|4|  
|*DecimalDigitsPtr|0|  
|*NullablePtr|SQL_NO_NULLS|  
  
### <a name="sqlgetdata"></a>SQLGetData  
 *Odbc 2.x 응용 프로그램* 에서 odbc *2.x 드라이버를* 사용 하 여 작업 하는 경우 **SQLGetData** 를 호출 하 여 책갈피를 검색 합니다.  
  
```  
SQLGetData(StatementHandle, 0, SQL_C_VARBOOKMARK, TargetValuePtr, BufferLength, StrLen_or_IndPtr)  
```  
  
 호출은 다음과 같이 SQL_GET_BOOKMARK의 *Foption* 을 사용 하 여 **SQLGetStmtOption** 에 매핑됩니다.  
  
```  
SQLGetStmtOption(hstmt, SQL_GET_BOOKMARK, TargetValuePtr)  
```  
  
 여기서 *hstmt* 및 *PvParam* 는 각각 *StatementHandle* 및 *targetvalueptr*의 값으로 설정 됩니다. 책갈피는 *pvParam* (*targetvalueptr*) 인수가 가리키는 버퍼에서 반환 됩니다. **SQLGetData** 호출에서 *StrLen_or_IndPtr* 인수가 가리키는 버퍼의 값이 4로 설정 됩니다.  
  
 이 매핑은 **SQLGetData** 를 호출 하기 전에 **sqlfetch** 를 호출한 경우 *와 ODBC 2.x* 드라이버가 **sqlextendedfetch**를 지원 하지 않는 경우를 고려 하는 데 필요 합니다. 이 경우 **Sqlfetch** 는 ODBC 2.x 드라이버로 전달 *됩니다 .이* 경우 책갈피 검색은 지원 되지 않습니다.  
  
 ODBC *2.x 드라이버에서* **sqlgetdata** 를 여러 번 호출 하 여 파트에서 책갈피를 검색할 수 없으므로 *bufferlength* 인수가 4 보다 작은 값으로 설정 된 **sqlgetdata** 를 호출 하 고 *COLUMNNUMBER* 인수를 0으로 설정 하면 SQLSTATE HY090 (잘못 된 문자열 또는 버퍼 길이)가 반환 됩니다. 그러나 **SQLGetData** 는 동일한 책갈피를 검색 하기 위해 여러 번 호출 될 수 있습니다.  
  
### <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 Odbc 2.x 드라이버를 사용 하 여 작업 하 *는 odbc* *2.X 응용 프로그램이* **SQLSetStmtAttr** 를 호출 하 여 SQL_ATTR_USE_BOOKMARKS 특성을 SQL_UB_VARIABLE로 설정 하면 드라이버 관리자는 기본 ODBC 2.x 드라이버에서 특성을 SQL_UB_ON로 설정 *합니다.*
