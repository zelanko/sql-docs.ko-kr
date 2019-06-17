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
manager: craigg
ms.openlocfilehash: 7051c94e4883c57daab4d5706feb073323e1c371
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65538033"
---
# <a name="sqlgetconnectattr-function"></a>SQLGetConnectAttr 함수(SQLGetConnectAttr Function)
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수 합니다. ISO 92  
  
 **요약**  
 **SQLGetConnectAttr** 연결 특성의 현재 설정을 반환 합니다.  
  
> [!NOTE]
>  새로운 드라이버 관리자는이 함수를 경우 맵을 ODBC 3 대 한 자세한 내용은 *.x* 는 ODBC 2를 사용 하 여 응용 프로그램이 작동 *.x* 드라이버를 참조 하세요. [뒤로 대 한 대체 함수 매핑 응용 프로그램의 호환성](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)합니다.  
  
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
  
 *특성*  
 [입력] 검색할 특성입니다.  
  
 *ValuePtr*  
 [출력] 로 지정 된 특성의 현재 값을 반환할 메모리에 대 한 포인터 *특성*합니다. 정수 형식 특성에 대 한 일부 드라이버 하위 32 비트에만 쓸 수 있습니다 또는 16 비트 두고 버퍼의 상위 비트 변경 되지 않습니다. 따라서 응용 프로그램 SQLULEN 버퍼를 사용 하 고이 함수를 호출 하기 전에 값을 0으로 초기화 해야 합니다.  
  
 하는 경우 *ValuePtr* 가 null 인 경우 *StringLengthPtr* 총 바이트 (문자 데이터에 대 한 null 종료 문자 제외)도 돌아갑니다 가리키는버퍼에서반환할사용가능한 *ValuePtr*합니다.  
  
 *BufferLength*  
 [입력] 하는 경우 *특성* 은 ODBC 정의 특성 및 *ValuePtr* 문자열 또는 이진 버퍼를 가리키는,이 인수 길이 여야 \* *ValuePtr*. 하는 경우 *특성* 은 ODBC 정의 특성 및 \* *ValuePtr* 정수 이면 *BufferLength* 무시 됩니다. 경우 값  *\*ValuePtr* 는 유니코드 문자열 (호출할 때 **SQLGetConnectAttrW**), *BufferLength* 인수 수는 짝수 여야 합니다.  
  
 하는 경우 *특성* 은 드라이버에서 정의 된 특성을 응용 프로그램을 설정 하 여 드라이버 관리자에 특성의 특성을 나타내는 합니다 *BufferLength* 인수. *BufferLength* 다음 값을 가질 수 있습니다.  
  
-   하는 경우  *\*ValuePtr* 문자열로 포인터가 *BufferLength* 문자열의 길이입니다.  
  
-   하는 경우  *\*ValuePtr* 결과인 이진 버퍼는 응용 프로그램 위치에 대 한 포인터를 SQL_LEN_BINARY_ATTR (*길이*)에서 매크로 *BufferLength*합니다. 에 음수 값이 배치 *BufferLength*합니다.  
  
-   하는 경우  *\*ValuePtr* 문자열 또는 이진 문자열 이외의 값에 대 한 포인터 *BufferLength* SQL_IS_POINTER 값이 있어야 합니다.  
  
-   하는 경우  *\*ValuePtr* 고정 길이 데이터 형식을 포함 *BufferLength* SQL_IS_INTEGER 또는 SQL_IS_UINTEGER를 적절 하 게 됩니다.  
  
 *StringLengthPtr*  
 [출력] (Null 종료 문자를 제외한) 바이트의 총 수를 반환 하는 버퍼에 대 한 포인터를 반환 하려면 사용 가능한 \* *ValuePtr*합니다. 하는 경우 \* *ValuePtr* 가 null 포인터인 경우 길이 없음이 반환 됩니다. 특성 값은 문자열 경우 반환할 사용 가능한 바이트 수가 보다 크면 *BufferLength* 의 데이터를 null 종료 문자 길이 뺀 값  *\*ValuePtr*잘립니다 *BufferLength* null 종료 문자 길이 뺀 값 및 드라이버에 의해 null로 종결 됩니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLGetConnectAttr** 를 호출 하 여 진단 데이터 구조에서 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 가져올 수 있습니다 **SQLGetDiagRec** 를사용하여*HandleType* SQL_HANDLE_DBC의 및는 *처리할* 의 *ConnectionHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLGetConnectAttr** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 앞 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 . 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|반환 되는 데이터 \* *ValuePtr* 되도록 잘렸습니다 *BufferLength* null 종료 문자 길이 뺀 값입니다. 잘리지 않은 문자열 값의 길이에서 **StringLengthPtr*합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08003|연결이 열려 있지 않습니다.|(DM)는 *특성* 에 대해 열린 연결에 필요한 값이 지정 되었습니다.|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버는 연결 된 데이터 원본 간의 통신 링크 하지 못했습니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 진단 데이터 구조에서 인수에 의해 반환 된 오류 메시지 *MessageText* 에 **SQLGetDiagField** 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 실행 또는 완료 함수를 지원 하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM) **SQLBrowseConnect** 에 대해 호출 된 합니다 *ConnectionHandle* SQL_NEED_DATA를 반환 합니다. 하기 전에이 함수를 호출한 **SQLBrowseConnect** SQL_SUCCESS_WITH_INFO 또는 관계 없이 SQL_SUCCESS를 반환 합니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대해 호출 된 합니다 *ConnectionHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|(DM)  *\*ValuePtr* 문자열이 이며 0 보다 작지만 같지 않음 SQL_NTS BufferLength 되었습니다.|  
|HY092|잘못 된 특성/옵션 식별자입니다.|인수에 지정 된 값 *특성* ODBC 드라이버에서 지 원하는 버전에 올바르지 않습니다.|  
|HY114|드라이버는 연결 수준 비동기 함수 실행을 지원 하지 않습니다.|(DM) 응용 프로그램 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 사용 하 여 비동기 연결 작업을 지원 하지 않는 드라이버에 대 한 비동기 함수 실행을 사용 하도록 설정 하려고 합니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|인수에 지정 된 값 *특성* ODBC의 버전 드라이버에서 지원 되지만 드라이버에서 지원 되지에 대 한 유효한 ODBC 연결 특성을 했습니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)에 해당 하는 드라이버는 *ConnectionHandle* 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 연결 특성에 대 한 일반적인 정보를 참조 하세요 [연결 특성](../../../odbc/reference/develop-app/connection-attributes.md)합니다.  
  
 설정할 수 있는 특성의 목록을 참조 하세요 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)합니다. 있는지를 확인할 수 있습니다 *특성* 문자열을 반환 하는 특성을 지정 합니다 *ValuePtr* 문자열 버퍼에 대 한 포인터 여야 합니다. Null 종료 문자를 포함 하 여 반환된 된 문자열의 최대 길이 됩니다 *BufferLength* 바이트입니다.  
  
 특성에 따라 응용 프로그램 되지 않은 호출 하기 전에 연결할 **SQLGetConnectAttr**합니다. 그러나 경우 **SQLGetConnectAttr** 이라고 지정된 된 특성 기본값 없고 이전 호출에서 설정 되지 않은 하 고 **SQLSetConnectAttr**, **SQLGetConnectAttr**SQL_NO_DATA를 반환 합니다.  
  
 하는 경우 *특성* SQL_ATTR_ 추적 또는 SQL_ATTR_ TRACEFILE *ConnectionHandle* 유효 하지 않아도 및 **SQLGetConnectAttr** SQL_ 또는 SQL_ERROR를 반환 하지 것입니다 INVALID_HANDLE 경우 *ConnectionHandle* 올바르지 않습니다. 이러한 특성은 모든 연결에 적용 됩니다. **SQLGetConnectAttr** 다른 인수가 유효 하지 않을 경우 SQL_ERROR 또는 SQL_INVALID_HANDLE 반환 합니다.  
  
 응용 프로그램 사용 하 여 문 특성을 설정할 수 있지만 **SQLSetConnectAttr**, 응용 프로그램에서 사용할 수 없습니다 **SQLGetConnectAttr** 문 특성을 검색할 값; 호출 해야  **SQLGetStmtAttr** 문 특성 설정을 검색 하기.  
  
 연결 특성 SQL_ATTR_CONNECTION_DEAD와 SQL_ATTR_AUTO_IPD를 호출 하 여 반환할 수 있습니다 **SQLGetConnectAttr** 를 호출 하 여 설정할 수 없습니다 **SQLSetConnectAttr**합니다.  
  
> [!NOTE]  
>  에 대 한 비동기 지원 되지 않습니다 **SQLGetConnectAttr**합니다. 구현 하는 경우 **SQLGetConnectAttr**, 드라이버 정보 전송 또는 서버에서 요청 하는 횟수를 최소화 하 여 성능을 향상 시킬 수 있습니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|반환 문 특성 설정|[SQLGetStmtAttr 함수](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|연결 특성을 설정합니다.|[SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|환경 특성 설정|[SQLSetEnvAttr 함수](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|문 특성 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
