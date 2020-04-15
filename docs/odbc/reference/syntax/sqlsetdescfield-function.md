---
title: SQLSetDescField 기능 | 마이크로 소프트 문서
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
ms.openlocfilehash: 122d4b26d1d75811d4a8e252378ce8f81ca2c66b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299553"
---
# <a name="sqlsetdescfield-function"></a>SQLSetDescField 함수

**규칙**  
 버전 출시: ODBC 3.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLSetDescField는** 설명자 레코드의 단일 필드의 값을 설정합니다.  
  
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
 [입력] 응용 프로그램에서 설정하려는 필드를 포함하는 설명자 레코드를 나타냅니다. 설명자 레코드는 0에서 번호가 매겨지며 레코드 번호 0은 책갈피 레코드입니다. *RecNumber* 인수는 헤더 필드에 대해 무시됩니다.  
  
 *FieldIdentifier*  
 [입력] 값을 설정할 설명자의 필드를 나타냅니다. 자세한 내용은 "주석" 섹션에서 *"필드 식별자* 인수"를 참조하십시오.  
  
 *ValuePtr*  
 [입력] 설명자 정보 또는 정수 값을 포함하는 버퍼에 대한 포인터입니다. 데이터 형식은 *FieldIdentifier*의 값에 따라 달라집니다. *ValuePtr이* 정수 값인 경우 *FieldIdentifier* 인수의 값에 따라 8바이트(SQLLEN), 4바이트(SQLINTEGER) 또는 2바이트(SQLSMALLINT)로 간주될 수 있습니다.  
  
 *버퍼 길이*  
 [입력] *FieldIdentifier가* ODBC 정의 필드이고 *ValuePtr이* 문자 문자열 또는 이진 버퍼를 가리키는 경우 이 인수는 **ValuePtr*의 길이여야 합니다. 문자열 데이터의 경우 이 인수에는 문자열의 바이트 수가 포함되어야 합니다.  
  
 *필드식별자가* ODBC 정의 필드이고 *ValuePtr이* 정수인 경우 *버퍼길이는* 무시됩니다.  
  
 *FieldIdentifier가* 드라이버 정의 필드인 경우 응용 프로그램은 *BufferLength* 인수를 설정하여 드라이버 관리자에 필드의 특성을 나타냅니다. *BufferLength에는* 다음 값이 있을 수 있습니다.  
  
-   *ValuePtr이* 문자 문자열에 대한 포인터인 경우 *BufferLength는* 문자열 또는 SQL_NTS 길이입니다.  
  
-   *ValuePtr이* 이진 버퍼에 대한 포인터인 경우 응용 프로그램은*SQL_LEN_BINARY_ATTR(길이)* 매크로의 결과를 *BufferLength*에 배치합니다. 이렇게 하면 *버퍼길이에*음수 값이 배치됩니다.  
  
-   *ValuePtr이* 문자 문자열 이나 이진 문자열 이외의 값에 대 한 포인터 인 경우 *BufferLength* 값 SQL_IS_POINTER 있어야 합니다.  
  
-   *ValuePtr* 고정 길이 값을 포함 하는 경우 *BufferLength는* SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT 또는 SQL_IS_USMALLINT 적절 하 게.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLSetDescField** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환 하는 경우 관련 된 SQLSTATE 값 은 *SQL_HANDLE_DESC 핸들 유형* 및 *설명자 핸들*의 *핸들을* 호출 하 여 **SQLGetDiagRec** 를 호출 할 수 있습니다. 다음 표에서는 **SQLSetDescField에서** 일반적으로 반환하는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01S02|옵션 값이 변경되었습니다.|드라이버는 * \*ValuePtr(ValuePtr이* 포인터인 *ValuePtr* 경우) 또는 *ValuePtr의* *값(값Ptr이* 정수 값인 경우) 또는 * \*ValuePtr에* 지정된 값을 지원하지 않았거나, 구현 작업 조건으로 인해 ValuePtr이 유효하지 않아 드라이버가 유사한 값을 대체했습니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|07009|잘못된 설명자 인덱스|*FieldIdentifier* 인수는 레코드 필드이고 *RecNumber* 인수는 0이고 *설명자핸들* 인수는 IPD 핸들을 참조했습니다.<br /><br /> *RecNumber* 인수가 0보다 적고 *설명자 핸들* 인수가 ARD 또는 APD를 참조했습니다.<br /><br /> *RecNumber* 인수는 데이터 원본이 지원할 수 있는 최대 열 또는 매개 변수 수보다 크고 *설명자핸들* 인수는 APD 또는 ARD를 참조했습니다.<br /><br /> (DM) *필드식별자* 인수가 SQL_DESC_COUNT * \*값Ptr* 인수가 0보다 적었습니다.<br /><br /> *RecNumber* 인수는 0이고 *설명자핸들* 인수는 암시적으로 할당된 APD를 참조했습니다. 이 오류는 명시적으로 할당된 응용 프로그램 설명자가 실행 시간까지 APD 또는 ARD인지 여부를 알 수 없기 때문에 명시적으로 할당된 응용 프로그램 설명자에서는 발생하지 않습니다.|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결된 데이터 원본 간의 통신 링크가 실패했습니다.|  
|22001|문자열 데이터, 오른쪽 잘린|*FieldIdentifier* 인수가 SQL_DESC_NAME *버퍼길이* 인수는 SQL_MAX_IDENTIFIER_LEN 값보다 큽했습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류|(DM) *설명자 핸들은* 비동기적으로 실행 되는 함수 (이 되지 않음)를 호출 하 고이 함수를 호출 할 때 여전히 실행 되 고 있는 *StatementHandle와* 연결 되었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *설명자 핸들이* 연결되고 SQL_NEED_DATA 반환되는 *문 핸들에* 대해 호출되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.<br /><br /> (DM) *설명자 핸들과*연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. **SQLSetDescField** 함수가 호출될 때 이 비동기 함수는 여전히 실행 중이었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *설명자 핸들과* 연결된 명령문 핸들 중 하나를 호출하고 SQL_PARAM_DATA_AVAILABLE 반환되었습니다. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY016|구현 행 설명자 수정할 수 없습니다.|*설명자핸들* 인수는 IRD와 연결되었으며 *FieldIdentifier* 인수는 SQL_DESC_ARRAY_STATUS_PTR SQL_DESC_ROWS_PROCESSED_PTR 않았습니다.|  
|HY021|일관되지 않은 설명자 정보|SQL_DESC_TYPE 및 SQL_DESC_DATETIME_INTERVAL_CODE 필드는 유효한 ODBC SQL 유형 또는 유효한 드라이버 관련 SQL 유형(IPD용) 또는 유효한 ODBC C 유형(APD 또는 ARD의 경우)을 형성하지 않습니다.<br /><br /> 일관성 검사 중에 확인된 설명자 정보가 일치하지 않았습니다. **(SQLSetDescRec에서**"일관성 검사"를 참조하십시오.)|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|(DM) * \*ValuePtr은* 문자 문자열이며 *BufferLength는* 0보다 작지만 SQL_NTS 같지 않았습니다.<br /><br /> (DM) 드라이버가 ODBC 2 *.x* 드라이버이고, 설명자가 ARD이고, *ColumnNumber* 인수가 0으로 설정되었으며, *인수 BufferLength에* 대해 지정된 값이 4와 같지 않았습니다.|  
|HY091|잘못된 설명자 필드 식별자|*FieldIdentifier* 인수에 대해 지정된 값은 ODBC 정의 필드가 아니며 구현 정의 값이 아닙니다.<br /><br /> 설명자 *핸들* 인수에 대해 *FieldIdentifier* 인수가 잘못되었습니다.<br /><br /> *FieldIdentifier* 인수는 읽기 전용 ODBC 정의 필드입니다.|  
|HY092|잘못된 특성/옵션 식별자|* \*ValuePtr의* 값이 *FieldIdentifier* 인수에 대해 유효하지 않습니다.<br /><br /> *필드식별자* 인수는 SQL_DESC_UNNAMED *값Ptr이* SQL_NAMED.|  
|HY105|잘못된 매개 변수 유형|(DM) SQL_DESC_PARAMETER_TYPE 필드에 지정된 값이 잘못되었습니다. (자세한 내용은 **SQLBindParameter의***"입력 출력 유형* 인수" 섹션을 참조하십시오.)|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [ODBC 3.8에서 새로운 내용을](../../../odbc/reference/what-s-new-in-odbc-3-8.md)참조 하십시오.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *설명자핸들과* 연결된 드라이버는 기능을 지원하지 않습니다.|  
  
## <a name="comments"></a>주석  
 응용 프로그램은 **SQLSetDescField를** 호출하여 설명자 필드를 한 번에 하나씩 설정할 수 있습니다. **SQLSetDescField에** 대한 한 호출은 단일 설명자에서 단일 필드를 설정합니다. 필드를 설정할 수 있는 경우 이 함수를 호출하여 모든 설명자 유형의 필드를 설정할 수 있습니다. (이 섹션의 후반표를 참조하십시오.)  
  
> [!NOTE]  
>  **SQLSetDescField에** 대한 호출이 실패하면 *RecNumber* 인수로 식별된 설명자 레코드의 내용은 정의되지 않습니다.  
  
 함수의 단일 호출로 여러 설명자 필드를 설정하기 위해 다른 함수를 호출할 수 있습니다. **SQLSetDescRec** 함수는 열 또는 매개 변수(SQL_DESC_TYPE, SQL_DESC_DATETIME_INTERVAL_CODE, SQL_DESC_OCTET_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE, SQL_DESC_DATA_PTR, SQL_DESC_OCTET_LENGTH_PTR 및 SQL_DESC_INDICATOR_PTR 필드)에 바인딩된 데이터 형식 및 버퍼에 영향을 주는 다양한 필드를 설정합니다. **SQLBindCol** 또는 **SQLBindParameter열** 또는 매개 변수의 바인딩에 대 한 전체 사양을 만드는 데 사용할 수 있습니다. 이러한 함수는 하나의 함수 호출을 통해 설명자 필드의 특정 그룹을 설정합니다.  
  
 **SQLSetDescField** 바인딩 포인터 (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR 또는 SQL_DESC_OCTET_LENGTH_PTR)에 오프셋을 추가 하 여 바인딩 버퍼를 변경 하려면 호출할 수 있습니다. 이렇게 하면 **SQLBindCol** 또는 **SQLBindParameter를**호출하지 않고 바인딩 버퍼가 변경되어 응용 프로그램이 SQL_DESC_DATA_TYPE 같은 다른 필드를 변경하지 않고 SQL_DESC_DATA_PTR 변경할 수 있습니다.  
  
 응용 프로그램에서 **SQLSetDescField를** 호출하여 SQL_DESC_COUNT 또는 지연된 필드 SQL_DESC_DATA_PTR, SQL_DESC_OCTET_LENGTH_PTR 또는 SQL_DESC_INDICATOR_PTR 이외의 필드를 설정하면 레코드가 언바운드됩니다.  
  
 설명자 헤더 필드는 **SQLSetDescField를** 적절 한 *필드 식별자를*호출 하 여 설정 됩니다. 많은 헤더 필드는 문 특성이므로 **SQLSetStmtAttr**에 대한 호출로 설정할 수도 있습니다. 이렇게 하면 응용 프로그램에서 설명자 핸들을 먼저 가져오지 않고 설명자 필드를 설정할 수 있습니다. **SQLSetDescField** 헤더 필드를 설정 하기 위해 호출 될 때 *RecNumber* 인수 무시 됩니다.  
  
 *RecNumber* 0은 책갈피 필드를 설정하는 데 사용됩니다.  
  
> [!NOTE]  
>  SQL_ATTR_USE_BOOKMARKS 문 특성은 **SQLSetDescField를** 호출하여 책갈피 필드를 설정하기 전에 항상 설정해야 합니다. 필수는 아니지만 강력히 권장됩니다.  
  
## <a name="sequence-of-setting-descriptor-fields"></a>설명자 필드 설정 시퀀스  
 **SQLSetDescField를**호출하여 설명자 필드를 설정할 때 응용 프로그램은 특정 순서를 따라야 합니다.  
  
1.  응용 프로그램은 먼저 SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE 또는 SQL_DESC_DATETIME_INTERVAL_CODE 필드를 설정해야 합니다.  
  
2.  이러한 필드 중 하나를 설정한 후 응용 프로그램은 데이터 형식의 특성을 설정할 수 있으며 드라이버세트 데이터 형식 특성 필드를 데이터 형식에 대한 적절한 기본값으로 설정합니다. 형식 특성 필드의 자동 기본 설정은 응용 프로그램에서 데이터 형식을 지정한 후 설명자가 항상 사용할 준비가 되도록 합니다. 응용 프로그램이 데이터 형식 특성을 명시적으로 설정하면 기본 특성이 재정의됩니다.  
  
3.  1단계에 나열된 필드 중 하나가 설정되고 데이터 형식 특성이 설정된 후 응용 프로그램은 SQL_DESC_DATA_PTR 설정할 수 있습니다. 이렇게 하면 설명자 필드의 일관성 검사가 표시됩니다. 응용 프로그램이 SQL_DESC_DATA_PTR 필드를 설정한 후 데이터 형식 또는 특성을 변경하면 드라이버는 SQL_DESC_DATA_PTR null 포인터로 설정하여 레코드의 바인딩을 해제합니다. 이렇게 하면 설명자 레코드를 사용할 수 있기 전에 응용 프로그램이 순서대로 적절한 단계를 완료해야 합니다.  
  
## <a name="initialization-of-descriptor-fields"></a>설명자 필드 초기화  
 설명자가 할당되면 설명자의 필드를 기본값으로 초기화하거나, 기본값 없이 초기화하거나, 설명자 유형에 대해 정의되지 않을 수 있습니다. 다음 표는 각 설명자 유형에 대한 각 필드의 초기화를 나타내며, "D"는 필드가 기본값으로 초기화되었음을 나타내고 필드가 기본값 없이 초기화되었음을 나타내는 "ND"를 나타냅니다. 숫자가 표시되면 필드의 기본값은 해당 숫자입니다. 또한 표는 필드가 읽기/쓰기(R/W) 또는 읽기 전용(R)인지를 나타냅니다.  
  
 IRD의 필드에는 명령문이 준비되거나 실행되고 IRD가 채워진 후에만 기본값이 있으며 명령문 핸들 또는 설명자가 할당된 경우는 아닙니다. IRD가 채워질 때까지 IRD 필드에 대한 액세스 권한을 얻으려는 모든 시도는 오류를 반환합니다.  
  
 일부 설명자 필드는 설명자 유형(ARD 및 IrD, APD 및 IPD)의 하나 이상에 대해 정의되지만 전부는 아닙니다. 설명자 유형에 대해 필드가 정의되지 않은 경우 해당 설명자(설명자)를 사용하는 함수에는 필드가 필요하지 않습니다.  
  
 **SQLGetDescField에서** 액세스할 수 있는 필드는 **SQLSetDescField**. **SQLSetDescField에서** 설정할 수 있는 필드는 다음 표에 나열됩니다.  
  
 헤더 필드의 초기화는 다음 표에 설명되어 있습니다.  
  
|헤더 필드 이름|Type|R/W|기본값|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_ALLOC_TYPE|SQLSMALLINT|ARD : R APD : R IRD : R IPD : R|ARD: 명시적 SQL_DESC_ALLOC_USER 대한 암시적 또는 SQL_DESC_ALLOC_USER SQL_DESC_ALLOC_AUTO<br /><br /> APD: 명시적 SQL_DESC_ALLOC_USER 대한 SQL_DESC_ALLOC_AUTO<br /><br /> IRD: SQL_DESC_ALLOC_AUTO<br /><br /> IPD: SQL_DESC_ALLOC_AUTO|  
|SQL_DESC_ARRAY_SIZE|볼렌 (미국)의|ARD: R/W APD: R/W IRD: 미사용 IPD: 미사용|ARD:[1] APD:[1] IRD: 사용하지 않은 IPD: 미사용|  
|SQL_DESC_ARRAY_STATUS_PTR|SQLUSmallinT*|ARD : R / W APD : R / W IRD : R / W IPD : R / W|ARD: 널 ptr APD: 널 ptr IRD: 널 ptr IPD: 널 ptr|  
|SQL_DESC_BIND_OFFSET_PTR|SQLLEN*|ARD: R/W APD: R/W IRD: 미사용 IPD: 미사용|ARD: 널 ptr APD: 널 ptr IRD: 미사용 IPD: 미사용|  
|SQL_DESC_BIND_TYPE|SQLINTEGER|ARD: R/W APD: R/W IRD: 미사용 IPD: 미사용|ARD: SQL_BIND_BY_COLUMN<br /><br /> APD: SQL_BIND_BY_COLUMN<br /><br /> IRD: 미사용<br /><br /> IPD: 미사용|  
|SQL_DESC_COUNT|SQLSMALLINT|ARD : R / W APD : R / W IRD : R IPD : R / W|ARD : 0 APD : 0 IRD : D IPD : 0|  
|SQL_DESC_ROWS_PROCESSED_PTR|SQLULEN*|ARD: 사용하지 않은 APD: 사용하지 않은 IRD: R/W IPD: R/W|ARD: 사용하지 않은 APD: 사용하지 않는 IRD: 널 ptr IPD: 널 ptr|  
  
 [1] 이러한 필드는 IPD가 드라이버에 의해 자동으로 채워지는 경우에만 정의됩니다. 그렇지 않은 경우 정의되지 않습니다. 응용 프로그램이 이러한 필드를 설정하려고 하면 SQLSTATE HY091(잘못된 설명자 필드 식별자)이 반환됩니다.  
  
 레코드 필드의 초기화는 다음 표와 같습니다.  
  
|레코드 필드 이름|Type|R/W|기본값|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|ARD: 사용하지 않은 APD: 사용하지 않은 IRD: R IPD: 미사용|ARD: 사용하지 않은 APD: 사용하지 않은 IRD: D IPD: 미사용|  
|SQL_DESC_BASE_COLUMN_NAME|SQLCHAR *|ARD: 사용하지 않은 APD: 사용하지 않은 IRD: R IPD: 미사용|ARD: 사용하지 않은 APD: 사용하지 않은 IRD: D IPD: 미사용|  
|SQL_DESC_BASE_TABLE_NAME|SQLCHAR *|ARD: 사용하지 않은 APD: 사용하지 않은 IRD: R IPD: 미사용|ARD: 사용하지 않은 APD: 사용하지 않은 IRD: D IPD: 미사용|  
|SQL_DESC_CASE_SENSITIVE|SQLINTEGER|ARD: 사용하지 않은 APD: 사용하지 않는 IRD: R IPD: R|ARD: 사용하지 않은 APD: 사용하지 않는 IRD: D IPD: D[1]|  
|SQL_DESC_CATALOG_NAME|SQLCHAR *|ARD: 사용하지 않은 APD: 사용하지 않은 IRD: R IPD: 미사용|ARD: 사용하지 않은 APD: 사용하지 않은 IRD: D IPD: 미사용|  
|SQL_DESC_CONCISE_TYPE|SQLSMALLINT|ARD : R / W APD : R / W IRD : R IPD : R / W|ARD: SQL_C_ 기본 APD: SQL_C_ 기본 IRD: D IPD: ND|  
|SQL_DESC_DATA_PTR|SQL포인터|ARD: R/W APD: R/W IRD: 미사용 IPD: 미사용|ARD: 널 ptr APD: 널 ptr IRD: 사용하지 않은 IPD: 미사용[2]|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQLSMALLINT|ARD : R / W APD : R / W IRD : R IPD : R / W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|SQLINTEGER|ARD : R / W APD : R / W IRD : R IPD : R / W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_DISPLAY_SIZE|SQLLEN|ARD: 사용하지 않은 APD: 사용하지 않은 IRD: R IPD: 미사용|ARD: 사용하지 않은 APD: 사용하지 않은 IRD: D IPD: 미사용|  
|SQL_DESC_FIXED_PREC_SCALE|SQLSMALLINT|ARD: 사용하지 않은 APD: 사용하지 않는 IRD: R IPD: R|ARD: 사용하지 않은 APD: 사용하지 않는 IRD: D IPD: D[1]|  
|SQL_DESC_INDICATOR_PTR|SQLLEN *|ARD: R/W APD: R/W IRD: 미사용 IPD: 미사용|ARD: 널 ptr APD: 널 ptr IRD: 미사용 IPD: 미사용|  
|SQL_DESC_LABEL|SQLCHAR *|ARD: 사용하지 않은 APD: 사용하지 않은 IRD: R IPD: 미사용|ARD: 사용하지 않은 APD: 사용하지 않은 IRD: D IPD: 미사용|  
|SQL_DESC_LENGTH|볼렌 (미국)의|ARD : R / W APD : R / W IRD : R IPD : R / W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_LITERAL_PREFIX|SQLCHAR *|ARD: 사용하지 않은 APD: 사용하지 않은 IRD: R IPD: 미사용|ARD: 사용하지 않은 APD: 사용하지 않은 IRD: D IPD: 미사용|  
|SQL_DESC_LITERAL_SUFFIX|SQLCHAR *|ARD: 사용하지 않은 APD: 사용하지 않은 IRD: R IPD: 미사용|ARD: 사용하지 않은 APD: 사용하지 않은 IRD: D IPD: 미사용|  
|SQL_DESC_LOCAL_TYPE_NAME|SQLCHAR *|ARD: 사용하지 않은 APD: 사용하지 않는 IRD: R IPD: R|ARD: 사용하지 않은 APD: 사용하지 않는 IRD: D IPD: D[1]|  
|SQL_DESC_NAME|SQLCHAR *|ARD: 사용하지 않은 APD: 사용하지 않는 IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_NULLABLE|SQLSMALLINT|ARD: 사용하지 않은 APD: 사용하지 않는 IRD: R IPD: R|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_NUM_PREC_RADIX|SQLINTEGER|ARD : R / W APD : R / W IRD : R IPD : R / W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_OCTET_LENGTH|SQLLEN|ARD : R / W APD : R / W IRD : R IPD : R / W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_OCTET_LENGTH_PTR|SQLLEN *|ARD: R/W APD: R/W IRD: 미사용 IPD: 미사용|ARD: 널 ptr APD: 널 ptr IRD: 미사용 IPD: 미사용|  
|SQL_DESC_PARAMETER_TYPE|SQLSMALLINT|ARD: 사용하지 않은 APD: 사용하지 않은 IRD: 사용하지 않은 IPD: R/W|ARD: 사용하지 않은 APD: 사용하지 않은 IRD: 사용하지 않는 IPD: D=SQL_PARAM_INPUT|  
|SQL_DESC_PRECISION|SQLSMALLINT|ARD : R / W APD : R / W IRD : R IPD : R / W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_ROWVER|SQLSMALLINT|ARD: 미사용<br /><br /> APD: 미사용<br /><br /> IRD: R<br /><br /> IPD: R|ARD: 미사용<br /><br /> APD: 미사용<br /><br /> IRD: ND<br /><br /> IPD: ND|  
|SQL_DESC_SCALE|SQLSMALLINT|ARD : R / W APD : R / W IRD : R IPD : R / W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_SCHEMA_NAME|SQLCHAR *|ARD: 사용하지 않은 APD: 사용하지 않은 IRD: R IPD: 미사용|ARD: 사용하지 않은 APD: 사용하지 않은 IRD: D IPD: 미사용|  
|SQL_DESC_SEARCHABLE|SQLSMALLINT|ARD: 사용하지 않은 APD: 사용하지 않은 IRD: R IPD: 미사용|ARD: 사용하지 않은 APD: 사용하지 않은 IRD: D IPD: 미사용|  
|SQL_DESC_TABLE_NAME|SQLCHAR *|ARD: 사용하지 않은 APD: 사용하지 않은 IRD: R IPD: 미사용|ARD: 사용하지 않은 APD: 사용하지 않은 IRD: D IPD: 미사용|  
|SQL_DESC_TYPE|SQLSMALLINT|ARD : R / W APD : R / W IRD : R IPD : R / W|ARD: SQL_C_DEFAULT APD: SQL_C_DEFAULT IRD: D IPD: ND|  
|SQL_DESC_TYPE_NAME|SQLCHAR *|ARD: 사용하지 않은 APD: 사용하지 않는 IRD: R IPD: R|ARD: 사용하지 않은 APD: 사용하지 않는 IRD: D IPD: D[1]|  
|SQL_DESC_UNNAMED|SQLSMALLINT|ARD: 사용하지 않은 APD: 사용하지 않는 IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_UNSIGNED|SQLSMALLINT|ARD: 사용하지 않은 APD: 사용하지 않는 IRD: R IPD: R|ARD: 사용하지 않은 APD: 사용하지 않는 IRD: D IPD: D[1]|  
|SQL_DESC_UPDATABLE|SQLSMALLINT|ARD: 사용하지 않은 APD: 사용하지 않은 IRD: R IPD: 미사용|ARD: 사용하지 않은 APD: 사용하지 않은 IRD: D IPD: 미사용|  
  
 [1] 이러한 필드는 IPD가 드라이버에 의해 자동으로 채워지는 경우에만 정의됩니다. 그렇지 않은 경우 정의되지 않습니다. 응용 프로그램이 이러한 필드를 설정하려고 하면 SQLSTATE HY091(잘못된 설명자 필드 식별자)이 반환됩니다.  
  
 [2] IPD의 SQL_DESC_DATA_PTR 필드를 설정하여 일관성 검사를 강제할 수 있습니다. **SQLGetDescField** 또는 **SQLGetDescRec에**대한 후속 호출에서 드라이버는 SQL_DESC_DATA_PTR 설정된 값을 반환할 필요가 없습니다.  
  
## <a name="fieldidentifier-argument"></a>필드 식별자 인수  
 *FieldIdentifier* 인수는 설정할 설명자 필드를 나타냅니다. 설명자는 다음 섹션인 "헤더 필드" 및 "헤더 필드" 섹션 다음에 설명된 레코드 필드로 *구성된* *설명자 레코드로* 구성된 설명자 헤더를 포함합니다.  
  
## <a name="header-fields"></a>헤더 필드  
 각 설명자는 다음 필드로 구성된 헤더를 가지고 있습니다.  
  
 **SQL_DESC_ALLOC_TYPE [모두]**  
 이 읽기 전용 SQLSMALLINT 헤더 필드는 설명자가 드라이버에 의해 자동으로 할당되었는지 또는 응용 프로그램에서 명시적으로 할당되었는지 여부를 지정합니다. 응용 프로그램은 이 필드를 가져오지만 수정할 수는 없습니다. 드라이버가 설명자가 자동으로 할당된 경우 필드가 드라이버에 의해 SQL_DESC_ALLOC_AUTO 설정됩니다. 설명자가 응용 프로그램에서 명시적으로 할당된 경우 드라이버에서 SQL_DESC_ALLOC_USER 설정됩니다.  
  
 **SQL_DESC_ARRAY_SIZE [응용 프로그램 설명자]**  
 ARD에서 이 SQLULEN 헤더 필드는 행 집합의 행 수를 지정합니다. **SQLFetch** 또는 **SQLFetchScroll** 에 대 한 호출에 의해 반환 되거나 **SQLBulkOperations** 또는 **SQLSetPos**에 대 한 호출에 의해 작동 될 행의 수입니다.  
  
 APD에서 이 SQLULEN 헤더 필드는 각 매개 변수에 대한 값 수를 지정합니다.  
  
 이 필드의 기본값은 1입니다. SQL_DESC_ARRAY_SIZE 1보다 크면 apD 또는 ARD 가 배열에 SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR. 각 배열의 카디널리티는 이 필드의 값과 같습니다.  
  
 ARD의 이 필드는 SQL_ATTR_ROW_ARRAY_SIZE 특성을 가진 **SQLSetStmtAttr을** 호출하여 설정할 수도 있습니다. APD의 이 필드는 **sqlSetStmtAttr을** SQL_ATTR_PARAMSET_SIZE 특성으로 호출하여 설정할 수도 있습니다.  
  
 **SQL_DESC_ARRAY_STATUS_PTR [모두]**  
 각 설명자 형식에 대해 이 SQLUSMALLINT * 헤더 필드는 SQLUSMALLINT 값의 배열을 가리킵니다. 이러한 배열의 이름은 다음과 같습니다: 행 상태 배열(IRD), 매개 변수 상태 배열(IPD), 행 작업 배열(ARD) 및 매개 변수 작업 배열(APD).  
  
 IRD에서 이 헤더 필드는 **SQLBulkOperations, SQLFetch**, **SQLFetchScroll**또는 **SQLFetch** **SQLSetPos**에 대한 호출 후 상태 값을 포함하는 행 상태 배열을 가리킵니다. 배열에는 행집합에 행이 있는 만큼의 요소가 있습니다. 응용 프로그램은 SQLUSMALLINT의 배열을 할당하고 배열을 가리키도록이 필드를 설정해야합니다. 필드는 기본적으로 null 포인터로 설정됩니다. SQL_DESC_ARRAY_STATUS_PTR 필드가 null 포인터로 설정되지 않는 한 드라이버는 배열을 채웁니다.  
  
> [!CAUTION]  
>  응용 프로그램이 IRD의 SQL_DESC_ARRAY_STATUS_PTR 필드가 가리키는 행 상태 배열의 요소를 설정하는 경우 드라이버 동작은 정의되지 않습니다.  
  
 배열은 처음에 **SQLBulkOperations,** **SQLFetch**, **SQLFetchScroll**또는 **SQLSetPos**에 대한 호출로 채워집니다. 호출이 SQL_SUCCESS 반환되지 않거나 SQL_SUCCESS_WITH_INFO 경우 이 필드가 가리키는 배열의 내용은 정의되지 않습니다. 배열의 요소에는 다음 값이 포함될 수 있습니다.  
  
-   SQL_ROW_SUCCESS: 행이 성공적으로 인출되었으며 마지막으로 가져온 이후로 변경되지 않았습니다.  
  
-   SQL_ROW_SUCCESS_WITH_INFO: 행이 성공적으로 인출되었으며 마지막으로 가져온 이후로 변경되지 않았습니다. 그러나 행에 대한 경고가 반환되었습니다.  
  
-   SQL_ROW_ERROR: 행을 가져오는 동안 오류가 발생했습니다.  
  
-   SQL_ROW_UPDATED: 행이 성공적으로 인출되었으며 마지막으로 가져온 이후 업데이트되었습니다. 행을 다시 가져온 경우 해당 상태가 SQL_ROW_SUCCESS.  
  
-   SQL_ROW_DELETED: 행이 마지막으로 가져온 이후 삭제되었습니다.  
  
-   SQL_ROW_ADDED: 행이 **SQLBulkOperations**. 행을 다시 가져온 경우 해당 상태가 SQL_ROW_SUCCESS.  
  
-   SQL_ROW_NOROW: 행 집합이 결과 집합의 끝을 겹치고 행 상태 배열의 이 요소에 해당하는 행이 반환되지 않았습니다.  
  
 IRD의 이 필드는 **sqlSetStmtAttr을** SQL_ATTR_ROW_STATUS_PTR 특성으로 호출하여 설정할 수도 있습니다.  
  
 IRD의 SQL_DESC_ARRAY_STATUS_PTR 필드는 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO 반환된 후에만 유효합니다. 반환 코드가 이들 중 하나가 아닌 경우 SQL_DESC_ROWS_PROCESSED_PTR 가리키는 위치는 정의되지 않습니다.  
  
 IPD에서 이 헤더 필드는 **SQLExecute** 또는 **SQLExecDirect**에 대한 호출 후 각 매개 변수 값 집합에 대한 상태 정보를 포함하는 매개 변수 상태 배열을 가리킵니다. **SQLExecute** 또는 **SQLExecDirect** 호출이 SQL_SUCCESS 반환되지 않거나 SQL_SUCCESS_WITH_INFO 경우 이 필드가 가리키는 배열의 내용은 정의되지 않습니다. 응용 프로그램은 SQLUSMALLINT의 배열을 할당하고 배열을 가리키도록이 필드를 설정해야합니다. SQL_DESC_ARRAY_STATUS_PTR 필드가 null 포인터로 설정되지 않는 한 드라이버는 배열을 채웁니다. 배열의 요소에는 다음 값이 포함될 수 있습니다.  
  
-   SQL_PARAM_SUCCESS: 이 매개 변수 집합에 대해 SQL 문이 성공적으로 실행되었습니다.  
  
-   SQL_PARAM_SUCCESS_WITH_INFO: 이 매개 변수 집합에 대해 SQL 문이 성공적으로 실행되었습니다. 그러나 진단 데이터 구조에서 경고 정보를 사용할 수 있습니다.  
  
-   SQL_PARAM_ERROR: 이 매개 변수 집합을 처리하는 동안 오류가 발생했습니다. 추가 오류 정보는 진단 데이터 구조에서 사용할 수 있습니다.  
  
-   SQL_PARAM_UNUSED: 이 매개 변수 집합은 일부 이전 매개 변수 집합이 추가 처리를 중단하는 오류를 발생했거나 APD의 SQL_DESC_ARRAY_STATUS_PTR 필드에 지정된 배열의 해당 매개 변수 집합에 대해 SQL_PARAM_IGNORE 설정되었기 때문에 사용되지 않았습니다.  
  
-   SQL_PARAM_DIAG_UNAVAILABLE: 진단 정보를 사용할 수 없습니다. 예를 들어 드라이버가 매개 변수 배열을 모놀리식 단위로 처리하므로 이 수준의 오류 정보를 생성하지 않는 경우를 예로 들 수 있습니다.  
  
 IPD의 이 필드는 **sqlSetStmtAttr을** SQL_ATTR_PARAM_STATUS_PTR 특성으로 호출하여 설정할 수도 있습니다.  
  
 ARD에서 이 헤더 필드는 **SQLSetPos** 작업에 대해 이 행을 무시할지 여부를 나타내기 위해 응용 프로그램에서 설정할 수 있는 값의 행 작업 배열을 가리킵니다. 배열의 요소에는 다음 값이 포함될 수 있습니다.  
  
-   SQL_ROW_PROCEED: 행은 **SQLSetPos를**사용 하 여 대량 작업에 포함 됩니다. 이 설정은 행에서 작업이 수행된다는 것을 보장하지 않습니다. 행에 IRD 행 상태 배열에 SQL_ROW_ERROR 상태가 있는 경우 드라이버가 행에서 작업을 수행하지 못할 수 있습니다.)  
  
-   SQL_ROW_IGNORE: 행은 **SQLSetPos를**사용 하 여 대량 작업에서 제외 됩니다.  
  
 배열의 요소가 설정되지 않으면 모든 행이 대량 작업에 포함됩니다. ARD의 SQL_DESC_ARRAY_STATUS_PTR 필드의 값이 null 포인터인 경우 모든 행이 대량 작업에 포함됩니다. 해석은 포인터가 유효한 배열을 가리키고 배열의 모든 요소가 SQL_ROW_PROCEED 것과 같습니다. 배열의 요소가 SQL_ROW_IGNORE 설정된 경우 무시된 행에 대한 행 상태 배열의 값은 변경되지 않습니다.  
  
 ARD의 이 필드는 SQL_ATTR_ROW_OPERATION_PTR 특성을 가진 **SQLSetStmtAttr을** 호출하여 설정할 수도 있습니다.  
  
 APD에서 이 헤더 필드는 **SQLExecute** 또는 **SQLExecDirect가** 호출될 때 이 매개 변수 집합을 무시할지 여부를 나타내기 위해 응용 프로그램에서 설정할 수 있는 값의 매개 변수 작업 배열을 가리킵니다. 배열의 요소에는 다음 값이 포함될 수 있습니다.  
  
-   SQL_PARAM_PROCEED: 매개 변수 집합은 **SQLExecute** 또는 **SQLExecDirect** 호출에 포함 됩니다.  
  
-   SQL_PARAM_IGNORE: 매개 변수 집합은 **SQLExecute** 또는 **SQLExecDirect** 호출에서 제외됩니다.  
  
 배열의 요소가 설정되지 않은 경우 배열의 모든 매개 변수 집합이 **SQLExecute** 또는 **SQLExecDirect** 호출에 사용됩니다. APD의 SQL_DESC_ARRAY_STATUS_PTR 필드의 값이 null 포인터인 경우 모든 매개 변수 집합이 사용됩니다. 해석은 포인터가 유효한 배열을 가리키고 배열의 모든 요소가 SQL_PARAM_PROCEED 것과 같습니다.  
  
 APD의 이 필드는 SQL_ATTR_PARAM_OPERATION_PTR 특성을 가진 **SQLSetStmtAttr을** 호출하여 설정할 수도 있습니다.  
  
 **SQL_DESC_BIND_OFFSET_PTR [응용 프로그램 설명자]**  
 이 SQLLEN * 헤더 필드는 바인딩 오프셋을 가리킵니다. 기본적으로 null 포인터로 설정됩니다. 이 필드가 null 포인터가 아닌 경우 드라이버는 포인터를 참조하고 디코딩자 레코드(SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR)에 null이 아닌 값이 있는 각 지연된 필드에 역참조 값을 추가하고 바인딩할 때 새 포인터 값을 사용합니다.  
  
 바인딩 오프셋은 항상 SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR 필드의 값에 직접 추가됩니다. 오프셋이 다른 값으로 변경된 경우에도 새 값은 각 설명자 필드의 값에 직접 추가됩니다. 새 오프셋은 필드 값에 이전 오프셋을 더한 값에 추가되지 않습니다.  
  
 이 필드는 *지연된 필드입니다:* 설정된 시간에 사용되지 않지만 데이터 버퍼의 주소를 결정해야 할 때 드라이버가 나중에 사용합니다.  
  
 ARD의 이 필드는 SQL_ATTR_ROW_BIND_OFFSET_PTR 특성을 가진 **SQLSetStmtAttr을** 호출하여 설정할 수도 있습니다. ARD의 이 필드는 **sqlSetStmtAttr을** SQL_ATTR_PARAM_BIND_OFFSET_PTR 특성으로 호출하여 설정할 수도 있습니다.  
  
 자세한 내용은 [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) 및 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)에서 행 별 바인딩에 대한 설명을 참조하십시오.  
  
 **SQL_DESC_BIND_TYPE [응용 프로그램 설명자]**  
 이 SQLUINTEGER 헤더 필드는 열 또는 매개 변수를 바인딩하는 데 사용할 바인딩 방향을 설정합니다.  
  
 ARD에서 이 필드는 연결된 명령문 핸들에서 **SQLFetchScroll** 또는 **SQLFetch가** 호출될 때 바인딩 방향을 지정합니다.  
  
 열에 대한 열별 바인딩을 선택하려면 이 필드는 SQL_BIND_BY_COLUMN(기본값)으로 설정됩니다.  
  
 ARD의 이 필드는 **sqlSetStmtAttr을** SQL_ATTR_ROW_BIND_TYPE *특성으로*호출하여 설정할 수도 있습니다.  
  
 APD에서 이 필드는 동적 매개 변수에 사용할 바인딩 방향을 지정합니다.  
  
 매개 변수에 대한 열 별 바인딩을 선택하려면 이 필드는 SQL_BIND_BY_COLUMN(기본값)으로 설정됩니다.  
  
 APD의 이 필드는 **sqlSetStmtAttr을** SQL_ATTR_PARAM_BIND_TYPE *특성으로*호출하여 설정할 수도 있습니다.  
  
 **SQL_DESC_COUNT [모두]**  
 이 SQLSMALLINT 헤더 필드는 데이터를 포함하는 가장 높은 번호의 레코드의 1기반 인덱스를 지정합니다. 드라이버가 설명자의 데이터 구조를 설정하는 경우 SQL_DESC_COUNT 필드를 설정하여 중요한 레코드 수를 표시해야 합니다. 응용 프로그램이 이 데이터 구조의 인스턴스를 할당하는 경우 공간을 예약할 레코드 수를 지정할 필요가 없습니다. 응용 프로그램이 레코드의 내용을 지정할 때 드라이버는 설명자 핸들이 적절한 크기의 데이터 구조를 참조하는지 확인하기 위해 필요한 작업을 수행합니다.  
  
 SQL_DESC_COUNT 필드가 ARD에 있는 경우 바인딩된 모든 데이터 열또는 바인딩된 모든 매개 변수(필드가 APD에 있는 경우)의 수가 아니라 번호가 가장 높은 레코드의 수입니다. 번호가 가장 많은 열 또는 매개 변수가 언바운드인 경우 SQL_DESC_COUNT 다음으로 번호가 매겨진 열 또는 매개 변수의 수로 변경됩니다. 번호가 가장 많은 열의 수보다 작은 열또는 매개 변수가 언바운드된 *경우(TargetValuePtr* 인수가 null 포인터로 설정된 **SQLBindCol을** 호출하거나, *ParameterValuePtr* 인수가 null 포인터로 설정된 **SQLBindParameter)SQL_DESC_COUNT** 변경되지 않습니다. 추가 열 또는 매개 변수가 데이터를 포함하는 가장 높은 번호의 레코드보다 큰 숫자로 바인딩된 경우 드라이버는 SQL_DESC_COUNT 필드의 값을 자동으로 증가시킵니다. SQL_UNBIND 옵션으로 **SQLFreeStmt를** 호출하여 모든 열이 언바운드된 경우 ARD 및 IRD의 SQL_DESC_COUNT 필드는 0으로 설정됩니다. **SQLFreeStmt가** SQL_RESET_PARAMS 옵션으로 호출되면 APD 및 IPD의 SQL_DESC_COUNT 필드가 0으로 설정됩니다.  
  
 SQL_DESC_COUNT 값은 **SQLSetDescField**를 호출하여 응용 프로그램에서 명시적으로 설정할 수 있습니다. SQL_DESC_COUNT 값이 명시적으로 감소하면 SQL_DESC_COUNT 새 값보다 큰 숫자가 있는 모든 레코드가 효과적으로 제거됩니다. SQL_DESC_COUNT 값이 명시적으로 0으로 설정되고 필드가 ARD에 있는 경우 바인딩된 책갈피 열을 제외한 모든 데이터 버퍼가 해제됩니다.  
  
 ARD의 이 필드의 레코드 수에는 바인딩된 책갈피 열이 포함되지 않습니다. 책갈피 열을 바인딩 해제하는 유일한 방법은 SQL_DESC_DATA_PTR 필드를 null 포인터로 설정하는 것입니다.  
  
 **SQL_DESC_ROWS_PROCESSED_PTR [구현 설명자]**  
 IRD에서 이 SQLULEN \* 헤더 필드는 **SQLFetch** 또는 **SQLFetchScroll**호출 후 가져온 행 수 또는 오류 행을 포함하여 **SQLBulkOperations** 또는 **SQLSetPos**호출에 의해 수행되는 대량 작업에서 영향을 받는 행 수를 포함하는 버퍼를 가리킵니다.  
  
 IPD에서 이 SQLUINTEGER * 헤더 필드는 오류 집합을 포함하여 처리된 매개 변수 집합 수를 포함하는 버퍼를 가리킵니다. null 포인터인 경우 번호가 반환되지 않습니다.  
  
 SQL_DESC_ROWS_PROCESSED_PTR **SQLFetch** 또는 **SQLFetchScroll(IRD** 필드의 경우) 또는 **SQLExecute,** **SQLExecDirect**또는 **SQLParamData(IPD** 필드의 경우)를 호출한 후 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO 반환된 후에만 유효합니다. 이 필드가 가리키는 버퍼를 채우는 호출이 SQL_SUCCESS 반환되지 않거나 SQL_SUCCESS_WITH_INFO 경우 버퍼의 내용은 SQL_NO_DATA 반환하지 않는 한 정의되지 않습니다.이 경우 버퍼의 값은 0으로 설정됩니다.  
  
 ARD의 이 필드는 **sqlSetStmtAttr을** SQL_ATTR_ROWS_FETCHED_PTR 특성으로 호출하여 설정할 수도 있습니다. APD의 이 필드는 SQL_ATTR_PARAMS_PROCESSED_PTR 특성을 가진 **SQLSetStmtAttr을** 호출하여 설정할 수도 있습니다.  
  
 이 필드가 가리키는 버퍼는 응용 프로그램에서 할당됩니다. 드라이버에 의해 설정된 지연된 출력 버퍼입니다. 기본적으로 null 포인터로 설정됩니다.  
  
## <a name="record-fields"></a>레코드 필드  
 각 설명자는 설명자의 유형에 따라 열 데이터 또는 동적 매개 변수를 정의하는 필드로 구성된 하나 이상의 레코드를 포함합니다. 각 레코드는 단일 열 또는 매개 변수의 전체 정의입니다.  
  
 **SQL_DESC_AUTO_UNIQUE_VALUE [IrDs]**  
 이 읽기 전용 SQLINTEGER 레코드 필드에는 열이 자동 증분 열인 경우 SQL_TRUE 포함하거나 열이 자동 증분 열이 아닌 경우 SQL_FALSE 포함됩니다. 이 필드는 읽기 전용이지만 기본 자동 증분 열이 반드시 읽기 전용이 되는 것은 아닙니다.  
  
 **SQL_DESC_BASE_COLUMN_NAME [IRD]**  
 이 읽기 전용 SQLCHAR * 레코드 필드에는 결과 집합 열의 기본 열 이름이 포함되어 있습니다. 식인 열의 경우와 같이 기준 열 이름이 없는 경우 이 변수에는 빈 문자열이 포함됩니다.  
  
 **SQL_DESC_BASE_TABLE_NAME [IRD]**  
 이 읽기 전용 SQLCHAR * 레코드 필드에는 결과 집합 열의 기본 테이블 이름이 포함되어 있습니다. 기본 테이블 이름을 정의할 수 없거나 적용할 수 없는 경우 이 변수에는 빈 문자열이 포함됩니다.  
  
 **SQL_DESC_CASE_SENSITIVE [구현 설명자]**  
 이 읽기 전용 SQLINTEGER 레코드 필드에 SQL_TRUE는 열 또는 매개 변수가 데이터 정렬 및 비교에 대/소문자 구분으로 처리되는 경우 또는 컬럼이 데이터 정렬 및 비교에 대/소문자를 구분하지 않거나 문자가 아닌 열인 경우 SQL_FALSE 포함됩니다.  
  
 **SQL_DESC_CATALOG_NAME [IrD]**  
 이 읽기 전용 SQLCHAR * 레코드 필드에는 열이 포함된 기본 테이블에 대한 카탈로그가 포함되어 있습니다. 반환 값은 열이 식이거나 열이 뷰의 일부인 경우 드라이버에 따라 다릅니다. 데이터 원본이 카탈로그를 지원하지 않거나 카탈로그를 확인할 수 없는 경우 이 변수에는 빈 문자열이 포함됩니다.  
  
 **SQL_DESC_CONCISE_TYPE [모두]**  
 이 SQLSMALLINT 헤더 필드는 날짜 시간 및 간격 데이터 형식을 포함하여 모든 데이터 형식에 대한 간결한 데이터 형식을 지정합니다.  
  
 SQL_DESC_CONCISE_TYPE, SQL_DESC_TYPE 및 SQL_DESC_DATETIME_INTERVAL_CODE 필드의 값은 상호 의존적입니다. 필드 중 하나가 설정될 때마다 다른 필드도 설정해야 합니다. SQL_DESC_CONCISE_TYPE **SQLBindCol** 또는 **SQLBind매개 변수**또는 **SQLSetDescField에**대한 호출로 설정할 수 있습니다. SQL_DESC_TYPE **SQLSetDescField 또는 SQLSetDescRec에** 대한 호출로 설정할 수 있습니다. **SQLSetDescRec**  
  
 SQL_DESC_CONCISE_TYPE 간격 또는 날짜 시간 데이터 형식 이 아닌 간결한 데이터 유형으로 설정되면 SQL_DESC_TYPE 필드가 동일한 값으로 설정되고 SQL_DESC_DATETIME_INTERVAL_CODE 필드가 0으로 설정됩니다.  
  
 SQL_DESC_CONCISE_TYPE 간결한 datetime 또는 간격 데이터 유형으로 설정되면 SQL_DESC_TYPE 필드는 해당 자세한 형식(SQL_DATETIME 또는 SQL_INTERVAL)으로 설정되고 SQL_DESC_DATETIME_INTERVAL_CODE 필드는 해당 하위 코드로 설정됩니다.  
  
 **SQL_DESC_DATA_PTR [응용 프로그램 설명자 및 IPD]**  
 이 SQLPOINTER 레코드 필드는 매개 변수 값(APD의 경우) 또는 열 값(ARD의 경우)을 포함하는 변수를 가리킵니다. 이 필드는 *지연된 필드입니다.* 설정된 시간에는 사용되지 않지만 나중에 드라이버가 데이터를 검색하는 데 사용됩니다.  
  
 ARD의 SQL_DESC_DATA_PTR 필드에 의해 지정 된 열은 UN바운드 **SQLBindCol에** 대 한 호출에서 *TargetValuePtr* 인수 null 포인터 또는 ARD의 SQL_DESC_DATA_PTR 필드 **가 SQLSetDescField** 또는 **SQLSetDescRec에** 대 한 호출에 의해 설정 되는 경우 null 포인터입니다. SQL_DESC_DATA_PTR 필드가 null 포인터로 설정된 경우 다른 필드는 영향을 받지 않습니다.  
  
 이 필드가 가리키는 버퍼를 채우는 **SQLFetch** 또는 **SQLFetchScroll** 호출이 SQL_SUCCESS 반환되지 않거나 SQL_SUCCESS_WITH_INFO 경우 버퍼의 내용은 정의되지 않습니다.  
  
 APD, ARD 또는 IPD의 SQL_DESC_DATA_PTR 필드가 설정될 때마다 드라이버는 SQL_DESC_TYPE 필드의 값에 유효한 ODBC C 데이터 형식 또는 드라이버 관련 데이터 형식 중 하나가 포함되어 있는지, 데이터 형식에 영향을 미치는 다른 모든 필드가 일치하는지 확인합니다. 일관성 검사를 묻는 메시지가 IPD의 SQL_DESC_DATA_PTR 필드를 사용하는 것만 사용하는 것입니다. 특히 응용 프로그램이 IPD의 SQL_DESC_DATA_PTR 필드를 설정하고 나중에 이 필드에서 **SQLGetDescField를** 호출하는 경우 설정한 값을 반드시 반환할 필요는 없습니다. 자세한 내용은 [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)의 "일관성 검사"를 참조하십시오.  
  
 **SQL_DESC_DATETIME_INTERVAL_CODE [모두]**  
 이 SQLSMALLINT 레코드 필드에는 SQL_DESC_TYPE 필드가 SQL_DATETIME 또는 SQL_INTERVAL 특정 날짜 시간 또는 간격 데이터 형식에 대한 하위 코드가 포함되어 있습니다. 이는 SQL 및 C 데이터 형식 모두에 해당됩니다. 코드는 "TYPE" 또는 "C_TYPE"(datetime 형식의 경우) 또는 "INTERVAL" 또는 "C_INTERVAL"(간격 형식의 경우)으로 대체된 "CODE"로 데이터 형식 이름으로 구성됩니다.  
  
 응용 프로그램 설명자의 SQL_DESC_TYPE 및 SQL_DESC_CONCISE_TYPE SQL_C_DEFAULT 설정되어 있고 설명자가 문 핸들과 연결되지 않은 경우 SQL_DESC_DATETIME_INTERVAL_CODE 내용은 정의되지 않습니다.  
  
 이 필드는 다음 표에 나열된 날짜 시간 데이터 형식에 대해 설정할 수 있습니다.  
  
|일시 적 유형|DATETIME_INTERVAL_CODE|  
|--------------------|------------------------------|  
|SQL_TYPE_DATE/SQL_C_TYPE_DATE|SQL_CODE_DATE|  
|SQL_TYPE_TIME/SQL_C_TYPE_TIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP/ SQL_C_TYPE_TIMESTAMP|SQL_CODE_TIMESTAMP|  
  
 이 필드는 다음 표에 나열된 간격 데이터 형식에 대해 설정할 수 있습니다.  
  
|간격 유형|DATETIME_INTERVAL_CODE|  
|-------------------|------------------------------|  
|SQL_INTERVAL_DAY/SQL_C_INTERVAL_DAY|SQL_CODE_DAY|  
|SQL_INTERVAL_DAY_TO_HOUR/SQL_C_INTERVAL_DAY_TO_HOUR|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE/SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_CODE_DAY_TO_MINUTE|  
|SQL_INTERVAL_DAY_TO_SECOND/ SQL_C_INTERVAL_DAY_TO_SECOND|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR/ SQL_C_INTERVAL_HOUR|SQL_CODE_HOUR|  
|SQL_INTERVAL_HOUR_TO_MINUTE/ SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND/ SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE/SQL_C_INTERVAL_MINUTE|SQL_CODE_MINUTE|  
|SQL_INTERVAL_MINUTE_TO_SECOND/SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_CODE_MINUTE_TO_SECOND|  
|SQL_INTERVAL_MONTH/ SQL_C_INTERVAL_MONTH|SQL_CODE_MONTH|  
|SQL_INTERVAL_SECOND/SQL_C_INTERVAL_SECOND|SQL_CODE_SECOND|  
|SQL_INTERVAL_YEAR/ SQL_C_INTERVAL_YEAR|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH/SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_CODE_YEAR_TO_MONTH|  
  
 데이터 간격 및 이 필드에 대한 자세한 내용은 [데이터 유형 식별자 및 설명자를](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)참조하십시오.  
  
 **SQL_DESC_DATETIME_INTERVAL_PRECISION [모두]**  
 이 SQLINTEGER 레코드 필드에는 SQL_DESC_TYPE 필드가 SQL_INTERVAL 경우 정밀도를 선도하는 간격이 포함됩니다. SQL_DESC_DATETIME_INTERVAL_CODE 필드가 간격 데이터 유형으로 설정되면 이 필드는 정밀도를 선도하는 기본 간격으로 설정됩니다.  
  
 **SQL_DESC_DISPLAY_SIZE [IrD]**  
 이 읽기 전용 SQLINTEGER 레코드 필드에는 열의 데이터를 표시하는 데 필요한 최대 문자 수가 포함됩니다.  
  
 **SQL_DESC_FIXED_PREC_SCALE [구현 설명자]**  
 이 읽기 전용 SQLSMALLINT 레코드 필드는 열이 정확한 숫자 열이고 고정 정밀도 및 영해 축척이 있는 경우 SQL_TRUE 또는 열이 고정된 정밀도와 배율이 있는 정확한 숫자 열이 아닌 경우 SQL_FALSE 설정됩니다.  
  
 **SQL_DESC_INDICATOR_PTR [응용 프로그램 설명자]**  
 ARD에서 이 SQLLEN * 레코드 필드는 표시기 변수를 가리킵니다. 이 변수에는 열 값이 NULL인 경우 SQL_NULL_DATA 포함됩니다. APD의 경우 표시기 변수가 null 동적 인수를 지정하도록 SQL_NULL_DATA 설정됩니다. 그렇지 않으면 변수가 0입니다(SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR 값이 동일한 포인터가 아니면).  
  
 ARD의 SQL_DESC_INDICATOR_PTR 필드가 null 포인터인 경우 드라이버는 열이 NULL인지 여부에 대한 정보를 반환하지 않습니다. 열이 null이고 SQL_DESC_INDICATOR_PTR null 포인터인 경우 SQLSTATE 22002(필수하지만 제공되지 않은 표시기 변수)는 드라이버가 **SQLFetch** 또는 **SQLFetchScroll**를 호출한 후 버퍼를 채우려고 할 때 반환됩니다. **SQLFetch** 또는 **SQLFetchScroll에** 대한 호출이 SQL_SUCCESS 반환되지 않거나 SQL_SUCCESS_WITH_INFO 경우 버퍼의 내용은 정의되지 않습니다.  
  
 SQL_DESC_INDICATOR_PTR 필드는 SQL_DESC_OCTET_LENGTH_PTR 가리키는 필드가 설정되어 있는지 여부를 결정합니다. 열의 데이터 값이 NULL이면 드라이버는 표시기 변수를 SQL_NULL_DATA 설정합니다. SQL_DESC_OCTET_LENGTH_PTR 가리키는 필드는 설정되지 않습니다. FETCH 중에 NULL 값이 발생하지 않으면 SQL_DESC_INDICATOR_PTR 가리키는 버퍼가 0으로 설정되고 SQL_DESC_OCTET_LENGTH_PTR 가리키는 버퍼가 데이터 길이로 설정됩니다.  
  
 APD의 SQL_DESC_INDICATOR_PTR 필드가 null 포인터인 경우 응용 프로그램은 이 설명자 레코드를 사용하여 NULL 인수를 지정할 수 없습니다.  
  
 이 필드는 *지연된 필드입니다:* 설정 시 사용되지 않지만 나중에 드라이버가 null가능성을 나타내거나(ARD의 경우) null가능성을 결정하는 데 사용됩니다(APD의 경우).  
  
 **SQL_DESC_LABEL [IrD]**  
 이 읽기 전용 SQLCHAR * 레코드 필드에는 열 레이블 또는 제목이 포함되어 있습니다. 열에 레이블이 없는 경우 이 변수에는 열 이름이 포함됩니다. 열의 이름이 지정되지 않고 레이블이 지정되지 않은 경우 이 변수에는 빈 문자열이 포함됩니다.  
  
 **SQL_DESC_LENGTH [모두]**  
 이 SQLULEN 레코드 필드는 문자 문자열의 최대 또는 실제 길이 또는 바이트의 이진 데이터 형식입니다. 고정 길이 데이터 형식의 최대 길이 또는 가변 길이 데이터 형식의 실제 길이입니다. 이 값은 항상 문자 문자열을 종료하는 null-termination 문자를 제외합니다. 형식이 SQL_TYPE_DATE 값, SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP 또는 SQL 간격 데이터 형식 중 하나인 값의 경우 이 필드에는 날짜 시간 또는 간격 값의 문자 문자열 표현 길이가 있습니다.  
  
 이 필드의 값은 ODBC 2 *.x에*정의된 "길이"의 값과 다를 수 있습니다. 자세한 내용은 [부록 D: 데이터 유형을](../../../odbc/reference/appendixes/appendix-d-data-types.md)참조하십시오.  
  
 **SQL_DESC_LITERAL_PREFIX [IrD]**  
 이 읽기 전용 SQLCHAR * 레코드 필드에는 드라이버가 이 데이터 형식의 리터럴에 대한 접두사로 인식하는 문자 나 문자가 포함되어 있습니다. 이 변수에는 리터럴 접두사를 적용할 수 없는 데이터 형식에 대한 빈 문자열이 포함되어 있습니다.  
  
 **SQL_DESC_LITERAL_SUFFIX [IrD]**  
 이 읽기 전용 SQLCHAR * 레코드 필드에는 드라이버가 이 데이터 형식의 리터럴에 대한 접미사로 인식하는 문자 또는 문자가 포함되어 있습니다. 이 변수에는 리터럴 접미사를 적용할 수 없는 데이터 형식에 대한 빈 문자열이 포함되어 있습니다.  
  
 **SQL_DESC_LOCAL_TYPE_NAME [구현 설명자]**  
 이 읽기 전용 SQLCHAR * 레코드 필드에는 데이터 형식의 일반 이름과 다를 수 있는 데이터 형식에 대한 지역화된(기본 언어) 이름이 포함되어 있습니다. 지역화된 이름이 없는 경우 빈 문자열이 반환됩니다. 이 필드는 표시용도로만 사용됩니다.  
  
 **SQL_DESC_NAME [구현 설명자]**  
 행 설명자의 이 SQLCHAR * 레코드 필드에는 적용되는 경우 열 별칭이 포함되어 있습니다. 열 별칭이 적용되지 않으면 열 이름이 반환됩니다. 두 경우 모두 드라이버는 SQL_DESC_NAME 필드를 설정할 때 SQL_NAMED SQL_DESC_UNNAMED 필드를 설정합니다. 열 이름이나 열 별칭이 없는 경우 드라이버는 SQL_DESC_NAME 필드에 빈 문자열을 반환하고 SQL_DESC_UNNAMED 필드를 SQL_UNNAMED 설정합니다.  
  
 응용 프로그램은 IPD의 SQL_DESC_NAME 필드를 매개 변수 이름 또는 별칭으로 설정하여 저장 프로시저 매개 변수를 이름으로 지정할 수 있습니다. (자세한 내용은 [이름으로 바인딩 매개 변수(명명된 매개 변수)를](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)참조하십시오.) IRD의 SQL_DESC_NAME 필드는 읽기 전용 필드입니다. SQLSTATE HY091(잘못된 설명자 필드 식별자)은 응용 프로그램이 설정하려고 하면 반환됩니다.  
  
 IPD에서 드라이버가 명명된 매개 변수를 지원하지 않는 경우 이 필드는 정의되지 않습니다. 드라이버가 명명된 매개 변수를 지원하고 매개 변수를 설명할 수 있는 경우 매개 변수 이름이 이 필드에 반환됩니다.  
  
 **SQL_DESC_NULLABLE [구현 설명자]**  
 IRD에서 이 읽기 전용 SQLSMALLINT 레코드 필드는 열에 NULL 값이 있을 수 있는 경우, SQL_NO_NULLS 열에 NULL 값이 없는 경우 또는 열이 NULL 값을 허용하는지 여부를 알 수 없는 경우 SQL_NULLABLE_UNKNOWN SQL_NULLABLE. 이 필드는 기준 열이 아닌 결과 집합 열과 관련이 있습니다.  
  
 IPD에서 동적 매개 변수는 항상 null 수 있고 응용 프로그램에서 설정할 수 없기 때문에 이 필드는 항상 SQL_NULLABLE 설정됩니다.  
  
 **SQL_DESC_NUM_PREC_RADIX [모두]**  
 이 SQLINTEGER 필드에는 SQL_DESC_TYPE 필드의 데이터 형식이 대략적인 숫자 데이터 형식인 경우 SQL_DESC_PRECISION 필드에 비트 수가 포함되어 있으므로 값이 2입니다. SQL_DESC_PRECISION 필드에 소수 자릿수가 포함되어 있으므로 SQL_DESC_TYPE 필드의 데이터 형식이 정확한 숫자 데이터 형식인 경우 이 필드에는 10의 값이 포함됩니다. 이 필드는 숫자가 아닌 모든 데이터 형식에 대해 0으로 설정됩니다.  
  
 **SQL_DESC_OCTET_LENGTH [모두]**  
 이 SQLLEN 레코드 필드에는 문자열 문자열 또는 이진 데이터 형식의 길이(바이트)가 포함됩니다. 고정 길이 문자 또는 이진 형식의 경우 실제 길이는 바이트입니다. 가변 길이 문자 또는 이진 형식의 경우 이 값은 바이트의 최대 길이입니다. 이 값은 항상 구현 설명자에 대 한 null 종료 문자에 대 한 공간을 제외 하 고 항상 응용 프로그램 설명자에 대 한 null 종료 문자에 대 한 공간을 포함 합니다. 응용 프로그램 데이터의 경우 이 필드에는 버퍼의 크기가 포함됩니다. APD의 경우 이 필드는 출력 또는 입력/출력 매개 변수에 대해서만 정의됩니다.  
  
 **SQL_DESC_OCTET_LENGTH_PTR [응용 프로그램 설명자]**  
 이 SQLLEN * 레코드 필드는 동적 인수의 바이트(매개 변수 설명자) 또는 바인딩된 열 값(행 설명자의 경우)의 총 길이를 포함하는 변수를 가리킵니다.  
  
 APD의 경우 이 값은 문자 문자열과 바이너리를 제외한 모든 인수에 대해 무시됩니다. 이 필드가 SQL_NTS 가리키는 경우 동적 인수는 null-종료되어야 합니다. 바인딩된 매개 변수가 실행 시 데이터 매개 변수임을 나타내기 위해 응용 프로그램은 APD의 적절한 레코드에서 이 필드를 실행 시 SQL_DATA_AT_EXEC 값 또는 SQL_LEN_DATA_AT_EXEC 매크로의 결과를 포함하는 변수로 설정합니다. 이러한 필드가 두 개 이상 있는 경우 SQL_DESC_DATA_PTR 응용 프로그램에서 요청되는 매개 변수를 결정하는 데 도움이 되는 매개 변수를 고유하게 식별하는 값으로 설정할 수 있습니다.  
  
 ARD의 OCTET_LENGTH_PTR 필드가 null 포인터인 경우 드라이버는 열에 대한 길이 정보를 반환하지 않습니다. APD의 SQL_DESC_OCTET_LENGTH_PTR 필드가 null 포인터인 경우 드라이버는 문자 문자열과 이진 값이 null-terminated라고 가정합니다. (이진 값은 null-terminated되지 않아야 하지만 잘림을 피하기 위해 길이를 부여해야 합니다.)  
  
 이 필드가 가리키는 버퍼를 채우는 **SQLFetch** 또는 **SQLFetchScroll** 호출이 SQL_SUCCESS 반환되지 않거나 SQL_SUCCESS_WITH_INFO 경우 버퍼의 내용은 정의되지 않습니다. 이 필드는 *지연된 필드입니다.* 설정된 시간에는 사용되지 않지만 나중에 드라이버가 데이터의 옥텟 길이를 결정하거나 나타내는 데 사용됩니다.  
  
 **SQL_DESC_PARAMETER_TYPE [IPD]**  
 이 SQLSMALLINT 레코드 필드는 입력 매개 변수에 대한 SQL_PARAM_INPUT, 입력/출력 매개 변수에 대한 SQL_PARAM_INPUT_OUTPUT, 출력 매개 변수에 대한 SQL_PARAM_OUTPUT, 입력/출력 스트리밍 매개변수에 대한 SQL_PARAM_INPUT_OUTPUT_STREAM 또는 출력 스트리밍 매개변수에 대한 SQL_PARAM_OUTPUT_STREAM 설정됩니다. 기본적으로 SQL_PARAM_INPUT 설정됩니다.  
  
 IPD의 경우 IPD가 드라이버에 의해 자동으로 채워지지 않으면 필드가 기본적으로 SQL_PARAM_INPUT 설정됩니다(SQL_ATTR_ENABLE_AUTO_IPD 문 특성은 SQL_FALSE). 응용 프로그램은 입력 매개 변수가 아닌 매개 변수에 대해 IPD에서 이 필드를 설정해야 합니다.  
  
 **SQL_DESC_PRECISION [모두]**  
 이 SQLSMALLINT 레코드 필드에는 정확한 숫자 형식의 자릿수, 대략적인 숫자 형식의 가사(이진 정밀도) 비트 수 또는 SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP 또는 SQL_INTERVAL_SECOND 데이터 형식의 분수 초 구성 요소의 숫자 수가 포함됩니다. 이 필드는 다른 모든 데이터 형식에 대해 정의되지 않습니다.  
  
 이 필드의 값은 ODBC 2 *.x에*정의된 "정밀도"에 대한 값과 다를 수 있습니다. 자세한 내용은 [부록 D: 데이터 유형을](../../../odbc/reference/appendixes/appendix-d-data-types.md)참조하십시오.  
  
 **SQL_DESC_ROWVER [구현 설명자]**  
 이 SQLSMALLINTrecord 필드는 행이 업데이트될 때 DBMS에서 열이 자동으로 수정되는지 여부를 나타냅니다(예: SQL Server의 "타임스탬프" 형식의 열). 이 레코드 필드의 값은 열이 행 버전 지정 열인 경우 SQL_TRUE 설정되고 그렇지 않으면 SQL_FALSE. 이 열 특성은 열이 자동으로 업데이트되는지 여부를 결정하기 위해 식별자유형 SQL_ROWVER **SQLSpecialColumns를** 호출하는 것과 유사합니다.  
  
 **SQL_DESC_SCALE [모두]**  
 이 SQLSMALLINT 레코드 필드에는 소수점 및 숫자 데이터 형식에 대해 정의된 축척이 포함되어 있습니다. 다른 모든 데이터 형식에 대해 필드가 정의되지 않습니다.  
  
 이 필드의 값은 ODBC 2 *.x에*정의된 "배율"의 값과 다를 수 있습니다. 자세한 내용은 [부록 D: 데이터 유형을](../../../odbc/reference/appendixes/appendix-d-data-types.md)참조하십시오.  
  
 **SQL_DESC_SCHEMA_NAME [IrD]**  
 이 읽기 전용 SQLCHAR * 레코드 필드에는 열이 포함된 기본 테이블의 스키마 이름이 포함되어 있습니다. 반환 값은 열이 식이거나 열이 뷰의 일부인 경우 드라이버에 따라 다릅니다. 데이터 원본이 스키마를 지원하지 않거나 스키마 이름을 확인할 수 없는 경우 이 변수에는 빈 문자열이 포함됩니다.  
  
 **SQL_DESC_SEARCHABLE [IrD]**  
 이 읽기 전용 SQLSMALLINT 레코드 필드는 다음 값 중 하나로 설정됩니다.  
  
-   **WHERE** 절에서 열을 사용할 수 없는 경우 SQL_PRED_NONE. (ODBC 2 *.x의*SQL_UNSEARCHABLE 값과 동일합니다.)  
  
-   SQL_PRED_CHAR **WHERE** 절에서 만 **LIKE** 조건자에서 열에 사용할 수 있습니다. (ODBC 2 *.x의*SQL_LIKE_ONLY 값과 동일합니다.)  
  
-   SQL_PRED_BASIC 열을 **LIKE를**제외한 모든 비교 연산자가 있는 **WHERE** 절에서 사용할 수 있는 경우를 (ODBC 2 *.x의*SQL_EXCEPT_LIKE 값과 동일합니다.)  
  
-   SQL_PRED_SEARCHABLE 비교 연산자가 있는 **WHERE** 절에서 열을 사용할 수 있는지 를 지정합니다.  
  
 **SQL_DESC_TABLE_NAME [IrD]**  
 이 읽기 전용 SQLCHAR * 레코드 필드에는 이 열이 포함된 기본 테이블의 이름이 포함되어 있습니다. 반환 값은 열이 식이거나 열이 뷰의 일부인 경우 드라이버에 따라 다릅니다.  
  
 **SQL_DESC_TYPE [모두]**  
 이 SQLSMALLINT 레코드 필드는 날짜 시간 및 간격 데이터 형식을 제외한 모든 데이터 형식에 대해 간결한 SQL 또는 C 데이터 형식을 지정합니다. datetime 및 간격 데이터 형식의 경우 이 필드는 SQL_DATETIME 또는 SQL_INTERVAL 자세한 데이터 형식을 지정합니다.  
  
 이 필드에 SQL_DATETIME 또는 SQL_INTERVAL 포함될 때마다 SQL_DESC_DATETIME_INTERVAL_CODE 필드에간결식 형식에 적합한 하위 코드가 포함되어야 합니다. datetime 데이터 형식의 경우 SQL_DESC_TYPE SQL_DATETIME 포함하고 SQL_DESC_DATETIME_INTERVAL_CODE 필드에는 특정 datetime 데이터 형식에 대한 하위 코드가 포함되어 있습니다. 간격 데이터 형식의 경우 SQL_DESC_TYPE SQL_INTERVAL 포함하고 SQL_DESC_DATETIME_INTERVAL_CODE 필드에는 특정 간격 데이터 형식에 대한 하위 코드가 포함됩니다.  
  
 SQL_DESC_TYPE 및 SQL_DESC_CONCISE_TYPE 필드의 값은 상호 의존적입니다. 필드 중 하나가 설정될 때마다 다른 필드도 설정해야 합니다. SQL_DESC_TYPE **SQLSetDescField 또는 SQLSetDescRec에** 대한 호출로 설정할 수 있습니다. **SQLSetDescRec** SQL_DESC_CONCISE_TYPE **SQLBindCol** 또는 **SQLBind매개 변수**또는 **SQLSetDescField에**대한 호출로 설정할 수 있습니다.  
  
 SQL_DESC_TYPE 간격 또는 날짜 시간 데이터 형식 이 아닌 간결한 데이터 유형으로 설정되면 SQL_DESC_CONCISE_TYPE 필드가 동일한 값으로 설정되고 SQL_DESC_DATETIME_INTERVAL_CODE 필드가 0으로 설정됩니다.  
  
 SQL_DESC_TYPE 자세한 날짜 시간 또는 간격 데이터 형식(SQL_DATETIME 또는 SQL_INTERVAL)으로 설정되고 SQL_DESC_DATETIME_INTERVAL_CODE 필드가 적절한 하위 코드로 설정되면 SQL_DESC_CONCISE TYPE 필드가 해당 간결한 유형으로 설정됩니다. 간결한 날짜 시간 또는 간격 형식 중 하나로 SQL_DESC_TYPE 설정하면 SQLSTATE HY021(일관되지 않은 설명자 정보)이 반환됩니다.  
  
 SQL_DESC_TYPE 필드를 **SQLBindCol,** **SQLBindParameter**또는 **SQLSetDescField에**대한 호출로 설정하면 아래 표와 같이 다음 기본값으로 설정됩니다. 동일한 레코드의 나머지 필드의 값은 정의되지 않습니다.  
  
|SQL_DESC_TYPE 값|암시적으로 설정된 다른 필드|  
|------------------------------|---------------------------------|  
|SQL_CHAR, SQL_VARCHAR, SQL_C_CHAR, SQL_C_VARCHAR|SQL_DESC_LENGTH 1로 설정됩니다. SQL_DESC_PRECISION 0으로 설정됩니다.|  
|SQL_DATETIME|SQL_DESC_DATETIME_INTERVAL_CODE SQL_CODE_DATE 또는 SQL_CODE_TIME 설정하면 SQL_DESC_PRECISION 0으로 설정됩니다. SQL_DESC_TIMESTAMP 설정하면 SQL_DESC_PRECISION 6으로 설정됩니다.|  
|SQL_DECIMAL, SQL_NUMERIC, SQL_C_NUMERIC|SQL_DESC_SCALE 0으로 설정됩니다. SQL_DESC_PRECISION 각 데이터 형식에 대한 구현 정의 정밀도로 설정됩니다.<br /><br /> SQL_C_NUMERIC 값을 수동으로 바인딩하는 방법에 대한 자세한 내용은 [SQL에서 C: 숫자를](../../../odbc/reference/appendixes/sql-to-c-numeric.md) 참조하십시오.|  
|SQL_FLOAT, SQL_C_FLOAT|SQL_DESC_PRECISION SQL_FLOAT 위해 구현 정의 기본 정밀도로 설정됩니다.|  
|SQL_INTERVAL|SQL_DESC_DATETIME_INTERVAL_CODE 간격 데이터 유형으로 설정되면 SQL_DESC_DATETIME_INTERVAL_PRECISION 2(정밀도를 선도하는 기본 간격)로 설정됩니다. 간격에 초 구성 요소가 있는 경우 SQL_DESC_PRECISION 6(기본 간격 초 정밀도)으로 설정됩니다.|  
  
 응용 프로그램이 **SQLSetDescField를** 호출하여 **SQLSetDescRec를**호출하는 대신 설명자의 필드를 설정하는 경우 응용 프로그램은 먼저 데이터 형식을 선언해야 합니다. 이 경우 이전 테이블에 표시된 다른 필드는 암시적으로 설정됩니다. 암시적으로 설정된 값 중 어느 값도 허용되지 않는 경우 응용 프로그램은 **SQLSetDescField** 또는 **SQLSetDescRec을** 호출하여 허용 되지 않는 값을 명시적으로 설정할 수 있습니다.  
  
 **SQL_DESC_TYPE_NAME [구현 설명자]**  
 이 읽기 전용 SQLCHAR * 레코드 필드에는 데이터 원본 종속 형식 이름(예: "CHAR", "VARCHAR" 등)이 포함되어 있습니다. 데이터 형식 이름을 알 수 없는 경우 이 변수에는 빈 문자열이 포함됩니다.  
  
 **SQL_DESC_UNNAMED [구현 설명자]**  
 행 설명자의 이 SQLSMALLINT 레코드 필드는 SQL_DESC_NAME 필드를 설정할 때 드라이버가 SQL_NAMED 또는 SQL_UNNAMED 설정합니다. SQL_DESC_NAME 필드에 열 별칭이 포함되어 있거나 열 별칭이 적용되지 않는 경우 드라이버는 SQL_DESC_UNNAMED 필드를 SQL_NAMED 설정합니다. 응용 프로그램이 IPD의 SQL_DESC_NAME 필드를 매개 변수 이름이나 별칭으로 설정하면 드라이버는 IPD의 SQL_DESC_UNNAMED 필드를 SQL_NAMED 설정합니다. 열 이름이나 열 별칭이 없는 경우 드라이버는 SQL_DESC_UNNAMED 필드를 SQL_UNNAMED 설정합니다.  
  
 응용 프로그램은 IPD의 SQL_DESC_UNNAMED 필드를 SQL_UNNAMED 설정할 수 있습니다. 응용 프로그램이 IPD의 SQL_DESC_UNNAMED 필드를 SQL_NAMED 설정하려고 하면 드라이버가 SQLSTATE HY091(잘못된 설명자 필드 식별자)을 반환합니다. IRD의 SQL_DESC_UNNAMED 필드는 읽기 전용입니다. SQLSTATE HY091(잘못된 설명자 필드 식별자)은 응용 프로그램이 설정하려고 하면 반환됩니다.  
  
 **SQL_DESC_UNSIGNED [구현 설명자]**  
 이 읽기 전용 SQLSMALLINT 레코드 필드는 열 형식이 서명되지 않았거나 숫자가 아닌 경우 SQL_TRUE 열 형식이 서명된 경우 SQL_FALSE 설정됩니다.  
  
 **SQL_DESC_UPDATABLE [IrDs]**  
 이 읽기 전용 SQLSMALLINT 레코드 필드는 다음 값 중 하나로 설정됩니다.  
  
-   결과 집합 열이 읽기 전용인지 SQL_ATTR_READ_ONLY.  
  
-   결과 집합 열이 읽기-쓰기인 경우 SQL_ATTR_WRITE.  
  
-   SQL_ATTR_READWRITE_UNKNOWN 결과 집합 열이 업데이터 인지 여부를 알 수 없는 경우입니다.  
  
 SQL_DESC_UPDATABLE 기준 테이블의 열이 아니라 결과 집합에서 열의 업데이터성을 설명합니다. 이 결과 집합 열의 기반이 되는 기본 테이블의 열의 업데이터성은 이 필드의 값과 다를 수 있습니다. 열이 업데이터인지 여부는 데이터 형식, 사용자 권한 및 결과 집합 자체의 정의를 기반으로 할 수 있습니다. 열이 업데이터 인지 여부가 명확하지 않은 경우 SQL_ATTR_READWRITE_UNKNOWN 반환해야 합니다.  
  
## <a name="consistency-checks"></a>일관성 검사  
 응용 프로그램이 ARD, APD 또는 IPD의 SQL_DESC_DATA_PTR 필드에 대한 값을 통과할 때마다 드라이버가 일관성 검사를 자동으로 수행합니다. 필드중 어느 것이라도 다른 필드와 일치하지 않는 경우 **SQLSetDescField는** SQLSTATE HY021(일관되지 않은 설명자 정보)을 반환합니다. 자세한 내용은 [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)의 "일관성 검사"를 참조하십시오.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|열 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|매개 변수 바인딩|[SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|설명자 필드 얻기|[SQLGetDescField 함수](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|여러 설명자 필드 얻기|[SQLGetDescRec 함수](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|여러 설명자 필드 설정|[SQLSetDescRec 함수](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)
