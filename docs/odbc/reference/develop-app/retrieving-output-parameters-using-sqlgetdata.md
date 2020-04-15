---
title: SQLGetData를 사용하여 출력 매개 변수 검색 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetData function [ODBC], retrieving output parameters
- output parameters [ODBC]
- retrieving output parameters [ODBC]
ms.assetid: 7a8c298a-2160-491d-a300-d36f45568d9c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c96a3f9fc81d081ce16fe8e75746aafe8962fd0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294593"
---
# <a name="retrieving-output-parameters-using-sqlgetdata"></a>SQLGetData를 사용하여 출력 매개 변수 검색
ODBC 3.8 이전에는 응용 프로그램이 바인딩된 출력 버퍼를 사용하는 쿼리의 출력 매개 변수만 검색할 수 있었습니다. 그러나 매개 변수 값의 크기가 매우 큰 경우(예: 큰 이미지) 매우 큰 버퍼를 할당하기가 어렵습니다. ODBC 3.8은 부품에서 출력 매개 변수를 검색하는 새로운 방법을 소개합니다. 이제 응용 프로그램은 작은 버퍼를 여러 번 사용하여 **큰** 매개 변수 값을 검색할 수 있습니다. 이는 큰 열 데이터를 검색하는 것과 유사합니다.  
  
 출력 매개 변수 또는 입력/출력 매개 변수를 파트에서 검색하려면 **sqlBindParameter를** 호출하고 *inputOutputType* 인수는 SQL_PARAM_OUTPUT_STREAM 또는 SQL_PARAM_INPUT_OUTPUT_STREAM 설정합니다. SQL_PARAM_INPUT_OUTPUT_STREAM 응용 프로그램은 **SQLPutData를** 사용하여 매개 변수에 데이터를 입력한 다음 **SQLGetData를** 사용하여 출력 매개 변수를 검색할 수 있습니다. 입력 데이터는 SQLPutData를 사용하여 대()에서 실행 시 데이터(DAE) 양식에 있어야 하며, 이는 **sqlPutData를** preallocated 버퍼에 바인딩하는 대신에 사용해야 합니다.  
  
 이 기능은 ODBC 3.8 응용 프로그램 또는 다시 컴파일된 ODBC 3.x 및 ODBC 2.x 응용 프로그램에서 사용할 수 있으며 이러한 응용 프로그램에는 **SQLGetData** 및 ODBC 3.8 드라이버 관리자를 사용하여 출력 매개 변수 검색을 지원하는 ODBC 3.8 드라이버가 있어야 합니다. 이전 응용 프로그램에서 새 ODBC 기능을 사용하도록 설정하는 방법에 대한 자세한 내용은 [호환성 매트릭스](../../../odbc/reference/develop-app/compatibility-matrix.md)를 참조하십시오.  
  
## <a name="usage-example"></a>사용 예  
 예를 들어 두 매개 변수가 모두 SQL_PARAM_OUTPUT_STREAM 바인딩되고 저장 프로시저가 결과 집합을 반환하지 않는 **{CALL sp_f(?,?)}의**저장 프로시저를 실행하는 것이 좋습니다(이 항목의 후반부에서는 더 복잡한 시나리오를 찾을 수 있음).  
  
1.  각 매개 변수에 대해 *inputOutputTypeset이* SQL_PARAM_OUTPUT_STREAM 설정된 **SQLBindParameter를** 호출하고 *ParameterValuePtr은* 매개 변수 번호, 데이터에 대한 포인터 또는 응용 프로그램에서 입력 매개 변수를 바인딩하는 데 사용하는 구조에 대한 포인터와 같은 토큰으로 설정합니다. 이 예제에서는 매개 변수 를 토큰으로 사용합니다.  
  
2.  **SQLExecDirect** 또는 **SQLExecute를**통해 쿼리를 실행합니다. SQL_PARAM_DATA_AVAILABLE 반환됩니다.  
  
3.  **SQLParamData를** 호출하여 검색에 사용할 수 있는 매개 변수를 가져옵니다. **SQLParamData** 는 SQLBindParameter(1단계)에 설정된 첫 **SQLBindParameter** 번째 사용 가능한 매개 변수의 토큰을 사용하여 SQL_PARAM_DATA_AVAILABLE 반환합니다. *ValuePtrPtr이* 가리키는 버퍼에서 토큰이 반환됩니다.  
  
4.  *Col*\_*Param_Num* _or 인인수로 **SQLGetData를** 호출하여 매개 변수 서수로 설정하여 사용 가능한 첫 번째 매개 변수의 데이터를 검색합니다. **SQLGetData** SQL_SUCCESS_WITH_INFO 및 SQLState 01004 (데이터 잘린)를 반환 하 고 형식은 클라이언트와 서버 모두에서 가변 길이, 첫 번째 사용 가능한 매개 변수에서 검색 할 더 많은 데이터가 있다. 다른 **SQLState를**사용하여 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO 반환할 때까지 **SQLGetData를** 계속 호출할 수 있습니다.  
  
5.  3단계와 4단계를 반복하여 현재 매개 변수를 검색합니다.  
  
6.  **SQLParamData를** 다시 호출합니다. SQL_PARAM_DATA_AVAILABLE 제외한 모든 것을 반환하면 검색할 스트리밍된 매개 변수 데이터가 더 이상 없으며 반환 코드는 실행되는 다음 문의 반환 코드가 됩니다.  
  
7.  **SQLMoreResults를** 호출하여 SQL_NO_DATA 반환될 때까지 다음 매개 변수 집합을 처리합니다. **SQLMoreResults** SQL_ATTR_PARAMSET_SIZE 명령문 특성이 1로 설정된 경우 이 예제에서 SQL_NO_DATA 반환합니다. 그렇지 않으면 **SQLMoreResults는** SQL_PARAM_DATA_AVAILABLE 반환하여 다음 매개 변수 집합에서 검색할 수 있는 스트리밍된 출력 매개 변수가 있음을 나타냅니다.  
  
 DAE 입력 매개 변수와 마찬가지로 **SQLBindParameter(1단계)의** *ParameterValuePtr* 인수에 사용되는 토큰은 필요한 경우 매개 변수의 서수와 더 많은 응용 프로그램 별 정보를 포함하는 응용 프로그램 데이터 구조를 가리키는 포인터일 수 있습니다.  
  
 반환된 스트리밍 된 출력 또는 입력/출력 매개 변수의 순서는 드라이버에 따라 다르며 항상 쿼리에 지정된 순서와 같지 않을 수 있습니다.  
  
 응용 프로그램이 4단계에서 **SQLGetData를** 호출하지 않으면 매개 변수 값이 삭제됩니다. 마찬가지로 응용 프로그램에서 **SQLParamData를** 호출하는 경우 모든 매개 변수 값을 **SQLGetData에서**읽기 전에 나머지 값은 삭제되고 응용 프로그램은 다음 매개 변수를 처리할 수 있습니다.  
  
 응용 프로그램에서 모든 스트리밍된 출력 매개 변수가 처리되기 전에 **SQLMoreResults를** 호출하면 나머지 모든 매개 변수가 모두 삭제됩니다(**SQLParamData는** 여전히 SQL_PARAM_DATA_AVAILABLE 반환합니다). 마찬가지로 응용 프로그램에서 **SQLMoreResults를** 호출하는 경우 모든 매개 변수 값을 **SQLGetData에서**읽기 전에 나머지 값과 나머지 매개 변수는 삭제되고 응용 프로그램은 다음 매개 변수 집합을 계속 처리할 수 있습니다.  
  
 응용 프로그램은 **SQLBindParameter** 및 **SQLGetData**에서 C 데이터 형식을 지정할 수 있습니다. **SQLGetData로** 지정된 C 데이터 형식은 **SQLGetData에** 지정된 C 데이터 형식이 SQL_APD_TYPE 않는 한 **SQLBindParameter에**지정된 C 데이터 형식을 재정의합니다.  
  
 스트리밍된 출력 매개 변수는 출력 매개 변수의 데이터 형식이 BLOB 형식인 경우 더 유용하지만 이 기능은 모든 데이터 형식에서도 사용할 수 있습니다. 스트리밍된 출력 매개 변수에서 지원하는 데이터 형식은 드라이버에 지정됩니다.  
  
 처리할 SQL_PARAM_INPUT_OUTPUT_STREAM 매개 변수가 있는 경우 **SQLExecute** 또는 **SQLExecDirect가** 먼저 SQL_NEED_DATA 반환합니다. 응용 프로그램은 **SQLParamData** 및 **SQLPutData를** 호출하여 DAE 매개 변수 데이터를 보낼 수 있습니다. 모든 DAE 입력 매개 변수가 처리되면 **SQLParamData는** 스트리밍된 출력 매개 변수를 사용할 수 있음을 나타내기 위해 SQL_PARAM_DATA_AVAILABLE 반환합니다.  
  
 스트리밍된 출력 매개 변수와 바인딩된 출력 매개 변수가 처리되는 경우 드라이버는 출력 매개 변수를 처리하는 순서를 결정합니다. 따라서 출력 매개 변수가 버퍼에 바인딩된 **경우(SQLBindParameter** 매개 변수 *InputOutputType이* SQL_PARAM_INPUT_OUTPUT 또는 SQL_PARAM_OUTPUT 설정됨) **SQLParamData가** SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO 반환할 때까지 버퍼가 채워지지 않을 수 있습니다. 응용 프로그램은 **SQLParamData가** SQL_SUCCESS 반환하거나 모든 스트리밍된 출력 매개 변수가 처리된 후 SQL_SUCCESS_WITH_INFO 후에만 바인딩된 버퍼를 읽어야 합니다.  
  
 데이터 원본은 스트리밍된 출력 매개 변수 외에 경고 및 결과 집합을 반환할 수 있습니다. 일반적으로 경고 및 결과 집합은 **SQLMoreResults**를 호출하여 스트리밍된 출력 매개 변수와 별도로 처리됩니다. 스트리밍된 출력 매개 변수를 처리하기 전에 경고 및 결과 집합을 처리합니다.  
  
 다음 표에서는 서버로 전송되는 단일 명령의 다양한 시나리오와 응용 프로그램의 작동 방식에 대해 설명합니다.  
  
|시나리오|SQLExecute 또는 SQLExecDirect에서 반환 값|다음에 수행할 작업|  
|--------------|---------------------------------------------------|---------------------|  
|데이터에는 스트리밍된 출력 매개변수만 포함됩니다.|SQL_PARAM_DATA_AVAILABLE|**SQLParamData** 및 **SQLGetData를** 사용하여 스트리밍된 출력 매개 변수를 검색합니다.|  
|데이터에 결과 집합 및 스트리밍된 출력 매개 변수가 포함됩니다.|SQL_SUCCESS|**SQLBindCol** 및 **SQLGetData를**사용하여 결과 집합을 검색합니다.<br /><br /> 스트리밍된 출력 매개 변수 처리를 시작하려면 **SQLMoreResults를** 호출합니다. SQL_PARAM_DATA_AVAILABLE 반환해야 합니다.<br /><br /> **SQLParamData** 및 **SQLGetData를** 사용하여 스트리밍된 출력 매개 변수를 검색합니다.|  
|데이터에 경고 메시지 및 스트리밍된 출력 매개 변수가 포함됩니다.|SQL_SUCCESS_WITH_INFO|**SQLGetDiagRec** 및 **SQLGetDiagField를** 사용하여 경고 메시지를 처리합니다.<br /><br /> 스트리밍된 출력 매개 변수 처리를 시작하려면 **SQLMoreResults를** 호출합니다. SQL_PARAM_DATA_AVAILABLE 반환해야 합니다.<br /><br /> **SQLParamData** 및 **SQLGetData를** 사용하여 스트리밍된 출력 매개 변수를 검색합니다.|  
|데이터에 경고 메시지, 결과 집합 및 스트리밍된 출력 매개 변수가 포함됩니다.|SQL_SUCCESS_WITH_INFO|**SQLGetDiagRec** 및 **SQLGetDiagField를** 사용하여 경고 메시지를 처리합니다. 그런 다음 **SQLMoreResults를** 호출하여 결과 집합 처리를 시작합니다.<br /><br /> **SQLBindCol** 및 **SQLGetData를**사용하여 결과 집합을 검색합니다.<br /><br /> 스트리밍된 출력 매개 변수 처리를 시작하려면 **SQLMoreResults를** 호출합니다. **SQLMoreResults는** SQL_PARAM_DATA_AVAILABLE 반환해야 합니다.<br /><br /> **SQLParamData** 및 **SQLGetData를** 사용하여 스트리밍된 출력 매개 변수를 검색합니다.|  
|DAE 입력 매개 변수(예: 스트리밍된 입력/출력)를 사용 하 고 쿼리|SQL NEED_DATA|**SQLParamData** 및 **SQLPutData를** 호출하여 DAE 입력 매개 변수 데이터를 보냅니다.<br /><br /> 모든 DAE 입력 매개 변수가 처리된 후 **SQLParamData는** **SQLExecute** 및 **SQLExecDirect가** 반환할 수 있는 반환 코드를 반환할 수 있습니다. 그런 다음 이 테이블의 사례를 적용할 수 있습니다.<br /><br /> 반환 코드가 SQL_PARAM_DATA_AVAILABLE 경우 스트리밍된 출력 매개 변수를 사용할 수 있습니다. 응용 프로그램은 이 테이블의 첫 번째 행에 설명된 대로 스트리밍된 출력 매개 변수에 대한 토큰을 검색하기 위해 **SQLParamData를** 다시 호출해야 합니다.<br /><br /> 반환 코드가 SQL_SUCCESS 경우 처리하도록 설정된 결과가 있거나 처리가 완료된 것입니다.<br /><br /> 반환 코드가 SQL_SUCCESS_WITH_INFO 경우 처리할 경고 메시지가 있습니다.|  
  
 **SQLExecute**후 , **SQLExecDirect**또는 **SQLMoreResults** SQL_PARAM_DATA_AVAILABLE 반환하면 응용 프로그램이 다음 목록에 없는 함수를 호출하는 경우 함수 시퀀스 오류가 발생합니다.  
  
-   **SQLAlloc핸들** / **SQLAlloc핸들스트드**  
  
-   **SQLDataSource** / **SQL드라이버**  
  
-   **SQLGetInfo** / **SQLGetFunctions**  
  
-   **SQLGetConnectAttr** / **SQLGetEnvAttr** / **SQLGetDescField** / **SQLGetDescRec**  
  
-   **SQLNumParams**  
  
-   **SQLDescribeParam**  
  
-   **SQLNativeSql**  
  
-   **SQLParamData**  
  
-   **SQLMoreResults**  
  
-   **SQLGetDiag필드** / **SQLGetDiagRec**  
  
-   **SQLCancel**  
  
-   **SQLCancelHandle(문** 핸들 있음)  
  
-   **SQLFreeStmt** (옵션 = SQL_CLOSE, SQL_DROP 또는 SQL_UNBIND)  
  
-   **SQLCloseCursor**  
  
-   **SQL분리**  
  
-   **SQLFreeHandle(핸들** 유형 = SQL_HANDLE_STMT)  
  
-   **SQLGetStmtAttr**  
  
 응용 프로그램은 여전히 **SQLSetDescField** 또는 **SQLSetDescRec를** 사용하여 바인딩 정보를 설정할 수 있습니다. 필드 매핑은 변경되지 않습니다. 그러나 설명자 내의 필드는 새 값을 반환할 수 있습니다. 예를 들어 SQL_DESC_PARAMETER_TYPE SQL_PARAM_INPUT_OUTPUT_STREAM 또는 SQL_PARAM_OUTPUT_STREAM 반환할 수 있습니다.  
  
## <a name="usage-scenario-retrieve-an-image-in-parts-from-a-result-set"></a>사용 시나리오: 결과 집합에서 파트에서 이미지 검색  
 **SQLGetData는** 저장 프로시저가 이미지에 대한 메타데이터의 한 행을 포함하는 결과 집합을 반환하고 이미지가 큰 출력 매개 변수로 반환될 때 부분적으로 데이터를 가져오는 데 사용할 수 있습니다.  
  
```  
// CREATE PROCEDURE SP_TestOutputPara  
//      @ID_of_picture   as int,  
//      @Picture         as varbinary(max) out  
// AS  
//     output the image data through streamed output parameter  
// GO  
BOOL displayPicture(SQLUINTEGER idOfPicture, SQLHSTMT hstmt) {  
   SQLLEN      lengthOfPicture;    // The actual length of the picture.  
   BYTE        smallBuffer[100];   // A very small buffer.  
   SQLRETURN   retcode, retcode2;  
  
   // Bind the first parameter (input parameter)  
   SQLBindParameter(  
         hstmt,  
         1,                         // The first parameter.   
         SQL_PARAM_INPUT,           // Input parameter: The ID_of_picture.  
         SQL_C_ULONG,               // The C Data Type.  
         SQL_INTEGER,               // The SQL Data Type.  
         0,                         // ColumnSize is ignored for integer.  
         0,                         // DecimalDigits is ignored for integer.  
         &idOfPicture,              // The Address of the buffer for the input parameter.  
         0,                         // BufferLength is ignored for integer.  
         NULL);                     // This is ignored for integer.  
  
   // Bind the streamed output parameter.  
   SQLBindParameter(  
         hstmt,   
         2,                         // The second parameter.  
         SQL_PARAM_OUTPUT_STREAM,   // A streamed output parameter.   
         SQL_C_BINARY,              // The C Data Type.    
         SQL_VARBINARY,             // The SQL Data Type.  
         0,                         // ColumnSize: The maximum size of varbinary(max).  
         0,                         // DecimalDigits is ignored for binary type.  
         (SQLPOINTER)2,             // ParameterValuePtr: An application-defined  
                                    // token (this will be returned from SQLParamData).  
                                    // In this example, we used the ordinal   
                                    // of the parameter.  
         0,                         // BufferLength is ignored for streamed output parameters.  
         &lengthOfPicture);         // StrLen_or_IndPtr: The status variable returned.   
  
   retcode = SQLPrepare(hstmt, L"{call SP_TestOutputPara(?, ?)}", SQL_NTS);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   retcode = SQLExecute(hstmt);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   // Assume that the retrieved picture exists.  Use SQLBindCol or SQLGetData to retrieve the result-set.  
  
   // Process the result set and move to the streamed output parameters.  
   retcode = SQLMoreResults( hstmt );  
  
   // SQLGetData retrieves and displays the picture in parts.  
   // The streamed output parameter is available.  
   while (retcode == SQL_PARAM_DATA_AVAILABLE) {  
      SQLPOINTER token;   // Output by SQLParamData.  
      SQLLEN cbLeft;      // #bytes remained  
      retcode = SQLParamData(hstmt, &token);   // returned token is 2 (according to the binding)  
      if ( retcode == SQL_PARAM_DATA_AVAILABLE ) {  
         // A do-while loop retrieves the picture in parts.  
         do {  
            retcode2 = SQLGetData(   
               hstmt,   
               (UWORD) token,          // the value of the token is the ordinal.   
               SQL_C_BINARY,           // The C-type.  
               smallBuffer,            // A small buffer.   
               sizeof(smallBuffer),    // The size of the buffer.  
               &cbLeft);               // How much data we can get.  
         }  
         while ( retcode2 == SQL_SUCCESS_WITH_INFO );  
      }  
   }  
  
   return TRUE;  
}  
```  
  
## <a name="usage-scenario-send-and-receive-a-large-object-as-a-streamed-inputoutput-parameter"></a>사용 시나리오: 스트리밍된 입력/출력 매개 변수로 큰 개체 보내기 및 수신  
 **SQLGetData는** 저장 프로시저가 큰 개체를 입력/출력 매개 변수로 전달할 때 부분적으로 데이터를 얻고 전송하여 데이터베이스에서 값을 스트리밍하는 데 사용할 수 있습니다. 모든 데이터를 메모리에 저장할 필요는 없습니다.  
  
```  
// CREATE PROCEDURE SP_TestInOut  
//       @picture as varbinary(max) out  
// AS  
//    output the image data through output parameter   
// go  
  
BOOL displaySimilarPicture(BYTE* image, ULONG lengthOfImage, SQLHSTMT hstmt) {  
   BYTE smallBuffer[100];   // A very small buffer.  
   SQLRETURN retcode, retcode2;  
   SQLLEN statusOfPicture;  
  
   // First bind the parameters, before preparing the statement that binds the output streamed parameter.  
   SQLBindParameter(  
      hstmt,   
      1,                                 // The first parameter.  
      SQL_PARAM_INPUT_OUTPUT_STREAM,     // I/O-streamed parameter: The Picture.  
      SQL_C_BINARY,                      // The C Data Type.  
      SQL_VARBINARY,                     // The SQL Data Type.  
      0,                                 // ColumnSize: The maximum size of varbinary(max).  
      0,                                 // DecimalDigits is ignored.   
      (SQLPOINTER)1,                     // An application defined token.   
      0,                                 // BufferLength is ignored for streamed I/O parameters.  
      &statusOfPicture);                 // The status variable.  
  
   statusOfPicture = SQL_DATA_AT_EXEC;   // Input data in parts (DAE parameter at input).  
  
   retcode = SQLPrepare(hstmt, L"{call SP_TestInOut(?) }", SQL_NTS);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   // Execute the statement.  
   retcode = SQLExecute(hstmt);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   if ( retcode == SQL_NEED_DATA ) {  
      // Use SQLParamData to loop through DAE input parameters.  For  
      // each, use SQLPutData to send the data to database in parts.  
  
      // This example uses an I/O parameter with streamed output.  
      // Therefore, the last call to SQLParamData should return  
      // SQL_PARAM_DATA_AVAILABLE to indicate the end of the input phrase   
      // and report that a streamed output parameter is available.  
  
      // Assume retcode is set to the return value of the last call to  
      // SQLParamData, which is equal to SQL_PARAM_DATA_AVAILABLE.  
   }  
  
   // Start processing the streamed output parameters.  
   while ( retcode == SQL_PARAM_DATA_AVAILABLE ) {  
      SQLPOINTER token;   // Output by SQLParamData.  
      SQLLEN cbLeft;     // #bytes remained  
      retcode = SQLParamData(hstmt, &token);  
      if ( retcode == SQL_PARAM_DATA_AVAILABLE ) {  
         do {  
            retcode2 = SQLGetData(   
               hstmt,   
               (UWORD) token,          // the value of the token is the ordinal.   
               SQL_C_BINARY,           // The C-type.  
               smallBuffer,            // A small buffer.   
               sizeof(smallBuffer),    // The size of the buffer.  
               &cbLeft);               // How much data we can get.  
         }  
         while ( retcode2 == SQL_SUCCESS_WITH_INFO );  
      }  
   }   
  
   return TRUE;  
}  
```  
  
## <a name="see-also"></a>참고 항목  
 [명령문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)
