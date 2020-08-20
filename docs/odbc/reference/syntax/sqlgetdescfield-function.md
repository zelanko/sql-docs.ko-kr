---
description: SQLGetDescField 함수(SQLGetDescField Function)
title: SQLGetDescField 함수 | Microsoft Docs
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
ms.openlocfilehash: 31618ca5283ae6875cb4243cc88e643452cef4d1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461069"
---
# <a name="sqlgetdescfield-function"></a>SQLGetDescField 함수(SQLGetDescField Function)
**규칙**  
 소개 된 버전: ODBC 3.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLGetDescField** 은 설명자 레코드의 단일 필드에 대 한 현재 설정 또는 값을 반환 합니다.  
  
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
 입력 설명자 핸들입니다.  
  
 *RecNumber*  
 입력 응용 프로그램에서 정보를 검색 하는 설명자 레코드를 나타냅니다. 설명자 레코드의 번호는 0에서, 레코드 번호 0은 책갈피 레코드입니다. *FieldIdentifier* 인수가 헤더 필드를 나타내는 경우에는 *값* 이 무시 됩니다. *값* 이 SQL_DESC_COUNT 보다 작거나 같지만 행에 열 또는 매개 변수에 대 한 데이터가 포함 되어 있지 않은 경우 **SQLGetDescField** 를 호출 하면 필드의 기본값이 반환 됩니다. 자세한 내용은 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)의 "설명자 필드 초기화"를 참조 하십시오.  
  
 *FieldIdentifier*  
 입력 값을 반환할 설명자의 필드를 나타냅니다. 자세한 내용은 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)의 "*FieldIdentifier* 인수" 섹션을 참조 하세요.  
  
 *ValuePtr*  
 출력 설명자 정보를 반환할 버퍼에 대 한 포인터입니다. 데이터 형식은 *FieldIdentifier*의 값에 따라 달라 집니다.  
  
 *Valueptr* 이 정수 형식이 면 응용 프로그램에서이 함수를 호출 하기 전에 SQLULEN의 버퍼를 사용 하 고이 32 함수를 호출 하기 전에 값을 0으로 초기화 해야 합니다.  
  
 *Valueptr* 이 NULL 인 경우 *StringLengthPtr* 는 해당 값을 가리키는 버퍼에서 반환 하는 데 사용할 수 있는 총 바이트 수 (문자 데이터의 NULL 종료 문자 제외)를 반환 *합니다.*  
  
 *BufferLength*  
 입력 *FieldIdentifier* 가 ODBC에 정의 된 필드이 고 *요소 문자열이* 나 이진 버퍼를 가리키는 경우이 인수는이 인수의 길이 여야 합니다 \* *ValuePtr*. *FieldIdentifier* 가 ODBC에 정의 된 필드이 고 이상 \* 값 *Eptr* 이 정수 이면 *bufferlength* 는 무시 됩니다. **SQLGetDescFieldW**를 호출할 때 값 * \* Eptr* 의 값이 유니코드 데이터 형식이 면 *bufferlength* 인수는 짝수 여야 합니다.  
  
 *FieldIdentifier* 가 드라이버 정의 필드인 경우 응용 프로그램은 *bufferlength* 인수를 설정 하 여 필드의 특성을 드라이버 관리자에 게 표시 합니다. *Bufferlength* 에는 다음 값을 사용할 수 있습니다.  
  
-   * \* Valueptr* 이 문자열에 대 한 포인터인 경우 *bufferlength* 는 문자열 또는 SQL_NTS의 길이입니다.  
  
-   * \* Valueptr* 이 이진 버퍼에 대 한 포인터인 경우 응용 프로그램은 SQL_LEN_BINARY_ATTR (*길이*) 매크로의 결과를 *bufferlength*로 배치 합니다. 그러면 음수 값이 *Bufferlength*에 배치 됩니다.  
  
-   * \* Valueptr* 이 문자열 또는 이진 문자열이 아닌 값에 대 한 포인터인 경우 *bufferlength* 의 값은 SQL_IS_POINTER 이어야 합니다.  
  
-   * \* Valueptr* 에 고정 길이 데이터 형식이 포함 된 경우 *bufferlength* 는 SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT 또는 SQL_IS_USMALLINT 중 하나입니다.  
  
 *StringLengthPtr*  
 출력 **Valueptr*에서 반환 하는 데 사용할 수 있는 총 바이트 수 (null 종결 문자에 필요한 바이트 수 제외)를 반환할 버퍼에 대 한 포인터입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_NO_DATA 또는 SQL_INVALID_HANDLE입니다.  
  
 *값* 이 현재 설명자 레코드 수보다 많은 경우 SQL_NO_DATA 반환 됩니다.  
  
 *DescriptorHandle* 가 IRD 핸들이 고 문이 준비 됨 또는 실행 됨 상태 이지만 연결 된 열린 커서가 없는 경우 SQL_NO_DATA 반환 됩니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetDescField** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 SQL_HANDLE_STMT의 *HandleType* 및 *StatementHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **SQLGetDescField** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01004|문자열 데이터, 오른쪽이 잘렸습니다.|Buffer \* *valueptr* 이 전체 설명자 필드를 반환 하기에 충분 하지 않아 필드가 잘렸습니다. 잘린 설명자 필드의 길이는 **StringLengthPtr*에서 반환 됩니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|07009|잘못 된 설명자 인덱스|(DM *) 인수는 0이 고,* SQL_ATTR_USE_BOOKMARK statement 특성이 SQL_UB_OFF 되었으며, *DescriptorHandle* 인수가 IRD 핸들입니다. 설명자가 문 핸들과 연결 된 경우에만 명시적으로 할당 된 설명자에 대해이 오류가 반환 될 수 있습니다.<br /><br /> *FieldIdentifier* 인수는 레코드 필드이 고, 인수 *는 0* 이 고, *DescriptorHandle* 인수는 IPD 핸들입니다.<br /><br /> 인수 *인수가* 0 보다 작은 경우|  
|08S01|통신 연결 오류|드라이버가 연결 된 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. * \* MessageText* 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버가 실행 또는 함수의 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY007|연결 된 문이 준비 되지 않았습니다.|*DescriptorHandle* 가 *StatementHandle* 와 연결 되어 있고 연결 된 문 핸들이 준비 또는 실행 되지 않았습니다.|  
|HY010|함수 시퀀스 오류|(DM) *DescriptorHandle* 가이 함수를 호출 하지 않고 비동기적으로 실행 되는 함수를 호출 하 고이 함수가 호출 될 때 실행 되는 *StatementHandle* 와 연결 되었습니다.<br /><br /> (DM) *DescriptorHandle* 는 **sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 를 호출 하 고 SQL_NEED_DATA 반환 하는 *StatementHandle* 와 연결 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.<br /><br /> (DM) *DescriptorHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. **SQLGetDescField** 함수가 호출 될 때이 비동기 함수는 계속 실행 중입니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY021|일관 되지 않은 설명자 정보|SQL_DESC_TYPE 및 SQL_DESC_DATETIME_INTERVAL_CODE 필드는 올바른 ODBC SQL 유형, 올바른 드라이버별 SQL 유형 (IPDs의 경우) 또는 유효한 ODBC C 유형 (APDs 또는 ARDs의 경우)이 아닙니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|(DM) * \* 값이 문자열이* 고 *bufferlength* 가 0 보다 작은 경우|  
|HY091|잘못 된 설명자 필드 식별자입니다.|*FieldIdentifier* 가 ODBC에 정의 된 필드가 아니므로 구현에 정의 된 값이 아닙니다.<br /><br /> *FieldIdentifier* 가 *DescriptorHandle*에 대해 정의 되지 않았습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *DescriptorHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 응용 프로그램은 **SQLGetDescField** 를 호출 하 여 설명자 레코드의 단일 필드 값을 반환할 수 있습니다. **SQLGetDescField** 에 대 한 호출은 헤더 필드, 레코드 필드 및 책갈피 필드를 포함 하 여 모든 설명자 형식의 필드에 대 한 설정을 반환할 수 있습니다. 응용 프로그램은 **SQLGetDescField**를 반복 해 서 호출 하 여 동일한 문이나 다른 설명자의 여러 필드에 대 한 설정을 임의의 순서로 가져올 수 있습니다. **SQLGetDescField** 를 호출 하 여 드라이버 정의 설명자 필드를 반환할 수도 있습니다.  
  
 성능상의 이유로 응용 프로그램은 문을 실행 하기 전에 IRD에 대 한 **SQLGetDescField** 를 호출 하지 않아야 합니다.  
  
 **SQLGetDescRec**에 대 한 단일 호출에서 열 또는 매개 변수 데이터의 이름, 데이터 형식 및 저장소를 설명 하는 여러 필드의 설정을 검색할 수도 있습니다. **SQLGetStmtAttr** 를 호출 하 여 설명자 헤더에 있는 단일 필드의 설정 (문 특성 이기도 함)을 반환할 수 있습니다. **Sqlcolattribute**, **SQLDescribeCol**및 **SQLDescribeParam** 반환 레코드 또는 책갈피 필드입니다.  
  
 응용 프로그램에서 **SQLGetDescField** 를 호출 하 여 특정 설명자 형식에 대해 정의 되지 않은 필드의 값을 검색 하는 경우이 함수는 SQL_SUCCESS를 반환 하지만 필드에 대해 반환 된 값은 정의 되지 않습니다. 예를 들어 APD의 SQL_DESC_NAME 또는 SQL_DESC_NULLABLE 필드에 대해 **SQLGetDescField** 를 호출 하면 SQL_SUCCESS 반환 되지만 필드에 대해 정의 되지 않은 값이 반환 됩니다.  
  
 응용 프로그램에서 **SQLGetDescField** 를 호출 하 여 특정 설명자 형식에 대해 정의 되었지만 기본값이 없고 아직 설정 되지 않은 필드의 값을 검색 하는 경우 함수는 SQL_SUCCESS를 반환 하지만 필드에 대해 반환 된 값은 정의 되지 않습니다. 설명자 필드와 필드에 대 한 설명을 초기화 하는 방법에 대 한 자세한 내용은 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)의 "설명자 필드 초기화"를 참조 하십시오. 설명자에 대 한 자세한 내용은 [설명자](../../../odbc/reference/develop-app/descriptors.md)를 참조 하십시오.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|여러 설명자 필드 가져오기|[SQLGetDescRec 함수](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|단일 설명자 필드 설정|[SQLSetDescField 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|여러 설명자 필드 설정|[SQLSetDescRec 함수](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
