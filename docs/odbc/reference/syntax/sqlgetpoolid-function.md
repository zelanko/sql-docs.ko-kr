---
title: SQLGetPoolID 기능 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303320"
---
# <a name="sqlgetpoolid-function"></a>SQLGetPoolID 함수
**규칙**  
 버전 출시: ODBC 3.81 표준 준수: ODBC  
  
 **요약**  
 **SQLGetPoolID는** 풀 ID를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp
  
SQLRETURN  SQLGetPoolID (  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                POOLID *              pPoolID );  
```  
  
## <a name="arguments"></a>인수  
 *hDbcInfo토큰*  
 [입력] 모든 연결 정보를 포함하는 토큰 핸들입니다.  
  
 *pPoolID*  
 [출력] 상호 교환적으로 사용할 수 있는 연결 집합을 식별하는 데 사용되는 풀 ID입니다(추가 재설정이 필요함).  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetPoolID가** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환하면 드라이버 관리자는 **핸들 SQL_HANDLE_DBC_INFO_TOKEN** *및 hDbcInfoToken* **핸들을** 사용합니다.  
  
## <a name="remarks"></a>설명  
 **SQLGetPoolID는** 연결 정보 집합이 주어진 풀 ID를 가져오는 데 **사용됩니다(SQLSetConnectAtTrForDbcInfo,** **SQLSetDriverConnectInfo**및 **SQLSetConnectInfo)에서.).** 이 풀 ID는 상호 교환적으로 사용할 수 있는 연결 집합을 식별하는 데 사용됩니다(추가 재설정이 필요한 경우). 풀 ID는 해당 연결 그룹에 대한 연결 풀을 식별하는 데 사용됩니다.  
  
 드라이버가 SQL_ERROR 또는 SQL_INVALID_HANDLE 반환할 때마다 드라이버 관리자는 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 또는 [SQLDriverConnect에서](../../../odbc/reference/syntax/sqldriverconnect-function.md)응용 프로그램에 오류를 반환합니다.  
  
 드라이버가 SQL_SUCCESS_WITH_INFO 반환할 때마다 드라이버 관리자는 *hDbcInfoToken에서*진단 정보를 얻고 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 및 [SQLDriverConnect에서](../../../odbc/reference/syntax/sqldriverconnect-function.md)응용 프로그램에 SQL_SUCCESS_WITH_INFO 반환합니다.  
  
 응용 프로그램은 이 함수를 직접 호출해서는 안 됩니다. 드라이버 인식 연결 풀링을 지원하는 ODBC 드라이버는 이 기능을 구현해야 합니다.  
  
 ODBC 드라이버 개발을 위해 sqlspi.h를 포함합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
