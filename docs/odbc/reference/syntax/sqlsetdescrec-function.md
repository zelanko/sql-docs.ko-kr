---
title: SQLSetDescRec 함수 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetDescRec
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetDescRec
helpviewer_keywords:
- SQLSetDescRec function [ODBC]
ms.assetid: bf55256c-7eb7-4e3f-97ef-b0fee09ba829
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b29879ff7635d6eb7d5a0f7489ff3994758d4a35
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299533"
---
# <a name="sqlsetdescrec-function"></a>SQLSetDescRec 함수
**규칙**  
 버전 출시: ODBC 3.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLSetDescRec** 함수는 열 또는 매개 변수 데이터에 바인딩된 데이터 형식 및 버퍼에 영향을 주는 여러 설명자 필드를 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLSetDescRec(  
      SQLHDESC      DescriptorHandle,  
      SQLSMALLINT   RecNumber,  
      SQLSMALLINT   Type,  
      SQLSMALLINT   SubType,  
      SQLLEN        Length,  
      SQLSMALLINT   Precision,  
      SQLSMALLINT   Scale,  
      SQLPOINTER    DataPtr,  
      SQLLEN *      StringLengthPtr,  
      SQLLEN *      IndicatorPtr);  
```  
  
## <a name="arguments"></a>인수  
 *DescriptorHandle*  
 [입력] 설명자 핸들입니다. IRD 핸들이 아니어야 합니다.  
  
 *RecNumber*  
 [입력] 설정할 필드를 포함하는 설명자 레코드를 나타냅니다. 설명자 레코드는 0에서 번호가 매겨지며 레코드 번호 0은 책갈피 레코드입니다. 이 인수는 0과 같거나 커야 합니다. *RecNumber가* SQL_DESC_COUNT 값보다 큰 경우 *SQL_DESC_COUNTis RecNumber*값으로 변경되었습니다.  
  
 *Type*  
 [입력] 설명자 레코드에 대한 SQL_DESC_TYPE 필드를 설정할 값입니다.  
  
 *하위*  
 [입력] 형식이 SQL_DATETIME 또는 SQL_INTERVAL 레코드의 경우 이 값은 SQL_DESC_DATETIME_INTERVAL_CODE 필드를 설정할 값입니다.  
  
 *길이*  
 [입력] 설명자 레코드에 대한 SQL_DESC_OCTET_LENGTH 필드를 설정할 값입니다.  
  
 *전체 자릿수*  
 [입력] 설명자 레코드에 대한 SQL_DESC_PRECISION 필드를 설정할 값입니다.  
  
 *확장*  
 [입력] 설명자 레코드에 대한 SQL_DESC_SCALE 필드를 설정할 값입니다.  
  
 *데이터 Ptr*  
 [지연된 입력 또는 출력] 설명자 레코드에 대한 SQL_DESC_DATA_PTR 필드를 설정할 값입니다. *DataPtr은* null 포인터로 설정할 수 있습니다.  
  
 *DataPtr* 인수를 null 포인터로 설정하여 SQL_DESC_DATA_PTR 필드를 null 포인터로 설정할 수 있습니다. *설명자핸들* 인수의 핸들이 ARD와 연결되어 있으면 열이 바인딩해제됩니다.  
  
 *문자열길이Ptr*  
 [지연된 입력 또는 출력] 설명자 레코드에 대한 SQL_DESC_OCTET_LENGTH_PTR 필드를 설정할 값입니다. *StringLengthPtr은* null 포인터로 설정하여 SQL_DESC_OCTET_LENGTH_PTR 필드를 null 포인터로 설정할 수 있습니다.  
  
 *인디케이터Ptr*  
 [지연된 입력 또는 출력] 설명자 레코드에 대한 SQL_DESC_INDICATOR_PTR 필드를 설정할 값입니다. *IndicatorPtr은* null 포인터로 설정하여 SQL_DESC_INDICATOR_PTR 필드를 null 포인터로 설정할 수 있습니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLSetDescRec** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환하는 *경우,* SQL_HANDLE_DESC 핸들 유형 및 *설명자 핸들*핸들을 사용하는 *Handle* **SQLGetDiagRec을** 호출하여 연결된 SQLSTATE 값을 가져올 수 있습니다. 다음 표에서는 **SQLSetDescRec에서** 일반적으로 반환되는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|07009|잘못된 설명자 인덱스|*RecNumber* 인수가 0으로 설정되었고 *설명자 핸들이* IPD 핸들을 참조했습니다.<br /><br /> *RecNumber* 인수가 0보다 적습니다.<br /><br /> *RecNumber* 인수는 데이터 원본이 지원할 수 있는 최대 열 또는 매개 변수 수보다 크고 *설명자핸들* 인수는 APD, IPD 또는 ARD입니다.<br /><br /> *RecNumber* 인수는 0이고 *설명자핸들* 인수는 암시적으로 할당된 APD를 참조했습니다. 이 오류는 명시적으로 할당된 응용 프로그램 설명자가 실행 시간까지 APD 또는 ARD인지 여부를 알 수 없기 때문에 명시적으로 할당된 응용 프로그램 설명자에서 발생하지 않습니다.|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결된 데이터 원본 간의 통신 링크가 실패했습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류|(DM) *설명자 핸들은* 비동기적으로 실행 되는 함수 (이 되지 않음)를 호출 하 고이 함수를 호출 할 때 여전히 실행 되 고 있는 *StatementHandle와* 연결 되었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *설명자 핸들이* 연결되고 SQL_NEED_DATA 반환되는 *문 핸들에* 대해 호출되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.<br /><br /> (DM) *설명자 핸들과*연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. **SQLSetDescRec** 함수가 호출될 때 이 아인크로너스 함수는 여전히 실행 중이었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *설명자 핸들과* 연결된 명령문 핸들 중 하나를 호출하고 SQL_PARAM_DATA_AVAILABLE 반환되었습니다. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY016|구현 행 설명자 수정할 수 없습니다.|*설명자핸들* 인수가 IRD와 연결되었습니다.|  
|HY021|일관되지 않은 설명자 정보|*설명자의 SQL_DESC_TYPE* 필드와 연결된 Type 필드 또는 다른 필드가 유효하지 않거나 일치하지 않았습니다.<br /><br /> 일관성 검사 중에 확인된 설명자 정보가 일치하지 않았습니다. (이 섹션의 후반부에서 "일관성 검사"를 참조하십시오.)|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|(DM) 드라이버가 ODBC *2.x* 드라이버이고, 설명자가 ARD이고, *ColumnNumber* 인수가 0으로 설정되었으며, *인수 BufferLength에* 대해 지정된 값이 4와 같지 않았습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *설명자핸들과* 연결된 드라이버는 기능을 지원하지 않습니다.|  
  
## <a name="comments"></a>주석  
 응용 프로그램은 **SQLSetDescRec를** 호출하여 단일 열 또는 매개 변수에 대해 다음 필드를 설정할 수 있습니다.  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE(형식이 SQL_DATETIME 또는 SQL_INTERVAL 레코드의 경우)  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_DATA_PTR  
  
-   SQL_DESC_OCTET_LENGTH_PTR  
  
-   SQL_DESC_INDICATOR_PTR  
  
> [!NOTE]  
>  **SQLSetDescRec에** 대한 호출이 실패하면 *RecNumber* 인수로 식별된 설명자 레코드의 내용은 정의되지 않습니다.  
  
 열 또는 매개 변수를 바인딩할 때 **SQLSetDescRec를** 사용하면 **SQLBindCol** 또는 **SQLBindParameter를** 호출하거나 **SQLSetDescField를**여러 번 호출하지 않고 바인딩에 영향을 주는 여러 필드를 변경할 수 있습니다. **SQLSetDescRec는** 현재 문과 연결되지 않은 설명자에서 필드를 설정할 수 있습니다. **SQLBindParameter는** **SQLSetDescRec보다**더 많은 필드를 설정하고 APD와 IPD 모두에서 한 번의 호출로 필드를 설정할 수 있으며 설명자 핸들이 필요하지 않습니다.  
  
> [!NOTE]  
>  SQL_ATTR_USE_BOOKMARKS 문 특성은 책갈피 필드를 설정하려면 *RecNumber* 인수를 0으로 **사용하여 SQLSetDescRec를** 호출하기 전에 항상 설정해야 합니다. 필수는 아니지만 강력히 권장됩니다.  
  
## <a name="consistency-checks"></a>일관성 검사  
 응용 프로그램이 APD, ARD 또는 IPD의 SQL_DESC_DATA_PTR 필드를 설정할 때마다 드라이버가 일관성 검사를 자동으로 수행합니다. 필드가 다른 필드와 일치하지 않으면 **SQLSetDescRec는 SQLSTATE** HY021(일관되지 않은 설명자 정보)을 반환합니다.  
  
 응용 프로그램이 APD, ARD 또는 IPD의 SQL_DESC_DATA_PTR 필드를 설정할 때마다 드라이버는 SQL_DESC_TYPE 필드의 값과 해당 SQL_DESC_TYPE 필드에 적용되는 값이 유효하고 일관적이지 확인합니다. 이 검사는 **SQLBindParameter** 또는 **SQLBindCol이** 호출되거나 **SQLSetDescRec가** APD, ARD 또는 IPD에 대해 호출될 때 항상 수행됩니다. 이 일관성 검사에는 설명자 필드에 대한 다음 검사가 포함됩니다.  
  
-   SQL_DESC_TYPE 필드는 유효한 ODBC C 또는 SQL 형식 또는 드라이버 별 SQL 유형 중 하나여야 합니다. SQL_DESC_CONCISE_TYPE 필드는 유효한 ODBC C 또는 SQL 형식 또는 간결한 datetime 및 간격 형식을 포함하여 드라이버별 C 또는 SQL 유형 중 하나여야 합니다.  
  
-   SQL_DESC_TYPE 레코드 필드가 SQL_DATETIME 또는 SQL_INTERVAL 경우 SQL_DESC_DATETIME_INTERVAL_CODE 필드는 유효한 날짜 시간 또는 간격 코드 중 하나여야 합니다. [(SQLSetDescField에서](../../../odbc/reference/syntax/sqlsetdescfield-function.md)SQL_DESC_DATETIME_INTERVAL_CODE 필드에 대한 설명을 참조하십시오.)  
  
-   SQL_DESC_TYPE 필드가 숫자 형식을 나타내면 SQL_DESC_PRECISION 및 SQL_DESC_SCALE 필드가 유효한지 확인합니다.  
  
-   SQL_DESC_CONCISE_TYPE 필드가 시간 또는 타임스탬프 데이터 형식, 초 구성 요소가 있는 간격 형식 또는 시간 구성 요소가 있는 간격 데이터 형식인 경우 SQL_DESC_PRECISION 필드는 유효한 초 정밀도로 확인됩니다.  
  
-   SQL_DESC_CONCISE_TYPE 간격 데이터 형식인 경우 SQL_DESC_DATETIME_INTERVAL_PRECISION 필드는 정밀도 값을 선도하는 유효한 간격으로 확인됩니다.  
  
 IPD의 SQL_DESC_DATA_PTR 필드는 일반적으로 설정되지 않습니다. 그러나 응용 프로그램은 IPD 필드의 일관성 검사를 강제로 수행할 수 있습니다. IRD에서 일관성 검사를 수행할 수 없습니다. IPD의 SQL_DESC_DATA_PTR 필드가 실제로 저장되지 않으며 **SQLGetDescField** 또는 **SQLGetDescRec에**대한 호출로 검색할 수 없습니다. 이 설정은 일관성 검사를 강제로 하기 위해서만 만들어집니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|열 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|매개 변수 바인딩|[SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|단일 설명자 필드 얻기|[SQLGetDescField 함수](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|여러 설명자 필드 얻기|[SQLGetDescRec 함수](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|단일 설명자 필드 설정|[SQLSetDesc필드 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
