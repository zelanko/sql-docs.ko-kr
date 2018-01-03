---
title: "SQLGetDescRec 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLGetDescRec
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLGetDescRec
helpviewer_keywords: SQLGetDescRec function [ODBC]
ms.assetid: 325e0907-8e87-44e8-a111-f39e636a9cbc
caps.latest.revision: "30"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 569a3708c13a4182e651c902ce7e1f1f9c7711dd
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlgetdescrec-function"></a>SQLGetDescRec 함수
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLGetDescRec** 현재 설정이 나 설명자 레코드의 여러 필드의 값을 반환 합니다. 반환 되는 필드 이름, 데이터 형식 및 열 또는 매개 변수 데이터 저장소에 설명 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
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
 [입력] 응용 프로그램 정보를 찾고 설명자 레코드를 나타냅니다. 설명자 레코드와 레코드 번호 책갈피 레코드 0 1부터 매겨집니다. *RecNumber* SQL_DESC_COUNT의 값 보다 작거나 같은 인수 이어야 합니다. 경우 *RecNumber* SQL_DESC_COUNT 보다 작은 하지만 행 열 또는 매개 변수에 대 한 호출에 대 한 데이터를 포함 하지 않는 **SQLGetDescRec** 필드의 기본값을 반환 합니다. (자세한 내용은의 "초기화의 설명자 필드" 참조 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
 *이름*  
 [출력] 설명자 레코드에 대 한 SQL_DESC_NAME 필드를 반환 하는 버퍼에 대 한 포인터입니다.  
  
 경우 *이름* 이 NULL 이면 *StringLengthPtr* 는 문자 (문자 데이터에 대 한 null 종결 문자 제외)의 총 수를 반환 여전히 가리키는버퍼에반환하는사용할수 *이름*합니다.  
  
 *BufferLength*  
 [입력] 길이 **이름* 문자에서 버퍼입니다.  
  
 *StringLengthPtr*  
 [출력] 반환 하려면 사용할 수 있는 데이터의 문자 수를 반환 하는 버퍼에 대 한 포인터는 \* *이름* 버퍼에 null 종결 문자를 제외 합니다. 문자 개수 보다 크거나 되었는지 *BufferLength*, 데이터에 \* *이름* 잘립니다 *BufferLength* 의 길이 만큼 뺀 길이로 null 종결 문자는 드라이버에서 null로 종결 되 고 있습니다.  
  
 *TypePtr*  
 [출력] 설명자 레코드에 대 한 SQL_DESC_TYPE 필드의 값을 반환 하는 버퍼에 대 한 포인터입니다.  
  
 *SubTypePtr*  
 [출력] 해당 형식이 SQL_DATETIME 또는 sql_interval 인 레코드의 값을 SQL_DESC_DATETIME_INTERVAL_CODE 필드의 값을 버퍼에 대 한 포인터입니다.  
  
 *LengthPtr*  
 [출력] 설명자 레코드에 대 한 SQL_DESC_OCTET_LENGTH 필드의 값을 반환 하는 버퍼에 대 한 포인터입니다.  
  
 *PrecisionPtr*  
 [출력] 설명자 레코드에 대 한 SQL_DESC_PRECISION 필드의 값을 반환 하는 버퍼에 대 한 포인터입니다.  
  
 *ScalePtr*  
 [출력] 설명자 레코드에 대 한 SQL_DESC_SCALE 필드의 값을 반환 하는 버퍼에 대 한 포인터입니다.  
  
 *NullablePtr*  
 [출력] 설명자 레코드에 대 한 SQL_DESC_NULLABLE 필드의 값을 반환 하는 버퍼에 대 한 포인터입니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_NO_DATA, 또는 SQL_INVALID_HANDLE 합니다.  
  
 경우 SQL_NO_DATA가 반환 *RecNumber* 현재 설명자 레코드 개수 보다 큽니다.  
  
 경우 SQL_NO_DATA가 반환 *DescriptorHandle* 은 IRD 핸들 및 문이 준비 또는 실행 된 상태의 가져왔지만 했습니다 관련 된 열린 커서가 없습니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLGetDescRec** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 관련된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 와 *HandleType* SQL_의 HANDLE_DESC 및 *처리* 의 *DescriptorHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLGetDescRec** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|버퍼 \* *이름* 충분히 전체 설명자 필드를 반환할 수 없습니다. 따라서 필드가 잘렸습니다. 잘리지 않은 설명자 필드의 길이에서 **StringLengthPtr*합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|07009|잘못 된 설명자 인덱스입니다.|*FieldIdentifier* 레코드 필드에 인수가 *RecNumber* 인수는 0으로 설정 된 및 *DescriptorHandle* IPD 핸들 되었습니다.<br /><br /> DM ()는 *RecNumber* 인수가 0으로 설정 되어 있고 SQL_ATTR_USE_BOOKMARKS 문 특성 SQL_UB_OFF로 설정 되었다면 및 *DescriptorHandle* IRD 핸들 되었습니다.<br /><br /> *RecNumber* 인수가 0 보다 작습니다.|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버 연결 된 데이터 원본 간에 통신 링크 하지 못했습니다.|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY007|관련 된 문이 준비 되지 않았습니다.|*DescriptorHandle* IRD, 연관 된 및 관련 된 문 핸들이 준비 또는 실행 된 상태가 아닙니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM) *DescriptorHandle* 연결 된 한 *StatementHandle* 는, 비동기적으로 실행 중인 (하지이 하나)를 호출한 함수와이 함수가 호출 될 때 계속 실행에 대 한 합니다.<br /><br /> (DM) *DescriptorHandle* 연결 된 한 *StatementHandle* 를 **SQLExecute**, **SQLExecDirect**,  **SQLBulkOperations**, 또는 **SQLSetPos** 호출 했으나 SQL_NEED_DATA를 반환 했습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 보내기 전에 호출 되었습니다.<br /><br /> DM ()는 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한는 *DescriptorHandle*합니다. 이 비동기 함수 계속 실행 될 때 **SQLGetDescRec** 호출 되었습니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 드라이버와 관련 된 *DescriptorHandle* 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 응용 프로그램에서 호출할 수 **SQLGetDescRec** 단일 열 또는 매개 변수 설명자 필드의 값을 검색 합니다.  
  
-   SQL_DESC_NAME  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE (형식이 SQL_DATETIME 또는 sql_interval 인 변수인 레코드)  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_NULLABLE  
  
 **SQLGetDescRec** 헤더 필드에 대 한 값을 검색 하지 않습니다.  
  
 응용 프로그램 필드를 null 포인터에 해당 하는 인수를 설정 하 여 필드의 설정 반환 하지 못할 수 있습니다.  
  
 응용 프로그램 호출 하는 경우 **SQLGetDescRec** 특정 설명자 형식에 대 한 정의 되지 않은 필드의 값을 검색 하려면 함수는 SQL_SUCCESS를 반환 하지만 필드에 대해 반환 되는 값 정의 되지 않습니다. 예를 들어 호출 **SQLGetDescRec** APD 또는 카드가 SQL_DESC_NAME 또는 SQL_DESC_NULLABLE 필드에 대 한는 SQL_SUCCESS 하지만 필드에 대 한 정의 되지 않은 값 반환 합니다.  
  
 응용 프로그램 호출 하는 경우 **SQLGetDescRec** 하지만 특정 설명자 형식에 대해 정의 된 기본값은 없습니다 및 아직 설정 되지 않은 필드의 값을 검색 하려면 함수는 SQL_SUCCESS를 반환 하지만 대해 반환 되는 값 필드 정의 되지 않습니다. 자세한 내용은의 "초기화의 설명자 필드" 참조 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)합니다.  
  
 필드의 값을 검색할 수도 있습니다 개별적으로 호출 하 여 **SQLGetDescField**합니다. 설명자 헤더 또는 레코드의 필드에 대 한 참조 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)합니다. 설명자에 대 한 자세한 내용은 참조 [설명자](../../../odbc/reference/develop-app/descriptors.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|열 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|매개 변수 바인딩|[SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|설명자 필드 가져오기|[SQLGetDescField 함수](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|여러 설명자 필드 설정|[SQLSetDescRec 함수](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
