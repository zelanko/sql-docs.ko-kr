---
title: SQLGetData를 사용 하 여 출력 매개 변수 검색 | Microsoft Docs
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
- SQLGetData function [ODBC], retrieving output parameters
- output parameters [ODBC]
- retrieving output parameters [ODBC]
ms.assetid: 7a8c298a-2160-491d-a300-d36f45568d9c
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 92903e38c31af40c7d2cf375cad6695a23acb010
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="retrieving-output-parameters-using-sqlgetdata"></a>SQLGetData를 사용 하 여 출력 매개 변수 검색
ODBC 3.8 하기 전에 응용 프로그램만 바인딩된 출력 버퍼를 사용 하 여 쿼리를 출력 매개 변수를 검색할 수 있습니다. 그러나 매개 변수 값의 크기가 매우 크게 (예: 큰 이미지) 매우 큰 버퍼를 할당 하는 어렵습니다. ODBC 3.8 부분에서 출력 매개 변수를 검색 하는 새로운 방법이 도입 되었습니다. 응용 프로그램이 호출할 수 **SQLGetData** 작은 버퍼로 여러 번 큰 매개 변수 값을 검색 합니다. 큰 열 데이터를 검색 하는 것과 비슷합니다.  
  
 출력 매개 변수 또는 부분에서 검색할 입/출력 매개 변수를 바인딩하려면 호출 **SQLBindParameter** 와 *InputOutputType* SQL_PARAM_OUTPUT_STREAM 또는 SQL_PARAM_INPUT_OUTPUT 인수 설정 _STREAM 합니다. SQL_PARAM_INPUT_OUTPUT_STREAM, 응용 프로그램이 사용할 수 **SQLPutData** 를 매개 변수로 데이터 입력을 사용 하 여 **SQLGetData** 를 출력 매개 변수를 검색 합니다. 입력된 데이터는 데이터 실행 시 (디지털 오디오)에 있어야 합니다. 사용 하 여 만들 **SQLPutData** 미리 할당 된 버퍼에 바인딩하는 대신 합니다.  
  
 이 기능은 ODBC 3.8 응용 프로그램에서 사용할 수 있습니다 또는 ODBC를 다시 컴파일될 3.x 및 ODBC 2.x 응용 프로그램 및 이러한 응용 프로그램에 검색 하는 동안 출력 매개 변수를 사용 하 여 지원 되는 ODBC 3.8 드라이버가 있어야 **SQLGetData** 및 ODBC 3.8 드라이버 관리자입니다. ODBC의 새로운 기능을 사용 하도록 이전 응용 프로그램을 사용 하도록 설정 하는 방법에 대 한 정보를 참조 하십시오. [호환성 매트릭스](../../../odbc/reference/develop-app/compatibility-matrix.md)합니다.  
  
## <a name="usage-example"></a>사용 예  
 예를 들어 저장된 프로시저를 실행 하는 것이 좋습니다 **{호출 sp_f(?,?)}** , 여기서 SQL_PARAM_OUTPUT_STREAM, 두 매개 변수에 바인딩된 및 없는 결과 집합을 반환 하는 저장된 프로시저 (이 항목의 뒷부분에 있습니다. 더 복잡 한 시나리오):  
  
1.  각 매개 변수에 대 한 호출 **SQLBindParameter** 와 *InputOutputType* SQL_PARAM_OUTPUT_STREAM로 설정 하 고 *ParameterValuePtr* 매개 변수 번호를 비롯 한 토큰으로 설정 데이터에 대 한 포인터 또는 입력된 매개 변수를 바인딩할 응용 프로그램을 사용 하는 구조에 대 한 포인터입니다. 이 예제에서는 토큰으로 서 수 매개 변수를 사용 합니다.  
  
2.  쿼리를 실행할 **SQLExecDirect** 또는 **SQLExecute**합니다. SQL_PARAM_DATA_AVAILABLE 반환 됩니다 없다는 스트리밍된 출력 매개 변수 검색에 사용할 수 있습니다.  
  
3.  호출 **SQLParamData** 검색에 사용할 수 있는 매개 변수를 얻으려고 합니다. **SQLParamData** 에 설정 된 첫 번째 사용 가능한 매개 변수의 토큰 SQL_PARAM_DATA_AVAILABLE 반환 **SQLBindParameter** (1 단계). 버퍼에 반환 된 토큰은 하는 *ValuePtrPtr* 를 가리킵니다.  
  
4.  호출 **SQLGetData** 인수와 함께 *Col*_or\_*Param_Num* 첫 번째 사용 가능한 매개 변수 데이터를 검색 하는 서 수 매개 변수로 설정 합니다. 경우 **SQLGetData** SQL_SUCCESS_WITH_INFO 및 SQLState 01004 (데이터 잘림)을 반환 하 고 형식을 클라이언트와 서버 모두에서 가변 길이, 더 많은 데이터가에서 첫 번째 사용 가능한 매개 변수를 검색 합니다. 호출을 계속할 수 있습니다 **SQLGetData** 다른 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 반환 될 때까지 **SQLState**합니다.  
  
5.  3 단계와 현재 매개 변수를 검색 하는 4 단계를 반복 합니다.  
  
6.  호출 **SQLParamData** 다시 합니다. SQL_PARAM_DATA_AVAILABLE 제외 하 고, 반환 하는 경우 더 이상 스트리밍된 매개 변수 데이터를 검색, 되며 반환 코드의 다음 문이 실행 되는 반환 코드가 됩니다.  
  
7.  호출 **SQLMoreResults** sql_no_data가 반환 될 때까지 다음 매개 변수 집합을 처리할 수 있습니다. **SQLMoreResults** SQL_ATTR_PARAMSET_SIZE 문 특성을 1로 설정 된 경우이 예제에서 SQL_NO_DATA를 반환 합니다. 그렇지 않으면 **SQLMoreResults** SQL_PARAM_DATA_AVAILABLE 있는데 스트리밍된 출력 매개 변수는 다음 매개 변수 집합을 검색에 사용할 수를 반환 합니다.  
  
 마찬가지로 디지털 오디오 입력된 매개 변수, 인수에 토큰 사용 *ParameterValuePtr* 에 **SQLBindParameter** (1 단계)를 포함 하는 응용 프로그램 데이터 구조를 가리키는 포인터 수는 필요한 경우 매개 변수 및 추가 응용 프로그램 관련 정보를의 서 수입니다.  
  
 입/출력 매개 변수 또는 반환 된 스트리밍된 출력의 순서는 드라이버 특정 있으며 쿼리에 지정 된 순서와 동일 항상 수 없을 수도 있습니다.  
  
 응용 프로그램을 호출 하지 않는 **SQLGetData** 4 단계에서 매개 변수 값은 무시 됩니다. 마찬가지로, 응용 프로그램을 호출 하는 경우 **SQLParamData** 전에 모든 매개 변수에서 값을 읽을 **SQLGetData**값의 나머지 부분에서는 무시 되 고 응용 프로그램에는 다음 처리할 수 있습니다, 매개 변수입니다.  
  
 응용 프로그램을 호출 하는 경우 **SQLMoreResults** 전에 모든 스트리밍된 출력 매개 변수 처리 (**SQLParamData** SQL_PARAM_DATA_AVAILABLE 반환 여전히 않는), 모든 나머지 매개 변수는 삭제 됩니다. 마찬가지로, 응용 프로그램을 호출 하는 경우 **SQLMoreResults** 전에 모든 매개 변수에서 값을 읽을 **SQLGetData**, 나머지 값과 나머지 모든 매개 변수는 무시 되 고 응용 프로그램 계속 다음 매개 변수 집합을 처리할 수 있습니다.  
  
 응용 프로그램을 둘 다에서 C 데이터 형식을 지정할 수 **SQLBindParameter** 및 **SQLGetData**합니다. C 데이터 형식으로 지정 된 **SQLGetData** C 데이터 형식에 지정 된 재정의 **SQLBindParameter**C 데이터 형식을 지정 하지 않는 한, **SQLGetData** SQL_APD_TYPE 됩니다.  
  
 스트리밍된 출력 매개 변수는 출력 매개 변수의 데이터 형식이 BLOB 형식의 때 보다 유용, 있지만이 기능 데이터 형식과 함께 사용 수도 있습니다. 드라이버에서 스트리밍된 출력 매개 변수에서 지 원하는 데이터 형식 지정 됩니다.  
  
 처리할 SQL_PARAM_INPUT_OUTPUT_STREAM 매개 변수가 **SQLExecute** 또는 **SQLExecDirect** 먼저 SQL_NEED_DATA를 반환 합니다. 응용 프로그램에서 호출할 수 **SQLParamData** 및 **SQLPutData** 디지털 오디오 매개 변수 데이터를 보내려고 합니다. 모든 디지털 오디오 입력된 매개 변수를 처리 하는 경우 **SQLParamData** SQL_PARAM_DATA_AVAILABLE 스트리밍된 출력 매개 변수를 나타내는 반환 합니다.  
  
 출력 매개 변수 및 바인딩된 출력 매개 변수 처리 스트리밍되는 기 하는 경우 드라이버는 출력 매개 변수를 처리 하는 것에 대 한 순서를 결정 합니다. 따라서 출력 매개 변수 버퍼에 바인딩된 경우 (의 **SQLBindParameter** 매개 변수 *InputOutputType* SQL_PARAM_OUTPUT 또는 SQL_PARAM_INPUT_OUTPUT로 설정), 버퍼 될때까지구성될수없습니다 **SQLParamData** SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 반환 합니다. 응용 프로그램에 바인딩된 읽어야 후에 버퍼 **SQLParamData** 처리 SQL_SUCCESS 또는 출력 매개 변수 모두 스트리밍되는 SQL_SUCCESS_WITH_INFO를 반환 합니다.  
  
 데이터 소스는 경고 및 결과 집합, 또한 스트리밍된 출력 매개 변수를 반환할 수 있습니다. 일반적으로 경고 및 결과 집합이 개별적으로 처리 되는 스트림된 출력 매개 변수에서 호출 하 여 **SQLMoreResults**합니다. 프로세스 경고 및 결과 집합의 스트리밍된 출력 매개 변수를 처리 하기 전에 합니다.  
  
 다음 표에서 단일 서버 및 응용 프로그램이 어떻게 작업 해야 전송 명령의 다른 시나리오를 설명 합니다.  
  
|시나리오|SQLExecute 또는 SQLExecDirect에서 값을 반환 합니다.|다음 작업을|  
|--------------|---------------------------------------------------|---------------------|  
|데이터에 스트리밍된 출력 매개 변수가 포함 됩니다.|SQL_PARAM_DATA_AVAILABLE|사용 하 여 **SQLParamData** 및 **SQLGetData** 스트리밍된 출력 매개 변수를 가져옵니다.|  
|데이터는 결과 집합을 포함 하 고 스트림된 출력 매개 변수|SQL_SUCCESS|결과 집합을 검색할 **SQLBindCol** 및 **SQLGetData**합니다.<br /><br /> 호출 **SQLMoreResults** 스트리밍된 출력 매개 변수를 처리 하기 시작 합니다. SQL_PARAM_DATA_AVAILABLE을 반환 합니다.<br /><br /> 사용 하 여 **SQLParamData** 및 **SQLGetData** 스트리밍된 출력 매개 변수를 가져옵니다.|  
|데이터 경고 메시지를 포함 하 고 스트림된 출력 매개 변수|SQL_SUCCESS_WITH_INFO|사용 하 여 **SQLGetDiagRec** 및 **SQLGetDiagField** 경고에서 메시지를 처리 합니다.<br /><br /> 호출 **SQLMoreResults** 스트리밍된 출력 매개 변수를 처리 하기 시작 합니다. SQL_PARAM_DATA_AVAILABLE을 반환 합니다.<br /><br /> 사용 하 여 **SQLParamData** 및 **SQLGetData** 스트리밍된 출력 매개 변수를 가져옵니다.|  
|결과 집합과 스트림된 출력 매개 변수, 데이터 경고 메시지에 포함 됩니다.|SQL_SUCCESS_WITH_INFO|사용 하 여 **SQLGetDiagRec** 및 **SQLGetDiagField** 경고에서 메시지를 처리 합니다. 그런 다음 호출 **SQLMoreResults** 결과 처리를 시작 하도록 설정 합니다.<br /><br /> 결과 집합을 검색할 **SQLBindCol** 및 **SQLGetData**합니다.<br /><br /> 호출 **SQLMoreResults** 스트리밍된 출력 매개 변수를 처리 하기 시작 합니다. **SQLMoreResults** SQL_PARAM_DATA_AVAILABLE 반환 해야 합니다.<br /><br /> 사용 하 여 **SQLParamData** 및 **SQLGetData** 스트리밍된 출력 매개 변수를 가져옵니다.|  
|예를 들어 스트리밍된 입/출력 (디지털 오디오) 매개 변수 디지털 오디오 입력된 매개 변수가 있는 쿼리|SQL NEED_DATA|호출 **SQLParamData** 및 **SQLPutData** 입력 매개 변수 데이터를 디지털 오디오를 보내려고 합니다.<br /><br /> 모든 디지털 오디오 입력된 매개 변수를 처리 한 후 **SQLParamData** 모든 반환 코드를 반환할 수 **SQLExecute** 및 **SQLExecDirect** 반환할 수 있습니다. 이 테이블의 경우 적용할 수 있습니다.<br /><br /> 반환 코드가 SQL_PARAM_DATA_AVAILABLE 이면 스트리밍된 출력 매개 변수는 사용할 수 있습니다. 호출 하는 응용 프로그램 **SQLParamData** 이 테이블의 첫 번째 행에 설명 된 대로 스트리밍된 출력 매개 변수에 대 한 토큰을 검색 하려면 다시 합니다.<br /><br /> 반환 코드는 관계 없이 SQL_SUCCESS를 처리할 결과 집합이 또는 처리가 완료 된 것입니다.<br /><br /> 반환 코드는 SQL_SUCCESS_WITH_INFO를 경우 경고 메시지를 처리 합니다.|  
  
 후 **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 응용 프로그램이 호출 하는 경우 반환 SQL_PARAM_DATA_AVAILABLE는 함수 시퀀스 오류 발생 한 다음 목록에 없는 기능:  
  
-   **SQLAllocHandle** / **SQLAllocHandleStd**  
  
-   **SQLDataSources** / **SQLDrivers**  
  
-   **SQLGetInfo** / **SQLGetFunctions**  
  
-   **SQLGetConnectAttr** / **SQLGetEnvAttr** / **SQLGetDescField** / **SQLGetDescRec**  
  
-   **SQLNumParams**  
  
-   **SQLDescribeParam**  
  
-   **SQLNativeSql**  
  
-   **SQLParamData**  
  
-   **SQLMoreResults**  
  
-   **SQLGetDiagField** / **SQLGetDiagRec**  
  
-   **SQLCancel**  
  
-   **SQLCancelHandle** (문 핸들로)  
  
-   **SQLFreeStmt** (옵션 = SQL_CLOSE, SQL_DROP 또는 SQL_UNBIND)  
  
-   **SQLCloseCursor**  
  
-   **SQLDisconnect**  
  
-   **SQLFreeHandle** (HandleType 여 =)  
  
-   **SQLGetStmtAttr**  
  
 응용 프로그램을 계속 사용할 수 **SQLSetDescField** 또는 **SQLSetDescRec** 바인딩 정보를 설정 합니다. 필드 매핑은 바뀌지 않습니다. 그러나 설명자 안에서 필드를 새 값을 반환할 수 있습니다. 예를 들어 SQL_PARAM_INPUT_OUTPUT_STREAM 또는 SQL_PARAM_OUTPUT_STREAM DESC_PARAMETER_TYPE 반환할 수 있습니다.  
  
## <a name="usage-scenario-retrieve-an-image-in-parts-from-a-result-set"></a>결과 집합에서 부분에 있는 이미지를 검색 하는 사용 시나리오의 경우:  
 **SQLGetData** 저장된 프로시저가 이미지에 대 한 메타 데이터의 한 행을 포함 하는 결과 집합을 반환 하 고 큰 출력 매개 변수에서 이미지 반환 됩니다 부분에서 데이터를 가져오는 데 사용할 수 있습니다.  
  
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
  
## <a name="usage-scenario-send-and-receive-a-large-object-as-a-streamed-inputoutput-parameter"></a>사용 시나리오의 경우: 스트리밍된 입/출력 매개 변수로 큰 개체를 주고받는 설정 합니다.  
 **SQLGetData** 가져오고 하 고 데이터베이스에서 값을 스트리밍 입/출력 매개 변수로 사용 하는 큰 개체를 전달 하는 저장된 프로시저 경우 파트의 데이터를 보내는 데 사용할 수 있습니다. 메모리에 모든 데이터를 저장할 필요가 없습니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)
