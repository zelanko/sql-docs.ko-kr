---
title: SQLRowCount 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 65683174ee5b48a8f7b861f3ba838334d70025ae
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68345440"
---
# <a name="sqlrowcount-function"></a>SQLRowCount 함수(SQLRowCount Function)
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **Sqlrowcount** 는 **UPDATE**, **INSERT**또는 **DELETE** 문의 영향을 받는 행 수를 반환 합니다. **SQLBulkOperations**의 SQL_ADD, SQL_UPDATE_BY_BOOKMARK 또는 SQL_DELETE_BY_BOOKMARK 작업 또는 **SQLSetPos**의 SQL_UPDATE 또는 SQL_DELETE 작업입니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLRowCount(  
      SQLHSTMT   StatementHandle,  
      SQLLEN *   RowCountPtr);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 입력 문 핸들입니다.  
  
 *함수의 rowcountptr*  
 출력 행 개수를 반환할 버퍼를 가리킵니다. **업데이트**, **삽입**및 **삭제** 문의 경우 **SQLBulkOperations**의 SQL_ADD, SQL_UPDATE_BY_BOOKMARK 및 SQL_DELETE_BY_BOOKMARK 작업에 대해, **SQLSetPos**의 SQL_UPDATE 또는 SQL_DELETE 작업의 경우 **rowcountptr* 에서 반환 되는 값은 요청의 영향을 받는 행 수 또는 영향을 받는 행 수를 사용할 수 없는 경우-1입니다.  
  
 **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**, **SQLSetPos 또는 SQLMoreResults** 가 호출 되 면 진단 데이터 구조의 SQL_DIAG_ROW_COUNT 필드가 행 개수로 설정 되 고, 행 개수는 구현에 따라 달라 지는 방식으로 캐시 됩니다. **Sqlrowcount** 는 캐시 된 행 개수 값을 반환 합니다. 캐시 된 행 개수 값은 문 핸들이 준비 됨 또는 할당 된 상태로 다시 설정 되거나 문이 명령을 다시 실행 되거나 **SQLCloseCursor** 가 호출 될 때까지 유효 합니다. SQL_DIAG_ROW_COUNT 필드가 설정 된 후 함수가 호출 된 경우 함수 호출로 인해 SQL_DIAG_ROW_COUNT 필드가 0으로 다시 설정 되므로 **Sqlrowcount** 에서 반환 된 값이 SQL_DIAG_ROW_COUNT 필드의 값과 다를 수 있습니다.  
  
 다른 문과 함수의 경우 드라이버는 \* *rowcountptr*에서 반환 되는 값을 정의할 수 있습니다. 예를 들어 일부 데이터 원본은 행을 페치 하기 전에 **SELECT** 문이나 카탈로그 함수에서 반환 된 행 수를 반환할 수 있습니다.  
  
> [!NOTE]  
>  많은 데이터 원본에서 결과 집합의 행 수를 인출 하기 전에 반환할 수 없습니다. 상호 운용성을 최대화 하기 위해 응용 프로그램은이 동작에 의존해 서는 안 됩니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **Sqlrowcount** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환할 때 SQL_HANDLE_STMT의 *HandleType* 및 *StatementHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 **Sqlrowcount** 에서 일반적으로 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각각에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. MessageText 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다. * \**|  
|HY001|메모리 할당 오류|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. 이 비동기 함수는 **Sqlrowcount** 함수가 호출 될 때 실행 되 고 있습니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 *StatementHandle* 에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM) 함수는 **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 *StatementHandle*에 대 한 **SQLSetPos** 를 호출 하기 전에 호출 되었습니다.<br /><br /> (DM) *StatementHandle* 에 대해 비동기적으로 실행 되는 함수가 호출 되었으며이 함수가 호출 될 때 여전히 실행 되 고 있습니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 가 *StatementHandle* 에 대해 호출 되 고 SQL_NEED_DATA 반환 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *StatementHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 문 핸들에서 실행 된 마지막 SQL 문이 **UPDATE**, **INSERT**또는 **DELETE** 문이 아니거나, **SQLBulkOperations** 에 대 한 이전 호출의 *작업* 인수가 SQL_ADD, SQL_UPDATE_BY_BOOKMARK 또는 SQL_DELETE_BY_BOOKMARK 되지 않았거나, **SQLSetPos** 에 대 한 이전 호출의 *작업* 인수가 SQL_UPDATE 또는 SQL_DELETE이 아닌 경우 **rowcountptr* 의 값은 드라이버에 정의 됩니다. 자세한 내용은 [영향을 받는 행 수 확인](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)을 참조 하세요.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문 실행|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
