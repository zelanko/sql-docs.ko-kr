---
title: SQLRowCount 함수 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRowCount
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLRowCount
helpviewer_keywords:
- SQLRowCount function [ODBC]
ms.assetid: 61e00a8a-9b3b-45b9-b397-7fe818822416
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2cbca03e7c3e381b803196a1bf7bb227ebeea03b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293373"
---
# <a name="sqlrowcount-function"></a>SQLRowCount 함수(SQLRowCount Function)
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLRowCount는** **UPDATE,** **INSERT**또는 **DELETE** 문의 영향을 받는 행 수를 반환합니다. **SQLBulkOperations에서**SQL_ADD, SQL_UPDATE_BY_BOOKMARK 또는 SQL_DELETE_BY_BOOKMARK 작업; 또는 **SQLSetPos에서**SQL_UPDATE 또는 SQL_DELETE 작업입니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLRowCount(  
      SQLHSTMT   StatementHandle,  
      SQLLEN *   RowCountPtr);  
```  
  
## <a name="arguments"></a>인수  
 *명령문 핸들*  
 [입력] 명령문 핸들입니다.  
  
 *행카운트Ptr*  
 [출력] 행 수를 반환할 버퍼를 가리킵니다. **UPDATE**, **INSERT**및 **DELETE** 명령문, **SQLBulkOperations의**SQL_ADD, SQL_UPDATE_BY_BOOKMARK 및 SQL_DELETE_BY_BOOKMARK 작업의 경우 **및 SQLSetPos의**SQL_UPDATE 또는 SQL_DELETE 작업의 경우 **RowCountPtr에서* 반환되는 값은 요청의 영향을 받는 행 수 또는 영향을 받는 행 수를 사용할 수 없는 경우 -1입니다.  
  
 **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, **SQLSetPos 또는 SQLMoreResults가** 호출되면 진단 데이터 구조의 SQL_DIAG_ROW_COUNT 필드가 행 수로 설정되고 행 수가 구현에 종속된 방식으로 캐시됩니다. **SQLRowCount** 캐시 된 행 개 수 값을 반환 합니다. 캐시된 행 개수 값은 문 핸들이 준비되거나 할당된 상태로 다시 설정되거나 문이 다시 실행되거나 **SQLCloseCursor가** 호출될 때까지 유효합니다. SQL_DIAG_ROW_COUNT 필드가 설정된 이후 함수가 호출된 경우 함수 호출에 의해 SQL_DIAG_ROW_COUNT 필드가 0으로 재설정되므로 **SQLRowCount에서** 반환되는 값은 SQL_DIAG_ROW_COUNT 필드의 값과 다를 수 있습니다.  
  
 다른 명령문 및 함수의 경우 드라이버는 \* *RowCountPtr*에서 반환되는 값을 정의할 수 있습니다. 예를 들어 일부 데이터 원본은 **행을** 가져오기 전에 SELECT 문 또는 카탈로그 함수에서 반환되는 행 수를 반환할 수 있습니다.  
  
> [!NOTE]  
>  많은 데이터 원본은 결과 집합의 행 수를 가져오기 전에 반환할 수 없습니다. 최대 상호 운용성을 위해 응용 프로그램은 이 동작에 의존해서는 안 됩니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLRowCount** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환하는 경우 *SQL_HANDLE_STMT 핸들 유형* 및 *문 핸들*핸들을 사용하는 **SQLGetDiagRec를** 호출하여 연결된 SQLSTATE 값을 가져올 수 있습니다. *Handle* 다음 표에서는 **SQLRowCount에서** 일반적으로 반환되는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. 이 비동기 함수는 **SQLRowCount** 함수가 호출될 때 계속 실행 중이었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *명령문 핸들에* 대해 호출되고 SQL_PARAM_DATA_AVAILABLE 반환되었습니다. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.<br /><br /> (DM) 이 함수는 **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**및 **SQLSetPos를** *호출하기*전에 호출되었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 *함수는 StatementHandle에* 대 한 호출 하 고이 함수를 호출 하는 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *문 핸들에* 대해 호출되고 SQL_NEED_DATA 반환되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle와* 연결된 드라이버는 함수를 지원하지 않습니다.|  
  
## <a name="comments"></a>주석  
 문 핸들에서 실행된 마지막 SQL 문이 **UPDATE,** **INSERT**또는 **DELETE** 문이 아니거나 **SQLBulkOperations에** 대한 이전 호출의 *작업* 인수가 SQL_ADD, SQL_UPDATE_BY_BOOKMARK 또는 SQL_DELETE_BY_BOOKMARK 아니거나 **SQLSetPos에** 대한 이전 호출의 *작업* 인수가 SQL_UPDATE SQL_DELETE 않은 경우 **RowCountPtr의* 값은 드라이버 정의됩니다. 자세한 내용은 [영향을 받는 행 수 확인을](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)참조하십시오.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비된 SQL 문 실행|[SQL실행 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
