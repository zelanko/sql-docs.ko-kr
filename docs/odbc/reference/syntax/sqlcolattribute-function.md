---
title: SQLColAttribute 함수 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c94de3dfc7036277f8be56c401326cdab07a9606
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301293"
---
# <a name="sqlcolattribute-function"></a>SQLColAttribute 함수(SQLColAttribute Function)
**규칙**  
 버전 출시: ODBC 3.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLColAttribute** 결과 집합의 열에 대 한 설명자 정보를 반환 합니다. 설명자 정보는 문자 문자열, 설명자 종속 값 또는 정수 값으로 반환됩니다.  
  
> [!NOTE]  
>  드라이버 관리자가 이 함수를 ODBC 3에 매핑하는 기능에 대한 자세한 내용을 참조하십시오. *x* 응용 프로그램이 ODBC 2로 작동합니다. *x* 드라이버, [응용 프로그램의 이전 버전과의 호환성에 대한 매핑 교체 함수를](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)참조하십시오.  
  
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
 *명령문 핸들*  
 [입력] 명령문 핸들입니다.  
  
 *ColumnNumber*  
 [입력] 필드 값을 검색할 IRD의 레코드 수입니다. 이 인수는 1부터 시작하여 열 순서를 증가시켜 순차적으로 정렬된 결과 데이터의 열 수에 해당합니다. 열은 임의의 순서로 설명할 수 있습니다.  
  
 열 0은 이 인수에 지정할 수 있지만 SQL_DESC_TYPE 및 SQL_DESC_OCTET_LENGTH 제외한 모든 값은 정의되지 않은 값을 반환합니다.  
  
 *FieldIdentifier*  
 [입력] 설명자 핸들입니다. 이 핸들은 IRD에서 쿼리할 필드(예: SQL_COLUMN_TABLE_NAME)를 정의합니다.  
  
 *CharacterAttributePtr*  
 [출력] 필드가 문자 문자열인 경우 *IRD의 ColumnNumber* 행의 *FieldIdentifier* 필드의 값을 반환할 버퍼를 포인터합니다. 그렇지 않으면 필드가 사용되지 않습니다.  
  
 *CharacterAttributePtr이* NULL인 경우 *StringLengthPtr은* *CharacterAttributePtr에서*가리키는 버퍼에서 반환할 수 있는 총 바이트 수(문자 데이터에 대한 null 종료 문자 제외)를 반환합니다.  
  
 *버퍼 길이*  
 [입력] *FieldIdentifier가* ODBC 정의 필드이고 *CharacterAttributePtr이* 문자 문자열 또는 이진 버퍼를 가리키는 \*경우 이 인수는 *CharacterAttributePtr*의 길이여야 합니다. *FieldIdentifier가* ODBC 정의 필드이고 \* *CharacterAttribute*Ptr이 정수인 경우 이 필드는 무시됩니다. CharacterAttributePtr이 유니코드 문자열인 **경우(SQLColAttributeW를**호출할 때) *BufferLength* 인수는 짝수여야 합니다. * \** *FieldIdentifier가* 드라이버 정의 필드인 경우 응용 프로그램은 *BufferLength* 인수를 설정하여 드라이버 관리자에 필드의 특성을 나타냅니다. *BufferLength에는* 다음 값이 있을 수 있습니다.  
  
-   *CharacterAttributePtr이* 포인터에 대한 포인터인 경우 *BufferLength는* SQL_IS_POINTER 값을 가져야 합니다.  
  
-   *CharacterAttributePtr이* 문자 문자열에 대한 포인터인 경우 *버퍼 길이는* 버퍼의 길이입니다.  
  
-   *CharacterAttributePtr이* 이진 버퍼에 대한 포인터인 경우 응용 프로그램은*SQL_LEN_BINARY_ATTR(길이)* 매크로의 결과를 *BufferLength*에 배치합니다. 이렇게 하면 *버퍼길이에*음수 값이 배치됩니다.  
  
-   *CharacterAttributePtr이* 고정 길이 데이터 형식에 대한 포인터인 경우 *버퍼길이는* SQL_IS_INTEGER, SQL_IS_UNINTEGER, SQL_SMALLINT 또는 SQLUSMALLINT 중 하나여야 합니다.  
  
 *문자열길이Ptr*  
 [출력] **CharacterAttributePtr에서*반환할 수 있는 총 바이트 수(문자 데이터에 대한 null-termination 바이트 제외)를 반환하는 버퍼에 대한 포인터입니다.  
  
 문자 데이터의 경우 반환할 수 있는 바이트 수가 *BufferLength보다*크거나 같으면 \* *CharacterAttributePtr의* 설명자 정보는 Null 종료 문자의 길이를 뺀 *BufferLength로* 잘리고 드라이버에 의해 null-종료됩니다.  
  
 다른 모든 유형의 데이터에 대해 *BufferLength* 값은 무시되고 드라이버는 **CharacterAttributePtr의* 크기를 32비트로 가정합니다.  
  
 *숫자 속성 Ptr*  
 [출력] 필드가 SQL_DESC_COLUMN_LENGTH 같은 숫자 설명자 유형인 *경우, IRD의 ColumnNumber* 행의 *FieldIdentifier* 필드에 있는 값을 반환하는 정수 버퍼에 대한 포인터입니다. 그렇지 않으면 필드가 사용되지 않습니다. 일부 드라이버는 버퍼의 하위 32비트 또는 16비트만 작성하고 상위 순서의 비트를 변경하지 않고 그대로 둘 수 있습니다. 따라서 응용 프로그램은 이 함수를 호출하기 전에 값을 0으로 초기화해야 합니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLColAttribute** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환하는 경우 *핸들 유형* SQL_HANDLE_STMT 및 *문 핸들*핸들을 사용하는 *Handle* **SQLGetDiagRec를** 호출하여 연결된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 **SQLColAttribute에서** 일반적으로 반환하는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01004|문자열 데이터, 오른쪽 잘린|버퍼 \* *CharacterAttributePtr* 전체 문자열 값을 반환할 만큼 크지 않았기 때문에 문자열 값이 잘렸습니다. 잘린 문자열 값의 길이는 **StringLengthPtr에서*반환됩니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|07005|*커서 사양이* 아닌 준비된 문|*StatementHandle와* 연관된 명령문이 결과 집합을 반환하지 않았고 *FieldIdentifier가* SQL_DESC_COUNT 않았습니다. 설명할 열이 없습니다.|  
|07009|잘못된 설명자 인덱스|(DM) *ColumnNumber에* 대해 지정된 값이 0이고 SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_OFF.<br /><br /> *ColumnNumber* 인수에 대해 지정된 값은 결과 집합의 열 수보다 큽합니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. 진단 데이터 구조에서 **SQLGetDiagField에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다.|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY08|작업 취소됨|*명령문 핸들*에 대해 비동기 처리가 활성화되었습니다. 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** *명령문 핸들*에서 호출되었습니다. 그런 다음 *함수가 StatementHandle*에서 다시 호출되었습니다.<br /><br /> 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle에서* 호출되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. SQLColAttribute이 호출될 때 이 아인크로니우스 함수는 여전히 실행 중이었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *명령문 핸들에* 대해 호출되고 SQL_PARAM_DATA_AVAILABLE 반환되었습니다. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.<br /><br /> (DM) 이 함수는 **SQLPrepare,** **SQLExecDirect**또는 *문 핸들에*대한 카탈로그 함수를 호출하기 전에 호출되었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 함수 (이 하나) *StatementHandle에* 대 한 호출 하 고이 함수를 호출 될 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *문 핸들에* 대해 호출되고 SQL_NEED_DATA 반환되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|(DM) * \*CharacterAttributePtr은* 문자 문자열이며 *버퍼길이는* 0보다 작지만 SQL_NTS 같지는 않습니다.|  
|HY091|잘못된 설명자 필드 식별자|인수 *FieldIdentifier에* 대해 지정된 값은 정의된 값 중 하나가 아니며 구현 정의 값이 아닙니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|하이크00|드라이버를 할 수 없습니다.|인수 *FieldIdentifier에* 대해 지정된 값은 드라이버에서 지원되지 않았습니다.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle와* 연결된 드라이버는 함수를 지원하지 않습니다.|  
|IM017|비동기 알림 모드에서 폴링이 비활성화됨|알림 모델을 사용할 때마다 폴링이 비활성화됩니다.|  
|IM018|**SQLCompleteAsync이** 핸들에 이전 비동기 작업을 완료 하기 위해 호출 되지 않았습니다.|핸들의 이전 함수 호출이 SQL_STILL_EXECUTING 반환하고 알림 모드가 활성화된 경우 **SQLCompleteAsync를** 호출하여 사후 처리를 수행하여 작업을 완료해야 합니다.|  
  
 **SQLPrepare** 후 와 **SQL실행**하기 전에 호출 하는 경우 **SQLColAttribute** **SQLPrepare** 또는 **SQLExecute에**의해 반환될 수 있는 모든 SQLSTATE를 반환할 수 있습니다., 데이터 *원본은 문 핸들과*관련 된 SQL 문을 평가 하는 시기에 따라 .  
  
 성능상의 이유로 응용 프로그램은 문을 실행하기 전에 **SQLColAttribute를** 호출해서는 안 됩니다.  
  
## <a name="comments"></a>주석  
 응용 프로그램에서 **SQLColAttribute에서**반환된 정보를 사용하는 방법에 대한 자세한 내용은 [결과 집합 메타데이터를](../../../odbc/reference/develop-app/result-set-metadata.md)참조하십시오.  
  
 **SQLColAttribute는** 숫자 \* *특성Ptr* 또는 \* *CharacterAttributePtr에서*정보를 반환합니다. 정수 정보는 SQLLEN \*값으로 *numericAttributePtr에서* 반환됩니다. 다른 모든 형식의 정보는 \* *CharacterAttributePtr에서*반환됩니다. 정보가 \* *numericAttributePtr에서*반환되면 드라이버는 *CharacterAttributePtr,* *버퍼 길이*및 *StringLengthPtr*을 무시합니다. \* *CharacterAttributePtr에서*정보가 반환되면 드라이버는 *숫자 characterAttributePtr*을 무시합니다.  
  
 **SQLColAttribute는** IRD의 설명자 필드에서 값을 반환합니다. 함수는 설명자 핸들이 아닌 문 핸들을 통해 호출됩니다. 이 섹션의 나중에 나열된 *필드 식별자* 값에 대한 **SQLColAttribute에서** 반환된 값은 적절한 IRD 핸들을 사용 하 여 **SQLGetDescField를** 호출 하 여 검색할 수도 있습니다.  
  
 현재 정의된 설명자 필드, ODBC가 도입된 버전 및 정보가 반환되는 인수는 이 섹션의 후반부에 표시됩니다. 드라이버가 다른 데이터 원본을 활용하기 위해 더 많은 설명자 형식을 정의할 수 있습니다.  
  
 ODBC 3. *x* 드라이버는 각 설명자 필드에 대한 값을 반환해야 합니다. 설명자 필드가 드라이버 또는 데이터 원본에 적용되지 않고 달리 명시되지 않는 \*한 드라이버는 *StringLengthPtr에서* 0 또는 **CharacterAttributePtr의*빈 문자열을 반환합니다.  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 ODBC 3. *x* 함수 **SQLColAttribute는** 더 이상 사용되지 않습니다 ODBC 2를 대체합니다. *x* 함수 **SQLColAttributes**. **SQLColAttributes를** **SQLColAttribute에** 매핑할 때(ODBC 2인 경우)* x* 응용 프로그램이 ODBC 3로 작동합니다. *x* 드라이버) 또는 **SQLColAttributes에 SQLColAttribute매핑(ODBC** 3인 경우) **SQLColAttribute** * x* 응용 프로그램이 ODBC 2로 작동합니다. *x* driver) 드라이버 관리자는 *FieldIdentifier* 값을 통해 전달하거나, 새 값에 매핑하거나, 다음과 같이 오류를 반환합니다.  
  
> [!NOTE]  
>  ODBC 3의 *필드 식별자* 값에 사용되는 접두사입니다. *x는* ODBC 2에서 사용되는 것과 변경되었습니다. *x*. 새 접두사는 "SQL_DESC"입니다. 이전 접두사는 "SQL_COLUMN"이었습니다.  
  
-   ODBC 2의 **#define** 값인 경우. *x* *필드식별자는* ODBC 3의 **#define** 값과 동일합니다. *x* *FieldIdentifier*- 함수 호출의 값이 방금 통과됩니다.  
  
-   ODBC 2의 **#define** 값입니다. *x* *필드식별자* SQL_COLUMN_LENGTH, SQL_COLUMN_PRECISION 및 SQL_COLUMN_SCALE ODBC 3의 **#define** 값과 다릅니다. *x* *필드식별자* SQL_DESC_PRECISION, SQL_DESC_SCALE 및 SQL_DESC_LENGTH. ODBC 2. *x* 드라이버는 ODBC 2만 지원하면 됩니다. *x 값입니다.* ODBC 3. *x* 드라이버는 이 세 *가지 FieldIdentifiers에*대해 "SQL_COLUMN" 및 "SQL_DESC" 값을 모두 지원해야 합니다. 이러한 값은 ODBC 3에서 정밀도, 배율 및 길이가 다르게 정의되기 때문에 다릅니다. *X는* ODBC 2에 있는 것보다 더 많았습니다. *x*. 자세한 내용은 [열 크기, 소수 자릿수, 전송 옥텟 길이 및 디스플레이 크기를](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)참조하십시오.  
  
-   ODBC 2의 **#define** 값인 경우. *x* *필드식별자는* ODBC 3의 **#define** 값과 다릅니다. *x* Count, NAME 및 NULLABLE 값에서 발생하는 경우 x *FieldIdentifier는*함수 호출의 값이 해당 값에 매핑됩니다. 예를 들어 SQL_COLUMN_COUNT SQL_DESC_COUNT 매핑되고 매핑 방향에 따라 SQL_DESC_COUNT SQL_COLUMN_COUNT 매핑됩니다.  
  
-   *필드식별자가* ODBC 3의 새 값인 경우. *x*, ODBC 2에 해당 값이 없습니다. *x*, ODBC 3일 때 매핑되지 않습니다. *x* 응용 프로그램은 ODBC 2에서 **SQLColAttribute에** 대한 호출에서 사용합니다. *x* 드라이버및 호출은 SQLSTATE HY091 (잘못된 설명자 필드 식별자)를 반환합니다.  
  
 다음 표에는 **SQLColAttribute**에서 반환된 설명자 형식이 나열되어 있습니다. *숫자속성 Ptr* 값의 형식은 ** \*SQLLEN입니다. **  
  
|*FieldIdentifier*|정보<br /><br /> 반환된 상태로|설명|  
|-----------------------|---------------------------------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE (ODBC 1.0)|*숫자 속성 Ptr*|열이 자동 증분 열인 경우 SQL_TRUE.<br /><br /> SQL_FALSE 열이 자동 증가 열이 아니거나 숫자가 아닌 경우입니다.<br /><br /> 이 필드는 숫자 데이터 형식 열에만 유효합니다. 응용 프로그램은 자동 증가 열을 포함하는 행에 값을 삽입할 수 있지만 일반적으로 열의 값을 업데이트할 수는 없습니다.<br /><br /> 인서트가 자동 증분 열에 만들어지면 삽입 시 고유한 값이 열에 삽입됩니다. 증분은 정의되지 않지만 데이터 원본에 따라 다릅니다. 응용 프로그램은 자동 증분 열이 특정 지점에서 시작하거나 특정 값으로 증분한다고 가정해서는 안 됩니다.|  
|SQL_DESC_BASE_COLUMN_NAME (ODBC 3.0)|*CharacterAttributePtr*|결과 집합 열의 기준 열 이름입니다. 식인 열의 경우와 같이 기준 열 이름이 없는 경우 이 변수에는 빈 문자열이 포함됩니다.<br /><br /> 이 정보는 읽기 전용 필드인 IRD의 SQL_DESC_BASE_COLUMN_NAME 레코드 필드에서 반환됩니다.|  
|SQL_DESC_BASE_TABLE_NAME (ODBC 3.0)|*CharacterAttributePtr*|열을 포함하는 기준 테이블의 이름입니다. 기본 테이블 이름을 정의할 수 없거나 적용할 수 없는 경우 이 변수에는 빈 문자열이 포함됩니다.<br /><br /> 이 정보는 읽기 전용 필드인 IRD의 SQL_DESC_BASE_TABLE_NAME 레코드 필드에서 반환됩니다.|  
|SQL_DESC_CASE_SENSITIVE (ODBC 1.0)|*숫자 속성 Ptr*|SQL_TRUE 컬럼이 데이터 정렬 및 비교에 대소한 대/소문자 구분으로 처리되는 경우를 SQL_TRUE.<br /><br /> SQL_FALSE 컬럼이 데이터 정렬 및 비교에 대 한 대/소문자로 처리 되지 않거나 문자가 아닌 경우입니다.|  
|SQL_DESC_CATALOG_NAME (ODBC 2.0)|*CharacterAttributePtr*|열이 포함된 테이블의 카탈로그입니다. 반환된 값은 열이 식이거나 열이 뷰의 일부인 경우 구현 정의됩니다. 데이터 원본이 카탈로그를 지원하지 않거나 카탈로그 이름을 확인할 수 없는 경우 빈 문자열이 반환됩니다. 이 VARCHAR 레코드 필드는 128자로 제한되지 않습니다.|  
|SQL_DESC_CONCISE_TYPE (ODBC 1.0)|*숫자 속성 Ptr*|간결한 데이터 형식입니다.<br /><br /> datetime 및 간격 데이터 형식의 경우 이 필드는 간결한 데이터 형식을 반환합니다. 예를 들어, SQL_TYPE_TIME 또는 SQL_INTERVAL_YEAR. 자세한 내용은 부록 D: 데이터 형식의 [데이터 형식 식별자 및 설명자를](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) 참조하십시오.<br /><br /> 이 정보는 IRD의 SQL_DESC_CONCISE_TYPE 레코드 필드에서 반환됩니다.|  
|SQL_DESC_COUNT (ODBC 1.0)|*숫자 속성 Ptr*|결과 집합에서 사용할 수 있는 열 수입니다. 결과 집합에 열이 없는 경우 0을 반환합니다. *ColumnNumber* 인수의 값은 무시됩니다.<br /><br /> 이 정보는 IRD의 SQL_DESC_COUNT 헤더 필드에서 반환됩니다.|  
|SQL_DESC_DISPLAY_SIZE (ODBC 1.0)|*숫자 속성 Ptr*|열에서 데이터를 표시하는 데 필요한 최대 문자 수입니다. 디스플레이 크기에 대한 자세한 내용은 [열 크기, 소수 자릿수, 전송 옥텟 길이 및](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 D: 데이터 유형의 디스플레이 크기를 참조하십시오.|  
|SQL_DESC_FIXED_PREC_SCALE (ODBC 1.0)|*숫자 속성 Ptr*|SQL_TRUE 열에 데이터 원본에 특정한 고정 정밀도와 0이 아닌 축척이 있는 경우를 SQL_TRUE.<br /><br /> SQL_FALSE 열에 데이터 원본에 특정한 고정 정밀도와 0이 아닌 축척이 없는 경우를 의미합니다.|  
|SQL_DESC_LABEL (ODBC 2.0)|*CharacterAttributePtr*|열 레이블 또는 제목입니다. 예를 들어 EmpName이라는 열은 직원 이름으로 레이블이 지정되거나 별칭으로 레이블이 지정될 수 있습니다.<br /><br /> 열에 레이블이 없는 경우 열 이름이 반환됩니다. 열의 레이블이 지정되지 않고 이름이 지정되지 않은 경우 빈 문자열이 반환됩니다.|  
|SQL_DESC_LENGTH (ODBC 3.0)|*숫자 속성 Ptr*|문자 문자열 또는 이진 데이터 형식의 최대 또는 실제 문자 길이인 숫자 값입니다. 고정 길이 데이터 형식의 최대 문자 길이 또는 가변 길이 데이터 형식의 실제 문자 길이입니다. 이 값은 항상 문자 문자열을 종료하는 null-termination 바이트를 제외합니다.<br /><br /> 이 정보는 IRD의 SQL_DESC_LENGTH 레코드 필드에서 반환됩니다.<br /><br /> 길이에 대한 자세한 내용은 [열 크기, 소수 자릿수, 전송 옥텟 길이 및](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 D: 데이터 유형의 표시 크기를 참조하십시오.|  
|SQL_DESC_LITERAL_PREFIX (ODBC 3.0)|*CharacterAttributePtr*|이 VARCHAR(128) 레코드 필드에는 드라이버가 이 데이터 형식의 리터럴에 대한 접두사로 인식하는 문자 또는 문자가 포함되어 있습니다. 이 필드에는 리터럴 접두사를 적용할 수 없는 데이터 형식에 대한 빈 문자열이 포함되어 있습니다. 자세한 내용은 [리터럴 접두사 및 접미사](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)를 참조하십시오.|  
|SQL_DESC_LITERAL_SUFFIX (ODBC 3.0)|*CharacterAttributePtr*|이 VARCHAR(128) 레코드 필드에는 드라이버가 이 데이터 형식의 리터럴에 대한 접미사로 인식하는 문자 또는 문자가 포함되어 있습니다. 이 필드에는 리터럴 접미사를 적용할 수 없는 데이터 형식에 대한 빈 문자열이 포함되어 있습니다. 자세한 내용은 [리터럴 접두사 및 접미사](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)를 참조하십시오.|  
|SQL_DESC_LOCAL_TYPE_NAME (ODBC 3.0)|*CharacterAttributePtr*|이 VARCHAR(128) 레코드 필드에는 데이터 형식의 일반 이름과 다를 수 있는 데이터 형식에 대한 지역화된(기본 언어) 이름이 포함되어 있습니다. 지역화된 이름이 없는 경우 빈 문자열이 반환됩니다. 이 필드는 표시용도로만 사용됩니다. 문자열의 문자 집합은 로캘에 종속되며 일반적으로 서버의 기본 문자 집합입니다.|  
|SQL_DESC_NAME (ODBC 3.0)|*CharacterAttributePtr*|열 별칭(적용되는 경우)입니다. 열 별칭이 적용되지 않으면 열 이름이 반환됩니다. 두 경우 모두 SQL_DESC_UNNAMED SQL_NAMED 설정됩니다. 열 이름이나 열 별칭이 없는 경우 빈 문자열이 반환되고 SQL_DESC_UNNAMED SQL_UNNAMED 설정됩니다.<br /><br /> 이 정보는 IRD의 SQL_DESC_NAME 레코드 필드에서 반환됩니다.|  
|SQL_DESC_NULLABLE (ODBC 3.0)|*숫자 속성 Ptr*|열에 NULL 값을 가질 수 있는 경우 nullable이 SQL_. 열에 NULL 값이 없는 경우 SQL_NO_NULLS. 또는 열이 NULL 값을 허용하는지 여부를 알 수 없는 경우 SQL_NULLABLE_UNKNOWN.<br /><br /> 이 정보는 IRD의 SQL_DESC_NULLABLE 레코드 필드에서 반환됩니다.|  
|SQL_DESC_NUM_PREC_RADIX (ODBC 3.0)|*숫자 속성 Ptr*|SQL_DESC_TYPE 필드의 데이터 형식이 대략적인 숫자 데이터 형식인 경우 SQL_DESC_PRECISION 필드에 비트 수가 포함되어 있으므로 이 SQLINTEGER 필드에는 값이 2입니다. SQL_DESC_TYPE 필드의 데이터 형식이 정확한 숫자 데이터 형식인 경우 SQL_DESC_PRECISION 필드에 소수 자릿수가 포함되어 있으므로 이 필드에는 값이 10입니다. 이 필드는 숫자가 아닌 모든 데이터 형식에 대해 0으로 설정됩니다.|  
|SQL_DESC_OCTET_LENGTH (ODBC 3.0)|*숫자 속성 Ptr*|문자열 또는 이진 데이터 형식의 길이(바이트)입니다. 고정 길이 문자 또는 이진 형식의 경우 실제 길이는 바이트입니다. 가변 길이 문자 또는 이진 형식의 경우 이 값은 바이트의 최대 길이입니다. 이 값에는 null 종사터가 포함되지 않습니다.<br /><br /> 이 정보는 IRD의 SQL_DESC_OCTET_LENGTH 레코드 필드에서 반환됩니다.<br /><br /> 길이에 대한 자세한 내용은 [열 크기, 소수 자릿수, 전송 옥텟 길이 및](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 D: 데이터 유형의 표시 크기를 참조하십시오.|  
|SQL_DESC_PRECISION (ODBC 3.0)|*숫자 속성 Ptr*|숫자 데이터 형식의 경우 해당 정밀도를 나타내는 숫자 값입니다. 시간 간격을 나타내는 데이터 형식 SQL_TYPE_TIME SQL_TYPE_TIMESTAMP 및 모든 간격 데이터 형식의 경우 해당 값은 분수 초 구성 요소의 적용 가능한 정밀도입니다.<br /><br /> 이 정보는 IRD의 SQL_DESC_PRECISION 레코드 필드에서 반환됩니다.|  
|SQL_DESC_SCALE (ODBC 3.0)|*숫자 속성 Ptr*|숫자 데이터 형식에 적용할 수 있는 축척인 숫자 값입니다. 소수점 및 숫자 데이터 형식의 경우 정의된 축척입니다. 다른 모든 데이터 형식에 대해 정의되지 않습니다.<br /><br /> 이 정보는 IRD의 SCALE 레코드 필드에서 반환됩니다.|  
|SQL_DESC_SCHEMA_NAME (ODBC 2.0)|*CharacterAttributePtr*|열을 포함하는 테이블의 스키마입니다. 반환된 값은 열이 식이거나 열이 뷰의 일부인 경우 구현 정의됩니다. 데이터 원본이 스키마를 지원하지 않거나 스키마 이름을 확인할 수 없는 경우 빈 문자열이 반환됩니다. 이 VARCHAR 레코드 필드는 128자로 제한되지 않습니다.|  
|SQL_DESC_SEARCHABLE (ODBC 1.0)|*숫자 속성 Ptr*|WHERE 절에서 열을 사용할 수 없는 경우 SQL_PRED_NONE. ODBC 2의 SQL_UNSEARCHABLE 값과 동일합니다. *x*.)<br /><br /> SQL_PRED_CHAR WHERE 절에서 만 LIKE 조건자에서 열에 사용할 수 있습니다. ODBC 2의 SQL_LIKE_ONLY 값과 동일합니다. *x*.)<br /><br /> SQL_PRED_BASIC 열을 LIKE를 제외한 모든 비교 연산자가 있는 WHERE 절에서 사용할 수 있는지 를 포함합니다. ODBC 2의 SQL_EXCEPT_LIKE 값과 동일합니다. *x*.)<br /><br /> SQL_PRED_SEARCHABLE 비교 연산자가 있는 WHERE 절에서 열을 사용할 수 있는지 를 지정합니다.<br /><br /> 형식 SQL_LONGVARCHAR 및 SQL_LONGVARBINARY 열은 일반적으로 SQL_PRED_CHAR 반환합니다.|  
|SQL_DESC_TABLE_NAME (ODBC 2.0)|*CharacterAttributePtr*|열을 포함하는 테이블의 이름입니다. 반환된 값은 열이 식이거나 열이 뷰의 일부인 경우 구현 정의됩니다.<br /><br /> 테이블 이름을 확인할 수 없는 경우 빈 문자열이 반환됩니다.|  
|SQL_DESC_TYPE (ODBC 3.0)|*숫자 속성 Ptr*|SQL 데이터 형식을 지정하는 숫자 값입니다.<br /><br /> *ColumnNumber가* 0이면 SQL_BINARY 길이가 가변 책갈피에 반환되고 SQL_INTEGER 길이의 책갈피의 경우 반환됩니다.<br /><br /> datetime 및 간격 데이터 형식의 경우 이 필드는 SQL_DATETIME 또는 SQL_INTERVAL 자세한 데이터 형식을 반환합니다. 자세한 내용은 부록 D: 데이터 형식의 [데이터 유형 식별자 및 설명자를](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) 참조하십시오.<br /><br /> 이 정보는 IRD의 SQL_DESC_TYPE 레코드 필드에서 반환됩니다. **참고:**  ODBC 2에 대해 작업합니다. *x* 드라이버, 대신 SQL_DESC_CONCISE_TYPE 사용합니다.|  
|SQL_DESC_TYPE_NAME (ODBC 1.0)|*CharacterAttributePtr*|데이터 원본 종속 데이터 형식 이름; 예를 들어 "CHAR", "VARCHAR", "MONEY", "LONG VARBINARY" 또는 "CHAR ()에 대한 비트 데이터"를 예로 들 수 있습니다.<br /><br /> 형식을 알 수 없는 경우 빈 문자열이 반환됩니다.|  
|SQL_DESC_UNNAMED (ODBC 3.0)|*숫자 속성 Ptr*|SQL_NAMED 또는 SQL_UNNAMED. IRD의 SQL_DESC_NAME 필드에 열 별칭 또는 열 이름이 포함되어 있으면 SQL_NAMED 반환됩니다. 열 이름 또는 열 별칭이 없는 경우 SQL_UNNAMED 반환됩니다.<br /><br /> 이 정보는 IRD의 SQL_DESC_UNNAMED 레코드 필드에서 반환됩니다.|  
|SQL_DESC_UNSIGNED (ODBC 1.0)|*숫자 속성 Ptr*|열이 서명되지 않은 경우(또는 숫자 아님)SQL_TRUE.<br /><br /> 열이 서명된 경우 SQL_FALSE.|  
|SQL_DESC_UPDATABLE (ODBC 1.0)|*숫자 속성 Ptr*|열은 정의된 상수에 대한 값으로 설명됩니다.<br /><br /> SQL_ATTR_READONLY SQL_ATTR_WRITE SQL_ATTR_READWRITE_UNKNOWN<br /><br /> SQL_DESC_UPDATABLE 기준 테이블의 열이 아니라 결과 집합에서 열의 업데이터성을 설명합니다. 결과 집합 열의 기반이 되는 기본 열의 업데이터성은 이 필드의 값과 다를 수 있습니다. 열이 업데이터인지 여부는 데이터 형식, 사용자 권한 및 결과 집합 자체의 정의를 기반으로 할 수 있습니다. 열이 업데이터 인지 여부가 명확하지 않은 경우 SQL_ATTR_READWRITE_UNKNOWN 반환해야 합니다.|  
  
 **SQLColAttribute는** **SQLDescribeCol에**대한 확장 가능한 대안입니다. **SQLDescribeCol** ANSI-89 SQL을 기반으로 설명자 정보의 고정 된 집합을 반환 합니다. **SQLColAttribute는** ANSI SQL-92 및 DBMS 공급업체 확장에서 사용할 수 있는 보다 광범위한 설명자 정보 집합에 액세스할 수 있도록 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|명령문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|결과 집합의 열에 대한 정보 반환|[SQLDescribeCol 함수](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|데이터 블록 가져오기 또는 결과 집합 스크롤|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|여러 데이터 행 가져오기|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
  
## <a name="example"></a>예제  
 다음 샘플 코드에서는 핸들과 연결을 해제하지 않습니다. 코드 샘플에서 무료 핸들 및 문을 사용할 수 있는 [SQLFreeHandle 함수,](../../../odbc/reference/syntax/sqlfreehandle-function.md) [샘플 ODBC 프로그램](../../../odbc/reference/sample-odbc-program.md)및 [SQLFreeStmt 함수를](../../../odbc/reference/syntax/sqlfreestmt-function.md) 참조하십시오.  
  
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
