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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 31ddab7291807222882050233715d3ad61e25124
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061460"
---
# <a name="sqlgetstmtattr-function"></a>SQLGetStmtAttr 함수
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수 합니다. ISO 92  
  
 **요약**  
 **SQLGetStmtAttr** 문 특성의 현재 설정을 반환 합니다.  
  
> [!NOTE]  
>  자세한 내용은 관리자에 대 한 어떤를 드라이버에 대 한 경우는 ODBC 3이이 함수를를 매핑합니다. *x* 는 ODBC 2를 사용 하 여 응용 프로그램이 작동 합니다. *x* 드라이버를 참조 하세요 [이전 버전과 호환성의 응용 프로그램에 대 한 대체 함수 매핑](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)합니다.  
  
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
 [입력] 문 핸들입니다.  
  
 *특성*  
 [입력] 검색할 특성입니다.  
  
 *ValuePtr*  
 [출력] 에 지정 된 특성의 값을 반환 하는 버퍼에 대 한 포인터 *특성*합니다.  
  
 하는 경우 *ValuePtr* 가 null 인 경우 *StringLengthPtr* 총 바이트 (문자 데이터에 대 한 null 종료 문자 제외)도 돌아갑니다 가리키는버퍼에서반환할사용가능한 *ValuePtr*합니다.  
  
 *BufferLength*  
 [입력] 하는 경우 *특성* 은 ODBC 정의 특성 및 *ValuePtr* 문자열 또는 이진 버퍼를 가리키는,이 인수 길이 여야 \* *ValuePtr*. 하는 경우 *특성* 은 ODBC 정의 특성 및 \* *ValuePtr* 정수 이면 *BufferLength* 무시 됩니다. 값을 반환 하는 경우  *\*ValuePtr* 는 유니코드 문자열 (호출할 때 **SQLGetStmtAttrW**), *BufferLength* 인수 수는 짝수 여야 합니다.  
  
 하는 경우 *특성* 은 드라이버에서 정의 된 특성을 응용 프로그램을 설정 하 여 드라이버 관리자에 특성의 특성을 나타내는 합니다 *BufferLength* 인수. *BufferLength* 다음 값을 가질 수 있습니다.  
  
-   하는 경우  *\*ValuePtr* 문자열에 대 한 포인터 이면 *BufferLength* SQL_NTS 또는 문자열의 길이입니다.  
  
-   하는 경우  *\*ValuePtr* 이진 버퍼에 대 한 포인터 이면 응용 프로그램을 SQL_LEN_BINARY_ATTR의 결과 배치 (*길이*)에서 매크로 *BufferLength*합니다. 에 음수 값이 배치 *BufferLength*합니다.  
  
-   하는 경우  *\*ValuePtr* 문자열 또는 이진 문자열 이외의 값에 대 한 포인터 이면 *BufferLength* SQL_IS_POINTER 값이 있어야 합니다.  
  
-   하는 경우  *\*ValuePtr* 은 고정 길이 데이터 형식에 다음 포함 *BufferLength* SQL_IS_INTEGER 또는 SQL_IS_UINTEGER를 적절 하 게 됩니다.  
  
 *StringLengthPtr*  
 [출력] (Null 종료 문자를 제외한) 바이트의 총 수를 반환 하는 버퍼에 대 한 포인터를 반환 하려면 사용 가능한  *\*ValuePtr*합니다. 하는 경우 *ValuePtr* 가 null 포인터인 경우 길이 없음이 반환 됩니다. 특성 값이 문자열을 반환할 사용 가능한 바이트 수가 보다 크거나 같은 경우 *BufferLength*, 데이터가  *\*ValuePtr* 잘립니다*BufferLength* null 종료 문자 길이 뺀 값 및 드라이버에 의해 null로 종결 됩니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLGetStmtAttr** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* sql _HANDLE_STMT와 *처리할* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLGetStmtAttr** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|반환 되는 데이터  *\*ValuePtr* 되도록 잘렸습니다 *BufferLength* null 종료 문자 길이 뺀 값입니다. 잘리지 않은 문자열 값의 길이에서 **StringLengthPtr*합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|24000|잘못된 커서 상태|인수 *특성* SQL_ATTR_ROW_NUMBER 및 되었거나 커서가 열리지 커서 결과 집합 또는 결과 집합의 끝을 시작 하기 전에 배치 되었습니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 인수의 *MessageText* 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)를 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한 합니다 *StatementHandle*합니다. 이 비동기 함수가 여전히 실행 시기를 **SQLGetStmtAttr** 함수를 호출 했습니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수에 대해 호출 된 합니다 *StatementHandle* 이 함수가 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**를 **SQLExecDirect**를 **SQLBulkOperations**, 또는 **SQLSetPos** 에 대해 호출 된는  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|*(DM) \*ValuePtr* 문자열이 이며 0 보다 작지만 같지 않음 SQL_NTS BufferLength 되었습니다.|  
|HY092|잘못 된 특성/옵션 식별자입니다.|인수에 지정 된 값 *특성* ODBC 드라이버에서 지 원하는 버전에 올바르지 않습니다.|  
|HY109|잘못 된 커서 위치|합니다 *특성* 인수가 SQL_ATTR_ROW_NUMBER 및 행 삭제 하거나 가져올 수 없습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|인수에 지정 된 값 *특성* ODBC의 버전 드라이버에서 지원 되지만 드라이버에서 지원 되지에 대 한 유효한 ODBC 문 특성 되었습니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)에 해당 하는 드라이버는 *StatementHandle* 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 문 특성에 대 한 일반적인 정보를 참조 하세요 [문 특성](../../../odbc/reference/develop-app/statement-attributes.md)합니다.  
  
 에 대 한 호출 **SQLGetStmtAttr** 반환  *\*ValuePtr* 문 특성에 지정 된 변수의 *특성*합니다. 해당 값은 SQLULEN 값 또는 null로 끝나는 문자열에는 일 수 있습니다. 값 SQLULEN value 인 경우 일부 드라이버 하위 32 비트에만 쓸 수 있습니다 또는 16 비트 두고 버퍼의 상위 비트 변경 되지 않습니다. 따라서 응용 프로그램 SQLULEN 버퍼를 사용 하 고이 함수를 호출 하기 전에 값을 0으로 초기화 해야 합니다. 또한 합니다 *BufferLength* 하 고 *StringLengthPtr* 인수가 사용 되지 않습니다. 값이 null로 끝나는 문자열을 응용 프로그램에서 해당 문자열의 최대 길이 지정 하는 합니다 *BufferLength* 인수와 드라이버에서 해당 문자열의 길이 반환 합니다  *\* StringLengthPtr* 버퍼입니다.  
  
 호출 응용 프로그램을 허용 하도록 **SQLGetStmtAttr** ODBC 2를 사용 하 여 작동 합니다. *x* 드라이버에 대 한 호출 **SQLGetStmtAttr** 드라이버 관리자에 매핑된 **SQLGetStmtOption**합니다.  
  
 다음 문 특성은 읽기 전용으로 검색할 수 있도록 **SQLGetStmtAttr**에 설정 되지 않지만 **SQLSetStmtAttr**:  
  
-   SQL_ATTR_IMP_PARAM_DESC  
  
-   SQL_ATTR_IMP_ROW_DESC  
  
-   SQL_ATTR_ROW_NUMBER  
  
 설정 하 고 검색할 수 있는 특성의 목록을 참조 하세요 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|연결 특성의 설정을 반환합니다.|[SQLGetConnectAttr 함수](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|연결 특성을 설정합니다.|[SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|문 특성 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
