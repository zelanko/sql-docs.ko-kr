---
description: SQLSetDriverConnectInfo 함수
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 21538fa93328790ad8173e5193ba377b0744d964
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461255"
---
# <a name="sqlsetdriverconnectinfo-function"></a>SQLSetDriverConnectInfo 함수
**규칙**  
 소개 된 버전: ODBC 3.81 표준 준수: ODBC  
  
 **요약**  
 **SQLSetDriverConnectInfo** 는 응용 프로그램의 **SQLDriverConnect** 호출에 대 한 연결 정보 토큰에 연결 문자열을 설정 하는 데 사용 됩니다.  
  
## <a name="syntax"></a>구문  
  
```cpp
  
SQLRETURN SQLSetDriverConnectInfo(  
                SQLHDBC_INFO_TOKEN   hDbcInfoToken,  
                WCHAR *              InConnectionString,  
                SQLSMALLINT          StringLength1 );  
```  
  
## <a name="arguments"></a>인수  
 *TokenHandle*  
 입력 토큰 핸들입니다.  
  
 *InConnectionString*  
 입력 전체 연결 문자열 ( [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)의 "Comments" 구문 참조), 부분 연결 문자열 또는 빈 문자열입니다.  
  
 *StringLength1*  
 입력 **Inconnectionstring*의 길이는 문자열이 Unicode 인 경우 문자이 고, 문자열은 ANSI 또는 DBCS 인 경우 바이트입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 SQLDriverConnect SQL_HANDLE_DBC_INFO_TOKEN의 **HandleType** 와 *Hdbcinfotoken*의 **핸들** 을 사용 한다는 점을 제외 하 고는 모든 입력 유효성 검사 오류와 관련 된 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 와 동일 합니다.  
  
## <a name="remarks"></a>설명  
 드라이버가 SQL_ERROR 또는 SQL_INVALID_HANDLE를 반환할 때마다 드라이버 관리자는 오류를 응용 프로그램 ( [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 또는 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md))으로 반환 합니다.  
  
 드라이버가 SQL_SUCCESS_WITH_INFO를 반환할 때마다 드라이버 관리자는 *Hdbcinfotoken*에서 진단 정보를 가져오고 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 및 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)의 응용 프로그램에 SQL_SUCCESS_WITH_INFO을 반환 합니다.  
  
 응용 프로그램은이 함수를 직접 호출 하면 안 됩니다. 드라이버 인식 연결 풀링을 지 원하는 ODBC 드라이버는이 함수를 구현 해야 합니다.  
  
 ODBC 드라이버 개발용으로 sqlspi .h를 포함 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
