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
ms.openlocfilehash: c4577b97c827d527422fe2448656496d7c196c40
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68118697"
---
# <a name="sqlcolattribute-function"></a>SQLColAttribute 함수(SQLColAttribute Function)
**규칙**  
 소개 된 버전: ODBC 3.0 표준 준수: ISO 92  
  
 **요약**  
 **Sqlcolattribute** 는 결과 집합의 열에 대 한 설명자 정보를 반환 합니다. 설명자 정보는 문자열, 설명자 종속 값 또는 정수 값으로 반환 됩니다.  
  
> [!NOTE]  
>  ODBC 3의 경우 드라이버 관리자가이 기능을에 매핑하는 방법에 대 한 자세한 내용을 확인 하십시오. *x* 응용 프로그램에서 ODBC 2를 사용 하 고 있습니다. *x* 드라이버 [응용 프로그램의 이전 버전과의 호환성을 위해 대체 함수 매핑](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)을 참조 하세요.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
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
 입력 문 핸들입니다.  
  
 *ColumnNumber*  
 입력 필드 값을 검색할 IRD의 레코드 수입니다. 이 인수는 1부터 시작 하 여 열 순서에 따라 순차적으로 정렬 된 결과 데이터의 열 수에 해당 합니다. 열은 순서에 관계 없이 설명할 수 있습니다.  
  
 이 인수에는 열 0을 지정할 수 있지만 SQL_DESC_TYPE 및 SQL_DESC_OCTET_LENGTH를 제외한 모든 값은 정의 되지 않은 값을 반환 합니다.  
  
 *FieldIdentifier*  
 입력 설명자 핸들입니다. 이 핸들은 IRD에서 쿼리할 필드를 정의 합니다 (예: SQL_COLUMN_TABLE_NAME).  
  
 *CharacterAttributePtr*  
 출력 IRD에 있는 *Columnnumber* 행의 *FieldIdentifier* 필드에 있는 값을 반환할 버퍼에 대 한 포인터입니다. 그렇지 않으면이 필드는 사용 되지 않습니다.  
  
 *CharacterAttributePtr* 가 NULL 인 경우 *StringLengthPtr* 는 *CharacterAttributePtr*가 가리키는 버퍼에서 반환 될 수 있는 총 바이트 수 (문자 데이터의 NULL 종료 문자 제외)를 반환 합니다.  
  
 *BufferLength*  
 입력 *FieldIdentifier* 가 ODBC 정의 필드이 고 *CharacterAttributePtr* 가 문자열 또는 이진 버퍼를 가리키는 경우이 인수는 \* *CharacterAttributePtr*의 길이 여야 합니다. *FieldIdentifier* 가 ODBC 정의 필드이 고 \* *CharacterAttribute*Ptr이 정수 이면이 필드는 무시 됩니다. CharacterAttributePtr가 유니코드 문자열이 면 ( **sqlcolattributew**를 호출할 때) *bufferlength* 인수는 짝수 여야 합니다. * \** *FieldIdentifier* 가 드라이버 정의 필드인 경우 응용 프로그램은 *bufferlength* 인수를 설정 하 여 필드의 특성을 드라이버 관리자에 게 표시 합니다. *Bufferlength* 에는 다음 값을 사용할 수 있습니다.  
  
-   *CharacterAttributePtr* 가 포인터에 대 한 포인터인 경우 *bufferlength* 의 값은 SQL_IS_POINTER 이어야 합니다.  
  
-   *CharacterAttributePtr* 이 문자열에 대 한 포인터인 경우 *bufferlength* 는 버퍼의 길이입니다.  
  
-   *CharacterAttributePtr* 가 이진 버퍼에 대 한 포인터인 경우 응용 프로그램은 SQL_LEN_BINARY_ATTR (*길이*) 매크로의 결과를 *bufferlength*로 배치 합니다. 그러면 음수 값이 *Bufferlength*에 배치 됩니다.  
  
-   *CharacterAttributePtr* 가 고정 길이 데이터 형식에 대 한 포인터인 경우 *bufferlength* 는 SQL_IS_INTEGER, SQL_IS_UNINTEGER, SQL_SMALLINT 또는 SQLUSMALLINT 중 하나 여야 합니다.  
  
 *StringLengthPtr*  
 출력 **CharacterAttributePtr*에서 반환 하는 데 사용할 수 있는 총 바이트 수 (문자 데이터의 경우 null 종료 바이트 제외)를 반환할 버퍼에 대 한 포인터입니다.  
  
 문자 데이터의 경우 반환할 수 있는 바이트 수가 *bufferlength*보다 크거나 같은 경우 \* *CharacterAttributePtr* 의 설명자 정보는 *bufferlength* 에서 null 종료 문자의 길이를 뺀 값으로 잘리고 드라이버에 의해 null로 종료 됩니다.  
  
 다른 모든 유형의 데이터에 대해 *Bufferlength* 값은 무시 되 고 드라이버는 **CharacterAttributePtr* 의 크기를 32 비트로 가정 합니다.  
  
 *NumericAttributePtr*  
 출력 필드가 SQL_DESC_COLUMN_LENGTH와 같은 숫자 설명자 형식인 경우 IRD의 *Columnnumber* 행에 있는 *FieldIdentifier* 필드의 값을 반환할 정수 버퍼에 대 한 포인터입니다. 그렇지 않으면이 필드는 사용 되지 않습니다. 일부 드라이버는 버퍼의 하위 32 비트 또는 16 비트만 쓸 수 있으며, 상위 비트는 변경 되지 않은 상태로 둘 수 있습니다. 따라서 응용 프로그램은이 함수를 호출 하기 전에 값을 0으로 초기화 해야 합니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **Sqlcolattribute** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 *HandleType* SQL_HANDLE_STMT의 및 *StatementHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 가져올 수 있습니다. 다음 표에서는 일반적으로 **Sqlcolattribute** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각각에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01004|문자열 데이터, 오른쪽이 잘렸습니다.|버퍼 \* *CharacterAttributePtr* 의 크기가 작아서 전체 문자열 값을 반환할 수 없으므로 문자열 값이 잘렸습니다. 잘리지 않는 문자열 값의 길이는 **StringLengthPtr*에서 반환 됩니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|07005|준비 된 문이 *커서 사양이* 아닙니다.|*StatementHandle* 와 연결 된 문이 결과 집합을 반환 하지 않았으며 *FieldIdentifier* 가 SQL_DESC_COUNT 되지 않았습니다. 설명 하는 열이 없습니다.|  
|07009|잘못 된 설명자 인덱스|(DM) *Columnnumber* 에 지정 된 값이 0이 고 SQL_ATTR_USE_BOOKMARKS statement 특성이 SQL_UB_OFF 되었습니다.<br /><br /> 인수 *Columnnumber* 에 지정 된 값이 결과 집합의 열 수보다 큽니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. 진단 데이터 구조의 **SQLGetDiagField** 에서 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업 취소됨|*StatementHandle*에 대해 비동기 처리를 사용 하도록 설정 했습니다. 함수가 호출 되었으며 실행이 완료 되기 전에 **sqlcancel** 또는 **Sqlcancelhandle** 이 *StatementHandle*에 대해 호출 되었습니다. 그런 다음 *StatementHandle*에서 함수를 다시 호출 했습니다.<br /><br /> 함수가 호출 되 고 실행이 완료 되기 전에 **sqlcancel** 또는 **sqlcancelhandle** 이 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle* 호출 되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. SQLColAttribute가 호출 될 때이 aynchronous 함수는 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 *StatementHandle* 에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM) **Sqlprepare**, **sqlexecdirect**또는 *StatementHandle*에 대 한 카탈로그 함수를 호출 하기 전에 함수가 호출 되었습니다.<br /><br /> (DM) *StatementHandle* 에 대해 비동기적으로 실행 되는 함수 (이 함수 아님)가 호출 되었으며이 함수가 호출 될 때 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 가 *StatementHandle* 에 대해 호출 되 고 SQL_NEED_DATA 반환 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|(DM) * \*CharacterAttributePtr* 은 문자열이 고, *bufferlength* 는 0 보다 작지만 SQL_NTS와 같지 않습니다.|  
|HY091|잘못 된 설명자 필드 식별자입니다.|*FieldIdentifier* 인수에 지정 된 값이 정의 된 값 중 하나가 아니고 구현에 정의 된 값이 아닙니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYC00|드라이버를 사용할 수 없음|*FieldIdentifier* 인수에 지정 된 값이 드라이버에서 지원 되지 않습니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *StatementHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드에서는 폴링을 사용할 수 없습니다.|알림 모델을 사용할 때마다 폴링은 사용 하지 않도록 설정 됩니다.|  
|IM018|이 핸들에서 이전 비동기 작업을 완료 하기 위해 **SQLCompleteAsync** 가 호출 되지 않았습니다.|핸들에 대 한 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드가 설정 된 경우에는 핸들에 대해 **SQLCompleteAsync** 를 호출 하 여 사후 처리를 수행 하 고 작업을 완료 해야 합니다.|  
  
 Sqlprepare와 **** 이전에 호출한 후 **sqlcolattribute** 는 데이터 소스가 *StatementHandle*와 연결 된 SQL 문을 평가 하는 시점에 따라 **sqlprepare** 또는 **sqlprepare**에서 반환 될 수 있는 모든 **SQLSTATE를 반환할**수 있습니다.  
  
 성능상의 이유로 응용 프로그램은 문을 실행 하기 전에 **Sqlcolattribute** 를 호출 하면 안 됩니다.  
  
## <a name="comments"></a>주석  
 응용 프로그램이 **Sqlcolattribute**에서 반환 하는 정보를 사용 하는 방법에 대 한 자세한 내용은 [결과 집합 메타 데이터](../../../odbc/reference/develop-app/result-set-metadata.md)를 참조 하세요.  
  
 **Sqlcolattribute** 는 \* *NumericAttributePtr* 또는 \* *CharacterAttributePtr*에서 정보를 반환 합니다. 정수 정보는 \* *NumericAttributePtr* 에서 sqllen 값으로 반환 됩니다. 모든 다른 형식의 정보는 \* *CharacterAttributePtr*에서 반환 됩니다. \* *NumericAttributePtr*에서 정보가 반환 되 면 드라이버는 *CharacterAttributePtr*, *bufferlength*및 *StringLengthPtr*를 무시 합니다. \* *CharacterAttributePtr*에서 정보가 반환 되 면 드라이버는 *NumericAttributePtr*를 무시 합니다.  
  
 **Sqlcolattribute** 는 IRD의 설명자 필드에서 값을 반환 합니다. 함수는 설명자 핸들이 아니라 문 핸들을 사용 하 여 호출 됩니다. 이 섹션 뒷부분에 나열 된 *FieldIdentifier* 값에 대 한 **sqlcolattribute** 에서 반환 하는 값은 적절 한 IRD 핸들을 사용 하 여 **SQLGetDescField** 를 호출 하 여 검색할 수도 있습니다.  
  
 현재 정의 된 설명자 필드, 해당 필드에 대 한 정보가 반환 되는 인수 및이에 대 한 정보가 반환 되는 인수는이 섹션의 뒷부분에 나와 있습니다. 다른 데이터 원본을 활용 하기 위해 드라이버에서 추가 설명자 유형을 정의할 수 있습니다.  
  
 ODBC 3. *x* 드라이버는 각 설명자 필드에 대 한 값을 반환 해야 합니다. 설명자 필드가 드라이버 또는 데이터 원본에 적용 되지 않고 달리 지정 되지 않은 경우 드라이버는 \* *StringLengthPtr* 에서 0을 반환 하거나 **CharacterAttributePtr*에 빈 문자열을 반환 합니다.  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 ODBC 3. *x* 함수 **sqlcolattribute** 는 사용 되지 않는 ODBC 2를 대체 합니다. *x* 함수 **sqlcolattributes**. **Sqlcolattributes** 를 **sqlcolattributes** 에 매핑할 때 (ODBC 2* 인 경우) x* 응용 프로그램이 ODBC 3에서 작동 하 고 있습니다. *x* 드라이버)를 만들거나 **sqlcolattribute** 를 **sqlcolattribute** (ODBC 3 인 경우)에 매핑합니다.* x* 응용 프로그램에서 ODBC 2를 사용 하 고 있습니다. *x* 드라이버) 드라이버 관리자는 *FieldIdentifier* 값을를 통해 전달 하거나, 새 값에 매핑하거나, 다음과 같이 오류를 반환 합니다.  
  
> [!NOTE]  
>  ODBC 3의 *FieldIdentifier* 값에 사용 되는 접두사입니다. *x* 는 ODBC 2에서 사용 된 것에서 변경 되었습니다. *x*. 새 접두사는 "SQL_DESC"입니다. 이전 접두사는 "SQL_COLUMN"입니다.  
  
-   ODBC 2의 **#define** 값 이면입니다. *x* *FieldIdentifier* 는 ODBC 3의 **#define** 값과 동일 합니다. *x* *FieldIdentifier*함수 호출의 값이 전달 됩니다.  
  
-   ODBC 2의 **#define** 값입니다. *x* *FieldIdentifiers* SQL_COLUMN_LENGTH, SQL_COLUMN_PRECISION 및 SQL_COLUMN_SCALE는 ODBC 3의 **#define** 값과 다릅니다. *x* *FieldIdentifiers* SQL_DESC_PRECISION, SQL_DESC_SCALE 및 SQL_DESC_LENGTH. ODBC 2. *x* 드라이버는 ODBC 2만 지원 해야 합니다. *x* 값입니다. ODBC 3. *x* 드라이버는 이러한 세 *FieldIdentifiers*의 "SQL_COLUMN" 및 "SQL_DESC" 값을 모두 지원 해야 합니다. 전체 자릿수, 소수 자릿수 및 길이는 ODBC 3에서 다르게 정의 되므로 이러한 값은 서로 다릅니다. *x* 는 ODBC 2에 있던 것 보다입니다. *x*. 자세한 내용은 [열 크기, 10 진수 숫자, 전송 옥텟 길이 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)를 참조 하세요.  
  
-   ODBC 2의 **#define** 값 이면입니다. *x* *FieldIdentifier* 는 ODBC 3의 **#define** 값과 다릅니다. *x* *FieldIdentifier*는 COUNT, NAME 및 NULLABLE 값을 사용 하 여 발생 하는 것 처럼 함수 호출의 값이 해당 값에 매핑됩니다. 예를 들어 SQL_COLUMN_COUNT SQL_DESC_COUNT에 매핑되고 SQL_DESC_COUNT 매핑의 방향에 따라 SQL_COLUMN_COUNT에 매핑됩니다.  
  
-   *FieldIdentifier* 가 ODBC 3의 새 값 이면입니다. *x*-ODBC 2에 해당 값이 없는 경우 *x*는 ODBC 3 일 때 매핑되지 않습니다. *x* 응용 프로그램은 ODBC 2의 **sqlcolattribute** 에 대 한 호출에서이를 사용 합니다. *x* 드라이버 및 호출은 SQLSTATE HY091 (잘못 된 설명자 필드 식별자)를 반환 합니다.  
  
 다음 표에서는 **Sqlcolattribute**에서 반환 되는 설명자 유형을 나열 합니다. *NumericAttributePtr* 값의 형식은 **sqllen \* **입니다.  
  
|*FieldIdentifier*|정보<br /><br /> 반환 된|Description|  
|-----------------------|---------------------------------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE (ODBC 1.0)|*NumericAttributePtr*|열이 자동 증가 열인지 여부를 SQL_TRUE 합니다.<br /><br /> 열이 자동 증가 열이 아니거나 숫자가 아닌 경우 SQL_FALSE 합니다.<br /><br /> 이 필드는 숫자 데이터 형식 열에만 유효 합니다. 응용 프로그램은 autoincrement 열을 포함 하는 행에 값을 삽입할 수 있지만 일반적으로 열의 값을 업데이트할 수 없습니다.<br /><br /> Autoincrement 열에 삽입을 수행 하는 경우 삽입 시 열에 고유한 값이 삽입 됩니다. 증가값은 정의 되지 않지만 데이터 원본에만 해당 됩니다. 응용 프로그램에서는 autoincrement 열이 특정 지점에서 시작 하거나 특정 값 만큼 증가 하는 것으로 가정 하지 않아야 합니다.|  
|SQL_DESC_BASE_COLUMN_NAME (ODBC 3.0)|*CharacterAttributePtr*|결과 집합 열의 기본 열 이름입니다. 식 열의 경우와 같이 기본 열 이름이 없는 경우이 변수에는 빈 문자열이 포함 됩니다.<br /><br /> 이 정보는 읽기 전용 필드인 IRD의 SQL_DESC_BASE_COLUMN_NAME 레코드 필드에서 반환 됩니다.|  
|SQL_DESC_BASE_TABLE_NAME (ODBC 3.0)|*CharacterAttributePtr*|열을 포함 하는 기본 테이블의 이름입니다. 기본 테이블 이름을 정의할 수 없거나 해당 사항이 적용 되지 않는 경우이 변수에는 빈 문자열이 포함 됩니다.<br /><br /> 이 정보는 읽기 전용 필드인 IRD의 SQL_DESC_BASE_TABLE_NAME 레코드 필드에서 반환 됩니다.|  
|SQL_DESC_CASE_SENSITIVE (ODBC 1.0)|*NumericAttributePtr*|열이 데이터 정렬과 비교 시 대/소문자를 구분 하 여 처리 되는 경우 SQL_TRUE 합니다.<br /><br /> 열이 데이터 정렬 및 비교에 대 한 대/소문자 구분으로 처리 되지 않거나 문자가 아닌 여부를 SQL_FALSE 합니다.|  
|SQL_DESC_CATALOG_NAME (ODBC 2.0)|*CharacterAttributePtr*|열이 포함 된 테이블의 카탈로그입니다. 반환 된 값은 열이 식인 경우 또는 열이 뷰의 일부인 경우에는 구현 시 정의 됩니다. 데이터 원본에서 카탈로그를 지원 하지 않거나 카탈로그 이름을 확인할 수 없는 경우 빈 문자열이 반환 됩니다. 이 VARCHAR 레코드 필드는 128 자로 제한 되지 않습니다.|  
|SQL_DESC_CONCISE_TYPE (ODBC 1.0)|*NumericAttributePtr*|간결한 데이터 형식입니다.<br /><br /> Datetime 및 interval 데이터 형식의 경우이 필드는 간결한 데이터 형식을 반환 합니다. 예를 들어 SQL_TYPE_TIME 또는 SQL_INTERVAL_YEAR입니다. 자세한 내용은 부록 D: 데이터 형식의 [데이터 형식 식별자 및 설명자](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) 를 참조 하세요.<br /><br /> 이 정보는 IRD의 레코드 SQL_DESC_CONCISE_TYPE 필드에서 반환 됩니다.|  
|SQL_DESC_COUNT (ODBC 1.0)|*NumericAttributePtr*|결과 집합에서 사용할 수 있는 열 수입니다. 결과 집합에 열이 없으면 0이 반환 됩니다. *Columnnumber* 인수의 값은 무시 됩니다.<br /><br /> 이 정보는 IRD의 헤더 SQL_DESC_COUNT 필드에서 반환 됩니다.|  
|SQL_DESC_DISPLAY_SIZE (ODBC 1.0)|*NumericAttributePtr*|열의 데이터를 표시 하는 데 필요한 최대 문자 수입니다. 표시 크기에 대 한 자세한 내용은 [열 크기, 10 진수 숫자, 전송 옥텟 길이 및](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 D: 데이터 형식의 표시 크기를 참조 하세요.|  
|SQL_DESC_FIXED_PREC_SCALE (ODBC 1.0)|*NumericAttributePtr*|열에 데이터 원본에 해당 하는 고정 전체 자릿수 및 0이 아닌 소수 자릿수가 있으면 SQL_TRUE 합니다.<br /><br /> 열의 고정 전체 자릿수와 0이 아닌 소수 자릿수가 데이터 원본에 해당 하는 경우 SQL_FALSE 합니다.|  
|SQL_DESC_LABEL (ODBC 2.0)|*CharacterAttributePtr*|열 레이블 또는 제목입니다. 예를 들어 이름이 EmpName 인 열은 Employee Name으로 표시 되거나 별칭으로 레이블을 지정할 수 있습니다.<br /><br /> 열에 레이블이 없으면 열 이름이 반환 됩니다. 열에 레이블이 없고 이름이 지정 되지 않은 경우 빈 문자열이 반환 됩니다.|  
|SQL_DESC_LENGTH (ODBC 3.0)|*NumericAttributePtr*|문자열 또는 이진 데이터 형식의 최대 또는 실제 문자 길이인 숫자 값입니다. 고정 길이 데이터 형식의 최대 문자 길이 또는 가변 길이 데이터 형식에 대 한 실제 문자 길이입니다. 해당 값은 항상 문자열을 종료 하는 null 종료 바이트를 제외 합니다.<br /><br /> 이 정보는 IRD의 레코드 SQL_DESC_LENGTH 필드에서 반환 됩니다.<br /><br /> 길이에 대 한 자세한 내용은 [열 크기, 10 진수 숫자, 전송 옥텟 길이 및](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 D: 데이터 형식의 표시 크기를 참조 하세요.|  
|SQL_DESC_LITERAL_PREFIX (ODBC 3.0)|*CharacterAttributePtr*|이 VARCHAR (128) 레코드 필드는 드라이버에서이 데이터 형식의 리터럴에 대 한 접두사로 인식 하는 문자를 포함 합니다. 이 필드에는 리터럴 접두사가 적용 되지 않는 데이터 형식에 대 한 빈 문자열이 포함 되어 있습니다. 자세한 내용은 [리터럴 접두사 및 접미사](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)를 참조 하세요.|  
|SQL_DESC_LITERAL_SUFFIX (ODBC 3.0)|*CharacterAttributePtr*|이 VARCHAR (128) 레코드 필드는 드라이버에서이 데이터 형식의 리터럴에 대 한 접미사로 인식 하는 문자를 포함 합니다. 이 필드에는 리터럴 접미사가 적용 되지 않는 데이터 형식에 대 한 빈 문자열이 포함 되어 있습니다. 자세한 내용은 [리터럴 접두사 및 접미사](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)를 참조 하세요.|  
|SQL_DESC_LOCAL_TYPE_NAME (ODBC 3.0)|*CharacterAttributePtr*|이 VARCHAR (128) 레코드 필드에는 데이터 형식의 일반 이름과 다를 수 있는 데이터 형식에 대 한 지역화 된 (네이티브 언어) 이름이 포함 됩니다. 지역화 된 이름이 없으면 빈 문자열이 반환 됩니다. 이 필드는 표시 목적 으로만 사용 됩니다. 문자열의 문자 집합은 로캘에 따라 다르며 일반적으로 서버의 기본 문자 집합입니다.|  
|SQL_DESC_NAME (ODBC 3.0)|*CharacterAttributePtr*|열 별칭입니다 (적용 되는 경우). 열 별칭이 적용 되지 않으면 열 이름이 반환 됩니다. 두 경우 모두 SQL_DESC_UNNAMED은 SQL_NAMED로 설정 됩니다. 열 이름이 나 열 별칭이 없으면 빈 문자열이 반환 되 고 SQL_DESC_UNNAMED SQL_UNNAMED로 설정 됩니다.<br /><br /> 이 정보는 IRD의 레코드 SQL_DESC_NAME 필드에서 반환 됩니다.|  
|SQL_DESC_NULLABLE (ODBC 3.0)|*NumericAttributePtr*|열에 NULL 값을 사용할 수 있는 경우 null을 허용 SQL_. 열에 NULL 값이 없는 경우 SQL_NO_NULLS 합니다. 또는 열이 NULL 값을 허용 하는지 여부를 알 수 없는 경우에 SQL_NULLABLE_UNKNOWN 합니다.<br /><br /> 이 정보는 IRD의 레코드 SQL_DESC_NULLABLE 필드에서 반환 됩니다.|  
|SQL_DESC_NUM_PREC_RADIX (ODBC 3.0)|*NumericAttributePtr*|SQL_DESC_TYPE 필드의 데이터 형식이 근사치 숫자 데이터 형식인 경우에는 SQL_DESC_PRECISION 필드에 비트 수가 포함 되기 때문에이 SQLINTEGER 필드에 값이 2가 포함 됩니다. SQL_DESC_TYPE 필드의 데이터 형식이 정확한 숫자 데이터 형식인 경우에는 SQL_DESC_PRECISION 필드에 10 진수가 포함 되므로이 필드의 값은 10입니다. 숫자가 아닌 모든 데이터 형식에 대해이 필드는 0으로 설정 됩니다.|  
|SQL_DESC_OCTET_LENGTH (ODBC 3.0)|*NumericAttributePtr*|문자열 또는 이진 데이터 형식의 길이 (바이트)입니다. 고정 길이 문자 또는 이진 형식의 경우 실제 길이 (바이트)입니다. 가변 길이 문자 또는 이진 형식의 경우 최대 길이 (바이트)입니다. 이 값은 null 종결자를 포함 하지 않습니다.<br /><br /> 이 정보는 IRD의 레코드 SQL_DESC_OCTET_LENGTH 필드에서 반환 됩니다.<br /><br /> 길이에 대 한 자세한 내용은 [열 크기, 10 진수 숫자, 전송 옥텟 길이 및](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 D: 데이터 형식의 표시 크기를 참조 하세요.|  
|SQL_DESC_PRECISION (ODBC 3.0)|*NumericAttributePtr*|숫자 데이터 형식에 대 한 숫자 값은 해당 하는 전체 자릿수를 나타냅니다. 데이터 형식 SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP 및 시간 간격을 나타내는 모든 간격 데이터 형식에 대해 해당 값은 소수 자릿수 초 구성 요소에 적용 되는 전체 자릿수입니다.<br /><br /> 이 정보는 IRD의 레코드 SQL_DESC_PRECISION 필드에서 반환 됩니다.|  
|SQL_DESC_SCALE (ODBC 3.0)|*NumericAttributePtr*|숫자 데이터 형식에 적용 가능한 소수 자릿수를 나타내는 숫자 값입니다. DECIMAL 및 NUMERIC 데이터 형식의 경우 정의 된 소수 자릿수입니다. 다른 모든 데이터 형식에 대해서는 정의 되지 않습니다.<br /><br /> 이 정보는 IRD의 크기 조정 레코드 필드에서 반환 됩니다.|  
|SQL_DESC_SCHEMA_NAME (ODBC 2.0)|*CharacterAttributePtr*|열이 포함 된 테이블의 스키마입니다. 반환 된 값은 열이 식인 경우 또는 열이 뷰의 일부인 경우에는 구현 시 정의 됩니다. 데이터 원본에서 스키마를 지원 하지 않거나 스키마 이름을 확인할 수 없는 경우 빈 문자열이 반환 됩니다. 이 VARCHAR 레코드 필드는 128 자로 제한 되지 않습니다.|  
|SQL_DESC_SEARCHABLE (ODBC 1.0)|*NumericAttributePtr*|WHERE 절에서 열을 사용할 수 없는 경우 SQL_PRED_NONE 합니다. 이 값은 ODBC 2의 SQL_UNSEARCHABLE 값과 동일 합니다. *x*.)<br /><br /> WHERE 절에서 열을 사용할 수 있지만 LIKE 조건자를 사용 하 여 열을 사용할 수 있는지 여부를 SQL_PRED_CHAR 합니다. 이 값은 ODBC 2의 SQL_LIKE_ONLY 값과 동일 합니다. *x*.)<br /><br /> LIKE를 제외한 모든 비교 연산자가 있는 WHERE 절에서 열을 사용할 수 있는지 여부를 SQL_PRED_BASIC 합니다. 이 값은 ODBC 2의 SQL_EXCEPT_LIKE 값과 동일 합니다. *x*.)<br /><br /> WHERE 절에서 비교 연산자를 사용 하 여 열을 사용할 수 있는지 여부를 SQL_PRED_SEARCHABLE 합니다.<br /><br /> SQL_LONGVARCHAR 및 SQL_LONGVARBINARY 형식의 열은 일반적으로 SQL_PRED_CHAR을 반환 합니다.|  
|SQL_DESC_TABLE_NAME (ODBC 2.0)|*CharacterAttributePtr*|열을 포함하는 테이블의 이름입니다. 반환 된 값은 열이 식인 경우 또는 열이 뷰의 일부인 경우에는 구현 시 정의 됩니다.<br /><br /> 테이블 이름을 확인할 수 없는 경우 빈 문자열이 반환 됩니다.|  
|SQL_DESC_TYPE (ODBC 3.0)|*NumericAttributePtr*|SQL 데이터 형식을 지정 하는 숫자 값입니다.<br /><br /> *Columnnumber* 가 0 이면 가변 길이 책갈피에 대 한 SQL_BINARY가 반환 되 고 고정 길이 책갈피에 대 한 SQL_INTEGER 반환 됩니다.<br /><br /> Datetime 및 interval 데이터 형식의 경우이 필드는 자세한 데이터 형식인 SQL_DATETIME 또는 SQL_INTERVAL을 반환 합니다. 자세한 내용은 부록 D: 데이터 형식의 [데이터 형식 식별자 및 설명자](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) 를 참조 하세요.<br /><br /> 이 정보는 IRD의 레코드 SQL_DESC_TYPE 필드에서 반환 됩니다. **참고:**  ODBC 2에 대 한 작업을 수행 합니다. *x* 드라이버, 대신 SQL_DESC_CONCISE_TYPE를 사용 합니다.|  
|SQL_DESC_TYPE_NAME (ODBC 1.0)|*CharacterAttributePtr*|데이터 원본 종속 데이터 형식 이름입니다. 예를 들면 "CHAR", "VARCHAR", "MONEY", "LONG VARBINARY" 또는 "CHAR () FOR BIT DATA"입니다.<br /><br /> 형식을 알 수 없으면 빈 문자열이 반환 됩니다.|  
|SQL_DESC_UNNAMED (ODBC 3.0)|*NumericAttributePtr*|SQL_NAMED 또는 SQL_UNNAMED. IRD의 SQL_DESC_NAME 필드에 열 별칭 또는 열 이름이 포함 된 경우 SQL_NAMED 반환 됩니다. 열 이름 또는 열 별칭이 없으면 SQL_UNNAMED 반환 됩니다.<br /><br /> 이 정보는 IRD의 레코드 SQL_DESC_UNNAMED 필드에서 반환 됩니다.|  
|SQL_DESC_UNSIGNED (ODBC 1.0)|*NumericAttributePtr*|열이 부호 없는 열 (또는 숫자 아님) 인 경우 SQL_TRUE 합니다.<br /><br /> 열이 서명 된 경우 SQL_FALSE 합니다.|  
|SQL_DESC_UPDATABLE (ODBC 1.0)|*NumericAttributePtr*|열은 정의 된 상수에 대 한 값으로 설명 됩니다.<br /><br /> SQL_ATTR_READONLY SQL_ATTR_WRITE SQL_ATTR_READWRITE_UNKNOWN<br /><br /> SQL_DESC_UPDATABLE은 기본 테이블의 열이 아니라 결과 집합의 열에 대 한 업데이트 가능성을 설명 합니다. 결과 집합 열이 기반으로 하는 기본 열의 업데이트 가능성은이 필드의 값과 다를 수 있습니다. 열을 업데이트할 수 있는지 여부는 데이터 형식, 사용자 권한 및 결과 집합 자체의 정의를 기반으로 할 수 있습니다. 열을 업데이트할 수 있는지 명확 하지 않은 경우 SQL_ATTR_READWRITE_UNKNOWN 반환 되어야 합니다.|  
  
 **Sqlcolattribute** 는 **SQLDescribeCol**에 대 한 확장 가능한 대안입니다. **SQLDescribeCol** 는 ANSI-89 SQL을 기반으로 하는 고정 설명자 정보 집합을 반환 합니다. **Sqlcolattribute** 를 사용 하면 ANSI SQL-92 및 DBMS 공급 업체 확장에서 제공 하는 보다 광범위 한 설명자 정보 집합에 액세스할 수 있습니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|결과 집합의 열에 대 한 정보 반환|[SQLDescribeCol 함수](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|데이터 블록 가져오기 또는 결과 집합을 통한 스크롤|[SQLFetchScroll 함수(SQLFetchScroll Function)](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|여러 행의 데이터 페치|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
  
## <a name="example"></a>예제  
 다음 샘플 코드에서는 핸들 및 연결을 해제 하지 않습니다. 코드 샘플에서 핸들 및 문을 해제 하려면 [Sqlfreehandle 함수](../../../odbc/reference/syntax/sqlfreehandle-function.md), [샘플 ODBC 프로그램](../../../odbc/reference/sample-odbc-program.md)및 [SQLFreeStmt 함수](../../../odbc/reference/syntax/sqlfreestmt-function.md) 를 참조 하세요.  
  
```cpp  
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
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [샘플 ODBC 프로그램](../../../odbc/reference/sample-odbc-program.md)
