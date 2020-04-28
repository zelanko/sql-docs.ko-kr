---
title: SQLGetData를 사용 하 여 출력 매개 변수 검색 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81294593"
---
# <a name="retrieving-output-parameters-using-sqlgetdata"></a>SQLGetData를 사용하여 출력 매개 변수 검색
ODBC 3.8 이전에는 응용 프로그램이 바인딩된 출력 버퍼를 사용 하는 쿼리의 출력 매개 변수만 검색할 수 있었습니다. 그러나 매개 변수 값의 크기가 매우 큰 경우 (예: 큰 이미지) 매우 큰 버퍼를 할당 하는 것은 어렵습니다. ODBC 3.8에는 파트에서 출력 매개 변수를 검색 하는 새로운 방법이 도입 되었습니다. 이제 응용 프로그램은 작은 버퍼로 **SQLGetData** 를 여러 번 호출 하 여 많은 매개 변수 값을 검색할 수 있습니다. 이는 많은 열 데이터를 검색 하는 것과 유사 합니다.  
  
 부분에서 검색할 출력 매개 변수 또는 입/출력 매개 변수를 바인딩하려면 *Inputoutputtype* 인수를 SQL_PARAM_OUTPUT_STREAM 또는 SQL_PARAM_INPUT_OUTPUT_STREAM로 설정 하 여 **SQLBindParameter** 를 호출 합니다. SQL_PARAM_INPUT_OUTPUT_STREAM를 사용 하면 응용 프로그램에서 **Sqlputdata** 를 사용 하 여 데이터를 매개 변수에 입력 한 다음 **SQLGetData** 를 사용 하 여 OUTPUT 매개 변수를 검색할 수 있습니다. 입력 데이터는 미리 할당 된 버퍼에 바인딩하는 대신 **Sqlputdata** 를 사용 하 여 실행 시 데이터 (DAE) 형식 이어야 합니다.  
  
 이 기능은 ODBC 3.8 응용 프로그램에서 사용 하거나 ODBC 2.x 및 ODBC 2.x 응용 프로그램을 다시 컴파일할 수 있으며, 이러한 응용 프로그램에는 **SQLGetData** 및 Odbc 3.8 드라이버 관리자를 사용 하 여 출력 매개 변수 검색을 지 원하는 odbc 3.8 드라이버가 있어야 합니다. 이전 응용 프로그램에서 새로운 ODBC 기능을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 [호환성 매트릭스](../../../odbc/reference/develop-app/compatibility-matrix.md)를 참조 하세요.  
  
## <a name="usage-example"></a>사용 예  
 예를 들어 저장 프로시저 **{CALL sp_f (?,?)}** 를 실행 하는 것이 좋습니다 .이 경우 두 매개 변수가 모두 SQL_PARAM_OUTPUT_STREAM로 바인딩되고 저장 프로시저는 결과 집합을 반환 하지 않습니다 .이 항목의 뒷부분에서는 더 복잡 한 시나리오를 찾을 것입니다.  
  
1.  각 매개 변수에 대해 *Inputoutputtype* 을 SQL_PARAM_OUTPUT_STREAM로 설정 *하 고 매개* 변수 번호, 데이터에 대 한 포인터 또는 응용 프로그램에서 입력 매개 변수를 바인딩하는 데 사용 하는 구조체에 대 한 포인터로 설정 된 **SQLBindParameter** 를 호출 합니다. 이 예제에서는 매개 변수 서 수를 토큰으로 사용 합니다.  
  
2.  **Sqlexecdirect** 또는 **sqlexecute**를 사용 하 여 쿼리를 실행 합니다. 검색에 사용할 수 있는 스트리밍 출력 매개 변수가 있음을 나타내는 SQL_PARAM_DATA_AVAILABLE 반환 됩니다.  
  
3.  **Sqlparamdata** 를 호출 하 여 검색에 사용할 수 있는 매개 변수를 가져옵니다. **Sqlparamdata** 는 **SQLBindParameter** 에서 설정 된 사용 가능한 첫 번째 매개 변수의 토큰과 함께 SQL_PARAM_DATA_AVAILABLE를 반환 합니다 (1 단계). 토큰 *은 고 지 수가 가리키는 버퍼* 에서 반환 됩니다.  
  
4.  _Or\_인수 *Col*으로 **SQLGetData** 를 호출 하 여 사용 가능한 첫 번째 매개 변수의 데이터를 검색 하는 매개 변수 서 수로 설정*Param_Num* 합니다. **SQLGetData** 가 SQL_SUCCESS_WITH_INFO 및 SQLState 01004 (데이터 잘림)을 반환 하 고 형식이 클라이언트와 서버 모두에서 가변 길이인 경우 사용 가능한 첫 번째 매개 변수에서 검색할 데이터가 더 있습니다. 다른 **SQLState**를 사용 하 여 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 반환할 때까지 **SQLGetData** 를 계속 호출할 수 있습니다.  
  
5.  3 단계와 4 단계를 반복 하 여 현재 매개 변수를 검색 합니다.  
  
6.  **Sqlparamdata** 를 다시 호출 합니다. SQL_PARAM_DATA_AVAILABLE를 제외한 모든 항목을 반환 하는 경우 더 이상 스트리밍된 매개 변수 데이터가 검색 되지 않으며 반환 코드는 실행 되는 다음 문의 반환 코드가 됩니다.  
  
7.  **SQLMoreResults** 를 호출 하 여 SQL_NO_DATA 반환 될 때까지 다음 매개 변수 집합을 처리 합니다. **SQLMoreResults** 는 문 특성 SQL_ATTR_PARAMSET_SIZE 1로 설정 된 경우이 예의 SQL_NO_DATA을 반환 합니다. 그렇지 않으면 **SQLMoreResults** 는 검색할 다음 매개 변수 집합에 사용할 수 있는 스트리밍 출력 매개 변수가 있음을 나타내는 SQL_PARAM_DATA_AVAILABLE를 반환 합니다.  
  
 DAE 입력 매개 변수와 마찬가지로 **SQLBindParameter** 의 *Parametervalueptr* 인수에 사용 되는 토큰 (1 단계)은 매개 변수의 서 수를 포함 하는 응용 프로그램 데이터 구조를 가리키는 포인터 일 수 있으며 필요한 경우 응용 프로그램 관련 정보를 추가로 나타낼 수 있습니다.  
  
 반환 된 스트리밍된 출력 또는 입/출력 매개 변수의 순서는 드라이버에 따라 달라 지 며 쿼리에 지정 된 순서와 다를 수 있습니다.  
  
 응용 프로그램에서 4 단계에서 **SQLGetData** 를 호출 하지 않는 경우 매개 변수 값이 삭제 됩니다. 마찬가지로 모든 매개 변수 값이 **SQLGetData**에서 읽기 전에 응용 프로그램에서 **sqlparamdata** 를 호출 하는 경우 나머지 값은 무시 되 고 응용 프로그램은 다음 매개 변수를 처리할 수 있습니다.  
  
 모든 스트리밍된 출력 매개 변수가 처리 되기 전에 응용 프로그램이 **SQLMoreResults** 를 호출 하는 경우 (**sqlparamdata** 는 계속 SQL_PARAM_DATA_AVAILABLE 반환) 나머지 모든 매개 변수는 무시 됩니다. 마찬가지로 모든 매개 변수 값이 **SQLGetData**에서 읽기 전에 응용 프로그램이 **SQLMoreResults** 를 호출 하는 경우 값의 나머지 및 나머지 매개 변수는 모두 무시 되 고 응용 프로그램은 다음 매개 변수 집합을 계속 처리할 수 있습니다.  
  
 응용 프로그램은 **SQLBindParameter** 및 **SQLGetData**모두에서 C 데이터 형식을 지정할 수 있습니다. **Sqlgetdata에서 지정** 된 c 데이터 형식이 SQL_APD_TYPE 않는 경우 **sqlgetdata** 로 지정 된 c 데이터 형식은 **SQLBindParameter**에 지정 된 c 데이터 형식을 재정의 합니다.  
  
 출력 매개 변수의 데이터 형식이 BLOB 형식일 때 스트리밍된 출력 매개 변수는 더 유용 하지만 모든 데이터 형식에도이 기능을 사용할 수 있습니다. 스트리밍된 출력 매개 변수에서 지원 되는 데이터 형식은 드라이버에서 지정 됩니다.  
  
 처리할 SQL_PARAM_INPUT_OUTPUT_STREAM 매개 변수가 있는 경우 **Sqlexecute** 또는 **sqlexecdirect** 는 SQL_NEED_DATA를 먼저 반환 합니다. 응용 프로그램은 **Sqlparamdata** 및 **sqlparamdata** 를 호출 하 여 DAE 매개 변수 데이터를 보낼 수 있습니다. 모든 DAE 입력 매개 변수를 처리 하는 경우 **Sqlparamdata** 는 스트리밍된 출력 매개 변수를 사용할 수 있음을 나타내는 SQL_PARAM_DATA_AVAILABLE 반환 합니다.  
  
 스트리밍된 출력 매개 변수와 바인딩된 출력 매개 변수가 처리 될 경우 드라이버는 출력 매개 변수를 처리 하는 순서를 결정 합니다. 따라서 출력 매개 변수가 버퍼에 바인딩되어 있는 경우 ( **SQLBindParameter** 매개 변수 *inputoutputtype* 이 SQL_PARAM_INPUT_OUTPUT 또는 SQL_PARAM_OUTPUT로 설정 됨) **sqlparamdata** 가 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 반환할 때까지 버퍼를 채우지 못할 수 있습니다. 응용 프로그램은 **Sqlparamdata** 가 SQL_SUCCESS 또는 모든 스트리밍된 출력 매개 변수가 처리 된 후의 SQL_SUCCESS_WITH_INFO를 반환한 후에만 바인딩된 버퍼를 읽어야 합니다.  
  
 데이터 원본은 스트리밍 출력 매개 변수 외에도 경고 및 결과 집합을 반환할 수 있습니다. 일반적으로 경고 및 결과 집합은 **SQLMoreResults**를 호출 하 여 스트리밍된 출력 매개 변수와 별도로 처리 됩니다. 스트리밍된 출력 매개 변수를 처리 하기 전에 경고와 결과 집합을 처리 합니다.  
  
 다음 표에서는 서버로 전송 되는 단일 명령의 여러 시나리오와 응용 프로그램의 작동 방식에 대해 설명 합니다.  
  
|시나리오|SQLExecute 또는 SQLExecDirect의 반환 값|다음에 수행할 작업|  
|--------------|---------------------------------------------------|---------------------|  
|데이터에는 스트리밍된 출력 매개 변수만 포함 됩니다.|SQL_PARAM_DATA_AVAILABLE|**Sqlparamdata** 및 **SQLGetData** 를 사용 하 여 스트리밍된 출력 매개 변수를 검색 합니다.|  
|데이터에는 결과 집합 및 스트리밍된 출력 매개 변수가 포함 됩니다.|SQL_SUCCESS|**SQLBindCol** 및 **SQLGetData**를 사용 하 여 결과 집합을 검색 합니다.<br /><br /> **SQLMoreResults** 를 호출 하 여 스트리밍된 출력 매개 변수 처리를 시작 합니다. SQL_PARAM_DATA_AVAILABLE를 반환 해야 합니다.<br /><br /> **Sqlparamdata** 및 **SQLGetData** 를 사용 하 여 스트리밍된 출력 매개 변수를 검색 합니다.|  
|데이터에는 경고 메시지와 스트리밍된 출력 매개 변수가 포함 됩니다.|SQL_SUCCESS_WITH_INFO|**SQLGetDiagRec** 및 **SQLGetDiagField** 를 사용 하 여 경고 메시지를 처리 합니다.<br /><br /> **SQLMoreResults** 를 호출 하 여 스트리밍된 출력 매개 변수 처리를 시작 합니다. SQL_PARAM_DATA_AVAILABLE를 반환 해야 합니다.<br /><br /> **Sqlparamdata** 및 **SQLGetData** 를 사용 하 여 스트리밍된 출력 매개 변수를 검색 합니다.|  
|데이터에는 경고 메시지, 결과 집합 및 스트리밍된 출력 매개 변수가 포함 됩니다.|SQL_SUCCESS_WITH_INFO|**SQLGetDiagRec** 및 **SQLGetDiagField** 를 사용 하 여 경고 메시지를 처리 합니다. 그런 다음 **SQLMoreResults** 를 호출 하 여 결과 집합 처리를 시작 합니다.<br /><br /> **SQLBindCol** 및 **SQLGetData**를 사용 하 여 결과 집합을 검색 합니다.<br /><br /> **SQLMoreResults** 를 호출 하 여 스트리밍된 출력 매개 변수 처리를 시작 합니다. **SQLMoreResults** 는 SQL_PARAM_DATA_AVAILABLE을 반환 해야 합니다.<br /><br /> **Sqlparamdata** 및 **SQLGetData** 를 사용 하 여 스트리밍된 출력 매개 변수를 검색 합니다.|  
|DAE 입력 매개 변수를 사용 하는 쿼리 (예: 스트리밍된 입력/출력 (DAE) 매개 변수)|SQL NEED_DATA|**Sqlparamdata** 및 **sqlparamdata** 를 호출 하 여 DAE 입력 매개 변수 데이터를 보냅니다.<br /><br /> 모든 DAE 입력 매개 변수를 처리 한 후 **Sqlparamdata** 는 **Sqlexecute** 및 **sqlparamdata** 에서 반환할 수 있는 모든 반환 코드를 반환할 수 있습니다. 그런 다음이 테이블의 사례를 적용할 수 있습니다.<br /><br /> 반환 코드가 SQL_PARAM_DATA_AVAILABLE 이면 스트리밍된 출력 매개 변수를 사용할 수 있습니다. 응용 프로그램은이 표의 첫 번째 행에 설명 된 대로 **Sqlparamdata** 를 다시 호출 하 여 스트리밍된 출력 매개 변수에 대 한 토큰을 검색 해야 합니다.<br /><br /> 반환 코드가 SQL_SUCCESS 이면 처리할 결과 집합이 있거나 처리가 완료 된 것입니다.<br /><br /> 반환 코드가 SQL_SUCCESS_WITH_INFO 경우 처리할 경고 메시지가 있습니다.|  
  
 **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 SQL_PARAM_DATA_AVAILABLE를 반환한 후 응용 프로그램이 다음 목록에 없는 함수를 호출 하면 함수 시퀀스 오류가 발생 합니다.  
  
-   **SQLAllocHandle** / **SQLAllocHandleStd**  
  
-   **Sqldatasources 원본** / **sqldatasources**  
  
-   **SQLGetInfo** / **SQLGetFunctions**  
  
-   **SQLGetConnectAttr** / **SQLGetEnvAttr**SQLGetEnvAttr / **SQLGetDescField**SQLGetDescField / **SQLGetDescRec**  
  
-   **SQLNumParams**  
  
-   **SQLDescribeParam**  
  
-   **SQLNativeSql**  
  
-   **SQLParamData**  
  
-   **SQLMoreResults**  
  
-   **SQLGetDiagField** / **SQLGetDiagRec**  
  
-   **SQLCancel**  
  
-   **Sqlcancelhandle** (문 핸들 포함)  
  
-   **SQLFreeStmt** (Option = SQL_CLOSE, SQL_DROP 또는 SQL_UNBIND)  
  
-   **SQLCloseCursor**  
  
-   **SQLDisconnect**  
  
-   **Sqlfreehandle** (HandleType = SQL_HANDLE_STMT)  
  
-   **SQLGetStmtAttr**  
  
 응용 프로그램은 여전히 **SQLSetDescField** 또는 **SQLSetDescRec** 를 사용 하 여 바인딩 정보를 설정할 수 있습니다. 필드 매핑이 변경 되지 않습니다. 그러나 설명자 내의 필드는 새 값을 반환할 수 있습니다. 예를 들어 SQL_DESC_PARAMETER_TYPE SQL_PARAM_INPUT_OUTPUT_STREAM 또는 SQL_PARAM_OUTPUT_STREAM를 반환할 수 있습니다.  
  
## <a name="usage-scenario-retrieve-an-image-in-parts-from-a-result-set"></a>사용 시나리오: 결과 집합에서 파트의 이미지를 검색 합니다.  
 **SQLGetData** 를 사용 하 여 저장 프로시저가 이미지에 대 한 메타 데이터의 한 행을 포함 하는 결과 집합을 반환 하 고 이미지가 긴 출력 매개 변수로 반환 될 때 데이터를 가져올 수 있습니다.  
  
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
  
## <a name="usage-scenario-send-and-receive-a-large-object-as-a-streamed-inputoutput-parameter"></a>사용 시나리오: 스트리밍된 입/출력 매개 변수로 Large 개체를 보내고 받습니다.  
 저장 프로시저에서 대량 개체를 입력/출력 매개 변수로 전달 하 고 데이터베이스에서 값을 스트리밍하는 경우 **SQLGetData** 를 사용 하 여 데이터를 가져와 데이터를 전송할 수 있습니다. 모든 데이터를 메모리에 저장할 필요는 없습니다.  
  
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
