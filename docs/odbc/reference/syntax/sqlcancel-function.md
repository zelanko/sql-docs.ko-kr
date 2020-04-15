---
title: SQLCancel 함수 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCancel
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLCancel
helpviewer_keywords:
- SQLCancel function [ODBC]
ms.assetid: ac0b5972-627f-4440-8c5a-0e8da728726d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fcc2afce495a1481692ba1f20162a2df5d9a9458
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301313"
---
# <a name="sqlcancel-function"></a>SQLCancel 함수
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLCancel는** 명령문에 대한 처리를 취소합니다.  
  
 연결 또는 명령문에 대한 처리를 취소하려면 [SQLCancelHandle 함수를](../../../odbc/reference/syntax/sqlcancelhandle-function.md)사용합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLCancel(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>인수  
 *명령문 핸들*  
 [입력] 명령문 핸들입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLCancel이** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환하는 경우 *핸들 유형* SQL_HANDLE_STMT 및 *명령문* *핸들* 핸들을 사용하는 **SQLGetDiagRec를** 호출하여 연결된 SQLSTATE 값을 가져올 수 있습니다. 다음 표에서는 **SQLCancel에서** 일반적으로 반환되는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. *인수 \*MessageText* 버퍼에서 [SQLGetDiagRec에서](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다.|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. 이 비동기 함수는 **SQLCancel** 함수가 호출될 때 계속 실행 중이었습니다.<br /><br /> (DM) *명령문 핸들과*연결된 연결 핸들에서 비동기 작업이 진행 중이기 때문에 작업이 취소되지 않았습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY018|서버 취소 요청 거부|서버가 취소 요청을 거부했습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle와* 연결된 드라이버는 함수를 지원하지 않습니다.|  
  
## <a name="comments"></a>주석  
 **SQLCancel는** 명령문에서 다음과 같은 처리 유형을 취소할 수 있습니다.  
  
-   명령문에서 비동기적으로 실행되는 함수입니다.  
  
-   데이터가 필요한 명령문의 함수입니다.  
  
-   다른 스레드의 명령문에서 실행되는 함수입니다.  
  
 ODBC 2. *x*, 응용 프로그램이 **SQLCancel을** 호출하는 경우 명령문에 대한 처리가 수행되지 않으면 **SQLCancel은** SQL_CLOSE 옵션을 사용 하 여 **SQLFreeStmt와** 동일한 영향을 받습니다. 이 동작은 완전성에 대해서만 정의되며 응용 프로그램은 **SQLFreeStmt** 또는 **SQLCloseCursor를** 호출하여 커서를 닫아야 합니다.  
  
 **SQLCancel이** 데이터가 필요한 명령문또는 명령문의 함수에서 비동기적으로 실행되는 함수를 취소하도록 호출되면 취소되는 함수에 의해 게시된 진단 레코드가 지워지고 **SQLCancel은** 자체 진단 레코드를 게시합니다. **그러나 SQLCancel이** 다른 스레드의 명령문에서 실행되는 함수를 취소하도록 호출되면 취소되는 함수의 진단 레코드가 지워지지 않고 자체 진단 레코드를 게시하지 않습니다.  
  
## <a name="canceling-asynchronous-processing"></a>비동기 처리 취소  
 응용 프로그램이 비동기적으로 함수를 호출한 후 함수를 반복적으로 호출하여 처리가 완료되었는지 확인합니다. 함수가 여전히 처리 중이면 SQL_STILL_EXECUTING 반환합니다. 함수가 처리를 완료하면 다른 코드를 반환합니다.  
  
 SQL_STILL_EXECUTING 반환하는 함수를 호출한 후 응용 프로그램은 **SQLCancel을** 호출하여 함수를 취소할 수 있습니다. 취소 요청이 성공하면 드라이버는 SQL_SUCCESS 반환합니다. 이 메시지는 함수가 실제로 취소되었음을 나타내지 않습니다. 취소 요청이 처리되었지만 있음을 나타냅니다. 함수가 실제로 취소되는 시기 또는 경우 드라이버에 따라 다르며 데이터 원본에 종속됩니다. 반환 코드가 SQL_STILL_EXECUTING 않을 때까지 응용 프로그램은 원래 함수를 계속 호출해야 합니다. 함수가 성공적으로 취소된 경우 반환 코드가 SQL_ERROR SQLSTATE HY008(작업이 취소)됩니다. 함수가 정상적인 처리를 완료하면 함수가 성공했거나 SQL_ERROR 함수가 실패한 경우 반환 코드가 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO 및 함수가 실패한 경우 HY008(작업 취소됨)이 아닌 SQLSTATE가 수행됩니다.  
  
> [!NOTE]  
>  ODBC 3.5에서 **SQLCancel에** 대 한 호출 은 명령문에 처리 되지 않는 경우 SQL_CLOSE 옵션으로 **SQLFreeStmt로** 처리 되지 않습니다 하지만 전혀 영향을 주지 않습니다. 커서를 닫기 위해 응용 프로그램은 **SQLCloseCursor를**호출해야 **합니다.**  
  
 비동기 처리에 대한 자세한 내용은 [비동기 실행](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)을 참조하십시오.  
  
## <a name="canceling-functions-that-need-data"></a>데이터가 필요한 함수 취소  
 **SQLExecute** 또는 **SQLExecDirect가** SQL_NEED_DATA 반환하고 모든 실행 시 데이터 매개 변수에 대한 데이터를 보내기 전에 응용 프로그램은 **SQLCancel을** 호출하여 명령문 실행을 취소할 수 있습니다. 명령문이 취소된 후 응용 프로그램은 **SQLExecute** 또는 **SQLExecDirect를** 다시 호출할 수 있습니다. 자세한 내용은 [SQLBind매개 변수](../../../odbc/reference/syntax/sqlbindparameter-function.md)를 참조하십시오.  
  
 **SQLBulkOperations** 또는 **SQLSetPos** SQL_NEED_DATA 반환 하 고 모든 실행 시 데이터 열에 대 한 데이터를 전송 하기 전에 응용 프로그램 **호출SQLCancel** 작업을 취소할 수 있습니다. 작업이 취소된 후 응용 프로그램은 **SQLBulkOperations** 또는 **SQLSetPos를** 다시 호출할 수 있습니다. 취소는 커서 상태 또는 현재 커서 위치에 영향을 주지 않습니다. 자세한 내용은 [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md) 또는 [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)를 참조하십시오.  
  
## <a name="canceling-functions-executing-on-another-thread"></a>다른 스레드에서 실행 하는 함수 취소  
 다중 스레드 응용 프로그램에서 응용 프로그램은 다른 스레드에서 실행 중인 함수를 취소할 수 있습니다. 함수를 취소하기 위해 응용 프로그램은 대상 함수에서 사용하는 것과 동일한 문 핸들을 사용하지만 다른 스레드에서 **SQLCancel을** 호출합니다. 이 기능을 취소하는 방법은 드라이버와 운영 체제에 따라 다릅니다. 비동기적으로 실행 중인 함수를 취소할 때와 마찬가지로 **SQLCancel의** 반환 코드는 드라이버가 요청을 성공적으로 처리했는지 여부만 나타냅니다. SQL_SUCCESS 또는 SQL_ERROR 반환할 수 있습니다. 진단 정보가 반환되지 않습니다. 원래 함수가 취소되면 SQL_ERROR 및 SQLSTATE HY008(작업 취소)이 반환됩니다.  
  
 **SQLCancel이** 다른 스레드에서 명령문 실행을 취소하도록 호출될 때 SQL 문이 실행되는 경우 실행이 성공하고 취소가 성공하는 동안 SQL_SUCCESS 반환할 수 있습니다. 이 경우 드라이버 관리자는 문 실행에 의해 열린 커서가 취소에 의해 닫혀 있다고 가정하므로 응용 프로그램은 커서를 사용할 수 없습니다.  
  
 스레딩에 대한 자세한 내용은 [다중 스레딩](../../../odbc/reference/develop-app/multithreading.md)을 참조하십시오.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|버퍼를 매개 변수에 바인딩|[SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|대량 삽입 또는 업데이트 작업 수행|[SQLBulkOperations 함수](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|**SQLCancel**의 기능 외에도 연결 핸들에서 비동기적으로 실행되는 함수를 취소합니다.|[SQLCancelHandle 함수](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비된 SQL 문 실행|[SQL실행 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|명령문 핸들 해제|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|진단 레코드 필드 또는 진단 헤더 필드 구하기|[SQLGetDiagField 함수](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
|진단 데이터 구조의 여러 필드 구하기|[SQLGetDiagRec 함수](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|  
|다음 매개 변수를 반환하여 데이터를|[SQLParamData 함수](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|실행 시 매개 변수 데이터 전송|[SQLPutData 함수](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|행 집합에 커서 위치 지정, 행 집합의 데이터 새로 고침 또는 결과 집합에서 데이터 업데이트 또는 삭제|[SQLSetPos 함수](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
