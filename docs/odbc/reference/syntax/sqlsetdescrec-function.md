---
title: SQLSetDescRec 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2b9940d55ca10292d6c90a241f47479a2178eff3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68343061"
---
# <a name="sqlsetdescrec-function"></a>SQLSetDescRec 함수
**규칙**  
 소개 된 버전: ODBC 3.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLSetDescRec** 함수는 열 또는 매개 변수 데이터에 바인딩된 데이터 형식 및 버퍼에 영향을 주는 여러 설명자 필드를 설정 합니다.  
  
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
 입력 설명자 핸들입니다. 이는 IRD 핸들이 아니어야 합니다.  
  
 *개수*  
 입력 설정할 필드가 포함 된 설명자 레코드를 나타냅니다. 설명자 레코드의 번호는 0에서, 레코드 번호 0은 책갈피 레코드입니다. 이 인수는 0 보다 크거나 같아야 합니다. 값 *이 SQL_DESC_COUNT* 값 보다 크면 SQL_DESC_COUNTis 값으로 변경 됩니다. **  
  
 *형식*  
 입력 설명자 레코드에 대 한 SQL_DESC_TYPE 필드를 설정 하는 데 사용할 값입니다.  
  
 *하위 형식*  
 입력 형식이 SQL_DATETIME 또는 SQL_INTERVAL 인 레코드의 경우이 값은 SQL_DESC_DATETIME_INTERVAL_CODE 필드를 설정 하는 데 사용할 값입니다.  
  
 *길이*  
 입력 설명자 레코드에 대 한 SQL_DESC_OCTET_LENGTH 필드를 설정 하는 데 사용할 값입니다.  
  
 *정밀도*  
 입력 설명자 레코드에 대 한 SQL_DESC_PRECISION 필드를 설정 하는 데 사용할 값입니다.  
  
 *규모*  
 입력 설명자 레코드에 대 한 SQL_DESC_SCALE 필드를 설정 하는 데 사용할 값입니다.  
  
 *DataPtr*  
 [지연 된 입력 또는 출력] 설명자 레코드에 대 한 SQL_DESC_DATA_PTR 필드를 설정 하는 데 사용할 값입니다. *Dataptr* 은 null 포인터로 설정할 수 있습니다.  
  
 *Dataptr* 인수는 null 포인터로 설정 하 여 SQL_DESC_DATA_PTR 필드를 null 포인터로 설정할 수 있습니다. *DescriptorHandle* 인수의 핸들이 나와 연결 된 경우이는 열을 바인딩 해제 합니다.  
  
 *StringLengthPtr*  
 [지연 된 입력 또는 출력] 설명자 레코드에 대 한 SQL_DESC_OCTET_LENGTH_PTR 필드를 설정 하는 데 사용할 값입니다. *StringLengthPtr* 는 null 포인터로 설정 하 여 SQL_DESC_OCTET_LENGTH_PTR 필드를 null 포인터로 설정할 수 있습니다.  
  
 *IndicatorPtr*  
 [지연 된 입력 또는 출력] 설명자 레코드에 대 한 SQL_DESC_INDICATOR_PTR 필드를 설정 하는 데 사용할 값입니다. *IndicatorPtr* 는 null 포인터로 설정 하 여 SQL_DESC_INDICATOR_PTR 필드를 null 포인터로 설정할 수 있습니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLSetDescRec** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 SQL_HANDLE_DESC의 *HandleType* 및 *DescriptorHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **SQLSetDescRec** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|07009|잘못 된 설명자 인덱스|DescriptorHandle *인수는* 0으로 설정 되 고, IPD 핸들 ** 을 참조 합니다.<br /><br /> 인수 *인수가* 0 보다 작은 경우<br /><br /> DescriptorHandle *인수가 데이터* 원본이 지원할 수 있는 열 또는 매개 변수의 최대 개수 보다 크고,이 인수는 APD, IPD 또는 ** 입니다.<br /><br /> *DescriptorHandle* *인수는 0* 과 같고 암시적으로 할당 된 apd 인수를 참조 합니다. (이 오류는 명시적으로 할당 된 응용 프로그램 설명자가 명시적으로 할당 된 응용 프로그램 설명자가 실행 시간을 초과 하는지 여부를 알 수 없기 때문에 명시적으로 할당 된 응용 프로그램 설명자에서 발생 하지 않습니다.)|  
|08S01|통신 연결 오류|드라이버가 연결 된 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. MessageText 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다. * \**|  
|HY001|메모리 할당 오류|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류|(DM) *DescriptorHandle* 가이 함수를 호출 하지 않고 비동기적으로 실행 되는 함수를 호출 하 고이 함수가 호출 될 때 여전히 실행 되는 *StatementHandle* 와 연결 되었습니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 는 *DescriptorHandle* 가 연결 되 고 SQL_NEED_DATA 반환 된 *StatementHandle* 에 대해 호출 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.<br /><br /> (DM) *DescriptorHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. **SQLSetDescRec** 함수가 호출 될 때이 aynchronous 함수는 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **Sqlexecdirect**또는 **SQLMoreResults** 가 *DescriptorHandle* 와 연결 된 문 핸들 중 하나에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY016|구현 행 설명자를 수정할 수 없습니다.|*DescriptorHandle* 인수는 IRD와 연결 되어 있습니다.|  
|HY021|일관 되지 않은 설명자 정보|*형식* 필드 또는 설명자의 SQL_DESC_TYPE 필드와 연결 된 다른 필드가 잘못 되었거나 일치 하지 않습니다.<br /><br /> 일관성 확인 중에 확인 된 설명자 정보가 일치 하지 않습니다. (이 섹션의 뒷부분에 나오는 "일관성 검사"를 참조 하세요.)|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|(DM) *드라이버가 ODBC 2.x* 드라이버이 고, 설명자가 되었고, *columnnumber* 인수를 0으로 설정 하 고, 인수 *bufferlength* 에 지정 된 값이 4와 같지 않습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *DescriptorHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 응용 프로그램은 **SQLSetDescRec** 를 호출 하 여 단일 열 또는 매개 변수에 대해 다음 필드를 설정할 수 있습니다.  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE (형식이 SQL_DATETIME 또는 SQL_INTERVAL 인 레코드의 경우)  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_DATA_PTR  
  
-   SQL_DESC_OCTET_LENGTH_PTR  
  
-   SQL_DESC_INDICATOR_PTR  
  
> [!NOTE]  
>  **SQLSetDescRec** 에 대 한 호출이 실패 하는 경우에는 지 *수* 인수로 식별 되는 설명자 레코드의 내용이 정의 되지 않습니다.  
  
 열 또는 매개 변수를 바인딩할 때 **SQLSetDescRec** 를 사용 하면 **SQLBindCol** 또는 **SQLBindParameter** 를 호출 하거나 **SQLSetDescField**를 여러 번 호출 하지 않고 바인딩에 영향을 주는 여러 필드를 변경할 수 있습니다. **SQLSetDescRec** 는 현재 문과 연결 되지 않은 설명자에 필드를 설정할 수 있습니다. **SQLBindParameter** 는 **SQLSetDescRec**보다 많은 필드를 설정 하 고, apd와 IPD 모두에서 필드를 한 번의 호출로 설정할 수 있으며, 설명자 핸들이 필요 하지 않습니다.  
  
> [!NOTE]  
>  **SQLSetDescRec** 를 호출 하기 전에 문 *SQL_ATTR_USE_BOOKMARKS 특성을* 항상 설정 해야 합니다. 반드시 필요한 것은 아니지만, 적극 권장 됩니다.  
  
## <a name="consistency-checks"></a>일관성 확인  
 응용 프로그램에서 APD, IPD 또는의 SQL_DESC_DATA_PTR 필드를 설정 하면 자동으로 일관성 확인이 수행 됩니다. 필드 중 하나라도 다른 필드와 일치 하지 않는 경우 **SQLSetDescRec** 는 SQLSTATE HY021 (일치 하지 않는 설명자 정보)를 반환 합니다.  
  
 응용 프로그램에서 APD, IPD 또는의 SQL_DESC_DATA_PTR 필드를 설정 하는 경우 드라이버는 SQL_DESC_TYPE 필드의 값과 해당 SQL_DESC_TYPE 필드에 적용 가능한 값이 유효 하 고 일관적인 지 확인 합니다. **SQLBindParameter** 또는 SQLBindCol를 호출 하거나 apd, **** 또는 IPD에 대해 **SQLSetDescRec** 가 호출 될 때이 검사가 항상 수행 됩니다. 이 일관성 확인에는 설명자 필드에 대 한 다음 검사가 포함 됩니다.  
  
-   SQL_DESC_TYPE 필드는 올바른 ODBC C 또는 SQL 형식 또는 드라이버별 SQL 유형 중 하나 여야 합니다. SQL_DESC_CONCISE_TYPE 필드는 간결한 datetime 및 interval 형식을 포함 하 여 유효한 ODBC C 또는 SQL 형식 또는 드라이버별 C 또는 SQL 형식 중 하나 여야 합니다.  
  
-   SQL_DESC_TYPE 레코드 필드가 SQL_DATETIME 또는 SQL_INTERVAL 이면 SQL_DESC_DATETIME_INTERVAL_CODE 필드가 유효한 날짜/시간 또는 간격 코드 중 하나 여야 합니다. [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)의 SQL_DESC_DATETIME_INTERVAL_CODE 필드에 대 한 설명을 참조 하세요.  
  
-   SQL_DESC_TYPE 필드가 숫자 형식을 나타내면 SQL_DESC_PRECISION 및 SQL_DESC_SCALE 필드가 유효 하다 고 확인 됩니다.  
  
-   SQL_DESC_CONCISE_TYPE 필드가 시간 또는 타임 스탬프 데이터 형식, 초 구성 요소를 포함 하는 간격 형식 또는 시간 구성 요소가 포함 된 interval 데이터 형식 중 하나인 경우 SQL_DESC_PRECISION 필드는 유효한 초 전체 자릿수로 확인 됩니다.  
  
-   SQL_DESC_CONCISE_TYPE interval 데이터 형식이 면 SQL_DESC_DATETIME_INTERVAL_PRECISION 필드가 유효한 간격 선행 전체 자릿수 값으로 확인 됩니다.  
  
 IPD의 SQL_DESC_DATA_PTR 필드는 일반적으로 설정 되지 않습니다. 그러나 IPD 필드에 대 한 일관성 확인을 강제 적용 하기 위해 응용 프로그램에서이 작업을 수행할 수 있습니다. IRD에 대해 일관성 확인을 수행할 수 없습니다. IPD의 SQL_DESC_DATA_PTR 필드가로 설정 된 값은 실제로 저장 되지 않으며 **SQLGetDescField** 또는 **SQLGetDescRec**를 호출 하 여 검색할 수 없습니다. 이 설정은 일관성 확인을 강제 적용 하는 경우에만 수행 됩니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|열 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|매개 변수 바인딩|[SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|단일 설명자 필드 가져오기|[SQLGetDescField 함수(SQLGetDescField Function)](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|여러 설명자 필드 가져오기|[SQLGetDescRec 함수](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|단일 설명자 필드 설정|[SQLSetDescField 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
