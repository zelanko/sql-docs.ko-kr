---
title: SQLGetEnvAttr 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetEnvAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetEnvAttr
helpviewer_keywords:
- SQLGetEnvAttr function [ODBC]
ms.assetid: 01f4590f-427a-4280-a1c3-18de9f7d86c1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 70fe1ca95f5160f801eaf3528e625116705eda6d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63258836"
---
# <a name="sqlgetenvattr-function"></a>SQLGetEnvAttr 함수
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수 합니다. ISO 92  
  
 **요약**  
 **SQLGetEnvAttr** 환경 특성의 현재 설정을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLGetEnvAttr(  
     SQLHENV        EnvironmentHandle,  
     SQLINTEGER     Attribute,  
     SQLPOINTER     ValuePtr,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>인수  
 *EnvironmentHandle*  
 [입력] 환경 핸들입니다.  
  
 *특성*  
 [입력] 검색할 특성입니다.  
  
 *ValuePtr*  
 [출력] 지정 된 특성의 현재 값을 반환 하는 버퍼에 대 한 포인터 *특성*합니다.  
  
 하는 경우 *ValuePtr* 가 null 인 경우 *StringLengthPtr* 총 바이트 (문자 데이터에 대 한 null 종료 문자 제외)도 돌아갑니다 가리키는버퍼에서반환할사용가능한 *ValuePtr*합니다.  
  
 *BufferLength*  
 [입력] 하는 경우 *ValuePtr* 문자열을 가리키는이 인수 길이 여야 합니다 \* *ValuePtr*합니다. 하는 경우 \* *ValuePtr* 정수 이면 *BufferLength* 무시 됩니다. 하는 경우  *\*ValuePtr* 는 유니코드 문자열 (호출할 때 **SQLGetEnvAttrW**), *BufferLength* 인수 수는 짝수 여야 합니다. 특성 값이 문자열이 없으면 *BufferLength* 사용 되지 않습니다.  
  
 *StringLengthPtr*  
 [출력] (Null 종료 문자를 제외한) 바이트의 총 수를 반환 하는 버퍼에 대 한 포인터를 반환 하려면 사용 가능한  *\*ValuePtr*합니다. 하는 경우 *ValuePtr* 가 null 포인터인 경우 길이 없음이 반환 됩니다. 특성 값은 문자열 하 고 반환할 사용 가능한 바이트 수가 보다 크거나 같음 *BufferLength*에 있는 데이터 \* *ValuePtr* 잘립니다  *BufferLength* null 종료 문자 길이 뺀 값 및 드라이버에 의해 null로 종결 됩니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLGetEnvAttr** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* SQL_의 HANDLE_ENV와 *처리할* 의 *EnvironmentHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLGetEnvAttr** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|반환 되는 데이터 \* *ValuePtr* 되도록 잘렸습니다 *BufferLength* null 종결 문자가 뺀 값입니다. 잘리지 않은 문자열 값의 길이에서 **StringLengthPtr*합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM) **SQL_ATTR_ODBC_VERSION** 를 통해 아직 설정 되지 않은 **SQLSetEnvAttr**합니다. 설정할 필요가 없습니다 **SQL_ATTR_ODBC_VERSION** 사용 하는 경우에 명시적으로 **SQLAllocHandleStd**합니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY092|잘못 된 특성/옵션 식별자입니다.|인수에 지정 된 값 *특성* ODBC 드라이버에서 지 원하는 버전에 올바르지 않습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|인수에 지정 된 값 *특성* ODBC의 버전 드라이버에서 지원 하지만 드라이버에서 지원 되지 ODBC 환경 특성을 잘못 되었습니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)에 해당 하는 드라이버는 *EnvironmentHandle* 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 특성의 목록을 참조 하세요 [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)합니다. 드라이버 관련 환경 특성이 없는 합니다. 하는 경우 *특성* 문자열을 반환 하는 특성을 지정 합니다 *ValuePtr* 문자열 반환할 버퍼에 대 한 포인터 여야 합니다. Null 종료 바이트를 포함 하 여 문자열의 최대 길이 됩니다 *BufferLength* 바이트입니다.  
  
 **SQLGetEnvAttr** 할당 하 고 환경 핸들을 해제 간에 언제 든 호출할 수 있습니다. 모든 환경 특성을 환경에 대 한 응용 프로그램에서 성공적으로 설정 될 때까지 지속 **SQLFreeHandle** 라고 하는 *EnvironmentHandle* 사용 하 여를 *HandleType*SQL_HANDLE_ENV입니다. 둘 이상의 환경 핸들이 ODBC 3에 동시에 할당할 수 있습니다 *.x*합니다. 다른 환경에 할당 된 환경 특성 환경에 영향을 주지 않습니다.  
  
> [!NOTE]
>  SQL_ATTR_OUTPUT_NTS 환경 특성은 표준 호환 응용 프로그램에서 지원 됩니다. 때 **SQLGetEnvAttr** 호출 되는 ODBC 3 *.x* 드라이버 관리자는 항상 SQL_TRUE이이 특성을 반환 합니다. 호출 하 여만 SQL_ATTR_OUTPUT_NTS SQL_TRUE로 설정할 수 있습니다 **SQLSetEnvAttr**합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|연결 특성의 설정을 반환합니다.|[SQLGetConnectAttr 함수](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|반환 문 특성 설정|[SQLGetStmtAttr 함수](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|연결 특성을 설정합니다.|[SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|환경 특성 설정|[SQLSetEnvAttr 함수](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|문 특성 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
