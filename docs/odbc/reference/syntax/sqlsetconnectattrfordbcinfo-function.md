---
title: SQLSetConnectAttrForDbcInfo 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLSetConnectAttrForDbcInfo function [ODBC]
ms.assetid: a28fadb9-b998-472a-b252-709507e92005
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8ef62393ac00b7d094e6ba47613038fdf7ac2175
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlsetconnectattrfordbcinfo-function"></a>SQLSetConnectAttrForDbcInfo 함수
**규칙**  
 도입 된 버전: ODBC 3.81 표준 준수: ODBC  
  
 **요약**  
 **SQLSetConnectAttrForDbcInfo** 동일 **SQLSetConnectAttr**, 하지만 연결 핸들에 연결 정보 토큰 대신에 특성을 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
SQLRETURN  SQLSetConnectAttrForDbcInfo(  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                SQLINTEGER            Attribute,  
                SQLPOINTER            ValuePtr,  
                SQLINTEGER            StringLength );  
```  
  
## <a name="arguments"></a>인수  
 *hDbcInfoToken*  
 [입력] 토큰 핸들입니다.  
  
 *Attribute*  
 [입력] 설정할 특성입니다. 유효한 특성 목록에는 특정 드라이버와 동일 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)합니다.  
  
 *ValuePtr*  
 [입력] 연결 된 값에 대 한 포인터 *특성*합니다. 값에 따라 *특성*, *ValuePtr* 32 비트 부호 없는 정수 값 또는 null로 끝나는 문자열을 가리킵니다. 되는 경우는 *특성* 인수는 드라이버 관련 값, 값에 *ValuePtr* 부호 있는 정수를 수 있습니다.  
  
 *StringLength*  
 [입력] 경우 *특성* 은 ODBC 정의 된 특성 및 *ValuePtr* 문자열 또는 이진 버퍼를 가리키거나,이 인수 길이 여야 합니다 **ValuePtr*합니다. 문자 문자열 데이터에 대 한이 인수는 문자열의 바이트 수를 포함 해야 합니다.  
  
 경우 *특성* 은 ODBC 정의 된 특성 및 *ValuePtr* 정수 이면 *StringLength* 는 무시 됩니다.  
  
 경우 *특성* 드라이버에서 정의 된 특성은 응용 프로그램을 설정 하 여 드라이버 관리자 특성의 특성을 나타내는 *StringLength* 인수입니다. *StringLength* 다음 값을 가질 수 있습니다.  
  
-   경우 *ValuePtr* 다음 문자열을에 대 한 포인터는 *StringLength* SQL_NTS 또는 문자열의 길이입니다.  
  
-   경우 *ValuePtr* 이진 버퍼에 대 한 포인터에 있으면 응용 프로그램은 SQL_LEN_BINARY_ATTR의 결과 배치 (*길이*) 매크로에서 *StringLength*합니다. 이렇게 하면 배치에 음수 값 *StringLength*합니다.  
  
-   경우 *ValuePtr* 문자열 또는 이진 문자열 이외의 값에 대 한 포인터는 *StringLength* SQL_IS_POINTER 값이 있어야 합니다.  
  
-   경우 *ValuePtr* 고정 길이 값이 다음 포함 *StringLength* 되었거나 SQL_IS_INTEGER SQL_IS_UINTEGER를 적절 하 게 합니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 와 동일 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)제외 드라이버 관리자에서 사용 하는 **HandleType** SQL_HANDLE_DBC_INFO_TOKEN의 및 **처리** 의 *hDbcInfoToken* .  
  
## <a name="remarks"></a>주의  
 **SQLSetConnectAttrForDbcInfo** 동일 **SQLSetConnectAttr**, 하지만 연결 핸들에 연결 정보 토큰에 있는 특성 대신 설정 합니다. 예를 들어 경우 **SQLSetConnectAttr** 특성을 인식 하지 않으므로 **SQLSetConnectAttrForDbcInfo** 해당 특성에 대 한도 SQL_ERROR를 반환 해야 합니다.  
  
 드라이버 풀 ID를 계산 하려면이 특성을 무시 해야 드라이버가 SQL_ERROR 또는 SQL_INVALID_HANDLE 반환 될 때마다 또한 드라이버 관리자의 진단 정보를 가져옵니다 *hDbcInfoToken*, 응용 프로그램에 sql_success_with_info가 반환 하 고 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 및 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md). 따라서 응용 프로그램 일부 특성을 설정할 수 없는 이유는 방법에 대 한 세부 정보를 검색할 수 있습니다.  
  
 응용 프로그램에서이 함수를 직접 호출 하지 않습니다. 드라이버 인식 연결 풀링을 지원 되는 ODBC 드라이버가이 함수를 구현 해야 합니다.  
  
 ODBC 드라이버 개발에 대 한 sqlspi.h를 포함 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC 드라이버를 개발합니다.](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
