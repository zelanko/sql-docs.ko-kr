---
title: SQLSetDescField 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetDescField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetDescField
helpviewer_keywords:
- SQLSetDescField function [ODBC]
ms.assetid: 8c544388-fe9d-4f94-a0ac-fa0b9c9c88a5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fb6061adf707a58737fd34d7cb7bbe33b2e9579a
ms.sourcegitcommit: 480961f14405dc0b096aa8009855dc5a2964f177
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/22/2019
ms.locfileid: "54420238"
---
# <a name="sqlsetdescfield-function"></a>SQLSetDescField 함수

**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수 합니다. ISO 92  
  
 **요약**  
 **SQLSetDescField** 설명자 레코드의 단일 필드의 값을 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
SQLRETURN SQLSetDescField(  
     SQLHDESC      DescriptorHandle,  
     SQLSMALLINT   RecNumber,  
     SQLSMALLINT   FieldIdentifier,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    BufferLength);  
```  
  
## <a name="arguments"></a>인수  
 *DescriptorHandle*  
 [입력] 설명자 핸들입니다.  
  
 *RecNumber*  
 [입력] 응용 프로그램 검색을 설정 하는 필드를 포함 하는 설명자 레코드를 나타냅니다. 0 책갈피 레코드 중 레코드 번호를 사용 하 여 0, 설명자 레코드 번호가 매겨집니다. 합니다 *RecNumber* 헤더 필드에 대 한 인수는 무시 됩니다.  
  
 *FieldIdentifier*  
 [입력] 설정할 값이 설명자의 필드를 나타냅니다. 자세한 내용은 참조 하세요. "*FieldIdentifier* 인수" "설명" 섹션에 있습니다.  
  
 *ValuePtr*  
 [입력] 설명자 정보 또는 정수 값을 포함 하는 버퍼에 대 한 포인터입니다. 데이터 형식 값에 따라 달라 집니다 *FieldIdentifier*합니다. 하는 경우 *ValuePtr* 는 정수 값을 8 바이트 (SQLLEN), 4 바이트 (SQLINTEGER) 또는 값에 따라 2 바이트 (SQLSMALLINT)로 간주 될 수 있습니다 합니다 *FieldIdentifier* 인수입니다.  
  
 *BufferLength*  
 [입력] 하는 경우 *FieldIdentifier* 은 ODBC 정의 된 필드와 *ValuePtr* 문자열 또는 이진 버퍼를 가리키는,이 인수 길이 여야 합니다 **ValuePtr*합니다. 문자 문자열 데이터의 경우이 인수는 문자열의 바이트 수를 포함 해야 합니다.  
  
 경우 *FieldIdentifier* 은 ODBC 정의 된 필드와 *ValuePtr* 정수 이면 *BufferLength* 무시 됩니다.  
  
 하는 경우 *FieldIdentifier* 드라이버에서 정의 된 필드는 응용 프로그램을 설정 하 여 드라이버 관리자에 필드의 특성을 나타내는 합니다 *BufferLength* 인수. *BufferLength* 다음 값을 가질 수 있습니다.  
  
-   하는 경우 *ValuePtr* 문자열에 대 한 포인터 이면 *BufferLength* SQL_NTS 또는 문자열의 길이입니다.  
  
-   하는 경우 *ValuePtr* 이진 버퍼에 대 한 포인터 이면 응용 프로그램을 SQL_LEN_BINARY_ATTR의 결과 배치 (*길이*)에서 매크로 *BufferLength*합니다. 에 음수 값이 배치 *BufferLength*합니다.  
  
-   하는 경우 *ValuePtr* 이 아닌 문자열 또는 이진 문자열 값에 대 한 포인터 이면 *BufferLength* SQL_IS_POINTER 값이 있어야 합니다.  
  
-   하는 경우 *ValuePtr* 다음을 고정 길이 값이 포함 되어 *BufferLength* 되었거나 SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT, SQL_IS_USMALLINT를 적절 하 게 합니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLSetDescField** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* 의 SQL_HANDLE_DESC와 *처리할* 의 *DescriptorHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLSetDescField** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01S02|옵션 값이 변경 됨|드라이버에서 지정 된 값을 지원 하지 않았습니다  *\*ValuePtr* (경우 *ValuePtr* 가 포인터) 값과 *ValuePtr* (경우 *ValuePtr*  는 정수 값), 또는  *\*ValuePtr* 드라이버 유사한 값을 대체 하도록 구현 작업 조건으로 인해 잘못 되었습니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|07009|잘못 된 설명자 인덱스입니다.|합니다 *FieldIdentifier* 인수가 레코드 필드를 *RecNumber* 인수가 0, 및 *DescriptorHandle* 인수 IPD 핸들을 참조 합니다.<br /><br /> 합니다 *RecNumber* 인수가 0 보다 작거나, 및 *DescriptorHandle* 인수는 카드가 또는 APD 참조 합니다.<br /><br /> *RecNumber* 인수 열 또는 매개 변수 데이터 원본을 지원할 수 있는 최대 수보다 큽니다. 하며 *DescriptorHandle* APD 또는 카드가 인수 참조 합니다.<br /><br /> (DM)는 *FieldIdentifier* 인수가 SQL_DESC_COUNT, 및  *\*ValuePtr* 인수가 0 보다 작습니다.<br /><br /> *RecNumber* 인수가 0 인 하며 *DescriptorHandle* 인수를 암시적으로 할당 된 APD 참조 합니다. (명시적으로 할당 된 응용 프로그램 설명자를 사용 하 여이 오류가 발생 하지 않습니다 APD 또는까지 카드가 명시적으로 할당 된 응용 프로그램 설명자를 인지 여부를 알 수 없습니다 때문에 실행 시간입니다.)|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버는 연결 된 데이터 원본 간의 통신 링크 하지 못했습니다.|  
|22001|문자열 데이터 오른쪽 잘림|합니다 *FieldIdentifier* 인수가 SQL_DESC_NAME, 및 *BufferLength* 인수가 SQL_MAX_IDENTIFIER_LEN 보다 큰 값입니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)는 *DescriptorHandle* 연관 된를 *StatementHandle* 는 비동기적으로 실행 중인 (이 없는 항목)를 호출한 함수와이 함수가 호출 되었을 때 계속 실행에 대 한 합니다.<br /><br /> (DM) **SQLExecute**를 **SQLExecDirect**를 **SQLBulkOperations**, 또는 **SQLSetPos** 에 대해 호출 된는  *StatementHandle* 있는 합니다 *DescriptorHandle* 연결 되었으며 SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한 합니다 *DescriptorHandle*합니다. 이 비동기 함수가 여전히 실행 시기를 **SQLSetDescField** 함수를 호출 했습니다.<br /><br /> (DM) **SQLExecute**를 **SQLExecDirect**, 또는 **SQLMoreResults** 관련 된 문 핸들 중 하나에 대해 호출한는 *DescriptorHandle* SQL_PARAM_DATA_AVAILABLE를 반환 합니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY016|구현 행 설명자를 수정할 수 없습니다.|*DescriptorHandle* 인수가 IRD, 연결 및 *FieldIdentifier* 인수 SQL_DESC_ARRAY_STATUS_PTR 또는 SQL_DESC_ROWS_PROCESSED_PTR 없습니다.|  
|HY021|일관성이 없는 설명자 정보|SQL_DESC_TYPE 및 값을 SQL_DESC_DATETIME_INTERVAL_CODE 필드 (Apd 또는 ARDs)에 유효한 ODBC SQL 형식 또는 올바른 드라이버별 SQL 형식 (IPDs)에 대 한 유효한 ODBC C 형식을 형성 하지 않습니다.<br /><br /> 설명자 정보 일관성 검사를 사용 하는 동안 체크 일관 되지 않았습니다. (의 "일관성 확인"을 참조 하세요 **SQLSetDescRec**.)|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|(DM)  *\*ValuePtr* 문자열, 및 *BufferLength* 0 보다 작거나 같으면 SQL_NTS 없었습니다. 합니다.<br /><br /> (DM) 드라이버는 ODBC 2 되었습니다 *.x* 드라이버 설명자가는 카드가 합니다 *ColumnNumber* 인수는 0이 고, 인수에 지정 된 값으로 설정 된 *BufferLength* 되었습니다 4 같지 않음.|  
|HY091|잘못 된 설명자 필드 식별자입니다.|지정 된 값을 *FieldIdentifier* 인수 ODBC 정의 필드를 없었으며 구현 시 정의 된 값이 없습니다.<br /><br /> 합니다 *FieldIdentifier* 에 대 한 잘못 된 인수를 *DescriptorHandle* 인수입니다.<br /><br /> 합니다 *FieldIdentifier* 인수가 ODBC 정의 읽기 전용 필드입니다.|  
|HY092|잘못 된 특성/옵션 식별자입니다.|값  *\*ValuePtr* 없습니다 합니다 *FieldIdentifier* 인수입니다.<br /><br /> 합니다 *FieldIdentifier* 인수가 SQL_DESC_UNNAMED, 및 *ValuePtr* SQL_NAMED 되었습니다.|  
|HY105|잘못 된 매개 변수 형식|(DM)으로 필드에 대해 지정 된 값을 잘못 되었습니다. (자세한 내용은 참조는 "*InputOutputType* 인수" 섹션 **SQLBindParameter**.)|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [What's New in ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)합니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 드라이버를 사용 하 여 연결 합니다 *DescriptorHandle* 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 응용 프로그램에서 호출할 수 있습니다 **SQLSetDescField** 한 번에 하나의 모든 설명자 필드를 설정할 수 있습니다. 한 번 호출 **SQLSetDescField** 단일 설명자에서 단일 필드를 설정 합니다. 이 함수 설명자 형식에서 모든 필드를 설정 하기 위해 호출 됩니다, 그리고 필드를 설정할 수 있습니다 제공 될 수 있습니다. (이 섹션의 뒷부분에 나오는 표를 참조 하세요.)  
  
> [!NOTE]  
>  호출 하는 경우 **SQLSetDescField** 실패 하 여 식별 되는 설명자 레코드의 콘텐츠를 *RecNumber* 인수가 정의 되지 않습니다.  
  
 함수의 단일 호출으로 여러 설명자 필드를 설정 하려면 다른 함수를 호출할 수 있습니다. 합니다 **SQLSetDescRec** 함수는 열 또는 매개 변수 (SQL_DESC_TYPE, 값을 SQL_DESC_DATETIME_INTERVAL_CODE, SQL_DESC_OCTET_LENGTH, 자릿수가 SQL_DESC_PRECISION, SQL_에 바인딩된 데이터 형식 및 버퍼에 영향을 주는 다양 한 필드 설정 DESC_SCALE SQL_DESC_DATA_PTR, SQL_DESC_OCTET_LENGTH_PTR을, SQL_DESC_INDICATOR_PTR 필드)입니다. **SQLBindCol** 나 **SQLBindParameter** 의 열 또는 매개 변수 바인딩에 대 한 완전 한 사양을 만드는 데 사용할 수 있습니다. 이러한 함수는 함수 호출이 하나를 사용 하 여 설명자 필드의 특정 그룹을 설정합니다.  
  
 **SQLSetDescField** 호출 (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, 또는 SQL_DESC_OCTET_LENGTH_PTR)에 대 한 바인딩 포인터에 오프셋을 추가 하 여 바인딩 버퍼를 변경할 수 있습니다. 호출 하지 않고 바인딩 버퍼 변경 **SQLBindCol** 하거나 **SQLBindParameter**, SQL_DESC_DATA_ 같은 기타 필드를 변경 하지 않고 SQL_DESC_DATA_PTR을 변경 하려면 응용 프로그램을 허용 하는 형식입니다.  
  
 응용 프로그램을 호출 하는 경우 **SQLSetDescField** 레코드 SQL_DESC_COUNT 이외의 모든 필드 또는 SQL_DESC_OCTET_LENGTH_PTR을, SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR 지연 된 필드를 설정 하려면 바인딩 해제 됩니다.  
  
 설명자 헤더 필드를 호출 하 여 설정 됩니다 **SQLSetDescField** 적절 한 *FieldIdentifier*합니다. 여러 헤더 필드 되므로 문 특성, 호출 하 여 설정할 수도 있습니다 **SQLSetStmtAttr**합니다. 이렇게 하면 응용 프로그램 첫 번째 설명자 핸들을 가져오지 않고도 설명자 필드를 설정할 수 있습니다. 때 **SQLSetDescField** 헤더 필드를 설정 하기 위해 호출 합니다 *RecNumber* 인수는 무시 됩니다.  
  
 A *RecNumber* 0 책갈피 필드 설정에 사용 됩니다.  
  
> [!NOTE]  
>  문 특성 SQL_ATTR_USE_BOOKMARKS 항상 설정할 호출 하기 전에 **SQLSetDescField** 책갈피 필드를 설정 합니다. 이것이 필수 것이 좋습니다.  
  
## <a name="sequence-of-setting-descriptor-fields"></a>설명자 필드를 설정 하는 시퀀스  
 호출 하 여 설명자 필드를 설정 하는 경우 **SQLSetDescField**, 응용 프로그램에는 특정 순서를 따라야 합니다.  
  
1.  응용 프로그램의 SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE, 또는 값을 SQL_DESC_DATETIME_INTERVAL_CODE 필드를 먼저 설정 해야 합니다.  
  
2.  이러한 필드 중 하나를 설정한 후 응용 프로그램의 데이터 형식 특성을 설정할 수 있습니다 및 드라이버 데이터 형식 특성 필드를 설정 하는 데이터 형식에 대 한 적절 한 기본값입니다. 형식 특성 필드를 자동으로 기본값 설명자는 항상 응용 프로그램에는 데이터 형식 지정에 사용할 준비가 되도록 합니다. 응용 프로그램이 데이터 형식 특성에 명시적으로 설정 하는 경우 기본 특성을 재정의 해당 합니다.  
  
3.  1 단계에서 나열 된 필드 중 하나를 설정한 후 데이터 형식 특성을 설정한 응용 프로그램 SQL_DESC_DATA_PTR을 설정할 수 있습니다. 이 메시지 설명자 필드의 일관성 확인을 표시합니다. 응용 프로그램 데이터 형식 또는 특성에 SQL_DESC_DATA_PTR 필드가 설정 후 변경 되 면 드라이버는 레코드를 바인딩 해제, null 포인터로 SQL_DESC_DATA_PTR을 설정 합니다. 이렇게 하면 응용 프로그램 설명자 레코드를 사용할 수 전에 순서 대로 적절 한 단계를 완료 합니다.  
  
## <a name="initialization-of-descriptor-fields"></a>설명자 필드 초기화  
 설명자가 할당 된 경우 설명자 필드는 기본값으로 초기화할 수 있습니다 하, 기본값이 없는 초기화 하거나 형식 설명자에 대해 정의 되지 않은. 다음 표에서 각 유형의와 "D" 필드는 기본적으로 초기화 되었음을 나타내는 "ND" 필드 기본값 없이 초기화 되었음을 나타내는 설명자에 대 한 각 필드의 초기화를 나타냅니다. 숫자로 표시 되는 경우 필드의 기본값은 숫자입니다. 테이블 (R/W)에 대 한 읽기/쓰기 또는 읽기 전용 (R) 인지를 나타낼 수도 있습니다.  
  
 IRD 필드에 기본값이 및 IRD 채워지면 설명자를 문 핸들 할당 된 때가 아니라 문이 준비 되거나 실행 된 후에 합니다. IRD 채워지면 될 때까지 IRD 필드에 액세스 하려는 모든 시도 오류가 반환 됩니다.  
  
 일부 설명자 필드 (ARDs IRDs, 및 Apd 및 IPDs) 설명자 형식 중 전부는 아님 하나 이상에 대해 정의 됩니다. 필드 형식 설명자에 대해 정의 되지 않으면, 해당 설명자를 사용 하는 함수 중 하나에서 필요 하지 않습니다.  
  
 액세스할 수 있는 필드 **SQLGetDescField** 가 반드시 설정할 수 없습니다 **SQLSetDescField**합니다. 설정할 수 있는 필드 **SQLSetDescField** 다음 표에 나열 됩니다.  
  
 헤더 필드의 초기화를 뒤에 오는 테이블에 설명 된 합니다.  
  
|헤더 필드 이름|형식|R/W|Default|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_ALLOC_TYPE|SQLSMALLINT|카드가: R APD: R IRD: R IPD: R|카드가: 에 대 한 SQL_DESC_ALLOC_AUTO 암시적 또는 SQL_DESC_ALLOC_USER에 대 한 명시적<br /><br /> APD: 에 대 한 SQL_DESC_ALLOC_AUTO 암시적 또는 SQL_DESC_ALLOC_USER에 대 한 명시적<br /><br /> IRD: SQL_DESC_ALLOC_AUTO<br /><br /> IPD: SQL_DESC_ALLOC_AUTO|  
|SQL_DESC_ARRAY_SIZE|SQLULEN|카드가: R/W APD: R/W IRD: 사용 되지 않는 IPD: 사용 되지 않는|ARD:[1] APD:[1] IRD: 사용 되지 않는 IPD: 사용 되지 않는|  
|SQL_DESC_ARRAY_STATUS_PTR|SQLUSMALLINT*|카드가: R/W APD: R/W IRD: R/W IPD: R/W|카드가: Ptr APD null. Null ptr IRD: Null ptr IPD: Null ptr|  
|SQL_DESC_BIND_OFFSET_PTR|SQLLEN*|카드가: R/W APD: R/W IRD: 사용 되지 않는 IPD: 사용 되지 않는|카드가: Ptr APD null. Null ptr IRD: 사용 되지 않는 IPD: 사용 되지 않는|  
|SQL_DESC_BIND_TYPE|SQLINTEGER|카드가: R/W APD: R/W IRD: 사용 되지 않는 IPD: 사용 되지 않는|카드가: SQL_BIND_BY_COLUMN<br /><br /> APD: SQL_BIND_BY_COLUMN<br /><br /> IRD: 사용 되지 않는<br /><br /> IPD: 사용 되지 않는|  
SQL_DESC_COUNT|SQLSMALLINT|카드가: R/W APD: R/W IRD: R IPD: R/W|카드가: 0 APD: 0 IRD: D IPD: 0|  
|SQL_DESC_ROWS_PROCESSED_PTR|SQLULEN*|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: R/W IPD: R/W|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: Null ptr IPD: Null ptr|  
  
 [1]이이 필드는 IPD 드라이버에 의해 자동으로 채워지는 경우에 정의 됩니다. 그렇지 않은 경우 정의 되지 않습니다. 응용 프로그램에서 SQLSTATE HY091 이러한 필드를 설정 하려고 하는 경우 (잘못 된 설명자 필드 식별자)가 반환 됩니다.  
  
 레코드 필드를 초기화 하는 다음 표에 나와 있는 것 처럼 됩니다.  
  
|레코드 필드 이름|형식|R/W|Default|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: 사용 되지 않는|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: 사용 되지 않는|  
|SQL_DESC_BASE_COLUMN_NAME|SQLCHAR *|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: 사용 되지 않는|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: 사용 되지 않는|  
|SQL_DESC_BASE_TABLE_NAME|SQLCHAR *|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: 사용 되지 않는|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: 사용 되지 않는|  
|SQL_DESC_CASE_SENSITIVE|SQLINTEGER|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: R|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: D[1]|  
|SQL_DESC_CATALOG_NAME|SQLCHAR *|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: 사용 되지 않는|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: 사용 되지 않는|  
|SQL_DESC_CONCISE_TYPE|SQLSMALLINT|카드가: R/W APD: R/W IRD: R IPD: R/W|카드가: SQL_C_ DEFAULT APD: SQL_C_ DEFAULT IRD: D IPD: ND|  
|SQL_DESC_DATA_PTR|대 SQLPOINTER|카드가: R/W APD: R/W IRD: 사용 되지 않는 IPD: 사용 되지 않는|카드가: Ptr APD null. Null ptr IRD: 사용 되지 않는 IPD: [2] 사용 안 함|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQLSMALLINT|카드가: R/W APD: R/W IRD: R IPD: R/W|카드가: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|SQLINTEGER|카드가: R/W APD: R/W IRD: R IPD: R/W|카드가: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_DISPLAY_SIZE|SQLLEN|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: 사용 되지 않는|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: 사용 되지 않는|  
|SQL_DESC_FIXED_PREC_SCALE|SQLSMALLINT|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: R|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: D[1]|  
|SQL_DESC_INDICATOR_PTR|SQLLEN *|카드가: R/W APD: R/W IRD: 사용 되지 않는 IPD: 사용 되지 않는|카드가: Ptr APD null. Null ptr IRD: 사용 되지 않는 IPD: 사용 되지 않는|  
|SQL_DESC_LABEL|SQLCHAR *|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: 사용 되지 않는|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: 사용 되지 않는|  
|SQL_DESC_LENGTH|SQLULEN|카드가: R/W APD: R/W IRD: R IPD: R/W|카드가: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_LITERAL_PREFIX|SQLCHAR *|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: 사용 되지 않는|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: 사용 되지 않는|  
|SQL_DESC_LITERAL_SUFFIX|SQLCHAR *|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: 사용 되지 않는|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: 사용 되지 않는|  
|SQL_DESC_LOCAL_TYPE_NAME|SQLCHAR *|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: R|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: D[1]|  
|SQL_DESC_NAME|SQLCHAR *|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: R/W|카드가: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_NULLABLE|SQLSMALLINT|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: R|카드가: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_NUM_PREC_RADIX|SQLINTEGER|카드가: R/W APD: R/W IRD: R IPD: R/W|카드가: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_OCTET_LENGTH|SQLLEN|카드가: R/W APD: R/W IRD: R IPD: R/W|카드가: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_OCTET_LENGTH_PTR|SQLLEN *|카드가: R/W APD: R/W IRD: 사용 되지 않는 IPD: 사용 되지 않는|카드가: Ptr APD null. Null ptr IRD: 사용 되지 않는 IPD: 사용 되지 않는|  
|SQL_DESC_PARAMETER_TYPE|SQLSMALLINT|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: 사용 되지 않는 IPD: R/W|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: 사용 되지 않는 IPD: D=SQL_PARAM_INPUT|  
|SQL_DESC_PRECISION|SQLSMALLINT|카드가: R/W APD: R/W IRD: R IPD: R/W|카드가: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_ROWVER|SQLSMALLINT|카드가: 사용 되지 않는<br /><br /> APD: 사용 되지 않는<br /><br /> IRD: R<br /><br /> IPD: R|카드가: 사용 되지 않는<br /><br /> APD: 사용 되지 않는<br /><br /> IRD: ND<br /><br /> IPD: ND|  
|SQL_DESC_SCALE|SQLSMALLINT|카드가: R/W APD: R/W IRD: R IPD: R/W|카드가: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_SCHEMA_NAME|SQLCHAR *|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: 사용 되지 않는|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: 사용 되지 않는|  
|SQL_DESC_SEARCHABLE|SQLSMALLINT|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: 사용 되지 않는|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: 사용 되지 않는|  
|SQL_DESC_TABLE_NAME|SQLCHAR *|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: 사용 되지 않는|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: 사용 되지 않는|  
|SQL_DESC_TYPE|SQLSMALLINT|카드가: R/W APD: R/W IRD: R IPD: R/W|카드가: SQL_C_DEFAULT APD: SQL_C_DEFAULT IRD: D IPD: ND|  
|SQL_DESC_TYPE_NAME|SQLCHAR *|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: R|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: D[1]|  
|SQL_DESC_UNNAMED|SQLSMALLINT|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: R/W|카드가: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_UNSIGNED|SQLSMALLINT|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: R|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: D[1]|  
|SQL_DESC_UPDATABLE|SQLSMALLINT|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: 사용 되지 않는|카드가: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: 사용 되지 않는|  
  
 [1]이이 필드는 IPD 드라이버에 의해 자동으로 채워지는 경우에 정의 됩니다. 그렇지 않은 경우 정의 되지 않습니다. 응용 프로그램에서 SQLSTATE HY091 이러한 필드를 설정 하려고 하는 경우 (잘못 된 설명자 필드 식별자)가 반환 됩니다.  
  
 [2]에서 SQL_DESC_DATA_PTR 필드는 IPD의 일관성 확인을 강제로 설정할 수 있습니다. 에 대 한 후속 호출에서 **SQLGetDescField** 하거나 **SQLGetDescRec**, 드라이버 SQL_DESC_DATA_PTR 되도록 설정 된 값을 반환 하지 않아도 됩니다.  
  
## <a name="fieldidentifier-argument"></a>FieldIdentifier 인수  
 합니다 *FieldIdentifier* 인수 설정할 설명자 필드를 나타냅니다. 설명자를 포함 합니다 *설명자 헤더* 다음 섹션, "헤더 필드를"와 0 개 이상의에서 설명 하는 헤더 필드 이루어진 *설명자 레코드* 레코드 필드로 구성 된 "헤더 필드" 섹션을 다음 섹션에서 설명 합니다.  
  
## <a name="header-fields"></a>헤더 필드  
 각 설명자에는 다음 필드로 구성 된 헤더에 있습니다.  
  
 **SQL_DESC_ALLOC_TYPE [All]**  
 이 읽기 전용 SQLSMALLINT 헤더 필드 드라이버 또는 응용 프로그램에서 명시적으로 설명자를 자동으로 할당 된 여부를 지정 합니다. 응용 프로그램을 수 있지만 수정할 수 없으며이 필드. 필드는 설명자를 드라이버에 의해 자동으로 할당 된 경우 드라이버에서 SQL_DESC_ALLOC_AUTO에 설정 됩니다. 설정은 SQL_DESC_ALLOC_USER 드라이버에서 설명자 응용 프로그램에서 명시적으로 할당 된 경우.  
  
 **SQL_DESC_ARRAY_SIZE [Application descriptors]**  
 ARDs,이 SQLULEN 헤더 필드를 행 집합의 행 수를 지정합니다. 호출 하 여 반환할 행의 수입니다 **SQLFetch** 하거나 **SQLFetchScroll** 를 호출 하 여 작업할 수 나 **SQLBulkOperations** 또는 **SQLSetPos** .  
  
 Apd,이 SQLULEN 헤더 필드는 각 매개 변수에 대해 값의 개수를 지정합니다.  
  
 이 필드의 기본값은 1입니다. SQL_DESC_ARRAY_SIZE 1 보다 큰 경우 SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, 및 카드가 APD의 SQL_DESC_OCTET_LENGTH_PTR 배열을 가리킵니다. 각 배열의 카디널리티가이 필드의 값과 동일합니다.  
  
 이 필드는 카드가에서 호출 하 여 설정할 수도 있습니다 **SQLSetStmtAttr** SQL_ATTR_ROW_ARRAY_SIZE 특성을 사용 합니다. APD의이 필드를 호출 하 여 설정할 수도 있습니다 **SQLSetStmtAttr** SQL_ATTR_PARAMSET_SIZE 특성을 사용 합니다.  
  
 **SQL_DESC_ARRAY_STATUS_PTR [All]**  
 이 SQLUSMALLINT 각 설명자 형식에 대해 * SQLUSMALLINT 값의 배열에 헤더 필드 지점입니다. 이러한 배열은 다음과 같은 이름이 지정 됩니다: 행 상태 배열 (IRD), 매개 변수 상태 배열을 (IPD), 행 작업 배열을 () 매개 변수 작업 배열 (APD).  
  
 IRD이 헤더 필드를 호출한 후 상태 값을 포함 하는 행 상태 배열 가리킵니다 **SQLBulkOperations**, **SQLFetch**합니다 **SQLFetchScroll**, 또는 **SQLSetPos**합니다. 배열에 행 집합의 행이 있는 만큼의 요소가 있습니다. 응용 프로그램 SQLUSMALLINTs 배열을 할당 하 고이 필드는 배열을 가리키도록 설정 해야 합니다. 필드는 기본적으로 null 포인터로 설정 됩니다. 드라이버는 SQL_DESC_ARRAY_STATUS_PTR 필드 없음 상태 값이 생성 되는 경우에 null 포인터로 설정 되 고 배열 채워지지 않는 경우가 아니면 배열을-채워집니다.  
  
> [!CAUTION]  
>  응용 프로그램 SQL_DESC_ARRAY_STATUS_PTR IRD 필드에서 가리키는 행 상태 배열 요소를 설정 하는 경우에 드라이버 동작이 정의 되지 않습니다.  
  
 호출 하 여 배열의 처음 채워집니다 **SQLBulkOperations**, **SQLFetch**를 **SQLFetchScroll**, 또는 **SQLSetPos**합니다. 호출 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO 반환 하지 않은 경우이 필드에서 가리키는 배열 콘텐츠가 정의 되지 않습니다. 배열의 요소에는 다음 값을 포함할 수 있습니다.  
  
-   SQL_ROW_SUCCESS: 행을 성공적으로 가져온 및 마지막 페치된 후 변경 되지 않은 합니다.  
  
-   SQL_ROW_SUCCESS_WITH_INFO: 행을 성공적으로 가져온 및 마지막 페치된 후 변경 되지 않은 합니다. 그러나 행에 대 한 경고가 반환 되었습니다.  
  
-   SQL_ROW_ERROR: 행을 인출 하는 동안 오류가 발생 했습니다.  
  
-   SQL_ROW_UPDATED: 행을 성공적으로 가져온 및 마지막으로 가져온 후에 업데이트 되었습니다. 행이 다시 인출 됩니다을 하는 경우 해당 상태가 SQL_ROW_SUCCESS입니다.  
  
-   SQL_ROW_DELETED: 마지막으로 페치된 이후로 행 삭제 되었습니다.  
  
-   SQL_ROW_ADDED: 행으로 삽입 된 **SQLBulkOperations**합니다. 행이 다시 인출 됩니다을 하는 경우 해당 상태가 SQL_ROW_SUCCESS입니다.  
  
-   SQL_ROW_NOROW: 행 집합 결과 집합의 끝을 중첩 하 고 행이 행 상태 배열이 요소에 해당 하는 반환 된 키를 누릅니다.  
  
 IRD에서이 필드를 호출 하 여 설정할 수도 있습니다 **SQLSetStmtAttr** SQL_ATTR_ROW_STATUS_PTR 특성을 사용 합니다.  
  
 IRD의 SQL_DESC_ARRAY_STATUS_PTR 필드 SQL_SUCCESS 또는 sql_success_with_info가 반환 된 후에 유효 합니다. 반환 코드는 다음 중 하나를 SQL_DESC_ROWS_PROCESSED_PTR 가리키는 위치 정의 되지 않습니다.  
  
 IPD,이 헤더 필드를 호출한 후 각 매개 변수 값 집합에 대 한 상태 정보를 포함 하는 매개 변수 상태 배열을 가리킵니다 **SQLExecute** 하거나 **SQLExecDirect**합니다. 경우에 대 한 호출 **SQLExecute** 하거나 **SQLExecDirect** SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를이 필드에서 가리키는 배열 콘텐츠가 정의 되지 않습니다. 반환 하지 않았습니다. 응용 프로그램 SQLUSMALLINTs 배열을 할당 하 고이 필드는 배열을 가리키도록 설정 해야 합니다. 드라이버는 SQL_DESC_ARRAY_STATUS_PTR 필드 없음 상태 값이 생성 되는 경우에 null 포인터로 설정 되 고 배열 채워지지 않는 경우가 아니면 배열을-채워집니다. 배열의 요소에는 다음 값을 포함할 수 있습니다.  
  
-   SQL_PARAM_SUCCESS: 이 매개 변수이 집합에 대 한 SQL 문이 성공적으로 실행 합니다.  
  
-   SQL_PARAM_SUCCESS_WITH_INFO: 이 매개 변수이 집합에 대 한 SQL 문이 성공적으로 실행 그러나 경고 정보는 진단 데이터 구조에서 사용할 수 있습니다.  
  
-   SQL_PARAM_ERROR: 이 매개 변수이 집합을 처리에서 오류가 발생 했습니다. 추가 오류 정보를 진단 데이터 구조에서 사용할 수 있습니다.  
  
-   SQL_PARAM_UNUSED: 이 매개 변수 집합 되지 않았거나 사용할 수 있는 때문에 일부 이전 매개 변수 집합 추가 처리를 중단 하는 오류가 발생 한 SQL_PARAM_IGNORE의 SQL_DESC_ARRAY_STATUS_PTR 필드에 의해 지정 된 배열에 매개 변수 집합에 대 한 설정 되었기 때문에 APD 합니다.  
  
-   SQL_PARAM_DIAG_UNAVAILABLE: 진단 정보를 사용할 수 없는 경우 이 예가 드라이버 모놀리식 단위로 매개 변수 배열을 처리 하는 경우 및이 수준의 오류 정보를 생성 하지 않도록 합니다.  
  
 이 필드는 IPD의 호출 하 여 설정할 수도 있습니다 **SQLSetStmtAttr** SQL_ATTR_PARAM_STATUS_PTR 특성을 사용 합니다.  
  
 카드가,이 헤더 필드를이 행에 대해 무시 되도록 인지 여부를 나타내는 응용 프로그램에서 설정할 수 있는 값의 행 작업 배열을 가리킵니다 **SQLSetPos** 작업 합니다. 배열의 요소에는 다음 값을 포함할 수 있습니다.  
  
-   SQL_ROW_PROCEED: 사용 하 여 대량 작업에는 행이 포함 **SQLSetPos**합니다. (이 설정은 보장 하지 않습니다 하 고 작업 행에서 수행 됩니다. 행 IRD 행 상태 배열에서 SQL_ROW_ERROR 상태에 있는 경우 드라이버 못할 행의 작업을 수행할 수 있습니다.)  
  
-   SQL_ROW_IGNORE: 행을 사용 하 여 대량 작업에서 제외 됩니다 **SQLSetPos**합니다.  
  
 배열의 요소가 설정 된 경우 대량 작업에서 모든 행이 포함 됩니다. 카드가 SQL_DESC_ARRAY_STATUS_PTR 필드에 값이 null 포인터 이면 모든 행의 대량 작업에 포함 됩니다. 해석은은 포인터가 유효한 배열 가리키는 배열의 모든 요소 SQL_ROW_PROCEED 것 처럼 동일 합니다. 배열의 요소 SQL_ROW_IGNORE로 설정 된 경우 무시 행을 행 상태 배열에 값을 변경 되지 않습니다.  
  
 이 필드는 카드가에서 호출 하 여 설정할 수도 있습니다 **SQLSetStmtAttr** SQL_ATTR_ROW_OPERATION_PTR 특성을 사용 합니다.  
  
 APD,이 헤더 필드 지 여부를 나타내는이 매개 변수이 집합이 되도록 응용 프로그램에서 설정할 수 있는 값의 매개 변수 작업 배열을 가리킵니다 때 무시 **SQLExecute** 또는 **SQLExecDirect**라고 합니다. 배열의 요소에는 다음 값을 포함할 수 있습니다.  
  
-   SQL_PARAM_PROCEED: 매개 변수 집합에 포함 되어는 **SQLExecute** 하거나 **SQLExecDirect** 호출 합니다.  
  
-   SQL_PARAM_IGNORE: 매개 변수 집합에서 제외 되는 **SQLExecute** 하거나 **SQLExecDirect** 호출 합니다.  
  
 모든 배열에 매개 변수 집합에 사용 될 배열 요소가 설정 된 경우는 **SQLExecute** 하거나 **SQLExecDirect** 호출 합니다. APD의 SQL_DESC_ARRAY_STATUS_PTR 필드의 값이 null 포인터 이면 모든 매개 변수 집합이 사용 됩니다. 해석은은 포인터가 유효한 배열 가리키는 배열의 모든 요소 SQL_PARAM_PROCEED 것 처럼 동일 합니다.  
  
 APD의이 필드를 호출 하 여 설정할 수도 있습니다 **SQLSetStmtAttr** SQL_ATTR_PARAM_OPERATION_PTR 특성을 사용 합니다.  
  
 **[응용 프로그램 설명자] SQL_DESC_BIND_OFFSET_PTR**  
 이 SQLLEN * 헤더 필드 가리키는 바인딩 오프셋입니다. 기본적으로 null 포인터로 설정 됩니다. 이 필드는 null 포인터를 없는 경우 드라이버는 포인터를 역참조 하 고 각 설명자 레코드 (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, 및 SQL_DESC_OCTET_LENGTH_PTR)의 null이 아닌 값이 있는 지연 된 필드에 역참조 된 값을 추가 에 바인딩할 때 시간 및 사용 하 여 새 포인터 값을 가져옵니다.  
  
 바인딩 오프셋은 항상 SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, 및 SQL_DESC_OCTET_LENGTH_PTR 필드의 값에 직접 추가 됩니다. 오프셋을 다른 값으로 변경 되 면 각 설명자 필드의 값에 직접 새 값 추가 계속 됩니다. 모든 이전 오프셋을 더한 필드 값을 새 오프셋 추가 되지 않습니다.  
  
 이 필드를 *지연 된 필드*: 설정 되어 있지만 데이터 버퍼에 대 한 주소를 확인 해야 할 경우 드라이버에서 나중에 사용 시 사용 되지 않습니다.  
  
 이 필드는 카드가에서 호출 하 여 설정할 수도 있습니다 **SQLSetStmtAttr** SQL_ATTR_ROW_BIND_OFFSET_PTR 특성을 사용 합니다. 이 필드는 카드가에서 호출 하 여 설정할 수도 있습니다 **SQLSetStmtAttr** SQL_ATTR_PARAM_BIND_OFFSET_PTR 특성을 사용 합니다.  
  
 자세한 내용은 행 단위 바인딩은에 대 한 설명은 참조 하세요 [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) 하 고 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)합니다.  
  
 **[응용 프로그램 설명자] SQL_DESC_BIND_TYPE**  
 이 SQLUINTEGER 헤더 필드에는 열 또는 매개 변수를 바인딩하는 데 사용할 바인딩 방향을 설정 합니다.  
  
 ARDs에서이 필드는 바인딩 방향을 지정 하면 **SQLFetchScroll** 또는 **SQLFetch** 관련된 문 핸들에서 호출 됩니다.  
  
 열에 대 한 열 단위 바인딩을 선택 하려면을 sql_bind_by_column으로 설정 (기본값)이이 필드를 설정 합니다.  
  
 이 필드는 카드가에서 호출 하 여 설정할 수도 있습니다 **SQLSetStmtAttr** 를 SQL_ATTR_ROW_BIND_TYPE을 사용 하 여 *특성*합니다.  
  
 Apd,이 필드는 데 동적 매개 변수 바인딩 방향을 지정 합니다.  
  
 열 단위 바인딩 매개 변수를 선택 하려면을 sql_bind_by_column으로 설정 (기본값)이이 필드를 설정 합니다.  
  
 APD의이 필드를 호출 하 여 설정할 수도 있습니다 **SQLSetStmtAttr** 를 SQL_ATTR_PARAM_BIND_TYPE로 *특성*합니다.  
  
 **SQL_DESC_COUNT [All]**  
 이 SQLSMALLINT 헤더 필드 지정 데이터를 포함 하는 번호가 가장 큰 레코드의 인덱스 1부터 시작 합니다. 드라이버는 설명자에 대 한 데이터 구조를 설정 하면 상당한 수 있는 레코드 수를 표시 하려면 SQL_DESC_COUNT 필드를 설정할 수도 있어야 합니다. 응용 프로그램에서이 데이터 구조체의 인스턴스를 할당 하는 경우를 위한 공간을 예약 하는 레코드 수를 지정 하는 것이 없습니다. 응용 프로그램 레코드의 콘텐츠를 지정 하는 대로 드라이버는 설명자 핸들을 적절 한 크기의 데이터 구조를 가리키는지 확인에 필요한 모든 작업을 수행 합니다.  
  
 SQL_DESC_COUNT (필드는 카드가 경우)에 바인딩되는 모든 데이터 열 또는 (필드는 APD 경우)에 바인딩되어 있는 모든 매개 변수의 수 없는 있지만 번호가 가장 큰 레코드의 수입니다. 번호가 가장 높은 열 또는 매개 변수 바인딩 해제 되는 경우에 다음 번호가 가장 높은 열 또는 매개 변수의 수 SQL_DESC_COUNT 변경 됩니다. 열 또는 여러 매개 변수가 하는 경우 가장 높은 열 수가 바인딩되지 미만 (호출 하 여 **SQLBindCol** 사용 하 여 합니다 *TargetValuePtr* 인수가 null 포인터 이거나 로**SQLBindParameter** 사용 하 여는 *ParameterValuePtr* 인수가 null 포인터로 설정), SQL_DESC_COUNT 변경 되지 않습니다. 추가 열 또는 매개 변수 데이터를 포함 하는 번호가 가장 높은 레코드 보다 큰 숫자를 사용 하 여 바인딩된 경우 드라이버 SQL_DESC_COUNT 필드의 값을 자동으로 증가 합니다. 호출 하 여 모든 열은 바인딩되지 않은 경우 **SQLFreeStmt** SQL_UNBIND 옵션과 카드가 및 IRD SQL_DESC_COUNT 필드를 0으로 설정 됩니다. 하는 경우 **SQLFreeStmt** 라고 SQL_RESET_PARAMS 옵션을 사용 하 여 APD IPD의 SQL_DESC_COUNT 필드는 0으로 설정 됩니다.  
  
 SQL_DESC_COUNT에서 값을 호출 하 여 명시적으로 응용 프로그램에서 설정할 수 있습니다 **SQLSetDescField**합니다. SQL_DESC_COUNT 값을 명시적으로 줄이면 SQL_DESC_COUNT의 새 값 보다 큰 숫자를 사용 하 여 모든 레코드 효과적으로 제거 됩니다. SQL_DESC_COUNT 값 0으로 명시적으로 설정 되는 카드가에 필드가 있는지 바인딩된 책갈피 열을 제외한 모든 데이터 버퍼가 해제 됩니다.  
  
 Record count는 카드가이 필드에 바인딩된 책갈피 열을 포함 하지 않습니다. 책갈피 열을 바인딩 해제 하는 유일한 방법은 null 포인터로 SQL_DESC_DATA_PTR 필드가 설정 하는 것입니다.  
  
 **SQL_DESC_ROWS_PROCESSED_PTR [구현 설명자]**  
 이 SQLULEN는 ird \* 헤더 필드가 가리키는 버퍼에 대 한 호출 후 가져온 행 수를 포함 하 **SQLFetch** 하거나 **SQLFetchScroll**, 또는 대량 작업에서 영향을 받는 행 수 에 대 한 호출을 수행한 **SQLBulkOperations** 하거나 **SQLSetPos**, 오류 행을 포함 합니다.  
  
 이 SQLUINTEGER는 IPD의 * 처리 된 경우 오류 집합을 포함 하는 매개 변수 집합 수를 포함 하는 버퍼를 헤더 필드 가리킵니다. 이 null 포인터인 경우 번호가 없으면 반환 됩니다.  
  
 SQL_DESC_ROWS_PROCESSED_PTR SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 호출한 후 반환 된 후에 유효 **SQLFetch** 하거나 **SQLFetchScroll** IRD 필드) (의 또는 **SQLExecute** , **SQLExecDirect**, 또는 **SQLParamData** (한 IPD 필드). 가리키는 버퍼에 채우는 호출 하는 경우이 필드와 관계 없이 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 반환 하지 않는에서 SQL_NO_DATA를 0으로 설정 되어 있는 경우 버퍼의 값을 반환 하지 않는 한 버퍼의 내용이 정의 되지 않습니다.  
  
 이 필드는 카드가에서 호출 하 여 설정할 수도 있습니다 **SQLSetStmtAttr** SQL_ATTR_ROWS_FETCHED_PTR 특성을 사용 하 여 합니다. APD의이 필드를 호출 하 여 설정할 수도 있습니다 **SQLSetStmtAttr** SQL_ATTR_PARAMS_PROCESSED_PTR 특성을 사용 하 여 합니다.  
  
 이 필드에서 가리키는 버퍼는 응용 프로그램에 의해 할당 됩니다. 이 드라이버에 의해 설정 된 지연 된 출력 버퍼입니다. 기본적으로 null 포인터로 설정 됩니다.  
  
## <a name="record-fields"></a>레코드 필드  
 각 설명자 필드 열 데이터 또는 설명자의 유형에 따라 동적 매개 변수를 정의 하는 구성 된 하나 이상의 레코드를 포함 합니다. 각 레코드는 단일 열 또는 매개 변수를의 전체 정의 합니다.  
  
 **SQL_DESC_AUTO_UNIQUE_VALUE [IRDs]**  
 이 읽기 전용 SQLINTEGER 레코드 필드 열이 자동 증분 열 또는 SQL_FALSE 열의 자동 증분 열이 아닌 경우 SQL_TRUE를 포함 합니다. 이 필드는 읽기 전용 이며 아닌 내부 자동 증분 열은 읽기 전용 반드시 합니다.  
  
 **SQL_DESC_BASE_COLUMN_NAME [IRDs]**  
 이 읽기 전용 SQLCHAR * 레코드 필드는 결과 집합 열에 대 한 기본 열 이름을 포함 합니다. 기본 열 이름 (예: 열을 식의 경우) 존재 하지 않는 경우이 변수는 빈 문자열을 포함 합니다.  
  
 **SQL_DESC_BASE_TABLE_NAME [IRDs]**  
 이 읽기 전용 SQLCHAR * 레코드 필드는 결과 집합 열에 대 한 기본 테이블 이름을 포함 합니다. 기본 테이블 이름을 정의할 수 없습니다 또는 적용할 수 없는 경우이 변수는 빈 문자열을 포함 합니다.  
  
 **SQL_DESC_CASE_SENSITIVE [구현 설명자]**  
 이 읽기 전용 SQLINTEGER 레코드 필드 포함 sql_true는 해당 열 또는 매개 변수는 처리 SQL_FALSE 데이터 정렬 및 비교에 대/소문자 구분 문자는 경우 또는 열 데이터 정렬 및 비교에 대 한 대/소문자 구분으로 처리 되 면 열입니다.  
  
 **SQL_DESC_CATALOG_NAME [IRDs]**  
 이 읽기 전용 SQLCHAR * 레코드 필드 열이 포함 된 기본 테이블에 대 한 카탈로그를 포함 합니다. 반환 값 또는 열이 뷰의 일부 열이 식이면 드라이버에 따라 다릅니다는입니다. 데이터 소스는 카탈로그를 지원 하지 않습니다 또는 카탈로그를 확인할 수 없는 경우이 변수는 빈 문자열을 포함 합니다.  
  
 **SQL_DESC_CONCISE_TYPE [All]**  
 이 SQLSMALLINT 헤더 필드에 날짜/시간 및 간격 데이터 유형을 포함 하는 모든 데이터 형식에 대해 간결한 데이터 형식을 지정 합니다.  
  
 SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE을 SQL_DESC_DATETIME_INTERVAL_CODE 필드의 값은 상호 종속적입니다. 다른 설정 해야 하는 필드 중 각 시간 설정 됩니다. SQL_DESC_CONCISE_TYPE를 호출 하 여 설정할 수 있습니다 **SQLBindCol** 하거나 **SQLBindParameter**, 또는 **SQLSetDescField**합니다. 호출 하 여 SQL_DESC_TYPE을 설정할 수 있습니다 **SQLSetDescField** 하거나 **SQLSetDescRec**합니다.  
  
 SQL_DESC_CONCISE_TYPE를 간격 또는 날짜/시간 데이터 형식이 아닌 간결한 데이터 형식으로 설정 되어 SQL_DESC_TYPE 필드는 동일한 값으로 설정 됩니다 하 고 값을 SQL_DESC_DATETIME_INTERVAL_CODE 필드 0으로 설정 됩니다.  
  
 SQL_DESC_CONCISE_TYPE 간결한 datetime 또는 간격 데이터 형식으로 설정 되어 SQL_DESC_TYPE 필드는 해당 세부 정보 표시 형식 (SQL_DATETIME 또는 sql_interval 인)으로 설정 하 고 값을 SQL_DESC_DATETIME_INTERVAL_CODE 필드 적절 한 하위 코드에 설정 됩니다.  
  
 **[응용 프로그램 설명자 및 IPDs] SQL_DESC_DATA_PTR**  
 이 대 SQLPOINTER 레코드 필드에는 매개 변수 값 (Apd) 또는 (ARDs)에 대 한 열 값을 포함 하는 변수를 가리킵니다. 이 필드를 *지연 된 필드*합니다. 설정 되어 있지만 데이터를 검색 하는 드라이버에서 나중에 사용 시 사용 되지 않습니다.  
  
 경우에 카드가의 SQL_DESC_DATA_PTR 필드가 지정 된 열의 바인딩 해제 되었는지 합니다 *TargetValuePtr* 호출에서 인수 **SQLBindCol** 이 null 포인터 이거나는 SQL_DESC_DATA_PTR 필드가 카드가 설정한는 에 대 한 호출 **SQLSetDescField** 또는 **SQLSetDescRec** null 포인터입니다. 다른 필드는 null 포인터는 SQL_DESC_DATA_PTR 필드가 설정 된 경우에 영향이 없습니다.  
  
 경우에 대 한 호출 **SQLFetch** 하거나 **SQLFetchScroll** 는 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 입력 한 후가이 필드에서 가리키는 버퍼에 반환 하지 않았습니다, 버퍼의 내용을 정의 되지 않습니다.  
  
 IPD, 카드가, APD의 SQL_DESC_DATA_PTR 필드가 설정 될 때마다 드라이버 SQL_DESC_TYPE 필드의 값이 유효한 ODBC C 데이터 형식 또는 드라이버별 데이터 형식 중 하나에 및 데이터 형식에 영향을 주는 다른 모든 필드는 일치를 확인 합니다. 일관성 확인 메시지를 표시는 IPD의 SQL_DESC_DATA_PTR 필드가 사용 하는 것입니다. 특히, 응용 프로그램을 IPD 및 나중에 호출 SQL_DESC_DATA_PTR 필드가 설정 **SQLGetDescField** 이 필드에서 반환 되지 않습니다 반드시 설정 해야 하는 값입니다. 자세한 내용은 "일관성 확인"의 참조 [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)합니다.  
  
 **SQL_DESC_DATETIME_INTERVAL_CODE [All]**  
 이 SQLSMALLINT 레코드 필드 SQL_DESC_TYPE 필드 SQL_DATETIME 또는 sql_interval 인 경우 특정 날짜/시간 또는 간격 데이터 형식에 대 한 하위 코드를 포함 합니다. 이것이 SQL 및 C 데이터 형식에 대해 true입니다. 코드는 데이터 형식 이름 (날짜/시간 형식)에 대 한 "TYPE" 또는 "C_TYPE" 대체 "코드" 또는 "CODE" (간격 유형)에 대 한 "INTERVAL" 또는 "C_INTERVAL"에 대 한 대체를 사용 하 여 구성 됩니다.  
  
 SQL_DESC_TYPE 및 응용 프로그램 설명자를에서 SQL_DESC_CONCISE_TYPE SQL_C_DEFAULT로 설명자를 문 핸들을 사용 하 여 연결 되지 경우 값을 SQL_DESC_DATETIME_INTERVAL_CODE의 내용을 정의 되지 않습니다.  
  
 이 필드는 다음 표에 나열 된 날짜/시간 데이터 형식에 대해 설정할 수 있습니다.  
  
|날짜/시간 형식|DATETIME_INTERVAL_CODE|  
|--------------------|------------------------------|  
|SQL_TYPE_DATE/SQL_C_TYPE_DATE|SQL_CODE_DATE|  
|SQL_TYPE_TIME/SQL_C_TYPE_TIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP/ SQL_C_TYPE_TIMESTAMP|SQL_CODE_TIMESTAMP|  
  
 이 필드는 다음 표에 나열 된 간격 데이터 형식에 대해 설정할 수 있습니다.  
  
|간격 유형|DATETIME_INTERVAL_CODE|  
|-------------------|------------------------------|  
|SQL_INTERVAL_DAY/ SQL_C_INTERVAL_DAY|SQL_CODE_DAY|  
|SQL_INTERVAL_DAY_TO_HOUR/ SQL_C_INTERVAL_DAY_TO_HOUR|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE/ SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_CODE_DAY_TO_MINUTE|  
|SQL_INTERVAL_DAY_TO_SECOND/ SQL_C_INTERVAL_DAY_TO_SECOND|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR / SQL_C_INTERVAL_HOUR|SQL_CODE_HOUR|  
|SQL_INTERVAL_HOUR_TO_MINUTE/ SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND / SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE/ SQL_C_INTERVAL_MINUTE|SQL_CODE_MINUTE|  
|SQL_INTERVAL_MINUTE_TO_SECOND/ SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_CODE_MINUTE_TO_SECOND|  
|SQL_INTERVAL_MONTH/ SQL_C_INTERVAL_MONTH|SQL_CODE_MONTH|  
|SQL_INTERVAL_SECOND/ SQL_C_INTERVAL_SECOND|SQL_CODE_SECOND|  
|SQL_INTERVAL_YEAR / SQL_C_INTERVAL_YEAR|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH / SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_CODE_YEAR_TO_MONTH|  
  
 데이터 간격으로이 필드에 대 한 자세한 내용은 참조 하세요. [데이터 형식 식별자 및 설명자](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)합니다.  
  
 **SQL_DESC_DATETIME_INTERVAL_PRECISION [All]**  
 이 SQLINTEGER 레코드 필드 SQL_DESC_TYPE 필드 sql_interval 인 경우 전체 자릿수를 유도 하는 간격을 포함 합니다. 값을 SQL_DESC_DATETIME_INTERVAL_CODE 필드 간격 데이터 형식으로 설정 되 면이 필드는 전체 자릿수를 유도 기본 간격으로 설정 됩니다.  
  
 **SQL_DESC_DISPLAY_SIZE [IRDs]**  
 이 읽기 전용 SQLINTEGER 레코드 필드 열에서 데이터를 표시 하는 데 필요한 문자의 최대 수를 포함 합니다.  
  
 **SQL_DESC_FIXED_PREC_SCALE [구현 설명자]**  
 열, 고정된 전체 자릿수와 소수 자릿수를 사용 하 여 정확한 숫자 열이 아닌 경우이 읽기 전용 SQLSMALLINT 레코드 필드는 SQL_FALSE 또는 열이 정확한 숫자 열이 있고 고정 전체 자릿수 및 0이 아닌 확장 SQL_TRUE로 설정 됩니다.  
  
 **[응용 프로그램 설명자] SQL_DESC_INDICATOR_PTR**  
 ARDs,이 SQLLEN에서에서 * 필드 요소는 표시자 변수를 기록 합니다. 이 변수는 열 값이 NULL은 모두 SQL_NULL_DATA를 포함 합니다. Apd, 표시기 변수의 NULL 동적 인수를 지정 하려면은 모두 SQL_NULL_DATA로 설정 됩니다. 그렇지 않으면 변수는 0 (SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR 값과 같은 포인터 않는)입니다.  
  
 카드가 SQL_DESC_INDICATOR_PTR 필드가 null 포인터, 드라이버 열 NULL 인지 여부에 대 한 정보를 반환 하지 않습니다. 열이 NULL 이면 SQL_DESC_INDICATOR_PTR가 null 포인터, SQLSTATE 22002 (지표 변수가 필요 하지만 제공 되지)는 반환 드라이버를 호출한 후 버퍼를 채우는 하려고 할 때 **SQLFetch** 또는  **SQLFetchScroll**합니다. 경우에 대 한 호출 **SQLFetch** 하거나 **SQLFetchScroll** SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 버퍼의 내용 정의 되지 않습니다. 반환 하지 않았습니다.  
  
 SQL_DESC_INDICATOR_PTR 필드 SQL_DESC_OCTET_LENGTH_PTR 가리키는 필드를 설정할지 여부를 결정 합니다. 열에 대 한 데이터 값이 NULL 인 경우 드라이버는 표시자 변수를 sql_null_data로 설정 합니다. SQL_DESC_OCTET_LENGTH_PTR 가리키는 필드 다음 설정 되지 않았습니다. NULL 값을 인출 하는 동안 발생 하지 않습니다, SQL_DESC_INDICATOR_PTR 가리키는 버퍼를 0으로 설정 되 고 SQL_DESC_OCTET_LENGTH_PTR 가리키는 버퍼 데이터의 길이를 설정 합니다.  
  
 APD의 SQL_DESC_INDICATOR_PTR 필드가 null 포인터인 경우 응용 프로그램 NULL 인수를 지정 하려면이 설명자 레코드를 사용할 수 없습니다.  
  
 이 필드를 *지연 된 필드*: 설정 되어 있지만 (하기 위한 ARDs) null 허용 여부를 나타내는 또는 null 허용 여부 (Apd)을 결정 하려면 드라이버에서 나중에 사용 시 사용 되지 않습니다.  
  
 **SQL_DESC_LABEL [IRDs]**  
 이 읽기 전용 SQLCHAR * 열 레이블 또는 제목 레코드 필드에 포함 되어 있습니다. 열에 레이블을 찾을 수 없는 경우이 변수는 열 이름을 포함 합니다. 명명 되지 않은 열은 레이블이 없는 경우,이 변수는 빈 문자열을 포함 합니다.  
  
 **SQL_DESC_LENGTH [All]**  
 이 SQLULEN 레코드 필드는 문자로 문자열의 최대 또는 실제 길이 이거나 바이트의 이진 데이터 형식입니다. 고정 길이 데이터 형식에 대 한 최대 길이 또는 가변 길이 데이터 형식에 대 한 실제 길이입니다. 해당 값에는 항상 문자열을 종료 하는 null 종결 문자가 제외 됩니다. SQL_TYPE_DATE, SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP, 또는 SQL 간격 데이터 형식 중 하나는 형식의 값에 대 한이 필드는 datetime 또는 간격 값의 문자 문자열 표현의 문자 길이 있습니다.  
  
 이 필드의 값 길이 대 한""로 ODBC 2에 정의 된 값에서 다를 수 있습니다 *.x*합니다. 자세한 내용은 참조 하세요. [부록 d: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md)합니다.  
  
 **SQL_DESC_LITERAL_PREFIX [IRDs]**  
 이 읽기 전용 SQLCHAR *이 데이터 형식의 리터럴에 접두사로 드라이버 인식 하는 문자를 레코드 필드에 포함 되어 있습니다. 이 변수는 리터럴 접두사는 해당 데이터 형식에 대 한 빈 문자열을 포함 합니다.  
  
 **SQL_DESC_LITERAL_SUFFIX [IRDs]**  
 이 읽기 전용 SQLCHAR * 레코드 필드에이 데이터 형식의 리터럴에 접미사로 드라이버 인식 하는 문자를 포함 합니다. 이 변수는에 대 한 리터럴 접미사는 해당 데이터 형식에 대 한 빈 문자열을 포함 합니다.  
  
 **SQL_DESC_LOCAL_TYPE_NAME [구현 설명자]**  
 이 읽기 전용 SQLCHAR * 레코드 필드 데이터 형식의 일반 이름과 다를 수 있는 데이터 형식에 대 한 모든 지역화 된 (native language) 이름이 포함 됩니다. 지역화 된 이름이 없는 경우 빈 문자열이 반환 됩니다. 이 필드는 표시 용도로 됩니다.  
  
 **SQL_DESC_NAME [구현 설명자]**  
 이 SQLCHAR * 레코드 필드를 행 설명자에 적용 되는 경우 열 별칭이 포함 되어 있습니다. 열 별칭이 적용 되지 않는 경우 열 이름이 반환 됩니다. 두 경우 모두 드라이버 SQL_DESC_NAME 필드 설정 하는 경우를 SQL_NAMED SQL_DESC_UNNAMED 필드를 설정 합니다. 열 이름 없음 또는 열 별칭을 있으면 드라이버 SQL_DESC_NAME 필드에 빈 문자열을 반환 하 고 하면 SQL_DESC_UNNAMED 필드 설정 됩니다.  
  
 응용 프로그램 매개 변수 이름 또는 이름으로 저장된 프로시저 매개 변수를 지정 하는 별칭 SQL_DESC_NAME 필드는 IPD의를 설정할 수 있습니다. (자세한 내용은 [Binding Parameters by Name (Named Parameters)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md).) IRD의 SQL_DESC_NAME 필드는 읽기 전용 필드입니다. SQLSTATE HY091 응용 프로그램을 설정 하려는 경우 (잘못 된 설명자 필드 식별자)이 반환 됩니다.  
  
 IPDs에서 드라이버 명명 된 매개 변수를 지원 하지 않는 경우이 필드는 정의 되지 않습니다. 드라이버 명명 된 매개 변수를 지원 하는 매개 변수를 설명 하는 수 하는 경우이 필드에 매개 변수 이름이 반환 됩니다.  
  
 **SQL_DESC_NULLABLE [구현 설명자]**  
 IRDs,이 읽기 전용 SQLSMALLINT 레코드 필드에서는 SQL_NULLABLE 열 값이 있는 경우 NULL, SQL_NO_NULLS 열에 NULL 값이 없는 경우 또는 SQL_NULLABLE_UNKNOWN 경우 열에 NULL 값 허용 하는지 여부를 알 수 없습니다. 이 필드는 결과 집합 열, 기본 열에 적용 됩니다.  
  
 IPDs,이 필드 동적 매개 변수는 항상 null을 허용 하 고 응용 프로그램에서 설정할 수 없습니다 때문에 메시지가 SQL_NULLABLE를 항상 설정 됩니다.  
  
 **SQL_DESC_NUM_PREC_RADIX [All]**  
 이 SQLINTEGER 필드에 값 2의 SQL_DESC_TYPE 필드의 데이터 형식이 근사 숫자 데이터 형식, SQL_DESC_PRECISION 필드 비트 수 있기 때문에 있습니다. 이 필드에 값 10의 SQL_DESC_TYPE 필드에서 해당 데이터 형식의 경우 정확한 숫자 데이터 형식의 경우 SQL_DESC_PRECISION 필드 10 진수 수 있기 때문에 합니다. 이 필드는 모든 숫자가 아닌 데이터 형식에 대해 0으로 설정 됩니다.  
  
 **SQL_DESC_OCTET_LENGTH [All]**  
 이 SQLLEN 레코드 필드에 문자열 또는 이진 데이터 형식의 길이 (바이트)를 포함합니다. 고정 길이 문자 또는 이진 형식의 실제 길이 (바이트)입니다. 가변 길이 문자 또는 이진 형식의 최대 길이 (바이트)입니다. 이 값이 항상 구현 설명자에 대 한 null 종료 문자에 대 한 공간을 제외 하 고 항상 응용 프로그램 설명자에 대 한 null 종료 문자에 대 한 공간을 포함 합니다. 응용 프로그램 데이터에 대 한이 필드는 버퍼의 크기를 포함합니다. Apd, 출력 또는 입출력 매개 변수에만이 필드 정의 됩니다.  
  
 **[응용 프로그램 설명자] SQL_DESC_OCTET_LENGTH_PTR**  
 이 SQLLEN * 필드 요소 (매개 변수 설명자)에 대 한 동적 인수 또는 바인딩된 열 값 (예: 행 설명자)의 총 길이 (바이트)를 포함 하는 변수에 기록 합니다.  
  
 APD에 대 한이 값은 문자열 및 이진;를 제외한 모든 인수에 대해 무시 됩니다. 이 필드 SQL_NTS를 가리키는 경우 동적 인수 null로 종결 되어야 합니다. SQL_DATA_AT_EXEC 값 또는 SQL_LEN_DATA_AT_EXEC 매크로의 결과가 포함 됩니다, 하는 바인딩된 매개 변수는 실행 시 데이터 매개 변수 수는 응용 프로그램이이 필드는 APD의 적절 한 레코드 변수에 설정, 실행 시간 . 이러한 필드를 둘 이상 있으면 응용 프로그램 매개 변수를 요청 하는 결정 하는 데 매개 변수를 고유 하 게 식별 하는 값에 SQL_DESC_DATA_PTR은 설정할 수 있습니다.  
  
 카드가의 OCTET_LENGTH_PTR 필드가 null 포인터인 경우 드라이버는 열에 대 한 길이 정보를 반환 하지 않습니다. APD의 SQL_DESC_OCTET_LENGTH_PTR 필드에 null 포인터 이면 문자열 및 이진 값은 null로 종료 되는 드라이버를 가정 합니다. (이진 값 null 종료 하지 않아야 하지만 잘리지 않도록 하려면 길이 지정 해야 합니다.)  
  
 경우에 대 한 호출 **SQLFetch** 하거나 **SQLFetchScroll** 는 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 입력 한 후가이 필드에서 가리키는 버퍼에 반환 하지 않았습니다, 버퍼의 내용을 정의 되지 않습니다. 이 필드를 *지연 된 필드*합니다. 설정 되어 있지만 확인 하거나 데이터의 8 진수 길이 나타냅니다 드라이버에 의해 나중에 사용 시 사용 되지 않습니다.  
  
 **SQL_DESC_PARAMETER_TYPE [IPDs]**  
 이 SQLSMALLINT 레코드 필드를 입력 매개 변수를 입/출력 매개 변수, 출력 매개 변수를 입/출력 스트리밍 매개 변수를 SQL_PARAM_INPUT_OUTPUT_STREAM 또는 SQL_ SQL_PARAM_OUTPUT SQL_PARAM_INPUT_OUTPUT SQL_PARAM_INPUT로 PARAM_OUTPUT_STREAM 스트리밍되는 출력 매개 변수입니다. 기본적으로 SQL_PARAM_INPUT에 설정 됩니다.  
  
 IPD에 대 한 필드는 IPD (SQL_ATTR_ENABLE_AUTO_IPD 문 특성이 SQL_FALSE) 드라이버에 의해 자동으로 채워지지 않는 경우 기본적으로 SQL_PARAM_INPUT에 설정 됩니다. 응용 프로그램은 입력된 매개 변수 없는 매개 변수에 대해 IPD의이 필드를 설정 해야 합니다.  
  
 **SQL_DESC_PRECISION [All]**  
 정확한 숫자 형식가 수 (이진 정밀도)는 근사 숫자 형식에 대 한 비트 수 또는 자릿수 SQL_TYPE SQL_TYPE_TIME, 소수 자릿수 초 구성 요소에서 숫자 자릿수를 포함 하는이 SQLSMALLINT 레코드 필드 _TIMESTAMP, 또는 SQL_INTERVAL_SECOND 데이터 형식입니다. 이 필드를 다른 모든 데이터 형식에 대 한 정의 되지 않습니다.  
  
 이 필드의 값이 "precision"로 ODBC 2에 정의 된 값에서 다를 수 있습니다 *.x*합니다. 자세한 내용은 참조 하세요. [부록 d: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md)합니다.  
  
 **SQL_DESC_ROWVER [구현 설명자]**  
 이 SQLSMALLINTrecord 필드 열 수정 되었는지 여부를 자동으로 DBMS에 의해 (예: SQL Server에서 "timestamp" 형식의 열) 행이 업데이트 될 때를 나타냅니다. 그렇지 않은 경우이 레코드 필드의 값은 SQL_FALSE 하는 열이 행 버전 관리 열 이면 SQL_TRUE로 설정 됩니다. 이 열 특성은 호출과 비슷하지만 **SQLSpecialColumns** IdentifierType의 SQL_ROWVER 열을 자동으로 업데이트 되는지 여부를 확인 하려면를 사용 하 여 합니다.  
  
 **SQL_DESC_SCALE [All]**  
 이 SQLSMALLINT 레코드 필드 decimal 및 numeric 데이터 형식에 대해 정의 된 확장을 포함합니다. 필드를 다른 모든 데이터 형식에 대 한 정의 되지 않습니다.  
  
 이 필드의 값이 "scale" ODBC 2에 정의 된 값에서 다를 수 있습니다 *.x*합니다. 자세한 내용은 참조 하세요. [부록 d: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md)합니다.  
  
 **SQL_DESC_SCHEMA_NAME [IRDs]**  
 이 읽기 전용 SQLCHAR * 레코드 필드에 열이 포함 된 기본 테이블의 스키마 이름을 포함 합니다. 반환 값 또는 열이 뷰의 일부 열이 식이면 드라이버에 따라 다릅니다는입니다. 데이터 원본 스키마를 지원 하지 않으므로 또는 스키마 이름을 확인할 수 없는 경우이 변수는 빈 문자열을 포함 합니다.  
  
 **SQL_DESC_SEARCHABLE [IRDs]**  
 이 읽기 전용 SQLSMALLINT 레코드 필드는 다음 값 중 하나로 설정 됩니다.  
  
-   SQL_PRED_NONE 열에서 사용할 수 없는 경우는 **여기서** 절. (이 ODBC 2 SQL_UNSEARCHABLE 값 동일 *.x*.)  
  
-   SQL_PRED_CHAR 열에서 사용할 수 있는 경우는 **여기서** 절만 합니다 **같은** 조건자입니다. (이 ODBC 2 SQL_LIKE_ONLY 값 동일 *.x*.)  
  
-   SQL_PRED_BASIC 열에서 사용할 수 있는 경우는 **여기서** 제외한 모든 비교 연산자를 사용 하 여 절 **와 같은**합니다. (이 ODBC 2 SQL_EXCEPT_LIKE 값 동일 *.x*.)  
  
-   SQL_PRED_SEARCHABLE 열에서 사용할 수 있는 경우는 **여기서** 임의의 비교 연산자를 사용 하 여 절.  
  
 **SQL_DESC_TABLE_NAME [IRDs]**  
 이 읽기 전용 SQLCHAR * 레코드 필드에는이 열이 포함 된 기본 테이블의 이름을 포함 합니다. 반환 값 또는 열이 뷰의 일부 열이 식이면 드라이버에 따라 다릅니다는입니다.  
  
 **SQL_DESC_TYPE [All]**  
 이 SQLSMALLINT 레코드 필드에 날짜/시간 및 간격 데이터 형식 제외한 모든 데이터 형식에 대 한 간단한 SQL 또는 C 데이터 형식을 지정합니다. 날짜/시간 및 간격 데이터 형식에 대 한이 필드는 자세한 데이터 형식을 SQL_DATETIME 또는 sql_interval 인을 지정 합니다.  
  
 이 필드에 SQL_DATETIME 또는 sql_interval 인 때마다 값을 SQL_DESC_DATETIME_INTERVAL_CODE 필드 간결한 형식에 대 한 적절 한 하위 코드를 포함 해야 합니다. 날짜/시간 데이터 형식에 대 한 SQL_DESC_TYPE SQL_DATETIME, 있어서 값을 SQL_DESC_DATETIME_INTERVAL_CODE 필드에 특정 날짜/시간 데이터 형식에 대 한 하위 코드가 포함 되어 있습니다. 간격 데이터 형식에 대 한 SQL_DESC_TYPE SQL_INTERVAL 있어서 값을 SQL_DESC_DATETIME_INTERVAL_CODE 필드에 특정 간격 데이터 형식에 대 한 하위 코드가 포함 되어 있습니다.  
  
 SQL_DESC_CONCISE_TYPE SQL_DESC_TYPE 필드에서 값은 상호 종속적입니다. 다른 설정 해야 하는 필드 중 각 시간 설정 됩니다. 호출 하 여 SQL_DESC_TYPE을 설정할 수 있습니다 **SQLSetDescField** 하거나 **SQLSetDescRec**합니다. SQL_DESC_CONCISE_TYPE를 호출 하 여 설정할 수 있습니다 **SQLBindCol** 하거나 **SQLBindParameter**, 또는 **SQLSetDescField**합니다.  
  
 SQL_DESC_TYPE을 간격 또는 날짜/시간 데이터 형식이 아닌 간결한 데이터 형식으로 설정 되어 SQL_DESC_CONCISE_TYPE 필드는 동일한 값으로 설정 됩니다 하 고 값을 SQL_DESC_DATETIME_INTERVAL_CODE 필드를 0으로 설정 됩니다.  
  
 SQL_DESC_TYPE을 자세한 날짜/시간 또는 간격 데이터 형식 (SQL_DATETIME 또는 sql_interval 인)로 설정 되어 값을 SQL_DESC_DATETIME_INTERVAL_CODE 필드를 적절 한 하위 코드를로 설정 하 고 SQL_DESC_CONCISE 유형 필드는 해당 간결한 형식으로 설정 됩니다. SQL_DESC_TYPE 간결한 datetime 또는 간격 유형 중 하나를 설정 하려고 하면 SQLSTATE HY021 반환 됩니다 (일관성이 없는 설명자 정보).  
  
 SQL_DESC_TYPE 필드를 호출 하 여 설정 되 면 **SQLBindCol**하십시오 **SQLBindParameter**, 또는 **SQLSetDescField**, 다음 필드는 다음과 같은 기본 값으로 설정 됩니다 다음 표에서 같이 합니다. 동일한 레코드의 나머지 필드의 값이 정의 되지 않습니다.  
  
|SQL_DESC_TYPE 값|다른 필드 암시적으로 설정합니다.|  
|------------------------------|---------------------------------|  
|SQL_CHAR, SQL_VARCHAR, SQL_C_CHAR, SQL_C_VARCHAR|SQL_DESC_LENGTH 1로 설정 됩니다. SQL_DESC_PRECISION 0으로 설정 됩니다.|  
|SQL_DATETIME|값을 SQL_DESC_DATETIME_INTERVAL_CODE SQL_CODE_DATE SQL_CODE_TIME에 설정 되 면 SQL_DESC_PRECISION 0으로 설정 됩니다. 설정은 SQL_DESC_TIMESTAMP, SQL_DESC_PRECISION 6으로 설정 됩니다.|  
|SQL_DECIMAL, SQL_NUMERIC, SQL_C_NUMERIC|자릿수가 SQL_DESC_SCALE 0으로 설정 됩니다. SQL_DESC_PRECISION 각 데이터 형식에 대 한 구현 시 정의 된 정밀도로 설정 됩니다.<br /><br /> 참조 [c: SQL 숫자](../../../odbc/reference/appendixes/sql-to-c-numeric.md) 수동으로 SQL_C_NUMERIC 값을 바인딩하는 방법에 대 한 정보에 대 한 합니다.|  
|SQL_FLOAT, SQL_C_FLOAT|SQL_DESC_PRECISION SQL_FLOAT 구현 시 정의 된 기본 정밀도로 설정 됩니다.|  
|SQL_INTERVAL|값을 SQL_DESC_DATETIME_INTERVAL_CODE 간격 데이터 형식으로 설정 되 면 SQL_DESC_DATETIME_INTERVAL_PRECISION 2 (기본 간격 선행 정밀도)으로 설정 됩니다. 간격의 초 구성 요소에 있는 경우 자릿수가 SQL_DESC_PRECISION (기본 간격 초 전체 자릿수) 6으로 설정 됩니다.|  
  
 응용 프로그램을 호출할 때 **SQLSetDescField** 호출 하지 않고 설명자 필드를 설정 하려면 **SQLSetDescRec**, 응용 프로그램 데이터 형식을 먼저 선언 해야 합니다. 이 경우 이전 표에 나와 있는 다른 필드는 암시적으로 설정 됩니다. 경우 값 암시적으로 집합 허용 되지 않는 응용 프로그램을 호출할 수 있습니다 **SQLSetDescField** 하거나 **SQLSetDescRec** 사용할 수 없는 값을 명시적으로 설정 합니다.  
  
 **Sql_desc_type_name으로 [구현 설명자]**  
 이 읽기 전용 SQLCHAR * 레코드 필드는 데이터 원본에 종속적인 형식 이름 (예를 들어, "CHAR", "VARCHAR", 및 등)를 포함 합니다. 데이터 형식 이름을 알 수 없는 경우이 변수는 빈 문자열을 포함 합니다.  
  
 **SQL_DESC_UNNAMED [구현 설명자]**  
 SQL_DESC_NAME 필드 설정 하는 경우이 SQLSMALLINT 레코드 필드를 행 설명자에서 SQL_NAMED 또는 하면 드라이버에 의해 설정 됩니다. SQL_DESC_NAME 필드에는 열 별칭 또는 열 별칭이 적용 되지 않는 경우 드라이버는 SQL_DESC_UNNAMED 필드 SQL_NAMED를 설정 합니다. 매개 변수 이름 또는 별칭에는 IPD의 SQL_DESC_NAME 필드를 설정 하는 응용 프로그램, 드라이버를 SQL_NAMED IPD의 SQL_DESC_UNNAMED 필드를 설정 합니다. 열 이름 없음 또는 열 별칭을 있으면 드라이버 하면 SQL_DESC_UNNAMED 필드를 설정 됩니다.  
  
 응용 프로그램 하면을 SQL_DESC_UNNAMED 필드는 IPD의를 설정할 수 있습니다. 드라이버는 SQLSTATE HY091 반환 (잘못 된 설명자 필드 식별자) 응용 프로그램 SQL_DESC_UNNAMED 필드는 IPD의 SQL_NAMED로 설정 하려고 합니다. IRD의 SQL_DESC_UNNAMED 필드는 읽기 전용입니다. SQLSTATE HY091 응용 프로그램을 설정 하려는 경우 (잘못 된 설명자 필드 식별자)이 반환 됩니다.  
  
 **SQL_DESC_UNSIGNED [구현 설명자]**  
 이 읽기 전용 SQLSMALLINT 레코드 필드는 열 형식 서명 되 면 SQL_TRUE 열 형식은 부호 없는 또는 숫자가 아닌 경우 또는 SQL_FALSE 설정 됩니다.  
  
 **SQL_DESC_UPDATABLE [IRDs]**  
 이 읽기 전용 SQLSMALLINT 레코드 필드는 다음 값 중 하나로 설정 됩니다.  
  
-   SQL_ATTR_READ_ONLY 결과 집합 열은 읽기 전용입니다.  
  
-   SQL_ATTR_WRITE 결과 집합 열은 읽기-쓰기입니다.  
  
-   결과 집합 열이 있는지 여부를 알지 못하는 경우 SQL_ATTR_READWRITE_UNKNOWN 인지 업데이트할 수 있는 합니다.  
  
 SQL_DESC_UPDATABLE 결과 집합의 열, 기본 테이블의 열이 아닌 업데이트 가능성을 설명합니다. 이 결과 집합 열 기준으로 하는 기본 테이블의 열 업데이트 가능성은이 필드의 값 보다 달라질 수 있습니다. 열이 업데이트할 수 있는 데이터 형식, 사용자 권한 및 결과 집합 자체의 정의에 기반 할 수 있습니다. 열을 업데이트할 수 있는지 여부에 명확한 아니라면 SQL_ATTR_READWRITE_UNKNOWN 반환 되어야 합니다.  
  
## <a name="consistency-checks"></a>일관성 검사  
 일관성 확인을 응용 프로그램 카드가, APD, IPD의 SQL_DESC_DATA_PTR 필드에 대 한 값이 전달 될 때마다 드라이버에 의해 수행 됩니다. 필드를 다른 필드와 일치 하지 않습니다 하는 경우 **SQLSetDescField** SQLSTATE HY021를 반환 합니다 (일관성이 없는 설명자 정보). 자세한 내용은 "일관성 확인"의 참조 [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|열 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|매개 변수 바인딩|[SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|설명자 필드 가져오기|[SQLGetDescField 함수](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|여러 설명자 필드 가져오기|[SQLGetDescRec 함수](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|여러 설명자 필드 설정|[SQLSetDescRec 함수](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)
