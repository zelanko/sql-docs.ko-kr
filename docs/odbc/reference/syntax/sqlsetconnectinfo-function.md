---
description: SQLSetConnectInfo 함수
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0ee3480678d228e26b16cc99e7df8955d45ade9e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499548"
---
# <a name="sqlsetconnectinfo-function"></a>SQLSetConnectInfo 함수
**규칙**  
 소개 된 버전: ODBC 3.81 표준 준수: ODBC  
  
 **요약**  
 **SQLSetConnectInfo** 는 응용 프로그램의 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 호출에 대 한 연결 정보 토큰으로 데이터 원본, 사용자 ID 및 암호를 설정 하는 데 사용 됩니다.  
  
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
 입력 토큰 핸들입니다.  
  
 *데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면*  
 입력 데이터 원본 이름입니다. 데이터는 프로그램과 동일한 컴퓨터 또는 네트워크의 다른 컴퓨터에 있을 수 있습니다. 응용 프로그램에서 데이터 원본을 선택 하는 방법에 대 한 자세한 내용은 [데이터 원본 또는 드라이버 선택](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)을 참조 하십시오.  
  
 *NameLength1*  
 입력 **ServerName* 의 길이 (문자)입니다.  
  
 *UserName*  
 입력 사용자 식별자입니다.  
  
 *NameLength2*  
 입력 **UserName* 의 길이 (문자)입니다.  
  
 *인증*  
 입력 인증 문자열 (일반적으로 암호)입니다.  
  
 *NameLength3*  
 입력 문자에서 **인증* 의 길이입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 입력 유효성 검사 오류에 대 한 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 와 동일 합니다. 단, 드라이버 관리자는 **HandleType** 의 SQL_HANDLE_DBC_INFO_TOKEN 및 *Hdbcinfotoken*의 **핸들** 을 사용 합니다.  
  
## <a name="remarks"></a>설명  
 드라이버가 SQL_ERROR 또는 SQL_INVALID_HANDLE를 반환할 때마다 드라이버 관리자는 오류를 응용 프로그램 ( [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 또는 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md))으로 반환 합니다.  
  
 드라이버가 SQL_SUCCESS_WITH_INFO를 반환할 때마다 드라이버 관리자는 *Hdbcinfotoken*에서 진단 정보를 가져오고 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 및 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)의 응용 프로그램에 SQL_SUCCESS_WITH_INFO을 반환 합니다.  
  
 응용 프로그램은이 함수를 직접 호출 하면 안 됩니다. 드라이버 인식 연결 풀링을 지 원하는 ODBC 드라이버는이 함수를 구현 해야 합니다.  
  
 ODBC 드라이버 개발용으로 sqlspi .h를 포함 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
