---
title: 앱 의 호환성을 위한 매핑 교체 기능 - ODBC | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301093"
---
# <a name="mapping-replacement-functions-for-backward-compatibility-of-applications"></a>애플리케이션의 이전 버전과의 호환성을 위한 대체 함수 매핑
ODBC *3.x* *드라이버* 관리자를 통해 작동하는 ODBC 3.x 응용 프로그램은 새로운 기능이 사용되지 않는 한 ODBC *2.x* 드라이버에 대해 작동합니다. 그러나 중복된 기능과 동작 변경은 ODBC *3.x* 응용 프로그램이 ODBC *2.x* 드라이버에서 작동하는 방식에 영향을 미칩니다. ODBC *2.x* 드라이버로 작업할 때 드라이버 관리자는 하나 이상의 ODBC *2.x* 함수를 대체한 다음 ODBC *3.x* 함수를 해당 ODBC *2.x* 함수에 매핑합니다.  
  
|ODBC *3.x* 기능|ODBC *2.x* 기능|  
|-------------------------|-------------------------|  
|**SQLAlloc핸들**|**SQLAllocEnv**, **SQLAllocConnect,** 또는 **SQLAllocStmt**|  
|**SQLBulk운영**|**SQLSetPos**|  
|**SQLColAttribute**|**SQLCol속성**|  
|**SQLEndTran**|**SQLTransact**|  
|**SQLFetch**|**SQLExtendedFetch**|  
|**SQLFetchScroll**|**SQLExtendedFetch**|  
|**SQLFreeHandle**|**SQLFreeEnv**, **SQLFreeConnect,** 또는 **SQLFreeStmt**|  
|**SQLGetConnectAttr**|**SQLGet연결 옵션**|  
|**SQLGetDiagRec**|**SQL오류**|  
|**SQLGetStmtAttr**|**SQLGetStmt옵션**[1]|  
|**SQLSetConnectAttr**|**SQLSet연결옵션**|  
|**SQLSetStmtAttr**|**SQLSetStmt옵션**[1]|  
  
 [1] 요청되는 특성에 따라 다른 작업도 수행할 수 있습니다.  
  
## <a name="sqlallochandle"></a>SQLAlloc핸들  
 드라이버 관리자는 이를 **SQLAllocEnv,** **SQLAllocConnect**또는 **SQLAllocStmt에**적절하게 매핑합니다. **SQLAllocHandle에**대한 다음 호출 :  
  
```  
SQLAllocHandle(HandleType, InputHandle, OutputHandlePtr);  
```  
  
 드라이버 관리자가 다음(개념적, 오류 확인 없음) 매핑을 수행하게 됩니다.  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLAllocEnv(OutputHandlePtr));  
   case SQL_HANDLE_DBC: return (SQLAllocConnect (InputHandle, OutputHandlePtr));  
   case SQL_HANDLE_STMT: return (SQLAllocStmt (InputHandle, OutputHandlePtr));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlbulkoperations"></a>SQLBulk운영  
 드라이버 관리자는 이를 **SQLSetPos에**매핑합니다. **SQLBulkOperations에**대한 다음 호출 :  
  
```  
SQLBulkOperations(hstmt, Operation);  
```  
  
 다음 단계 순서가 생성됩니다.  
  
1.  작업 인수가 SQL_ADD 경우 드라이버 관리자는 다음과 같이 **SQLSetPos를** 호출합니다.  
  
    ```  
    SQLSetPos (hstmt, 0, SQL_ADD, SQL_LOCK_NO_CHANGE);  
    ```  
  
2.  작업 인수가 SQL_ADD 않으면 드라이버는 SQLSTATE HY092(잘못된 특성/옵션 식별자)를 반환합니다.  
  
3.  응용 프로그램이 **SQLFetch** 또는 **SQLFetchScroll** 및 **SQLBulkOperations에**대한 호출 간에 SQL_ATTR_ROW_STATUS_PTR 변경하려고 하면 드라이버 관리자가 SQLSTATE HY011을 반환합니다(특성은 지금 설정할 수 없음).  
  
4.  작업 인수가 SQL_ADD 경우 응용 프로그램은 **SQLBindCol을** 호출하여 삽입할 데이터를 바인딩해야 합니다. 삽입할 데이터를 바인딩하기 위해 **SQLSetDescField** 또는 **SQLSetDescRec를** 호출할 수 없습니다.  
  
5.  작업 인수가 SQL_ADD 삽입할 행 수가 현재 행 집합 크기와 같지 않은 경우 **SQLSetStmtAttr을** 호출하여 **SQLBulkOperations**를 호출하기 전에 삽입할 행 수에 SQL_ATTR_ROW_ARRAY_SIZE 문 특성을 설정해야 합니다. 이전 행 집합 크기로 되돌리려면 **SQLFetch,** **SQLFetchScroll**또는 **SQLSetPos가** 호출되기 전에 응용 프로그램에서 SQL_ATTR_ROW_ARRAY_SIZE 문 특성을 설정해야 합니다.  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
 드라이버 관리자는 이를 **SQLColAttributes에 매핑합니다.** **SQLColAttribute에**대한 다음 호출 :  
  
```  
SQLColAttribute(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
```  
  
 다음 단계 순서가 생성됩니다.  
  
1.  *필드식별자가* 다음 중 하나인 경우:  
  
     SQL_DESC_PRECISION, SQL_DESC_SCALE, SQL_DESC_LENGTH, SQL_DESC_OCTET_LENGTH, SQL_DESC_UNNAMED, SQL_DESC_BASE_COLUMN_NAME, SQL_DESC_LITERAL_PREFIX, SQL_DESC_LITERAL_SUFFIX 또는 SQL_DESC_LOCAL_TYPE_NAME  
  
     드라이버 관리자는 SQLSTATE HY091(잘못된 설명자 필드 식별자)을 통해 SQL_ERROR 반환합니다. 이 섹션의 추가 규칙은 적용되지 않습니다.  
  
2.  드라이버 관리자는 SQL_COLUMN_COUNT, SQL_COLUMN_NAME 또는 SQL_COLUMN_NULLABLE 각각 SQL_DESC_COUNT, SQL_DESC_NAME 또는 SQL_DESC_NULLABLE 매핑합니다. (ODBC *2.x* 드라이버는 SQL_DESC_COUNT, SQL_DESC_NAME 및 SQL_DESC_NULLABLE 아닌 SQL_COLUMN_COUNT, SQL_COLUMN_NAME 및 SQL_COLUMN_NULLABLE 지원만 하면 됩니다. SQLColAttribute에 대한 호출은 다음과 같은 매핑으로 표시됩니다.  
  
    ```  
    SQLColAttributes(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
    ```  
  
3.  다른 모든 *FieldIdentifier* 값은 **SQLColAttribute가** 이전에 표시된 것처럼 **SQLColAttribute에** 매핑된 드라이버로 전달됩니다.  
  
4.  *BufferLength가* 0보다 적으면 드라이버 관리자는 SQLSTATE HY090(잘못된 문자열 또는 버퍼 길이)을 SQL_ERROR 반환합니다. 이 섹션의 추가 규칙은 적용되지 않습니다.  
  
5.  *FieldIdentifier가* SQL_DESC_CONCISE_TYPE 반환된 형식이 간결한 날짜 시간 데이터 형식인 경우 드라이버 관리자는 날짜, 시간 및 타임스탬프 코드에 대한 반환 값을 매핑합니다.  
  
6.  드라이버 관리자는 SQLSTATE HY010(함수 시퀀스 오류)을 발생시켜야 하는지 여부를 확인하기 위해 필요한 검사를 수행합니다. 이 경우 드라이버 관리자는 SQL_ERROR 및 SQLSTATE HY010(함수 시퀀스 오류)을 반환합니다. 이 섹션의 추가 규칙은 적용되지 않습니다.  
  
## <a name="sqlendtran"></a>SQLEndTran  
 드라이버 관리자는 이를 **SQLTransact에**매핑합니다. **SQLEndTran에**대한 다음 호출 :  
  
```  
SQLEndTran(HandleType, Handle, CompletionType);  
```  
  
 드라이버 관리자가 다음(개념적, 오류 확인 없음) 매핑을 수행하게 됩니다.  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV:return(SQLTransact(Handle, SQL_NULL_HDBC, CompletionType));  
   case SQL_HANDLE_DBC:return(SQLTransact(SQL_NULL_HENV, Handle, CompletionType);  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlfetch"></a>SQLFetch  
 드라이버 관리자는 SQL_FETCH_NEXT *FetchOrientation* 인수를 사용하여 **SQLExtendedFetch에** 이 것을 매핑합니다. **SQLFetch에**대한 다음 호출 :  
  
```  
SQLFetch (StatementHandle);  
```  
  
 다음과 같이 드라이버 관리자가 **SQLExtendedFetch를**호출합니다.  
  
```  
rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, &RowCount, RowStatusArray);  
```  
  
 이 호출에서 *pcRow* 인수는 응용 프로그램이 **SQLSetStmtAtTr에**대한 호출을 통해 SQL_ATTR_ROWS_FETCHED_PTR 문 특성을 설정하는 값으로 설정됩니다.  
  
> [!NOTE]  
>  응용 프로그램이 **SQLSetStmtAttr을** 호출하여 상태 배열을 가리키는 SQL_ATTR_ROW_STATUS_PTR 설정하면 드라이버 관리자는 포인터를 캐시합니다. *RowStatusArray는* null 포인터와 같을 수 있습니다.  
  
 드라이버가 **SQLExtendedFetch를** 지원하지 않고 커서 라이브러리가 로드된 경우 드라이버 관리자는 커서 라이브러리의 **SQLExtendedFetch를** 사용하여 **SQLExtendedFetch** 에 **SQLFetch를**매핑합니다. 드라이버가 **SQLExtendedFetch를** 지원하지 않고 커서 라이브러리가 로드되지 않은 경우 드라이버 관리자는 **SQLFetch에** 대한 호출을 드라이버로 전달합니다. 응용 프로그램이 **SQLSetStmtAttr을** 호출하여 SQL_ATTR_ROW_STATUS_PTR 설정하는 경우 드라이버 관리자는 배열이 채워지는지 확인합니다. 응용 프로그램이 **SQLSetStmtAttr을** 호출하여 SQL_ATTR_ROWS_FETCHED_PTR 설정하면 드라이버 관리자는 이 필드를 1로 설정합니다.  
  
## <a name="sqlfetchscroll"></a>SQLFetchScroll  
 드라이버 관리자는 이를 **SQLExtendedFetch**에 매핑합니다. **SQLFetchScroll에**대한 다음 호출 :  
  
```  
SQLFetchScroll(StatementHandle, FetchOrientation, FetchOffset);  
```  
  
 다음 단계 순서가 생성됩니다.  
  
1.  응용 프로그램이 **SQLSetStmtAttr을** 호출하여 상태 배열을 가리키는 SQL_ATTR_ROW_STATUS_PTR(IRD의 SQL_DESC_ARRAY_STATUS_PTR 필드를 설정)로 설정하면 드라이버 관리자는 이 포인터를 캐시합니다. 이 포인터를 *RowStatusArray가*되게 하십시오. 그렇지 않으면 *RowStatusArray를* null 포인터와 같게 합니다. *RowStatusArray* 인수가 null 포인터로 설정된 경우 드라이버 관리자는 행 상태 배열을 생성합니다.  
  
2.  *FetchOrientation* SQL_FETCH_NEXT, SQL_FETCH_PRIOR, SQL_FETCH_ABSOLUTE, SQL_FETCH_RELATIVE, SQL_FETCH_FIRST, SQL_FETCH_LAST 또는 SQL_FETCH_BOOKMARK 중 하나가 아닌 경우 드라이버 관리자는 SQL_ERROR 및 SQLSTATE HY106(가져오기 형식 범위를 벗어나는 형식)으로 반환합니다. 이 섹션의 추가 규칙은 적용되지 않습니다.  
  
3.  사례:  
  
-   *FetchOrientation이* SQL_FETCH_BOOKMARK 같으면 다음을 수행합니다.  
  
    -   **SQLSetStmtAttr이** SQL_ATTR_FETCH_BOOKMARK_PTR 값을 설정하기 위해 이전에 호출된 경우 *Bmk가* 포인터 SQL_DESC_FETCH_BOOKMARK_PTR 다시 참조하여 얻은 값입니다.  
  
    -   그렇지 않으면 SQLSTATE HY111(잘못된 책갈피 값)으로 SQL_ERROR 반환합니다. 이 섹션의 추가 규칙은 적용되지 않습니다.  
  
     드라이버 관리자는 이제 다음과 같이 **SQLExtendedFetch를**호출합니다.  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, Bmk, pcRow, RowStatusArray);  
    ```  
  
-   그렇지 않으면 드라이버 관리자는 다음과 같이 **SQLExtendedFetch를**호출합니다.  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, pcRow, RowStatusArray);  
    ```  
  
     이러한 호출에서 *pcRow* 인수는 응용 프로그램이 **SQLSetStmtAtTr**에 대한 호출을 통해 SQL_ATTR_ROWS_FETCHED_PTR 문 특성을 설정하는 값으로 설정됩니다.  
  
-   SQL_ATTR_ROW_ARRAY_SIZE SQL_ROWSET_SIZE 매핑됩니다.  
  
-   *rc가* SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO 같고 *FetchOrientation가* SQL_FETCH_BOOKMARK 같고 *FetchOffset이* 0과 같지 않은 경우 드라이버 관리자는 경고, SQLSTATE 01S10(책갈피 오프셋으로 가져오기 시도, 오프셋 값 무시됨)을 게시하고 SQL_SUCCESS_WITH_INFO 반환합니다.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 드라이버 관리자는 이를 **SQLFreeEnv,** **SQLFreeConnect**또는 **SQLFreeStmt에** 적절하게 매핑합니다. **SQLFreeHandle에**대한 다음 호출 :  
  
```  
SQLFreeHandle(HandleType, Handle);  
```  
  
 드라이버 관리자가 다음(개념적, 오류 확인 없음) 매핑을 수행하게 됩니다.  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLFreeEnv(Handle));  
   case SQL_HANDLE_DBC: return (SQLFreeConnect(Handle));  
   case SQL_HANDLE_STMT: return (SQLFreeStmt(Handle, SQL_DROP));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
 드라이버 관리자는 이를 **SQLGetConnectOption에**매핑합니다. **SQLGetConnectAttr에**대한 다음 호출 :  
  
```  
SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 다음 단계 순서가 생성됩니다.  
  
1.  *특성이* 드라이버 정의 연결 또는 문 특성이 아니며 ODBC *2.x에*정의된 특성이 아닌 경우 드라이버 관리자는 SQLSTATE HY092(잘못된 특성/옵션 식별자)를 통해 SQL_ERROR 반환합니다. 이 섹션의 추가 규칙은 적용되지 않습니다.  
  
2.  *특성이* SQL_ATTR_AUTO_IPD 또는 SQL_ATTR_METADATA_ID 같으면 드라이버 관리자는 SQLSTATE HY092(잘못된 특성/옵션 식별자)를 사용하여 SQL_ERROR 반환합니다.  
  
3.  드라이버 관리자는 SQLSTATE 08003(연결이 열리지 않음) 또는 SQLSTATE HY010(함수 시퀀스 오류)을 발생시켜야 하는지 확인하기 위해 필요한 검사를 수행합니다. 이 경우 드라이버 관리자는 SQL_ERROR 반환하고 적절한 오류 메시지를 게시합니다. 이 섹션의 추가 규칙은 적용되지 않습니다.  
  
4.  드라이버 관리자는 다음과 같이 **SQLGetConnectOption을** 호출합니다.  
  
    ```  
    SQLGetConnectOption (ConnectionHandle, Attribute, ValuePtr);  
    ```  
  
     *버퍼 길이* 및 *문자열LengthPtr은* 무시됩니다.  
  
## <a name="sqlgetdata"></a>SQLGetData  
 ODBC *2.x* 드라이버로 작업하는 ODBC *3.x* 응용 프로그램이 *columnNumber* 인수를 0과 같은 으로 **SQLGetData를** 호출하면 ODBC *3.x* 드라이버 관리자는 SQL_GET_BOOKMARK 설정된 *옵션* 특성을 사용하여 **SQLGetStmtOption에** 대한 호출에 이 것을 매핑합니다.  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
 드라이버 관리자는 이를 **SQLGetStmt옵션에**매핑합니다. **SQLGetStmtAttr에**대한 다음 호출 :  
  
```  
SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 다음 단계 순서가 생성됩니다.  
  
1.  *특성이* 드라이버 정의 연결 또는 문 특성이 아니며 ODBC *2.x에*정의된 특성이 아닌 경우 드라이버 관리자는 SQLSTATE HY092(잘못된 특성/옵션 식별자)를 통해 SQL_ERROR 반환합니다. 이 섹션의 추가 규칙은 적용되지 않습니다.  
  
2.  *특성이* 다음 중 하나인 경우:  
  
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
  
     드라이버 관리자는 SQLSTATE HY092(잘못된 특성/옵션 식별자)를 사용 하 SQL_ERROR 반환 합니다. 이 섹션의 추가 규칙은 적용되지 않습니다.  
  
3.  드라이버 관리자는 SQLSTATE HY010(함수 시퀀스 오류)을 발생시켜야 하는지 여부를 확인하기 위해 필요한 검사를 수행합니다. 이 경우 드라이버 관리자는 SQL_ERROR 및 SQLSTATE HY010(함수 시퀀스 오류)을 반환합니다. 이 섹션의 추가 규칙은 적용되지 않습니다.  
  
4.  *특성이* SQL_ATTR_ROWS_FETCHED_PTR 같으면 드라이버 관리자는 **SQLExtendedFetch**에 대한 호출에서 사용했거나 사용할 내부 드라이버 관리자 변수 *cRow에*대한 포인터를 반환합니다. 이 섹션의 추가 규칙은 적용되지 않습니다.  
  
5.  *특성이* SQL_DESC_FETCH_BOOKMARK_PTR 같으면 드라이버 관리자는 **SQLSetStmtAttr**을 호출하는 동안 캐시한 적절한 포인터를 반환합니다.  
  
6.  *특성이* SQL_ATTR_ROW_STATUS_PTR 같으면 드라이버 관리자는 **SQLSetStmtAttr**을 호출하는 동안 캐시한 적절한 포인터를 반환합니다.  
  
7.  드라이버 관리자는 다음과 같이 **SQLGetStmtOption을** 호출합니다.  
  
    ```  
    SQLGetStmtOption (hstmt, fOption, pvParam);  
    ```  
  
     여기서 *hstmt*, *fOption*및 *pvParam은* 각각 *문핸들,* *속성*및 *ValuePtr*의 값으로 설정됩니다. *버퍼 길이* 및 *문자열LengthPtr은* 무시됩니다.  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
 드라이버 관리자는 이를 **SQLSetConnectOption에**매핑합니다. **SQLSetConnectAttr에**대한 다음 호출 :  
  
```  
SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, StringLength);  
```  
  
 다음 단계 순서가 생성됩니다.  
  
1.  *특성이* 드라이버 정의 연결 또는 문 특성이 아니며 ODBC *2.x에*정의된 특성이 아닌 경우 드라이버 관리자는 SQLSTATE HY092(잘못된 특성/옵션 식별자)를 통해 SQL_ERROR 반환합니다. 이 섹션의 추가 규칙은 적용되지 않습니다.  
  
2.  *특성이* SQL_ATTR_AUTO_IPD 같으면 드라이버 관리자는 SQLSTATE HY092(잘못된 특성/옵션 식별자)를 사용하여 SQL_ERROR 반환합니다.  
  
3.  드라이버 관리자는 SQLSTATE 08003(연결이 열리지 않음) 또는 SQLSTATE HY010(함수 시퀀스 오류)을 발생시켜야 하는지 여부를 확인하기 위해 필요한 검사를 수행합니다. 이러한 오류 중 하나를 발생 해야 하는 경우 드라이버 관리자는 SQL_ERROR 반환 하 고 적절 한 오류 메시지를 게시 합니다. 이 섹션의 추가 규칙은 적용되지 않습니다.  
  
4.  드라이버 관리자는 다음과 같이 **SQLSetConnectOption을** 호출합니다.  
  
    ```  
    SQLSetConnectOption (hdbc, fOption, vParam);  
    ```  
  
     여기서 *hdbc,* *fOption*및 *vParam은* 각각 *연결 핸들,* *속성*및 *ValuePtr의*값으로 설정됩니다. *문자열LengthPtr은* 무시됩니다.  
  
> [!NOTE]  
>  연결 수준에서 문 특성을 설정하는 기능은 더 이상 사용되지 않습니다. 명령문 특성은 ODBC *3.x* 응용 프로그램에서 연결 수준에서 설정해서는 안 됩니다.  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 드라이버 관리자는 이를 **SQLSetStmtOption에**매핑합니다. **SQLSetStmtAttr에**대한 다음 호출 :  
  
```  
SQLSetStmtAttr(StatementHandle, Attribute, ValuePtr, StringLength);  
```  
  
 다음 단계 순서가 생성됩니다.  
  
1.  *특성이* 드라이버 정의 연결 또는 문 특성이 아니며 ODBC *2.x에*정의된 특성이 아닌 경우 드라이버 관리자는 SQLSTATE HY092(잘못된 특성/옵션 식별자)를 통해 SQL_ERROR 반환합니다. 이 섹션의 추가 규칙은 적용되지 않습니다.  
  
2.  *특성이* 다음 중 하나인 경우:  
  
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
  
     드라이버 관리자는 SQLSTATE HY092(잘못된 특성/옵션 식별자)를 사용 하 SQL_ERROR 반환 합니다. 이 섹션의 추가 규칙은 적용되지 않습니다.  
  
3.  드라이버 관리자는 SQLSTATE HY010(함수 시퀀스 오류)을 발생시켜야 하는지 여부를 확인하기 위해 필요한 검사를 수행합니다. 이 경우 드라이버 관리자는 SQL_ERROR 및 SQLSTATE HY010(함수 시퀀스 오류)을 반환합니다. 이 섹션의 추가 규칙은 적용되지 않습니다.  
  
4.  *특성이* SQL_ATTR_PARAMSET_SIZE 또는 SQL_ATTR_PARAMS_PROCESSED_PTR 같으면 이 항목의 후반부 "매개 변수 배열 처리를 위한 매핑" 섹션을 참조하십시오. 이 섹션의 추가 규칙은 적용되지 않습니다.  
  
5.  *특성이* SQL_ATTR_ROWS_FETCHED_PTR 같으면 드라이버 관리자는 **SQLFetchScroll**에서 나중에 사용할 수 있도록 포인터 값을 캐시합니다.  
  
6.  *특성이* SQL_ATTR_ROW_STATUS_PTR 같으면 드라이버 관리자는 **SQLFetchScroll** 또는 **SQLSetPos**에서 나중에 사용할 수 있도록 포인터 값을 캐시합니다. 이 섹션의 추가 규칙은 적용되지 않습니다.  
  
7.  *특성이* SQL_ATTR_FETCH_BOOKMARK_PTR 같으면 드라이버 관리자는 *ValuePtr을* 캐시하고 **나중에 SQLFetchScroll**에 대한 호출에서 캐시된 값을 사용합니다. 이 섹션의 추가 규칙은 적용되지 않습니다.  
  
8.  드라이버 관리자는 다음과 같이 **SQLSetStmtOption을** 호출합니다.  
  
    ```  
    SQLSetStmtOption (hstmt, fOption, vParam);  
    ```  
  
     여기서 *hstmt*, *fOption*및 *vParam은* 각각 *StatementHandle,* *특성*및 *ValuePtr*의 값으로 설정됩니다. *StringLength* 인수는 무시됩니다.  
  
     ODBC *2.x* 드라이버가 문자 문자열, 드라이버별 문 옵션을 지원하는 경우 ODBC *3.x* 응용 프로그램은 **SQLSetStmtOption을** 호출하여 이러한 옵션을 설정해야 합니다.  
  
## <a name="mappings-for-handling-parameter-arrays"></a>매개 변수 배열 처리를 위한 매핑  
 응용 프로그램이 호출할 때:  
  
```  
SQLSetStmtAttr (StatementHandle, SQL_ATTR_PARAMSET_SIZE, Size, StringLength);  
```  
  
 드라이버 관리자는 다음을 호출합니다.  
  
```  
SQLParamOptions (StatementHandle, Size, &RowCount);  
```  
  
 드라이버 관리자는 나중에 응용 프로그램이 **sqlGetStmtAttr을** 호출하여 SQL_ATTR_PARAMS_PROCESSED_PTR 검색할 때 이 변수에 대한 포인터를 반환합니다. 드라이버 관리자는 명령문 핸들이 준비되거나 할당된 상태로 반환될 때까지 이 내부 변수를 변경할 수 없습니다.  
  
 ODBC *3.x* 응용 프로그램은 APD에서 SQL_DESC_ARRAY_SIZE 필드를 명시적으로 설정하지 않은 경우에도 **SQLGetStmtAttr을** 호출하여 SQL_ATTR_PARAMS_PROCESSED_PTR 값을 얻을 수 있습니다. 예를 들어 응용 프로그램에 **SQLExecute가** SQL_NEED_DATA 반환할 때 처리중인 매개 변수의 현재 "행"을 확인하는 제네릭 루틴이 있는 경우 이러한 상황이 발생할 수 있습니다. 이 루틴은 SQL_DESC_ARRAY_SIZE 1인지 1보다 큰지 여부에 관계없이 호출됩니다. 이를 설명하기 위해 드라이버 관리자는 응용 프로그램이 APD에서 SQL_DESC_ARRAY_SIZE 필드를 설정하기 위해 **SQLSetStmtAttr을** 호출했는지 여부를 이 내부 변수를 정의해야 합니다. SQL_DESC_ARRAY_SIZE 설정되지 않은 경우 드라이버 관리자는 **SQLExecDirect** 또는 **SQLExecute**에서 반환하기 전에 이 변수에 값 1이 포함되어 있는지 확인해야 합니다.  
  
## <a name="error-handling"></a>오류 처리  
 ODBC *3.x에서* **SQLFetch** 또는 **SQLFetchScroll호출은** IRD의 SQL_DESC_ARRAY_STATUS_PTR 채우고 지정된 진단 레코드의 SQL_DIAG_ROW_NUMBER 필드에는 이 레코드와 관련된 행 집합의 행 수가 포함됩니다. 이를 사용하여 응용 프로그램은 오류 메시지와 지정된 행 위치의 상관 관계를 지정할 수 있습니다.  
  
 ODBC *2.x* 드라이버는 이 기능을 제공할 수 없습니다. 그러나 SQLSTATE 01S01 (행의 오류)을 사용 하 고 오류 경계를 제공 합니다. ODBC *2.x* 드라이버에 대해 가는 동안 **SQLFetch** 또는 **SQLFetchScroll를** 사용하는 ODBC *3.x* 응용 프로그램은 이 사실을 알고 있어야 합니다. 또한 이러한 응용 프로그램은 **SQLGetDiagField를** 호출하여 실제로 SQL_DIAG_ROW_NUMBER 필드를 얻을 수 없습니다. ODBC *2.x* 드라이버로 작업하는 ODBC *3.x* 응용 프로그램은 SQL_DIAG_MESSAGE_TEXT, SQL_DIAG_NATIVE, SQL_DIAG_RETURNCODE 또는 SQL_DIAG_SQLSTATE *대한 DiagIdentifier* 인수를 통해서만 **SQLGetDiagField를** 호출할 수 있습니다. ODBC *3.x* 드라이버 관리자는 ODBC *2.x* 드라이버로 작업할 때 진단 데이터 구조를 유지 하지만 ODBC *2.x* 드라이버는 이러한 4개 필드만 반환합니다.  
  
 ODBC *2.x* 응용 프로그램이 ODBC *2.x* 드라이버로 작업하는 경우 드라이버 관리자가 여러 오류를 반환할 수 있는 경우 ODBC *2.x* 드라이버 *2.x* 관리자가 다른 오류를 반환할 수 있습니다.  
  
## <a name="mappings-for-bookmark-operations"></a>북마크 작업에 대한 매핑  
 ODBC *3.x* 드라이버 관리자는 ODBC *2.x* 드라이버로 작업하는 ODBC *3.x* 응용 프로그램이 책갈피 작업을 수행할 때 다음과 같은 매핑을 수행합니다.  
  
### <a name="sqlbindcol"></a>SQLBindCol  
 ODBC *2.x* 드라이버로 작업하는 ODBC *3.x* 응용 프로그램이 **SQLBindCol을** 호출하여 SQL_C_VARBOOKMARK 동일한 *fCType을* 사용하여 열 0에 바인딩하면 ODBC *3.x* 드라이버 관리자는 *BufferLength* 인수가 4 보다 크거나 4보다 큰지 확인하고, 그렇다면 SQLSTATE HY090(잘못된 문자열 또는 버퍼 길이)을 반환합니다. *BufferLength* 인수가 4인 경우 드라이버 관리자는 *fCType을* SQL_C_BOOKMARK 대체한 후 드라이버에서 **SQLBindCol을** 호출합니다.  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 ODBC *2.x* 드라이버로 작업하는 ODBC *3.x* 응용 프로그램이 *ColumnNumber* 인수를 0으로 설정한 **SQLColAttribute을** 호출하면 드라이버 관리자는 다음 표에 나열된 *FieldIdentifier* 값을 반환합니다.  
  
|*FieldIdentifier*|값|  
|-----------------------|-----------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_FALSE|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|  
|SQL_DESC_CATALOG_NAME|""(빈 문자열)|  
|SQL_DESC_CONCISE_TYPE|SQL_BINARY|  
|SQL_DESC_COUNT|**SQLNumResultCols에서 반환된** 동일한 값|  
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
 ODBC *2.x* 드라이버로 작업하는 ODBC *3.x* 응용 프로그램이 *ColumnNumber* 인수를 0으로 설정한 **SQLDescribeCol을** 호출하면 드라이버 관리자는 다음 표에 나열된 값을 반환합니다.  
  
|Buffer|값|  
|------------|-----------|  
|ColumnName|""(빈 문자열)|  
|*이름길이Ptr|0|  
|*데이터 타이핑Ptr|SQL_BINARY|  
|*열크기Ptr|4|  
|*소수자릿수Ptr|0|  
|*무효 Ptr|SQL_NO_NULLS|  
  
### <a name="sqlgetdata"></a>SQLGetData  
 ODBC *2.x* 드라이버로 작업하는 ODBC *3.x* 응용 프로그램이 **SQLGetData를** 호출하여 책갈피를 검색하는 경우:  
  
```  
SQLGetData(StatementHandle, 0, SQL_C_VARBOOKMARK, TargetValuePtr, BufferLength, StrLen_or_IndPtr)  
```  
  
 호출은 다음과 같이 SQL_GET_BOOKMARK *f옵션과* 함께 **SQLGetStmtOption에** 매핑됩니다.  
  
```  
SQLGetStmtOption(hstmt, SQL_GET_BOOKMARK, TargetValuePtr)  
```  
  
 *여기서 hstmt* 와 *pvParam은* 각각 *StatementHandle* 및 *TargetValuePtr의*값으로 설정됩니다. 책갈피는 *pvParam* *(TargetValuePtr)* 인수에 의해 가리키는 버퍼에 반환됩니다. **SQLGetData에** 대 한 호출에서 *StrLen_or_IndPtr* 인수에 의해 가리키는 버퍼의 값은 4로 설정 됩니다.  
  
 이 매핑은 **SQLGetData를** 호출하기 전에 **SQLFetch가** 호출되고 ODBC *2.x* 드라이버가 **SQLExtendedFetch**를 지원하지 않는 경우를 설명하는 데 필요합니다. 이 경우 **SQLFetch는** ODBC *2.x* 드라이버로 전달되며, 이 경우 북마크 검색이 지원되지 않습니다.  
  
 **SQLGetData는** 부분적으로 책갈피를 검색하기 위해 ODBC *2.x* 드라이버에서 여러 번 호출 할 수 없으므로 *BufferLength* 인수를 4 보다 작은 값으로 설정하고 *ColumnNumber* 인수가 0으로 설정된 **SQLGetData를** 호출하면 SQLSTATE HY090 (잘못된 문자열 또는 버퍼 길이)이 반환됩니다. 그러나 **SQLGetData는** 동일한 책갈피를 검색하기 위해 여러 번 호출할 수 있습니다.  
  
### <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 ODBC *2.x* 드라이버로 작업하는 ODBC *3.x* 응용 프로그램이 **SQLSetStmtAttr을** 호출하여 SQL_ATTR_USE_BOOKMARKS 특성을 SQL_UB_VARIABLE 설정하면 드라이버 관리자는 기본 ODBC *2.x* 드라이버에서 SQL_UB_ON 특성을 설정합니다.
