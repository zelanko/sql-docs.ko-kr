---
title: SQLGetEnvAttr 함수 | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetEnvAttr
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLGetEnvAttr
helpviewer_keywords:
- SQLGetEnvAttr function [ODBC]
ms.assetid: 01f4590f-427a-4280-a1c3-18de9f7d86c1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0940a5a2c70a7b670ca6a81521759fd08e60461e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68345632"
---
# <a name="sqlgetenvattr-function"></a>SQLGetEnvAttr 함수
**규칙**  
 소개 된 버전: ODBC 3.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLGetEnvAttr** 는 환경 특성의 현재 설정을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLGetEnvAttr(  
     SQLHENV        EnvironmentHandle,  
     SQLINTEGER     Attribute,  
     SQLPOINTER     ValuePtr,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>인수  
 *EnvironmentHandle*  
 입력 환경 핸들.  
  
 *Attribute*  
 입력 검색할 특성입니다.  
  
 *ValuePtr*  
 출력 *특성*으로 지정 된 특성의 현재 값을 반환할 버퍼에 대 한 포인터입니다.  
  
 *Valueptr* 이 NULL 인 경우 *StringLengthPtr* 는 해당 값을 가리키는 버퍼에서 반환 하는 데 사용할 수 있는 총 바이트 수 (문자 데이터의 NULL 종료 문자 제외)를 반환 *합니다.*  
  
 *BufferLength*  
 입력 *Valueptr* 이 문자열을 가리키는 경우이 인수는의 \*길이 여야 합니다. ** \* *Valueptr* 이 정수인 경우 *bufferlength* 는 무시 됩니다. **SQLGetEnvAttrW**를 호출할 때 * \*valueptr* 이 유니코드 문자열이 면 *bufferlength* 인수는 짝수 여야 합니다. 특성 값이 문자열이 아닌 경우 *Bufferlength* 는 사용 되지 않습니다.  
  
 *StringLengthPtr*  
 출력 * \*Valueptr*에서 반환 하는 데 사용할 수 있는 총 바이트 수 (null 종료 문자 제외)를 반환할 버퍼에 대 한 포인터입니다. *Valueptr* 이 null 포인터인 경우 길이가 반환 되지 않습니다. 특성 값이 문자열이 고 반환할 수 있는 바이트 수가 *bufferlength*보다 크거나 같은 경우에는 값 \* *eptr* 의 데이터가 *bufferlength* 에서 null 종료 문자의 길이를 뺀 값으로 잘리고 드라이버에 의해 null로 종료 됩니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetEnvAttr** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 SQL_HANDLE_ENV의 *HandleType* 및 *EnvironmentHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **SQLGetEnvAttr** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01004|문자열 데이터, 오른쪽이 잘렸습니다.|\* *Valueptr* 에서 반환 된 데이터가 *bufferlength* 에서 null 종료 문자를 뺀 값으로 잘렸습니다. 잘리지 않는 문자열 값의 길이는 **StringLengthPtr*에서 반환 됩니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. MessageText 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다. * \**|  
|HY001|메모리 할당 오류|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류|(DM) **SQL_ATTR_ODBC_VERSION** **SQLSetEnvAttr**를 통해 아직 설정 되지 않았습니다. **SQLAllocHandleStd**를 사용 하는 경우 **SQL_ATTR_ODBC_VERSION** 를 명시적으로 설정할 필요가 없습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY092|특성/옵션 식별자가 잘못 되었습니다.|인수 *특성* 에 지정 된 값이 드라이버에서 지원 되는 ODBC 버전에 적합 하지 않습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYC00|선택적 기능이 구현 되지 않음|인수 *특성* 에 지정 된 값이 드라이버에서 지원 되는 odbc 버전에 대 한 올바른 odbc 환경 특성 이지만 드라이버에서 지원 하지 않습니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *EnvironmentHandle* 에 해당 하는 드라이버는 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 특성 목록은 [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)를 참조 하세요. 드라이버별 환경 특성은 없습니다. *특성이* 문자열을 반환 하는 특성을 지정 하는 경우에는 문자열을 반환할 버퍼에 대 한 포인터 *여야 합니다.* Null 종료 바이트를 포함 하는 문자열의 최대 길이는 *bufferlength* 바이트입니다.  
  
 **SQLGetEnvAttr** 는 환경 핸들을 할당 하 고 해제 하는 동안 언제 든 지 호출할 수 있습니다. 환경에 대 한 응용 프로그램에서 설정 하는 모든 환경 특성은 *EnvironmentHandle* SQL_HANDLE_ENV *HandleType* 를 사용 하 여 **sqlfreehandle** 이 호출 될 때까지 지속 됩니다. 두 개 이상의 환경*핸들을 ODBC*3.x에서 동시에 할당할 수 있습니다. 한 환경의 환경 특성은 다른 환경이 할당 될 때 영향을 받지 않습니다.  
  
> [!NOTE]
>  SQL_ATTR_OUTPUT_NTS 환경 특성은 표준 규격 응용 프로그램에서 지원 됩니다. **SQLGetEnvAttr** 가 호출 되 면 ODBC*3.x 드라이버 관리자* 는이 특성에 대 한 SQL_TRUE를 항상 반환 합니다. **SQLSetEnvAttr**에 대 한 호출에 의해서만 SQL_TRUE SQL_ATTR_OUTPUT_NTS 설정할 수 있습니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|연결 특성의 설정 반환|[SQLGetConnectAttr 함수(SQLGetConnectAttr Function)](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|문 특성의 설정 반환|[SQLGetStmtAttr 함수](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|연결 특성 설정|[SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|환경 특성 설정|[SQLSetEnvAttr 함수](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|문 특성 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
