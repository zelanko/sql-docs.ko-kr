---
title: SQLGetDescField 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDescField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDescField
helpviewer_keywords:
- SQLGetDescField function [ODBC]
ms.assetid: f09ff660-1e4a-4370-be85-90d4da0487d3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cdf2990056c297d217248543812e347b61d3486d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103810"
---
# <a name="sqlgetdescfield-function"></a>SQLGetDescField 함수(SQLGetDescField Function)
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수 합니다. ISO 92  
  
 **요약**  
 **SQLGetDescField** 설명자 레코드의 단일 필드의 값을 현재 설정을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLGetDescField(  
     SQLHDESC        DescriptorHandle,  
     SQLSMALLINT     RecNumber,  
     SQLSMALLINT     FieldIdentifier,  
     SQLPOINTER      ValuePtr,  
     SQLINTEGER      BufferLength,  
     SQLINTEGER *    StringLengthPtr);  
```  
  
## <a name="arguments"></a>인수  
 *DescriptorHandle*  
 [입력] 설명자 핸들입니다.  
  
 *RecNumber*  
 [입력] 응용 프로그램 정보를 검색 하는 설명자 레코드를 나타냅니다. 0 책갈피 레코드 중 레코드 번호를 사용 하 여 0, 설명자 레코드 번호가 매겨집니다. 경우는 *FieldIdentifier* 인수는 헤더 필드를 나타냅니다 *RecNumber* 무시 됩니다. 하는 경우 *RecNumber* 되었지만 SQL_DESC_COUNT 보다 작거나 같은 행에 열 또는 매개 변수에 대 한 호출에 대 한 데이터가 없습니다 **SQLGetDescField** 필드의 기본값을 반환 합니다. (자세한 내용은 "설명자 필드의 초기화"를 참조 하세요 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
 *FieldIdentifier*  
 [입력] 값이 반환 되는 설명자 필드를 나타냅니다. 자세한 내용은 참조는 "*FieldIdentifier* 인수" 섹션 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)합니다.  
  
 *ValuePtr*  
 [출력] 설명자 정보를 반환 하는 버퍼에 대 한 포인터입니다. 데이터 형식 값에 따라 달라 집니다 *FieldIdentifier*합니다.  
  
 하는 경우 *ValuePtr* 정수 형식이, SQLULEN 버퍼를 사용 하는 응용 프로그램 및 일부 드라이버가이 함수를 호출 하기 전에 값을 0으로 초기화 될 수 있습니다만 하위 32 비트 또는 16 비트는 버퍼의 쓰는 상위 비트를 유지 변경 되지 않습니다.  
  
 하는 경우 *ValuePtr* 가 null 인 경우 *StringLengthPtr* 총 바이트 (문자 데이터에 대 한 null 종료 문자 제외)도 돌아갑니다 가리키는버퍼에서반환할사용가능한 *ValuePtr*합니다.  
  
 *BufferLength*  
 [입력] 경우 *FieldIdentifier* 은 ODBC 정의 된 필드와 *ValuePtr* 문자열 또는 이진 버퍼를 가리키는,이 인수 길이 여야 \* *ValuePtr*. 경우 *FieldIdentifier* 은 ODBC 정의 된 필드와 \* *ValuePtr* 정수 이면 *BufferLength* 무시 됩니다. 경우 값  *\*ValuePtr* 유니코드 데이터 형식입니다 (호출할 때 **SQLGetDescFieldW**), *BufferLength* 인수 수는 짝수 여야 합니다.  
  
 하는 경우 *FieldIdentifier* 드라이버에서 정의 된 필드는 응용 프로그램을 설정 하 여 드라이버 관리자에 필드의 특성을 나타내는 합니다 *BufferLength* 인수. *BufferLength* 다음 값을 가질 수 있습니다.  
  
-   하는 경우  *\*ValuePtr* 문자열에 대 한 포인터 이면 *BufferLength* SQL_NTS 또는 문자열의 길이입니다.  
  
-   하는 경우  *\*ValuePtr* 이진 버퍼에 대 한 포인터 이면 응용 프로그램을 SQL_LEN_BINARY_ATTR의 결과 배치 (*길이*)에서 매크로 *BufferLength*합니다. 에 음수 값이 배치 *BufferLength*합니다.  
  
-   하는 경우  *\*ValuePtr* 문자열 또는 이진 문자열 이외의 값에 대 한 포인터 이면 *BufferLength* SQL_IS_POINTER 값이 있어야 합니다.  
  
-   하는 경우  *\*ValuePtr* 은 다음에 고정 길이 데이터 형식인 *BufferLength* 되었거나 SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT, SQL_IS_USMALLINT를 적절 하 게 합니다.  
  
 *StringLengthPtr*  
 [출력] 바이트 (null 종료 문자에 필요한 바이트 수가 제외)의 총 수를 반환 하는 버퍼에 대 한 포인터를 반환 하려면 사용할 수 있습니다 **ValuePtr*합니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR에서 SQL_NO_DATA를 또는 SQL_INVALID_HANDLE 합니다.  
  
 경우 SQL_NO_DATA가 반환 *RecNumber* 현재 설명자 레코드 개수 보다 큽니다.  
  
 경우 SQL_NO_DATA가 반환 *DescriptorHandle* IRD 핸들 및 문을 상태인 준비 또는 실행 되었지만 연결 된 열린 커서가 없습니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLGetDescField** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* 의 호출 및 *처리할* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLGetDescField** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|버퍼 \* *ValuePtr* 필드 잘렸습니다. 전체 설명자 필드를 반환할 수 없습니다. 잘리지 않은 설명자 필드의 길이에서 **StringLengthPtr*합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|07009|잘못 된 설명자 인덱스입니다.|(DM)는 *RecNumber* 인수가 0, SQL_ATTR_USE_BOOKMARK 문 특성 된 SQL_UB_OFF, 및 *DescriptorHandle* 인수가 IRD 핸들을 합니다. (이 오류 반환할 수 있습니다를 명시적으로 할당 된 설명자에 대 한 설명자를 문 핸들을 사용 하 여 연결 된 경우에.)<br /><br /> 합니다 *FieldIdentifier* 인수가 레코드 필드를 *RecNumber* 인수가 0, 및 *DescriptorHandle* 인수가 IPD 핸들을 합니다.<br /><br /> 합니다 *RecNumber* 인수가 0 보다 작습니다.|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버는 연결 된 데이터 원본 간의 통신 링크 하지 못했습니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY007|연결 된 문이 준비 되지 않았습니다.|*DescriptorHandle* 연관 된를 *StatementHandle* 는 IRD 및 연결된 된 문 핸들 했습니다 된 준비 또는 실행 되지 않습니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM) *DescriptorHandle* 연관 된를 *StatementHandle* 는 비동기적으로 실행 중인 (이 없는 항목)를 호출한 함수와이 함수가 호출 되었을 때 계속 실행에 대 한 합니다.<br /><br /> (DM) *DescriptorHandle* 연관 된를 *StatementHandle* 입니다 **SQLExecute**를 **SQLExecDirect**,  **SQLBulkOperations**, 또는 **SQLSetPos** 호출 되 고 SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한 합니다 *DescriptorHandle*합니다. 이 비동기 함수가 여전히 실행 시기를 **SQLGetDescField** 함수를 호출 했습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY021|일관성이 없는 설명자 정보|SQL_DESC_TYPE 및 값을 SQL_DESC_DATETIME_INTERVAL_CODE 필드 (Apd 또는 ARDs)에 유효한 ODBC SQL 형식, (IPDs)에 대 한 유효한 드라이버별 SQL 형식 또는 유효한 ODBC C 형식을 형성 하지 않습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|(DM)  *\*ValuePtr* 된 문자열을 및 *BufferLength* 가 0 보다 작습니다.|  
|HY091|잘못 된 설명자 필드 식별자입니다.|*FieldIdentifier* ODBC 정의 필드를 없었으며 구현 시 정의 된 값이 없습니다.<br /><br /> *FieldIdentifier* 에 대해 정의 된 합니다 *DescriptorHandle*합니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 드라이버를 사용 하 여 연결 합니다 *DescriptorHandle* 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 응용 프로그램에서 호출할 수 있습니다 **SQLGetDescField** 설명자 레코드의 단일 필드의 값을 반환 합니다. 에 대 한 호출 **SQLGetDescField** 헤더 필드, 레코드 필드 및 책갈피 필드를 포함 하 여 모든 설명자 형식에서 모든 필드의 설정을 반환할 수 있습니다. 응용 프로그램 반복 호출 하 여 동일 하거나 다른 설명자에 있는 임의의 순서로 여러 필드의 설정을 가져올 수 있습니다 **SQLGetDescField**합니다. **SQLGetDescField** 드라이버에서 정의 된 설명자 필드를 반환 하려면 호출할 수도 있습니다.  
  
 성능상의 이유로 응용 프로그램 호출 하지 않아야 **SQLGetDescField** 문을 실행 하기 전에 IRD에 대 한 합니다.  
  
 이름, 데이터 형식 및 열 또는 매개 변수 데이터의 저장소를 설명 하는 여러 필드의 설정에 대 한 단일 호출에서 검색할 수도 있습니다 **SQLGetDescRec**합니다. **SQLGetStmtAttr** 문 특성 이기도 설명자 헤더의 단일 필드의 설정을 반환 하려면 호출할 수 있습니다. **SQLColAttribute**, **SQLDescribeCol**, 및 **SQLDescribeParam** 레코드 또는 책갈피 필드를 반환 합니다.  
  
 응용 프로그램을 호출할 때 **SQLGetDescField** 특정 설명자 형식에 대해 정의 되지 않은 필드의 값을 검색할 함수는 SQL_SUCCESS를 반환 하지만 필드에 대해 반환 되는 값이 정의 되지 않습니다. 예를 들어, 호출 **SQLGetDescField** APD 또는 카드가 SQL_DESC_NAME 또는 SQL_DESC_NULLABLE 필드는 SQL_SUCCESS 되지만 정의 되지 않은 필드 값을 반환 합니다.  
  
 응용 프로그램을 호출할 때 **SQLGetDescField** 특정 설명자 형식에 대해 정의 되는 있지만 기본값이 없으며을 아직 설정 되지 않은 필드의 값을 검색 하려면 반환 SQL_SUCCESS 값 반환 필드에 대해 정의 되지 않습니다. 설명자 필드 및 설명 필드의 초기화에 자세한 내용은 "설명자 필드의 초기화"를 참조 하세요 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)합니다. 설명자에 대 한 자세한 내용은 참조 하세요. [설명자](../../../odbc/reference/develop-app/descriptors.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|여러 설명자 필드 가져오기|[SQLGetDescRec 함수](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|단일 설명자 필드 설정|[SQLSetDescField 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|여러 설명자 필드 설정|[SQLSetDescRec 함수](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
