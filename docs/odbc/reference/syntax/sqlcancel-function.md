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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036122"
---
# <a name="sqlcancel-function"></a>SQLCancel 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수 합니다. ISO 92  
  
 **요약**  
 **SQLCancel** 문에서 처리를 취소 합니다.  
  
 연결 또는 명령문에서 처리를 취소 하려면 사용 하 여 [SQLCancelHandle 함수](../../../odbc/reference/syntax/sqlcancelhandle-function.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLCancel(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 [입력] 문 핸들입니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLCancel** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* SQL_의 HANDLE_STMT와 *처리할* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLCancel** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) 인수의  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)를 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한 합니다 *StatementHandle*합니다. 이 비동기 함수가 여전히 실행 시기를 **SQLCancel** 함수를 호출 했습니다.<br /><br /> (DM) 비동기 작업을 연관 된 연결 핸들의 진행 중 이므로 실패 한 작업을 취소할 *StatementHandle*합니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY018|취소 요청을 거부 했습니다.|서버가 취소 요청을 거부 합니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 드라이버를 사용 하 여 연결 합니다 *StatementHandle* 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 **SQLCancel** 다음과 같은 유형의 문에서 처리를 취소할 수 있습니다.  
  
-   문에서 비동기적으로 실행 하는 함수입니다.  
  
-   데이터는 문에서 사용 되는 함수입니다.  
  
-   다른 스레드에서 문을 실행 하는 함수입니다.  
  
 Odbc 2. *x*이면 응용 프로그램이 호출 **SQLCancel** 문에서 프로세스가 수행 되 면 **SQLCancel** 것과 동일한 효과가 **SQLFreeStmt** SQL_CLOSE 옵션과; 참조용 으로만이 동작이 정의 되 고 응용 프로그램을 호출 해야 **SQLFreeStmt** 하거나 **SQLCloseCursor** 를 커서를 닫습니다.  
  
 때 **SQLCancel** 이 호출 함수는 필요한 데이터를 취소 하는 함수에 의해 게시 되는 진단 레코드는 선택을 취소 하면 문에서 문 또는 함수에서 비동기적으로 실행을 취소 하 고 **SQLCancel 그러나**  자체 진단 레코드 게시는 경우 **SQLCancel** 다른 스레드에서 문을 실행 하는 함수를 취소 하려면 지워지지 않습니다 진단 라고 되는 레코드 함수 및 취소 되지 않습니다 자체 진단 레코드를 게시 합니다.  
  
## <a name="canceling-asynchronous-processing"></a>비동기 처리를 취소합니다.  
 응용 프로그램이 함수를 비동기적으로 호출 하는 후 처리를 완료 되었는지 여부를 결정 하는 반복적으로 함수를 호출 합니다. 함수 처리 되 고 SQL_STILL_EXECUTING을 반환. 함수에서 처리를 완료 하는 경우에 다른 코드를 반환 합니다.  
  
 응용 프로그램을 호출할 수 SQL_STILL_EXECUTING을 반환 하는 함수를 호출한 후 **SQLCancel** 함수를 취소 합니다. 취소 요청이 성공 하면 드라이버는 SQL_SUCCESS를 반환 합니다. 이 메시지는 실제로 취소 되었음을; 나타내지 않습니다. 취소 요청이 처리 된 것을 나타냅니다. 또는 함수는 실제로 취소 되어 드라이버에 따라 다릅니다 데이터 원본에 따라 결정 합니다. 응용 프로그램 계속 반환 코드를 SQL_STILL_EXECUTING 없을 때까지 원래 함수를 호출 해야 합니다. 반환 코드는 SQL_ERROR 및 SQLSTATE HY008 함수를 성공적으로 취소 하는 경우 (작업이 취소 됨). 반환 코드는 SQL_SUCCESS 또는 함수에 성공 하면 SQL_SUCCESS_WITH_INFO 또는 SQL_ERROR 및 HY008 이외의 SQLSTATE는 일반적으로 처리를 완료 한 경우 (작업이 취소 됨)는 실패 한 경우.  
  
> [!NOTE]  
>  ODBC 3.5에 대 한 호출 **SQLCancel** 문에서 프로세스가 완료 되 고 되 면 처리 되지 않습니다 **SQLFreeStmt** SQL_CLOSE 옵션을 사용 하지만 전혀 영향을 주지 않습니다. 커서 닫기, 응용 프로그램에서 호출 해야 **SQLCloseCursor**가 아닌 **SQLCancel**합니다.  
  
 비동기 처리에 대 한 자세한 내용은 참조 하세요. [비동기 실행](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)합니다.  
  
## <a name="canceling-functions-that-need-data"></a>데이터를 필요로 하는 함수를 취소 합니다.  
 이후에 **SQLExecute** 하거나 **SQLExecDirect** SQL_NEED_DATA를 반환 합니다. 모든 실행 시 데이터 매개 변수에 대 한 데이터를 보내기 전에 응용 프로그램을 호출할 수 있습니다 **SQLCancel** 문 실행을 취소 합니다. 문이 취소 된 후에 응용 프로그램 호출 수 **SQLExecute** 하거나 **SQLExecDirect** 다시 합니다. 자세한 내용은 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)합니다.  
  
 이후에 **SQLBulkOperations** 하거나 **SQLSetPos** SQL_NEED_DATA를 반환 합니다. 모든 실행 시 데이터 열에 대 한 데이터를 보내기 전에 응용 프로그램을 호출할 수 있습니다 **SQLCancel** 작업을 취소 합니다. 작업이 취소 된 후에 응용 프로그램 호출 수 **SQLBulkOperations** 하거나 **SQLSetPos** 다시 취소 영향을 주지 않습니다 커서 상태 또는 현재 커서 위치입니다. 자세한 내용은 [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md) 하거나 [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)합니다.  
  
## <a name="canceling-functions-executing-on-another-thread"></a>다른 스레드에서 실행 하는 함수를 취소 합니다.  
 다중 스레드 응용 프로그램에서는 응용 프로그램이 다른 스레드에서 실행 하는 함수를 취소할 수 있습니다. 함수를 호출 하 여 응용 프로그램을 취소 하려면 **SQLCancel** 대상 함수로 하지만 다른 스레드에서 사용 된 것과 동일한 문 핸들을 사용 하 여 합니다. 함수를 취소 하는 방법을 드라이버 및 운영 체제에 따라 달라 집니다. 반환 코드를 비동기적으로 실행 되는 함수가 취소와 같이 합니다 **SQLCancel** 여부만 드라이버 요청을 성공적으로 처리 하는지 여부를 나타냅니다. SQL_SUCCESS 또는 sql_error가 반환 될 수 있습니다. 진단 정보 없음이 반환 됩니다. SQL_ERROR 및 SQLSTATE HY008 반환 원래 함수 취소 되 면 (작업이 취소 됨).  
  
 SQL 문이 되 면 실행 될 때 **SQLCancel** 은 문 실행을 취소 하려면 다른 스레드에서 호출 성공 하 고 실행이 가능 하며를 성공적으로 취소 하는 동안 관계 없이 SQL_SUCCESS를 반환 합니다. 이 경우 드라이버 관리자 응용 프로그램이 커서를 사용할 수 없게 되지 않도록를 취소 하 여 문 실행 하 여 열린 커서 닫히도록 가정 합니다.  
  
 스레딩에 대 한 자세한 내용은 참조 하세요. [다중 스레딩](../../../odbc/reference/develop-app/multithreading.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|버퍼 매개 변수 바인딩|[SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|수행 하 고 대량 삽입 또는 업데이트 작업|[SQLBulkOperations 함수](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|비동기적으로 실행 연결 핸들의 또한의 기능에는 함수를 취소 **SQLCancel**합니다.|[SQLCancelHandle 함수](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|SQL 문을 실행합니다.|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문을 실행합니다.|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|문 핸들 해제|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|진단 레코드의 필드 또는 진단 헤더 필드 가져오기|[SQLGetDiagField 함수](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
|진단 데이터 구조체의 여러 필드 가져오기|[SQLGetDiagRec 함수](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|  
|에 대 한 데이터를 보내도록 다음 매개 변수를 반환 합니다.|[SQLParamData 함수](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|실행 시 매개 변수 데이터 전송|[SQLPutData 함수](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|행 집합에서 커서를 놓고, 행 집합에서 데이터 새로 고침, 업데이트 또는 결과 집합의 데이터 삭제|[SQLSetPos 함수](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
