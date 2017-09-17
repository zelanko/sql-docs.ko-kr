---
title: "SQLSetConnectInfo 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLSetConnectInfo function [ODBC]
ms.assetid: 0782a1c3-c5d1-499b-a8ba-134162db9990
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6e4c974a8cf4bb46f955ec8f2bae0a766f58f692
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetconnectinfo-function"></a>SQLSetConnectInfo 함수
**규칙**  
 도입 된 버전: ODBC 3.81 표준 준수: ODBC  
  
 **요약**  
 **SQLSetConnectInfo** 응용 프로그램에 대 한 연결 정보 토큰으로 데이터 원본, 사용자 ID 및 암호를 설정 하는 데는 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 호출 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
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
 *TokenHandle*  
 [입력] 토큰 핸들입니다.  
  
 *데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면*  
 [입력] 데이터 원본 이름입니다. 데이터에는 프로그램과 동일한 컴퓨터에서 또는 네트워크의 임의 위치에서 다른 컴퓨터에 있을 수 있습니다. 응용 프로그램에서 데이터 소스를 선택 하는 방법에 대 한 정보를 참조 하십시오. [데이터 원본이 나 드라이버 선택](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)합니다.  
  
 *NameLength1*  
 [입력] 길이 **ServerName* 문자 수입니다.  
  
 *UserName*  
 [입력] 사용자 식별자입니다.  
  
 *NameLength2*  
 [입력] 길이 **UserName* 문자 수입니다.  
  
 *인증*  
 [입력] 인증 문자열 (일반적으로 암호)입니다.  
  
 *NameLength3*  
 [입력] 길이 **인증* 문자 수입니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 와 동일 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 에 대 한 드라이버 관리자가 사용할 제외 하 고 유효성 검사 오류를 입력 한 **HandleType** SQL_HANDLE_DBC_INFO_TOKEN의 및 **처리** 의*hDbcInfoToken*합니다.  
  
## <a name="remarks"></a>주의  
 드라이버 관리자 응용 프로그램에 오류를 반환 하는 드라이버 SQL_ERROR 또는 SQL_INVALID_HANDLE 반환 될 때마다 (에서 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 또는 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 드라이버 관리자의 진단 정보를 가져옵니다는 드라이버에서 SQL_SUCCESS_WITH_INFO를 반환할 때마다 *hDbcInfoToken*, 응용 프로그램에 sql_success_with_info가 반환 하 고 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)및 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)합니다.  
  
 응용 프로그램에서이 함수를 직접 호출 하지 않습니다. 드라이버 인식 연결 풀링을 지원 되는 ODBC 드라이버가이 함수를 구현 해야 합니다.  
  
 ODBC 드라이버 개발에 대 한 sqlspi.h를 포함 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC 드라이버를 개발합니다.](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
