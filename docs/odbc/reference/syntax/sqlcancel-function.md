---
title: SQLCancel 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 94f823cdefe4b3e5a62beb62062356dad3a88a03
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036122"
---
# <a name="sqlcancel-function"></a>SQLCancel 함수
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **Sqlcancel** 은 문에서 처리를 취소 합니다.  
  
 연결 또는 문에서 처리를 취소 하려면 [Sqlcancelhandle 함수](../../../odbc/reference/syntax/sqlcancelhandle-function.md)를 사용 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLCancel(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 입력 문 핸들입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **Sqlcancel** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환 하는 경우 *HandleType* SQL_HANDLE_STMT의 및 *StatementHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 **Sqlcancel** 에서 일반적으로 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. MessageText 버퍼에서 [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다. * \**|  
|HY001|메모리 할당 오류|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. 이 비동기 함수는 **Sqlcancel** 함수가 호출 될 때 실행 되 고 있습니다.<br /><br /> *StatementHandle*와 연결 된 연결 핸들에 대해 비동기 작업이 진행 중 이므로 (DM) 취소 작업이 실패 했습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY018|서버 취소 요청 거부|서버에서 취소 요청을 거부 했습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *StatementHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 **Sqlcancel** 은 문에서 다음 유형의 처리를 취소할 수 있습니다.  
  
-   문에서 비동기적으로 실행 되는 함수입니다.  
  
-   데이터를 필요로 하는 문에 대 한 함수입니다.  
  
-   다른 스레드의 문에서 실행 되는 함수입니다.  
  
 ODBC 2. *x*는 문에 대해 처리를 수행 하지 않는 경우 응용 프로그램이 **sqlcancel** 을 호출 하는 경우 **sqlcancel** 은 SQL_CLOSE 옵션을 사용 하 여 **SQLFreeStmt** 와 동일한 효과를 가집니다. 이 동작은 완전성을 위해서만 정의 되며 응용 프로그램은 **SQLFreeStmt** 또는 **SQLCloseCursor** 를 호출 하 여 커서를 닫아야 합니다.  
  
 문이 나 데이터를 필요로 하는 문의 함수에서 비동기적으로 실행 되는 함수를 취소 하기 위해 **sqlcancel** 이 호출 되 면 취소 중인 함수에서 게시 된 진단 레코드가 지워지고 **sqlcancel** 에서 자체 진단 레코드를 게시 합니다. 그러나 **Sqlcancel** 을 호출 하 여 다른 스레드의 문에서 실행 중인 함수를 취소 하는 경우에는 취소 된 함수의 진단 레코드를 지우지 않고 자체 진단 레코드를 게시 하지 않습니다.  
  
## <a name="canceling-asynchronous-processing"></a>비동기 처리 취소  
 응용 프로그램은 비동기적으로 함수를 호출 하면 함수를 반복적으로 호출 하 여 처리가 완료 되었는지 여부를 확인 합니다. 함수가 아직 처리 중인 경우 SQL_STILL_EXECUTING 반환 됩니다. 함수 처리가 완료 되 면 다른 코드를 반환 합니다.  
  
 SQL_STILL_EXECUTING를 반환 하는 함수를 호출한 후 응용 프로그램에서 **Sqlcancel** 을 호출 하 여 함수를 취소할 수 있습니다. 취소 요청이 성공 하면 드라이버는 SQL_SUCCESS을 반환 합니다. 이 메시지는 함수가 실제로 취소 되었음을 나타내는 것은 아닙니다. 이는 취소 요청이 처리 되었음을 나타냅니다. 함수가 실제로 취소 된 경우 또는는 드라이버 종속 및 데이터 소스에 따라 다릅니다. 응용 프로그램은 반환 코드를 SQL_STILL_EXECUTING 하지 않을 때까지 계속 원래 함수를 호출 해야 합니다. 함수가 성공적으로 취소 된 경우 반환 코드는 SQL_ERROR 및 SQLSTATE HY008 (작업 취소 됨)입니다. 함수가 정상적으로 처리를 완료 한 경우에는 함수가 성공 하거나 SQL_ERROR 경우 반환 코드는 SQL_SUCCESS 되거나 함수가 실패 한 경우에는 HY008 (작업 취소 됨) 이외의 SQLSTATE가 SQL_SUCCESS_WITH_INFO 됩니다.  
  
> [!NOTE]  
>  ODBC 3.5에서 문에 대해 수행 되는 처리가 없는 경우 **Sqlcancel** 호출은 SQL_CLOSE 옵션을 사용 하 여 **SQLFreeStmt** 로 처리 되지 않지만 전혀 영향을 주지는 않습니다. 커서를 닫으려면 응용 프로그램이 **Sqlcancel**이 아닌 **SQLCloseCursor**를 호출 해야 합니다.  
  
 비동기 처리에 대 한 자세한 내용은 [비동기 실행](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)을 참조 하세요.  
  
## <a name="canceling-functions-that-need-data"></a>데이터가 필요한 함수 취소  
 **Sqlexecute** 또는 **sqlexecdirect** 는 SQL_NEED_DATA을 반환 하 고 모든 실행 시 데이터 매개 변수에 대해 데이터를 전송 하기 전에 응용 프로그램에서 **sqlexecute** 을 호출 하 여 문 실행을 취소할 수 있습니다. 문이 취소 된 후에는 응용 프로그램에서 **Sqlexecute** 또는 **sqlexecdirect** 를 다시 호출할 수 있습니다. 자세한 내용은 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)를 참조 하세요.  
  
 **SQLBulkOperations** 또는 **SQLSetPos** 는 SQL_NEED_DATA을 반환 하 고 모든 실행 시 데이터 열에 대해 데이터를 전송 하기 전에 응용 프로그램에서 **sqlcancel** 을 호출 하 여 작업을 취소할 수 있습니다. 작업이 취소 되 면 응용 프로그램은 **SQLBulkOperations** 또는 **SQLSetPos** 를 다시 호출할 수 있습니다. 취소 해도 커서 상태나 현재 커서 위치에는 영향을 주지 않습니다. 자세한 내용은 [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md) 또는 [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)를 참조 하세요.  
  
## <a name="canceling-functions-executing-on-another-thread"></a>다른 스레드에서 실행 중인 함수 취소  
 다중 스레드 응용 프로그램에서 응용 프로그램은 다른 스레드에서 실행 중인 함수를 취소할 수 있습니다. 함수를 취소 하기 위해 응용 프로그램은 대상 함수에서 사용 하는 것과 동일한 문 핸들을 사용 하 여 **Sqlcancel** 을 호출 하지만 다른 스레드에서는 호출 합니다. 함수를 취소 하는 방법은 드라이버 및 운영 체제에 따라 달라 집니다. 비동기적으로 실행 되는 함수를 취소 하는 것 처럼 **Sqlcancel** 의 반환 코드는 드라이버가 요청을 성공적으로 처리 했는지 여부를 나타냅니다. SQL_SUCCESS 또는 SQL_ERROR만 반환 될 수 있습니다. 진단 정보는 반환 되지 않습니다. 원래 함수가 취소 되 면 SQL_ERROR 및 SQLSTATE HY008 (작업 취소 됨)를 반환 합니다.  
  
 문 실행을 취소 하기 위해 **Sqlcancel** 이 다른 스레드에서 호출 될 때 SQL 문이 실행 되는 경우 취소가 성공 하는 동안 실행이 성공 하 고 SQL_SUCCESS를 반환할 수 있습니다. 이 경우 드라이버 관리자는 문 실행에 의해 열린 커서가 취소에 의해 닫 혔으 므로 응용 프로그램은 커서를 사용할 수 없습니다.  
  
 스레딩에 대 한 자세한 내용은 [다중 스레딩](../../../odbc/reference/develop-app/multithreading.md)을 참조 하세요.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|매개 변수에 버퍼 바인딩|[SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|대량 삽입 또는 업데이트 작업 수행|[SQLBulkOperations 함수](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|**Sqlcancel**의 기능 외에도 연결 핸들에서 비동기적으로 실행 되는 함수를 취소 합니다.|[SQLCancelHandle 함수](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문 실행|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|문 핸들 해제|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|진단 레코드의 필드 또는 진단 헤더의 필드 가져오기|[SQLGetDiagField 함수(SQLGetDiagField Function)](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
|진단 데이터 구조의 여러 필드 가져오기|[SQLGetDiagRec 함수](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|  
|다음 매개 변수를 반환 하 여 데이터 보내기|[SQLParamData 함수](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|실행 시 매개 변수 데이터 보내기|[SQLPutData 함수](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|행 집합에서 커서 위치를 지정 하거나, 행 집합의 데이터를 새로 고치거 나, 결과 집합에서 데이터를 업데이트 하거나 삭제 합니다.|[SQLSetPos 함수](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
