---
description: SQLSetDescField 함수
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2c21d3a21e863d62a3cc8d685e81c6e3265c1551
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421137"
---
# <a name="sqlsetdescfield-function"></a>SQLSetDescField 함수

**규칙**  
 소개 된 버전: ODBC 3.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLSetDescField** 설명자 레코드의 단일 필드 값을 설정 합니다.  
  
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
 입력 설명자 핸들입니다.  
  
 *RecNumber*  
 입력 응용 프로그램에서 설정 하려는 필드가 포함 된 설명자 레코드를 나타냅니다. 설명자 레코드의 번호는 0에서, 레코드 번호 0은 책갈피 레코드입니다. 헤더 필드의 경우에는 *값* 인수가 무시 됩니다.  
  
 *FieldIdentifier*  
 입력 값을 설정할 설명자의 필드를 나타냅니다. 자세한 내용은 "Comments" 섹션의 "*FieldIdentifier* 인수"를 참조 하세요.  
  
 *ValuePtr*  
 입력 설명자 정보 또는 정수 값을 포함 하는 버퍼에 대 한 포인터입니다. 데이터 형식은 *FieldIdentifier*의 값에 따라 달라 집니다. *Valueptr* 이 정수 값 이면 *FieldIdentifier* 인수의 값에 따라 8 바이트 (sqllen), 4 바이트 (sqllen) 또는 2 바이트 (sqllen)로 간주할 수 있습니다.  
  
 *BufferLength*  
 입력 *FieldIdentifier* 가 ODBC에 정의 된 필드 *이 고 요소* 문자열이 나 이진 버퍼를 가리키는 경우이 인수는 **eptr*의 길이 여야 합니다. 문자열 데이터의 경우이 인수는 문자열의 바이트 수를 포함 해야 합니다.  
  
 *FieldIdentifier* 가 ODBC에 정의 된 필드이 고 이상 값 *eptr* 이 정수 이면 *bufferlength* 는 무시 됩니다.  
  
 *FieldIdentifier* 가 드라이버 정의 필드인 경우 응용 프로그램은 *bufferlength* 인수를 설정 하 여 필드의 특성을 드라이버 관리자에 게 표시 합니다. *Bufferlength* 에는 다음 값을 사용할 수 있습니다.  
  
-   *Valueptr* 이 문자열에 대 한 포인터인 경우 *bufferlength* 는 문자열 또는 SQL_NTS의 길이입니다.  
  
-   *Valueptr* 이 이진 버퍼에 대 한 포인터인 경우 응용 프로그램은 SQL_LEN_BINARY_ATTR (*길이*) 매크로의 결과를 *bufferlength*로 배치 합니다. 그러면 음수 값이 *Bufferlength*에 배치 됩니다.  
  
-   *Valueptr* 이 문자열 또는 이진 문자열이 아닌 값에 대 한 포인터인 경우 *bufferlength* 의 값은 SQL_IS_POINTER 이어야 합니다.  
  
-   *Valueptr* 이 고정 길이 값을 포함 하는 경우 *bufferlength* 는 SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT 또는 SQL_IS_USMALLINT 중 하나입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLSetDescField** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 SQL_HANDLE_DESC의 *HandleType* 및 *DescriptorHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **SQLSetDescField** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01 S 02|옵션 값 변경 됨|드라이버가 지정 된 값을 지원 하지 않았습니다. * \* (값* *eptr* 이 *포인터인 경우)* *또는 (값 eptr이* 정수 값 인 경우)에는 * \* 값이 구현* 작업 조건으로 인해 잘못 된 것으로 처리 되므로 드라이버는 유사한 값을 대체 합니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|07009|잘못 된 설명자 인덱스|*FieldIdentifier* 인수는 레코드 필드이 고, 인수 *는 0* 이며, *DescriptorHandle* 인수는 IPD 핸들을 참조 합니다.<br /><br /> 인수 *인수가 0* 보다 작고 *DescriptorHandle* 인수는가 나 apd를 참조 합니다.<br /><br /> 인수 *인수가 데이터* 원본이 지원할 수 있는 열 또는 매개 변수의 최대 개수 보다 크거나 apd 또는 *DescriptorHandle* 인수를 참조 합니다.<br /><br /> (DM) FieldIdentifier 인수가 SQL_DESC_COUNT 되었으며, *FieldIdentifier* * \* eptr* 인수가 0 보다 작은 경우<br /><br /> *DescriptorHandle* *인수는 0* 과 같고 암시적으로 할당 된 apd 인수를 참조 합니다. 명시적으로 할당 된 응용 프로그램 설명자는 명시적으로 할당 된 응용 프로그램 설명자가 APD 인지 아니면 실행 시간이 될 때까지이를 알 수 없기 때문에 명시적으로 할당 된 응용 프로그램 설명자에서는이 오류가 발생 하지 않습니다.|  
|08S01|통신 연결 오류|드라이버가 연결 된 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|22001|문자열 데이터, 오른쪽이 잘렸습니다.|*FieldIdentifier* 인수가 SQL_DESC_NAME 되었으며 *bufferlength* 인수가 SQL_MAX_IDENTIFIER_LEN 보다 큰 값입니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. * \* MessageText* 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류|(DM) *DescriptorHandle* 가이 함수를 호출 하지 않고 비동기적으로 실행 되는 함수를 호출 하 고이 함수가 호출 될 때 여전히 실행 되는 *StatementHandle* 와 연결 되었습니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 는 *DescriptorHandle* 가 연결 되 고 SQL_NEED_DATA 반환 된 *StatementHandle* 에 대해 호출 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.<br /><br /> (DM) *DescriptorHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. **SQLSetDescField** 함수가 호출 될 때이 비동기 함수는 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **Sqlexecdirect**또는 **SQLMoreResults** 가 *DescriptorHandle* 와 연결 된 문 핸들 중 하나에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY016|구현 행 설명자를 수정할 수 없습니다.|*DescriptorHandle* 인수가 IRD와 연결 되어 있고 *FieldIdentifier* 인수가 SQL_DESC_ARRAY_STATUS_PTR 되지 않았거나 SQL_DESC_ROWS_PROCESSED_PTR.|  
|HY021|일관 되지 않은 설명자 정보|SQL_DESC_TYPE 및 SQL_DESC_DATETIME_INTERVAL_CODE 필드는 올바른 ODBC SQL 유형 또는 올바른 드라이버별 SQL 유형 (IPDs의 경우) 또는 유효한 ODBC C 유형 (APDs 또는 ARDs의 경우)이 아닙니다.<br /><br /> 일관성 확인 중에 확인 된 설명자 정보가 일치 하지 않습니다. **SQLSetDescRec**의 "일관성 확인"을 참조 하십시오.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|( *DM)는 \* 문자열* 입니다. *bufferlength* 는 0 보다 작지만 SQL_NTS와 같지 않습니다.<br /><br /> (DM) 드라이버가 ODBC*2.x 드라이버이* 고, 설명자가 되었고, *columnnumber* 인수를 0으로 설정 하 고, 인수 *bufferlength* 에 지정 된 값이 4와 같지 않습니다.|  
|HY091|잘못 된 설명자 필드 식별자입니다.|*FieldIdentifier* 인수에 지정 된 값이 ODBC 정의 필드가 아니고 구현에서 정의 된 값이 아닙니다.<br /><br /> *FieldIdentifier* 인수가 *DescriptorHandle* 인수에 적합 하지 않습니다.<br /><br /> *FieldIdentifier* 인수는 읽기 전용 ODBC 정의 필드입니다.|  
|HY092|특성/옵션 식별자가 잘못 되었습니다.|*FieldIdentifier* *인수에 대 한 값이 잘못 \* * 되었습니다.<br /><br /> *FieldIdentifier* 인수가 SQL_DESC_UNNAMED 되었으며,이 인수 *를 SQL_NAMED 했습니다.*|  
|HY105|매개 변수 형식이 잘못 되었습니다.|(DM) SQL_DESC_PARAMETER_TYPE 필드에 지정 된 값이 잘못 되었습니다. 자세한 내용은 **SQLBindParameter**의 "*inputoutputtype* 인수" 섹션을 참조 하세요.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [ODBC 3.8의 새로운 기능](../../../odbc/reference/what-s-new-in-odbc-3-8.md)을 참조 하십시오.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *DescriptorHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 응용 프로그램은 **SQLSetDescField** 를 호출 하 여 설명자 필드를 한 번에 하나씩 설정할 수 있습니다. **SQLSetDescField** 에 대 한 한 번의 호출은 단일 설명자의 단일 필드를 설정 합니다. 필드를 설정할 수 있는 경우이 함수를 호출 하 여 설명자 형식의 모든 필드를 설정할 수 있습니다. 이 단원의 뒷부분에 나오는 표를 참조 하십시오.  
  
> [!NOTE]  
>  **SQLSetDescField** 에 대 한 호출이 실패 하는 경우에는 지 *수* 인수로 식별 되는 설명자 레코드의 내용이 정의 되지 않습니다.  
  
 함수를 한 번 호출 하 여 여러 설명자 필드를 설정 하기 위해 다른 함수를 호출할 수 있습니다. **SQLSetDescRec** 함수는 열 또는 매개 변수에 바인딩된 데이터 형식 및 버퍼에 영향을 주는 다양 한 필드 (SQL_DESC_TYPE, SQL_DESC_DATETIME_INTERVAL_CODE, SQL_DESC_OCTET_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE, SQL_DESC_DATA_PTR, SQL_DESC_OCTET_LENGTH_PTR 필드)를 설정 합니다. **SQLBindCol** 또는 **SQLBindParameter** 를 사용 하 여 열 또는 매개 변수의 바인딩을 완벽 하 게 지정할 수 있습니다. 이러한 함수는 하나의 함수 호출을 사용 하 여 특정 설명자 필드 그룹을 설정 합니다.  
  
 **SQLSetDescField** 를 호출 하 여 바인딩 포인터 (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR 또는 SQL_DESC_OCTET_LENGTH_PTR)에 오프셋을 추가 하 여 바인딩 버퍼를 변경할 수 있습니다. **SQLBindCol** 또는 **SQLBindParameter**를 호출 하지 않고 바인딩 버퍼를 변경 하 여 응용 프로그램에서 SQL_DESC_DATA_TYPE 같은 다른 필드를 변경 하지 않고 SQL_DESC_DATA_PTR를 변경할 수 있도록 합니다.  
  
 응용 프로그램에서 **SQLSetDescField** 를 호출 하 여 SQL_DESC_COUNT 또는 지연 된 필드 SQL_DESC_DATA_PTR, SQL_DESC_OCTET_LENGTH_PTR 또는 SQL_DESC_INDICATOR_PTR 이외의 필드를 설정 하는 경우 레코드가 바인딩되지 않게 됩니다.  
  
 설명자 헤더 필드는 적절 한 *FieldIdentifier*로 **SQLSetDescField** 를 호출 하 여 설정 합니다. 많은 헤더 필드는 문 특성 이기도 하므로 **SQLSetStmtAttr**에 대 한 호출로 설정할 수도 있습니다. 이렇게 하면 응용 프로그램에서 설명자 핸들을 먼저 가져오지 않고 설명자 필드를 설정할 수 있습니다. **SQLSetDescField** 을 호출 하 여 헤더 필드를 설정 *하면 해당 인수는 무시* 됩니다.  
  
 *번호* 0은 책갈피 필드를 설정 하는 데 사용 됩니다.  
  
> [!NOTE]  
>  **SQLSetDescField** 를 호출 하 여 책갈피 필드를 설정 하기 전에 statement 특성 SQL_ATTR_USE_BOOKMARKS 항상 설정 해야 합니다. 반드시 필요한 것은 아니지만, 적극 권장 됩니다.  
  
## <a name="sequence-of-setting-descriptor-fields"></a>설정 설명자 필드의 시퀀스  
 **SQLSetDescField**를 호출 하 여 설명자 필드를 설정 하는 경우 응용 프로그램은 특정 시퀀스를 따라야 합니다.  
  
1.  응용 프로그램은 먼저 SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE 또는 SQL_DESC_DATETIME_INTERVAL_CODE 필드를 설정 해야 합니다.  
  
2.  이러한 필드 중 하나를 설정한 후에는 응용 프로그램에서 데이터 형식의 특성을 설정할 수 있으며 드라이버는 데이터 형식 특성 필드를 데이터 형식에 대 한 적절 한 기본값으로 설정 합니다. 형식 특성 필드의 자동 기본값을 사용 하면 응용 프로그램에서 데이터 형식을 지정한 후에 항상 설명자를 사용할 준비가 됩니다. 응용 프로그램에서 데이터 형식 특성을 명시적으로 설정 하는 경우 기본 특성을 재정의 합니다.  
  
3.  1 단계에 나열 된 필드 중 하나를 설정 하 고 데이터 형식 특성을 설정한 후에는 응용 프로그램에서 SQL_DESC_DATA_PTR 설정할 수 있습니다. 그러면 설명자 필드에 대 한 일관성 확인 메시지가 표시 됩니다. SQL_DESC_DATA_PTR 필드를 설정한 후 응용 프로그램에서 데이터 형식이 나 특성을 변경 하는 경우 드라이버는 SQL_DESC_DATA_PTR를 null 포인터로 설정 하 고 레코드의 바인딩을 해제 합니다. 그러면 설명자 레코드를 사용할 수 있기 전에 응용 프로그램이 순서 대로 적절 한 단계를 완료 합니다.  
  
## <a name="initialization-of-descriptor-fields"></a>설명자 필드 초기화  
 설명자가 할당 되 면 설명자의 필드를 기본값으로 초기화 하거나, 기본값 없이 초기화 하거나, 설명자 형식에 대해 정의 되지 않은 상태일 수 있습니다. 다음 표에서는 각 설명자 형식에 대 한 각 필드를 초기화 하 고, 필드가 기본값을 사용 하 여 초기화 되었음을 나타내는 "D"와, 필드가 기본값 없이 초기화 됨을 나타내는 "ND"를 나타냅니다. 숫자가 표시 되는 경우 필드의 기본값은 해당 숫자입니다. 또한이 테이블은 필드가 읽기/쓰기 (R/W) 또는 읽기 전용 (R) 인지를 나타냅니다.  
  
 문 핸들이 나 설명자가 할당 되지 않은 경우에만 IRD의 필드에는 문이 준비 되거나 실행 되 고 IRD가 채워지는 후에만 기본값이 있습니다. IRD이 채워질 때까지 IRD의 필드에 액세스 하려고 하면 오류가 반환 됩니다.  
  
 일부 설명자 필드는 하나 이상의 설명자 형식 (ARDs 및 IRDs 및 APDs 및 IPDs)에 대해 정의 됩니다. 설명자 형식에 대해 필드가 정의 되어 있지 않으면 해당 설명자를 사용 하는 함수에 필요 하지 않습니다.  
  
 **SQLGetDescField** 에서 액세스할 수 있는 필드는 **SQLSetDescField**로 반드시 설정할 수 없습니다. **SQLSetDescField** 에서 설정할 수 있는 필드는 다음 표에 나와 있습니다.  
  
 헤더 필드의 초기화는 다음 표에 설명 되어 있습니다.  
  
|헤더 필드 이름|형식|R/W|기본값|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_ALLOC_TYPE|SQLSMALLINT|작업: R APD: R IRD: R IPD: R|작업: 암시적 또는 SQL_DESC_ALLOC_USER에 대 한 SQL_DESC_ALLOC_AUTO입니다.<br /><br /> APD: explicit 또는 SQL_DESC_ALLOC_USER에 대 한 SQL_DESC_ALLOC_AUTO<br /><br /> IRD: SQL_DESC_ALLOC_AUTO<br /><br /> IPD: SQL_DESC_ALLOC_AUTO|  
|SQL_DESC_ARRAY_SIZE|SQLULEN|사용: R/W APD: R/W IRD: 사용 되지 않는 IPD: 사용 안 함|사용: [1] APD: [1] IRD: 사용 되지 않는 IPD: 사용 안 함|  
|SQL_DESC_ARRAY_STATUS_PTR|SQLUSMALLINT*|작업: R/W APD: R/W IRD: R/W IPD: R/W|작업: Null ptr APD: null ptr IRD: null ptr IPD: Null ptr|  
|SQL_DESC_BIND_OFFSET_PTR|SQLLEN|사용: R/W APD: R/W IRD: 사용 되지 않는 IPD: 사용 안 함|사용: Null ptr APD: Null ptr IRD: 사용 되지 않는 IPD: 사용 되지 않음|  
|SQL_DESC_BIND_TYPE|SQLINTEGER|사용: R/W APD: R/W IRD: 사용 되지 않는 IPD: 사용 안 함|카드: SQL_BIND_BY_COLUMN<br /><br /> APD: SQL_BIND_BY_COLUMN<br /><br /> IRD: 사용 안 함<br /><br /> IPD: 사용 안 함|  
|SQL_DESC_COUNT|SQLSMALLINT|작업: R/W APD: R/W IRD: R IPD: R/W|작업: 0 APD: 0 IRD: D IPD: 0|  
|SQL_DESC_ROWS_PROCESSED_PTR|SQLULEN *|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: R/W IPD: R/W|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: Null ptr IPD: Null ptr|  
  
 [1] 이러한 필드는 IPD가 드라이버에 의해 자동으로 채워지는 경우에만 정의 됩니다. 그렇지 않으면 정의 되지 않습니다. 응용 프로그램에서 이러한 필드를 설정 하려고 하면 SQLSTATE HY091 (잘못 된 설명자 필드 식별자)가 반환 됩니다.  
  
 레코드 필드의 초기화는 다음 표에 나와 있는 것과 같습니다.  
  
|레코드 필드 이름|형식|R/W|기본값|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: 사용 안 함|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: 사용 되지 않음|  
|SQL_DESC_BASE_COLUMN_NAME|SQLCHAR|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: 사용 안 함|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: 사용 되지 않음|  
|SQL_DESC_BASE_TABLE_NAME|SQLCHAR|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: 사용 안 함|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: 사용 되지 않음|  
|SQL_DESC_CASE_SENSITIVE|SQLINTEGER|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: R|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: D [1]|  
|SQL_DESC_CATALOG_NAME|SQLCHAR|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: 사용 안 함|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: 사용 되지 않음|  
|SQL_DESC_CONCISE_TYPE|SQLSMALLINT|작업: R/W APD: R/W IRD: R IPD: R/W|작업: SQL_C_ 기본 APD: SQL_C_ 기본 IRD: D IPD: ND|  
|SQL_DESC_DATA_PTR|대 한 SQLPOINTER|사용: R/W APD: R/W IRD: 사용 되지 않는 IPD: 사용 안 함|사용: Null ptr APD: Null ptr IRD: 사용 되지 않는 IPD: 사용 되지 않는 [2]|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQLSMALLINT|작업: R/W APD: R/W IRD: R IPD: R/W|작업: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|SQLINTEGER|작업: R/W APD: R/W IRD: R IPD: R/W|작업: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_DISPLAY_SIZE|SQLLEN|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: 사용 안 함|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: 사용 되지 않음|  
|SQL_DESC_FIXED_PREC_SCALE|SQLSMALLINT|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: R|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: D [1]|  
|SQL_DESC_INDICATOR_PTR|SQLLEN|사용: R/W APD: R/W IRD: 사용 되지 않는 IPD: 사용 안 함|사용: Null ptr APD: Null ptr IRD: 사용 되지 않는 IPD: 사용 되지 않음|  
|SQL_DESC_LABEL|SQLCHAR|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: 사용 안 함|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: 사용 되지 않음|  
|SQL_DESC_LENGTH|SQLULEN|작업: R/W APD: R/W IRD: R IPD: R/W|작업: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_LITERAL_PREFIX|SQLCHAR|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: 사용 안 함|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: 사용 되지 않음|  
|SQL_DESC_LITERAL_SUFFIX|SQLCHAR|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: 사용 안 함|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: 사용 되지 않음|  
|SQL_DESC_LOCAL_TYPE_NAME|SQLCHAR|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: R|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: D [1]|  
|SQL_DESC_NAME|SQLCHAR|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: R/W|작업: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_NULLABLE|SQLSMALLINT|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: R|작업: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_NUM_PREC_RADIX|SQLINTEGER|작업: R/W APD: R/W IRD: R IPD: R/W|작업: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_OCTET_LENGTH|SQLLEN|작업: R/W APD: R/W IRD: R IPD: R/W|작업: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_OCTET_LENGTH_PTR|SQLLEN|사용: R/W APD: R/W IRD: 사용 되지 않는 IPD: 사용 안 함|사용: Null ptr APD: Null ptr IRD: 사용 되지 않는 IPD: 사용 되지 않음|  
|SQL_DESC_PARAMETER_TYPE|SQLSMALLINT|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: 사용 되지 않는 IPD: R/W|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: 사용 되지 않는 IPD: D = SQL_PARAM_INPUT|  
|SQL_DESC_PRECISION|SQLSMALLINT|작업: R/W APD: R/W IRD: R IPD: R/W|작업: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_ROWVER|SQLSMALLINT|사용: 사용 안 함<br /><br /> APD: 사용 안 함<br /><br /> IRD: R<br /><br /> IPD: R|사용: 사용 안 함<br /><br /> APD: 사용 안 함<br /><br /> IRD: ND<br /><br /> IPD: ND|  
|SQL_DESC_SCALE|SQLSMALLINT|작업: R/W APD: R/W IRD: R IPD: R/W|작업: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_SCHEMA_NAME|SQLCHAR|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: 사용 안 함|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: 사용 되지 않음|  
|SQL_DESC_SEARCHABLE|SQLSMALLINT|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: 사용 안 함|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: 사용 되지 않음|  
|SQL_DESC_TABLE_NAME|SQLCHAR|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: 사용 안 함|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: 사용 되지 않음|  
|SQL_DESC_TYPE|SQLSMALLINT|작업: R/W APD: R/W IRD: R IPD: R/W|작업: SQL_C_DEFAULT APD: SQL_C_DEFAULT IRD: D IPD: ND|  
|SQL_DESC_TYPE_NAME|SQLCHAR|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: R|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: D [1]|  
|SQL_DESC_UNNAMED|SQLSMALLINT|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: R/W|작업: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_UNSIGNED|SQLSMALLINT|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: R|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: D [1]|  
|SQL_DESC_UPDATABLE|SQLSMALLINT|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: R IPD: 사용 안 함|사용: 사용 되지 않는 APD: 사용 되지 않는 IRD: D IPD: 사용 되지 않음|  
  
 [1] 이러한 필드는 IPD가 드라이버에 의해 자동으로 채워지는 경우에만 정의 됩니다. 그렇지 않으면 정의 되지 않습니다. 응용 프로그램에서 이러한 필드를 설정 하려고 하면 SQLSTATE HY091 (잘못 된 설명자 필드 식별자)가 반환 됩니다.  
  
 [2] 일관성 확인을 강제 적용 하도록 IPD의 SQL_DESC_DATA_PTR 필드를 설정할 수 있습니다. **SQLGetDescField** 또는 **SQLGetDescRec**에 대 한 후속 호출에서 드라이버는 SQL_DESC_DATA_PTR 설정 된 값을 반환 하는 데 필요 하지 않습니다.  
  
## <a name="fieldidentifier-argument"></a>FieldIdentifier 인수  
 *FieldIdentifier* 인수는 설정할 설명자 필드를 나타냅니다. 설명자에는 다음 섹션에 설명 된 헤더 필드 "헤더 필드"와 0 개 이상의 *설명자 레코드가* 포함 된 *설명자 헤더가* 포함 되어 있습니다 .이는 "헤더 필드" 섹션의 섹션에 설명 된 레코드 필드로 구성 됩니다.  
  
## <a name="header-fields"></a>헤더 필드  
 각 설명자에는 다음 필드로 구성 된 헤더가 있습니다.  
  
 **SQL_DESC_ALLOC_TYPE [모두]**  
 이 읽기 전용 SQLSMALLINT 헤더 필드는 설명자가 자동으로 드라이버에 의해 할당 되었는지 아니면 응용 프로그램에 의해 명시적으로 할당 되었는지를 지정 합니다. 응용 프로그램은이 필드를 가져올 수 있지만 수정할 수는 없습니다. 드라이버에서 설명자가 자동으로 할당 된 경우이 필드는 드라이버에 의해 SQL_DESC_ALLOC_AUTO 설정 됩니다. 응용 프로그램에서 설명자를 명시적으로 할당 한 경우 드라이버에서 SQL_DESC_ALLOC_USER 하도록 설정 됩니다.  
  
 **SQL_DESC_ARRAY_SIZE [응용 프로그램 설명자]**  
 ARDs에서이 SQLULEN 헤더 필드는 행 집합의 행 수를 지정 합니다. **Sqlfetch** 또는 **sqlfetchscroll** 에 대 한 호출에 의해 반환 되거나 **SQLBulkOperations** 또는 **SQLSetPos**를 호출 하 여 작동 하는 행의 수입니다.  
  
 APDs에서이 SQLULEN 헤더 필드는 각 매개 변수의 값 수를 지정 합니다.  
  
 이 필드의 기본값은 1입니다. SQL_DESC_ARRAY_SIZE가 1 보다 크면 APD의 SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR 배열에 대 한 포인터입니다. 각 배열의 카디널리티는이 필드의 값과 같습니다.  
  
 이 필드는 SQL_ATTR_ROW_ARRAY_SIZE 특성을 사용 하 여 **SQLSetStmtAttr** 를 호출 하 여 설정할 수도 있습니다. APD의이 필드는 SQL_ATTR_PARAMSET_SIZE 특성을 사용 하 여 **SQLSetStmtAttr** 를 호출 하 여 설정할 수도 있습니다.  
  
 **SQL_DESC_ARRAY_STATUS_PTR [모두]**  
 각 설명자 형식에 대해이 SQLUSMALLINT * 헤더 필드는 SQLUSMALLINT 값의 배열을 가리킵니다. 이러한 배열은 IRD (행 상태 배열), IPD (parameter status array), 행 작업 배열 () 및 APD (parameter operation array)와 같이 이름이 지정 됩니다.  
  
 IRD에서이 헤더 필드는 **SQLBulkOperations**, **sqlfetch**, **sqlfetchscroll**또는 **SQLSetPos**를 호출한 후 상태 값을 포함 하는 행 상태 배열을 가리킵니다. 배열에 행 집합의 행 수 만큼의 요소가 있습니다. 응용 프로그램은 SQLUSMALLINTs의 배열을 할당 하 고 배열을 가리키도록이 필드를 설정 해야 합니다. 기본적으로이 필드는 null 포인터로 설정 됩니다. SQL_DESC_ARRAY_STATUS_PTR 필드가 null 포인터로 설정 되지 않는 한 드라이버는 배열을 채웁니다 .이 경우 상태 값이 생성 되지 않고 배열이 채워지지 않습니다.  
  
> [!CAUTION]  
>  응용 프로그램에서 IRD의 SQL_DESC_ARRAY_STATUS_PTR 필드가 가리키는 행 상태 배열의 요소를 설정 하는 경우 드라이버 동작은 정의 되지 않습니다.  
  
 배열은 처음에 **SQLBulkOperations**, **sqlfetch**, **sqlfetchscroll**또는 **SQLSetPos**를 호출 하 여 채워집니다. 호출이 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 반환 하지 않은 경우이 필드가 가리키는 배열의 내용이 정의 되지 않습니다. 배열의 요소에는 다음 값이 포함 될 수 있습니다.  
  
-   SQL_ROW_SUCCESS: 행이 인출 되었으며 마지막으로 인출 된 이후 변경 되지 않았습니다.  
  
-   SQL_ROW_SUCCESS_WITH_INFO: 행이 인출 되었으며 마지막으로 인출 된 이후 변경 되지 않았습니다. 그러나 행에 대 한 경고가 반환 되었습니다.  
  
-   SQL_ROW_ERROR: 행을 페치하는 동안 오류가 발생 했습니다.  
  
-   SQL_ROW_UPDATED: 행이 인출 되 고 마지막으로 인출 된 후 업데이트 되었습니다. 다시 인출 된 행의 상태는 SQL_ROW_SUCCESS입니다.  
  
-   SQL_ROW_DELETED: 행이 마지막으로 인출 된 후 삭제 되었습니다.  
  
-   SQL_ROW_ADDED: **SQLBulkOperations**에 의해 행이 삽입 되었습니다. 다시 인출 된 행의 상태는 SQL_ROW_SUCCESS입니다.  
  
-   SQL_ROW_NOROW: 행 집합은 결과 집합의 끝을 겹쳐져 행 상태 배열의이 요소로 속하는지를 행이 반환 되지 않습니다.  
  
 IRD의이 필드는 SQL_ATTR_ROW_STATUS_PTR 특성을 사용 하 여 **SQLSetStmtAttr** 를 호출 하 여 설정할 수도 있습니다.  
  
 IRD의 SQL_DESC_ARRAY_STATUS_PTR 필드는 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO 반환 된 후에만 유효 합니다. 반환 코드가 이러한 항목 중 하나가 아닌 경우 SQL_DESC_ROWS_PROCESSED_PTR가 가리키는 위치가 정의 되지 않습니다.  
  
 IPD에서이 헤더 필드는 **Sqlexecute** 또는 **sqlexecdirect**를 호출한 후 각 매개 변수 값 집합에 대 한 상태 정보를 포함 하는 매개 변수 상태 배열을 가리킵니다. **Sqlexecute** 또는 **sqlexecdirect** 호출에서 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 반환 하지 않은 경우이 필드가 가리키는 배열의 내용이 정의 되지 않습니다. 응용 프로그램은 SQLUSMALLINTs의 배열을 할당 하 고 배열을 가리키도록이 필드를 설정 해야 합니다. SQL_DESC_ARRAY_STATUS_PTR 필드가 null 포인터로 설정 되지 않는 한 드라이버는 배열을 채웁니다 .이 경우 상태 값이 생성 되지 않고 배열이 채워지지 않습니다. 배열의 요소에는 다음 값이 포함 될 수 있습니다.  
  
-   SQL_PARAM_SUCCESS:이 매개 변수 집합에 대해 SQL 문이 성공적으로 실행 되었습니다.  
  
-   SQL_PARAM_SUCCESS_WITH_INFO:이 매개 변수 집합에 대해 SQL 문이 성공적으로 실행 되었습니다. 그러나 경고 정보는 진단 데이터 구조에서 사용할 수 있습니다.  
  
-   SQL_PARAM_ERROR:이 매개 변수 집합을 처리 하는 동안 오류가 발생 했습니다. 추가 오류 정보는 진단 데이터 구조에서 사용할 수 있습니다.  
  
-   SQL_PARAM_UNUSED:이 매개 변수 집합은 일부 이전 매개 변수 설정에서 추가 처리를 중단 한 오류가 발생 했거나 APD의 SQL_DESC_ARRAY_STATUS_PTR 필드로 지정 된 배열에 있는 해당 매개 변수 집합에 대해 SQL_PARAM_IGNORE 설정 되었기 때문에 사용 되지 않았습니다.  
  
-   SQL_PARAM_DIAG_UNAVAILABLE: 진단 정보를 사용할 수 없습니다. 이에 대 한 예는 드라이버에서 매개 변수 배열을 모놀리식 unit으로 처리 하므로이 수준의 오류 정보를 생성 하지 않는 경우입니다.  
  
 IPD의이 필드는 SQL_ATTR_PARAM_STATUS_PTR 특성을 사용 하 여 **SQLSetStmtAttr** 를 호출 하 여 설정할 수도 있습니다.  
  
 이 헤더 필드는 응용 프로그램에서 설정할 수 있는 값의 행 작업 배열을 가리키며 **SQLSetPos** 작업에서이 행을 무시할지 여부를 나타냅니다. 배열의 요소에는 다음 값이 포함 될 수 있습니다.  
  
-   SQL_ROW_PROCEED: **SQLSetPos**를 사용 하 여 대량 작업에 행이 포함 됩니다. 이 설정은 행에서 작업이 발생 하는 것을 보장 하지 않습니다. 행의 상태가 IRD row status 배열에 SQL_ROW_ERROR 경우 드라이버는 행에서 작업을 수행 하지 못할 수 있습니다.  
  
-   SQL_ROW_IGNORE: **SQLSetPos**를 사용 하 여 대량 작업에서 행이 제외 됩니다.  
  
 배열의 요소를 설정 하지 않으면 모든 행이 대량 작업에 포함 됩니다. SQL_DESC_ARRAY_STATUS_PTR 필드의 값이 null 포인터인 경우 모든 행이 대량 작업에 포함 됩니다. 해석은 유효한 배열을 가리키는 포인터와 배열의 모든 요소가 SQL_ROW_PROCEED 된 것과 동일 합니다. 배열의 요소가 SQL_ROW_IGNORE로 설정 된 경우 무시 된 행의 행 상태 배열 값은 변경 되지 않습니다.  
  
 이 필드는 SQL_ATTR_ROW_OPERATION_PTR 특성을 사용 하 여 **SQLSetStmtAttr** 를 호출 하 여 설정할 수도 있습니다.  
  
 APD에서이 헤더 필드는 **Sqlexecute** 또는 **sqlexecdirect** 를 호출할 때이 매개 변수 집합을 무시할지 여부를 나타내기 위해 응용 프로그램에서 설정할 수 있는 값의 매개 변수 작업 배열을 가리킵니다. 배열의 요소에는 다음 값이 포함 될 수 있습니다.  
  
-   SQL_PARAM_PROCEED: **Sqlexecute** 또는 **sqlexecdirect** 호출에 매개 변수 집합이 포함 됩니다.  
  
-   SQL_PARAM_IGNORE: 매개 변수 집합은 **Sqlexecute** 또는 **sqlexecdirect** 호출에서 제외 됩니다.  
  
 배열의 요소를 설정 하지 않은 경우에는 배열의 모든 매개 변수 집합이 **Sqlexecute** 또는 **sqlexecdirect** 호출에 사용 됩니다. APD의 SQL_DESC_ARRAY_STATUS_PTR 필드 값이 null 포인터인 경우 모든 매개 변수 집합이 사용 됩니다. 해석은 유효한 배열을 가리키는 포인터와 배열의 모든 요소가 SQL_PARAM_PROCEED 된 것과 동일 합니다.  
  
 APD의이 필드는 SQL_ATTR_PARAM_OPERATION_PTR 특성을 사용 하 여 **SQLSetStmtAttr** 를 호출 하 여 설정할 수도 있습니다.  
  
 **SQL_DESC_BIND_OFFSET_PTR [응용 프로그램 설명자]**  
 이 SQLLEN * 헤더 필드는 바인딩 오프셋을 가리킵니다. 기본적으로 null 포인터로 설정 됩니다. 이 필드가 null 포인터가 아닌 경우 드라이버는 포인터를 역참조 하 고 인출 시 설명자 레코드에 null이 아닌 값 (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR)이 있는 각 지연 필드에 역참조 된 값을 추가 하 고 바인딩할 때 새 포인터 값을 사용 합니다.  
  
 바인딩 오프셋은 항상 SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR 필드의 값에 직접 추가 됩니다. 오프셋이 다른 값으로 변경 되는 경우에도 새 값이 각 설명자 필드의 값에 직접 추가 됩니다. 새 오프셋은 필드 값에 앞의 오프셋을 더한 값에 추가 되지 않습니다.  
  
 이 필드는 *지연 된 필드*입니다 .이 필드는 설정 시 사용 되지 않지만 나중에 데이터 버퍼의 주소를 결정 해야 할 때 드라이버에서 사용 됩니다.  
  
 이 필드는 SQL_ATTR_ROW_BIND_OFFSET_PTR 특성을 사용 하 여 **SQLSetStmtAttr** 를 호출 하 여 설정할 수도 있습니다. 이 필드는 SQL_ATTR_PARAM_BIND_OFFSET_PTR 특성을 사용 하 여 **SQLSetStmtAttr** 를 호출 하 여 설정할 수도 있습니다.  
  
 자세한 내용은 [Sqlfetchscroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) 및 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)의 행 단위 바인딩에 대 한 설명을 참조 하세요.  
  
 **SQL_DESC_BIND_TYPE [응용 프로그램 설명자]**  
 이 SQLUINTEGER 헤더 필드는 열 또는 매개 변수를 바인딩하는 데 사용할 바인딩 방향을 설정 합니다.  
  
 ARDs에서이 필드는 연결 된 문 핸들에 대해 **Sqlfetchscroll** 또는 **sqlfetch** 를 호출할 때 바인딩 방향을 지정 합니다.  
  
 열에 대 한 열 단위 바인딩을 선택 하려면이 필드가 SQL_BIND_BY_COLUMN (기본값)로 설정 됩니다.  
  
 이 필드는 SQL_ATTR_ROW_BIND_TYPE *특성*을 사용 하 여 **SQLSetStmtAttr** 를 호출 하 여 설정할 수도 있습니다.  
  
 APDs에서이 필드는 동적 매개 변수에 사용할 바인딩 방향을 지정 합니다.  
  
 매개 변수에 대 한 열 단위 바인딩을 선택 하려면이 필드가 SQL_BIND_BY_COLUMN (기본값)로 설정 됩니다.  
  
 APD의이 필드는 SQL_ATTR_PARAM_BIND_TYPE *특성*을 사용 하 여 **SQLSetStmtAttr** 를 호출 하 여 설정할 수도 있습니다.  
  
 **SQL_DESC_COUNT [모두]**  
 이 SQLSMALLINT 헤더 필드는 데이터를 포함 하는 가장 번호가 매겨진 레코드의 인덱스 (1부터 사용)를 지정 합니다. 드라이버에서 설명자에 대 한 데이터 구조를 설정 하는 경우에는 SQL_DESC_COUNT 필드를 설정 하 여 중요 한 레코드 수를 표시 해야 합니다. 응용 프로그램에서이 데이터 구조의 인스턴스를 할당 하는 경우 공간을 예약 하는 데 사용할 레코드 수를 지정할 필요가 없습니다. 응용 프로그램이 레코드의 내용을 지정할 때 드라이버는 설명자 핸들이 적절 한 크기의 데이터 구조를 참조 하는지 확인 하는 데 필요한 모든 작업을 수행 합니다.  
  
 SQL_DESC_COUNT은 바인딩된 모든 데이터 열의 개수 (필드가 있는 경우) 또는 바인딩된 모든 매개 변수 (필드가 APD 인 경우)가 아니라 가장 높은 번호의 레코드 수입니다. 가장 번호가 매겨진 열 또는 매개 변수가 바인딩 해제 된 경우 SQL_DESC_COUNT는 다음으로 가장 높은 번호의 열 또는 매개 변수 수로 변경 됩니다. **SQLBindCol** 을 호출 하 여 가장 높은 번호의 열 수보다 작은 수의 열 또는 매개 변수가 바인딩 해제 된 경우 ( *Targetvalueptr* 인수를 Null 포인터로 설정 하거나 *parametervalueptr* 인수가 null 포인터로 설정 된 **SQLBindParameter** )에는 SQL_DESC_COUNT 변경 되지 않습니다. 데이터를 포함 하는 번호가 가장 높은 레코드 보다 큰 숫자를 사용 하 여 열 또는 매개 변수를 추가로 바인딩하면 드라이버가 SQL_DESC_COUNT 필드의 값을 자동으로 늘립니다. SQL_UNBIND 옵션을 사용 하 여 **SQLFreeStmt** 를 호출 하 여 모든 열을 바인딩 해제 한 경우에는 IRD의 SQL_DESC_COUNT 필드가 0으로 설정 됩니다. SQL_RESET_PARAMS 옵션을 사용 하 여 **SQLFreeStmt** 를 호출 하면 APD 및 IPD의 SQL_DESC_COUNT 필드가 0으로 설정 됩니다.  
  
 SQL_DESC_COUNT의 값은 응용 프로그램에서 **SQLSetDescField**를 호출 하 여 명시적으로 설정할 수 있습니다. SQL_DESC_COUNT의 값을 명시적으로 줄이면 SQL_DESC_COUNT에서 새 값 보다 큰 숫자가 있는 모든 레코드가 효과적으로 제거 됩니다. SQL_DESC_COUNT 값이 명시적으로 0으로 설정 되 고 필드가 있는 경우 바인딩된 책갈피 열을 제외한 모든 데이터 버퍼가 해제 됩니다.  
  
 이 필드의 레코드 수에는 바인딩된 책갈피 열이 포함 되지 않습니다. 책갈피 열을 바인딩 해제 하는 유일한 방법은 SQL_DESC_DATA_PTR 필드를 null 포인터로 설정 하는 것입니다.  
  
 **SQL_DESC_ROWS_PROCESSED_PTR [구현 설명자]**  
 IRD에서이 SQLULEN \* 헤더 필드는 **sqlfetch** 또는 **sqlulen**을 호출한 후 인출 된 행 수 또는 오류 행을 포함 하 여 **SQLBulkOperations** 또는 **SQLSetPos**를 호출 하 여 수행 된 대량 작업에서 영향을 받는 행 수를 포함 하는 버퍼를 가리킵니다.  
  
 IPD에서이 SQLUINTEGER * 헤더 필드는 오류 집합을 포함 하 여 처리 된 매개 변수 집합의 수를 포함 하는 버퍼를 가리킵니다. Null 포인터인 경우에는 숫자가 반환 되지 않습니다.  
  
 SQL_DESC_ROWS_PROCESSED_PTR는 **Sqlfetch** 또는 **SQLFETCHSCROLL** (IRD 필드의 경우) 또는 **sqlfetch**, **SQLEXECDIRECT**또는 **sqlparamdata** (IPD 필드의 경우)를 호출한 후 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO 반환 된 후에만 유효 합니다. 이 필드가 가리키는 버퍼를 채우는 호출이 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 반환 하지 않는 경우에는 SQL_NO_DATA을 반환 하지 않으면 버퍼의 내용이 정의 되지 않습니다 .이 경우 버퍼의 값이 0으로 설정 됩니다.  
  
 이 필드는 SQL_ATTR_ROWS_FETCHED_PTR 특성을 사용 하 여 **SQLSetStmtAttr** 를 호출 하 여 설정할 수도 있습니다. APD의이 필드는 SQL_ATTR_PARAMS_PROCESSED_PTR 특성을 사용 하 여 **SQLSetStmtAttr** 를 호출 하 여 설정할 수도 있습니다.  
  
 이 필드가 가리키는 버퍼는 응용 프로그램에 의해 할당 됩니다. 드라이버에 의해 설정 되는 지연 된 출력 버퍼입니다. 기본적으로 null 포인터로 설정 됩니다.  
  
## <a name="record-fields"></a>레코드 필드  
 각 설명자에는 설명자 유형에 따라 열 데이터 또는 동적 매개 변수 중 하나를 정의 하는 필드로 구성 된 하나 이상의 레코드가 포함 되어 있습니다. 각 레코드는 단일 열 또는 매개 변수의 전체 정의입니다.  
  
 **SQL_DESC_AUTO_UNIQUE_VALUE [IRDs]**  
 이 읽기 전용 SQLINTEGER 레코드 필드에는 열이 자동 증분 열인 경우 SQL_TRUE 포함 되 고 열이 자동 증분 열이 아닌 경우에는 SQL_FALSE. 이 필드는 읽기 전용 이지만 기본 자동 증분 열은 반드시 읽기 전용이 아닙니다.  
  
 **SQL_DESC_BASE_COLUMN_NAME [IRDs]**  
 이 읽기 전용 SQLCHAR * 레코드 필드에는 결과 집합 열의 기본 열 이름이 포함 되어 있습니다. 식 열의 경우와 같이 기본 열 이름이 없는 경우이 변수에는 빈 문자열이 포함 됩니다.  
  
 **SQL_DESC_BASE_TABLE_NAME [IRDs]**  
 이 읽기 전용 SQLCHAR * 레코드 필드에는 결과 집합 열에 대 한 기본 테이블 이름이 포함 됩니다. 기본 테이블 이름을 정의할 수 없거나 해당 사항이 적용 되지 않는 경우이 변수에는 빈 문자열이 포함 됩니다.  
  
 **SQL_DESC_CASE_SENSITIVE [구현 설명자]**  
 이 읽기 전용 SQLINTEGER 레코드 필드에는 열 또는 매개 변수가 데이터 정렬과 비교 시 대/소문자를 구분 하 여 처리 되는 경우 SQL_TRUE 포함 되 고, 열이 데이터 정렬 및 비교 시 대/소문자를 구분 하 여 처리 되지 않거나 문자가 아닌 열인 경우 SQL_FALSE.  
  
 **SQL_DESC_CATALOG_NAME [IRDs]**  
 이 읽기 전용 SQLCHAR * 레코드 필드는 열을 포함 하는 기본 테이블에 대 한 카탈로그를 포함 합니다. 열이 식인 경우 또는 열이 뷰의 일부인 경우 반환 값은 드라이버에 따라 달라 집니다. 데이터 원본에서 카탈로그를 지원 하지 않거나 카탈로그를 확인할 수 없는 경우이 변수에는 빈 문자열이 포함 됩니다.  
  
 **SQL_DESC_CONCISE_TYPE [모두]**  
 이 SQLSMALLINT header 필드는 datetime 및 interval 데이터 형식을 비롯 한 모든 데이터 형식에 대 한 간결한 데이터 형식을 지정 합니다.  
  
 SQL_DESC_CONCISE_TYPE, SQL_DESC_TYPE 및 SQL_DESC_DATETIME_INTERVAL_CODE 필드의 값은 상호 종속적입니다. 필드 중 하나가 설정 될 때마다 다른 필드도 설정 해야 합니다. **SQLBindCol** 또는 **SQLBindParameter**또는 **SQLSetDescField**에 대 한 호출을 통해 SQL_DESC_CONCISE_TYPE를 설정할 수 있습니다. **SQLSetDescField** 또는 **SQLSetDescRec**를 호출 하 여 SQL_DESC_TYPE를 설정할 수 있습니다.  
  
 SQL_DESC_CONCISE_TYPE가 interval 또는 datetime 데이터 형식이 아닌 간결한 데이터 형식으로 설정 된 경우에는 SQL_DESC_TYPE 필드가 동일한 값으로 설정 되 고 SQL_DESC_DATETIME_INTERVAL_CODE 필드가 0으로 설정 됩니다.  
  
 SQL_DESC_CONCISE_TYPE를 간결한 datetime 또는 interval 데이터 형식으로 설정 하면 SQL_DESC_TYPE 필드가 해당 하는 자세한 형식 (SQL_DATETIME 또는 SQL_INTERVAL)으로 설정 되 고 SQL_DESC_DATETIME_INTERVAL_CODE 필드가 적절 한 하위 코드로 설정 됩니다.  
  
 **SQL_DESC_DATA_PTR [응용 프로그램 설명자 및 IPDs]**  
 이 SQLPOINTER 레코드 필드는 매개 변수 값 (APDs의 경우) 또는 열 값 (ARDs)을 포함 하는 변수를 가리킵니다. 이 필드는 *지연 된 필드*입니다. 설정 시에는 사용 되지 않지만 나중에 드라이버에서 데이터를 검색 하는 데 사용 됩니다.  
  
 **SQLBindCol** 에 대 한 호출의 *Targetvalueptr* 인수가 Null 포인터인 경우 또는 SQLSetDescField 또는 **SQLSetDescRec** 에 대 한 호출에서 Null 포인터로 설정 된 SQL_DESC_DATA_PTR 경우 **SQLSetDescField** 의 SQL_DESC_DATA_PTR 필드로 지정 된 열이 바인딩되지 않습니다. SQL_DESC_DATA_PTR 필드가 null 포인터로 설정 된 경우 다른 필드는 영향을 받지 않습니다.  
  
 이 필드가 가리키는 버퍼를 채우는 **Sqlfetch** 또는 **sqlfetchscroll** 에 대 한 호출이 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO을 반환 하지 않은 경우 버퍼 내용이 정의 되지 않습니다.  
  
 APD, IPD 또는의 SQL_DESC_DATA_PTR 필드가 설정 될 때마다 드라이버는 SQL_DESC_TYPE 필드의 값이 유효한 ODBC C 데이터 형식 또는 드라이버별 데이터 형식 중 하나를 포함 하 고 데이터 형식에 영향을 주는 다른 모든 필드가 일치 하는지 확인 합니다. 일관성 확인 메시지를 표시 하는 것은 IPD의 SQL_DESC_DATA_PTR 필드만 사용 한다는 것입니다. 특히, 응용 프로그램이 IPD의 SQL_DESC_DATA_PTR 필드를 설정 하 고 나중에이 필드에 **SQLGetDescField** 를 호출 하는 경우 설정 된 값을 반드시 반환 하는 것은 아닙니다. 자세한 내용은 [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)의 "일관성 검사"를 참조 하세요.  
  
 **SQL_DESC_DATETIME_INTERVAL_CODE [모두]**  
 이 SQLSMALLINT record 필드에는 SQL_DESC_TYPE 필드가 SQL_DATETIME 되거나 SQL_INTERVAL 때 특정 날짜/시간 또는 간격 데이터 형식에 대 한 하위 코드가 포함 됩니다. 이는 SQL 및 C 데이터 형식 모두에 적용 됩니다. 코드는 "TYPE" 또는 "C_TYPE" (datetime 형식의 경우)로 대체 되는 데이터 형식 이름 또는 "INTERVAL" 또는 "C_INTERVAL" (간격 형식의 경우)로 대체 되는 "코드"로 구성 됩니다.  
  
 응용 프로그램 설명자의 SQL_DESC_TYPE 및 SQL_DESC_CONCISE_TYPE이 SQL_C_DEFAULT로 설정 되 고 설명자가 문 핸들과 연결 되지 않은 경우 SQL_DESC_DATETIME_INTERVAL_CODE의 내용이 정의 되지 않습니다.  
  
 이 필드는 다음 표에 나열 된 datetime 데이터 형식에 대해 설정할 수 있습니다.  
  
|Datetime 형식|DATETIME_INTERVAL_CODE|  
|--------------------|------------------------------|  
|SQL_TYPE_DATE/SQL_C_TYPE_DATE|SQL_CODE_DATE|  
|SQL_TYPE_TIME/SQL_C_TYPE_TIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP/SQL_C_TYPE_TIMESTAMP|SQL_CODE_TIMESTAMP|  
  
 이 필드는 다음 표에 나열 된 간격 데이터 형식에 대해 설정할 수 있습니다.  
  
|간격 유형|DATETIME_INTERVAL_CODE|  
|-------------------|------------------------------|  
|SQL_INTERVAL_DAY/SQL_C_INTERVAL_DAY|SQL_CODE_DAY|  
|SQL_INTERVAL_DAY_TO_HOUR/SQL_C_INTERVAL_DAY_TO_HOUR|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE/SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_CODE_DAY_TO_MINUTE|  
|SQL_INTERVAL_DAY_TO_SECOND/SQL_C_INTERVAL_DAY_TO_SECOND|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR/SQL_C_INTERVAL_HOUR|SQL_CODE_HOUR|  
|SQL_INTERVAL_HOUR_TO_MINUTE/SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND/SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE/SQL_C_INTERVAL_MINUTE|SQL_CODE_MINUTE|  
|SQL_INTERVAL_MINUTE_TO_SECOND/SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_CODE_MINUTE_TO_SECOND|  
|SQL_INTERVAL_MONTH/SQL_C_INTERVAL_MONTH|SQL_CODE_MONTH|  
|SQL_INTERVAL_SECOND/SQL_C_INTERVAL_SECOND|SQL_CODE_SECOND|  
|SQL_INTERVAL_YEAR/SQL_C_INTERVAL_YEAR|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH/SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_CODE_YEAR_TO_MONTH|  
  
 데이터 간격 및이 필드에 대 한 자세한 내용은 [데이터 형식 식별자 및 설명자](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)를 참조 하세요.  
  
 **SQL_DESC_DATETIME_INTERVAL_PRECISION [모두]**  
 SQL_DESC_TYPE 필드가 SQL_INTERVAL 되는 경우이 SQLINTEGER 레코드 필드에는 선행 전체 자릿수가 포함 됩니다. SQL_DESC_DATETIME_INTERVAL_CODE 필드가 INTERVAL 데이터 형식으로 설정 된 경우이 필드는 기본 간격으로 선행 전체 자릿수로 설정 됩니다.  
  
 **SQL_DESC_DISPLAY_SIZE [IRDs]**  
 이 읽기 전용 SQLINTEGER 레코드 필드는 열의 데이터를 표시 하는 데 필요한 최대 문자 수를 포함 합니다.  
  
 **SQL_DESC_FIXED_PREC_SCALE [구현 설명자]**  
 이 읽기 전용 SQLSMALLINT record 필드는 열이 정확한 숫자 열 이거나 고정 전체 자릿수와 0이 아닌 소수 자릿수를 갖는 경우 SQL_TRUE로 설정 되 고 전체 자릿수 및 소수 자릿수가 고정 된 정확한 숫자 열이 아닌 경우에는 SQL_FALSE로 설정 됩니다.  
  
 **SQL_DESC_INDICATOR_PTR [응용 프로그램 설명자]**  
 ARDs에서는이 SQLLEN * 레코드 필드가 표시기 변수를 가리킵니다. 이 변수에는 열 값이 NULL 인 경우 SQL_NULL_DATA 포함 됩니다. APDs의 경우 표시기 변수가 SQL_NULL_DATA로 설정 되어 NULL 동적 인수를 지정 합니다. 그렇지 않으면 SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR의 값이 같은 포인터인 경우를 제외 하 고는 변수가 0입니다.  
  
 고의 SQL_DESC_INDICATOR_PTR 필드가 null 포인터인 경우 드라이버가 열이 NULL 인지 여부에 대 한 정보를 반환할 수 없습니다. 열이 NULL이 고 SQL_DESC_INDICATOR_PTR null 포인터인 경우 드라이버가 **Sqlfetch** 또는 **sqlfetchscroll**을 호출한 후에 버퍼를 채우려고 할 때 SQLSTATE 22002 (표시기 변수가 필요 하지만 제공 되지 않음)이 반환 됩니다. **Sqlfetch** 또는 **sqlfetchscroll** 에 대 한 호출이 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 반환 하지 않은 경우 버퍼 내용이 정의 되지 않습니다.  
  
 SQL_DESC_INDICATOR_PTR 필드는 SQL_DESC_OCTET_LENGTH_PTR가 가리키는 필드가 설정 되어 있는지 여부를 확인 합니다. 열에 대 한 데이터 값이 NULL 이면 드라이버는 표시기 변수를 SQL_NULL_DATA 설정 합니다. SQL_DESC_OCTET_LENGTH_PTR에서 가리키는 필드가 설정 되지 않습니다. 인출 중에 NULL 값이 발견 되지 않으면 SQL_DESC_INDICATOR_PTR에 의해 가리키는 버퍼가 0으로 설정 되 고 SQL_DESC_OCTET_LENGTH_PTR에 의해 가리키는 버퍼가 데이터 길이로 설정 됩니다.  
  
 APD의 SQL_DESC_INDICATOR_PTR 필드가 null 포인터인 경우 응용 프로그램은이 설명자 레코드를 사용 하 여 NULL 인수를 지정할 수 없습니다.  
  
 이 필드는 *지연 된 필드*입니다 .이 필드는 설정 시 사용 되지 않지만 나중에 드라이버에서 null 허용 여부를 나타내거나 (ARDs) null 허용 여부를 확인 하는 데 사용 됩니다 (apds의 경우).  
  
 **SQL_DESC_LABEL [IRDs]**  
 이 읽기 전용 SQLCHAR * 레코드 필드에는 열 레이블이나 제목이 포함 됩니다. 열에 레이블이 없으면이 변수에 열 이름이 포함 됩니다. 열이 명명 되지 않은 열이 고 레이블이 지정 되지 않은 경우이 변수에는 빈 문자열이 포함 됩니다.  
  
 **SQL_DESC_LENGTH [모두]**  
 이 SQLULEN 레코드 필드는 문자 문자열의 최대 길이 또는 실제 길이 (바이트)입니다. 고정 길이 데이터 형식의 최대 길이 또는 가변 길이 데이터 형식의 실제 길이입니다. 해당 값은 항상 문자열을 종료 하는 null 종료 문자를 제외 합니다. 형식이 SQL_TYPE_DATE, SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP 또는 SQL interval 데이터 형식 중 하나인 값의 경우이 필드의 길이는 datetime 또는 interval 값의 문자열 표현 문자 길이입니다.  
  
 이 필드의 값은 ODBC 2.x에 정의 된 "길이"의 값과 다를 수 있습니다 *.* 자세한 내용은 [부록 D: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md)을 참조 하세요.  
  
 **SQL_DESC_LITERAL_PREFIX [IRDs]**  
 이 읽기 전용 SQLCHAR * 레코드 필드는 드라이버에서이 데이터 형식의 리터럴에 대 한 접두사로 인식 하는 문자를 포함 합니다. 이 변수에는 리터럴 접두사가 적용 되지 않는 데이터 형식에 대 한 빈 문자열이 포함 되어 있습니다.  
  
 **SQL_DESC_LITERAL_SUFFIX [IRDs]**  
 이 읽기 전용 SQLCHAR * 레코드 필드는 드라이버에서이 데이터 형식의 리터럴에 대 한 접미사로 인식 하는 문자를 포함 합니다. 이 변수에는 리터럴 접미사가 적용 되지 않는 데이터 형식에 대 한 빈 문자열이 포함 되어 있습니다.  
  
 **SQL_DESC_LOCAL_TYPE_NAME [구현 설명자]**  
 이 읽기 전용 SQLCHAR * 레코드 필드에는 데이터 형식의 일반 이름과 다를 수 있는 데이터 형식에 대 한 지역화 된 (네이티브 언어) 이름이 포함 됩니다. 지역화 된 이름이 없으면 빈 문자열이 반환 됩니다. 이 필드는 표시 목적 으로만 사용 됩니다.  
  
 **SQL_DESC_NAME [구현 설명자]**  
 행 설명자의이 SQLCHAR * 레코드 필드는 적용 되는 경우 열 별칭을 포함 합니다. 열 별칭이 적용 되지 않으면 열 이름이 반환 됩니다. 두 경우 모두 드라이버는 SQL_DESC_NAME 필드를 설정 하는 경우 SQL_DESC_UNNAMED 필드를 SQL_NAMED으로 설정 합니다. 열 이름이 나 열 별칭이 없으면 드라이버는 SQL_DESC_NAME 필드에서 빈 문자열을 반환 하 고 SQL_DESC_UNNAMED 필드를 SQL_UNNAMED로 설정 합니다.  
  
 응용 프로그램은 IPD의 SQL_DESC_NAME 필드를 매개 변수 이름 또는 별칭으로 설정 하 여 저장 프로시저 매개 변수를 이름으로 지정할 수 있습니다. 자세한 내용은 [이름으로 매개 변수 바인딩 (명명 된 매개 변수)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)을 참조 하세요. IRD의 SQL_DESC_NAME 필드는 읽기 전용 필드입니다. 응용 프로그램에서 설정 하려고 시도 하는 경우 SQLSTATE HY091 (잘못 된 설명자 필드 식별자)가 반환 됩니다.  
  
 IPDs에서 드라이버가 명명 된 매개 변수를 지원 하지 않는 경우이 필드는 정의 되지 않습니다. 드라이버가 명명 된 매개 변수를 지원 하 고 매개 변수를 설명할 수 있는 경우이 필드에 매개 변수 이름이 반환 됩니다.  
  
 **SQL_DESC_NULLABLE [구현 설명자]**  
 이 읽기 전용 SQLSMALLINT record 필드는 열이 null 값을 가질 수 있는 경우, 열에 null 값이 없는 경우 SQL_NO_NULLS SQL_NULLABLE_UNKNOWN 또는 열이 NULL 값을 허용 하는지 여부를 알 수 없는 경우에 SQL_NULLABLE 됩니다. 이 필드는 기본 열이 아닌 결과 집합 열과 관련이 있습니다.  
  
 IPDs에서 동적 매개 변수는 항상 null을 허용 하며 응용 프로그램에서 설정할 수 없기 때문에이 필드는 항상 SQL_NULLABLE로 설정 됩니다.  
  
 **SQL_DESC_NUM_PREC_RADIX [모두]**  
 SQL_DESC_TYPE 필드의 데이터 형식이 근사 숫자 데이터 형식인 경우이 SQLINTEGER 필드에는 값 2가 포함 됩니다. SQL_DESC_PRECISION 필드에는 비트 수가 포함 되어 있기 때문입니다. SQL_DESC_TYPE 필드의 데이터 형식이 정확한 숫자 데이터 형식인 경우에는이 필드의 값이 10입니다. SQL_DESC_PRECISION 필드에는 10 진수 숫자가 포함 되어 있기 때문입니다. 숫자가 아닌 모든 데이터 형식에 대해이 필드는 0으로 설정 됩니다.  
  
 **SQL_DESC_OCTET_LENGTH [모두]**  
 이 SQLLEN 레코드 필드에는 문자열 또는 이진 데이터 형식의 길이 (바이트)가 포함 됩니다. 고정 길이 문자 또는 이진 형식의 경우 실제 길이 (바이트)입니다. 가변 길이 문자 또는 이진 형식의 경우 최대 길이 (바이트)입니다. 이 값은 항상 구현 설명자의 null 종료 문자에 대 한 공간을 제외 하며, 항상 응용 프로그램 설명자의 null 종료 문자에 대 한 공간을 포함 합니다. 응용 프로그램 데이터의 경우이 필드는 버퍼의 크기를 포함 합니다. APDs의 경우이 필드는 출력 또는 입/출력 매개 변수에 대해서만 정의 됩니다.  
  
 **SQL_DESC_OCTET_LENGTH_PTR [응용 프로그램 설명자]**  
 이 SQLLEN * 레코드 필드는 동적 인수 (매개 변수 설명자의 경우) 또는 바인딩된 열 값 (행 설명자의 경우)의 총 길이 (바이트)를 포함 하는 변수를 가리킵니다.  
  
 APD의 경우 문자열 및 binary를 제외한 모든 인수에 대해이 값이 무시 됩니다. 이 필드가 SQL_NTS를 가리키는 경우 동적 인수는 null로 종료 되어야 합니다. 바인딩된 매개 변수가 실행 시 데이터 매개 변수가 됨을 나타내기 위해 응용 프로그램은 APD의 적절 한 레코드에서이 필드를 실행 시간에 SQL_DATA_AT_EXEC 값 또는 SQL_LEN_DATA_AT_EXEC 매크로의 결과를 포함 하는 변수로 설정 합니다. 이러한 필드가 둘 이상 있는 경우 매개 변수를 고유 하 게 식별 하는 값으로 설정 하 여 응용 프로그램에서 요청 된 매개 변수를 확인할 수 있도록 SQL_DESC_DATA_PTR 수 있습니다.  
  
 가 중의 OCTET_LENGTH_PTR 필드가 null 포인터인 경우 드라이버는 열에 대 한 길이 정보를 반환 하지 않습니다. APD의 SQL_DESC_OCTET_LENGTH_PTR 필드가 null 포인터인 경우 드라이버는 문자열 및 이진 값이 null로 종료 된 것으로 가정 합니다. 이진 값은 null로 종료 되어서는 안 되며 잘림 방지를 위해 길이가 지정 되어야 합니다.  
  
 이 필드가 가리키는 버퍼를 채우는 **Sqlfetch** 또는 **sqlfetchscroll** 에 대 한 호출이 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO을 반환 하지 않은 경우 버퍼 내용이 정의 되지 않습니다. 이 필드는 *지연 된 필드*입니다. 설정 시에는 사용 되지 않지만 나중에 드라이버에서 데이터의 옥텟 길이를 확인 하거나 나타내는 데 사용 됩니다.  
  
 **SQL_DESC_PARAMETER_TYPE [IPDs]**  
 이 SQLSMALLINT record 필드는 입력 매개 변수에 대 한 SQL_PARAM_INPUT, 입력/출력 매개 변수 SQL_PARAM_INPUT_OUTPUT, 출력 매개 변수에 대 한 SQL_PARAM_OUTPUT, 입력/출력 스트리밍된 매개 변수에 대 한 SQL_PARAM_INPUT_OUTPUT_STREAM 또는 출력 스트리밍된 매개 변수의 SQL_PARAM_OUTPUT_STREAM로 설정 됩니다. 기본적으로 SQL_PARAM_INPUT로 설정 됩니다.  
  
 IPD의 경우 IPD가 자동으로 드라이버에 의해 채워지지 않은 경우 (SQL_ATTR_ENABLE_AUTO_IPD 문 특성이 SQL_FALSE) 필드는 기본적으로 SQL_PARAM_INPUT 설정 됩니다. 응용 프로그램에서는 입력 매개 변수가 아닌 매개 변수에 대 한 IPD 필드를 설정 해야 합니다.  
  
 **SQL_DESC_PRECISION [모두]**  
 이 SQLSMALLINT 레코드 필드에는 정확한 숫자 형식의 자릿수, 근사 숫자 형식에 대 한가 수 (이진 전체 자릿수)의 비트 수 또는 SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP 또는 SQL_INTERVAL_SECOND 데이터 형식에 대 한 소수 자릿수 초의 구성 요소 수를 포함 합니다. 다른 모든 데이터 형식에 대해서는이 필드가 정의 되어 있지 않습니다.  
  
 이 필드의 값은 ODBC 2.x에 정의 된 "전체 자릿수"의 값과 다를 수*있습니다.* 자세한 내용은 [부록 D: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md)을 참조 하세요.  
  
 **SQL_DESC_ROWVER [구현 설명자]**  
 이 SQLSMALLINTrecord 필드는 행이 업데이트 될 때 DBMS에서 열을 자동으로 수정 하는지 여부를 나타냅니다 (예: SQL Server). 열이 행 버전 관리 열 이면이 레코드 필드의 값이 SQL_TRUE로 설정 되 고, 그렇지 않으면 SQL_FALSE 됩니다. 이 열 특성은 열이 자동으로 업데이트 되는지 여부를 확인 하기 위해 SQL_ROWVER IdentifierType를 사용 하 여 **SQLSpecialColumns** 를 호출 하는 것과 비슷합니다.  
  
 **SQL_DESC_SCALE [모두]**  
 이 SQLSMALLINT record 필드는 decimal 및 numeric 데이터 형식에 대해 정의 된 소수 자릿수를 포함 합니다. 필드는 다른 모든 데이터 형식에 대해 정의 되지 않습니다.  
  
 이 필드의 값은 ODBC 2.x에 정의 된 "scale"의 값과 다를 수 있습니다 *.* 자세한 내용은 [부록 D: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md)을 참조 하세요.  
  
 **SQL_DESC_SCHEMA_NAME [IRDs]**  
 이 읽기 전용 SQLCHAR * 레코드 필드에는 열을 포함 하는 기본 테이블의 스키마 이름이 포함 됩니다. 열이 식인 경우 또는 열이 뷰의 일부인 경우 반환 값은 드라이버에 따라 달라 집니다. 데이터 원본에서 스키마를 지원 하지 않거나 스키마 이름을 확인할 수 없는 경우이 변수에는 빈 문자열이 포함 됩니다.  
  
 **SQL_DESC_SEARCHABLE [IRDs]**  
 이 읽기 전용 SQLSMALLINT record 필드는 다음 값 중 하나로 설정 됩니다.  
  
-   **WHERE** 절에서 열을 사용할 수 없는 경우 SQL_PRED_NONE 합니다. 이 값은 ODBC 2.x의 SQL_UNSEARCHABLE 값과 동일*합니다.*  
  
-   **Where** 절에서 열을 사용할 수 있지만 **LIKE** 조건자를 사용 하 여 열을 사용할 수 있는지 여부를 SQL_PRED_CHAR 합니다. 이 값은 ODBC 2.x의 SQL_LIKE_ONLY 값과 동일*합니다.*  
  
-   **LIKE**를 제외한 모든 비교 연산자가 있는 **WHERE** 절에서 열을 사용할 수 있는지 여부를 SQL_PRED_BASIC 합니다. 이 값은 ODBC 2.x의 SQL_EXCEPT_LIKE 값과 동일*합니다.*  
  
-   **WHERE** 절에서 비교 연산자를 사용 하 여 열을 사용할 수 있는지 여부를 SQL_PRED_SEARCHABLE 합니다.  
  
 **SQL_DESC_TABLE_NAME [IRDs]**  
 이 읽기 전용 SQLCHAR * 레코드 필드는이 열을 포함 하는 기본 테이블의 이름을 포함 합니다. 열이 식인 경우 또는 열이 뷰의 일부인 경우 반환 값은 드라이버에 따라 달라 집니다.  
  
 **SQL_DESC_TYPE [모두]**  
 이 SQLSMALLINT record 필드는 datetime 및 interval 데이터 형식을 제외한 모든 데이터 형식에 대 한 간결한 SQL 또는 C 데이터 형식을 지정 합니다. Datetime 및 interval 데이터 형식의 경우이 필드는 SQL_DATETIME 또는 SQL_INTERVAL 상세 데이터 형식을 지정 합니다.  
  
 이 필드에 SQL_DATETIME 또는 SQL_INTERVAL 포함 될 때마다 SQL_DESC_DATETIME_INTERVAL_CODE 필드에 간결한 형식에 대 한 적절 한 하위 코드가 포함 되어야 합니다. Datetime 데이터 형식의 경우 SQL_DESC_TYPE에는 SQL_DATETIME 포함 되 고 SQL_DESC_DATETIME_INTERVAL_CODE 필드에는 특정 datetime 데이터 형식에 대 한 하위 코드가 포함 됩니다. Interval 데이터 형식의 경우 SQL_DESC_TYPE에는 SQL_INTERVAL 포함 되 고 SQL_DESC_DATETIME_INTERVAL_CODE 필드에는 특정 interval 데이터 형식에 대 한 하위 코드가 포함 됩니다.  
  
 SQL_DESC_TYPE 및 SQL_DESC_CONCISE_TYPE 필드의 값은 상호 종속적입니다. 필드 중 하나가 설정 될 때마다 다른 필드도 설정 해야 합니다. **SQLSetDescField** 또는 **SQLSetDescRec**를 호출 하 여 SQL_DESC_TYPE를 설정할 수 있습니다. **SQLBindCol** 또는 **SQLBindParameter**또는 **SQLSetDescField**에 대 한 호출을 통해 SQL_DESC_CONCISE_TYPE를 설정할 수 있습니다.  
  
 SQL_DESC_TYPE가 interval 또는 datetime 데이터 형식이 아닌 간결한 데이터 형식으로 설정 된 경우에는 SQL_DESC_CONCISE_TYPE 필드가 동일한 값으로 설정 되 고 SQL_DESC_DATETIME_INTERVAL_CODE 필드가 0으로 설정 됩니다.  
  
 SQL_DESC_TYPE이 verbose datetime 또는 interval 데이터 형식 (SQL_DATETIME 또는 SQL_INTERVAL)으로 설정 되 고 SQL_DESC_DATETIME_INTERVAL_CODE 필드가 적절 한 하위 코드로 설정 된 경우 SQL_DESC_CONCISE 형식 필드는 해당 하는 간결한 형식으로 설정 됩니다. SQL_DESC_TYPE를 간결한 datetime 또는 interval 유형 중 하나로 설정 하려고 하면 SQLSTATE HY021 (일치 하지 않는 설명자 정보)가 반환 됩니다.  
  
 **SQLBindCol**, **SQLBindParameter**또는 **SQLSetDescField**에 대 한 호출로 SQL_DESC_TYPE 필드가 설정 된 경우 다음 필드는 아래 표에 나와 있는 것 처럼 다음과 같은 기본값으로 설정 됩니다. 같은 레코드의 나머지 필드 값은 정의 되지 않습니다.  
  
|SQL_DESC_TYPE의 값|암시적으로 설정 되는 다른 필드|  
|------------------------------|---------------------------------|  
|SQL_CHAR, SQL_VARCHAR, SQL_C_CHAR, SQL_C_VARCHAR|SQL_DESC_LENGTH 1로 설정 됩니다. SQL_DESC_PRECISION는 0으로 설정 됩니다.|  
|SQL_DATETIME|SQL_DESC_DATETIME_INTERVAL_CODE SQL_CODE_DATE 또는 SQL_CODE_TIME으로 설정 된 경우 SQL_DESC_PRECISION는 0으로 설정 됩니다. SQL_DESC_TIMESTAMP로 설정 된 경우 SQL_DESC_PRECISION는 6으로 설정 됩니다.|  
|SQL_DECIMAL, SQL_NUMERIC, SQL_C_NUMERIC|SQL_DESC_SCALE는 0으로 설정 됩니다. SQL_DESC_PRECISION는 각 데이터 형식에 대해 구현에 정의 된 전체 자릿수로 설정 됩니다.<br /><br /> SQL_C_NUMERIC 값을 수동으로 바인딩하는 방법에 대 한 자세한 내용은 [SQL에서 C로: Numeric](../../../odbc/reference/appendixes/sql-to-c-numeric.md) 을 참조 하세요.|  
|SQL_FLOAT, SQL_C_FLOAT|SQL_DESC_PRECISION은 SQL_FLOAT의 구현에서 정의 된 기본 전체 자릿수로 설정 됩니다.|  
|SQL_INTERVAL|SQL_DESC_DATETIME_INTERVAL_CODE INTERVAL 데이터 형식으로 설정 된 경우 SQL_DESC_DATETIME_INTERVAL_PRECISION는 2 (기본 간격으로 선행 전체 자릿수)로 설정 됩니다. 간격에 초 구성 요소가 있는 경우 SQL_DESC_PRECISION은 6 (기본 간격 초 전체 자릿수)으로 설정 됩니다.|  
  
 응용 프로그램에서 **SQLSetDescField** 를 호출 하 여 **SQLSetDescRec**를 호출 하는 대신 설명자의 필드를 설정 하는 경우 응용 프로그램은 먼저 데이터 형식을 선언 해야 합니다. 이 경우 앞의 표에 나와 있는 다른 필드는 암시적으로 설정 됩니다. 암시적으로 설정 된 값이 허용 되지 않는 경우 응용 프로그램에서 **SQLSetDescField** 또는 **SQLSetDescRec** 를 호출 하 여 허용 되지 않는 값을 명시적으로 설정할 수 있습니다.  
  
 **SQL_DESC_TYPE_NAME [구현 설명자]**  
 이 읽기 전용 SQLCHAR * 레코드 필드에는 데이터 원본 종속 형식 이름 (예: "CHAR", "VARCHAR" 등)이 포함 되어 있습니다. 데이터 형식 이름을 알 수 없는 경우이 변수에는 빈 문자열이 포함 됩니다.  
  
 **SQL_DESC_UNNAMED [구현 설명자]**  
 행 설명자의이 SQLSMALLINT record 필드는 SQL_DESC_NAME 필드를 설정 하는 경우 SQL_NAMED 또는 SQL_UNNAMED에 의해 설정 됩니다. SQL_DESC_NAME 필드에 열 별칭이 있거나 열 별칭이 적용 되지 않는 경우 드라이버는 SQL_DESC_UNNAMED 필드를 SQL_NAMED로 설정 합니다. 응용 프로그램에서 IPD의 SQL_DESC_NAME 필드를 매개 변수 이름 또는 별칭으로 설정 하는 경우 드라이버는 IPD의 SQL_DESC_UNNAMED 필드를 SQL_NAMED로 설정 합니다. 열 이름이 나 열 별칭이 없으면 드라이버는 SQL_DESC_UNNAMED 필드를 SQL_UNNAMED으로 설정 합니다.  
  
 응용 프로그램은 IPD의 SQL_DESC_UNNAMED 필드를 SQL_UNNAMED으로 설정할 수 있습니다. 응용 프로그램에서 IPD의 SQL_DESC_UNNAMED 필드를 SQL_NAMED로 설정 하려고 시도 하는 경우 드라이버는 SQLSTATE HY091 (잘못 된 설명자 필드 식별자)를 반환 합니다. IRD의 SQL_DESC_UNNAMED 필드는 읽기 전용입니다. 응용 프로그램에서 설정 하려고 시도 하는 경우 SQLSTATE HY091 (잘못 된 설명자 필드 식별자)가 반환 됩니다.  
  
 **SQL_DESC_UNSIGNED [구현 설명자]**  
 이 읽기 전용 SQLSMALLINT record 필드는 열 유형이 부호가 없거나 숫자가 아닌 경우 SQL_TRUE로 설정 되 고, 열 유형이 서명 된 경우에는 SQL_FALSE.  
  
 **SQL_DESC_UPDATABLE [IRDs]**  
 이 읽기 전용 SQLSMALLINT record 필드는 다음 값 중 하나로 설정 됩니다.  
  
-   결과 집합 열이 읽기 전용인 경우 SQL_ATTR_READ_ONLY 합니다.  
  
-   결과 집합 열이 읽기/쓰기로 설정 되 면 SQL_ATTR_WRITE 합니다.  
  
-   결과 집합 열을 업데이트할 수 있는지 여부를 알 수 없는 경우에 SQL_ATTR_READWRITE_UNKNOWN 합니다.  
  
 SQL_DESC_UPDATABLE은 기본 테이블의 열이 아니라 결과 집합의 열에 대 한 업데이트 가능성을 설명 합니다. 이 결과 집합 열이 기반으로 하는 기본 테이블의 열에 대 한 업데이트 가능성은이 필드의 값과 다를 수 있습니다. 열을 업데이트할 수 있는지 여부는 데이터 형식, 사용자 권한 및 결과 집합 자체의 정의를 기반으로 할 수 있습니다. 열을 업데이트할 수 있는지 명확 하지 않은 경우 SQL_ATTR_READWRITE_UNKNOWN 반환 되어야 합니다.  
  
## <a name="consistency-checks"></a>일관성 확인  
 응용 프로그램이 IPD, APD 또는의 SQL_DESC_DATA_PTR 필드 값을 전달할 때마다 자동으로 일관성 확인이 수행 됩니다. 필드 중 하나라도 다른 필드와 일치 하지 않는 경우 **SQLSetDescField** 는 SQLSTATE HY021 (일치 하지 않는 설명자 정보)를 반환 합니다. 자세한 내용은 [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)의 "일관성 확인"을 참조 하십시오.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|열 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|매개 변수 바인딩|[SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|설명자 필드 가져오기|[SQLGetDescField 함수](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|여러 설명자 필드 가져오기|[SQLGetDescRec 함수](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|여러 설명자 필드 설정|[SQLSetDescRec 함수](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)
