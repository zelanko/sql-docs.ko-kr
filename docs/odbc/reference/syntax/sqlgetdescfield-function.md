---
title: "SQLGetDescField 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1cbf48f5346d507505573391598cbd98017ccd8d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetdescfield-function"></a>SQLGetDescField 함수(SQLGetDescField Function)
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLGetDescField** 설명자 레코드의 단일 필드의 값 또는 현재 설정을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
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
 [입력] 응용 프로그램 정보를 찾고 설명자 레코드를 나타냅니다. 설명자 레코드는 0 또는 레코드 번호가 0 책갈피 레코드 번호가 지정 됩니다. 경우는 *FieldIdentifier* 인수는 헤더 필드를 나타냅니다. *RecNumber* 는 무시 됩니다. 경우 *RecNumber* SQL_DESC_COUNT 보다 작은 하지만 행 열 또는 매개 변수에 대 한 호출에 대 한 데이터를 포함 하지 않는 **SQLGetDescField** 필드의 기본값을 반환 합니다. (자세한 내용은의 "초기화의 설명자 필드" 참조 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
 *FieldIdentifier*  
 [입력] 값을 반환 하는 설명자 필드를 나타냅니다. 자세한 내용은 참조는 "*FieldIdentifier* 인수" 섹션 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)합니다.  
  
 *ValuePtr*  
 [출력] 버퍼 설명자 정보를 반환할에 대 한 포인터입니다. 데이터 형식 값에 따라 달라 집니다 *FieldIdentifier*합니다.  
  
 경우 *ValuePtr* 는 정수 형식, 응용 프로그램 SQLULEN의 버퍼를 사용 해야 및 일부 드라이버가이 함수를 호출 하기 전에 값을 0으로 초기화 될 수 있습니다만 하위 32 비트 또는 16 비트는 버퍼의 쓰기 및 상위 비트를 그대로 둡니다. 변경 되지 않습니다.  
  
 경우 *ValuePtr* 이 NULL 이면 *StringLengthPtr* 바이트 (문자 데이터에 대 한 null 종결 문자 제외)의 총 수를 반환 여전히 가리키는버퍼에서반환할수* ValuePtr*합니다.  
  
 *BufferLength*  
 [입력] 경우 *FieldIdentifier* 은 ODBC 정의 된 필드 및 *ValuePtr* 문자열 또는 이진 버퍼를 가리키거나,이 인수 길이 여야 \* *ValuePtr*. 경우 *FieldIdentifier* 은 ODBC 정의 된 필드 및 \* *ValuePtr* 정수 이면 *BufferLength* 는 무시 됩니다. 경우에 값 * \*ValuePtr* 유니코드 데이터 형식의 (호출할 때 **SQLGetDescFieldW**), *BufferLength* 인수 수는 짝수 여야 합니다.  
  
 경우 *FieldIdentifier* 드라이버에서 정의 된 필드는 응용 프로그램을 설정 하 여 드라이버 관리자에 필드의 특성을 나타내는 *BufferLength* 인수입니다. *BufferLength* 다음 값을 가질 수 있습니다.  
  
-   경우 * \*ValuePtr* 다음 문자열을에 대 한 포인터는 *BufferLength* SQL_NTS 또는 문자열의 길이입니다.  
  
-   경우 * \*ValuePtr* 이진 버퍼에 대 한 포인터에 있으면 응용 프로그램은 SQL_LEN_BINARY_ATTR의 결과 배치 (*길이*) 매크로에서 *BufferLength*합니다. 이렇게 하면 배치에 음수 값 *BufferLength*합니다.  
  
-   경우 * \*ValuePtr* 문자열이 나 이진 문자열 이외의 값에 대 한 포인터는 *BufferLength* SQL_IS_POINTER 값이 있어야 합니다.  
  
-   경우 * \*ValuePtr* 은 다음에 고정 길이 데이터 형식인 *BufferLength* 은 SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT, 또는 SQL_IS_USMALLINT를 적절 하 게 합니다.  
  
 *StringLengthPtr*  
 [출력] 바이트 (null 종결 문자에 필요한 바이트 수가 제외)의 총 수를 반환 하는 버퍼에 대 한 포인터를 반환 하려면 사용할 수 있는 **ValuePtr*합니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_NO_DATA, 또는 SQL_INVALID_HANDLE 합니다.  
  
 경우 SQL_NO_DATA가 반환 *RecNumber* 현재 설명자 레코드 개수 보다 큽니다.  
  
 경우 SQL_NO_DATA가 반환 *DescriptorHandle* 은 IRD 핸들 및 문이 준비 또는 실행 된 상태의 가져왔지만 했습니다 관련 된 열린 커서가 없습니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLGetDescField** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 관련된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 와 *HandleType* 의 여는 및 *처리* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLGetDescField** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|오류|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|버퍼 \* *ValuePtr* 충분히 필드 잘렸습니다 하므로 전체 설명자 필드를 반환할 수 없습니다. 잘리지 않은 설명자 필드의 길이에서 **StringLengthPtr*합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|07009|잘못 된 설명자 인덱스입니다.|DM ()는 *RecNumber* 인수를 0으로, SQL_ATTR_USE_BOOKMARK 문 특성은 SQL_UB_OFF, 및 *DescriptorHandle* IRD 핸들 되었습니다. (이 오류 반환할 수 있습니다는 명시적으로 할당 된 설명자에 대 한 설명자가 된 문 핸들에 연결 하는 경우에.)<br /><br /> *FieldIdentifier* 레코드 필드에 인수가 *RecNumber* 되었습니다. 0, 인수 및 *DescriptorHandle* IPD 핸들 되었습니다.<br /><br /> *RecNumber* 인수가 0 보다 작습니다.|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버 연결 된 데이터 원본 간에 통신 링크 하지 못했습니다.|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에 * \*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY007|관련 된 문이 준비 되지 않았습니다.|*DescriptorHandle* 연결 된 한 *StatementHandle* 관련 된 문이 IRD과 핸들에 준비 또는 되지 실행 합니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM) *DescriptorHandle* 연결 된 한 *StatementHandle* 는, 비동기적으로 실행 중인 (하지이 하나)를 호출한 함수와이 함수가 호출 될 때 계속 실행에 대 한 합니다.<br /><br /> (DM) *DescriptorHandle* 연결 된 한 *StatementHandle* 를 **SQLExecute**, **SQLExecDirect**, ** SQLBulkOperations**, 또는 **SQLSetPos** 호출 했으나 SQL_NEED_DATA를 반환 했습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 보내기 전에 호출 되었습니다.<br /><br /> DM ()는 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한는 *DescriptorHandle*합니다. 이 비동기 함수 계속 실행 될 때는 **SQLGetDescField** 함수를 호출 했습니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY021|일관성 없는 설명자 정보|SQL_DESC_TYPE 및 값을 SQL_DESC_DATETIME_INTERVAL_CODE 필드 (Apd 또는 ARDs)에 유효한 ODBC SQL 유형, (Ipd)에 대 한 유효한 드라이버별 SQL 형식 또는 유효한 ODBC C 형식을 형성 하지 않습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|(DM) * \*ValuePtr* 문자 문자열이 고 *BufferLength* 0 보다 작은 합니다.|  
|HY091|잘못 된 설명자 필드 식별자입니다.|*FieldIdentifier* ODBC 정의 필드 되었으며 구현에서 정의 된 값이 아닙니다.<br /><br /> *FieldIdentifier* 에 대 한 정의 되지 않은는 *DescriptorHandle*합니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)와 관련 된 드라이버의 *DescriptorHandle* 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>설명  
 응용 프로그램에서 호출할 수 **SQLGetDescField** 설명자 레코드의 단일 필드의 값을 반환 합니다. 에 대 한 호출 **SQLGetDescField** 헤더 필드, 레코드의 필드 및 책갈피 필드를 포함 하 여 모든 설명자 형식의 모든 필드의 설정을 반환할 수 있습니다. 응용 프로그램 반복 된 호출 하 여 동일한 또는 다른 설명자 임의의 순서로에서 여러 필드의 설정을 가져오려면 먼저 **SQLGetDescField**합니다. **SQLGetDescField** 드라이버에서 정의 된 설명자 필드를 반환 하려면 호출할 수도 있습니다.  
  
 성능상의 이유로 응용 프로그램 호출 하지 않아야 **SQLGetDescField** 문을 실행 하기 전에 IRD에 대 한 합니다.  
  
 단일 호출에서 이름, 데이터 형식 및 열 또는 매개 변수 데이터의 저장소를 설명 하는 여러 필드의 설정을 검색할 수 있습니다 **SQLGetDescRec**합니다. **SQLGetStmtAttr** 문 특성도 사용 되는 설명자 헤더의 단일 필드의 설정을 반환 하도록 호출 될 수 있습니다. **SQLColAttribute**, **SQLDescribeCol**, 및 **SQLDescribeParam** 레코드 또는 책갈피 필드를 반환 합니다.  
  
 응용 프로그램 호출 하는 경우 **SQLGetDescField** 특정 설명자 형식에 대 한 정의 되지 않은 필드의 값을 검색 하려면 함수는 SQL_SUCCESS를 반환 하지만 필드에 대해 반환 되는 값 정의 되지 않습니다. 예를 들어 호출 **SQLGetDescField** APD 또는 카드가 SQL_DESC_NAME 또는 SQL_DESC_NULLABLE 필드에 대 한는 SQL_SUCCESS 하지만 필드에 대 한 정의 되지 않은 값 반환 합니다.  
  
 응용 프로그램 호출 하는 경우 **SQLGetDescField** 하지만 특정 설명자 형식에 대해 정의 된 기본값은 없습니다 및 아직 설정 되지 않은 필드의 값을 검색 하려면 함수 반환 SQL_SUCCESS 하지만 값 반환 필드에 대해 정의 되지 않습니다. 설명자 필드 및 필드의 설명은의 초기화에 자세한 내용은의 "초기화의 설명자 필드" 참조 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)합니다. 설명자에 대 한 자세한 내용은 참조 하십시오. [설명자](../../../odbc/reference/develop-app/descriptors.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|여러 설명자 필드 가져오기|[SQLGetDescRec 함수](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|단일 설명자 필드 설정|[SQLSetDescField 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|여러 설명자 필드 설정|[SQLSetDescRec 함수](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)

