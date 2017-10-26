---
title: "SQLGetEnvAttr 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a7e353d41c1065f8d65a70c6633901ef22547a61
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetenvattr-function"></a>SQLGetEnvAttr 함수
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수: ISO 92  
  
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
  
 *Attribute*  
 [입력] 검색할 특성입니다.  
  
 *ValuePtr*  
 [출력] 에 의해 지정 된 특성의 현재 값을 버퍼에 대 한 포인터 *특성*합니다.  
  
 경우 *ValuePtr* 이 NULL 이면 *StringLengthPtr* 바이트 (문자 데이터에 대 한 null 종결 문자 제외)의 총 수를 반환 여전히 가리키는버퍼에서반환할수* ValuePtr*합니다.  
  
 *BufferLength*  
 [입력] 경우 *ValuePtr* 문자열을 가리키는이 인수 길이 여야 \* *ValuePtr*합니다. 경우 \* *ValuePtr* 정수 이면 *BufferLength* 는 무시 됩니다. 경우 * \*ValuePtr* 는 유니코드 문자열 (호출할 때 **SQLGetEnvAttrW**), *BufferLength* 인수 수는 짝수 여야 합니다. 특성 값이 문자열이 없으면 *BufferLength* 는 사용 되지 않습니다.  
  
 *StringLengthPtr*  
 [출력] 바이트 (null 종결 문자 제외)의 총 수를 반환 하는 버퍼에 대 한 포인터를 반환 하려면 사용 가능한 * \*ValuePtr*합니다. 경우 *ValuePtr* 가 null 포인터 이면 길이가 반환 됩니다. 특성 값은 문자열 및 반환할 수 있는 바이트 수는 보다 크거나 경우 *BufferLength*, 데이터에 \* *ValuePtr* 잘립니다 * BufferLength* null 종결 문자 길이 만큼 뺀 길이로 고 드라이버에서 null로 종료 합니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLGetEnvAttr** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 관련된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 와 *HandleType* SQL_의 HANDLE_ENV 및 *처리* 의 *EnvironmentHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLGetEnvAttr** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|오류|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|반환 되는 데이터 \* *ValuePtr* 되도록 잘렸습니다 *BufferLength* null 종결 문자가 뺀 값입니다. 잘리지 않은 문자열 값의 길이에서 **StringLengthPtr*합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에 * \*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM) **SQL_ATTR_ODBC_VERSION** 통해 아직 설정 되지 않은 **SQLSetEnvAttr**합니다. 설정할 필요가 없습니다 **SQL_ATTR_ODBC_VERSION** 사용 하는 경우에 명시적으로 **SQLAllocHandleStd**합니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY092|잘못 된 특성/옵션 식별자|인수에 대해 지정 된 값 *특성* ODBC 드라이버에서 지 원하는 버전에 대해 올바르지 않습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|인수에 대해 지정 된 값 *특성* ODBC의 버전 드라이버에서 지원 되지만 드라이버에서 지원 하지 않아 유효한 ODBC 환경 특성을 했습니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)에 해당 하는 드라이버는 *EnvironmentHandle* 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>설명  
 특성 목록이 참조 [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)합니다. 드라이버 관련 환경 특성이 없는 합니다. 경우 *특성* 지정는 문자열을 반환 하는 특성 *ValuePtr* 문자열을 반환 하는 버퍼에 대 한 포인터 여야 합니다. Null 종료 바이트를 포함 하 여 문자열의 최대 길이 됩니다 *BufferLength* 바이트입니다.  
  
 **SQLGetEnvAttr** 언제 든 지 할당 및 환경 핸들의 해제 간의 호출할 수 있습니다. 모든 환경 특성 환경에 대 한 응용 프로그램에 의해 성공적으로 설정 될 때까지 지속 **SQLFreeHandle** 라고 하는 *EnvironmentHandle* 와 *HandleType*SQL_HANDLE_ENV입니다. ODBC 3에서 개 이상의 환경 핸들을 동시에 할당 될 수*.x*합니다. 다른 환경에서 할당 한 환경에 대 한 환경 특성 영향을 주지 않습니다.  
  
> [!NOTE]  
>  SQL_ATTR_OUTPUT_NTS 환경 특성은 표준 호환 응용 프로그램에서 지원 됩니다. 때 **SQLGetEnvAttr** 호출 되는 ODBC 3*.x* 드라이버 관리자에서이 특성에 대 한이 SQL_TRUE을 항상 반환 합니다. 에 대 한 호출에 의해서만 SQL_ATTR_OUTPUT_NTS SQL_TRUE로 설정할 수 있습니다 **SQLSetEnvAttr**합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|연결 특성의 설정은 반환|[SQLGetConnectAttr 함수](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|문 특성 설정을 반환합니다.|[SQLGetStmtAttr 함수](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|연결 특성을 설정합니다.|[SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|환경 특성 설정|[SQLSetEnvAttr 함수](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|문 특성 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)

