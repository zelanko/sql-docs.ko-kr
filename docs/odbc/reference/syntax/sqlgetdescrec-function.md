---
title: SQLGetDescRec 함수 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDescRec
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDescRec
helpviewer_keywords:
- SQLGetDescRec function [ODBC]
ms.assetid: 325e0907-8e87-44e8-a111-f39e636a9cbc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 87d7b971b379f19f8451e924932a5e699e9b9983
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285488"
---
# <a name="sqlgetdescrec-function"></a>SQLGetDescRec 함수
**규칙**  
 버전 출시: ODBC 3.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLGetDescRec는** 설명자 레코드의 여러 필드의 현재 설정 또는 값을 반환합니다. 반환된 필드는 열 또는 매개 변수 데이터의 이름, 데이터 형식 및 저장소를 설명합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLGetDescRec(  
      SQLHDESC        DescriptorHandle,  
      SQLSMALLINT     RecNumber,  
      SQLCHAR *       Name,  
      SQLSMALLINT     BufferLength,  
      SQLSMALLINT *   StringLengthPtr,  
      SQLSMALLINT *   TypePtr,  
      SQLSMALLINT *   SubTypePtr,  
      SQLLEN *        LengthPtr,  
      SQLSMALLINT *   PrecisionPtr,  
      SQLSMALLINT *   ScalePtr,  
      SQLSMALLINT *   NullablePtr);  
```  
  
## <a name="arguments"></a>인수  
 *DescriptorHandle*  
 [입력] 설명자 핸들입니다.  
  
 *RecNumber*  
 [입력] 응용 프로그램이 정보를 검색하는 설명자 레코드를 나타냅니다. 설명자 레코드는 1에서 번호가 매겨지며 레코드 번호 0은 책갈피 레코드입니다. *RecNumber* 인수는 SQL_DESC_COUNT 값보다 적거나 같아야 합니다. *RecNumber가* SQL_DESC_COUNT 작거나 같지만 행에 열 또는 매개 변수에 대한 데이터가 없는 경우 **SQLGetDescRec를** 호출하면 필드의 기본값이 반환됩니다. 자세한 내용은 [SQLSetDescField의](../../../odbc/reference/syntax/sqlsetdescfield-function.md)"설명자 필드의 초기화"를 참조하십시오.  
  
 *이름*  
 [출력] 설명자 레코드에 대한 SQL_DESC_NAME 필드를 반환하는 버퍼에 대한 포인터입니다.  
  
 *이름이* NULL인 경우 *StringLengthPtr은* *Name로*가리키는 버퍼에서 반환할 수 있는 총 문자 수(문자 데이터에 대한 null-termination 문자 제외)를 반환합니다.  
  
 *버퍼 길이*  
 [입력] **이름* 버퍼의 길이(문자)입니다.  
  
 *문자열길이Ptr*  
 [출력] null-termination 문자를 제외 하 고 \* *Name* 버퍼에서 반환 할 수 있는 데이터의 문자 수를 반환 하는 버퍼에 대 한 포인터입니다. 문자 수가 *BufferLength보다*크거나 같으면 \* *이름의* 데이터가 *BufferLength에* 잘려null 종료 문자의 길이를 뺀 값이며 드라이버에 의해 null-종료됩니다.  
  
 *타이핑 Ptr*  
 [출력] 설명자 레코드에 대한 SQL_DESC_TYPE 필드의 값을 반환하는 버퍼에 대한 포인터입니다.  
  
 *하위 유형 Ptr*  
 [출력] 형식이 SQL_DATETIME 또는 SQL_INTERVAL 레코드의 경우 SQL_DESC_DATETIME_INTERVAL_CODE 필드의 값을 반환하는 버퍼에 대한 포인터입니다.  
  
 *길이 Ptr*  
 [출력] 설명자 레코드에 대한 SQL_DESC_OCTET_LENGTH 필드 값을 반환하는 버퍼에 대한 포인터입니다.  
  
 *정밀Ptr*  
 [출력] 설명자 레코드에 대한 SQL_DESC_PRECISION 필드의 값을 반환하는 버퍼에 대한 포인터입니다.  
  
 *스케일 Ptr*  
 [출력] 설명자 레코드에 대한 SQL_DESC_SCALE 필드의 값을 반환하는 버퍼에 대한 포인터입니다.  
  
 *널러블 Ptr*  
 [출력] 설명자 레코드에 대한 SQL_DESC_NULLABLE 필드의 값을 반환하는 버퍼에 대한 포인터입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_NO_DATA 또는 SQL_INVALID_HANDLE.  
  
 *SQL_NO_DATA RecNumber가* 현재 설명자 레코드 수보다 큰 경우 반환됩니다.  
  
 *설명자핸들이* IRD 핸들이고 명령문이 준비되거나 실행된 상태이지만 연결된 열린 커서가 없는 경우 SQL_NO_DATA 반환됩니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetDescRec** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환하는 *경우,* SQL_HANDLE_DESC 핸들 유형 및 *설명자 핸들*핸들을 사용하는 *Handle* **SQLGetDiagRec을** 호출하여 연결된 SQLSTATE 값을 가져올 수 있습니다. 다음 표에서는 **SQLGetDescRec에서** 일반적으로 반환하는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01004|문자열 데이터, 오른쪽 잘린|버퍼 \* *Name이* 전체 설명자 필드를 반환할 만큼 충분히 크지 않았습니다. 따라서 필드가 잘렸습니다. 잘린 설명자 필드의 길이는 **StringLengthPtr에서*반환됩니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|07009|잘못된 설명자 인덱스|*FieldIdentifier* 인수는 레코드 필드이고 *RecNumber* 인수는 0으로 설정되었으며 *설명자 핸들* 인수는 IPD 핸들입니다.<br /><br /> (DM) *RecNumber* 인수가 0으로 설정되고 SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_OFF 설정되었으며 *설명자 핸들* 인수는 IRD 핸들입니다.<br /><br /> *RecNumber* 인수가 0보다 적습니다.|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결된 데이터 원본 간의 통신 링크가 실패했습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY007|관련 문이 준비되지 않았습니다.|*설명자핸들은* IRD와 연결되었으며 연결된 명령문 핸들이 준비되거나 실행된 상태가 아닙니다.|  
|HY010|함수 시퀀스 오류|(DM) *설명자핸들은* 비동기적으로 실행되는 함수(이 함수가 아님)가 호출되고 이 함수가 호출될 때 여전히 실행 중인 *StatementHandle과* 연결되었습니다.<br /><br /> (DM) *설명자핸들은* **SQLExecute,** **SQLExecDirect**, **SQLBulkOperations**또는 **SQLSetPos가** 호출되어 반환된 SQL_NEED_DATA 대한 *문핸들와* 연결되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.<br /><br /> (DM) *설명자 핸들과*연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. **SQLGetDescRec가** 호출될 때 이 비동기 함수는 여전히 실행 중이었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *설명자핸들과* 연결된 드라이버는 기능을 지원하지 않습니다.|  
  
## <a name="comments"></a>주석  
 응용 프로그램은 **SQLGetDescRec을** 호출하여 단일 열 또는 매개 변수에 대한 다음 설명자 필드의 값을 검색할 수 있습니다.  
  
-   SQL_DESC_NAME  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE(형식이 SQL_DATETIME 또는 SQL_INTERVAL 레코드의 경우)  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_NULLABLE  
  
 **SQLGetDescRec** 헤더 필드에 대 한 값을 검색 하지 않습니다.  
  
 응용 프로그램은 필드에 해당하는 인수를 null 포인터에 설정하여 필드 설정의 반환을 방지할 수 있습니다.  
  
 응용 프로그램이 **SQLGetDescRec를** 호출하여 특정 설명자 형식에 대해 정의되지 않은 필드의 값을 검색하면 함수가 SQL_SUCCESS 반환하지만 필드에 대해 반환되는 값은 정의되지 않습니다. 예를 들어 APD 또는 ARD의 SQL_DESC_NAME 또는 SQL_DESC_NULLABLE 필드에 **대해 SQLGetDescRec을** 호출하면 필드에 대해 정의되지 않은 값이 SQL_SUCCESS 반환됩니다.  
  
 응용 프로그램이 **SQLGetDescRec를** 호출하여 특정 설명자 형식에 대해 정의되었지만 기본값이 없고 아직 설정되지 않은 필드의 값을 검색하면 함수는 SQL_SUCCESS 반환되지만 필드에 대해 반환되는 값은 정의되지 않습니다. 자세한 내용은 [SQLSetDescField의](../../../odbc/reference/syntax/sqlsetdescfield-function.md)"설명자 필드의 초기화"를 참조하십시오.  
  
 **SQLGetDescField**에 대한 호출을 통해 필드 값을 개별적으로 검색할 수도 있습니다. 설명자 헤더 또는 레코드의 필드에 대한 설명은 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)을 참조하십시오. 설명자에 대한 자세한 내용은 [설명자](../../../odbc/reference/develop-app/descriptors.md)를 참조하십시오.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|열 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|매개 변수 바인딩|[SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|설명자 필드 얻기|[SQLGetDescField 함수](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|여러 설명자 필드 설정|[SQLSetDescRec 함수](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
