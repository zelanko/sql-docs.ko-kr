---
title: SQLGetConnectAttr 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetConnectOption
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConnectAttr
helpviewer_keywords:
- SQLGetConnectAttr function [ODBC]
ms.assetid: 2cb4ffa8-19d3-4664-8c2f-6682cdcc3f33
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 06c158c49c0ce175204bc9738a4f4136db7fe344
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68006217"
---
# <a name="sqlgetconnectattr-function"></a>SQLGetConnectAttr 함수(SQLGetConnectAttr Function)
**규칙**  
 소개 된 버전: ODBC 3.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLGetConnectAttr** 는 연결 특성의 현재 설정을 반환 합니다.  
  
> [!NOTE]
>  ODBC*2.x 응용 프로그램이* odbc*2.x 드라이버를 사용할 때 드라이버 관리자* 가이 기능을에 매핑하는 방법에 대 한 자세한 내용은 [응용 프로그램의 이전 버전과의 호환성을 위한 대체 함수 매핑](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)을 참조 하세요.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLGetConnectAttr(  
     SQLHDBC        ConnectionHandle,  
     SQLINTEGER     Attribute,  
     SQLPOINTER     ValuePtr,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>인수  
 *ConnectionHandle*  
 [Input] 연결 핸들입니다.  
  
 *Attribute*  
 입력 검색할 특성입니다.  
  
 *ValuePtr*  
 출력 *특성*으로 지정 된 특성의 현재 값을 반환할 메모리에 대 한 포인터입니다. 정수 형식 특성의 경우 일부 드라이버는 버퍼의 하위 32 비트 또는 16 비트만 쓸 수 있고 고차 비트는 변경 되지 않은 상태로 둘 수 있습니다. 따라서 응용 프로그램은이 함수를 호출 하기 전에 SQLULEN의 버퍼를 사용 하 고 값을 0으로 초기화 해야 합니다.  
  
 *Valueptr* 이 NULL 인 경우 *StringLengthPtr* 는 해당 값을 가리키는 버퍼에서 반환 하는 데 사용할 수 있는 총 바이트 수 (문자 데이터의 NULL 종료 문자 제외)를 반환 *합니다.*  
  
 *BufferLength*  
 입력 *특성이* ODBC에 정의 된 *특성이 고,* 이상 문자열이 문자열 또는 이진 버퍼를 가리키는 경우이 인수는이 인수의 길이 \*여야 *합니다.* *특성이* ODBC 정의 특성이 고 \*값 *eptr* 이 정수 이면 *bufferlength* 는 무시 됩니다. **SQLGetConnectAttrW**를 호출할 때 인수 * \*값이 유니코드* 문자열이 면 *bufferlength* 인수는 짝수 여야 합니다.  
  
 *특성이* 드라이버 정의 특성인 경우 응용 프로그램은 *bufferlength* 인수를 설정 하 여 특성의 특성을 드라이버 관리자에 게 표시 합니다. *Bufferlength* 에는 다음 값을 사용할 수 있습니다.  
  
-   * \*Valueptr* 이 문자열에 대 한 포인터인 경우 *bufferlength* 는 문자열의 길이입니다.  
  
-   * \*Valueptr* 이 이진 버퍼에 대 한 포인터인 경우 응용 프로그램은 SQL_LEN_BINARY_ATTR (*길이*) 매크로의 결과를 *bufferlength*로 배치 합니다. 그러면 음수 값이 *Bufferlength*에 배치 됩니다.  
  
-   * \*Valueptr* 이 문자열 또는 이진 문자열이 아닌 값에 대 한 포인터인 경우 *bufferlength* 의 값은 SQL_IS_POINTER 이어야 합니다.  
  
-   * \*Valueptr* 에 고정 길이 데이터 형식이 포함 된 경우 *bufferlength* 는 SQL_IS_INTEGER 또는 SQL_IS_UINTEGER입니다.  
  
 *StringLengthPtr*  
 출력 \* *Valueptr*에서 반환 하는 데 사용할 수 있는 총 바이트 수 (null 종료 문자 제외)를 반환할 버퍼에 대 한 포인터입니다. \* *Valueptr* 이 null 포인터인 경우 길이가 반환 되지 않습니다. 특성 값이 문자열이 고 반환할 수 있는 바이트 수가 *버퍼 길이* 에서 null 종료 문자의 길이를 뺀 값 보다 큰 경우, 값 * \*eptr* 의 데이터는 *bufferlength* 에서 null 종료 문자의 길이를 뺀 값으로 잘리고 드라이버에 의해 null로 종료 됩니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetConnectAttr** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 SQLGetDiagRec의 SQL_HANDLE_DBC *HandleType* 및 *ConnectionHandle* *핸들* 을 사용 하 여 **** 를 호출 함으로써 진단 데이터 구조에서 연결 된 SQLSTATE 값을 가져올 수 있습니다. 다음 표에서는 일반적으로 **SQLGetConnectAttr** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01004|문자열 데이터, 오른쪽이 잘렸습니다.|\* *Valueptr* 에서 반환 된 데이터가 *bufferlength* 에서 null 종료 문자의 길이를 뺀 값으로 잘렸습니다. 잘리지 않는 문자열 값의 길이는 **StringLengthPtr*에서 반환 됩니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|08003|연결이 열려 있지 않음|(DM) 열린 연결을 지정 해야 하는 *특성* 값입니다.|  
|08S01|통신 연결 오류|드라이버가 연결 된 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. **SQLGetDiagField** 의 인수 *MessageText* 진단 데이터 구조에서 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버가 실행 또는 함수의 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류|(DM) **SQLBrowseConnect** 가 *ConnectionHandle* 에 대해 호출 되 고 SQL_NEED_DATA 반환 되었습니다. 이 함수는 **SQLBrowseConnect** 가 SQL_SUCCESS_WITH_INFO 또는 SQL_SUCCESS을 반환 하기 전에 호출 되었습니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 *ConnectionHandle* 에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|( * \*DM)는 문자열 이며* bufferlength는 0 보다 작지만 SQL_NTS와 같지 않습니다.|  
|HY092|특성/옵션 식별자가 잘못 되었습니다.|인수 *특성* 에 지정 된 값이 드라이버에서 지원 되는 ODBC 버전에 적합 하지 않습니다.|  
|HY114|드라이버가 연결 수준의 비동기 함수 실행을 지원 하지 않습니다.|(DM) 비동기 연결 작업을 지원 하지 않는 드라이버에 대 한 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE를 사용 하 여 비동기 함수 실행을 사용 하도록 응용 프로그램을 시도 했습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYC00|선택적 기능이 구현 되지 않음|인수 *특성* 에 지정 된 값이 드라이버에서 지원 되는 odbc 버전에 대 한 올바른 odbc 연결 특성 이지만 드라이버에서 지원 하지 않습니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *ConnectionHandle* 에 해당 하는 드라이버는 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 연결 특성에 대 한 일반적인 내용은 [연결 특성](../../../odbc/reference/develop-app/connection-attributes.md)을 참조 하세요.  
  
 설정할 수 있는 특성 목록은 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)를 참조 하세요. *특성* 에서 문자열을 반환 하는 *특성을 지정* 하는 경우에는 문자열에 대 한 버퍼에 대 한 포인터 여야 합니다. Null 종료 문자를 포함 하 여 반환 된 문자열의 최대 길이는 *bufferlength* 바이트입니다.  
  
 특성에 따라 응용 프로그램은 **SQLGetConnectAttr**를 호출 하기 전에 연결을 설정할 필요가 없습니다. 그러나 **SQLGetConnectAttr** 가 호출 되 고 지정 된 특성에 기본값이 없고 **SQLSetConnectAttr**에 대 한 이전 호출로 설정 되지 않은 경우 **SQLGetConnectAttr** 는 SQL_NO_DATA을 반환 합니다.  
  
 *특성이* TRACE 또는 SQL_ATTR_ tracefile SQL_ATTR_ 경우 *ConnectionHandle* 는 유효 하지 않아도 되며 **SQLGetConnectAttr** 은 *ConnectionHandle* 가 잘못 된 경우에는 SQL_ERROR 또는 SQL_INVALID_HANDLE을 반환 하지 않습니다. 이러한 특성은 모든 연결에 적용 됩니다. 다른 인수가 잘못 된 경우 **SQLGetConnectAttr** 에서 SQL_ERROR 또는 SQL_INVALID_HANDLE을 반환 합니다.  
  
 응용 프로그램에서 **SQLSetConnectAttr**를 사용 하 여 문 특성을 설정할 수 있지만 응용 프로그램은 **SQLGetConnectAttr** 를 사용 하 여 문 특성 값을 검색할 수 없습니다. 문 특성의 설정을 검색 하려면 **SQLGetStmtAttr** 를 호출 해야 합니다.  
  
 **SQLGetConnectAttr** 에 대 한 호출로 SQL_ATTR_AUTO_IPD 및 SQL_ATTR_CONNECTION_DEAD 연결 특성을 모두 반환할 수 있지만 **SQLSetConnectAttr**를 호출 하 여 설정할 수는 없습니다.  
  
> [!NOTE]  
>  **SQLGetConnectAttr**에 대 한 비동기 지원은 없습니다. **SQLGetConnectAttr**를 구현 하는 경우 드라이버는 서버에서 정보를 보내거나 요청 하는 횟수를 최소화 하 여 성능을 향상 시킬 수 있습니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|문 특성의 설정 반환|[SQLGetStmtAttr 함수](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|연결 특성 설정|[SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|환경 특성 설정|[SQLSetEnvAttr 함수](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|문 특성 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
