---
title: SQLGetPoolID 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetPoolID function [ODBC]
ms.assetid: 95a8666a-ad68-4d89-bf65-f2cc797f8820
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 32cc973f4dab5bde7bcedade0365d233987dda72
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303320"
---
# <a name="sqlgetpoolid-function"></a>SQLGetPoolID 함수
**규칙**  
 소개 된 버전: ODBC 3.81 표준 준수: ODBC  
  
 **요약**  
 **SQLGetPoolID** 는 풀 ID를 검색 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp
  
SQLRETURN  SQLGetPoolID (  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                POOLID *              pPoolID );  
```  
  
## <a name="arguments"></a>인수  
 *hDbcInfoToken*  
 입력 모든 연결 정보를 포함 하는 토큰 핸들입니다.  
  
 *pPoolID*  
 출력 풀 ID는 서로 바꿔 사용할 수 있는 연결 집합을 식별 하는 데 사용 됩니다 (추가 재설정을 요구할 수도 있음).  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetPoolID** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 드라이버 관리자는 **HandleType** SQL_HANDLE_DBC_INFO_TOKEN의 및 *Hdbcinfotoken*의 **핸들** 을 사용 합니다.  
  
## <a name="remarks"></a>설명  
 **SQLGetPoolID** 는 **SQLSetConnectAttrForDbcInfo**, **SQLSetDriverConnectInfo**및 **SQLSetConnectInfo**에서 연결 정보 집합이 제공 된 풀 ID를 가져오는 데 사용 됩니다. 이 풀 ID는 서로 바꿔 사용할 수 있는 연결 집합을 식별 하는 데 사용 됩니다 (추가 재설정을 요구할 수 있음). 풀 ID는 해당 연결 그룹에 대 한 연결 풀을 식별 하는 데 사용 됩니다.  
  
 드라이버가 SQL_ERROR 또는 SQL_INVALID_HANDLE를 반환할 때마다 드라이버 관리자는 오류를 응용 프로그램 ( [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 또는 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md))으로 반환 합니다.  
  
 드라이버가 SQL_SUCCESS_WITH_INFO를 반환할 때마다 드라이버 관리자는 *Hdbcinfotoken*에서 진단 정보를 가져오고 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 및 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)의 응용 프로그램에 SQL_SUCCESS_WITH_INFO을 반환 합니다.  
  
 응용 프로그램은이 함수를 직접 호출 하면 안 됩니다. 드라이버 인식 연결 풀링을 지 원하는 ODBC 드라이버는이 함수를 구현 해야 합니다.  
  
 ODBC 드라이버 개발용으로 sqlspi .h를 포함 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
