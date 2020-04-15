---
title: SQLGetDesc필드 기능 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 89972d7f36b436868cc8e243b03827f095b90492
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285478"
---
# <a name="sqlgetdescfield-function"></a>SQLGetDescField 함수(SQLGetDescField Function)
**규칙**  
 버전 출시: ODBC 3.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLGetDescField는** 설명자 레코드의 단일 필드의 현재 설정 또는 값을 반환합니다.  
  
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
 [입력] 응용 프로그램이 정보를 검색하는 설명자 레코드를 나타냅니다. 설명자 레코드는 0에서 번호가 매겨지며 레코드 번호 0은 책갈피 레코드입니다. *FieldIdentifier* 인수가 헤더 필드를 나타내는 경우 *RecNumber는* 무시됩니다. *RecNumber가* SQL_DESC_COUNT 작거나 같지만 행에 열 또는 매개 변수에 대한 데이터가 없는 경우 **SQLGetDescField를** 호출하면 필드의 기본값이 반환됩니다. 자세한 내용은 [SQLSetDescField의](../../../odbc/reference/syntax/sqlsetdescfield-function.md)"설명자 필드의 초기화"를 참조하십시오.  
  
 *FieldIdentifier*  
 [입력] 값을 반환할 설명자의 필드를 나타냅니다. 자세한 내용은 [SQLSetDescField의](../../../odbc/reference/syntax/sqlsetdescfield-function.md)*"필드 식별자* 인수" 섹션을 참조하십시오.  
  
 *ValuePtr*  
 [출력] 설명자 정보를 반환할 버퍼에 대한 포인터입니다. 데이터 형식은 *FieldIdentifier*의 값에 따라 달라집니다.  
  
 *ValuePtr이* 정수 형식인 경우 응용 프로그램은 SQLULEN 버퍼를 사용하고 값을 0으로 초기화해야 하며 일부 드라이버는 32비트 또는 16비트 버퍼만 작성하고 상위 순서의 비트를 변경하지 않고 그대로 둘 수 있기 때문에 이 함수를 호출하기 전에 값을 0으로 초기화해야 합니다.  
  
 *ValuePtr이* NULL인 경우 *StringLengthPtr은* *ValuePtr에서*가리키는 버퍼에서 반환할 수 있는 총 바이트 수(문자 데이터에 대한 null 종료 문자 제외)를 반환합니다.  
  
 *버퍼 길이*  
 [입력] *FieldIdentifier가* ODBC 정의 필드이고 *ValuePtr이* 문자 문자열 또는 이진 버퍼를 가리키는 \*경우 이 인수는 *ValuePtr*의 길이여야 합니다. *필드식별자가* ODBC 정의 필드이고 \* *ValuePtr이* 정수인 경우 *버퍼길이는* 무시됩니다. ValuePtr의 값이 유니코드 데이터 **형식(SQLGetDescFieldW를**호출할 때)인 경우 *BufferLength* 인수는 짝수여야 합니다. * \**  
  
 *FieldIdentifier가* 드라이버 정의 필드인 경우 응용 프로그램은 *BufferLength* 인수를 설정하여 드라이버 관리자에 필드의 특성을 나타냅니다. *BufferLength에는* 다음 값이 있을 수 있습니다.  
  
-   * \*ValuePtr이* 문자 문자열에 대한 포인터인 경우 *BufferLength는* 문자열의 길이 또는 SQL_NTS.  
  
-   * \*ValuePtr이* 이진 버퍼에 대한 포인터인 경우 응용 프로그램은 *버퍼길이*에 SQL_LEN_BINARY_ATTR(길이) 매크로의 결과를 배치합니다.*length* 이렇게 하면 *버퍼길이에*음수 값이 배치됩니다.  
  
-   * \*ValuePtr이* 문자열 문자열 이나 이진 문자열 이외의 값에 대 한 포인터 인 경우 *BufferLength* 값 SQL_IS_POINTER 있어야 합니다.  
  
-   * \*ValuePtr고정* 길이 데이터 형식이 포함되어 있는 경우 *BufferLength는* 적절히 SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT 또는 SQL_IS_USMALLINT.  
  
 *문자열길이Ptr*  
 [출력] **ValuePtr에서*반환할 수 있는 총 바이트 수(null-termination 문자에 필요한 바이트 수 제외)를 반환하는 버퍼에 대한 포인터입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_NO_DATA 또는 SQL_INVALID_HANDLE.  
  
 *SQL_NO_DATA RecNumber가* 현재 설명자 레코드 수보다 큰 경우 반환됩니다.  
  
 *설명자핸들이* IRD 핸들이고 명령문이 준비되거나 실행된 상태이지만 연결된 열린 커서가 없는 경우 SQL_NO_DATA 반환됩니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetDescField** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환하는 경우 *핸들 유형* SQL_HANDLE_STMT 및 *명령문* *핸들* 핸들을 사용하는 **SQLGetDiagRec를** 호출하여 연결된 SQLSTATE 값을 가져올 수 있습니다. 다음 표에서는 **SQLGetDescField에서** 일반적으로 반환하는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01004|문자열 데이터, 오른쪽 잘린|버퍼 \* *ValuePtr* 전체 설명자 필드를 반환할 만큼 크지 않았기 때문에 필드가 잘렸습니다. 잘린 설명자 필드의 길이는 **StringLengthPtr에서*반환됩니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|07009|잘못된 설명자 인덱스|(DM) *RecNumber* 인수는 0이고 SQL_ATTR_USE_BOOKMARK 문 특성은 SQL_UB_OFF *설명자 핸들 인수는* IRD 핸들입니다. 이 오류는 설명자가 문 핸들과 연결된 경우에만 명시적으로 할당된 설명자에 대해 반환될 수 있습니다.<br /><br /> *FieldIdentifier* 인수는 레코드 필드이고 *RecNumber* 인수는 0이고 *설명자 핸들* 인수는 IPD 핸들입니다.<br /><br /> *RecNumber* 인수가 0보다 적습니다.|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결된 데이터 원본 간의 통신 링크가 실패했습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY007|관련 문이 준비되지 않았습니다.|*설명자핸들은* *명령문 핸들을* IRD로 연결되었으며 관련 문 핸들이 준비되거나 실행되지 않았습니다.|  
|HY010|함수 시퀀스 오류|(DM) *설명자핸들은* 비동기적으로 실행되는 함수(이 함수가 아님)가 호출되고 이 함수가 호출될 때 여전히 실행 중인 *StatementHandle과* 연결되었습니다.<br /><br /> (DM) *설명자핸들은* **SQLExecute,** **SQLExecDirect**, **SQLBulkOperations**또는 **SQLSetPos가** 호출되어 반환된 SQL_NEED_DATA 대한 *문핸들와* 연결되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.<br /><br /> (DM) *설명자 핸들과*연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. 이 비동기 함수는 **SQLGetDescField** 함수가 호출될 때 계속 실행 중이었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY021|일관되지 않은 설명자 정보|SQL_DESC_TYPE 및 SQL_DESC_DATETIME_INTERVAL_CODE 필드는 유효한 ODBC SQL 형식, 유효한 드라이버 별 SQL 유형(IPD용) 또는 유효한 ODBC C 유형(APD 또는 ARD)을 형성하지 않습니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|(DM) * \*ValuePtr은* 문자 문자열이고 *버퍼 길이는* 0보다 적습니다.|  
|HY091|잘못된 설명자 필드 식별자|*FieldIdentifier는* ODBC 정의 필드가 아니며 구현 정의 값이 아닙니다.<br /><br /> *설명자* *핸들에*대해 필드 식별자가 정의되지 않았습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *설명자핸들과* 연결된 드라이버는 기능을 지원하지 않습니다.|  
  
## <a name="comments"></a>주석  
 응용 프로그램은 **SQLGetDescField를** 호출하여 설명자 레코드의 단일 필드 값을 반환할 수 있습니다. **SQLGetDescField를** 호출하면 헤더 필드, 레코드 필드 및 책갈피 필드를 포함하여 모든 설명자 형식의 모든 필드의 설정을 반환할 수 있습니다. 응용 프로그램은 **SQLGetDescField에**반복적으로 호출하여 임의의 순서로 동일하거나 다른 설명자의 여러 필드 설정을 가져올 수 있습니다. **SQLGetDescField는** 드라이버 정의 설명자 필드를 반환하기 위해 호출할 수도 있습니다.  
  
 성능상의 이유로 응용 프로그램은 문을 실행하기 전에 IRD에 대해 **SQLGetDescField를** 호출해서는 안 됩니다.  
  
 열 또는 매개 변수 데이터의 이름, 데이터 형식 및 저장소를 설명하는 여러 필드의 설정은 **SQLGetDescRec**에 대한 단일 호출에서 검색할 수도 있습니다. **SQLGetStmtAttr는** 설명자 헤더에서 단일 필드의 설정을 반환하기 위해 호출할 수 있습니다. **SQLColAttribute**, **SQLDescribeCol**및 **SQLDescribeParam** 반환 레코드 또는 책갈피 필드.  
  
 응용 프로그램이 **SQLGetDescField를** 호출하여 특정 설명자 형식에 대해 정의되지 않은 필드의 값을 검색하면 함수가 SQL_SUCCESS 반환되지만 필드에 대해 반환되는 값은 정의되지 않습니다. 예를 들어 APD 또는 ARD의 SQL_DESC_NAME 또는 SQL_DESC_NULLABLE 필드에 **대해 SQLGetDescField를** 호출하면 필드에 대한 정의되지 않은 값만 반환되는 SQL_SUCCESS 반환됩니다.  
  
 응용 프로그램이 **SQLGetDescField를** 호출하여 특정 설명자 형식에 대해 정의되었지만 기본값이 없고 아직 설정되지 않은 필드의 값을 검색하면 함수가 SQL_SUCCESS 반환되지만 필드에 대해 반환되는 값은 정의되지 않습니다. 설명자 필드의 초기화 및 필드에 대한 설명에 대한 자세한 내용은 [SQLSetDescField의](../../../odbc/reference/syntax/sqlsetdescfield-function.md)"설명자 필드의 초기화"를 참조하십시오. 설명자에 대한 자세한 내용은 [설명자](../../../odbc/reference/develop-app/descriptors.md)를 참조하십시오.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|여러 설명자 필드 얻기|[SQLGetDescRec 함수](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|단일 설명자 필드 설정|[SQLSetDesc필드 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|여러 설명자 필드 설정|[SQLSetDescRec 함수](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
