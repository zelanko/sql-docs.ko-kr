---
title: SQLSetConnectAttrForDbcInfo 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectAttrForDbcInfo function [ODBC]
ms.assetid: a28fadb9-b998-472a-b252-709507e92005
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9f43a0fc6cd02fe566579a543667f9a4c4c1a108
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301890"
---
# <a name="sqlsetconnectattrfordbcinfo-function"></a>SQLSetConnectAttrForDbcInfo 함수
**규칙**  
 버전 출시: ODBC 3.81 표준 준수: ODBC  
  
 **요약**  
 **SQLSetConnectAttrForDbcInfo는** **SQLSetConnectAttr와**동일하지만 연결 핸들 대신 연결 정보 토큰에 대한 특성을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp
  
SQLRETURN  SQLSetConnectAttrForDbcInfo(  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                SQLINTEGER            Attribute,  
                SQLPOINTER            ValuePtr,  
                SQLINTEGER            StringLength );  
```  
  
## <a name="arguments"></a>인수  
 *hDbcInfo토큰*  
 [입력] 토큰 핸들입니다.  
  
 *특성*  
 [입력] 설정할 특성입니다. 유효한 특성 목록은 드라이버에 따라 다르며 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 *ValuePtr*  
 [입력] *속성에*연결할 값에 대한 포인터 . *특성값에*따라 *ValuePtr은* 32비트 서명되지 않은 정수 값이거나 null 종료된 문자 문자열을 가리킵니다. *특성* 인수가 드라이버 관련 값인 경우 *ValuePtr의* 값은 서명된 정수일 수 있습니다.  
  
 *문자열 길이*  
 [입력] *특성이* ODBC 정의 특성이고 *ValuePtr이* 문자 문자열 또는 이진 버퍼를 가리키는 경우 이 인수는 **ValuePtr*의 길이여야 합니다. 문자열 데이터의 경우 이 인수에는 문자열의 바이트 수가 포함되어야 합니다.  
  
 *특성이* ODBC 정의 특성이고 *ValuePtr이* 정수인 경우 *StringLength는* 무시됩니다.  
  
 *특성이* 드라이버 정의 특성인 경우 응용 프로그램은 *StringLength* 인수를 설정하여 드라이버 관리자에 대한 특성의 특성을 나타냅니다. *StringLength에는* 다음 값이 있을 수 있습니다.  
  
-   *ValuePtr이* 문자열 문자열에 대한 포인터인 경우 *StringLength는* 문자열 또는 SQL_NTS 길이입니다.  
  
-   *ValuePtr이* 이진 버퍼에 대한 포인터인 경우 응용 프로그램은 *stringLength에**SQL_LEN_BINARY_ATTR(길이)* 매크로의 결과를 배치합니다. 그러면 *문자열Length에*음수 값이 배치됩니다.  
  
-   *ValuePtr이* 문자열 또는 이진 문자열 이외 값에 대한 포인터인 경우 *StringLength는* SQL_IS_POINTER 값을 가져야 합니다.  
  
-   *ValuePtr* 고정 길이 값을 포함 하는 경우 *StringLength는* SQL_IS_INTEGER 또는 SQL_IS_UINTEGER 적절 하 게.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)SQL_HANDLE_DBC_INFO_TOKEN와 동일합니다. **HandleType** **Handle** *hDbcInfoToken*  
  
## <a name="remarks"></a>설명  
 **SQLSetConnectAttrForDbcInfo는** **SQLSetConnectAttr과**동일하지만 연결 핸들 대신 연결 정보 토큰에 특성을 설정합니다. 예를 들어 **SQLSetConnectAttr 특성을** 인식하지 못하는 경우 **SQLSetConnectAttrForDbcInfo도** 해당 특성에 대한 SQL_ERROR 반환해야 합니다.  
  
 드라이버가 SQL_ERROR 반환하거나 SQL_INVALID_HANDLE 때마다 드라이버는 이 특성을 무시하고 풀 ID를 계산해야 합니다. 또한 드라이버 관리자는 *hDbcInfoToken에서*진단 정보를 가져오고 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 및 [SQLDriverConnect의](../../../odbc/reference/syntax/sqldriverconnect-function.md)응용 프로그램에 SQL_SUCCESS_WITH_INFO 반환합니다. 따라서 응용 프로그램은 일부 특성을 설정할 수 없는 이유에 대한 세부 정보를 검색할 수 있습니다.  
  
 응용 프로그램은 이 함수를 직접 호출해서는 안 됩니다. 드라이버 인식 연결 풀링을 지원하는 ODBC 드라이버는 이 기능을 구현해야 합니다.  
  
 ODBC 드라이버 개발을 위해 sqlspi.h를 포함합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
