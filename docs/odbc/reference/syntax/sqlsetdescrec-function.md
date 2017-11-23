---
title: "SQLSetDescRec 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLSetDescRec
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLSetDescRec
helpviewer_keywords: SQLSetDescRec function [ODBC]
ms.assetid: bf55256c-7eb7-4e3f-97ef-b0fee09ba829
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dda8ecdee1830805c51b5e795f91ff4025218260
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="sqlsetdescrec-function"></a>SQLSetDescRec 함수
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLSetDescRec** 열 또는 매개 변수에 바인딩된 버퍼 데이터 및 데이터 형식에 영향을 주는 여러 설명자 필드를 설정 하는 함수입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
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
 [입력] 설명자 핸들입니다. IRD 핸들 되지 않아야 합니다.  
  
 *RecNumber*  
 [입력] 필드를 설정할 수 있는 설명자 레코드를 나타냅니다. 설명자 레코드는 0 또는 레코드 번호가 0 책갈피 레코드 번호가 지정 됩니다. 이 인수는 0 보다 크거나 같은 이어야 합니다. 경우 *RecNumber* SQL_DESC_COUNT, SQL_DESC_COUNTis의 값으로 변경의 값 보다 크면 *RecNumber*합니다.  
  
 *형식*  
 [입력] 설명자 레코드에 대 한 SQL_DESC_TYPE 필드를 설정할 값입니다.  
  
 *하위 유형*  
 [입력] 해당 형식이 SQL_DATETIME 또는 sql_interval 인 레코드를 위한 값을 SQL_DESC_DATETIME_INTERVAL_CODE 필드를 설정할 값입니다.  
  
 *길이*  
 [입력] 설명자 레코드에 대 한 SQL_DESC_OCTET_LENGTH 필드를 설정할 값입니다.  
  
 *전체 자릿수*  
 [입력] 설명자 레코드에 대 한 SQL_DESC_PRECISION 필드를 설정할 값입니다.  
  
 *소수 자릿수*  
 [입력] 설명자 레코드에 대 한 SQL_DESC_SCALE 필드를 설정할 값입니다.  
  
 *DataPtr*  
 [지연 된 입력 또는 출력] 설명자 레코드에 SQL_DESC_DATA_PTR 필드가 설정 하는 값입니다. *DataPtr* null 포인터를 설정할 수 있습니다.  
  
 *DataPtr* SQL_DESC_DATA_PTR 필드가 null 포인터를 설정 하려면 인수는 null 포인터를 설정할 수 있습니다. 경우에 대 한 핸들은 *DescriptorHandle* 인수는 연결 된,이 열을 바인딩 해제 합니다.  
  
 *StringLengthPtr*  
 [지연 된 입력 또는 출력] 설명자 레코드에 대 한 SQL_DESC_OCTET_LENGTH_PTR 필드를 설정할 값입니다. *StringLengthPtr* SQL_DESC_OCTET_LENGTH_PTR 필드는 null 포인터를 설정 하는 null 포인터를 설정할 수 있습니다.  
  
 *IndicatorPtr*  
 [지연 된 입력 또는 출력] 설명자 레코드에 대 한 SQL_DESC_INDICATOR_PTR 필드를 설정할 값입니다. *IndicatorPtr* SQL_DESC_INDICATOR_PTR 필드는 null 포인터를 설정 하는 null 포인터를 설정할 수 있습니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLSetDescRec** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 관련된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 와 *HandleType* SQL_의 HANDLE_DESC 및 *처리* 의 *DescriptorHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLSetDescRec** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|오류|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|07009|잘못 된 설명자 인덱스입니다.|*RecNumber* 인수는 0으로 설정 된 및 *DescriptorHandle* IPD 핸들을 참조 합니다.<br /><br /> *RecNumber* 인수가 0 보다 작습니다.<br /><br /> *RecNumber* 인수 열 또는 매개 변수를 데이터 원본에서 지원할 수 있는 최대 수보다 큽니다. 및 *DescriptorHandle* 는 APD, IPD, 또는 인수 했습니다.<br /><br /> *RecNumber* 0에 인수가 및 *DescriptorHandle* 암시적으로 할당 된 APD 인수 라고 합니다. (이 오류는 발생 하지 응용 프로그램이 명시적으로 할당 된 설명자와 APD 또는까지 명시적으로 할당 된 응용 프로그램 설명자 인지 실행 시간 알 수 없습니다.)|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버 연결 된 데이터 원본 간에 통신 링크 하지 못했습니다.|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류입니다.|DM ()는 *DescriptorHandle* 연결 된 한 *StatementHandle* 는, 비동기적으로 실행 중인 (하지이 하나)를 호출한 함수와이 함수가 호출 될 때 계속 실행에 대 한 합니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, 또는 **SQLSetPos** 가 대 한 호출에서  *StatementHandle* 입니다는 *DescriptorHandle* 연결 했으며 SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 보내기 전에 호출 되었습니다.<br /><br /> DM ()는 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한는 *DescriptorHandle*합니다. 이 aynchronous 함수 계속 실행 될 때는 **SQLSetDescRec** 함수를 호출 했습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 와 관련 된 문 핸들 중 하나에 대해 호출한는 *DescriptorHandle* SQL_PARAM_DATA_AVAILABLE를 반환 합니다. 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에이 함수가 호출 되었습니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY016|구현 행 설명자를 수정할 수 없습니다.|*DescriptorHandle* 인수 IRD에 연결 되었습니다.|  
|HY021|일관성 없는 설명자 정보|*형식* 필드나 다른 필드는 설명자의 SQL_DESC_TYPE 필드와 연결 된 되지 않았거나 잘못 일치 합니다.<br /><br /> 일관성 확인을 하는 동안 체크 설명자 정보 일관 되지 않았습니다. ("일관성 검사,"이이 섹션의 뒷부분에 나오는 참조).|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|(DM) 드라이버는 ODBC 2는*.x* 드라이버, 설명자에서는 카드가 *ColumnNumber* 인수는 0이 고, 인수에 대해 지정 된 값으로 설정 된 *BufferLength* 되었습니다 4과 같지 않습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)와 관련 된 드라이버의 *DescriptorHandle* 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>설명  
 응용 프로그램에서 호출할 수 **SQLSetDescRec** 단일 열 또는 매개 변수에 대해 다음 필드를 설정 하려면:  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE (형식이 SQL_DATETIME 또는 sql_interval 인 변수인 레코드)  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_DATA_PTR  
  
-   SQL_DESC_OCTET_LENGTH_PTR  
  
-   SQL_DESC_INDICATOR_PTR  
  
> [!NOTE]  
>  호출 하는 경우 **SQLSetDescRec** 실패 하면로 식별 되는 설명자 레코드의 콘텐츠는 *RecNumber* 인수 정의 되지 않습니다.  
  
 열 또는 매개 변수를 바인딩할 때 **SQLSetDescRec** 바인딩을 호출 하지 않고 영향을 주는 여러 필드를 변경할 수 있습니다 **SQLBindCol** 또는 **SQLBindParameter** 또는 여러 번 호출 **SQLSetDescField**합니다. **SQLSetDescRec** 현재 문에 연결 된 설명자에 필드를 설정할 수 있습니다. **SQLBindParameter** 보다 더 많은 필드를 설정 **SQLSetDescRec**는 APD와 한 번 호출에서 IPD 필드를 설정할 수 있으며 설명자 핸들을 필요 하지 않습니다.  
  
> [!NOTE]  
>  문 특성 SQL_ATTR_USE_BOOKMARKS 항상 설정할지 호출 하기 전에 **SQLSetDescRec** 와 *RecNumber* 책갈피 필드를 설정 하려면 0의 인수입니다. 이 옵션은 필수, 것이 좋습니다.  
  
## <a name="consistency-checks"></a>일관성 검사  
 일관성 확인을 응용 프로그램에서 IPD, 카드가, APD의 SQL_DESC_DATA_PTR 필드가 설정 될 때마다 드라이버에 의해 수행 됩니다. 이 다른 필드와 일치 하지 않으면 필드 **SQLSetDescRec** SQLSTATE HY021를 반환 합니다 (설명자 정보).  
  
 응용 프로그램에서 IPD, 카드가, APD의 SQL_DESC_DATA_PTR 필드가 설정 될 때마다 드라이버 SQL_DESC_TYPE 필드의 값과 해당 SQL_DESC_TYPE 필드에 적용할 수 있는 값은 유효 하 고 일관성을 확인 합니다. 이 검사는 항상 때 수행 되 **SQLBindParameter** 또는 **SQLBindCol** 호출 되거나 **SQLSetDescRec** 는 APD, 카드가, 또는 IPD에 대해 호출 됩니다. 일관성 확인이 설명자 필드에 대해 다음 검사에 포함 됩니다.  
  
-   SQL_DESC_TYPE 필드는 유효한 ODBC C 또는 SQL 형식 또는 드라이버별 SQL 유형 중 하나 여야 합니다. SQL_DESC_CONCISE_TYPE 필드는 유효한 ODBC C 또는 SQL 형식 또는 드라이버 관련 C 또는 SQL 형식으로 간결 날짜/시간 및 간격 형식을 포함 한 중 하나 여야 합니다.  
  
-   SQL_DESC_TYPE 레코드 필드가 SQL_DATETIME 또는 SQL_INTERVAL 인 경우 값을 SQL_DESC_DATETIME_INTERVAL_CODE 필드는 유효한 날짜/시간 또는 간격 코드 중 하나 여야 합니다. (에 값을 SQL_DESC_DATETIME_INTERVAL_CODE 필드의 설명을 참조 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
-   SQL_DESC_TYPE 필드는 숫자 형식의 나타내지만 SQL_DESC_PRECISION 및 SQL_DESC_SCALE 필드는 유효한 것으로 확인 됩니다.  
  
-   SQL_DESC_CONCISE_TYPE 필드가 시간 또는 타임 스탬프 데이터 형식이 인 경우 간격 입력 초 구성 요소 또는 한 시간 구성 요소와 간격 데이터 형식 중 하나가 SQL_DESC_PRECISION 필드를 확인 하는 유효한 초의 전체 자릿수가 되도록 합니다.  
  
-   SQL_DESC_CONCISE_TYPE이 간격 데이터 형식인 경우 SQL_DESC_DATETIME_INTERVAL_PRECISION 필드는 유효한 간격 선행 정밀도 값으로 확인 됩니다.  
  
 일반적으로 IPD의 SQL_DESC_DATA_PTR 필드가 설정 되지 않았습니다. 그러나 응용 프로그램 이렇게 하려면 IPD 필드의 일관성 확인을 적용 합니다. IRD에서 일관성 확인을 수행할 수 없습니다. 값으로는 IPD의 SQL_DESC_DATA_PTR 필드가 설정 된 실제로 저장 되지 않으며, 호출 하 여 검색할 수 없습니다 **SQLGetDescField** 또는 **SQLGetDescRec**; 설정을 적용 하기 위해만 이루어집니다는 일관성 확인입니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|열 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|매개 변수 바인딩|[SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|단일 설명자 필드 가져오기|[SQLGetDescField 함수](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|여러 설명자 필드 가져오기|[SQLGetDescRec 함수](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|단일 설명자 필드 설정|[SQLSetDescField 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
