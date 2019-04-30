---
title: SQLSetDriverConnectInfo 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1c344315764eac32e2e63663f07b7f797571a0e6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63233435"
---
# <a name="sqlsetdriverconnectinfo-function"></a>SQLSetDriverConnectInfo 함수
**규칙**  
 도입 된 버전: ODBC 3.81 표준 준수 합니다. ODBC  
  
 **요약**  
 **SQLSetDriverConnectInfo** 응용 프로그램에 대 한 연결 정보 토큰에 연결 문자열을 설정 하는 데 사용 됩니다 **SQLDriverConnect** 호출 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
SQLRETURN SQLSetDriverConnectInfo(  
                SQLHDBC_INFO_TOKEN   hDbcInfoToken,  
                WCHAR *              InConnectionString,  
                SQLSMALLINT          StringLength1 );  
```  
  
## <a name="arguments"></a>인수  
 *TokenHandle*  
 [입력] 토큰 핸들입니다.  
  
 *InConnectionString*  
 [입력] 전체 연결 문자열 ("설명"의 구문에 나오는 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)), 부분 연결 문자열 또는 빈 문자열입니다.  
  
 *StringLength1*  
 [입력] 길이 **InConnectionString*, 인지 문자열을 유니코드 또는 바이트 문자열은 ANSI 또는 DBCS 문자에서입니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 동일 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 드라이버 관리자를 사용 한다는 점을 제외 하면 모든 입력된 유효성 검사 오류와 관련 된 **HandleType** SQL_HANDLE_DBC_INFO_TOKEN의 및 **처리** 의 *hDbcInfoToken*합니다.  
  
## <a name="remarks"></a>Remarks  
 드라이버는 SQL_ERROR 또는 SQL_INVALID_HANDLE 반환 될 때마다 응용 프로그램에 드라이버 관리자 오류를 반환 합니다 (에서 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 하거나 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 드라이버에서 SQL_SUCCESS_WITH_INFO를 반환할 때마다 드라이버 관리자에서 진단 정보를 가져옵니다 *hDbcInfoToken*, 응용 프로그램에 SQL_SUCCESS_WITH_INFO를 반환 하 고 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)하 고 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)합니다.  
  
 응용 프로그램에서이 함수를 직접 호출 하지 않습니다. 드라이버 인식 연결 풀링을 지 원하는 ODBC 드라이버는이 함수를 구현 해야 합니다.  
  
 ODBC 드라이버 개발을 위한 sqlspi.h 포함 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
