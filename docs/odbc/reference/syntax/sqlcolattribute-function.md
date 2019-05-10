---
title: SQLColAttribute 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLColAttribute
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLColAttribute
helpviewer_keywords:
- SQLColAttribute function [ODBC]
ms.assetid: 8c45c598-cb01-4789-a571-e93619a18ed9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ca10614062a495de2c8f0ee80d7bbd5c0e675ad4
ms.sourcegitcommit: 603d5ef9b45c2f111d36d11864dc032917e4a321
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/08/2019
ms.locfileid: "65449751"
---
# <a name="sqlcolattribute-function"></a>SQLColAttribute 함수(SQLColAttribute Function)
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수 합니다. ISO 92  
  
 **요약**  
 **SQLColAttribute** 결과 집합의 열에 대 한 설명자 정보를 반환 합니다. 설명자 정보 문자열, 설명자 종속 값 또는 정수 값으로 반환 됩니다.  
  
> [!NOTE]  
>  자세한 내용은 관리자에 대 한 어떤를 드라이버에 대 한 경우는 ODBC 3이이 함수를를 매핑합니다. *x* 는 ODBC 2를 사용 하 여 응용 프로그램이 작동 합니다. *x* 드라이버를 참조 하세요 [이전 버전과 호환성의 응용 프로그램에 대 한 대체 함수 매핑](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLColAttribute (  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ColumnNumber,  
      SQLUSMALLINT    FieldIdentifier,  
      SQLPOINTER      CharacterAttributePtr,  
      SQLSMALLINT     BufferLength,  
      SQLSMALLINT *   StringLengthPtr,  
      SQLLEN *        NumericAttributePtr);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 [입력] 문 핸들입니다.  
  
 *ColumnNumber*  
 [입력] IRD 필드 값이 올 검색할 레코드의 수입니다. 이 인수는 1부터 증가 열 순서로 순차적으로 정렬 하 고 결과 데이터를 열 수에 해당 합니다. 순서에 관계 없이 열을 설명할 수 있습니다.  
  
 열 0이이 인수를 지정할 수 있습니다 하지만 SQL_DESC_TYPE 및 SQL_DESC_OCTET_LENGTH를 제외한 모든 값은 정의 되지 않은 값을 반환 합니다.  
  
 *FieldIdentifier*  
 [입력] 설명자 핸들입니다. 이 핸들 IRD 필드 (예: SQL_COLUMN_TABLE_NAME) 쿼리해야 정의 합니다.  
  
 *CharacterAttributePtr*  
 [출력] 값을 반환 하는 버퍼에 대 한 포인터를 *FieldIdentifier* 필드를 *ColumnNumber* IRD 필드는 문자 문자열인 경우의 행입니다. 그렇지 않으면 필드가 사용 되지 않습니다.  
  
 하는 경우 *CharacterAttributePtr* 가 null 인 경우 *StringLengthPtr* 바이트 (문자 데이터에 대 한 null 종료 문자 제외)의 총 수를 반환 여전히는 버퍼에서 반환할 사용 가능한 가 가리키는 *CharacterAttributePtr*합니다.  
  
 *BufferLength*  
 [입력] 하는 경우 *FieldIdentifier* 은 ODBC 정의 된 필드와 *CharacterAttributePtr* 문자열 또는 이진 버퍼를 가리키는이 인수 길이 여야 \*  *CharacterAttributePtr*합니다. 하는 경우 *FieldIdentifier* 은 ODBC 정의 된 필드와 \* *CharacterAttribute*Ptr 정수 이면이 필드는 무시 됩니다. 경우는  *\*CharacterAttributePtr* 는 유니코드 문자열 (호출할 때 **SQLColAttributeW**), *BufferLength* 인수 수는 짝수 여야 합니다. 하는 경우 *FieldIdentifier* 드라이버에서 정의 된 필드는 응용 프로그램을 설정 하 여 드라이버 관리자에 필드의 특성을 나타내는 합니다 *BufferLength* 인수. *BufferLength* 다음 값을 가질 수 있습니다.  
  
-   하는 경우 *CharacterAttributePtr* 포인터에 대 한 포인터 *BufferLength* SQL_IS_POINTER 값이 있어야 합니다.  
  
-   하는 경우 *CharacterAttributePtr* 문자열에 대 한 포인터는 *BufferLength* 버퍼의 길이입니다.  
  
-   하는 경우 *CharacterAttributePtr* 결과인 이진 버퍼는 응용 프로그램 위치에 대 한 포인터를 SQL_LEN_BINARY_ATTR (*길이*)에서 매크로 *BufferLength*합니다. 에 음수 값이 배치 *BufferLength*합니다.  
  
-   하는 경우 *CharacterAttributePtr* 고정 길이 데이터 형식에 대 한 포인터 *BufferLength* 다음 중 하나 여야 합니다. SQL_IS_INTEGER, SQL_IS_UNINTEGER, SQL_SMALLINT, 또는 SQLUSMALLINT 합니다.  
  
 *StringLengthPtr*  
 [출력] 바이트 (문자 데이터에 대 한 null 종료 바이트 제외)의 총 수를 반환 하는 버퍼에 대 한 포인터를 반환 하려면 사용할 수 있습니다 **CharacterAttributePtr*합니다.  
  
 문자 데이터를 반환할 수 있는 바이트 수가 보다 크거나 같은 경우에 대 한 *BufferLength*에서 설명자 정보를 \* *CharacterAttributePtr* 잘립니다 *BufferLength* null 종료 문자 길이 뺀 값 및 드라이버에 의해 null로 종결 됩니다.  
  
 다른 모든 유형의 데이터를 값 *BufferLength* 무시 됩니다 드라이버의 크기를 가정 하 고 **CharacterAttributePtr* 는 32 비트입니다.  
  
 *NumericAttributePtr*  
 [출력] 값을 반환 하는 정수 버퍼에 대 한 포인터를 *FieldIdentifier* 필드를 *ColumnNumber* IRD 필드 형식인 숫자 설명자 SQL_DESC_COLUMN_LENGTH 같은 경우의 행입니다. 그렇지 않으면 필드가 사용 되지 않습니다. 일부 드라이버 하위 32 비트에만 쓸 수 있습니다 또는 변경 하지 않고 16 비트 두고 버퍼의 상위 비트는 note 하십시오. 따라서 응용 프로그램이이 함수를 호출 하기 전에 값을 0으로 초기화 해야 합니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLColAttribute** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 합니다. 호출 하 여 연관된 된 SQLSTATE 값을 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여를 *HandleType*호출의와 *처리할* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLColAttribute** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|버퍼 \* *CharacterAttributePtr* 작아서 전체 문자열 값을 반환 문자열 값이 잘렸습니다 하므로 수 없습니다. 잘리지 않은 문자열 값의 길이에서 **StringLengthPtr*합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|07005|준비 된 문이 없습니다를 *커서 사양이*|관련 된 문을 합니다 *StatementHandle* 결과 집합을 반환 하지 않았습니다 하 고 *FieldIdentifier* SQL_DESC_COUNT 없습니다. 열을 설명 했습니다.|  
|07009|잘못 된 설명자 인덱스입니다.|(DM)에 대 한 지정 된 값 *ColumnNumber* 0이 고 SQL_ATTR_USE_BOOKMARKS 문 특성 SQL_UB_OFF 합니다.<br /><br /> 인수에 지정 된 값 *ColumnNumber* 결과 집합의 열 수보다 큽니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagField** 진단 데이터의 구조 오류 및 해당 원인을 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정 합니다 *StatementHandle*합니다. 함수 호출 및 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 가 호출 된 *StatementHandle*합니다. 함수에서 다시 호출 된 다음 합니다 *StatementHandle*합니다.<br /><br /> 함수 호출 및 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출한 합니다 *StatementHandle* 의 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)를 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한 합니다 *StatementHandle*합니다. SQLColAttribute가 호출 될 때이 aynchronous 함수가 계속 실행 합니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대해 호출 된 합니다 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM) 함수를 호출한 호출 하기 전에 **SQLPrepare**를 **SQLExecDirect**, 또는 카탈로그 함수에 대 한 합니다 *StatementHandle*합니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수 (없습니다이 하나)에 대해 호출 된 합니다 *StatementHandle* 이 함수가 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**를 **SQLExecDirect**를 **SQLBulkOperations**, 또는 **SQLSetPos** 에 대해 호출 된는  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|(DM)  *\*CharacterAttributePtr* 문자열, 및 *BufferLength* 0 보다 작지만 같지 않음 SQL_NTS 되었습니다.|  
|HY091|잘못 된 설명자 필드 식별자입니다.|인수에 지정 된 값 *FieldIdentifier* 정의 된 값 중 하나가 아니었습니다 및 구현 시 정의 된 값이 없습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|드라이버를 사용할 수 없습니다.|인수에 지정 된 값 *FieldIdentifier* 가 드라이버에서 지원 되지 않습니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 드라이버를 사용 하 여 연결 합니다 *StatementHandle* 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드로 폴링 되지|알림 모델을 사용할 때마다 폴링 비활성화 됩니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하려면 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
 호출 **SQLPrepare** 전과 **SQLExecute**하십시오 **SQLColAttribute** 에서 반환 될 수 있는 모든 SQLSTATE를 반환할 수 있습니다 **SQLPrepare**나 **SQLExecute**데이터 원본에 연결 된 SQL 문을 평가 하는 경우에 따라 합니다 *StatementHandle*합니다.  
  
 성능상의 이유로 응용 프로그램 호출 하지 않아야 **SQLColAttribute** 문을 실행 하기 전에 합니다.  
  
## <a name="comments"></a>주석  
 응용 프로그램에서 반환 하는 정보를 사용 하는 방법에 대 한 자세한 **SQLColAttribute**를 참조 하십시오 [결과 집합 메타 데이터](../../../odbc/reference/develop-app/result-set-metadata.md)입니다.  
  
 **SQLColAttribute** 하거나 정보를 반환 합니다에 \* *NumericAttributePtr* 나 \* *CharacterAttributePtr*합니다. 정수 정보에서 반환 됩니다 \* *NumericAttributePtr* SQLLEN 값;으로 다른 모든 형식의 정보에 반환 됩니다 \* *CharacterAttributePtr*합니다. 정보에서 반환 될 때 \* *NumericAttributePtr*, 드라이버 무시 *CharacterAttributePtr*를 *BufferLength*, 및  *StringLengthPtr*합니다. 정보에서 반환 될 때 \* *CharacterAttributePtr*, 드라이버 무시 *NumericAttributePtr*합니다.  
  
 **SQLColAttribute** IRD의 설명자 필드에서 값을 반환 합니다. 설명자 핸들을 하지 않고 문 핸들을 사용 하 여 함수를 호출 합니다. 반환 하는 값 **SQLColAttribute** 에 대 한 합니다 *FieldIdentifier* 호출 하 여이 섹션의 뒷부분에 나열 된 값을 검색할 수도 있습니다 **SQLGetDescField** 으로 적절 한 IRD 핸들입니다.  
  
 현재 정의 된 설명자 필드는 도입 된 및이 섹션에 있는 정보를 반환 하는 인수는 뒷부분에 나오는 하는 ODBC의 버전 더 많은 설명자 형식은 다른 데이터 원본 활용 하기 위해 드라이버에서 정의할 수 있습니다.  
  
 ODBC 3입니다. *x* 드라이버의 각 설명자 필드에 대 한 값을 반환 해야 합니다. 설명자 필드는 드라이버나 데이터 원본에 적용 되지 않습니다 하 고 드라이버에서 0을 반환 별도로 언급 하지 않는 한 \* *StringLengthPtr* 에서 빈 문자열 또는 **CharacterAttributePtr*합니다.  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 ODBC 3입니다. *x* 함수 **SQLColAttribute** 대체 사용 되지 않는 ODBC 2. *x* 함수 **SQLColAttributes**합니다. 매핑하면 **SQLColAttributes** 하 **SQLColAttribute** (경우는 ODBC 2. *x* 응용 프로그램을 ODBC 3을 사용 하 여 작동 합니다. *x* 드라이버), 또는 매핑을 **SQLColAttribute** 하려면 **SQLColAttributes** (때는 ODBC 3. *x* 는 ODBC 2를 사용 하 여 응용 프로그램이 작동 합니다. *x* 드라이버), 드라이버 관리자의 값을 전달 하거나 *FieldIdentifier* 통해 maps에 새 값으로 또는 다음과 같은 오류를 반환 합니다.  
  
> [!NOTE]  
>  에 사용 되는 접두사 *FieldIdentifier* 값 ODBC 3에서. *x* 해당에서 사용 되는 ODBC 2에서에서 변경 되었습니다. *x*합니다. 새 접두사는 "SQL_DESC"; 이전에는 "SQL_COLUMN" 했습니다.  
  
-   경우는 **#define** 값이 ODBC 2. *x* *FieldIdentifier* 와 동일 합니다 **#define** ODBC 3. *x* *FieldIdentifier*, 함수 호출에 값 전달 됩니다.  
  
-   합니다 **#define** 값 ODBC 2. *x* *FieldIdentifiers* SQL_COLUMN_LENGTH, SQL_COLUMN_PRECISION, 및 SQL_COLUMN_SCALE 다릅니다 합니다 **#define** ODBC 3의 값입니다. *x* *FieldIdentifiers* SQL_DESC_PRECISION, 자릿수가 SQL_DESC_SCALE, 및 SQL_DESC_LENGTH 합니다. ODBC 2입니다. *x* 드라이버는 ODBC 2를 지원만 필요 합니다. *x* 값입니다. ODBC 3입니다. *x* 드라이버가 세이 가지에 대 한 "SQL_COLUMN" 및 "SQL_DESC" 값을 지원 해야 *FieldIdentifiers*합니다. 이러한 값은 전체 자릿수, 소수 자릿수 및 길이 ODBC 3에서 다르게 정의 되기 때문에 다른입니다. *x* ODBC 2에 있는 것 보다. *x*합니다. 자세한 내용은 [열 크기, 십진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)합니다.  
  
-   경우는 **#define** 값이 ODBC 2. *x* *FieldIdentifier* 다릅니다 합니다 **#define** ODBC 3. *x* *FieldIdentifier*, 이름, 개수를 사용 하 여 발생으로 및 null 허용 값, 함수 호출에서 값을 해당 값에 매핑되 합니다. SQL_COLUMN_COUNT SQL_DESC_COUNT에 매핑되는 예를 들어 SQL_DESC_COUNT는 매핑 방향에 따라 SQL_COLUMN_COUNT에 매핑됩니다.  
  
-   하는 경우 *FieldIdentifier* 새 값인 ODBC 3에서. *x*에 값이 없습니다. 해당 ODBC 2에서. *x*때 ODBC 3를 매핑할 수 있습니다. *x* 응용 프로그램에 대 한 호출에 사용 **SQLColAttribute** 는 ODBC 2. *x* 드라이버 및 호출에는 SQLSTATE HY091 반환 됩니다 (잘못 된 설명자 필드 식별자)입니다.  
  
 다음 표에서 나열 하 여 반환 되는 설명자 형식 **SQLColAttribute**합니다. 형식은 *NumericAttributePtr* 값은 **SQLLEN \*** 합니다.  
  
|*FieldIdentifier*|정보<br /><br /> 반환|Description|  
|-----------------------|---------------------------------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE (ODBC 1.0)|*NumericAttributePtr*|열이 자동 증가 열 이면 SQL_TRUE 합니다.<br /><br /> 열 자동 증가 열이 아닌 또는 숫자가 아닌 경우 SQL_FALSE입니다.<br /><br /> 이 필드는 숫자 데이터 형식 열에만 적합 합니다. 응용 프로그램 값을 자동 증분 열이 포함 된 행을 삽입할 수 있지만 일반적으로 열의 값을 업데이트할 수 없습니다.<br /><br /> Autoincrement 열에 삽입 수행 되 면 삽입 시 고유 값 열에 삽입 됩니다. Increment를 정의 하지 않은 이지만 데이터 소스 관련 있습니다. 응용 프로그램 특정 값으로 자동 증분 열을 증가 나 특정 지점에서 시작 하는 것을 가정 하지 않아야 합니다.|  
|SQL_DESC_BASE_COLUMN_NAME (ODBC 3.0)|*CharacterAttributePtr*|기본 열 이름을 결과 집합 열입니다. 기본 열 이름 (예: 열을 식의 경우) 존재 하지 않는 경우이 변수는 빈 문자열을 포함 합니다.<br /><br /> 이 정보는 읽기 전용 필드인 IRD의 SQL_DESC_BASE_COLUMN_NAME 레코드 필드에서 반환 됩니다.|  
|SQL_DESC_BASE_TABLE_NAME (ODBC 3.0)|*CharacterAttributePtr*|열이 포함 된 기본 테이블의 이름입니다. 기본 테이블 이름을 정의할 수 없습니다 또는 적용할 수 없는 경우이 변수는 빈 문자열을 포함 합니다.<br /><br /> 이 정보는 읽기 전용 필드인 IRD의 SQL_DESC_BASE_TABLE_NAME 레코드 필드에서 반환 됩니다.|  
|SQL_DESC_CASE_SENSITIVE (ODBC 1.0)|*NumericAttributePtr*|열 데이터 정렬 및 비교에 대 한 대/소문자 구분으로 처리 되 면 SQL_TRUE 합니다.<br /><br /> 열 데이터 정렬 및 비교에 대 한 대/소문자 구분으로 처리 되지 않습니다 이거나 문자가 아닌 경우 SQL_FALSE입니다.|  
|SQL_DESC_CATALOG_NAME (ODBC 2.0)|*CharacterAttributePtr*|열이 포함 된 테이블의 카탈로그입니다. 반환된 된 값 또는 열이 뷰의 일부 열이 식이면 구현 시 정의 됩니다. 데이터 소스는 카탈로그를 지원 하지 않습니다 또는 카탈로그 이름을 확인할 수 없는 경우 빈 문자열이 반환 됩니다. 이 VARCHAR 레코드 필드 128 자로 제한 됩니다.|  
|SQL_DESC_CONCISE_TYPE (ODBC 1.0)|*NumericAttributePtr*|간결한 데이터 형식입니다.<br /><br /> 이 필드는 날짜/시간 및 간격 데이터 형식에 대 한 간결한 데이터 형식으로를 반환 합니다. 예를 들어, SQL_TYPE_TIME 또는 SQL_INTERVAL_YEAR 합니다. (자세한 내용은 [데이터 형식 식별자 및 설명자](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) 부록 d: 데이터 형식입니다.)<br /><br /> 이 정보는 IRD의 SQL_DESC_CONCISE_TYPE 레코드 필드에서 반환 됩니다.|  
|SQL_DESC_COUNT  (ODBC 1.0)|*NumericAttributePtr*|결과 집합에서 사용할 수 있는 열의 수입니다. 이 결과 집합의 열이 없는 경우 0을 반환 합니다. 값을 *ColumnNumber* 인수는 무시 됩니다.<br /><br /> 이 정보는 IRD의 SQL_DESC_COUNT 헤더 필드에서 반환 됩니다.|  
|SQL_DESC_DISPLAY_SIZE (ODBC 1.0)|*NumericAttributePtr*|열의 데이터를에서 표시 하는 데 필요한 문자의 최대 수입니다. 디스플레이 크기에 대 한 자세한 내용은 참조 하세요. [열 크기, 십진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 d: 데이터 형식입니다.|  
|SQL_DESC_FIXED_PREC_SCALE (ODBC 1.0)|*NumericAttributePtr*|Sql_true는 해당 열에 데이터 소스 관련 된 고정된 전체 자릿수 및 0이 아닌 확장 합니다.<br /><br /> 고정 전체 자릿수 및 0이 아닌 확장 데이터 원본 관련 된 열에 없는 경우 SQL_FALSE입니다.|  
|SQL_DESC_LABEL (ODBC 2.0)|*CharacterAttributePtr*|열 레이블 또는 제목입니다. 예를 들어 EmpName 라는 열 직원 이름 레이블을 지정할 수 있습니다 또는 별칭으로 레이블을 지정할 수 있습니다.<br /><br /> 열에는 레이블이 없는 경우 열 이름이 반환 됩니다. 레이블 열은 명명 되지 않은 경우, 빈 문자열이 반환 됩니다.|  
|SQL_DESC_LENGTH  (ODBC 3.0)|*NumericAttributePtr*|숫자 값을 문자 문자열 또는 이진 데이터의 실제 또는 최대 문자 길이 입력 합니다. 고정 길이 데이터 형식에 대 한 최대 문자 길이 또는 가변 길이 데이터 형식에 대 한 실제 문자 길이입니다. 해당 값에는 항상 null 종료 바이트 문자열을 종료 하는 제외 됩니다.<br /><br /> 이 정보는 IRD의 SQL_DESC_LENGTH 레코드 필드에서 반환 됩니다.<br /><br /> 길이 대 한 자세한 내용은 참조 하세요. [열 크기, 십진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 d: 데이터 형식입니다.|  
|SQL_DESC_LITERAL_PREFIX (ODBC 3.0)|*CharacterAttributePtr*|이 VARCHAR(128) 레코드 필드에는이 데이터 형식의 리터럴에 접두사로 드라이버 인식 하는 문자를 포함 합니다. 이 필드는 리터럴 접두사는 해당 데이터 형식에 대 한 빈 문자열을 포함 합니다. 자세한 내용은 [리터럴 접두사 및 접미사](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)합니다.|  
|SQL_DESC_LITERAL_SUFFIX (ODBC 3.0)|*CharacterAttributePtr*|이 VARCHAR(128) 레코드 필드에는이 데이터 형식의 리터럴에 접미사로 드라이버 인식 하는 문자를 포함 합니다. 이 필드는에 대 한 리터럴 접미사는 해당 데이터 형식에 대 한 빈 문자열을 포함 합니다. 자세한 내용은 [리터럴 접두사 및 접미사](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)합니다.|  
|SQL_DESC_LOCAL_TYPE_NAME (ODBC 3.0)|*CharacterAttributePtr*|이 VARCHAR(128) 레코드 필드에는 데이터 형식의 일반 이름과 다를 수 있는 데이터 형식에 대 한 모든 지역화 된 (native language) 이름을 포함 합니다. 지역화 된 이름이 없는 경우 빈 문자열이 반환 됩니다. 이 필드는 표시 용도로 됩니다. 문자열의 문자 집합을 로캘별 이며 일반적으로 서버의 기본 문자 집합입니다.|  
|SQL_DESC_NAME (ODBC 3.0)|*CharacterAttributePtr*|열 별칭에 적용 되는 경우입니다. 열 별칭이 적용 되지 않는 경우 열 이름이 반환 됩니다. 두 경우 모두 SQL_DESC_UNNAMED는 SQL_NAMED 설정 됩니다. 열 이름 없음 또는 열 별칭을 있으면 빈 문자열 반환 되 고 SQL_DESC_UNNAMED 하면으로 설정 됩니다.<br /><br /> 이 정보는 IRD의 SQL_DESC_NAME 레코드 필드에서 반환 됩니다.|  
|SQL_DESC_NULLABLE (ODBC 3.0)|*NumericAttributePtr*|SQL_ null 허용 열에 NULL 값을 가질 수 있으면 SQL_NO_NULLS 열에 NULL 값이 없는 경우 또는 SQL_NULLABLE_UNKNOWN 경우 열에 NULL 값 허용 하는지 여부를 알 수 없습니다.<br /><br /> 이 정보는 IRD의 SQL_DESC_NULLABLE 레코드 필드에서 반환 됩니다.|  
|SQL_DESC_NUM_PREC_RADIX (ODBC 3.0)|*NumericAttributePtr*|SQL_DESC_TYPE 필드의 데이터 형식은 근사 숫자 데이터 형식이 면 SQL_DESC_PRECISION 필드 비트 수 있기 때문에이 SQLINTEGER 필드 값이 2 포함 합니다. SQL_DESC_TYPE 필드의 데이터 형식은 정확한 숫자 데이터 형식인 경우이 필드 SQL_DESC_PRECISION 필드 10 진수 수 있기 때문에 있는 값 10 포함 합니다. 이 필드는 모든 숫자가 아닌 데이터 형식에 대해 0으로 설정 됩니다.|  
|SQL_DESC_OCTET_LENGTH (ODBC 3.0)|*NumericAttributePtr*|문자 문자열 또는 이진 데이터 형식의 길이 (바이트) 합니다. 고정 길이 문자 또는 이진 형식의 실제 길이 (바이트)입니다. 가변 길이 문자 또는 이진 형식의 최대 길이 (바이트)입니다. 이 값에 null 종결자를 포함 되지 않습니다.<br /><br /> 이 정보는 IRD의 SQL_DESC_OCTET_LENGTH 레코드 필드에서 반환 됩니다.<br /><br /> 길이 대 한 자세한 내용은 참조 하세요. [열 크기, 십진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 d: 데이터 형식입니다.|  
|자릿수가 SQL_DESC_PRECISION (ODBC 3.0)|*NumericAttributePtr*|나타내는 숫자 데이터 형식에 대 한 해당 전체 자릿수는 숫자 값입니다. 데이터에 대 한 형식 SQL_TYPE_TIMESTAMP, SQL_TYPE_TIME 이며 시간 간격, 해당 값을 나타내는 모든 interval 데이터 형식을 해당 전체 자릿수 소수 자릿수 초 구성 요소입니다.<br /><br /> 이 정보는 IRD의 자릿수가 SQL_DESC_PRECISION 레코드 필드에서 반환 됩니다.|  
|자릿수가 SQL_DESC_SCALE (ODBC 3.0)|*NumericAttributePtr*|숫자 데이터 형식에 대 한 해당 소수 자릿수는 숫자 값입니다. DECIMAL 및 NUMERIC 데이터 형식에 정의 된 소수 자릿수입니다. 다른 모든 데이터 형식에 대해 정의 된 것입니다.<br /><br /> 이 정보는 IRD의 배율 레코드 필드에서 반환 됩니다.|  
|SQL_DESC_SCHEMA_NAME (ODBC 2.0)|*CharacterAttributePtr*|열이 포함 된 테이블의 스키마입니다. 반환된 된 값 또는 열이 뷰의 일부 열이 식이면 구현 시 정의 됩니다. 데이터 원본 스키마를 지원 하지 않으므로 또는 스키마 이름을 확인할 수 없는 경우 빈 문자열이 반환 됩니다. 이 VARCHAR 레코드 필드 128 자로 제한 됩니다.|  
|SQL_DESC_SEARCHABLE (ODBC 1.0)|*NumericAttributePtr*|SQL_PRED_NONE WHERE 절에서 열을 사용할 수 없는 경우. (이 / ODBC 2에서 SQL_UNSEARCHABLE 값과 동일 합니다. *x*.)<br /><br /> SQL_PRED_CHAR LIKE 조건자만 하지만 WHERE 절에서 열을 사용할 수 있는 경우. (이 / ODBC 2에서 SQL_LIKE_ONLY 값과 동일 합니다. *x*.)<br /><br /> SQL_PRED_BASIC 같은 제외한 모든 비교 연산자를 사용 하 여 WHERE 절에서 열을 사용할 수 있는 경우. (이 / ODBC 2에서 SQL_EXCEPT_LIKE 값과 동일 합니다. *x*.)<br /><br /> SQL_PRED_SEARCHABLE 모든 비교 연산자와 함께 WHERE 절에서 열을 사용할 수 있는 경우.<br /><br /> 열에는 일반적으로 반환 SQL_PRED_CHAR SQL_LONGVARBINARY 및 SQL_LONGVARCHAR 입력합니다.|  
|SQL_DESC_TABLE_NAME (ODBC 2.0)|*CharacterAttributePtr*|열을 포함하는 테이블의 이름입니다. 반환된 된 값 또는 열이 뷰의 일부 열이 식이면 구현 시 정의 됩니다.<br /><br /> 테이블 이름을 확인할 수 없는 경우 빈 문자열이 반환 됩니다.|  
|SQL_DESC_TYPE (ODBC 3.0)|*NumericAttributePtr*|SQL 데이터 형식을 지정 하는 숫자 값입니다.<br /><br /> 때 *ColumnNumber* 같으면 0으로 SQL_BINARY 가변 길이 책갈피에 대 한 반환 되 고 SQL_INTEGER 고정 길이 책갈피에 대해 반환 됩니다.<br /><br /> 날짜/시간 및 간격 데이터 형식에 대 한이 필드에 자세한 데이터 형식을 반환합니다. SQL_DATETIME 또는 sql_interval 인 합니다. (자세한 내용은 [데이터 형식 식별자 및 설명자](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) 부록 d: 데이터 형식입니다.<br /><br /> 이 정보는 IRD의 SQL_DESC_TYPE 레코드 필드에서 반환 됩니다. **참고:**  ODBC 2에 대해 작동 합니다. *x* 드라이버 SQL_DESC_CONCISE_TYPE를 대신 사용 합니다.|  
|인 SQL_DESC_TYPE_NAME (ODBC 1.0)|*CharacterAttributePtr*|데이터 원본에 종속적인 데이터 형식 이름입니다. 예를 들어, "CHAR", "VARCHAR", "MONEY", "LONG VARBINARY" 또는 "CHAR () FOR BIT DATA"입니다.<br /><br /> 종류를 알 수 없는 경우 빈 문자열이 반환 됩니다.|  
|SQL_DESC_UNNAMED (ODBC 3.0)|*NumericAttributePtr*|SQL_NAMED 또는 하면 합니다. IRD의 SQL_DESC_NAME 필드 열 별칭 또는 열 이름이 있으면 SQL_NAMED 반환 됩니다. 열 이름이 나 열 별칭 없습니다 있으면 하면 반환 됩니다.<br /><br /> 이 정보는 IRD의 SQL_DESC_UNNAMED 레코드 필드에서 반환 됩니다.|  
|SQL_DESC_UNSIGNED (ODBC 1.0)|*NumericAttributePtr*|부호 없는 (또는 숫자가 아닌) 열 이면 SQL_TRUE 합니다.<br /><br /> SQL_FALSE 열 서명 된 경우입니다.|  
|SQL_DESC_UPDATABLE (ODBC 1.0)|*NumericAttributePtr*|열 정의 된 상수에 대 한 값으로 설명 되어 있습니다.<br /><br /> SQL_ATTR_READONLY SQL_ATTR_WRITE SQL_ATTR_READWRITE_UNKNOWN<br /><br /> SQL_DESC_UPDATABLE 결과 집합의 열, 기본 테이블의 열이 아닌 업데이트 가능성을 설명합니다. 결과 집합 열 기준으로 하는 기본 열의 업데이트 가능성은이 필드의 값과에서 다를 수 있습니다. 열이 업데이트할 수 있는 데이터 형식, 사용자 권한 및 결과 집합 자체의 정의에 기반 할 수 있습니다. 열을 업데이트할 수 있는지 여부에 명확한 아니라면 SQL_ATTR_READWRITE_UNKNOWN 반환 되어야 합니다.|  
  
 **SQLColAttribute** extensible 대안인 **SQLDescribeCol**합니다. **SQLDescribeCol** 89 ANSI SQL을 사용 하는 설명자 정보 고정된 집합을 반환 합니다. **SQLColAttribute** 더 광범위 한 ANSI SQL-92 및 DBMS 공급 업체 확장 기능에서 사용할 수 있는 설명자 정보 집합에 대 한 액세스를 허용 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|버퍼를 결과 집합의 열에 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|결과 집합의 열에 대 한 정보를 반환합니다.|[SQLDescribeCol 함수](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|데이터 블록을 인출 또는 결과 통해 스크롤 설정|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|여러 행의 데이터를 가져오는 중|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
  
## <a name="example"></a>예제  
 다음 샘플 코드에는 핸들 및 연결 해제 하지 않습니다. 참조 [SQLFreeHandle 함수](../../../odbc/reference/syntax/sqlfreehandle-function.md)를 [샘플 ODBC 프로그램](../../../odbc/reference/sample-odbc-program.md), 및 [SQLFreeStmt 함수](../../../odbc/reference/syntax/sqlfreestmt-function.md) 핸들과 문을 해제 하는 코드 샘플입니다.  
  
```  
// SQLColAttibute.cpp  
// compile with: user32.lib odbc32.lib  
  
#define UNICODE  
  
#include <windows.h>  
#include <sqlext.h>  
#include <strsafe.h>  
  
struct DataBinding {  
   SQLSMALLINT TargetType;  
   SQLPOINTER TargetValuePtr;  
   SQLINTEGER BufferLength;  
   SQLLEN StrLen_or_Ind;  
};  
  
void printStatementResult(SQLHSTMT hstmt) {  
   int bufferSize = 1024, i;  
   SQLRETURN retCode;  
   SQLSMALLINT numColumn = 0, bufferLenUsed;
   
   retCode = SQLNumResultCols(hstmt, &numColumn);  
   
   SQLPOINTER* columnLabels = (SQLPOINTER *)malloc( numColumn * sizeof(SQLPOINTER*) );  
   struct DataBinding* columnData = (struct DataBinding*)malloc( numColumn * sizeof(struct DataBinding) );  
  
   printf( "Columns from that table:\n" );  
   for ( i = 0 ; i < numColumn ; i++ ) {  
      columnLabels[i] = (SQLPOINTER)malloc( bufferSize*sizeof(char) );  
  
      retCode = SQLColAttribute(hstmt, (SQLUSMALLINT)i + 1, SQL_DESC_LABEL, columnLabels[i], (SQLSMALLINT)bufferSize, &bufferLenUsed, NULL);  
      wprintf( L"Column %d: %s\n", i, (wchar_t*)columnLabels[i] );  
   }  
  
   // allocate memory for the binding  
   for ( i = 0 ; i < numColumn ; i++ ) {  
      columnData[i].TargetType = SQL_C_CHAR;  
      columnData[i].BufferLength = (bufferSize+1);  
      columnData[i].TargetValuePtr = malloc( sizeof(unsigned char)*columnData[i].BufferLength );  
   }  
  
   // setup the binding   
   for ( i = 0 ; i < numColumn ; i++ ) {  
      retCode = SQLBindCol(hstmt, (SQLUSMALLINT)i + 1, columnData[i].TargetType,   
         columnData[i].TargetValuePtr, columnData[i].BufferLength, &(columnData[i].StrLen_or_Ind));  
   }  
  
   printf( "Data from that table:\n" );  
   // fetch the data and print out the data  
   for ( retCode = SQLFetch(hstmt) ; retCode == SQL_SUCCESS || retCode == SQL_SUCCESS_WITH_INFO ; retCode = SQLFetch(hstmt) ) {  
      int j;  
      for ( j = 0 ; j < numColumn ; j++ )  
         wprintf( L"%s: %hs\n", columnLabels[j], columnData[j].TargetValuePtr );  
      printf( "\n" );  
   }  
   printf( "\n" );   
}  
  
int main() {  
   int bufferSize = 1024, i, count = 1, numCols = 5;  
   wchar_t firstTableName[1024], * dbName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize ), * userName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize );  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLWCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen, bufferLen;  
   SQLRETURN retCode;  
  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   struct DataBinding* catalogResult = (struct DataBinding*) malloc( numCols * sizeof(struct DataBinding) );  
   SQLWCHAR* selectAllQuery = (SQLWCHAR *)malloc( sizeof(SQLWCHAR) * bufferSize );  
  
   // connect to database  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLCHAR *)(void*)SQL_OV_ODBC3, -1);  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
   retCode = SQLDriverConnect(hdbc, desktopHandle, L"Driver={SQL Server}", SQL_NTS, connStrbuffer, 1025, &connStrBufferLen, SQL_DRIVER_PROMPT);  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   // display the database information  
   retCode = SQLGetInfo(hdbc, SQL_DATABASE_NAME, dbName, (SQLSMALLINT)bufferSize, (SQLSMALLINT *)&bufferLen);  
   retCode = SQLGetInfo(hdbc, SQL_USER_NAME, userName, (SQLSMALLINT)bufferSize, &bufferLen);  
  
   for ( i = 0 ; i < numCols ; i++ ) {  
      catalogResult[i].TargetType = SQL_C_CHAR;  
      catalogResult[i].BufferLength = (bufferSize + 1);  
      catalogResult[i].TargetValuePtr = malloc( sizeof(unsigned char)*catalogResult[i].BufferLength );  
   }  
  
   // Set up the binding. This can be used even if the statement is closed by closeStatementHandle  
   for ( i = 0 ; i < numCols ; i++ )  
      retCode = SQLBindCol(hstmt, (SQLUSMALLINT)i + 1, catalogResult[i].TargetType, catalogResult[i].TargetValuePtr, catalogResult[i].BufferLength, &(catalogResult[i].StrLen_or_Ind));  
  
   retCode = SQLTables( hstmt, (SQLWCHAR*)SQL_ALL_CATALOGS, SQL_NTS, L"", SQL_NTS, L"", SQL_NTS, L"", SQL_NTS );  
   retCode = SQLFreeStmt(hstmt, SQL_CLOSE);  
  
   retCode = SQLTables( hstmt, dbName, SQL_NTS, userName, SQL_NTS, L"%", SQL_NTS, L"TABLE", SQL_NTS );  
  
   for ( retCode = SQLFetch(hstmt) ; retCode == SQL_SUCCESS || retCode == SQL_SUCCESS_WITH_INFO ; retCode = SQLFetch(hstmt), ++count )  
      if ( count == 1 )  
         StringCchPrintfW( firstTableName, 1024, L"%hs", catalogResult[2].TargetValuePtr );  
   retCode = SQLFreeStmt(hstmt, SQL_CLOSE);  
  
   wprintf( L"Select all data from the first table (%s)\n", firstTableName );  
   StringCchPrintfW( selectAllQuery, bufferSize, L"SELECT * FROM %s", firstTableName );  
  
   retCode = SQLExecDirect(hstmt, selectAllQuery, SQL_NTS);  
   printStatementResult(hstmt);  
}  
```  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [샘플 ODBC 프로그램](../../../odbc/reference/sample-odbc-program.md)
