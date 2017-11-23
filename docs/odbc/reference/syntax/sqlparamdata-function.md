---
title: "SQLParamData 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLParamData
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLParamData
helpviewer_keywords: SQLParamData function [ODBC]
ms.assetid: 68fe010d-9539-4e5b-a260-c8d32423b1db
caps.latest.revision: "26"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 10bd29a112823ea3c4aa400b0fd63d1627d55ac5
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="sqlparamdata-function"></a>SQLParamData 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLParamData** 와 함께 사용 **SQLPutData** 및 문 실행 시 매개 변수 데이터 제공 **SQLGetData** 스트리밍된 출력 매개 변수 데이터를 검색 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLParamData(  
     SQLHSTMT       StatementHandle,  
     SQLPOINTER *   ValuePtrPtr);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 [입력] 문 핸들입니다.  
  
 *ValuePtrPtr*  
 [출력] 주소를 반환 하는 버퍼에 대 한 포인터는 *ParameterValuePtr* 에 지정 된 버퍼 **SQLBindParameter** (데이터용 매개 변수) 또는의 주소는 *TargetValuePtr* 에 지정 된 버퍼 **SQLBindCol** (열 데이터의 경우)에 대 한 SQL_DESC_DATA_PTR 설명자 레코드 필드에 포함 된 것입니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR, SQL_INVALID_HANDLE, 또는 SQL_PARAM_DATA_AVAILABLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLParamData** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 관련된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 와 *HandleType* SQL_의 HANDLE_STMT 및 *처리* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLParamData** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|오류|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|07006|제한 된 데이터 형식 특성 위반|데이터 값으로 식별 된 *ValueType* 인수에 **SQLBindParameter** 바인딩된 매개 변수에서 식별 되는 데이터 형식 변환 하지 못했습니다에 대 한는 *ParameterType*인수 **SQLBindParameter**합니다.<br /><br /> SQL_PARAM_OUTPUT 또는 SQL_PARAM_INPUT_OUTPUT 하지 변환 못했습니다으로 식별 되는 데이터 형식으로 바인딩된 매개 변수에 대해 반환 되는 데이터 값의 *ValueType* 인수 **SQLBindParameter**합니다.<br /><br /> (하나 이상의 행에 대 한 데이터 값을 변환할 수 없습니다, 하지만 성공적으로 반환 된 하나 이상의 행을이 함수 SQL_SUCCESS_WITH_INFO를 반환 합니다.)|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버 연결 된 데이터 원본 간에 통신 링크 하지 못했습니다.|  
|22026|문자열 데이터, 길이가 일치하지 않음|SQL_NEED_LONG_DATA_LEN 정보 유형을 **SQLGetInfo** "Y" 였으며가 지정 된 것 보다 적은 양의 데이터 (데이터 형식이 SQL_LONGVARCHAR, SQL_LONGVARBINARY, 또는 긴 데이터 원본에 따른 특정 데이터 형식) 긴 매개 변수에 대 한 전송 와 *StrLen_or_IndPtr* 인수 **SQLBindParameter**합니다.<br /><br /> SQL_NEED_LONG_DATA_LEN 정보 유형을 **SQLGetInfo** "Y" 였으며에 지정 된 것 보다 긴 열 (데이터 형식이 SQL_LONGVARCHAR, SQL_LONGVARBINARY, 또는 긴 데이터 원본에 따른 특정 데이터 형식)에 대 한 전송 하지 않는 데이터는 추가 되었거나 업데이트 된 데이터의 행에 열에 해당 하는 길이 버퍼 **SQLBulkOperations** 또는와 업데이트 된 **SQLSetPos**합니다.|  
|40001|Serialization 오류|트랜잭션이 다른 트랜잭션 사용 하 여 리소스 교착 상태로 인해 롤백 되었습니다.|  
|40003|알 수 없는 문 완성|이 함수를 실행 하는 동안 관련된 연결 실패 및 트랜잭션의 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정할는 *StatementHandle*합니다. 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle*; 함수가에서 다시 호출 후 *StatementHandle*합니다.<br /><br /> 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle* 의 서로 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM) 함수 호출 없습니다에 대 한 호출 **SQLExecDirect**, **SQLExecute**, **SQLBulkOperations**, 또는 **SQLSetPos** 위치는 반환 코드 sql_need_data가 없거나 이전 함수 호출에 대 한 호출 **SQLPutData**합니다.<br /><br /> 이전 함수 호출에 대 한 호출을 했습니다 **SQLParamData**합니다.<br /><br /> DM ()는 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한는 *StatementHandle*합니다. 이 비동기 함수 계속 실행 될 때는 **SQLParamData** 함수를 호출 했습니다.<br /><br /> DM ()를 비동기적으로 실행 중인 함수 (하지이 하나)에 대해 호출 되었습니다는 *StatementHandle* 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, 또는 **SQLSetPos** 가 대 한 호출에서 *StatementHandle* 및 SQL_NEED_DATA를 반환된 합니다. **SQLCancel** 모든 실행 시 데이터 매개 변수 또는 열에 대 한 전송 된 데이터에 호출 되었습니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)에 해당 하는 드라이버는 *StatementHandle* 함수를 지원 하지 않습니다.|  
|IM017|폴링 비동기 알림 모드 사용 불가능|알림 모델을 사용할 때마다 폴링 사용할 수 없습니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하는 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업을 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
 경우 **SQLParamData** 호출 되는 SQL 문의 매개 변수에 대 한 데이터를 전송 하는 동안 문을 실행 하는 호출 되는 함수에서 반환 될 수 있는 모든 SQLSTATE 반환할 수 있습니다 (**SQLExecute** 또는 **SQLExecDirect**). 열에 대 한 데이터를 전송 하는 동안 호출 되 면 업데이트 되거나 추가 된 **SQLBulkOperations** 로 업데이트 또는 **SQLSetPos**, 반환할 수 있지만에서 반환 될 수 있는 모든 SQLSTATE  **SQLBulkOperations** 또는 **SQLSetPos**합니다.  
  
## <a name="comments"></a>설명  
 **SQLParamData** 두 가지 용도 대 한 데이터 실행 시 데이터를 제공 하기 위해 호출할 수:에 대 한 호출에서 사용할 수 있는 매개 변수 데이터 **SQLExecute** 또는 **SQLExecDirect**, 또는 사용 되는 열 데이터 행이 업데이트 되거나 추가를 호출 하 여이 **SQLBulkOperations** 에 대 한 호출에 의해 업데이트 **SQLSetPos**합니다. 실행 시 **SQLParamData** 표시기는 데이터의 드라이버 필요한 응용 프로그램에 반환 합니다.  
  
 응용 프로그램 호출 하는 경우 **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, 또는 **SQLSetPos**, 드라이버 SQL_NEED_를 반환 합니다. 실행 시 데이터 데이터가 필요한 경우 데이터입니다. 응용 프로그램이 호출 **SQLParamData** 보낼 데이터를 확인 하려면. 드라이버 매개 변수 데이터가 필요한 경우 드라이버에서 반환 된  *\*ValuePtrPtr* 출력 버퍼는 행 집합 버퍼에 응용 프로그램이 포함 하는 값입니다. 응용 프로그램은 드라이버가 요청 하는 매개 변수 데이터를 확인 하려면이 값을 사용할 수 있습니다. 드라이버에 열 데이터가 필요한 경우 드라이버에서 반환 된  *\*ValuePtrPtr* 버퍼 열에, 다음과 같이 바인딩된 원래 주소:  
  
 *주소 바인딩된* + *오프셋 바인딩* + ((*행 번호* – 1) x *요소 크기*)  
  
 여기서 변수는 다음 표와 같이 정의 됩니다.  
  
|변수|Description|  
|--------------|-----------------|  
|*바인딩된 주소*|지정 된 주소는 *TargetValuePtr* 인수 **SQLBindCol**합니다.|  
|*바인딩 오프셋*|SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성으로 지정 된 주소에 저장 된 값입니다.|  
|*행 번호*|행 집합의 행 수가 1부터 시작 합니다. 기본값 이므로 단일 행 인출,이 1입니다.|  
|*요소 크기*|데이터와 길이/표시기 버퍼에 대 한 SQL_ATTR_ROW_BIND_TYPE 문 특성의 값입니다.|  
  
 또한 호출 해야 하는 응용 프로그램을 나타내는 sql_need_data가 반환 **SQLPutData** 데이터를 보내려고 합니다.  
  
 응용 프로그램 호출 **SQLPutData** 열 이나 매개 변수에 데이터 실행 시 데이터를 보내는 데 필요한 만큼 반복 합니다. 응용 프로그램 호출 하는 열 이나 매개 변수에 있는 모든 데이터를 보낸 후 **SQLParamData** 다시 합니다. 경우 **SQLParamData** 다시 sql_need_data가 반환 다른 매개 변수 또는 열에 대 한 데이터를 전송 해야 합니다. 따라서 응용 프로그램을 다시 호출 **SQLPutData**합니다. 모든 실행 시 데이터 데이터 보내진 경우 모든 매개 변수 또는 열에 대해 다음 **SQLParamData** SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를에서 값 반환  *\*ValuePtrPtr* 이 정의 되지 않습니다 SQL 문을 실행할 수 있습니다 및 또는 **SQLBulkOperations** 또는 **SQLSetPos** 호출을 처리할 수 있습니다.  
  
 경우 **SQLParamData** 는 검색 결과 대 한 매개 변수 데이터를 공급 업데이트 또는 삭제는 데이터 원본에 대 한 호출에 모든 행에 영향을 미치지 않는 문이 **SQLParamData** SQL_NO_DATA를 반환 합니다.  
  
 문 실행 시 전달 된 방법 데이터 실행 시 매개 변수 데이터에 대 한 자세한 내용은에서 "매개 변수 값 전달" 참조 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) 및 [긴 데이터를 보내는](../../../odbc/reference/develop-app/sending-long-data.md)합니다. 어떻게 데이터 실행 시 열 데이터에 대 한 자세한 내용은 업데이트 되거나 추가 된 섹션을 참조 "를 사용 하 여 SQLSetPos"에서 [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md), "수행 대량 업데이트를 사용 하 여"에서 책갈피 [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), 및 [긴 데이터와 SQLSetPos SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)합니다.  
  
 **SQLParamData** 스트리밍된 출력 매개 변수를 검색 하도록 호출 될 수 있습니다. 때 **SQLMoreResults**, **SQLExecute**, **SQLGetData**, 또는 **SQLExecDirect** 반환 SQL_PARAM_DATA_AVAILABLE, 호출 **SQLParamData** 되는 매개 변수 사용 가능한 값의이를 결정 합니다. SQL_PARAM_DATA_AVAILABLE 및 스트리밍된 출력 매개 변수에 대 한 자세한 내용은 참조 하십시오. [SQLGetData를 사용 하 여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)합니다.  
  
## <a name="code-example"></a>코드 예  
 참조 [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|버퍼는 매개 변수 바인딩|[SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|문의 매개 변수에 대 한 정보 반환|[SQLDescribeParam 함수](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문을 실행합니다.|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|실행 시 매개 변수 데이터 보내기|[SQLPutData 함수](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [SQLGetData를 사용하여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
