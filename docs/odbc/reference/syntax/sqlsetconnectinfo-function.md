---
title: SQLSetConnectInfo 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectInfo function [ODBC]
ms.assetid: 0782a1c3-c5d1-499b-a8ba-134162db9990
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b575e0d09f87ad21e1190b8081b6604349a98263
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301854"
---
# <a name="sqlsetconnectinfo-function"></a>SQLSetConnectInfo 함수
**규칙**  
 버전 출시: ODBC 3.81 표준 준수: ODBC  
  
 **요약**  
 **SQLSetConnectInfo는** 응용 프로그램의 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 호출에 대 한 연결 정보 토큰에 데이터 원본, 사용자 ID 및 암호를 설정 하는 데 사용 됩니다.  
  
## <a name="syntax"></a>구문  
  
```cpp
  
SQLRETURN  SQLSetConnectInfo(  
                SQLHDBC_INFO_TOKEN   TokenHandle,  
                WCHAR *              ServerName,  
                SQLSMALLINT          NameLength1,  
                WCHAR *              UserName,  
                SQLSMALLINT          NameLength2,  
                WCHAR *              Authentication,  
                SQLSMALLINT          NameLength3 );  
```  
  
## <a name="arguments"></a>인수  
 *토큰 핸들*  
 [입력] 토큰 핸들입니다.  
  
 *ServerName*  
 [입력] 데이터 원본 이름입니다. 데이터는 프로그램과 동일한 컴퓨터에 있거나 네트워크의 다른 컴퓨터에 있을 수 있습니다. 응용 프로그램이 데이터 원본을 선택하는 방법에 대한 자세한 내용은 [데이터 원본 또는 드라이버 선택을](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)참조하십시오.  
  
 *NameLength1*  
 [입력] 문자의 ** 서버 이름의* 길이입니다.  
  
 *사용자*  
 [입력] 사용자 식별자입니다.  
  
 *이름 길이2*  
 [입력] * 문자의*사용자 이름* 길이입니다.  
  
 *인증*  
 [입력] 인증 문자열(일반적으로 암호)입니다.  
  
 *이름 길이3*  
 [입력] * 문자*인증의* 길이입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 드라이버 관리자가 **핸들 SQL_HANDLE_DBC_INFO_TOKEN** *hDbcInfoToken*핸들을 사용 한다는 점을 제외 하 고 입력 유효성 검사 오류에 대 **한** [SQLConnect와](../../../odbc/reference/syntax/sqlconnect-function.md) 동일 합니다.  
  
## <a name="remarks"></a>설명  
 드라이버가 SQL_ERROR 또는 SQL_INVALID_HANDLE 반환할 때마다 드라이버 관리자는 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 또는 [SQLDriverConnect에서](../../../odbc/reference/syntax/sqldriverconnect-function.md)응용 프로그램에 오류를 반환합니다.  
  
 드라이버가 SQL_SUCCESS_WITH_INFO 반환할 때마다 드라이버 관리자는 *hDbcInfoToken에서*진단 정보를 얻고 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 및 [SQLDriverConnect에서](../../../odbc/reference/syntax/sqldriverconnect-function.md)응용 프로그램에 SQL_SUCCESS_WITH_INFO 반환합니다.  
  
 응용 프로그램은 이 함수를 직접 호출해서는 안 됩니다. 드라이버 인식 연결 풀링을 지원하는 ODBC 드라이버는 이 기능을 구현해야 합니다.  
  
 ODBC 드라이버 개발을 위해 sqlspi.h를 포함합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
