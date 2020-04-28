---
title: SQLGetStmtAttr 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetStmtAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetStmtAttr
helpviewer_keywords:
- SQLGetStmtAttr function [ODBC]
ms.assetid: e321d460-e997-4527-aee6-207cf5a498e9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 89e7c75b412a6358806017102915989a8370dd43
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303307"
---
# <a name="sqlgetstmtattr-function"></a>SQLGetStmtAttr 함수
**규칙**  
 소개 된 버전: ODBC 3.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLGetStmtAttr** 는 문 특성의 현재 설정을 반환 합니다.  
  
> [!NOTE]  
>  ODBC 3의 경우 드라이버 관리자가이 기능을에 매핑하는 방법에 대 한 자세한 내용을 확인 하십시오. *x* 응용 프로그램에서 ODBC 2를 사용 하 고 있습니다. *x* 드라이버 [응용 프로그램의 이전 버전과의 호환성을 위해 대체 함수 매핑](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)을 참조 하세요.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLGetStmtAttr(  
     SQLHSTMT        StatementHandle,  
     SQLINTEGER      Attribute,  
     SQLPOINTER      ValuePtr,  
     SQLINTEGER      BufferLength,  
     SQLINTEGER *    StringLengthPtr);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 입력 문 핸들입니다.  
  
 *특성도*  
 입력 검색할 특성입니다.  
  
 *ValuePtr*  
 출력 *특성*에 지정 된 특성의 값을 반환할 버퍼에 대 한 포인터입니다.  
  
 *Valueptr* 이 NULL 인 경우 *StringLengthPtr* 는 해당 값을 가리키는 버퍼에서 반환 하는 데 사용할 수 있는 총 바이트 수 (문자 데이터의 NULL 종료 문자 제외)를 반환 *합니다.*  
  
 *BufferLength*  
 입력 *특성이* ODBC에 정의 된 *특성이 고,* 이상 문자열이 문자열 또는 이진 버퍼를 가리키는 경우이 인수는이 인수의 길이 \*여야 *합니다.* *특성이* ODBC 정의 특성이 고 \*값 *eptr* 이 정수 이면 *bufferlength* 는 무시 됩니다. **SQLGetStmtAttrW**를 호출할 때 값 * \*eptr* 에서 반환 된 값이 유니코드 문자열이 면 *bufferlength* 인수는 짝수 여야 합니다.  
  
 *특성이* 드라이버 정의 특성인 경우 응용 프로그램은 *bufferlength* 인수를 설정 하 여 특성의 특성을 드라이버 관리자에 게 표시 합니다. *Bufferlength* 에는 다음 값을 사용할 수 있습니다.  
  
-   * \*Valueptr* 이 문자열에 대 한 포인터인 경우 *bufferlength* 는 문자열 또는 SQL_NTS의 길이입니다.  
  
-   * \*Valueptr* 이 이진 버퍼에 대 한 포인터인 경우 응용 프로그램은 SQL_LEN_BINARY_ATTR (*길이*) 매크로의 결과를 *bufferlength*로 배치 합니다. 그러면 음수 값이 *Bufferlength*에 배치 됩니다.  
  
-   * \*Valueptr* 이 문자열 또는 이진 문자열이 아닌 값에 대 한 포인터인 경우 *bufferlength* 의 값은 SQL_IS_POINTER 이어야 합니다.  
  
-   * \*Valueptr* 에 고정 길이 데이터 형식이 포함 된 경우에는 *bufferlength* 가 SQL_IS_INTEGER 또는 SQL_IS_UINTEGER입니다.  
  
 *StringLengthPtr*  
 출력 * \*Valueptr*에서 반환 하는 데 사용할 수 있는 총 바이트 수 (null 종료 문자 제외)를 반환할 버퍼에 대 한 포인터입니다. *Valueptr* 이 null 포인터인 경우 길이가 반환 되지 않습니다. 특성 값이 문자열이 고 반환할 수 있는 바이트 수가 *bufferlength*보다 크거나 같은 경우에는 값 * \*eptr* 의 데이터가 *bufferlength* 에서 null 종료 문자의 길이를 뺀 값으로 잘리고 드라이버에 의해 null로 종료 됩니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetStmtAttr** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 SQL_HANDLE_STMT의 *HandleType* 및 *StatementHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **SQLGetStmtAttr** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01004|문자열 데이터, 오른쪽이 잘렸습니다.|* \*Valueptr* 에서 반환 된 데이터가 *bufferlength* 에서 null 종료 문자의 길이를 뺀 값으로 잘렸습니다. 잘리지 않는 문자열 값의 길이는 **StringLengthPtr*에서 반환 됩니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|24000|잘못된 커서 상태|인수 *특성이* SQL_ATTR_ROW_NUMBER 되었거나 커서가 열려 있지 않거나 결과 집합의 시작 앞 이나 결과 집합의 끝에 커서를 배치 했습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. *MessageText* 인수에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. **SQLGetStmtAttr** 함수가 호출 될 때이 비동기 함수는 계속 실행 중입니다.<br /><br /> (DM) *StatementHandle* 에 대해 비동기적으로 실행 되는 함수가 호출 되었으며이 함수가 호출 될 때 여전히 실행 되 고 있습니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 가 *StatementHandle* 에 대해 호출 되 고 SQL_NEED_DATA 반환 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|*DM () \** 은 문자열이 고, bufferlength는 0 보다 작지만 SQL_NTS와 같지 않습니다.|  
|HY092|특성/옵션 식별자가 잘못 되었습니다.|인수 *특성* 에 지정 된 값이 드라이버에서 지원 되는 ODBC 버전에 적합 하지 않습니다.|  
|HY109|커서 위치가 잘못 되었습니다.|*특성* 인수가 SQL_ATTR_ROW_NUMBER 되었으며 행이 삭제 되었거나 가져올 수 없습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYC00|선택적 기능이 구현 되지 않음|인수 *특성* 에 지정 된 값이 드라이버에서 지원 되는 odbc 버전에 대 한 올바른 odbc 문 특성 이지만 드라이버에서 지원 하지 않습니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *StatementHandle* 에 해당 하는 드라이버는 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 문 특성에 대 한 일반 정보는 [문 특성](../../../odbc/reference/develop-app/statement-attributes.md)을 참조 하세요.  
  
 **SQLGetStmtAttr** 에 대 한 호출은 *특성*에 지정 된 문 특성의 * \*값을 지정 하는* 값을 반환 합니다. 이 값은 SQLULEN 값 또는 null로 끝나는 문자열 일 수 있습니다. 값이 SQLULEN 값인 경우 일부 드라이버는 버퍼의 하위 32 비트 또는 16 비트만 쓸 수 있고 고차 비트는 변경 되지 않은 상태로 둘 수 있습니다. 따라서 응용 프로그램은이 함수를 호출 하기 전에 SQLULEN의 버퍼를 사용 하 고 값을 0으로 초기화 해야 합니다. 또한 *Bufferlength* 및 *StringLengthPtr* 인수는 사용 되지 않습니다. 값이 null로 끝나는 문자열인 경우 응용 프로그램은 *bufferlength* 인수에서 해당 문자열의 최대 길이를 지정 하 고 드라이버는 * \*StringLengthPtr* 버퍼에서 해당 문자열의 길이를 반환 합니다.  
  
 **SQLGetStmtAttr** 를 호출 하는 응용 프로그램에서 ODBC 2를 사용할 수 있도록 허용 합니다. *x* 드라이버는 **SQLGetStmtAttr** 에 대 한 호출이 드라이버 관리자에서 **SQLGetStmtOption**로 매핑됩니다.  
  
 다음 문 특성은 읽기 전용 이므로 **SQLGetStmtAttr**에서 검색할 수 있지만 **SQLSetStmtAttr**에 의해 설정 되지 않습니다.  
  
-   SQL_ATTR_IMP_PARAM_DESC  
  
-   SQL_ATTR_IMP_ROW_DESC  
  
-   SQL_ATTR_ROW_NUMBER  
  
 설정 하 고 검색할 수 있는 특성 목록은 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)를 참조 하세요.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|연결 특성의 설정 반환|[SQLGetConnectAttr 함수(SQLGetConnectAttr Function)](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|연결 특성 설정|[SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|문 특성 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
