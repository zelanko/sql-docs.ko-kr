---
title: SQLParamData 함수 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLParamData
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLParamData
helpviewer_keywords:
- SQLParamData function [ODBC]
ms.assetid: 68fe010d-9539-4e5b-a260-c8d32423b1db
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8ed149e125e3231d670c6ddbd4569ff5ccee5c15
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306924"
---
# <a name="sqlparamdata-function"></a>SQLParamData 함수
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLParamData는** **SQLPutData와** 함께 사용하여 문 실행 시간에 매개 변수 데이터를 제공하고 **SQLGetData와** 함께 스트리밍된 출력 매개 변수 데이터를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLParamData(  
     SQLHSTMT       StatementHandle,  
     SQLPOINTER *   ValuePtrPtr);  
```  
  
## <a name="arguments"></a>인수  
 *명령문 핸들*  
 [입력] 명령문 핸들입니다.  
  
 *밸류PtrPtr*  
 [출력] SQL_DESC_DATA_PTR 설명자 레코드 필드에 포함된 것처럼 *ParameterValuePtr* **SQLBindParameter(매개** 변수 데이터) 또는 **SQLBindCol(열** 데이터의 경우)에 지정된 *TargetValuePtr* 버퍼의 주소를 반환하는 버퍼에 대한 포인터입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR, SQL_INVALID_HANDLE 또는 SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLParamData** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환 하는 경우 관련 된 SQLSTATE 값 SQL_HANDLE_STMT *핸들 SQL_HANDLE_STMT* 핸들 *Handle* *핸들을*호출 하 여 **SQLGetDiagRec를** 호출 하 여 가져올 수 있습니다. 다음 표에서는 **SQLParamData에서** 일반적으로 반환하는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|07006|제한된 데이터 형식 특성 위반|바인딩된 매개 변수에 대 한 **SQLBindParameter의** *ValueType* 인수로 식별 된 데이터 **값은 SQLBindParameter**에서 *ParameterType* 인수에 의해 식별 된 데이터 유형으로 변환할 수 없습니다.<br /><br /> SQL_PARAM_INPUT_OUTPUT 또는 SQL_PARAM_OUTPUT 바인딩된 매개 변수에 대해 반환된 데이터 값은 **SQLBindParameter**에서 *ValueType* 인수로 식별된 데이터 유형으로 변환할 수 없습니다.<br /><br /> 하나 이상의 행에 대한 데이터 값을 변환할 수 없지만 하나 이상의 행이 성공적으로 반환된 경우 이 함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결된 데이터 원본 간의 통신 링크가 실패했습니다.|  
|22026|문자열 데이터, 길이가 일치하지 않음|**SQLGetInfo의** SQL_NEED_LONG_DATA_LEN 정보 형식은 "Y"이고 **SQLBindParameter에서** *StrLen_or_IndPtr* 인수로 지정된 것보다 긴 매개 변수(데이터 형식이 SQL_LONGVARCHAR, SQL_LONGVARBINARY 또는 긴 데이터 원본 별 데이터 형식)에 대해 전송된 데이터가 적습니다.<br /><br /> **SQLGetInfo의** SQL_NEED_LONG_DATA_LEN 정보 형식은 "Y"이고 **SQLBulkOperations로** 추가또는 업데이트된 데이터 행의 열에 해당하는 길이 버퍼에 지정된 것보다 긴 열(데이터 형식이 SQL_LONGVARCHAR, SQL_LONGVARBINARY 또는 긴 데이터 원본 별 데이터 형식)에 대해 전송된 데이터가 **적습니다.**|  
|40001|직렬화 실패|다른 트랜잭션의 리소스 교착 상태 때문에 트랜잭션이 롤백되었습니다.|  
|40003|명령문 완료를 알 수 없음|이 함수를 실행하는 동안 연결된 연결이 실패했으며 트랜잭션 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY08|작업 취소됨|*명령문 핸들*에 대해 비동기 처리가 활성화되었습니다. 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** *명령문 핸들에서*호출되었습니다. 그런 다음 *명령문 핸들에서*함수를 다시 호출했습니다.<br /><br /> 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle에서* 호출되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) 이전 함수 호출은 **SQLExecDirect**, **SQLExecute**, **SQLBulkOperations**또는 반환 코드가 SQL_NEED_DATA **SQLSetPos** 에 대한 호출이 아니며 이전 함수 호출이 **SQLPutData**에 대한 호출이 아니었습니다.<br /><br /> 이전 함수 호출은 **SQLParamData**에 대한 호출이었습니다.<br /><br /> (DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. **SQLParamData** 함수가 호출될 때 이 비동기 함수가 계속 실행중이었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 함수 (이 하나) *StatementHandle에* 대 한 호출 하 고이 함수를 호출 될 때 여전히 실행 되 고.<br /><br /> **SQLExecDirect**, **SQLBulkOperations**또는 **SQLSetPos는** 문 *핸들에* 대해 호출되고 SQL_NEED_DATA 반환되었습니다. **SQLExecDirect** **SQLCancel은** 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle에* 해당하는 드라이버는 함수를 지원하지 않습니다.|  
|IM017|비동기 알림 모드에서 폴링이 비활성화됨|알림 모델을 사용할 때마다 폴링이 비활성화됩니다.|  
|IM018|**SQLCompleteAsync이** 핸들에 이전 비동기 작업을 완료 하기 위해 호출 되지 않았습니다.|핸들의 이전 함수 호출이 SQL_STILL_EXECUTING 반환하고 알림 모드가 활성화된 경우 **SQLCompleteAsync를** 호출하여 사후 처리를 수행하여 작업을 완료해야 합니다.|  
  
 SQL문의 매개 변수에 대한 데이터를 보내는 동안 **SQLParamData가** 호출되는 경우 문을 실행하기 위해 호출된 함수에서 반환할 수 있는 모든 SQLSTATE를 반환할 수**있습니다(SQLExecute** 또는 **SQLExecDirect).** **SQLBulkOperations로** 업데이트되거나 추가되는 열에 대한 데이터를 보내거나 **SQLSetPos로**업데이트하는 동안 호출되는 경우 **SQLBulkOperations** 또는 **SQLSetPos에서**반환할 수 있는 모든 SQLSTATE를 반환할 수 있습니다.  
  
## <a name="comments"></a>주석  
 **SQLParamData는** **SQLExecute** 또는 **SQLExecDirect에**대한 호출에서 사용되는 매개 변수 데이터 또는 행이 **SQLBulkOperations에** 대한 호출에 의해 업데이트되거나 **SQLSetPos**호출에 의해 업데이트될 때 사용되는 열 데이터 등 두 가지 용도에 대한 실행 시 데이터 데이터를 제공하도록 호출할 수 있습니다. 실행 시 **SQLParamData** 드라이버에 필요한 데이터의 표시기를 응용 프로그램에 반환 합니다.  
  
 응용 프로그램이 **SQLExecute,** **SQLExecDirect**, **SQLBulkOperations**또는 **SQLSetPos를**호출하면 실행 시 데이터 데이터가 필요한 경우 드라이버가 SQL_NEED_DATA 반환합니다. 그런 다음 응용 프로그램이 **SQLParamData를** 호출하여 보낼 데이터를 결정합니다. 드라이버에 매개 변수 데이터가 필요한 경우 드라이버는 * \*응용* 프로그램이 행 집합 버퍼에 넣은 값을 ValuePtrPtr 출력 버퍼에서 반환합니다. 응용 프로그램은 이 값을 사용하여 드라이버가 요청하는 매개 변수 데이터를 확인할 수 있습니다. 드라이버에 열 데이터가 필요한 경우 드라이버는 * \*다음과* 같이 열이 원래 바인딩된 주소를 ValuePtrPtr 버퍼에서 반환합니다.  
  
 *바인딩된 주소* + *바인딩 오프셋* +(행*번호* - 1) x *요소 크기)*  
  
 여기서 변수는 다음 표에 표시된 대로 정의됩니다.  
  
|변수|설명|  
|--------------|-----------------|  
|*바운드 주소*|**SQLBindCol**에서 *TargetValuePtr* 인수로 지정된 주소입니다.|  
|*바인딩 오프셋*|SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성으로 지정된 주소에 저장된 값입니다.|  
|*Row Number*|행 집합의 행의 1기반 번호입니다. 기본값인 단일 행 인출의 경우 1입니다.|  
|*요소 크기*|데이터 및 길이/표시기 버퍼모두에 대한 SQL_ATTR_ROW_BIND_TYPE 문 특성의 값입니다.|  
  
 또한 데이터를 보내기 위해 **SQLPutData를** 호출해야 하는 응용 프로그램의 표시기인 SQL_NEED_DATA 반환합니다.  
  
 응용 프로그램은 열 또는 매개 변수에 대한 실행 시 데이터 데이터를 전송하는 데 필요한 만큼 **SQLPutData를** 호출합니다. 열 또는 매개 변수에 대한 모든 데이터가 전송된 후 응용 프로그램은 **SQLParamData를** 다시 호출합니다. **SQLParamData** 다시 SQL_NEED_DATA 반환 하는 경우 다른 매개 변수 또는 열에 대 한 데이터를 보내야 합니다. 따라서 응용 프로그램은 다시 **SQLPutData**를 호출합니다. 모든 매개 변수 또는 열에 대해 모든 실행 시 데이터가 전송된 경우 **SQLParamData는** SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO 반환하고 * \*ValuePtrPtr의* 값이 정의되지 않고 SQL 문을 실행하거나 **SQLBulkOperations** 또는 **SQLSetPos** 호출을 처리할 수 있습니다.  
  
 **SQLParamData** 는 데이터 원본의 행에 영향을 주지 않는 검색된 업데이트 또는 delete 문에 대한 매개 변수 데이터를 제공하는 경우 **SQLParamData** 호출은 SQL_NO_DATA 반환합니다.  
  
 명령문 실행 시간에 데이터 실행 매개 변수 데이터가 전달되는 방법에 대한 자세한 내용은 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) 및 [긴 데이터 전송의](../../../odbc/reference/develop-app/sending-long-data.md)"매개 변수 값 전달"을 참조하십시오. 실행 시 데이터 열 데이터를 업데이트하거나 추가하는 방법에 대한 자세한 내용은 [SQLSetPos의](../../../odbc/reference/syntax/sqlsetpos-function.md)"SQLSetPos 사용" 섹션, [SQLBulkOperations의](../../../odbc/reference/syntax/sqlbulkoperations-function.md)"책갈피를 사용하여 대량 업데이트 수행" 및 [긴 데이터 및 SQLSetPos 및 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)를 참조하십시오.  
  
 **SQLParamData** 스트리밍 된 출력 매개 변수를 검색 하기 위해 호출할 수 있습니다. **SQLMoreResults,** **SQLGetData**또는 **SQLExecDirect가** SQL_PARAM_DATA_AVAILABLE 반환하면 **SQLParamData를** 호출하여 사용 가능한 값이 있는 매개 변수를 확인합니다. **SQLGetData** SQL_PARAM_DATA_AVAILABLE 및 스트리밍된 출력 매개 변수에 대한 자세한 내용은 [SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)를 사용하여 출력 매개 변수 검색을 참조하십시오.  
  
## <a name="code-example"></a>코드 예  
 [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)를 참조하십시오.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|버퍼를 매개 변수에 바인딩|[SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|명령문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|명령문에서 매개 변수에 대한 정보 반환|[SQLDescribeParam 함수(SQLDescribeParam Function)](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비된 SQL 문 실행|[SQL실행 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|실행 시 매개 변수 데이터 전송|[SQLPutData 함수](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [SQLGetData를 사용하여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
