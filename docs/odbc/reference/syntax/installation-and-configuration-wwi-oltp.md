---
title: SQLSetDriverConnectInfo 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetDriverConnectInfo function [ODBC]
ms.assetid: bfd4dfc2-fbca-4ef3-81e5-2706f2389256
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 10336475e39598161126c13771ad822de0d5f7d8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298805"
---
# <a name="sqlsetdriverconnectinfo-function"></a>SQLSetDriverConnectInfo 함수
**규칙**  
 버전 출시: ODBC 3.81 표준 준수: ODBC  
  
 **요약**  
 **SQLSetDriverConnectInfo는** 응용 프로그램의 **SQLDriverConnect** 호출에 대 한 연결 정보 토큰에 연결 문자열을 설정 하는 데 사용 됩니다.  
  
## <a name="syntax"></a>구문  
  
```cpp
  
SQLRETURN SQLSetDriverConnectInfo(  
                SQLHDBC_INFO_TOKEN   hDbcInfoToken,  
                WCHAR *              InConnectionString,  
                SQLSMALLINT          StringLength1 );  
```  
  
## <a name="arguments"></a>인수  
 *토큰 핸들*  
 [입력] 토큰 핸들입니다.  
  
 *인커넥션 스트링*  
 [입력] 전체 연결 [문자열(SQLDriverConnect의](../../../odbc/reference/syntax/sqldriverconnect-function.md)"주석"의 구문 참조), 부분 연결 문자열 또는 빈 문자열입니다.  
  
 *문자열 길이1*  
 [입력] **InConnectionString의*길이는 문자열이 유니코드인 경우 문자로, 문자열이 ANSI 또는 DBCS인 경우 바이트입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 드라이버 관리자가 **핸들 SQL_HANDLE_DBC_INFO_TOKEN** *hDbcInfoToken*핸들을 사용 한다는 점을 제외 하 고 입력 유효성 검사 오류와 관련 **된** [SQLDriverConnect와](../../../odbc/reference/syntax/sqldriverconnect-function.md) 동일 합니다.  
  
## <a name="remarks"></a>설명  
 드라이버가 SQL_ERROR 또는 SQL_INVALID_HANDLE 반환할 때마다 드라이버 관리자는 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 또는 [SQLDriverConnect에서](../../../odbc/reference/syntax/sqldriverconnect-function.md)응용 프로그램에 오류를 반환합니다.  
  
 드라이버가 SQL_SUCCESS_WITH_INFO 반환할 때마다 드라이버 관리자는 *hDbcInfoToken에서*진단 정보를 얻고 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 및 [SQLDriverConnect에서](../../../odbc/reference/syntax/sqldriverconnect-function.md)응용 프로그램에 SQL_SUCCESS_WITH_INFO 반환합니다.  
  
 응용 프로그램은 이 함수를 직접 호출해서는 안 됩니다. 드라이버 인식 연결 풀링을 지원하는 ODBC 드라이버는 이 기능을 구현해야 합니다.  
  
 ODBC 드라이버 개발을 위해 sqlspi.h를 포함합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
