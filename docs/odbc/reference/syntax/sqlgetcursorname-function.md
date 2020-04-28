---
title: SQLGetCursorName 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetCursorName
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetCursorName
helpviewer_keywords:
- SQLGetCursorName function [ODBC]
ms.assetid: e6e92199-7bb6-447c-8987-049a4c6ce05d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d3ac65dc07897ddc789ee03b06b1bc1f71d37c3c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81285551"
---
# <a name="sqlgetcursorname-function"></a>SQLGetCursorName 함수(SQLGetCursorName Function)
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLGetCursorName** 는 지정 된 문과 연결 된 커서 이름을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLGetCursorName(  
     SQLHSTMT        StatementHandle,  
     SQLCHAR *       CursorName,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   NameLengthPtr);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 입력 문 핸들입니다.  
  
 *CursorName*  
 출력 커서 이름을 반환할 버퍼에 대 한 포인터입니다.  
  
 *CursorName* 가 NULL 인 경우 *NameLengthPtr* 는 *CursorName*가 가리키는 버퍼에서 반환 하는 데 사용할 수 있는 문자 데이터의 NULL 종료 문자를 제외한 총 문자 수를 반환 합니다.  
  
 *BufferLength*  
 입력 \* *CursorName*의 길이 (문자)입니다. * \*CursorName* 의 값이 유니코드 문자열이 면 ( **SQLGetCursorNameW**호출 시) *bufferlength* 인수는 짝수 여야 합니다.  
  
 *NameLengthPtr*  
 출력 \* *CursorName*에서 반환 하는 데 사용할 수 있는 총 문자 수 (null 종결 문자 제외)를 반환할 메모리에 대 한 포인터입니다. 반환할 수 있는 문자 수가 *bufferlength*보다 크거나 같으면 \* *CursorName* 의 커서 이름이 *bufferlength* 에서 null 종료 문자의 길이를 뺀 값으로 잘립니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetCursorName** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환할 때 SQL_HANDLE_STMT의 *HandleType* 및 *StatementHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **SQLGetCursorName** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01004|문자열 데이터, 오른쪽이 잘렸습니다.|버퍼 \* *CursorName* 는 전체 커서 이름을 반환할 만큼 크지 않으므로 커서 이름이 잘렸습니다. 잘린 커서 이름의 길이는 **NameLengthPtr*에서 반환 됩니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. MessageText 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다. * \**|  
|HY001|메모리 할당 오류|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. **SQLGetCursorName** 함수가 호출 될 때이 비동기 함수는 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 *StatementHandle* 에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM) *StatementHandle* 에 대해 비동기적으로 실행 되는 함수가 호출 되었으며이 함수가 호출 될 때 여전히 실행 되 고 있습니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 가 *StatementHandle* 에 대해 호출 되 고 SQL_NEED_DATA 반환 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY015|사용할 수 있는 커서 이름이 없습니다.|(DM) 드라이버가 ODBC*2.x 드라이버이* 고, 문에 열린 커서가 없고, **SQLSetCursorName**로 설정 된 커서 이름이 없습니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|(DM) 인수 *Bufferlength* 에 지정 된 값이 0 보다 작은 경우|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *StatementHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 커서 이름은 위치 지정 update 및 delete 문에서만 사용 됩니다. 예를 들어 **update** _table-name_ ... **WHERE CURRENT OF** _cursor name_). 자세한 내용은 [위치 지정 Update 및 Delete 문](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)을 참조 하세요. 응용 프로그램에서 **SQLSetCursorName** 를 호출 하 여 커서 이름을 정의 하지 않는 경우 드라이버는 이름을 생성 합니다. 이 이름은 SQL_CUR 문자로 시작 합니다.  
  
> [!NOTE]
>  ODBC*2.x에서 열린*커서가 없고 **SQLSetCursorName**에 대 한 호출로 이름이 설정 되지 않은 경우 **SQLGETCURSORNAME** 에 대 한 호출은 SQLSTATE HY015 (사용할 수 있는 커서 이름 없음)를 반환 합니다. ODBC*3.x에서는 더*이상 true가 아닙니다. **SQLGetCursorName** 가 호출 되는 시기와 관계 없이 드라이버는 커서 이름을 반환 합니다.  
  
 **SQLGetCursorName** 는 이름이 명시적으로 만들어졌는지 아니면 암시적으로 생성 되었는지 여부에 상관 없이 커서 이름을 반환 합니다. **SQLSetCursorName** 를 호출 하지 않으면 암시적으로 커서 이름이 생성 됩니다. 커서가 할당 된 상태 이거나 준비 된 상태에 있는 경우 **SQLSetCursorName** 를 호출 하 여 문에 커서의 이름을 바꿀 수 있습니다.  
  
 명시적으로 설정 되거나 암시적으로 설정 되는 커서 이름은 *HandleType* 가 SQL_HANDLE_STMT 인 **sqlfreehandle** 을 사용 하 여 연결 된 *StatementHandle* 이 삭제 될 때까지 설정 된 상태로 유지 됩니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문 실행|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|실행을 위한 문 준비|[SQLPrepare 함수](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|커서 이름 설정|[SQLSetCursorName 함수](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
