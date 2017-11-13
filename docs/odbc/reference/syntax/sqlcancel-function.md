---
title: "SQLCancel 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 079a1ac7467348472c501c4dcb055d2cef8e9306
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlcancel-function"></a>SQLCancel 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLCancel** 문에서 처리를 취소 합니다.  
  
 연결 또는 명령문에 대 한 처리를 취소 하려면 사용 하 여 [SQLCancelHandle 함수](../../../odbc/reference/syntax/sqlcancelhandle-function.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLCancel(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 [입력] 문 핸들입니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLCancel** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 관련된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 와 *HandleType* SQL_의 HANDLE_STMT 및 *처리* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLCancel** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|오류|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) 인수에  *\*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류입니다.|DM ()는 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한는 *StatementHandle*합니다. 이 비동기 함수 계속 실행 될 때는 **SQLCancel** 함수를 호출 했습니다.<br /><br /> DM ()는 비동기 작업 연관 된 연결 핸들에 진행 중 이므로 실패 했습니다. 작업을 취소 *StatementHandle*합니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY018|취소 요청을 거부 했습니다.|서버 관리자 취소 요청을 거부 합니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)와 관련 된 드라이버의 *StatementHandle* 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>설명  
 **SQLCancel** 다음과 같은 유형의 명령문에 대 한 처리를 취소할 수 있습니다.  
  
-   문에서 비동기적으로 실행 되는 함수입니다.  
  
-   데이터를 요구 하는 문에서 작동 합니다.  
  
-   다른 스레드에서 문이 실행 되는 함수입니다.  
  
 Odbc 2. *x*응용 프로그램을 호출 하는 경우, **SQLCancel** 문을 없는 처리로 수행 되는 경우 **SQLCancel** 것과 동일한 결과가 **SQLFreeStmt** SQL_CLOSE 옵션입니다. 이 문제는 완전성을 위해서만 정의 되며 응용 프로그램 호출 해야 **SQLFreeStmt** 또는 **SQLCloseCursor** 를 커서를 닫습니다.  
  
 때 **SQLCancel** 함수, 데이터 요구를 취소 하는 함수에 의해 게시 되는 진단 레코드 선택 취소 하는 문에 대 한 문 또는 함수에서 비동기적으로 실행을 취소 하기 위해 호출 하 고 **SQLCancel 그러나**  자체 진단 레코드에 게시 때 **SQLCancel** 문에서 다른 스레드에서 실행 되는 함수를 취소 하려면 지워지지 않습니다 진단 호출 되는 레코드 함수 및 취소 하지 자체 진단 레코드를 게시 합니다.  
  
## <a name="canceling-asynchronous-processing"></a>비동기 처리를 취소합니다.  
 응용 프로그램 함수를 비동기적으로 호출 후 반복 해 서 처리를 완료 되었는지 여부를 결정 하는 함수를 호출 합니다. 함수를 계속 처리 하는 경우 SQL_STILL_EXECUTING을 반환 합니다. 함수 처리를 완료 하는 경우에 다른 코드를 반환 합니다.  
  
 응용 프로그램을 호출할 수 SQL_STILL_EXECUTING을 반환 하는 함수를 호출한 후 **SQLCancel** 함수를 취소 합니다. 취소 요청에 성공 하면 드라이버는 SQL_SUCCESS를 반환 합니다. 이 메시지는 함수가 실제로 취소 된; 나타내지 않습니다. 취소 요청을 처리 하는 것을 나타냅니다. 시기 또는 함수는 실제로 취소가 드라이버 종속 하 고 데이터 소스에 따라 다릅니다. 응용 프로그램 계속 반환 코드를 SQL_STILL_EXECUTING 없을 때까지 원래 함수를 호출 해야 합니다. 반환 코드는 SQL_ERROR 및 SQLSTATE HY008 함수 성공적으로 취소 되 면 (작업이 취소 됨). 반환 코드는 SQL_SUCCESS 또는 함수에 성공 하면 SQL_SUCCESS_WITH_INFO 또는 SQL_ERROR와 HY008 이외의 SQLSTATE 함수는 일반적으로 처리를 완료 한 경우 (작업이 취소 됨) 함수가 실패 한 경우.  
  
> [!NOTE]  
>  ODBC 3.5에 대 한 호출에서 **SQLCancel** 문에서 프로세스가 완료 되 고 되 면으로 처리 되지 않습니다는 **SQLFreeStmt** SQL_CLOSE 옵션을 사용 하지만 포함 전혀 영향을 주지 않습니다. 커서 닫기, 응용 프로그램 호출 해야 **SQLCloseCursor**이 아니라 **SQLCancel**합니다.  
  
 비동기 처리에 대 한 자세한 내용은 참조 [비동기 실행](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)합니다.  
  
## <a name="canceling-functions-that-need-data"></a>데이터를 필요로 하는 함수를 취소 합니다.  
 후 **SQLExecute** 또는 **SQLExecDirect** SQL_NEED_DATA를 반환 합니다. 응용 프로그램을 호출할 수 있습니다 모든 실행 시 데이터 매개 변수에 대 한 데이터를 보내기 전에 **SQLCancel** 문 실행을 취소 합니다. 응용 프로그램을 호출할 수는 문이 취소 된 후 **SQLExecute** 또는 **SQLExecDirect** 다시 합니다. 자세한 내용은 참조 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)합니다.  
  
 후 **SQLBulkOperations** 또는 **SQLSetPos** SQL_NEED_DATA를 반환 합니다. 응용 프로그램을 호출할 수 있습니다 모든 실행 시 데이터 열에 대 한 데이터를 보내기 전에 **SQLCancel** 작업을 취소 하 합니다. 작업이 취소 된 후에 응용 프로그램이 호출할 수 **SQLBulkOperations** 또는 **SQLSetPos** 다시; 취소 영향을 주지 않습니다 커서 상태 또는 현재 커서 위치입니다. 자세한 내용은 참조 [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md) 또는 [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)합니다.  
  
## <a name="canceling-functions-executing-on-another-thread"></a>함수에서 다른 스레드로 실행을 취소 합니다.  
 다중 스레드 응용 프로그램을 응용 프로그램에서 다른 스레드로 실행 되는 함수를 취소할 수 있습니다. 함수를 호출 하 여 응용 프로그램을 취소 하려면 **SQLCancel** 대상 함수에 의해 하지만 다른 스레드에서 사용 된 것과 동일한 문 핸들을 포함 합니다. 함수는 취소 방법 드라이버 및 운영 체제에 따라 달라 집니다. 취소의 반환 코드는 비동기적으로 실행 하는 함수에서와 같이 **SQLCancel** 드라이버 요청을 성공적으로 처리 하는지 여부를을 나타냅니다. SQL_SUCCESS 또는 SQL_ERROR를 반환 될 수 있습니다. 진단 정보 없음이 반환 됩니다. SQL_ERROR 및 SQLSTATE HY008 반환 원래 함수 취소 되는 경우 (작업이 취소 됨).  
  
 SQL 문이 되 고 있으면 때 실행 **SQLCancel** 은 문 실행을 취소 하려면 다른 스레드에서 호출, 실행에 성공 하려면에 대 한 가능한 하며를 성공적으로 취소 하는 동안 관계 없이 SQL_SUCCESS를 반환 합니다. 이 경우 드라이버 관리자는 응용 프로그램이 커서를 사용 하려면 수 문 실행 하 여 열린 커서에서는 취소 하 여 닫혀 가정 합니다.  
  
 스레딩에 대 한 자세한 내용은 참조 [다중 스레딩](../../../odbc/reference/develop-app/multithreading.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|버퍼는 매개 변수 바인딩|[SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|수행 된 대량 삽입 또는 업데이트 작업|[SQLBulkOperations 함수](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|비동기적으로 실행 중인 연결 핸들에 또한의 기능에는 함수를 취소 **SQLCancel**합니다.|[SQLCancelHandle 함수](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문을 실행합니다.|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|문 핸들 해제|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|진단 레코드의 필드 또는 진단 헤더의 필드|[SQLGetDiagField 함수](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
|진단 데이터 구조의 여러 필드 가져오기|[SQLGetDiagRec 함수](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|  
|에 대 한 데이터를 보내는 다음 매개 변수를 반환 합니다.|[SQLParamData 함수](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|실행 시 매개 변수 데이터 보내기|[SQLPutData 함수](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|행 집합에서 커서를 놓고, 행 집합에서 데이터 새로 고침 또는 업데이트 또는 결과 집합의 데이터를 삭제 합니다.|[SQLSetPos 함수](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)

