---
description: SQLGetDescRec 함수
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5237d8b1a1d070752219abd22936615060371a89
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461053"
---
# <a name="sqlgetdescrec-function"></a>SQLGetDescRec 함수
**규칙**  
 소개 된 버전: ODBC 3.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLGetDescRec** 은 설명자 레코드의 여러 필드에 대 한 현재 설정이 나 값을 반환 합니다. 반환 된 필드는 열 또는 매개 변수 데이터의 이름, 데이터 형식 및 저장을 설명 합니다.  
  
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
 입력 설명자 핸들입니다.  
  
 *RecNumber*  
 입력 응용 프로그램에서 정보를 검색 하는 설명자 레코드를 나타냅니다. 설명자 레코드의 번호는 1 이며 레코드 번호 0은 책갈피 레코드입니다. 지 *수* 인수는 SQL_DESC_COUNT 값 보다 작거나 같아야 합니다. *값* 이 SQL_DESC_COUNT 보다 작거나 같지만 행에 열 또는 매개 변수에 대 한 데이터가 포함 되어 있지 않은 경우 **SQLGetDescRec** 를 호출 하면 필드의 기본값이 반환 됩니다. 자세한 내용은 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)의 "설명자 필드 초기화"를 참조 하십시오.  
  
 *이름*  
 출력 설명자 레코드에 대 한 SQL_DESC_NAME 필드를 반환할 버퍼에 대 한 포인터입니다.  
  
 *Name* 이 NULL 인 경우 *StringLengthPtr* 는 *이름*으로 가리키는 버퍼에서 반환 하는 데 사용할 수 있는 문자 데이터의 NULL 종료 문자를 제외 하 고 전체 문자 수를 반환 합니다.  
  
 *BufferLength*  
 입력 **이름* 버퍼의 길이 (문자)입니다.  
  
 *StringLengthPtr*  
 출력 Null 종료 문자를 제외 하 고 이름 버퍼에서 반환할 수 있는 데이터의 문자 수를 반환할 버퍼에 대 한 포인터 \* *Name* 입니다. 문자 수가 *Bufferlength*보다 크거나 같은 경우 \* *이름의* 데이터는 *bufferlength* 에서 null 종료 문자의 길이를 뺀 값으로 잘리고 드라이버에 의해 null로 종료 됩니다.  
  
 *TypePtr*  
 출력 설명자 레코드에 대 한 SQL_DESC_TYPE 필드의 값을 반환할 버퍼에 대 한 포인터입니다.  
  
 *SubTypePtr*  
 출력 형식이 SQL_DATETIME 또는 SQL_INTERVAL 인 레코드의 경우 SQL_DESC_DATETIME_INTERVAL_CODE 필드의 값을 반환 하는 버퍼에 대 한 포인터입니다.  
  
 *LengthPtr*  
 출력 설명자 레코드에 대 한 SQL_DESC_OCTET_LENGTH 필드의 값을 반환할 버퍼에 대 한 포인터입니다.  
  
 *PrecisionPtr*  
 출력 설명자 레코드에 대 한 SQL_DESC_PRECISION 필드의 값을 반환할 버퍼에 대 한 포인터입니다.  
  
 *ScalePtr*  
 출력 설명자 레코드에 대 한 SQL_DESC_SCALE 필드의 값을 반환할 버퍼에 대 한 포인터입니다.  
  
 *NullablePtr*  
 출력 설명자 레코드에 대 한 SQL_DESC_NULLABLE 필드의 값을 반환할 버퍼에 대 한 포인터입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_NO_DATA 또는 SQL_INVALID_HANDLE입니다.  
  
 *값* 이 현재 설명자 레코드 수보다 많은 경우 SQL_NO_DATA 반환 됩니다.  
  
 *DescriptorHandle* 가 IRD 핸들이 고 문이 준비 됨 또는 실행 됨 상태 이지만 연결 된 열린 커서가 없는 경우 SQL_NO_DATA 반환 됩니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetDescRec** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 SQL_HANDLE_DESC의 *HandleType* 및 *DescriptorHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **SQLGetDescRec** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01004|문자열 데이터, 오른쪽이 잘렸습니다.|버퍼 \* *이름이* 작아서 전체 설명자 필드를 반환할 수 없습니다. 따라서 필드가 잘렸습니다. 잘린 설명자 필드의 길이는 **StringLengthPtr*에서 반환 됩니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|07009|잘못 된 설명자 인덱스|*FieldIdentifier* 인수는 레코드 필드이 고, *값* 인수는 0으로 설정 되 고, *DescriptorHandle* 인수는 IPD 핸들입니다.<br /><br /> (DM) 인수는 0으로 설정 되 고 SQL_ATTR_USE_BOOKMARKS statement *특성은 SQL_UB_OFF* 로 설정 되었으며 *DESCRIPTORHANDLE* 인수는 IRD 핸들입니다.<br /><br /> 인수 *인수가* 0 보다 작은 경우|  
|08S01|통신 연결 오류|드라이버가 연결 된 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. * \* MessageText* 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버가 실행 또는 함수의 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY007|연결 된 문이 준비 되지 않았습니다.|*DescriptorHandle* 가 IRD와 연결 되어 있고 연결 된 문 핸들이 준비 됨 또는 실행 됨 상태가 아닙니다.|  
|HY010|함수 시퀀스 오류|(DM) *DescriptorHandle* 가이 함수를 호출 하지 않고 비동기적으로 실행 되는 함수를 호출 하 고이 함수가 호출 될 때 실행 되는 *StatementHandle* 와 연결 되었습니다.<br /><br /> (DM) *DescriptorHandle* 는 **sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 를 호출 하 고 SQL_NEED_DATA 반환 하는 *StatementHandle* 와 연결 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.<br /><br /> (DM) *DescriptorHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. **SQLGetDescRec** 가 호출 될 때이 비동기 함수는 계속 실행 중입니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *DescriptorHandle* 와 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 응용 프로그램은 **SQLGetDescRec** 를 호출 하 여 단일 열 또는 매개 변수에 대 한 다음 설명자 필드의 값을 검색할 수 있습니다.  
  
-   SQL_DESC_NAME  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE (형식이 SQL_DATETIME 또는 SQL_INTERVAL 인 레코드의 경우)  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_NULLABLE  
  
 **SQLGetDescRec** 는 헤더 필드 값을 검색 하지 않습니다.  
  
 응용 프로그램은 필드에 해당 하는 인수를 null 포인터로 설정 하 여 필드 설정의 반환을 방지할 수 있습니다.  
  
 응용 프로그램에서 **SQLGetDescRec** 를 호출 하 여 특정 설명자 형식에 대해 정의 되지 않은 필드의 값을 검색 하는 경우이 함수는 SQL_SUCCESS를 반환 하지만 필드에 대해 반환 된 값은 정의 되지 않습니다. 예를 들어 APD의 SQL_DESC_NAME 또는 SQL_DESC_NULLABLE 필드에 대해 **SQLGetDescRec** 를 호출 하면 SQL_SUCCESS 반환 되지만 필드에 대해 정의 되지 않은 값이 반환 됩니다.  
  
 응용 프로그램에서 **SQLGetDescRec** 를 호출 하 여 특정 설명자 형식에 대해 정의 되었지만 기본값이 없고 아직 설정 되지 않은 필드의 값을 검색 하는 경우 함수는 SQL_SUCCESS를 반환 하지만 필드에 대해 반환 된 값은 정의 되지 않습니다. 자세한 내용은 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)의 "설명자 필드 초기화"를 참조 하십시오.  
  
 **SQLGetDescField**를 호출 하 여 필드 값을 개별적으로 검색할 수도 있습니다. 설명자 헤더 또는 레코드의 필드에 대 한 설명은 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)를 참조 하세요. 설명자에 대 한 자세한 내용은 [설명자](../../../odbc/reference/develop-app/descriptors.md)를 참조 하십시오.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|열 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|매개 변수 바인딩|[SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|설명자 필드 가져오기|[SQLGetDescField 함수](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|여러 설명자 필드 설정|[SQLSetDescRec 함수](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
