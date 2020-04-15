---
title: SQLDisconnect 함수 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a5ea73919fbe90719d881fb43108ab1934933708
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301153"
---
# <a name="sqldisconnect-function"></a>SQLDisconnect 함수
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLDisconnect는** 특정 연결 핸들과 연결된 연결을 닫습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLDisconnect(  
     SQLHDBC     ConnectionHandle);  
```  
  
## <a name="arguments"></a>인수  
 *연결 핸들*  
 [Input] 연결 핸들입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE 또는 SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>진단  
 **SQLDisconnect가** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환하는 경우 *핸들 유형* SQL_HANDLE_DBC 및 *연결 핸들*핸들을 사용하는 *Handle* **SQLGetDiagRec를** 호출하여 연결된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 **SQLDisconnect에서** 일반적으로 반환되는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01002|연결 오류|연결을 끊는 동안 오류가 발생했습니다. 그러나 연결 끊김이 성공했습니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|08003|연결이 열려 있지 않음|(DM) 인수 *연결핸들에* 지정된 연결이 열려 있지 않았습니다.|  
|25000|잘못된 트랜잭션 상태|인수 ConnectionHandle 에 의해 지정 된 연결에 프로세스에 *트랜잭션이*있었다 . 트랜잭션은 활성 상태로 유지됩니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY08|작업 취소됨|*연결 핸들*에 대해 비동기 처리가 활성화되었습니다. 함수가 호출되었고 [SQLCancelHandle 함수를](../../../odbc/reference/syntax/sqlcancelhandle-function.md) 실행하기 전에 *연결 핸들*에서 호출되었습니다. 그런 다음 *연결이*핸들 에서 함수를 다시 호출했습니다.<br /><br /> 함수가 호출되었고 **SQLCancelHandle** 실행이 완료되기 전에 다중 스레드 응용 프로그램의 다른 스레드에서 *ConnectionHandle에서* 호출되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) 비동기적으로 실행 되는 *함수는 연결 핸들과* 연결 된 *StatementHandle에* 대 한 호출 하 고 **SQLDisconnect** 호출 될 때 여전히 실행 중 이었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 함수 (이 하나) *연결 핸들에* 대 한 호출 하 고이 함수를 호출 될 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *연결 핸들과* 연결된 *문핸들을* 호출하고 SQL_NEED_DATA 반환했습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 시간이 만료되었으며 연결이 계속 활성화되어 있습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *연결 핸들과* 연결된 드라이버가 기능을 지원하지 않습니다.|  
|IM017|비동기 알림 모드에서 폴링이 비활성화됨|알림 모델을 사용할 때마다 폴링이 비활성화됩니다.|  
|IM018|**SQLCompleteAsync이** 핸들에 이전 비동기 작업을 완료 하기 위해 호출 되지 않았습니다.|핸들의 이전 함수 호출이 SQL_STILL_EXECUTING 반환하고 알림 모드가 활성화된 경우 **SQLCompleteAsync를** 호출하여 사후 처리를 수행하여 작업을 완료해야 합니다.|  
  
## <a name="comments"></a>주석  
 응용 프로그램이 **SQLBrowseConnect가** SQL_NEED_DATA 반환하고 다른 반환 코드를 반환하기 전에 **SQLDisconnect를** 호출하면 드라이버는 연결 검색 프로세스를 취소하고 연결되지 않은 상태로 연결을 반환합니다.  
  
 응용 프로그램이 연결 핸들과 연결된 불완전한 트랜잭션이 있는 동안 **SQLDisconnect를** 호출하는 경우 드라이버는 트랜잭션이 변경되지 않고 연결이 열려 있음을 나타내는 SQLSTATE 25000(잘못된 트랜잭션 상태)을 반환합니다. 불완전한 트랜잭션은 **SQLEndTran**.  
  
 응용 프로그램이 연결과 관련된 모든 문을 해제하기 전에 **SQLDisconnect를** 호출하면 드라이버는 데이터 원본에서 성공적으로 연결을 끊은 후 해당 명령문과 연결에 명시적으로 할당된 모든 설명자가 해제됩니다. 그러나 연결과 연결된 명령문 중 하나 이상이 여전히 비동기적으로 실행 중인 경우 **SQLDisconnect는** HY010(함수 시퀀스 오류)의 SQLSTATE 값으로 SQL_ERROR 반환합니다. 또한 **SQLDisconnect는** 연결이 일시 중단된 상태이거나 **SQLDisconnect가** **SQLCancelHandle**에 의해 성공적으로 취소된 경우 연결에 명시적으로 할당된 모든 설명자와 모든 설명자가 해제됩니다.  
  
 응용 프로그램에서 **SQLDisconnect를**사용하는 방법에 대한 자세한 내용은 [데이터 원본 또는 드라이버의 연결 끊김을](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)참조하십시오.  
  
## <a name="disconnecting-from-a-pooled-connection"></a>풀링된 연결에서 연결 끊기  
 공유 환경에 대해 연결 풀링을 사용하도록 설정하고 응용 프로그램이 해당 환경의 연결에서 **SQLDisconnect를** 호출하는 경우 연결은 연결 풀로 반환되고 동일한 공유 환경을 사용하는 다른 구성 요소에서 계속 사용할 수 있습니다.  
  
## <a name="code-example"></a>코드 예  
 [샘플 ODBC 프로그램,](../../../odbc/reference/sample-odbc-program.md) [SQLBrowseConnect 함수](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)및 [SQLConnect 함수를](../../../odbc/reference/syntax/sqlconnect-function.md)참조하십시오.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|핸들 할당|[SQLAllocHandle 함수](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|데이터 원본에 연결|[SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|연결 문자열 또는 대화 상자를 사용하여 데이터 원본에 연결|[SQLDriverConnect 함수](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|커밋 또는 롤백 작업 실행|[SQLEndTran 함수(SQLEndTran Function)](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|연결 핸들 해제|[SQLFreeConnect 함수](../../../odbc/reference/syntax/sqlfreeconnect-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
