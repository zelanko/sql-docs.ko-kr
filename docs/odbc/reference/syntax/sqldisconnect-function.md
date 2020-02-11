---
title: SQLDisconnect 함수 | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDisconnect
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLDisconnect
helpviewer_keywords:
- SQLDisconnect function [ODBC]
ms.assetid: 9e84a58e-db48-4821-a0cd-5c711fcbe36b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 788ca2eb7cf37314eb7d5386a23f17123f9ccaff
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68343014"
---
# <a name="sqldisconnect-function"></a>SQLDisconnect 함수
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **Sqldisconnect** 는 특정 연결 핸들과 연결 된 연결을 닫습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLDisconnect(  
     SQLHDBC     ConnectionHandle);  
```  
  
## <a name="arguments"></a>인수  
 *ConnectionHandle*  
 [Input] 연결 핸들입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE 또는 SQL_STILL_EXECUTING입니다.  
  
## <a name="diagnostics"></a>진단  
 **Sqldisconnect** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 *HandleType* SQL_HANDLE_DBC의 및 *ConnectionHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 **Sqldisconnect** 에서 일반적으로 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01002|연결 끊기 오류|연결을 끊는 동안 오류가 발생 했습니다. 그러나 연결 끊기에 성공 했습니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|08003|연결이 열려 있지 않음|(DM) 인수 *ConnectionHandle* 에 지정 된 연결이 열려 있지 않습니다.|  
|25000|잘못된 트랜잭션 상태|*ConnectionHandle*인수에 지정 된 연결에 트랜잭션 프로세스가 있습니다. 트랜잭션은 활성 상태로 유지 됩니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. MessageText 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다. * \**|  
|HY001|메모리 할당 오류|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업 취소됨|*ConnectionHandle*에 대해 비동기 처리를 사용 하도록 설정 했습니다. 함수가 호출 되었고 *ConnectionHandle*에서 [sqlcancelhandle 함수](../../../odbc/reference/syntax/sqlcancelhandle-function.md) 를 실행 하기 전에이 함수가 호출 되었습니다. 그런 다음 *ConnectionHandle*에서 함수를 다시 호출 했습니다.<br /><br /> 함수가 호출 되었고 **Sqlcancelhandle** 실행이 완료 되기 전에 다중 스레드 응용 프로그램의 다른 스레드에서 *ConnectionHandle* 에 대해 호출 되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) *ConnectionHandle* 와 연결 된 *StatementHandle* 에 대해 비동기적으로 실행 되는 함수가 호출 되었으며 **sqldisconnect** 가 호출 될 때 계속 실행 중입니다.<br /><br /> (DM) *ConnectionHandle* 에 대해 비동기적으로 실행 되는 함수 (이 함수 아님)가 호출 되었으며이 함수가 호출 될 때 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 는 *ConnectionHandle* 와 연결 된 *StatementHandle* 에 대해 호출 되 고 SQL_NEED_DATA 반환 됩니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되어 연결이 여전히 활성 상태입니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *ConnectionHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드에서는 폴링을 사용할 수 없습니다.|알림 모델을 사용할 때마다 폴링은 사용 하지 않도록 설정 됩니다.|  
|IM018|이 핸들에서 이전 비동기 작업을 완료 하기 위해 **SQLCompleteAsync** 가 호출 되지 않았습니다.|핸들에 대 한 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드가 설정 된 경우에는 핸들에 대해 **SQLCompleteAsync** 를 호출 하 여 사후 처리를 수행 하 고 작업을 완료 해야 합니다.|  
  
## <a name="comments"></a>주석  
 **SQLBrowseConnect** 가 SQL_NEED_DATA 반환 하 고 다른 반환 코드를 반환 하기 전에 응용 프로그램에서 **sqldisconnect** 를 호출 하는 경우 드라이버는 연결 검색 프로세스를 취소 하 고 연결 되지 않은 상태로의 연결을 반환 합니다.  
  
 연결 핸들과 연결 된 불완전 한 트랜잭션이 있는 동안 응용 프로그램이 **Sqldisconnect** 를 호출 하는 경우 드라이버는 SQLSTATE 25000 (잘못 된 트랜잭션 상태)을 반환 하 여 트랜잭션이 변경 되지 않고 연결이 열려 있음을 나타냅니다. 불완전 한 트랜잭션은 **Sqlendtran**을 사용 하 여 커밋되거나 롤백되지 않은 트랜잭션입니다.  
  
 응용 프로그램에서 연결에 연결 된 모든 문을 해제 하기 전에 **Sqldisconnect** 를 호출 하는 경우, 데이터 원본에서 연결을 성공적으로 끊은 후 해당 문과 연결에 명시적으로 할당 된 모든 설명자를 해제 합니다. 그러나 연결과 관련 된 하나 이상의 문이 비동기적으로 실행 중인 경우 **Sqldisconnect** 는 HY010 (함수 시퀀스 오류)의 SQLSTATE 값을 사용 하 여 SQL_ERROR 반환 합니다. 또한 연결이 일시 중단 된 상태 이거나 **Sqlcancelhandle**에서 **sqldisconnect** 가 성공적으로 취소 된 경우 **sqldisconnect** 를 사용 하면 연결 된 모든 문 및 연결에 명시적으로 할당 된 모든 설명자를 해제할 수 있습니다.  
  
 응용 프로그램에서 **Sqldisconnect**를 사용 하는 방법에 대 한 자세한 내용은 [데이터 원본 또는 드라이버에서 연결 끊기](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)를 참조 하세요.  
  
## <a name="disconnecting-from-a-pooled-connection"></a>풀링된 연결에서 연결 끊기  
 공유 환경에 연결 풀링을 사용 하는 경우 응용 프로그램이 해당 환경에서 연결을 통해 **Sqldisconnect** 를 호출 하면 연결이 연결 풀로 반환 되 고 동일한 공유 환경을 사용 하는 다른 구성 요소에서 계속 사용할 수 있습니다.  
  
## <a name="code-example"></a>코드 예  
 [샘플 ODBC 프로그램](../../../odbc/reference/sample-odbc-program.md), [SQLBrowseConnect 함수](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)및 [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)를 참조 하세요.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|핸들 할당|[SQLAllocHandle 함수](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|데이터 원본에 연결|[SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|연결 문자열 또는 대화 상자를 사용 하 여 데이터 원본에 연결|[SQLDriverConnect 함수(SQLDriverConnect Function)](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|커밋 또는 롤백 작업 실행|[SQLEndTran 함수(SQLEndTran Function)](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|연결 핸들 해제|[SQLFreeConnect 함수](../../../odbc/reference/syntax/sqlfreeconnect-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
