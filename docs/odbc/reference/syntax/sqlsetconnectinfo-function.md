---
title: SQLSetConnectInfo 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 448b0f5e34a6b7421c23a1267dd9cd68bd93ca6f
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537176"
---
# <a name="sqlsetconnectinfo-function"></a>SQLSetConnectInfo 함수
**규칙**  
 도입 된 버전: ODBC 3.81 표준 준수 합니다. ODBC  
  
 **요약**  
 **SQLSetConnectInfo** 응용 프로그램에 대 한 연결 정보 토큰으로 데이터 원본, 사용자 ID 및 암호를 설정 하는 데 사용 됩니다 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 호출 합니다.  
  
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
 *TokenHandle*  
 [입력] 토큰 핸들입니다.  
  
 *데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면*  
 [입력] 데이터 원본 이름입니다. 데이터는 프로그램과 동일한 컴퓨터 또는 네트워크에서 다른 컴퓨터에 있을 수 있습니다. 응용 프로그램에서 데이터 소스를 선택 하는 방법에 대 한 자세한 내용은 [데이터 원본 또는 드라이버 선택](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)합니다.  
  
 *NameLength1*  
 [입력] 길이 **ServerName* 문자에서입니다.  
  
 *UserName*  
 [입력] 사용자 식별자입니다.  
  
 *NameLength2*  
 [입력] 길이 **UserName* 문자에서입니다.  
  
 *인증*  
 [입력] 인증 문자열 (일반적으로 암호)입니다.  
  
 *NameLength3*  
 [입력] 길이 **인증* 문자에서입니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 동일 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 에 대 한 드라이버 관리자를 사용 한다는 점을 제외 하면 유효성 검사 오류를 입력 한 **HandleType** SQL_HANDLE_DBC_INFO_TOKEN의와 **처리** 의*hDbcInfoToken*합니다.  
  
## <a name="remarks"></a>Remarks  
 드라이버는 SQL_ERROR 또는 SQL_INVALID_HANDLE 반환 될 때마다 응용 프로그램에 드라이버 관리자 오류를 반환 합니다 (에서 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 하거나 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 드라이버에서 SQL_SUCCESS_WITH_INFO를 반환할 때마다 드라이버 관리자에서 진단 정보를 가져옵니다 *hDbcInfoToken*, 응용 프로그램에 SQL_SUCCESS_WITH_INFO를 반환 하 고 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)하 고 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)합니다.  
  
 응용 프로그램에서이 함수를 직접 호출 하지 않습니다. 드라이버 인식 연결 풀링을 지 원하는 ODBC 드라이버는이 함수를 구현 해야 합니다.  
  
 ODBC 드라이버 개발을 위한 sqlspi.h 포함 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
