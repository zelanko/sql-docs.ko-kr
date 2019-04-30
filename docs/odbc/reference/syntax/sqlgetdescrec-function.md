---
title: SQLGetDescRec 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2f8c585bc758b74c666c8da625c1e57af7af2582
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63258797"
---
# <a name="sqlgetdescrec-function"></a>SQLGetDescRec 함수
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수 합니다. ISO 92  
  
 **요약**  
 **SQLGetDescRec** 설명자 레코드의 여러 필드의 값을 현재 설정을 반환 합니다. 반환 되는 필드 이름, 데이터 형식 및 열 또는 매개 변수 데이터의 저장소를 설명 합니다.  
  
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
 [입력] 응용 프로그램 정보를 검색 하는 설명자 레코드를 나타냅니다. 설명자 레코드는 레코드 번호 0 책갈피 레코드를 사용 하 여 1부터 번호가 지정 됩니다. 합니다 *RecNumber* SQL_DESC_COUNT 값 보다 작거나 같은 인수 여야 합니다. 하는 경우 *RecNumber* 되었지만 SQL_DESC_COUNT 보다 작거나 같은 행에 열 또는 매개 변수에 대 한 호출에 대 한 데이터가 없습니다 **SQLGetDescRec** 필드의 기본값을 반환 합니다. (자세한 내용은 "설명자 필드의 초기화"를 참조 하세요 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
 *이름*  
 [출력] 설명자 레코드에 대 한 SQL_DESC_NAME 필드를 반환할 버퍼에 대 한 포인터입니다.  
  
 하는 경우 *이름을* 가 null 인 경우 *StringLengthPtr* (문자 데이터에 대 한 null 종료 문자를 제외한) 문자의 총 수를 반환 계속 됩니다 가리키는버퍼에서반환할사용가능한 *이름*합니다.  
  
 *BufferLength*  
 [입력] 길이 **이름을* 문자에서 버퍼입니다.  
  
 *StringLengthPtr*  
 [출력] 반환할 사용 가능한 데이터의 문자 수를 반환 하는 버퍼에 대 한 포인터를 \* *이름* 버퍼를 null 종료 문자를 제외 합니다. 문자 개수 보다 크거나 같은 경우 *BufferLength*에 있는 데이터 \* *이름* 잘립니다 *BufferLength* 의 길이 뺀 값을 null 종료 문자 및 드라이버에 의해 null로 종결 됩니다.  
  
 *TypePtr*  
 [출력] 설명자 레코드에 대 한 SQL_DESC_TYPE 필드의 값을 반환 하는 버퍼에 대 한 포인터입니다.  
  
 *SubTypePtr*  
 [출력] 해당 형식이 SQL_DATETIME 또는 sql_interval 인 레코드 값을 SQL_DESC_DATETIME_INTERVAL_CODE 필드의 값을 반환 하는 버퍼에 대 한 포인터입니다.  
  
 *LengthPtr*  
 [출력] 설명자 레코드에 대 한 SQL_DESC_OCTET_LENGTH 필드의 값을 반환 하는 버퍼에 대 한 포인터입니다.  
  
 *PrecisionPtr*  
 [출력] 설명자 레코드에 대 한 SQL_DESC_PRECISION 필드의 값을 반환 하는 버퍼에 대 한 포인터입니다.  
  
 *ScalePtr*  
 [출력] 설명자 레코드에 대 한 자릿수가 SQL_DESC_SCALE 필드의 값을 반환 하는 버퍼에 대 한 포인터입니다.  
  
 *NullablePtr*  
 [출력] 설명자 레코드에 대 한 SQL_DESC_NULLABLE 필드의 값을 반환 하는 버퍼에 대 한 포인터입니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR에서 SQL_NO_DATA를 또는 SQL_INVALID_HANDLE 합니다.  
  
 경우 SQL_NO_DATA가 반환 *RecNumber* 현재 설명자 레코드 개수 보다 큽니다.  
  
 경우 SQL_NO_DATA가 반환 *DescriptorHandle* IRD 핸들 및 문을 상태인 준비 또는 실행 되었지만 연결 된 열린 커서가 없습니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLGetDescRec** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* SQL_의 HANDLE_DESC와 *처리할* 의 *DescriptorHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLGetDescRec** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|버퍼 \* *이름을* 충분히 전체 설명자 필드를 반환할 수 없습니다. 따라서 필드가 잘렸습니다. 잘리지 않은 설명자 필드의 길이에서 **StringLengthPtr*합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|07009|잘못 된 설명자 인덱스입니다.|합니다 *FieldIdentifier* 인수가 레코드 필드를 *RecNumber* 인수를 0으로 설정 된 및 *DescriptorHandle* 인수가 IPD 핸들을 합니다.<br /><br /> (DM)는 *RecNumber* 인수가 0으로 설정 되어 있고 SQL_ATTR_USE_BOOKMARKS 문 특성 SQL_UB_OFF로 설정 되었다면 하며 *DescriptorHandle* 인수가 IRD 핸들을 합니다.<br /><br /> 합니다 *RecNumber* 인수가 0 보다 작습니다.|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버는 연결 된 데이터 원본 간의 통신 링크 하지 못했습니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 실행 또는 완료 함수를 지원 하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY007|연결 된 문이 준비 되지 않았습니다.|*DescriptorHandle* IRD, 연관 된 및 관련된 문 핸들 준비 또는 실행 상태가 없습니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM) *DescriptorHandle* 연관 된를 *StatementHandle* 는 비동기적으로 실행 중인 (이 없는 항목)를 호출한 함수와이 함수가 호출 되었을 때 계속 실행에 대 한 합니다.<br /><br /> (DM) *DescriptorHandle* 연관 된를 *StatementHandle* 입니다 **SQLExecute**를 **SQLExecDirect**,  **SQLBulkOperations**, 또는 **SQLSetPos** 호출 되 고 SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한 합니다 *DescriptorHandle*합니다. 이 비동기 함수가 계속 실행 될 때 **SQLGetDescRec** 호출 되었습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)와 연결 된 드라이버가 *DescriptorHandle* 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 응용 프로그램에서 호출할 수 있습니다 **SQLGetDescRec** 단일 열 또는 매개 변수 설명자 필드의 값을 검색 합니다.  
  
-   SQL_DESC_NAME  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE (형식이 SQL_DATETIME 또는 SQL_INTERVAL 인 레코드)  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_NULLABLE  
  
 **SQLGetDescRec** 헤더 필드 값을 검색 하지 않습니다.  
  
 응용 프로그램 필드를 null 포인터에 해당 하는 인수를 설정 하 여 필드의 설정 반환을 방지할 수 있습니다.  
  
 응용 프로그램을 호출할 때 **SQLGetDescRec** 특정 설명자 형식에 대해 정의 되지 않은 필드의 값을 검색할 함수는 SQL_SUCCESS를 반환 하지만 필드에 대해 반환 되는 값이 정의 되지 않습니다. 예를 들어, 호출 **SQLGetDescRec** APD 또는 카드가 SQL_DESC_NAME 또는 SQL_DESC_NULLABLE 필드는 SQL_SUCCESS 되지만 정의 되지 않은 필드 값을 반환 합니다.  
  
 응용 프로그램을 호출할 때 **SQLGetDescRec** 특정 설명자 형식에 대해 정의 되는 있지만 기본값이 없으며을 아직 설정 되지 않은 필드의 값을 검색할 함수는 SQL_SUCCESS를 반환 하지만 대 한 반환 값 필드 정의 되지 않습니다. 자세한 내용은 "설명자 필드의 초기화"를 참조 하세요 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)합니다.  
  
 호출 하 여 필드의 값을 개별적으로 검색할 수도 있습니다 **SQLGetDescField**합니다. 설명자 헤더 또는 레코드의 필드 설명을 참조 하세요 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)합니다. 설명자에 대 한 자세한 내용은 참조 하세요. [설명자](../../../odbc/reference/develop-app/descriptors.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|열 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|매개 변수 바인딩|[SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|설명자 필드 가져오기|[SQLGetDescField 함수](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|여러 설명자 필드 설정|[SQLSetDescRec 함수](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
