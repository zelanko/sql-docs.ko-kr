---
title: SQLParamData 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 41cb718b5425315856fe4db27658cce873f90e6b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68018939"
---
# <a name="sqlparamdata-function"></a>SQLParamData 함수
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **Sqlparamdata** 는 **sqlparamdata** 와 함께 사용 되어 문 실행 시에 매개 변수 데이터를 제공 하 고, **SQLGetData** 를 사용 하 여 스트리밍된 출력 매개 변수 데이터를 검색 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLParamData(  
     SQLHSTMT       StatementHandle,  
     SQLPOINTER *   ValuePtrPtr);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 입력 문 핸들입니다.  
  
 *이상 포인터*  
 출력 SQL_DESC_DATA_PTR 설명자 레코드 필드에 포함 된 것 처럼 **SQLBindParameter** (매개 변수 데이터의 경우) 또는 **SQLBindCol** (열 데이터의 경우)에 지정 된 *targetvalueptr* *버퍼의* 주소를 반환할 버퍼에 대 한 포인터입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR, SQL_INVALID_HANDLE 또는 SQL_PARAM_DATA_AVAILABLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **Sqlparamdata** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 *HandleType* SQL_HANDLE_STMT의 및 *StatementHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **Sqlparamdata** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|07006|제한 된 데이터 형식 특성 위반|바인딩된 매개 변수에 대 한 **SQLBindParameter** 의 *ValueType* 인수에 의해 식별 되는 데이터 값을 **SQLBindParameter**의 *ParameterType* 인수로 식별 된 데이터 형식으로 변환할 수 없습니다.<br /><br /> SQL_PARAM_INPUT_OUTPUT 또는 SQL_PARAM_OUTPUT로 바인딩된 매개 변수에 대해 반환 된 데이터 값을 **SQLBindParameter**의 *ValueType* 인수로 식별 된 데이터 형식으로 변환할 수 없습니다.<br /><br /> 하나 이상의 행에 대 한 데이터 값을 변환할 수 없지만 하나 이상의 행이 성공적으로 반환 된 경우이 함수는 SQL_SUCCESS_WITH_INFO을 반환 합니다.|  
|08S01|통신 연결 오류|드라이버가 연결 된 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|22026|문자열 데이터, 길이가 일치하지 않음|**SQLGetInfo** 의 SQL_NEED_LONG_DATA_LEN 정보 형식은 "Y" 이며 긴 매개 변수 (데이터 형식 SQL_LONGVARCHAR, SQL_LONGVARBINARY 또는 긴 데이터 원본 관련 데이터 형식)에 대해 전송 된 데이터는 **SQLBindParameter**의 *StrLen_or_IndPtr* 인수로 지정 된 것 보다 짧습니다.<br /><br /> **SQLGetInfo** 의 SQL_NEED_LONG_DATA_LEN 정보 형식은 "Y"이 고, 긴 열 (데이터 형식 SQL_LONGVARCHAR, SQL_LONGVARBINARY 또는 긴 데이터 원본 관련 데이터 형식)이 **SQLBulkOperations** 로 추가 또는 업데이트 되거나 **SQLSetPos**로 업데이트 된 데이터 행의 열에 해당 하는 길이 버퍼에 지정 된 것 보다 더 작은 데이터를 보냈습니다.|  
|40001|Serialization 오류|다른 트랜잭션과의 리소스 교착 상태가 발생 하 여 트랜잭션이 롤백 되었습니다.|  
|40003|문 완료를 알 수 없음|이 함수를 실행 하는 동안 연결 된 연결에 실패 하 여 트랜잭션의 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. MessageText 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다. * \**|  
|HY001|메모리 할당 오류|드라이버가 실행 또는 함수의 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업 취소됨|*StatementHandle*에 대해 비동기 처리를 사용 하도록 설정 했습니다. 함수가 호출 되었으며 실행이 완료 되기 전에 **sqlcancel** 또는 **Sqlcancelhandle** 이 *StatementHandle*에 대해 호출 되었습니다. 그런 다음 *StatementHandle*에서 함수를 다시 호출 했습니다.<br /><br /> 함수가 호출 되 고 실행이 완료 되기 전에 **sqlcancel** 또는 **sqlcancelhandle** 이 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle* 호출 되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) 이전 함수 호출은 **Sqlexecdirect**, **sqlexecute**, **SQLBulkOperations**또는 반환 코드가 SQL_NEED_DATA 된 **SQLSetPos** 를 호출 하지 않았거나 이전 함수 호출이 **sqlexecdirect**에 대 한 호출입니다.<br /><br /> 이전 함수 호출은 **Sqlparamdata**에 대 한 호출입니다.<br /><br /> (DM) *StatementHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. **Sqlparamdata** 함수가 호출 될 때이 비동기 함수는 계속 실행 중입니다.<br /><br /> (DM) *StatementHandle* 에 대해 비동기적으로 실행 되는 함수 (이 함수 아님)가 호출 되었으며이 함수가 호출 될 때 계속 실행 중입니다.<br /><br /> **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 가 *StatementHandle* 에 대해 호출 되 고 SQL_NEED_DATA 반환 되었습니다. 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 **Sqlcancel** 이 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *StatementHandle* 에 해당 하는 드라이버는 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드에서는 폴링을 사용할 수 없습니다.|알림 모델을 사용할 때마다 폴링은 사용 하지 않도록 설정 됩니다.|  
|IM018|이 핸들에서 이전 비동기 작업을 완료 하기 위해 **SQLCompleteAsync** 가 호출 되지 않았습니다.|핸들에 대 한 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드가 설정 된 경우에는 핸들에 대해 **SQLCompleteAsync** 를 호출 하 여 사후 처리를 수행 하 고 작업을 완료 해야 합니다.|  
  
 SQL 문의 매개 변수에 대 한 데이터를 전송 하는 동안 **Sqlparamdata** 를 호출 하는 경우 문 (**Sqlexecute** 또는 **sqlparamdata**)을 실행 하기 위해 호출 된 함수에 의해 반환 될 수 있는 SQLSTATE를 반환할 수 있습니다. 업데이트 되거나 **SQLBulkOperations** 를 사용 하 여 추가 되거나 **sqlsetpos**로 업데이트 되는 열에 대 한 데이터를 전송 하는 동안 호출 되는 경우 **SQLBulkOperations** 또는 **sqlsetpos**에서 반환 될 수 있는 SQLSTATE를 반환할 수 있습니다.  
  
## <a name="comments"></a>주석  
 **Sqlparamdata** 는 **Sqlexecute** 또는 **sqlparamdata**호출에 사용 되는 매개 변수 데이터 또는 **SQLBulkOperations** 에 대 한 호출에 의해 행이 업데이트 또는 추가 되는 경우 사용 되는 열 데이터 또는 **SQLSetPos**에 대 한 호출로 업데이트 될 때 사용 되는 열 데이터를 실행 하 여 데이터를 호출할 수 있습니다. 실행 시 **Sqlparamdata** 는 드라이버에 필요한 데이터에 대 한 표시기를 응용 프로그램에 반환 합니다.  
  
 응용 프로그램이 **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos**를 호출 하는 경우 드라이버는 실행 시 데이터 데이터가 필요한 경우 SQL_NEED_DATA을 반환 합니다. 그런 다음 응용 프로그램은 **Sqlparamdata** 를 호출 하 여 전송할 데이터를 결정 합니다. 드라이버에서 매개 변수 데이터를 요구 하는 경우 드라이버는 응용 프로그램이 행 집합 버퍼에 배치 하는 값을 * \*valueptrptr* 출력 버퍼에 반환 합니다. 응용 프로그램은이 값을 사용 하 여 드라이버에서 요청 하는 매개 변수 데이터를 확인할 수 있습니다. 드라이버가 열 데이터를 요구 하는 경우 드라이버는 다음과 같이 열이 원래 바인딩된 주소를 * \*valueptrptr* 버퍼로 반환 합니다.  
  
 *바인딩된 주소* + *바인딩 오프셋* + ((*행 번호* -1) x *요소 크기*)  
  
 여기서 변수는 다음 표에 나와 있는 것 처럼 정의 됩니다.  
  
|변수|Description|  
|--------------|-----------------|  
|*바인딩된 주소*|**SQLBindCol**의 *Targetvalueptr* 인수를 사용 하 여 지정 된 주소입니다.|  
|*바인딩 오프셋*|SQL_ATTR_ROW_BIND_OFFSET_PTR statement 특성으로 지정 된 주소에 저장 된 값입니다.|  
|*Row Number*|행 집합의 행 번호 (1부터 수)입니다. 단일 행 페치의 경우 기본값은 1입니다.|  
|*요소 크기*|데이터 및 길이/표시기 버퍼에 대 한 SQL_ATTR_ROW_BIND_TYPE statement 특성의 값입니다.|  
  
 또한 데이터를 보내기 위해 **Sqlputdata** 를 호출 해야 하는 응용 프로그램에 대 한 지표로 SQL_NEED_DATA 반환 합니다.  
  
 응용 프로그램은 열 또는 매개 변수에 대 한 실행 시 데이터 데이터를 보내는 데 필요한 횟수 만큼 **Sqlputdata** 를 호출 합니다. 열 또는 매개 변수에 대 한 모든 데이터를 보낸 후 응용 프로그램은 **Sqlparamdata** 를 다시 호출 합니다. **Sqlparamdata** 가 SQL_NEED_DATA 반환 하는 경우 다른 매개 변수 또는 열에 대해 데이터를 전송 해야 합니다. 따라서 응용 프로그램은 **Sqlputdata**를 다시 호출 합니다. 모든 매개 변수 또는 열에 대해 실행 시 모든 데이터 데이터를 보낸 경우 **sqlparamdata** * \*는 SQL_SUCCESS* 또는 SQL_SUCCESS_WITH_INFO을 반환 하 고, 이상 값을 반환 하거나, SQL 문을 실행 하거나, **SQLBulkOperations** 또는 **SQLSetPos** 호출을 처리할 수 있습니다.  
  
 **Sqlparamdata** 가 데이터 원본의 행에 영향을 주지 않는 검색 된 update 또는 delete 문에 대 한 매개 변수 데이터를 제공 하는 경우 **sqlparamdata** 를 호출 하면 SQL_NO_DATA 반환 됩니다.  
  
 실행 시 데이터 매개 변수 데이터가 문 실행 시 전달 되는 방법에 대 한 자세한 내용은 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) 의 "매개 변수 값 전달" 및 [긴 데이터 전송](../../../odbc/reference/develop-app/sending-long-data.md)을 참조 하세요. 실행 시 데이터 열 데이터를 업데이트 하거나 추가 하는 방법에 대 한 자세한 내용은 [sqlsetpos](../../../odbc/reference/syntax/sqlsetpos-function.md)의 "sqlsetpos 사용" 및 [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)의 "책갈피를 사용 하 여 대량 업데이트 수행" 및 [Long data 및 SQLSetPos 및 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)섹션을 참조 하세요.  
  
 **Sqlparamdata** 를 호출 하 여 스트리밍된 출력 매개 변수를 검색할 수 있습니다. **SQLMoreResults**, **sqlexecute**, **SQLGetData**또는 **sqlexecdirect** 가 SQL_PARAM_DATA_AVAILABLE 반환 하는 경우 **sqlparamdata** 를 호출 하 여 사용할 수 있는 값이 포함 된 매개 변수를 확인 합니다. SQL_PARAM_DATA_AVAILABLE 및 스트리밍된 출력 매개 변수에 대 한 자세한 내용은 [SQLGetData를 사용 하 여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)을 참조 하세요.  
  
## <a name="code-example"></a>코드 예  
 [Sqlputdata](../../../odbc/reference/syntax/sqlputdata-function.md)를 참조 하세요.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|매개 변수에 버퍼 바인딩|[SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|문의 매개 변수에 대 한 정보 반환|[SQLDescribeParam 함수(SQLDescribeParam Function)](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문 실행|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|실행 시 매개 변수 데이터 보내기|[SQLPutData 함수](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [SQLGetData를 사용하여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
