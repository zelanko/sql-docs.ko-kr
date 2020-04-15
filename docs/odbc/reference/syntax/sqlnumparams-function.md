---
title: SQLNumParams 함수 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLNumParams
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLNumParams
helpviewer_keywords:
- SQLNumParams function [ODBC]
ms.assetid: dbf2da44-253b-4094-bd6b-29bafc23c7a3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1a968e6c7bc7c502d507072f0d7fd70c12c46901
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306944"
---
# <a name="sqlnumparams-function"></a>SQLNumParams 함수
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLNumParams은** SQL 문의 매개 변수 수를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLNumParams(  
     SQLHSTMT        StatementHandle,  
     SQLSMALLINT *   ParameterCountPtr);  
```  
  
## <a name="arguments"></a>인수  
 *명령문 핸들*  
 [입력] 명령문 핸들입니다.  
  
 *매개 변수CountPtr*  
 [출력] 명령문의 매개 변수 수를 반환할 버퍼를 포인터합니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLNumParams** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환 하는 경우 관련 된 SQLSTATE 값 SQL_HANDLE_STMT *핸들 유형* 및 문 *핸들*핸들의 *핸들을* 호출 하 여 **SQLGetDiagRec를** 호출 하 여 가져올 수 있습니다. 다음 표에서는 **SQLNumParams에서** 일반적으로 반환되는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결된 데이터 원본 간의 통신 링크가 실패했습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY08|작업 취소됨|*명령문 핸들*에 대해 비동기 처리가 활성화되었습니다. **SQLNumParams** 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** *명령문 핸들에서*호출되었습니다. 그런 다음 **SQLNumParams** 함수가 *문 핸들에서*다시 호출되었습니다.<br /><br /> 또는 **SQLNumParams** 함수가 호출되고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle에서* 호출되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) 이 함수는 **SQLPrepare** 또는 **SQLExecDirect** 를 *명령문 핸들에*대해 호출하기 전에 호출되었습니다.<br /><br /> (DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. **SQLNumParams** 함수가 호출될 때 이 비동기 함수가 계속 실행중이었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 함수 (이 하나) *StatementHandle에* 대 한 호출 하 고이 함수를 호출 될 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *문 핸들에* 대해 호출되고 SQL_NEED_DATA 반환되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle와* 연결된 드라이버는 함수를 지원하지 않습니다.|  
|IM017|비동기 알림 모드에서 폴링이 비활성화됨|알림 모델을 사용할 때마다 폴링이 비활성화됩니다.|  
|IM018|**SQLCompleteAsync이** 핸들에 이전 비동기 작업을 완료 하기 위해 호출 되지 않았습니다.|핸들의 이전 함수 호출이 SQL_STILL_EXECUTING 반환하고 알림 모드가 활성화된 경우 **SQLCompleteAsync를** 호출하여 사후 처리를 수행하여 작업을 완료해야 합니다.|  
  
## <a name="comments"></a>주석  
 **SQLNumParamsSQLPrepare가** 호출된 후에만 호출할 수 있습니다. **SQLPrepare**  
  
 *StatementHandle와* 연결된 명령문에 매개 변수가 포함되어 있지 않으면 **SQLNumParams은** **ParameterCountPtr을* 0으로 설정합니다.  
  
 **SQLNumParams에서** 반환되는 매개 변수 수는 IPD의 SQL_DESC_COUNT 필드와 동일한 값입니다.  
  
 자세한 내용은 [매개 변수 설명을](../../../odbc/reference/develop-app/describing-parameters.md)참조하십시오.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|버퍼를 매개 변수에 바인딩|[SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|명령문에서 매개 변수에 대한 정보 반환|[SQLDescribeParam 함수(SQLDescribeParam Function)](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
